---
layout: post
title:  "0508-[Project]-Baduk"
subtitle:   "0508-Baduk"
categories: devlog
tags: project

---
## Baduk

<hr style="height: 1px; background: skyblue; "/>

#### Baduk

~~~

//================================================
//	바둑알 하나에 대한 정보를 저장하는 클래스
//================================================

public class Baduk implements java.io.Serializable
{  

	public static int			BLACK_BADUK = 0;
	public static int      		WHITE_BADUK = 1;
	public static int      		NONE_BADUK = -1;

    int row;
    int col;
    int color;

    public Baduk(){
      this(0,0,0);
    }
    public Baduk(int color, int row, int col ){
      this.row = row;
      this.col = col;
      this.color = color;
    }

    public int getRow(){
      return row;
    }
    public int getCol(){
      return col;
    }
    public int getColor(){
      return color;
    }
    public void setValue(int row, int col, int color){
      this.row = row;
      this.col = col;
      this.color = color;
    }
}

~~~

<hr style="height: 1px; background: skyblue"/>

#### BadukClient

~~~

//=====================================================
//	 서버에 연결하여 클라이언트의 이벤트 및 메세지를 받아
//	서버에 전송하고 서버에서 보내는 데이타를 받아
//  화면에 표시해주는 클래스
//=====================================================

import java.awt.*;
import javax.swing.*;
import java.awt.event.*;
import java.net.*;
import java.io.*;
import java.util.*;

class  BadukClient extends JPanel implements ActionListener, Runnable
{
	// 생성자 기본 인자
	String serverIP;
	String id;

	// 화면 구성에 관련된 멤버 변수
	MyCanvas	canvas;
	JButton		btnStop, btnGame;

	JTextField	tfBlackRock, tfWhiteRock, tfOrder, tfWinner;

	JComboBox	comMember;
	JTextArea	taChatting;
	JTextField	tfMessage;

	// 네트워크 연결에 관련된 멤버 변수
	Socket		socClient;
	ObjectInputStream	inStream;
	ObjectOutputStream	outStream;

	final static int	PORT=7777;

	Thread		thread;

	// 게임정보에 관련된 멤버 변수
	Vector		badukRock;	// 바둑알정보(Rock)를 저장할 벡터
	boolean		bGamming;


	//==================================================
	/* ClientBadukMain 실행시 도스에서 입력값으로 서버IP와 사용자아이디 지정
	   인자값이 없는 경우는 127.0.0.1 서버에 guest 아이디 지정
	*/
	BadukClient(){
		this( "127.0.0.1", "guest" );
	}

	BadukClient(String serverIP, String id){
		this.serverIP = serverIP;
		this.id		= id;

		createGUI();		// 화면출력 UI 완성

		connectServer();	// 서버에 연결하기
	}

	//=================================================
	/* 화면을 완성하는 GUI 구성하기
		- 화면 관련 멤버 변수의 객체를 생성
		- JPanel에 layout에 맞게 붙이기
	*/
	void createGUI(){
//<- 1
		// West 영역 완성
		tfBlackRock	= new JTextField(10);
		tfWhiteRock	= new JTextField(10);
		tfOrder		= new JTextField(10);
		tfWinner	= new JTextField(10);
		JLabel lBlackRock	= new JLabel(" 흑기사 ");
		JLabel lWhiteRock	= new JLabel(" 백기사 ");		
		JLabel lOrder		= new JLabel(" 순  번 ");
		JLabel lWinner		= new JLabel(" 승  리 ");

		JPanel p_west	= new JPanel();
		p_west.setLayout( new GridLayout( 14, 1 ) );
		p_west.add( lBlackRock );
		p_west.add( tfBlackRock );
		p_west.add( lWhiteRock );
		p_west.add( tfWhiteRock );
		p_west.add( lOrder );
		p_west.add( tfOrder );
		p_west.add( lWinner );
		p_west.add( tfWinner );


		//	East 영역 완성
		comMember	= new JComboBox();
		taChatting	= new JTextArea(40,15);
		tfMessage	= new JTextField(15);
		JPanel p_east = new JPanel();
		p_east.setLayout( new BorderLayout( 10, 10 ) );
			JPanel p_east_up = new JPanel();
			JLabel lMember	= new JLabel(" 접속자 " );
			p_east_up.add( lMember );
			p_east_up.add( comMember );		
			//** TextArea의 내용이 많이지만 스크롤바 생기도록
			JScrollPane sp = new JScrollPane(taChatting);
		p_east.add("North", p_east_up );
		p_east.add("Center",  sp);
		p_east.add("South", tfMessage );


		//	South 영역 완성
		btnStop	= new JButton(" 그만하기 ");
		btnGame	= new JButton(" 게임하기 ");

		JPanel p_south = new JPanel();
		p_south.setLayout( new GridLayout( 1, 3 ) );
		p_south.add( btnGame );
		p_south.add( btnStop );

		//	Center 영역 완성
		canvas	= new MyCanvas();


		// 전체 클래스에 부분완성된 영역 붙이기
		setLayout( new BorderLayout() );
		add("West", p_west );
		add("East", p_east );
		add("South", p_south );
		add("Center", canvas );
//-> 1

//<- 2
		// 이벤트 등록
		tfMessage.addActionListener( this );
		btnGame.addActionListener( this );
		btnStop.addActionListener( this );
	}

