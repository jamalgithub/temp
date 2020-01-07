package com.oca.a1;

import java.io.IOException;
import java.io.Reader;
import java.math.BigDecimal;
import java.math.BigInteger;
import java.util.ArrayList;
import java.util.Arrays;
import java.util.Collections;
import java.util.HashMap;
import java.util.HashSet;
import java.util.List;
import java.util.stream.IntStream;

public class Test {

	public static void main(String[] args) {
		HashMap m = new HashMap();

		Object o1 = new Object();
		Object o2 = o1;

		m.put(o1, 1);
		m.put(o2, 2);

		System.out.println(m.get(o1));

		BigInteger bi = new BigInteger("1");
		BigInteger bi2 = bi.add(new BigInteger("1"));

		System.out.println(bi);
		System.out.println(bi2);

		System.out.println(isFoo("foo"));

		ArrayList l = new ArrayList();
		l.add(1);
		l.add(1);
		l.add(1);

		System.out.println(l.size());

		HashSet hs = new HashSet();
		hs.add(new Integer(1));
		// hs.add(new Integer(1));
		// hs.add(new Integer(2));

		System.out.println(hs.size());

		char ch = 'Z';
		int asciiValue = ch;
		System.out.printf("Ascii Value of %c = %d\n", ch, asciiValue);

		char s = 'B';
		if (s >= 'A' && s <= 'Z')
			System.out.printf("%d", (int) s);
		System.out.println();

		int[] tab = { 12, 1, 21, 8 };
		int min = Arrays.stream(tab).min().getAsInt();
		System.out.println(min);

		System.out.println(sum("99.35", "1.10"));

	}
	
	void print(Reader reader) throws IOException {
		try {
		     int code = reader.read();
		     while (code != -1) {
		        System.out.print((char) code);
		        code = reader.read();
		     }
		 } finally {
		    try {
		        reader.close();
		    } catch(IOException e) {}
		 }
	}

	public static boolean isFoo(String param) {
		return "foo".equals(param);
	}

	static char scanChar(String s) {
		for (char c = 'A'; c < 'Z'; c++) {
			if (AsciiArt.printChar(c) == s)
				return c;
		}
		return '?';
	}
	
	static String concat(String[] strings) {
		String res = "";
		for (String string : strings) {
			res = res.concat(string);
		}
		return res;
	}

	/**
	 * Finding the Max Value sorting the array and returning the largest number.
	 */
	public static int getLargest(int[] numbers) {
		int temp;
		int size = numbers.length;
		for (int i = 0; i < size; i++) {
			for (int j = i + 1; j < size; j++) {
				if (numbers[i] > numbers[j]) {
					temp = numbers[i];
					numbers[i] = numbers[j];
					numbers[j] = temp;
				}
			}
		}
		return numbers[size - 1];
	}

	/**
	 * Finding the Max Value using Arrays built in sort function
	 */
	public static int getLargest2(int[] a) {
		Arrays.sort(a);
		return a[a.length - 1];
	}

	/**
	 * Finding the Max Value using collections
	 */
	public static int getLargest3(Integer[] a) {
		List<Integer> list = Arrays.asList(a);
		Collections.sort(list);
		int element = list.get(a.length - 1);
		return element;
	}

	/**
	 * Finding the Min Value in array Using Stream
	 */
	public static int MinUsesIntegerComparator(int[] a) {
		return Arrays.stream(a).min().getAsInt();
	}

	/**
	 * Finding the Max Value in array Using Stream
	 */
	public static int MaxUsesIntegerComparator(int[] a) {
		return Arrays.stream(a).max().getAsInt();
	}

	/**
	 * Is Number In Array
	 */
	public static boolean exist(int[] ints, int k) {
		return Arrays.asList(ints).contains(k);
	}

	/**
	 * Is Number In Array Using Stream
	 */
	public static boolean exist2(int[] ints, int k) {
		return IntStream.of(ints).anyMatch(x -> x == k);
		//return Arrays.stream(ints).anyMatch(x -> x == k);
	}

	/**
	 * is Twin
	 */
	public static boolean isTwin(String a, String b) {
		char[] first = a.toLowerCase().toCharArray();
		char[] second = b.toLowerCase().toCharArray();

		Arrays.sort(first);
		Arrays.sort(second);

		return Arrays.equals(first, second);
	}

	/**
	 * Bad calculator
	 */
	static BigDecimal sum(String... numbers) {
		BigDecimal sum = new BigDecimal(0);
		for (String number : numbers) {
			sum = sum.add(new BigDecimal(number));
		}

		return sum;
	}

	/**
	 * Computes the position of the dancer: Kariakoo
	 * Algorithm
	 * 
	 * stage(n) = stage(n-1) - stage(n-2) 
	 * pos(n) = pos(n-1) + stage(n) At stage 4,
	 * the dancer is at position -5.
	 */
	static int getPositionAt(int n) {
		int nopp = 6;
		int[] pp = { 0, 1, -1, -4, -5, -3 };

		return pp[n % nopp];
	}

}

class AsciiArt {
	public static String printChar(char s) {
		return "S";
	}
}

class Node {
	Node left, right;
	int value;

	public Node(int value) {
		this.value = value;
	}

	public Node add(int value) {
		if (value < this.value)
			if (this.left != null)
				return this.left.add(value);
			else
				return this.left = new Node(value);
		if (value > this.value)
			if (this.right != null)
				return this.right.add(value);
			else
				return this.right = new Node(value);
		return this;
	}

	public Node find(int v) {
		if (this == null || v == value)
			return this;
		else if (value > v && this.left != null)
			return left.find(v);
		else if (value < v && this.right != null)
			return right.find(v);
		else
			return null;
	}

	public int findSmallestValue() {
		return this.left == null ? this.value : this.left.findSmallestValue();
	}

	public void traverseInOrder() {
		if (this.left != null)
			this.left.traverseInOrder();
		System.out.print(" " + this.value);
		if (this.right != null)
			this.right.traverseInOrder();
	}

	public void traversePreOrder() {
		System.out.print(" " + this.value);
		if (this.left != null)
			this.left.traversePreOrder();
		if (this.right != null)
			this.right.traversePreOrder();
	}

	public void traversePostOrder() {
		if (this.left != null)
			this.left.traversePostOrder();
		if (this.right != null)
			this.right.traversePostOrder();
		System.out.print(" " + this.value);
	}
}

class Change {
	long coin2 = 0;
	long bill5 = 0;
	long bill10 = 0;
}

class ChangeSolution {

	static void printResult(Change m, long s) {
		// Change m = Solution2.optimalChange(s);

		System.out.println();
		if (m == null)
			System.out.println("given money " + s + " return null");
		else {
			System.out.println("Coin(s)  2€: " + m.coin2);
			System.out.println("Bill(s)  5€: " + m.bill5);
			System.out.println("Bill(s) 10€: " + m.bill10);
		}
	}

	// Do not modify this method signature
	static Change optimalChange(long s) {

		// Integral values
		long remaining = 0;
		long NbrOfBill10 = 0;
		long NbrOfBill5 = 0;
		long NbrOfCoin2 = 0;

		NbrOfBill10 = s / 10;
		remaining = s % 10;

		NbrOfBill5 = remaining / 5;
		remaining = remaining % 5;

		if (remaining >= 2) {
			NbrOfCoin2 = remaining / 2;
			remaining = remaining % 2;
		}

		// return null if change cannot be rendered
		if (remaining != 0)
			return null;

		Change change = new Change();
		change.coin2 = NbrOfCoin2;
		change.bill5 = NbrOfBill5;
		change.bill10 = NbrOfBill10;

		return change;
	}

}
