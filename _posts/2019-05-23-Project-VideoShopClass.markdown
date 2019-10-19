---
layout: post
title:  "0523-[Project]-VideoShopClass"
subtitle:   "0523-VideoShopClass"
categories: devlog
tags: project

---

## (default package)

<hr style="height: 1px; background: skyblue; "/>

#### VideoShop

~~~


import java.awt.*;
import javax.swing.*;

import  view.CustomerView;
import  view.RentView;
import  view.VideoView;

public class VideoShop extends JFrame
{
	CustomerView	customer;
	VideoView			video;
	RentView			rent;

	public VideoShop(){
		//각각의 화면을 관리하는 클래스 객체 생성
			customer = new CustomerView();
			video		= new VideoView();
			rent			= new RentView();

			JTabbedPane  pane = new JTabbedPane();
			pane.addTab("고객관리", customer );
			pane.addTab("비디오관리", video);
			pane.addTab("대여관리", rent );

			pane.setSelectedIndex(2);

			// 화면크기지정
			add("Center", pane );
			setSize(800,600);
			setVisible( true );

			setDefaultCloseOperation( JFrame.EXIT_ON_CLOSE );
	}
	public static void main(String[] args)
	{
			new VideoShop();
	}
}



~~~

<hr style="height: 1px; background: skyblue"/>

## model

<hr style="height: 1px; background: skyblue; "/>

#### CustomerDao

~~~

package model;

import model.vo.Customer;

/** 고객관리 JDBC 연결 */
public interface CustomerDao {
	public void insertCustomer(Customer vo) throws Exception;		// 회원가입
	public Customer selectByTel(String tel) throws Exception;			// 전화번호로 검색
	public int updateCustomer(Customer vo) throws Exception;		// 고객정보 수정
}



~~~

<hr style="height: 1px; background: skyblue"/>

#### RentDao

~~~

package model;

import java.util.ArrayList;

public interface RentDao {

	// 대여 메소드
	public void rentVideo(String tel, int vnum) throws Exception;
	// 반납 메소드
	public void returnVideo(int vnum) throws Exception;
	// 미납정보 메소드
	public ArrayList selectList() throws Exception;
}



~~~

<hr style="height: 1px; background: skyblue"/>

#### VideoDao

~~~

package model;

import java.util.ArrayList;

import model.vo.Video;

public interface VideoDao {
	public void insertVideo(Video vo, int count) throws Exception;
	public ArrayList SearchVideo(int sel, String word) throws Exception;
	public Video selectByPk(int vNum) throws Exception;
}



~~~

<hr style="height: 1px; background: skyblue"/>

## model.dao

<hr style="height: 1px; background: skyblue; "/>

#### CustomerModel

~~~


package model.dao;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;

import model.CustomerDao;
import model.vo.Customer;

public class CustomerModel implements CustomerDao {
	String driver = "oracle.jdbc.OracleDriver";
	String url = "jdbc:oracle:thin:@localhost:1521:orcl";
	String user = "oracle";
	String pass = "oracle";
	Connection con = null;
	PreparedStatement st = null;

	public CustomerModel() throws Exception {
		// 1. 드라이버로딩
		OracleCon.getInstance();
		con = DriverManager.getConnection(url, user, pass);

	}

	public void insertCustomer(Customer vo) throws Exception {
		// 2. Connection 연결객체 얻어오기
		con = DriverManager.getConnection(url, user, pass);
		String sql = "INSERT INTO MEMBER(PHONE_NUMBER,NAME,HOME_NUMBER,ADDRESS,EMAIL)" + "VALUES(?,?,?,?,?)";
		// 3. sql 문장 만들기
		st = con.prepareStatement(sql);
		st.setString(1, vo.getCustName());
		st.setString(2, vo.getCustTel1());
		st.setString(3, vo.getCustTel2());
		st.setString(4, vo.getCustAddr());
		st.setString(5, vo.getCustEmail());
		// 4. sql 전송객체 (PreparedStatement)

		// 5. sql 전송
		int result = st.executeUpdate();
		// 6. 닫기
		st.close();
		con.close();

	}

	public Customer selectByTel(String tel) throws Exception {
		Customer dao = new Customer();
		Customer vo = new Customer();
		Connection con = null;
		PreparedStatement st = null;
		ResultSet rs = null;
		try {

			con = DriverManager.getConnection(url, user, pass);
//			3. sql 문장 만들기 (*****)
			String sql = "SELECT * FROM MEMBER WHERE PHONE_NUMBER=?";

//			4. sql 전송 객체 얻어오기
			st = con.prepareStatement(sql);
			st.setString(1, tel);

//			5. sql 전송
			rs = st.executeQuery();

//			6. 결과 처리
			if (rs.next()) {
				dao.setCustName(rs.getString("NAME"));
				dao.setCustTel1(rs.getString("PHONE_NUMBER"));
				dao.setCustTel2(rs.getString("HOME_NUMBER"));
				dao.setCustAddr(rs.getString("ADDRESS"));
				dao.setCustEmail(rs.getString("EMAIL"));
			}

			return dao;
		} finally {
//			7. 닫기
//			(연결 닫기 제일 중요함)
			rs.close();
			st.close();
			con.close();
		}

	}