	//==================================================
	/*	소켓클래스로 서버에 연결
		1. 소켓클래스 생성 ( serverIP, port번호 )
		2. 생성된 소켓객체의 입력/출력 스트림 얻어오기
	*/
	void connectServer(){
		try{
//<- 2
			socClient	= new Socket( serverIP, PORT );
			inStream	= new ObjectInputStream( socClient.getInputStream() );
			outStream	= new ObjectOutputStream( socClient.getOutputStream() );

			// => 서버로부터 데이타 읽기 위해 쓰레드 구현
			thread		= new Thread( this );
			thread.start();

//-> 3		//	=> 접속후 아이디를 서버에 전송
			sendId();

		} catch(Exception ex){
			JOptionPane.showMessageDialog(null, "서버 연결 실패 :"+ ex.getMessage() );
		}
	}

//<- 2
	//====================================================
	/*	서버에서 데이타를 보내는 데이타 읽기
		0. 반복문
		1. 소켓의 입력스트림으로 BadukServerProtocol 객체 읽어오기
		2. 1의 객체에서 상태값과 데이타 얻어오기
		3. 상태값에 따라 각각의 구현 함수 호출
	*/
	public void run(){
		while( socClient != null ){
			try{
				BadukServerProtocol obj = (BadukServerProtocol)inStream.readObject();
				int state	= obj.getState();
				Object data	= obj.getData();
				switch( state ){
					// 챗팅메세지를 받은 경우
					case BadukServerProtocol.Chatting :
						setChatting( data ); break;
//<-- 3				// 멤버가 추가된 경우 멤버아이디들를 받은 경우
					case BadukServerProtocol.CHANGE_MEMBER_ID :
						addMemberId( data ); break;

//<-- 4				// 게임신청자 데이타를 받은 경우
					case BadukServerProtocol.SET_BADUK_GAMMER :
						setBadukGammer( data ); break;

//<-- 5				// 게임시작됨을 알리는 데이타 받은 경우
					case BadukServerProtocol.START_GAME :
						startGameConfirm( ); break;

//<-- 6				// 놓여진 바둑알에 대한 데이타 받은 경우
					case BadukServerProtocol.SET_BADUK_ROCK :
						setBakukRock( data ); break;

//<-- 7				// 게임이 종료됨을 알리는 데이타 받은 경우
					case BadukServerProtocol.END_GAME :
						endGame( data ); break;
				}
			}catch(Exception ex){
			}
		}
	}


	public void actionPerformed(ActionEvent ev){
		Object o = ev.getSource();

	 	// 챗메세지 텍스트필드에서 엔터 이벤트 발생시
		if( o == tfMessage )	chatMessageSend();

//<-- 4
		// "게임하기" 버튼을 눌렸을때
		else if( o == btnGame ) startGame();


	}


	//==================================================
	/*	클라이언트에서 서버로 전송할 데이타클래스 생성하고,
		텍스트필드에 입력한 값 얻어서 지정후 서버로 전송
		1. 메세지입력 텍스트필드에서 입력값 얻어오기
		2. 공백인지 확인후 공백이면 리턴
		3. 클라이언트에서 서버로 전송 데이타 객체 생성
			( BadukClientProtocol )
		4. 3번 객체에 상태와 데이타 지정
		5. 서버로 전송 ( 소켓의 출력스트림에 write )
		6. 텍스트필드를 초기화하고 포커스 지정
	*/
	void chatMessageSend(){
		String msg = tfMessage.getText();
		if( msg.equals("")) return;
		BadukClientProtocol obj	= new BadukClientProtocol();
		obj.setState( BadukClientProtocol.Chatting);
		obj.setData( msg );
		sendInformation(obj);

		// 데이타 전송후 텍스트필드 지우고 포커스 맞추기
		tfMessage.setText("");
		tfMessage.requestFocus();
	}

	void sendInformation( BadukClientProtocol obj ){
		try{
			outStream.writeObject( obj );
		}catch(Exception ex){
			JOptionPane.showMessageDialog(null, "메세지 전송 실패 :"+ ex.getMessage() );
		}
	}

