---
layout: post
title:  "0503-[Project]-menuTable"
subtitle:   "0503-BucketList"
categories: devlog
tags: project

---
## BucketList

<hr style="height: 1px; background: skyblue; "/>

#### khBucket

~~~

package khbucket;

import java.awt.*;
import java.awt.event.*;
import java.text.DecimalFormat;
import javax.swing.*;

public class BucketList extends JFrame {

//=============멤버 변수 선언====================================================

	// 멤버 변수 생성 3x3 버튼 생성
	int getsu = 3;
	JButton[][] la = new JButton[getsu][getsu];

	// Label 변수 생성
	JLabel jl, jl_result, jl_price;

	// 결과 버튼 변수 생성
	JButton jb_limit, jb_cancel;
	TextField tf_sum = new TextField(50);
	TextField tf_price = new TextField(30);
	int day = 75750; // 일급
	long s_day;
	int month = 1500000; // 월급
	long s_month;
	int year = 18000000; // 연봉
	long s_year;

	// int의 숫자 한계로 long 다차원 배열 생성
	long[][] price = { { 245650L, 887000L, 2000000000L }, { 300000000L, 4000000L, 1000000L },
			{ 4000000L, 1000000L, 1200000000L } };
	// 가격 텍스트 필드
	String[][] price1 = { { "에어팟: 245,650원", "아이패드: 887,000원", "요트: 2,000,000,000원" },
			{ "아우디: 300,000,000원", "바디프렌드: 4,000,000원", "커피머신: 1,000,000원" },
			{ "아이맥: 4,000,000원", "기타: 1,000,000원", "단독주택: 1,200,000,000원" } };
	// long 형 총액 결과 값
	long total, select;

//===============================================================================
	// 객체 생성
	public BucketList() {

		// 이미지 아이콘 버튼 생성
		ImageIcon ic1 = new ImageIcon("src/img/1.png");
		ImageIcon ic2 = new ImageIcon("src/img/2.png");
		ImageIcon ic3 = new ImageIcon("src/img/3.png");
		ImageIcon ic4 = new ImageIcon("src/img/4.png");
		ImageIcon ic5 = new ImageIcon("src/img/5.png");
		ImageIcon ic6 = new ImageIcon("src/img/6.png");
		ImageIcon ic7 = new ImageIcon("src/img/7.png");
		ImageIcon ic8 = new ImageIcon("src/img/8.png");
		ImageIcon ic9 = new ImageIcon("src/img/9.png");

		la[0][0] = new JButton(ic1);
		la[0][1] = new JButton(ic2);
		la[0][2] = new JButton(ic3);
		la[1][0] = new JButton(ic4);
		la[1][1] = new JButton(ic5);
		la[1][2] = new JButton(ic6);
		la[2][0] = new JButton(ic7);
		la[2][1] = new JButton(ic8);
		la[2][2] = new JButton(ic9);

		new JFrame("버킷리스트");

		jl = new JLabel("버킷리스트 ", JLabel.LEFT);
		jl.setFont(new Font("", Font.BOLD, 42));
		jl.setForeground(new Color(204, 61, 61));
		jl_result = new JLabel("총액");
		jl_result.setFont(new Font("", Font.BOLD, 15));

		jb_limit = new JButton("결제");
		jb_cancel = new JButton("취소");

		jl_price = new JLabel("가격");
		jl_price.setFont(new Font("", Font.BOLD, 15));
	}

	// 화면 붙이기 및 출력
	void addLayout() {
		JPanel p = new JPanel();
		JPanel p2 = new JPanel();
		JPanel p3 = new JPanel();

		p.setLayout(new GridLayout(3, 4)); // 레이아웃 지정
		p2.add(jl, "NORTH");
		p3.setLayout(new FlowLayout());
		for (int i = 0; i < getsu; i++) {
			for (int j = 0; j < la[i].length; j++) {
				p.add(la[i][j]);

				p3.add(jl_price);
				p3.add(tf_price);
				p3.add(jl_result);
				p3.add(tf_sum);
				p3.add(jb_limit);
				p3.add(jb_cancel);

			}
		}
		// 프레임영역에 붙이기
		setLayout(new BorderLayout(4, 3));

		add(p, BorderLayout.CENTER);
		add(p2, BorderLayout.NORTH);
		add(p3, BorderLayout.SOUTH);
		setSize(900, 900);
		setVisible(true);
		setDefaultCloseOperation(EXIT_ON_CLOSE);
	}

	// 4. 이벤트 등록 및 처리
	void eventProc() {
		MyHdlr cb = new MyHdlr();
		// 결제 버튼 클릭 이벤트
		jb_limit.addActionListener(new ActionListener() {

			public void actionPerformed(ActionEvent e) {
				int i = JOptionPane.showConfirmDialog(null, "결제 하시겠습니까?");
				if (i == 0) {
					if (total <= 300000) {
						JOptionPane.showMessageDialog(null, " 조금더 노력하면 살수 있습니다.! ");
					} else {
						JOptionPane.showMessageDialog(null, " 카드에 잔액이 없습니다.... ");
					}

				}
			}
		});
		// 취소 버튼 클릭 이벤트
		jb_cancel.addActionListener(new ActionListener() {

			public void actionPerformed(ActionEvent e) {
				total = 0;
				tf_sum.setText(null);

			}
		});

		for (int i = 0; i < getsu; i++) {
			for (int j = 0; j < getsu; j++) {
				la[i][j].addActionListener(cb);
			}
		}
	} // end of eventProc

	// 이벤트 핸들러 - 액션 리스너 사용
	class MyHdlr implements ActionListener {

		public void actionPerformed(ActionEvent e) {

			JButton obj = (JButton) e.getSource();
			// 물건의 단위 마다 점을 찍어주기 위해서
			DecimalFormat form = new DecimalFormat("#,###");
			// 물건의 누를때마다 이벤트를 발생 시키고
			for (int i = 0; i < getsu; i++) {
				for (int j = 0; j < getsu; j++) {
					if (obj == la[i][j]) {

						obj.setBackground(new Color(204, 61, 61));

						total += price[i][j]; // 총합 계산
						select = price[i][j]; // 개별 값

						s_day = select / day;
						s_month = select / month;
						s_year = select / year;

						String s_total = form.format(total);
						tf_sum.setText(s_total);

						JOptionPane.showMessageDialog(null,
								"최저 시급 기준으로"+s_year + "년 을 일하고, 개월 수로는" + s_month + "개월, 일수로는" + s_day + "일을 해야 결제 가능합니다.");

					}
					obj.setBackground(null);
					// 클릭한 물건의 값을 가격 텍스트필드에 띄우기
					if (obj == la[i][j]) {
						tf_price.setText(price1[i][j]);
					}
				}
			}

		}
	}// end of MyHdlr

	public static void main(String[] args) {
		BucketList f = new BucketList();
		f.addLayout();
		f.eventProc();

	} // end of main
}// end of Bucket



~~~

<hr style="height: 1px; background: skyblue"/>