	public int updateCustomer(Customer vo) throws Exception {
		int result = 0;
		String sql = "UPDATE MEMBER SET NAME=?,HOME_NUMBER=?,ADDRESS=?,EMAIL=? WHERE PHONE_NUMBER=?";

		Connection con = DriverManager.getConnection(url, user, pass);
		st = con.prepareStatement(sql);

		st.setString(1, vo.getCustName());
		st.setString(2, vo.getCustTel2());
		st.setString(3, vo.getCustAddr());
		st.setString(4, vo.getCustEmail());
		st.setString(5, vo.getCustTel1());

		result = st.executeUpdate();

		st.close();
		con.close();

		return result;

	}
}


~~~

<hr style="height: 1px; background: skyblue"/>

#### OracleCon

~~~

package model.dao;

public class OracleCon {

	static OracleCon con = null;

	OracleCon() throws Exception{
		Class.forName("oracle.jdbc.OracleDriver");
		System.out.println("단 한번");
	}

	public static void getInstance() throws Exception{

		if(con == null ) {
		 con =	new OracleCon();
		}


	}
}



~~~

<hr style="height: 1px; background: skyblue"/>

#### RentModel

~~~

package model.dao;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.Statement;
import java.util.ArrayList;
import java.util.Vector;

import model.RentDao;
import model.vo.Video;

public class RentModel implements RentDao {
	String driver = "oracle.jdbc.OracleDriver";
	String url = "jdbc:oracle:thin:@localhost:1521:orcl";
	String user = "oracle";
	String pass = "oracle";

	Connection con = null;

	PreparedStatement st = null;
	ResultSet rs = null;

	public RentModel() throws Exception {
		// 1. 드라이버로딩
		OracleCon.getInstance();
		con = DriverManager.getConnection(url, user, pass);
	}

	// 대여 메소드
	public void rentVideo(String tel, int vnum) throws Exception {
		con = DriverManager.getConnection(url, user, pass);
		// 2. 연결객체
		// 3. sql 문장

		String sql = "INSERT INTO RENTAL(COL,PHONE_NUMBER,VIDEO_NUMBER,YESNO)  "
				+ "VALUES (VIDEO_SEQ.nextval,?,?,'F') ";

		// 4. 전송 객체
		st = con.prepareStatement(sql);

		st.setString(1, tel);
		st.setInt(2, vnum);

		st.executeUpdate();

		// 5. 전송

		st.close();
		con.close();
		// 6. 닫기
	}

	// 반납 메소드
	public void returnVideo(int vnum) throws Exception {
		con = DriverManager.getConnection(url, user, pass);

		String sql = "UPDATE RENTAL SET YESNO = 'T' WHERE VIDEO_NUMBER= ? AND YESNO ='F'  ";
//		String sql = "UPDATE 대여테이블명 SET 반납일=sysdate, 반납여부 ='T'"
//				+ "WHERE 비디오 번호=? AND 반납일 IS NULL AND 반납여부='F' ";



		st = con.prepareStatement(sql);
		st.setInt(1, vnum);


		st.executeUpdate();

		st.close();
		con.close();
	}

	// 미납정보 메소드
	public ArrayList selectList() throws Exception {
		con = DriverManager.getConnection(url, user, pass);

		//SELECT 비디오번호,제목,고객명,전화번호,대여일 + 반납예정일,'미납'반납여부
		//FROM 대여테이블 r, 비디오테이블 v, 고객테이블 c
		//WHERE r.비디오번호=v.비디오번호
		// AND r.전화번호 = c.전화번호
		//
		ArrayList list = new ArrayList();

		String sql = "SELECT v.VIDEO_NUMBER vnum ,m.NAME name ,v.TITLE title ,m.PHONE_NUMBER pnumber , r.YESNO yn  "
				+ "FROM RENTAL r, VIDEO v, MEMBER m  "
				+ "WHERE r.VIDEO_NUMBER = v.VIDEO_NUMBER AND r.PHONE_NUMBER = m.PHONE_NUMBER AND r.YESNO='F'  ";
//		System.out.println(sql);
		st = con.prepareStatement(sql);

		rs = st.executeQuery();

		while(rs.next()) {
			ArrayList data = new ArrayList();
			data.add(rs.getInt("vnum"));
			data.add(rs.getString("title"));
			data.add(rs.getString("name"));
			data.add(rs.getString("pnumber"));
			data.add("--");
			data.add(rs.getString("yn"));
			list.add(data);
		}

		st.close();
		con.close();

		return list;
	}

}



~~~

<hr style="height: 1px; background: skyblue"/>

#### VideoModel

~~~

package model.dao;

import java.beans.Statement;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.util.ArrayList;

import model.VideoDao;
import model.vo.Video;

public class VideoModel implements VideoDao {

	String driver = "oracle.jdbc.OracleDriver";
	String url = "jdbc:oracle:thin:@localhost:1521:orcl";
	String user = "oracle";
	String pass = "oracle";
	Connection con = null;
	PreparedStatement st = null;
	ResultSet rs = null;

	public VideoModel() throws Exception {

		// 1. 드라이버로딩

		OracleCon.getInstance();
		con = DriverManager.getConnection(url, user, pass);
	}