	void setChatting( Object data ){
		taChatting.append( (String)data + "\n");

		//**  ScrollBar를 밑으로 자동으로 내리도록
		//**
		taChatting.setCaretPosition( taChatting.getText().lastIndexOf("\n") + 1 );
	}

//-> 2

//<-- 3
	//----------------------------------------------------
	/*	서버에 접속후 입력한 아이디를 서버에 전송
		1. 클라이언트에서 서버로 전송 데이타 객체 생성
			( BadukClientProtocol )
		2. 1번 객체에 state는 BadukClientProtocol.SEND_ID로 지정
		3. 1번 객체에 data는 입력받은 id로 지정
		4. 서버로 전송 ( 소켓의 출력스트림에 write )
			: sendInformation() 이용
	*/
	void sendId(){
		BadukClientProtocol obj	= new BadukClientProtocol();
		obj.setState( BadukClientProtocol.SEND_ID);
		obj.setData( id );
		sendInformation(obj);

	}

	//---------------------------------------------------
	/*	넘겨받은 아이디값들을 콤보박스에 추가
		1. 넘겨받은 객체를 다시 String[]로 형변환
		2. 기존의 콤보박스의 내용들 모두 지움
		3. String[] 배열값을 콤보박스에 하나씩 추가
	*/
	void addMemberId( Object data ){
		String ids[] = (String [])data;
		comMember.removeAllItems();  // removeAll() 는 AWT 메소드라 안됨
		for( int i=0; i< ids.length; i++){
			comMember.addItem( ids[i] );
		}
	}

	//---------------------------------------------------
	// 과제 클라이언트가 종료하고 나갈때 서버에 알린후 소켓 닫기
	void sendExit(){
		BadukClientProtocol obj	= new BadukClientProtocol();
		obj.setState( BadukClientProtocol.EXIT);
		obj.setData( id );
		sendInformation(obj);
		try{
		inStream.close();
		outStream.close();
		socClient.close();
		}catch(Exception ex){}
	}

//--> 3


//<-- 4
	//---------------------------------------------------
	/*	"게임하기", "구경하기" 버튼 클릭시 서버에 전송
		1. 클라이언트에서 서버로 전송 데이타 객체 생성
			( BadukClientProtocol )
		2. 1번 객체에 state는 넘겨받은 상태값으로 지정
		3. 서버로 전송 ( 소켓의 출력스트림에 write )
			: sendInformation() 이용
		4. "게임하기" 버튼을 한번 누르면 비활성화
	*/
	void startGame(){
		//if( socClient == null ) connectServer();
		BadukClientProtocol obj = new BadukClientProtocol();
		obj.setState(  BadukClientProtocol.REQUEST_GAME );
		sendInformation( obj );
		btnGame.setEnabled( false );
	}

	//--------------------------------------------------
	/*	1. 넙겨받은 데이타(BadukServerProtocol의 data임)를 벡터로 변환
		2. 벡터의 0번째 요소( 흑돌 게임자의 아이디 )를 얻어 흑돌게임자 텍스트필드에 지정
		3. 벡터의 1번째 요소( 흰돌 게임자의 아이디 )를 얻어 흰돌게임자 텍스트필드에 지정
	*/
	void setBadukGammer( Object data ){
		Vector gammers = (Vector) data;
		tfBlackRock.setText( (String)gammers.get(0) );
		tfWhiteRock.setText( (String)gammers.get(1) );
	}
//--> 4


//<-- 5
	//--------------------------------------------------
	/*	게임시작시 초기화 작업
		1. 바둑알정보(Rock 클래스)을 저장할 벡터변수(badukRock) 객체 생성
		2. 게임이 시작됨을 지정할 변수(bGamming)을 true로 초기화
		3. 승리자 텍스트필드 초기화
		4. 바둑판 캔버스 초기화
	 */
	void startGameConfirm(){
		badukRock	= new Vector();
		bGamming	= true;
		tfWinner.setText("");
		canvas.repaint();
	}

