# 6　配列

**配列とは、同じ型の要素を複数まとめて扱うことのできるデータ構造です。**

## 6.1.　定義, 宣言

~~~java
要素型[] 変数名 = new 要素型[配列サイズ];
要素型[] 変数名 = new 要素型[]{要素0,要素1,要素2....};
~~~

配列に含まれる要素は0から順番に並べられています。この番号を**インデックス**といいます。このインデックスを用いて配列中の要素の取得や更新を行います。ただ、**配列のサイズは一度生成すると後から変更することができません**

また、すべての要素は同じ型である必要があります。
配列の要素の型は、**基本データ型と参照型どちらも使うことができます**。

~~~java

int[] a = {1,2,3,4,5};

int[] b = new int[5];//配列の宣言
for (int i = 0; i < b.length; i++) {
    b[i] = i+1; // インデックスiごとにi+1の値を代入
}
int[] c = new int[]{1,2,3,4,5};

System.out.println(a[0]);
System.out.println(b[1]);
System.out.println(c[2]);
~~~

~~~java
実行結果：
1
2
3
~~~

配列は宣言・生成した段階で、配列の各要素に予め初期値が設定されます。そのためコンパイルエラーになりません。初期値は、配列の型により異なります。

|配列型|初期値|
|--|--|
|intなどの数値型|0|
|boolean|false|
|参照型|null|

~~~java
int[] a = new int[10];
System.out.println(a[9]);
String[] b = new String[10];
System.out.println(b[9]);
~~~

~~~java
実行結果：
0
null
~~~

次のように、配列に対して要素数より大きいインデックスにアクセスしようとすると
`ArrayIndexOutOfBoundsException`が投げられます

~~~java
int[] a = new int[]{1,2,3,4,5};
System.out.println(a[5]);
~~~

~~~
Exception in thread "main" java.lang.ArrayIndexOutOfBoundsException: Index 5 out of bounds for length 5 
~~~

また、配列の要素の数をは**lengthフィールド**から取得することができます。

~~~java
String[] str = new String[]{"Red" , "Green" , "Blue"};
System.out.println(str.length);
int a[] arr = new int[10];
System.out.println(arr.length);
~~~

~~~java
実行結果：
3
10
~~~

## 6.2. 多次元配列

配列の要素として配列を扱うこともできます。
2次元配列の場合は

~~~java
要素型[][] 変数名 = new 要素型[配列サイズ][配列サイズ];
要素型[][] 変数名 = new 要素型[][]{要素0,要素1..}{要素0,要素1..};
~~~

と宣言します

~~~java

int[][] p = new int[][]{
    { 0, 1, 2, 3},
    { 4, 5, 6, 7},
    { 8, 9,10,11},
    {12,13,14,15}
};

System.out.println(p[0][3]);
System.out.println(p[3][2]);
~~~

~~~java
実行結果：
3
14
~~~

## 6.3. ArrayList