	public void insertVideo(Video vo, int count) throws Exception {
		// 2. Connection 연결객체 얻어오기
		// 3. sql 문장 만들기
		String sql = "INSERT INTO VIDEO(VIDEO_NUMBER, GENRE,TITLE, DIRECTOR, ACTOR ) "
				+ "VALUES(VIDEO_SEQ.nextval,?,?,?,?) ";
		// 4. sql 전송객체 (PreparedStatement)
		st = con.prepareStatement(sql);

		st.setString(1, vo.getGenre());
		st.setString(2, vo.getVideoName());
		st.setString(3, vo.getDirector());
		st.setString(4, vo.getActor());

		for (int i = 0; i < count; i++) {
			// 5. sql 전송
			st.executeUpdate();
		}
		// 6. 닫기
		st.close();
		con.close();
	}

	public ArrayList SearchVideo(int sel, String word) throws Exception {
		con = DriverManager.getConnection(url, user, pass);

		String[] cols = { "TITLE", "DIRECTOR" };
		// 2. 연결 객체 얻어오기

		// 3. sql 문장
		String sql = "SELECT VIDEO_NUMBER, TITLE, GENRE, DIRECTOR, ACTOR FROM VIDEO   " + "WHERE  " + cols[sel]
				+ " LIKE '%" + word + "%'  ";
//		System.out.println(sql);

		// 2차원 배열이니깐 arraylist 안에 arraylist 로 해줘야 한다.
		ArrayList list = new ArrayList();
		// 4. sql 전송객체 얻어오기

		st = con.prepareStatement(sql);

		// 5.sql 전송
		rs = st.executeQuery();

		// 6. 결과처리
		while (rs.next()) {
			ArrayList data = new ArrayList();
			// data 에 각 컬럼에서 얻어 온 값을 추가
			data.add(rs.getInt("VIDEO_NUMBER"));
			// 나머지도
			data.add(rs.getString("TITLE"));
			data.add(rs.getString("GENRE"));
			data.add(rs.getString("DIRECTOR"));
			data.add(rs.getString("ACTOR"));

			list.add(data);
		}
		// 7. 연결 해제
		st.close();
		con.close();

		return list;
	}

	public Video selectByPk(int vNum) throws Exception {
		Video vo = new Video();
		con = DriverManager.getConnection(url, user, pass);
		// 2. 연결 객체 얻어오기
		// 3. sql 문장
		String sql = "SELECT * FROM VIDEO WHERE VIDEO_NUMBER=?";

		// 4. sql 전송객체 얻어오기

		st = con.prepareStatement(sql);
		st.setString(1,String.valueOf(vNum));


		// 5.sql 전송
		rs = st.executeQuery();

		// 6. 결과처리

		if(rs.next()) {
			vo.setVideoNo(rs.getInt("VIDEO_NUMBER"));
			vo.setVideoName(rs.getString("TITLE"));
			vo.setGenre(rs.getString("GENRE"));
			vo.setDirector(rs.getString("DIRECTOR"));
			vo.setActor(rs.getString("ACTOR"));
			vo.setExp(rs.getString("DESCRIPTION"));
		}

		// 7. 연결 해제
				st.close();
				con.close();

		return vo;
	}
}



~~~

<hr style="height: 1px; background: skyblue"/>

## model.vo

<hr style="height: 1px; background: skyblue; "/>

#### Customer

~~~

package model.vo;

public class Customer {
	String custName; // 고객명
	String custTel1; // 전화번호
	String custTel2; // 보조 전화번호
	String custAddr; // 주소
	String custEmail; // 이메일

	public Customer() {
	}

	public Customer(String custName, String custTel1, String custTel2, String custAddr, String custEmail) {
		super();
		this.custName = custName;
		this.custTel1 = custTel1;
		this.custTel2 = custTel2;
		this.custAddr = custAddr;
		this.custEmail = custEmail;

	}

	public String getCustName() {
		return custName;
	}

	public void setCustName(String custName) {
		this.custName = custName;
	}

	public String getCustTel1() {
		return custTel1;
	}

	public void setCustTel1(String custTel1) {
		this.custTel1 = custTel1;
	}

	public String getCustTel2() {
		return custTel2;
	}

	public void setCustTel2(String custTel2) {
		this.custTel2 = custTel2;
	}

	public String getCustAddr() {
		return custAddr;
	}

	public void setCustAddr(String custAddr) {
		this.custAddr = custAddr;
	}

	public String getCustEmail() {
		return custEmail;
	}

	public void setCustEmail(String custEmail) {
		this.custEmail = custEmail;
	}

}



~~~

<hr style="height: 1px; background: skyblue"/>

#### Video

~~~

package model.vo;

public class Video {

	int videoNo;					// 비디오번호
	String genre;				// 장르
	String videoName;			// 비디오명
	String director;				// 감독
	String actor;					// 배우
	String exp;					// 설명

	public int getVideoNo() {
		return videoNo;
	}
	public void setVideoNo(int videoNo) {
		this.videoNo = videoNo;
	}
	public String getGenre() {
		return genre;
	}
	public void setGenre(String genre) {
		this.genre = genre;
	}
	public String getVideoName() {
		return videoName;
	}
	public void setVideoName(String videoName) {
		this.videoName = videoName;
	}
	public String getDirector() {
		return director;
	}
	public void setDirector(String director) {
		this.director = director;
	}
	public String getActor() {
		return actor;
	}
	public void setActor(String actor) {
		this.actor = actor;
	}
	public String getExp() {
		return exp;
	}
	public void setExp(String exp) {
		this.exp = exp;
	}



}