	//--------------------------------------------------
	/* 마우스 클릭한 위치에 대한 바둑알의 정보를 서버에 전송
		1. 인자로 넘어온 값을 벡터에 저장
		2. 서버에 전송
			- BadukClientProtocol 객체 생성
			- state에 BadukClientProtocol.SET_BADUK_ROCK로 지정
			- data에 1번 객체
			- BadukClientProtocol 객체 서버로 전송
	 */
	void sendSetBaduk( int row, int col ){
		Vector v = new Vector();
		v.add( new Integer(row) );
		v.add( new Integer(col) );

		BadukClientProtocol	obj = new BadukClientProtocol();
		obj.setState( BadukClientProtocol.SET_BADUK_ROCK );
		obj.setData( v );
		sendInformation( obj );
	}
//--> 5

//<-- 6
	//-----------------------------------------------------
	/* 서버로부터 놓여진 바둑돌의 위치정보를 받았을때
		1. 넘겨받은 객체를 Baduk클래스로 형변환
		2. Baduk객체에서 색상을 얻어서 흑인지 비교후 순서를 백으로 지정
		3. 아니면 흑으로 지정
		4. Baduk객체를 바둑돌을 저장하는 벡터(badukRock)에 추가
		5. 캔버스를 다시 그리기
	 */
	void setBakukRock( Object data ){
		Baduk al = (Baduk)data;

		if( al.getColor() == Baduk.BLACK_BADUK )
			tfOrder.setText(" 백 ");
		else
			tfOrder.setText(" 흑 ");

		badukRock.add( al );
		canvas.repaint();

	}


//<-- 7
	//------------------------------------------------
	/* 게임승리자를 출력하고 모든 화면 초기화
		1. 게임진행중을 확인하는 boolean 변수(bGamming)에 false 지정
		2. 넘겨받은 데이타값을 승리자 텍스트필드에 출력
		3. "게임하기"버튼을 활성화
	 */
	void endGame( Object data ){
		bGamming = false;
		String winner = (String) data;
		//tfWinner.setText( winner );
		JOptionPane.showMessageDialog(null, winner + "님께서 승리하셨습니다!!");
		btnGame.setEnabled( true );
		tfBlackRock.setText("");
		tfWhiteRock.setText("");
		tfOrder.setText("");
		tfWinner.setText("");
	}



	//###################################################
	/* 바둑판 모양을 만든 Canvas
	*/
	class MyCanvas extends Canvas
	{
		int term;			// 한칸의 길이
		Point ptS, ptE;		// 바둑판의 시작점과 끝점좌표

		//----------------------------------------------
		/* Canvas의 그림 그리는 역할을 하는 paint() overriding
		*/
		public void paint(Graphics g){
			// 캔버스의 폭과 높이를 구하여 정사각형의 폭과 높이로 계산
			int w = getWidth();
			int h = getHeight();
			if( w > h ) w = h;
			else if( w < h ) h =w;

			// 4면의 여백
			int margin = 20;

			// 바둑 한칸의 길이
			term = w / 18;

			// 시작좌표와 끝좌표 지정
			ptS = new Point( margin, margin );
			ptE = new Point( w - margin, h - margin );

			// 바둑판 글 긋기
			for( int i=0; i < 19 ; i++){
				g.drawLine( ptS.x, ptS.y + term*i , ptE.x,  ptS.y + term*i );
				g.drawLine( ptS.x + term*i, ptS.y, ptS.x + term*i, ptE.y );
			}

			//!!!!!!!! 여기는 나중에 참고
			//^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
			// 서버로 넘어온 바둑알정보를 저장하는 벡터에 데이타가 있다면
			// 벡터의 각각 바둑알정보(Rock 클래스)을 얻어 row,column,color 값을 얻어와서
			// 화면에 그 정보로 원 그리기
			int x = 0, y = 0, c = 0;	// 바둑알의  x좌표, y좌표, 색상을 저장할 변수
			int r = term / 2;			// 바둑알의 반지름을 저장할 변수
			if(	badukRock != null ){				
				for( int i =0; i< badukRock.size(); i++){
					Baduk	al = (Baduk)badukRock.get(i);
					x = al.getCol();
					y = al.getRow();
					c = al.getColor();

					if( c == Baduk.BLACK_BADUK )	g.setColor(Color.black);
					else	g.setColor( Color.yellow );

					g.fillArc( ptS.x + x*term-r, ptS.y + y*term-r, term, term, 0, 360 );
				}
				// 마지막바둑알에는 빨간 사각표시
				g.setColor( Color.red );
				g.drawRect( ptS.x + x*term-r, ptS.y + y*term-r, term, term );
			}

		}


		//----------------------------------------------
		/* 생성자 함수
		 */
		MyCanvas(){
//<-- 6
			// 바둑판에서 마우스 클릭시 서버에 데이타 전송
			/*	1. 눌려진 좌표값 얻어오기
				2. 1번에서 x값이 바둑판의 몇번째 세로줄인지 지정
					( getXValue() 이용 )
				3. 1번에서 y값이 바둑판의 몇번째 가로줄인지 지정
					( getYValue() 이용 )
				4. 서버에 전송하기 위해 sendSetBaduk() 호출
			 */
			addMouseListener( new MouseAdapter(){
				public void mouseReleased( MouseEvent ev ){
					Point pt = ev.getPoint();
					int col = getXValue( pt.x );
					int row = getYValue( pt.y );

					if( bGamming ){
						if( row < 0 || row > 18 || col < 0 || col > 18 )
							return;
						sendSetBaduk( row, col);
					}

				}
			});
//--> 6
		}


