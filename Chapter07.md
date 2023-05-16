# 7.標準入力

**コマンドラインからの入力を受け取ってプログラムをより動的にする為に標準入力を行います。**

---

## 7.1. Scanner

Javaにおいて、標準入力を受け取るためには`java.util.Scanner`クラスを使用します。Scannerクラスは、コマンドラインからの入力、ファイルからの入力、または文字列からの入力を受け取ることができます。

```java
/*
コマンドラインから文字列を受け取って、"Hello (文字列)"と出力するコード
*/
import java.util.Scanner;
public class Main{
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.println("Your Name");
        String str = sc.nextLine();
        System.out.println("Hello " + str);
        sc.close();
    }
}

```

```java
入力：
Java!
出力：
Hello Java!
```

---

```java
import java.util.Scanner;
```

上記のサンプルコードではまず、`Scanner`クラスをインポートしています。
`Scanner`クラスは`java.utilパッケージ`にあるクラスで、コマンドラインからの入力やファイルからの入力を読み込んだり、指定した型の値を構文解析したりするために使います。
また、

```java
import java.util.*;
```

とアスタリスク`*`をつけることで、`java.utilパッケージ`にある全てのクラスをインポートする事ができます。
**Javaの慣習として、import文はソースコードの先頭に、パッケージ宣言の下に記述します**

---

```java
Scanner sc = new Scanner(System.in);
```

この行ではScannerクラスのインスタンスを作成しています。

Scannerクラスのインスタンスを作成するときには、`System.in`をコンストラクタの引数に指定します。このコードではScannerクラスのインスタンスを参照する変数名を`sc`にしています。

Javaの`new`キーワードは、クラスのインスタンスを作成するときに使います。つまり、**新しいオブジェクトのためにメモリを割り当てて、そのメモリへの参照を返す**ということです。

---

```java
String str = sc.nextLine();
```

この行では文字列の変数`str`に入力された文字列を代入しています。

Scannerクラスは、次のような一連のメソッドを提供しています。

+ `next()`: スペースや改行までの次のトークンを読み込みます。
+ `nextLine()`: 次の行までの文字列を読み込みます。
+ `nextInt()`: 次の整数を読み込みます。
+ `nextDouble()`: 次の浮動小数点数を読み込みます。
+ `hasNext()`: 次のトークンが存在するかどうかを判断します。
+ `close()`: 入力ストリームを閉じます。

---

```java
sc.close();
```

この行ではScannerクラスの`close()`メソッドを呼び出してScannerを閉じています。
`close`メソッドを呼び出すことで。リソースの解放やエラーの回避などができます

他のメソッドについてはOracle公式ページを参考にしてください。
[Oracle公式ページ Scannerクラス](https://docs.oracle.com/javase/jp/8/docs/api/java/util/Scanner.html)