~~~

<hr style="height: 1px; background: skyblue"/>

## view

<hr style="height: 1px; background: skyblue; "/>

#### CustomerView

~~~

package view;

import java.awt.BorderLayout;
import java.awt.GridBagConstraints;
import java.awt.GridBagLayout;
import java.awt.GridLayout;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

import javax.swing.JButton;
import javax.swing.JLabel;
import javax.swing.JOptionPane;
import javax.swing.JPanel;
import javax.swing.JTextField;

import model.CustomerDao;
import model.dao.CustomerModel;
import model.vo.Customer;

public class CustomerView extends JPanel {
//	JFrame frm;
	JTextField tfCustName, tfCustTel, tfCustTelAid, tfCustAddr, tfCustEmail;
	JButton bCustRegist, bCustModify;

	JTextField tfCustNameSearch, tfCustTelSearch;
	JButton bCustNameSearch, bCustTelSearch;

	// **************************************
	CustomerDao dao;

	public CustomerView() {
		addLayout();
		connectDB();
		eventProc();
	}

	public void eventProc() {
		ButtonEventHandler btnHandler = new ButtonEventHandler();

		// 이벤트 등록
		bCustRegist.addActionListener(btnHandler);
		bCustModify.addActionListener(btnHandler);
		bCustNameSearch.addActionListener(btnHandler);
		bCustTelSearch.addActionListener(btnHandler);
	}

	// 버튼 이벤트 핸들러 만들기
	class ButtonEventHandler implements ActionListener {
		public void actionPerformed(ActionEvent ev) {
			Object o = ev.getSource();

			if (o == bCustRegist) {
				registCustomer(); // 회원등록
			} else if (o == bCustModify) {
				updateCustomer(); // 회원정보수정
			} else if (o == bCustTelSearch) { // 이름검색
				searchByTel(); // 전화번호 검색
			} else if (o == bCustNameSearch) { // 이름검색
				System.out.println("이름검색");
			}
		}
	}

	// 회원가입하는 메소드
	public void registCustomer() {
		Customer vo = new Customer();
		// 1. 화면 텍스트필드의 입력값 얻어오기
		vo.setCustName(tfCustName.getText());
		vo.setCustTel1(tfCustTel.getText());
		vo.setCustTel2(tfCustTelAid.getText());
		vo.setCustAddr(tfCustAddr.getText());
		vo.setCustEmail(tfCustEmail.getText());
		// 2. 1값들을 Customer 클래스의 멤버로지정
		try {
			dao.insertCustomer(vo);
			// 3. Model 클래스 안에 insertCustomer () 메소드 호출하여 2번 VO 객체를 넘김
		} catch (Exception e) {
			JOptionPane.showMessageDialog(null, "입력" + e.getMessage());
		}
		// 4. 화면 초기화
		clearTextField();
//		JOptionPane.showMessageDialog(null, "입력");

	}

	// 전화번호에 의한 검색
	public void searchByTel() {
		// 1. 입력한 전화번호 얻어오기
		String tel = tfCustTelSearch.getText();
		try {
			Customer vo = dao.selectByTel(tel);
			// 2. Model의 전화번호 검색메소드 selectByTel() 호출
			tfCustName.setText(vo.getCustName());
			tfCustTel.setText(vo.getCustTel1());
			tfCustTelAid.setText(vo.getCustTel2());
			tfCustAddr.setText(vo.getCustAddr());
			tfCustEmail.setText(vo.getCustEmail());
		} catch (Exception e) {
			// 3. 2번의 넘겨받은 Customer의 각각의 값을 화면 텍스트 필드 지정

			JOptionPane.showMessageDialog(null, "검색");
		}
	}

	// 회원정보수정
	public void updateCustomer() {
		Customer vo = new Customer();

		vo.setCustName(tfCustName.getText());
		vo.setCustTel1(tfCustTel.getText());
		vo.setCustTel2(tfCustTelAid.getText());
		vo.setCustAddr(tfCustAddr.getText());
		vo.setCustEmail(tfCustEmail.getText());

		try {
			dao.updateCustomer(vo);
		} catch (Exception e) {
			JOptionPane.showMessageDialog(null, "수정");
		}

	}

	public void connectDB() {
		try {
			dao = new CustomerModel();
		} catch (Exception ex) {
			JOptionPane.showMessageDialog(null, "드라이버 오류:" + ex.getMessage());
		}
	}

	void clearTextField() {
		tfCustName.setText(null);
		tfCustTel.setText(null);
		tfCustTelAid.setText(null);
		tfCustAddr.setText(null);
		tfCustEmail.setText(null);
	}