		//^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
		// 클릭한 x좌표값을 바둑판에서의 column 값으로 변경
		int getXValue( int x ){
			x -= ptS.x;
			int v = x / term;
			int r = x % term;
			if( r > term /2 ) v++;
			return v;
		}
		//^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
		// 클릭한 x좌표값을 바둑판에서의 column 값으로 변경
		int getYValue( int y ){
			y -= ptS.y;
			int v = y / term;
			int r = y % term;
			if( r > term /2 ) v++;
			return v;
		}
	};
}


~~~

<hr style="height: 1px; background: skyblue"/>

#### BadukClientMain

~~~

//====================================================
//	클라이언트 프로그램을 실행하는 클래스
//	( main() 포함 )
//====================================================

import javax.swing.*;
import java.awt.event.*;


public class BadukClientMain extends JFrame
{
	BadukClient			badukClient;       

	public BadukClientMain(String server, String id){
		badukClient = new BadukClient(server, id);
		getContentPane(). add(badukClient);
		//setDefaultCloseOperation( JFrame.EXIT_ON_CLOSE );


//--> 3
		// 종료시 서버에 나감을 알림
		addWindowListener( new WindowAdapter(){
			public void windowClosing( WindowEvent ev){
				badukClient.sendExit();
				System.exit(0);
			}
		});
	}
	public static void main(String[] args){
		BadukClientMain main = new BadukClientMain(args[0], args[1]);
		main.setSize(880,660);
		main.setVisible(true);
	}
}






~~~

<hr style="height: 1px; background: skyblue"/>

#### BadukClientProtocol

~~~

//=============================================================
//	클라이언트에서 서버로 전송할  데이타를 캡슐화한 클래스
//=============================================================

public class BadukClientProtocol implements java.io.Serializable
{
	//---------------------------------------------
	// 클라이언트에서 서버로 전송시 상태값

    public static final int			Chatting    =  200;	// 챗팅메세지
	public static final int			SEND_ID		=  300; // 처음 접속시 아이디
	public static final int			EXIT		=  400; // 접속을 끊을때

	public static final int			REQUEST_GAME =  0;
	public static final int			VIEW_GAME    =  1;


    public static final int			SET_BADUK_ROCK    =  11;

	Object 						 data;
	int                          state;

	public BadukClientProtocol(){
	}
	public void setData(Object obj){
		data = obj;		
	}
	public void setState(int s){
		state = s;
	}
	public Object getData(){
		return data;
	}
	public int getState(){
		return state;
	}

}

~~~

<hr style="height: 1px; background: skyblue"/>

#### BadukServer

~~~

//===================================================================
//	서버 프로그램을 시작하는 클래스
//	클라이언트가 요청한 결과를 구현한 클래스
//===================================================================
import java.io.*;
import java.util.*;
import java.net.*;
import java.awt.*;
import java.awt.event.*;


public class BadukServer  implements Runnable
{
  Vector 				member;		// 클라이언트접속시 정보 저장할 벡터
  ServerSocket 			server;
  Thread 				serverThread;
  int                 	serverPort = 7777;

	// 게임에 관한 멤버 변수
	BadukService	blackClient;	// 흑돌게임 클라이언트
	BadukService	whiteClient;	// 흰돌게임 클라이언트
	BadukService	currentClient;	// 현재차례 클라이언트
	Vector			badukRock;		// 바둑알정보를 저장할 벡터
	int				badukPan[][];	// 바둑판 위치 저장
	String			winner;			// 이긴사람의 아이디 저장

  //--------------------------------------------------------
  /*	생성자 함수
	1. ServerSocket 객체 생성
	2. 벡터 객체 생성
	3. 클라이언트 접속을 기다리기 위해 쓰레드 구현
  */
  public BadukServer(){
    try{
       server = new ServerSocket(serverPort);
    }catch(Exception e){
	    //System.out.println(e);
    }
    member = new Vector();

    serverThread = new Thread(this);
    serverThread.start();
  }

  //--------------------------------------------------------
  /* 쓰레드 구현
	1. ServerSocket의 accept() 함수로 클라이언트 접속 대기
	2. 접속한 클라이언트와 소켓을 주고받을 역할을 하는 클래스 생성
		( BadukService )
	3. 2의 객체를 벡터에 추가
  */
  public void run(){
      try{
			System.out.println("서버 구동 시작 !!!  ");    			
    		while(true) {
				Socket s = server.accept();
				BadukService cs = new BadukService(this, s );
				member.addElement(cs);
				System.out.println("Client 접속 : " + cs);    			
    		}
      }catch(Exception e){

      }
  }

  //-------------------------------------------------------
  /* 각 클라이언트와 데이타 전송을 담당하는 BadukService객체에서
    한 클라이언트에서 데이타를 읽었으면 모든 멤버에게 전송
  */  
  public synchronized void setChatting(Object data){
		BadukServerProtocol  p = new BadukServerProtocol();
		p.setState(BadukServerProtocol.Chatting);
		p.setData(data);
		broadcast(p);
	}

