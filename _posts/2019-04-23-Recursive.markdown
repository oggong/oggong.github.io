---
layout: post
title:  "0423-[자바]-Recursive"
subtitle:   "0423-recursive"
categories: devlog
tags: Java

---
## recursive

<hr style="height: 1px; background: skyblue; "/>

#### ASumTest

~~~

package f_recursive;

public class ASumTest {

//	public static void main(String[] args) {
//
//		int sum = 0;
//		for (int i = 1; i <= 10; i++) {
//			// sum += i;
//
//			int exsum = sum;
//			sum = exsum + i;
//
//			System.out.println(sum + "=" + exsum + "+" + i);
//
//		}
//		System.out.println("합:" + sum);
//
//	} // end of main

	public static void main(String[] args) {
		int sum = 0;
		sum = sumFunc(3);
		System.out.println("총합:" + sum);
	}// end of main2

	static int sumFunc(int i) {
		if (i == 1)
			return 1;
		return i + sumFunc(i - 1); // 자기 자신이름을 자기가 호출 할때 재귀 호출!
									// 내비 두면 무한 루프 ---> 반드시 마지막 설정 해줘야 함!
									// 제어권도 확실히 하기

	}
}// end of class



~~~

<hr style="height: 1px; background: skyblue; "/>

#### Factorial

~~~

package f_recursive;

public class Factorial {

//	5! = 5*4*3*2*1

	public static void main(String[] args) {
		int fac = 0;
		fac = facFunc(5);
		System.out.println("5 factorial :" + fac);
	}

	static int facFunc(int i) {
		if (i == 1)
			return 1;
		return i * facFunc(i - 1);
	}
}



~~~

<hr style="height: 1px; background: skyblue; "/>

#### Fibonacci

~~~

package f_recursive;

public class Fibonacci {

	// 피보나치 수열!!@#!@#!@#!#

	public static void main(String[] args) {
		int n = 5;
		int result = fib(n);
		System.out.println("결과 : " + result);
	}

	static int fib(int n) {
		if (n == 1)
			return 1;
		if (n == 2)
			return 2;

		return fib(n - 1) + fib(n - 2);
	}

} // 일반적으로 쓰지 않는 이유는 가독성이 떨어지기 때문임! 재귀호출1@#!@#!@#!@#



~~~

<hr style="height: 1px; background: skyblue; "/>