	public void addLayout() {

		tfCustName = new JTextField(20);
		tfCustTel = new JTextField(20);
		tfCustTelAid = new JTextField(20);
		tfCustAddr = new JTextField(20);
		tfCustEmail = new JTextField(20);

		tfCustNameSearch = new JTextField(20);
		tfCustTelSearch = new JTextField(20);

		bCustRegist = new JButton("회원가입");
		bCustModify = new JButton("회원수정");
		bCustNameSearch = new JButton("이름검색");
		bCustTelSearch = new JButton("번호검색");

		// 회원가입 부분 붙이기
		// ( 그 복잡하다던 GridBagLayout을 사용해서 복잡해 보임..다른 쉬운것으로...대치 가능 )
		JPanel pRegist = new JPanel();
		pRegist.setLayout(new GridBagLayout());
		GridBagConstraints cbc = new GridBagConstraints();
		cbc.weightx = 1.0;
		cbc.weighty = 1.0;
		cbc.fill = GridBagConstraints.BOTH;
		cbc.gridx = 0;
		cbc.gridy = 0;
		cbc.gridwidth = 1;
		cbc.gridheight = 1;
		pRegist.add(new JLabel("	이	름	"), cbc);
		cbc.gridx = 1;
		cbc.gridy = 0;
		cbc.gridwidth = 1;
		cbc.gridheight = 1;
		pRegist.add(tfCustName, cbc);
		cbc.gridx = 2;
		cbc.gridy = 0;
		cbc.gridwidth = 1;
		cbc.gridheight = 1;
		pRegist.add(bCustModify, cbc);
		cbc.gridx = 3;
		cbc.gridy = 0;
		cbc.gridwidth = 1;
		cbc.gridheight = 1;
		pRegist.add(bCustRegist, cbc);

		cbc.gridx = 0;
		cbc.gridy = 1;
		cbc.gridwidth = 1;
		cbc.gridheight = 1;
		pRegist.add(new JLabel("	전	화	"), cbc);
		cbc.gridx = 1;
		cbc.gridy = 1;
		cbc.gridwidth = 1;
		cbc.gridheight = 1;
		pRegist.add(tfCustTel, cbc);
		cbc.gridx = 2;
		cbc.gridy = 1;
		cbc.gridwidth = 1;
		cbc.gridheight = 1;
		pRegist.add(new JLabel(" 추가전화  "), cbc);
		cbc.gridx = 3;
		cbc.gridy = 1;
		cbc.gridwidth = 1;
		cbc.gridheight = 1;
		pRegist.add(tfCustTelAid, cbc);

		cbc.gridx = 0;
		cbc.gridy = 2;
		cbc.gridwidth = 1;
		cbc.gridheight = 1;
		pRegist.add(new JLabel("	주	소	"), cbc);
		cbc.gridx = 1;
		cbc.gridy = 2;
		cbc.gridwidth = 3;
		cbc.gridheight = 1;
		pRegist.add(tfCustAddr, cbc);

		cbc.gridx = 0;
		cbc.gridy = 3;
		cbc.gridwidth = 1;
		cbc.gridheight = 1;
		pRegist.add(new JLabel("	이메일	"), cbc);
		cbc.gridx = 1;
		cbc.gridy = 3;
		cbc.gridwidth = 3;
		cbc.gridheight = 1;
		pRegist.add(tfCustEmail, cbc);

		// 회원검색 부분 붙이기
		JPanel pSearch = new JPanel();
		pSearch.setLayout(new GridLayout(2, 1));
		JPanel pSearchName = new JPanel();
		pSearchName.add(new JLabel("		이 	름	"));
		pSearchName.add(tfCustNameSearch);
		pSearchName.add(bCustNameSearch);
		JPanel pSearchTel = new JPanel();
		pSearchTel.add(new JLabel("	전화번호	"));
		pSearchTel.add(tfCustTelSearch);
		pSearchTel.add(bCustTelSearch);
		pSearch.add(pSearchName);
		pSearch.add(pSearchTel);

		// 전체 패널에 붙이기
		setLayout(new BorderLayout());
		add("Center", pRegist);
		add("South", pSearch);

	}

}



~~~

<hr style="height: 1px; background: skyblue"/>

#### RentView

~~~

package view;

import java.awt.BorderLayout;
import java.awt.FlowLayout;
import java.awt.GridLayout;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.awt.event.MouseAdapter;
import java.awt.event.MouseEvent;
import java.util.ArrayList;

import javax.swing.JButton;
import javax.swing.JLabel;
import javax.swing.JOptionPane;
import javax.swing.JPanel;
import javax.swing.JScrollPane;
import javax.swing.JTable;
import javax.swing.JTextField;
import javax.swing.border.TitledBorder;
import javax.swing.table.AbstractTableModel;

import model.dao.RentModel;

public class RentView extends JPanel {
	JTextField tfRentTel, tfRentCustName, tfRentVideoNum;
	JButton bRent;

	JTextField tfReturnVideoNum;
	JButton bReturn;

	JTable tableRecentList;

	RentTableModel rentTM;

	// **********************
	// 비지니스 로직 역할을 하는 모델 클래스 선언

	RentModel db;

	// ==============================================
	// 생성자 함수
	public RentView() {
		addLayout(); // 화면구성
		eventProc(); // DB연결
		connectDB();
		selectNonReturn(); // 화면이 켜지자 마자 미납 목록 출력
	}

	// DB 연결
	void connectDB() {
		try {
			db = new RentModel();
		} catch (Exception e) {
			e.printStackTrace();
		}
	}