  public  synchronized void broadcast(BadukServerProtocol obj){
  		for ( int i = 0; i < member.size() ; i++ ){
  				BadukService client = (BadukService)member.get(i);
  				client.sendInformation(obj);
  		}
  }

//@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
//<-- 3
   //-------------------------------------------------------
   /*	Vector의 요소인 BadukService를 얻어서 각각의 아이디를 얻어
		String 배열에 추가후 각각 클라이언트에 전송
		1. Vector의 크기만큼 String 배열을 생성
		2. 배열에서 하나씩 요소(BadukService)를 얻기
		3. 얻은 각 BadukService의 id값을 String 배열에 추가
		4. 클라이언트로 전송할 객체 생성 ( BadukServerProtocol )
		5. 4번 객체의 state값을 BadukServerProtocol.CHANGE_MEMBER_ID로 지정
		6. 4번 객체의 data값을 위의 String배열로 지정
		7. 모든 클라이언트에 전송 ( boaadcast() 이용 )
	*/
   public synchronized void sendAddMember(){
		String[] str = new String[member.size()];
		for ( int i = 0; i < str.length; i++ ){
			BadukService client = (BadukService) member.get(i);
			str[i] = new String(client.getID());
		}
		BadukServerProtocol  p = new BadukServerProtocol();
		p.setState(BadukServerProtocol.CHANGE_MEMBER_ID);
		p.setData(str);
		broadcast(p);

  }

  // 종료시
  /* 나가는 접속자의 아이디를 인자로 받아 같은 아이디를 가지고 있는 BadukService를 찾아
    벡터에서 제거
	1. 벡터의 크기만큼 반복문 구동하여 요소(BadukService)를 하나씩 얻어온다
	2. 인자로 받은 아이디와 같은 아이디 있는지 비교하여
	3. 벡터에서 그 요소를 제거
	4. 다른 클라이언트에게 전송 sendAddMember(); 호출
   */
  void sendRemoveMember( String removeId ){
		for ( int i = 0; i < member.size() ; i++ ){
			BadukService client = (BadukService) member.get(i);
			if( removeId.equals(client.getID()) ){
				System.out.println( removeId +" 나간다~!!");
				member.removeElementAt( i );
				// 다른 클라이언트에게 알리기 위해
				sendAddMember();
			}
		}		
  }

//<-- 4
  //------------------------------------------------------
  /* 처음에 신청한 게임자는 흑돌로 지정하고, 그다음에 신청한
	게임자는 흰돌로 지정한후 게임을 시작한다
	1. 흑돌 게임자 변수( blackClient )가 null 이라면 첫번째 게임자이므로
		인자로 넘어온 BadukService객체를 흑돌게임머 변수로 지정
	2. 흑돌 게임자 아이디를 모든 클라이언트에 전송
		sendBadukGammer()를 이용하여 모든 클라이언트에 전송
	3. 흰돌 게임자 변수( whiteClient )가 null 이라면 두번째 게임자이므로
		인자로 넘어온 BadukService객체를 흰돌게임머 변수로 지정
	4. 흰돌 게임자 아이디를 모든 클라이언트에 전송
		sendBadukGammer()를 이용하여 모든 클라이언트에 전송
   */
  public synchronized void requestGame(BadukService c){
  	   	if (  blackClient == null ){
  	   		blackClient = c;
		   	BadukServerProtocol  p = sendBadukGammer();
			broadcast(p);			
  	   	}
  	   	else if ( whiteClient == null ){
	  		whiteClient = c;
  		   	BadukServerProtocol  p = sendBadukGammer();
			broadcast(p);

//<-- 5		// 게임시작
			startGame();
  	   	}
   }


  //####################################################
  //----------------------------------------------------
  /* 흑돌게임자의 아이디와 흰돌게임자의 아이디를 얻어
	벡터에 저장하고나서 모든 클라이언트에 전송
	( BadukServerProtocol 객체로 전송하고자 )
   */
  public synchronized BadukServerProtocol sendBadukGammer(){
		String blackID = "";
		if ( blackClient != null )
		   blackID = blackClient.getID();
		String whiteID = "";
		if ( whiteClient != null )
			whiteID = whiteClient.getID();
		Vector v = new Vector();
		v.addElement(blackID);
		v.addElement(whiteID);
		BadukServerProtocol  p = new BadukServerProtocol();
		p.setState(BadukServerProtocol.SET_BADUK_GAMMER);
		p.setData(v);
		return p;
  }