	// 이벤트 등록
	public void eventProc() {

		// 객체 생성
		ActionHandler ah = new ActionHandler();
		// 이벤트가 발생할 객체들을 핸들러와 연결
		tfRentTel.addActionListener(ah);
		bRent.addActionListener(ah);
		bReturn.addActionListener(ah);

	}

	class ActionHandler implements ActionListener {

		public void actionPerformed(ActionEvent e) {
//			System.out.println("이벤트");
			Object evt = e.getSource();

			if (evt == tfRentTel) {
				selectCustName();

			} else if (evt == bRent) {
				rentVideo();
				selectNonReturn();
			} else if (evt == bReturn) {
				returnVideo();
				selectNonReturn();
			}

		}

	}

	// 미납 목록 출력 메소드
	public void selectNonReturn() {
		try {
			rentTM.data = db.selectList();
			rentTM.fireTableDataChanged();
		} catch (Exception ex) {
			System.out.println("검색 실패");
		}
	}

	// 전화 입력 후 엔터치면 고객명을 출력하는 메소드
	public void selectCustName() {

	}

	// 비디오 반납시 처리하는 메소드
	public void returnVideo() {
		int vnum = Integer.parseInt(tfReturnVideoNum.getText());

		try {
			db.returnVideo(vnum);
		} catch (Exception e) {
			e.printStackTrace();
		}

	}

	// 비디오 대여시 처리하는 메소드
	public void rentVideo() {
		// 1. 화면에서 필요한 정보를 얻어오기

		// 2. 모델 쪽 메소드 호출

		// 3. 결과처리 (대여 후)

		String tel = tfRentTel.getText();
		int vnum = Integer.parseInt(tfRentVideoNum.getText());
		try {
			db.rentVideo(tel, vnum);

		} catch (Exception e) {
			e.printStackTrace();
		}
	}

	/* 객체 생성 및 화면 구성 */
	void addLayout() {
		// 멤버 변수의 객체 생성
		tfRentTel = new JTextField();
		tfRentCustName = new JTextField(15);
		tfRentVideoNum = new JTextField(15);
		bRent = new JButton("대여");

		tfReturnVideoNum = new JTextField(15);
		bReturn = new JButton("반납");

		rentTM = new RentTableModel();
		tableRecentList = new JTable(rentTM);

		// ************************************************
		// 화면 구성
		// north 영역
		JPanel p_north = new JPanel();
//		p_north.setBorder(new TitledBorder("north"));
		p_north.setLayout(new GridLayout(1, 2));

		// north 왼쪽 영역
		JPanel p_north_west = new JPanel();
		p_north_west.setLayout(new GridLayout(4, 2));
		p_north_west.setBorder(new TitledBorder("대여"));
		p_north_west.add(new JLabel("전화번호"));
		p_north_west.add(tfRentTel);
		p_north_west.add(new JLabel("고객명"));
		p_north_west.add(tfRentCustName);
		p_north_west.add(new JLabel("비디오 번호"));
		p_north_west.add(tfRentVideoNum);
		p_north_west.add(bRent);
		p_north.add(p_north_west);

		// north 오른쪽 영역
		JPanel p_north_east = new JPanel();
		p_north_east.setLayout(new FlowLayout());
		p_north_east.setBorder(new TitledBorder("반납"));
		p_north_east.add(new JLabel("비디오 번호"));
		p_north_east.add(tfReturnVideoNum);
		p_north_east.add(bReturn);

		p_north.add(p_north_east);

		// south 영역
		JPanel p_south = new JPanel();
//		p_south.setBorder(new TitledBorder("south"));
		p_south.setLayout(new BorderLayout());

		p_south.add(new JScrollPane(tableRecentList));
		// 전체영역 붙히기
		setLayout(new BorderLayout());

		add(p_north, BorderLayout.NORTH);
		add(p_south, BorderLayout.CENTER);

	}

	class RentTableModel extends AbstractTableModel {

		ArrayList data = new ArrayList();
		String[] columnNames = { "비디오번호", "제목", "고객명", "전화번호", "반납예정일", "반납여부" };

		public int getColumnCount() {
			return columnNames.length;
		}

		public int getRowCount() {
			return data.size();
		}

		public Object getValueAt(int row, int col) {
			ArrayList temp = (ArrayList) data.get(row);
			return temp.get(col);
		}

		public String getColumnName(int col) {
			return columnNames[col];
		}
	}

}



~~~

<hr style="height: 1px; background: skyblue"/>

#### VideoView

~~~

package view;

import java.awt.BorderLayout;
import java.awt.GridLayout;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.awt.event.MouseAdapter;
import java.awt.event.MouseEvent;
import java.util.ArrayList;

import javax.swing.JButton;
import javax.swing.JCheckBox;
import javax.swing.JComboBox;
import javax.swing.JLabel;
import javax.swing.JOptionPane;
import javax.swing.JPanel;
import javax.swing.JScrollPane;
import javax.swing.JTable;
import javax.swing.JTextArea;
import javax.swing.JTextField;
import javax.swing.border.TitledBorder;
import javax.swing.table.AbstractTableModel;

import model.dao.VideoModel;
import model.vo.Video;