  //-------------------------------------------------
  /* 게임을 시작하면 흑돌 먼저 순서로 지정하고 바둑알 저장할 벡터 생성하고
	바둑판정보 저장할 변수 초기화 한 후	모든 클라이언트에게 게임시작임을 전송
   */
  public synchronized void startGame(){
		currentClient = blackClient;
  		badukRock = new Vector(5, 5);
  		badukPan = new int[19][19];
  		for ( int i = 0; i < 19; i++ )
  			for ( int j = 0; j < 19; j++ )
  				badukPan[i][j] = Baduk.NONE_BADUK;
		BadukServerProtocol  p2 = new BadukServerProtocol();
		p2.setState(BadukServerProtocol.START_GAME);
		broadcast(p2);
  }
//--> 4


//<-- 6
//------------------------------------------------------------
/*  1. 클릭한 접속자가 현재게임자가 아니라면 리턴
	2. 넘겨받은 Object 인자에서 x,y좌표 얻어오기
	3. 흑돌게임자라면 흑색을 흰돌게임자라면 흰색을 지정
	4. 2번과 3번의 데이타 ( x값, y값, 색상)을 Baduk 객체에 저장
	5. 4번의 Baduk객체를 바둑알정보를 저장하는 벡터(badukRock)에 추가 저장
	6. 모든 클라이언트에 SET_BADUK_ROCK 상태에 5번 객체를 전송
 */
  public synchronized void sendBadukRock(BadukService c, Object obj){
		if ( currentClient != c ) return;


		Vector v = (Vector)obj;
   		int row = ((Integer)v.get(0)).intValue();
   		int col = ((Integer)v.get(1)).intValue();

		int color = Baduk.BLACK_BADUK;
  	    if ( c == whiteClient )
  	   	  color = Baduk.WHITE_BADUK;

  	   Baduk al = new Baduk( color, row, col);
  	   badukRock.add(al);

  	   	BadukServerProtocol  p = new BadukServerProtocol();
		p.setState(BadukServerProtocol.SET_BADUK_ROCK);
		p.setData(al);
  		broadcast(p);

  	   //------------------------------------------------------------
 	   //  2. 오목 확인 체크하기
 	   badukPan[row][col] = color;
 	   // isGame(b);

   		if  ( isGame(al) ){
 			// 승패가 결정되면 게임종료하기
   			gameEnd();
   			return;
   		}


		//------------------------------------------------------------
		//  1. 순서를 바꾸기 ( 흑-> 백, 백 -> 흑 )
  	   	if ( 	currentClient == blackClient )
  	   	   currentClient = 	whiteClient;
  	   	else
  	   	   currentClient = 	blackClient;



  }

	//##################################################################
	/*  가장 최근에 놓여진 바둑알 정보를 기점으로 상하좌우대각선 방향으로
	  동일한 색의 바둑알이 5개 있는지 확인
	 */
     public  synchronized boolean isGame(Baduk curBaduk)
   {
		boolean bend = false;
		int row = curBaduk.getRow();
		int col = curBaduk.getCol();
		int color = curBaduk.getColor();
		int number = 0;
		winner = currentClient.getID();
		number += getSerialNumber(row, col, color, -1, 0 );//Up
		if ( number >= 5 )
			return true;
		number += getSerialNumber(row+1, col, color, 1, 0 );//Down
		if ( number >= 5 )
			return true;
		number = getSerialNumber(row, col, color, 0, -1);//Left
		if ( number >= 5 )
			return true;
		number += getSerialNumber(row, col+1, color, 0, 1);//Right
		if ( number >= 5 )
			return true;
		number = getSerialNumber(row, col, color, -1, -1 );//left , Up
		if ( number >= 5 )
			return true;
		number += getSerialNumber(row+1, col+1, color, 1, 1 );//right, down
		if ( number >= 5 )
			return true;
		number = getSerialNumber(row, col, color, -1, 1 );//right, up
		if ( number >= 5 )
			return true;
		number += getSerialNumber(row+1, col-1, color, 1, -1 );//left , Down
		if ( number >= 5 )
			return true;
	   winner = "무승부";
		return false;
   }

   public synchronized int getSerialNumber(int row, int col, int color, int rInc, int cInc){
   		int n = 0;

   		while(true){
   			if ( row < 0 || row > 18 || col < 0 || col > 18 )
   				break;
   			if ( badukPan[row][col] != color )
   				break;
   			row += rInc;
   			col += cInc;
   			n++;
   		}
   		return n;
   }


   //------------------------------------------------------------
   /* 클라이언트에게 게임이 끝났음을 전송
	*/
   public synchronized void gameEnd(){
	    reStartInit();
  	   	BadukServerProtocol  p = new BadukServerProtocol();
		p.setState(BadukServerProtocol.END_GAME);
		p.setData(winner);
  		broadcast(p);
  }

  public synchronized void reStartInit(){
		currentClient	= null;
		whiteClient		= null;
		blackClient		= null;
		badukRock		= null;
		badukPan		= null;
  }