public class VideoView extends JPanel {
	// member field
	JTextField tfVideoNum, tfVideoTitle, tfVideoDirector, tfVideoActor;
	JComboBox comVideoJanre;
	JTextArea taVideoContent;

	JCheckBox cbMultiInsert;
	JTextField tfInsertCount;

	JButton bVideoInsert, bVideoModify, bVideoDelete;

	JComboBox comVideoSearch;
	JTextField tfVideoSearch;
	JTable tableVideo; // view 역할만

	VideoTableModel tbModelVideo;

	VideoModel db;

	// ##############################################
	// constructor method
	public VideoView() {
		addLayout(); // 화면설계
		initStyle();
		eventProc();
		connectDB(); // DB연결
	}

	public void connectDB() { // DB연결
		try {
			db = new VideoModel();
		} catch (Exception e) {
			e.printStackTrace();
		}

	}

	public void eventProc() {
		ButtonEventHandler hdlr = new ButtonEventHandler();
		bVideoInsert.addActionListener(hdlr);
		bVideoModify.addActionListener(hdlr);
		bVideoDelete.addActionListener(hdlr);
		tfVideoSearch.addActionListener(hdlr); // 버튼 아니어도 이벤트 가능

		cbMultiInsert.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent e) {
				tfInsertCount.setEditable(cbMultiInsert.isSelected());
				// 체크박스가 선택이 되서 true 가 되면 편집가능
				// 체크박스가 선택이 되서 false 가 되면 편집 불가능

			}
		}); // 액션리스너를 상속받아 이름없는 클래스를 선언함과 동시에 객체 생성

		// JTable 비디오 검색을 클릭 했을때
		tableVideo.addMouseListener(new MouseAdapter() {

			public void mouseClicked(MouseEvent e) {
				int col = 0;
				int row = tableVideo.getSelectedRow();
				int vNum = (Integer)tableVideo.getValueAt(row, col); // 1.5 버전 이후로 casting
//				JOptionPane.showMessageDialog(null,vNum);

				// 1. 선택한 비디오 번호를 모델단의 selectByPK() 호출시 인자로 보내기
				// 2. 넘겨 받은 Video 에서 해당 값들 화면 출력하기
				Video vo;
				try {
					vo = db.selectByPk(vNum);
					tfVideoNum.setText(String.valueOf(vo.getVideoNo()));
					comVideoJanre.setSelectedItem(vo.getGenre());
					tfVideoTitle.setText(vo.getVideoName());
					tfVideoDirector.setText(vo.getDirector());
					tfVideoActor.setText(vo.getActor());
					// 나머지도

				} catch (Exception e1) {
					e1.printStackTrace();
				}

			}
		});
	}

	// 버튼 이벤트 핸들러 만들기
	class ButtonEventHandler implements ActionListener {
		public void actionPerformed(ActionEvent ev) {
			Object o = ev.getSource();

			if (o == bVideoInsert) {
				registVideo(); // 비디오 등록
			} else if (o == bVideoModify) {
				modifyVideo(); // 비디오 정보 수정
			} else if (o == bVideoDelete) {
				deleteVideo(); // 비디오 정보 삭제
			} else if (o == tfVideoSearch) {
				searchVideo(); // 비디오 검색
			}
		}
	}

	// 입고 클릭시 - 비디오 정보 등록
	public void registVideo() {
		Video vo = new Video();
//		JOptionPane.showMessageDialog(null, "입고");
		// 1.화면의 입력 및 선택 값들 얻어오기 -> Video(=vo) 객체로 생성 \

//		vo.setVideoNo(Integer.parseInt(tfVideoNum.getText()));
		vo.setGenre((String) comVideoJanre.getSelectedItem());
		vo.setVideoName(tfVideoTitle.getText());
		vo.setDirector(tfVideoDirector.getText());
		vo.setActor(tfVideoActor.getText());
		vo.setExp(taVideoContent.getText());
		int count = Integer.parseInt(tfInsertCount.getText());

		// 2. 모델단의 메소드 1번값들 전송
		try {
			db.insertVideo(vo, count);

		} catch (Exception e) {
			e.printStackTrace();
		}

	}

	public void initStyle() { // 입력하지 못하게 만듬.
		tfVideoNum.setEditable(false); // setEnable 은 값도 못가져오게 됨
		tfInsertCount.setEditable(false);
		tfInsertCount.setHorizontalAlignment(JTextField.RIGHT);
	}

	// 수정 클릭시 - 비디오 정보 수정
	public void modifyVideo() {
		JOptionPane.showMessageDialog(null, "수정");
	}

	// 삭제 클릭시 - 비디오 정보 삭제
	public void deleteVideo() {

		JOptionPane.showMessageDialog(null, "삭제");
	}

	// 비디오현황검색
	public void searchVideo() {
//		JOptionPane.showMessageDialog(null, "검색");
		// 글씨보다 index 처리해서 받아오려 한다.
		int sel = comVideoSearch.getSelectedIndex();

		String word = tfVideoSearch.getText();
		try {
			// 검색 결과를 화면 JTable의 내용을 담당하는 TableModel 안의 data에 지정
			tbModelVideo.data = db.SearchVideo(sel, word);
			tbModelVideo.fireTableDataChanged();
		} catch (Exception e) {
			e.printStackTrace();
		}

	}

	// 화면설계 메소드
	public void addLayout() {
		// 멤버변수의 객체 생성
		tfVideoNum = new JTextField();
		tfVideoTitle = new JTextField();
		tfVideoDirector = new JTextField();
		tfVideoActor = new JTextField();

		String[] cbJanreStr = { "멜로", "엑션", "스릴", "코미디" };
		comVideoJanre = new JComboBox(cbJanreStr);
		taVideoContent = new JTextArea();

		cbMultiInsert = new JCheckBox("다중입고");
		tfInsertCount = new JTextField("1", 5);

		bVideoInsert = new JButton("입고");
		bVideoModify = new JButton("수정");
		bVideoDelete = new JButton("삭제");

		String[] cbVideoSearch = { "제목", "감독" };
		comVideoSearch = new JComboBox(cbVideoSearch);
		tfVideoSearch = new JTextField(15);

		tbModelVideo = new VideoTableModel();
		tableVideo = new JTable(tbModelVideo);

		// *********************************************************************
		// 화면 구성

		// 왼쪽 영역
		JPanel p_west = new JPanel();
//		p_west.setBorder(new TitledBorder("WEST")); // title
		p_west.setLayout(new BorderLayout());
		// 왼쪽- 메인 영역
		JPanel p_west_c = new JPanel();
		p_west_c.setLayout(new BorderLayout());

		// 왼쪽-메인 - 중앙
		JPanel p_west_c_c = new JPanel();
		p_west_c_c.setBorder(new TitledBorder("비디오정보입력"));
		p_west_c.add(p_west_c_c, BorderLayout.CENTER);

		// 비디오 정보 입력 부분
		JPanel p_w_c_c_1 = new JPanel();
		p_w_c_c_1.setLayout(new GridLayout(5, 2));
		p_w_c_c_1.add(new JLabel("비디오 번호"));
		p_w_c_c_1.add(tfVideoNum);
		p_w_c_c_1.add(new JLabel("장르"));
		p_w_c_c_1.add(comVideoJanre);
		p_w_c_c_1.add(new JLabel("제목"));
		p_w_c_c_1.add(tfVideoTitle);
		p_w_c_c_1.add(new JLabel("감독"));
		p_w_c_c_1.add(tfVideoDirector);
		p_w_c_c_1.add(new JLabel("배우"));
		p_w_c_c_1.add(tfVideoActor);

		// 비디오 설명 입력 부분
		JPanel p_w_c_c_2 = new JPanel();
		p_w_c_c_2.setLayout(new BorderLayout());
		p_w_c_c_2.add(new JLabel("설명"), BorderLayout.WEST);
		p_w_c_c_2.add(taVideoContent, BorderLayout.CENTER);

		p_west_c_c.setLayout(new GridLayout(2, 1));
		p_west_c_c.add(p_w_c_c_1);
		p_west_c_c.add(p_w_c_c_2);

		// 왼쪽-메인 -아래
		JPanel p_west_c_s = new JPanel();
		p_west_c_s.setBorder(new TitledBorder("다중입고시 선택하시오"));
		p_west_c_s.add(cbMultiInsert);
		p_west_c_s.add(tfInsertCount);
		p_west_c_s.add(new JLabel("개"));

		p_west_c.add(p_west_c_s, BorderLayout.SOUTH);

		p_west.add(p_west_c, BorderLayout.CENTER);
		// 왼쪽 - 버튼 영역
		JPanel p_west_south = new JPanel();
		p_west_south.add(bVideoInsert);
		p_west_south.add(bVideoModify);
		p_west_south.add(bVideoDelete);
		p_west.add(p_west_south, BorderLayout.SOUTH);

		p_west_south.setLayout(new GridLayout(1, 3));

		// 오른쪽 영역
		JPanel p_east = new JPanel();
		p_east.setBorder(new TitledBorder("비디오검색")); // title
		p_east.setLayout(new BorderLayout());

		JPanel p_east_north = new JPanel();
		p_east_north.add(comVideoSearch);
		p_east_north.add(tfVideoSearch);

		p_east.add(p_east_north, BorderLayout.NORTH);
		p_east.add(new JScrollPane(tableVideo), BorderLayout.CENTER); // tableVideo 는 뷰만 제공

		// 전체 영역 붙히기
		setLayout(new GridLayout(1, 2));
		add(p_west);
		add(p_east);
	}

	// 화면에 테이블 붙이는 메소드
	class VideoTableModel extends AbstractTableModel {

		ArrayList data = new ArrayList();
		String[] columnNames = { "비디오번호", "제목", "장르", "감독", "배우" };

		// =============================================================
		// 1. 기본적인 TabelModel 만들기
		// 아래 세 함수는 TabelModel 인터페이스의 추상함수인데
		// AbstractTabelModel에서 구현되지 않았기에...
		// 반드시 사용자 구현 필수!!!!

		public int getColumnCount() {
			return columnNames.length;
		}

		public int getRowCount() {
			return data.size();
		}

		public Object getValueAt(int row, int col) {
			ArrayList temp = (ArrayList) data.get(row);
			return temp.get(col);
		}

		public String getColumnName(int col) {
			return columnNames[col];
		}
	}
}



~~~

<hr style="height: 1px; background: skyblue"/>