   public static void main(String[] arg) {
   		BadukServer cs = new BadukServer();
   }
}

~~~

<hr style="height: 1px; background: skyblue"/>

#### BadukServerProtocol

~~~

//=============================================================
//	서버에서 클라이언트로 전송할  데이타를 캡슐화한 클래스
//=============================================================

public class BadukServerProtocol implements java.io.Serializable
{
	// 서버에서 클라이언트로 전송시 상태값

	public static final int		Chatting		 = 200; // 채팅메세지
	public static final int		CHANGE_MEMBER_ID = 100; 	// 멤버 아이디 변경시
	public static final int		SET_BADUK_GAMMER = 300; // 게임자 지정시

	public static final int		START_GAME		 =  10; // 게임 시작시
	public static final int		END_GAME		 =  20; // 게임 종료시
	public static final int		SET_BADUK_ROCK   =  30; // 바둑알이 놓여졌을때


	Object 						data;
	int                          state;
	public BadukServerProtocol(){

	}
	public void setData(Object obj){
		data = obj;		
	}
	public void setState(int s){
		state = s;
	}
	public Object getData(){
		return data;
	}
	public int getState(){
		return state;
	}

}

~~~

<hr style="height: 1px; background: skyblue"/>

#### BadukService

~~~

//===================================================
//	한 클라이언트와 소켓으로 데이타를 주고 받는 클래스
//===================================================

import java.io.*;
import java.util.*;
import java.net.*;
import java.awt.*;
import java.awt.event.*;

public class BadukService extends Thread
  {
    String id = "guest";

	Socket				socServer ;

	ObjectInputStream   inStream;
	ObjectOutputStream	outStream;
    BadukServer 		server;



    //----------------------------------------------------------
	/*	생성자 함수
		1. 인자로 넘겨받은 객체를 멤버변수로 지정
		2. 소켓의 입출력 스트림 얻어오기
		3. 쓰레드 구현
	*/
    public BadukService(BadukServer server, Socket s ){
      try{
      	   this.server = server;
      	   socServer = s;

			outStream = new ObjectOutputStream(socServer.getOutputStream());
			inStream = new ObjectInputStream(socServer.getInputStream());
			start();

      }catch(Exception e){}
    }



	//---------------------------------------------------------
	/*	쓰레드 루핑구문으로 클라이언트가 전송한 데이타 읽기
		데이타의 상태에 따라 각각의 구현 함수 호출
	*/
   	public void run()	{
		try{
			while(true)
			{
				BadukClientProtocol  obj = (BadukClientProtocol)inStream.readObject();
				int state = obj.getState();
				Object  data = obj.getData();
				switch(state){
					// 클라이언트의 쳇팅 메세지를 받은 경우
					case BadukClientProtocol.Chatting :	setChatting(data); break;

//--> 3				// 클라이언트 접속 후 아이디를 받은 경우
					case BadukClientProtocol.SEND_ID :	setID((String)data); break;
					// 종료시
					case BadukClientProtocol.EXIT	:	removeID((String)data); break;

//--> 4				// 클라이언트의 게임요청을 받은 경우
					case BadukClientProtocol.REQUEST_GAME : requestGame(); break;

//--> 6				// 클라이언트가 바둑판에 클릭했을때의 바둑알정보를 받은 경우
					case BadukClientProtocol.SET_BADUK_ROCK :  setBadukRock(data); break;

				}
			}
		}catch(Exception ex){
		}
	}//run



	//--------------------------------------------------------
	/*	클라이언트가 챗팅을 위한 데이타 객체를 전송했을때
		그 객체의 data 값을 각 클라이언트에 전송
	*/
	public void setChatting(Object data){
		String str = id + " >> "+ (String)data;
		server.setChatting(str);
	}

	//--------------------------------------------------------
	/*	소켓의 출력스트림으로 전송객체 전송
	*/
    public void sendInformation(Object obj){
    	try{
    		outStream.writeObject(obj);
    	}catch(IOException e){
    	}
    }


// --> 3
	//--------------------------------------------------------
	/*	읽어들인 아이디를 멤버변수 id로 지정하고 모든 클라이언트의 멤버 추가를 전송
	*/
    public void setID(String id){

    	this.id = id;
      	server.sendAddMember();		

    }

    public String getID(){
    	return id;
    }

	// 종료시
    public void removeID(String id){
      	server.sendRemoveMember(id);
    }

//--> 4
   public void requestGame(){
   		server.requestGame(this);
   }

//--> 6
	//-----------------------------------------------------
	/* 바둑알의 정보를 담은 데이타를 받아 각각의 행과 열값을 얻어 각각 클라이언트에 전송
	 */
   	public void setBadukRock(Object data){
		server.sendBadukRock(this, data);		
   	}

}	 

~~~

<hr style="height: 1px; background: skyblue"/>
