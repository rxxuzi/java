# 5.例外処理

**例外処理とはプログラムの実行中に想定外の事態や事象が発生したときに、その対応を記述したコードのことです**
これを行う事でプログラムの安全性を高めることができます

## 5.0. 例外

Javaの例外は**Throwableクラス**を継承した**Errorクラス**と、**Exceptionクラス**に分類されます。

+ **Errorクラス**は、**プログラムで対処できない重大なエラー**を表します。
例えば、`OutOfMemoryError`や`ClassFormatError`などがあります。

+ **Exceptionクラス**は、**プログラムで対処できる可能性のあるエラー**を表します。
例えば、IOExceptionやNullPointerExceptionなどがあります

**Exceptionクラス**はさらに、**検査例外**と**非検査例外**に分けられます。

+ **検査例外**は**コンパイル時にチェックされる例外**で、try-catch文やthrows宣言で処理しなければなりません。
+ **非検査例外**は**コンパイル時にチェックされない例外**で、RuntimeExceptionクラスのサブクラスです

**よく使われる検査例外**
| 例外 | 投げるケース |
| ----|----|
|IOException|ファイル入出力に関するエラーが発生するケース|
|SQLException| データベース操作に関するエラーが発生するケース|

**よく使われる非検査例外**
| 例外 | 投げるケース |
| ----|----|
|IllegalArgumentException| メソッドが呼び出された際に引数の値が正しくないケース|
|NullPointerException| nullが禁止されている引数にnullが渡されるケース|
|IndexOutOfBoundsException|配列やリストなどのコレクションから範囲外の要素を取得しようするケース|
|ArithmeticException| 算術演算で不正な値が発生したケース|

## 5.1. throw

**throwとは、エラーを発生させるためのキーワードです。**
例外クラスのインスタンスを作成して`throw`することで、エラーを表現できます。

~~~java
throw new 例外クラス(メッセージ);
~~~

***

## 5.2. try catch

**try-catchとは、エラーが発生する可能性のあるコードブロックをtryで囲み、catchの中でエラーが発生した場合に行いたい処理を行う為の文です**

~~~java
try {
  // 例外が発生する可能性のある処理
} catch (例外クラス 変数名) {
  // 例外が発生した時の処理
}

try {
  // 例外が発生する可能性のある処理
} catch (例外クラス 変数名) {
  // 例外が発生した時の処理
} finally {
    //必ず実行される処理
}
~~~

`try`ブロックには例外が発生する可能性のあるコードを記述し、
`catch`ブロックには例外が発生したときに実行するコードを記述しています。
`finally`ブロックには、最後に必ず実行するコードを記述しています。
これらのブロックは、プログラムの安全性や可読性を高めるために重要です

~~~java
int person = 0;
int candy = 100;
try {
    candy = 100 / person; //ゼロ除算エラー
    System.out.println("candy / person : " + candy);
} catch (ArithmeticException e) {
    System.out.println("例外が発生しました");
    System.out.println(e);
} finally {
    System.out.println("person : " + person);
}
~~~

~~~java
実行結果：
例外が発生しました
java.lang.ArithmeticException: / by zero
person : 0
~~~

上記のコードを見てみましょう。
変数`candy`に`100 / 0`を入れようとしていますね。数学において0で割ってはいけないというルールがある為、`100/0`をしようとするとエラーが起きてしまいます。
そこで、エラーの可能性がある`candy = 100 / person`を`try`で囲み、`catch`にエラーが起きてしまった時の処理を書きます。上記のコードではエラーが起きた時にスローされた`java.lang.ArithmeticException: / by zero`という例外を出力しています。
`finally`で囲まれた処理は例外が発生してもしなくても必ず実行されます。主にファイルをcloseしたい時などに使われます。

## 5.3. throws

**throwsは、メソッドの宣言の後に記述するキーワードで、そのメソッドが発生させる可能性のある例外を列挙することができます。**
`throws`を使うと、そのメソッドを呼び出す側に例外処理を任せることができます。

~~~java
void something() throws Exception {
  // 例外が発生する可能性のあるコード
}
~~~

また、`throws`キーワードは複数書けます。メソッドが発生させる可能性のある例外の種類が複数ある場合は、カンマ`,`で区切って列挙することができます

~~~java
import java.io.FileNotFoundException;
import java.io.FileReader;
public class Main {
    public static void main(String[] args) {
    String fpath = "Sample.txt";//読み込みたいファイルパス
    try {
        readFile(fpath);//readFileメソッドにパスを投げる
    } catch (Exception e) {
        //　ファイルが無かった場合の処理
    }

    }
    public static void readFile(String path) throws FileNotFoundException {
        FileReader r = new FileReader(path);
        /* 
        *ファイル読み込み処理
        */

    }   
}
~~~

上記のコードはmainメソッドから`readFile`メソッドで`FileReader`クラスを使用しているのでエラー処理を実施する必要があります。

例外処理は`throws`を使って呼び出し元のクラスに投げています。
throwsで呼び出し元のクラスに例外処理を投げた後の処理は中止され、例外処理をmainメソッドでcatchしてその後処理をしています。

## 5.4. 例外の読み方

`Main.java`で以下のコードを実行しようとするとエラーが投げられます。

~~~java
public class Main {
    public static void main(String[] args) {
        String str = null;
        System.out.println(str.length());
    }
}
~~~

~~~java
実行結果：
Exception in thread "main" java.lang.NullPointerException: Cannot invoke "String.length()" because "str" is null at Main.main(Main.java:4)
~~~

上記のコードは、文字列`str`の長さを出す`.length()`メソッドを呼び出そうとしていますが、`str`が`null`なので、エラーが出てしまっています。

`Exception in thread "main" java.lang.NullPointerException: ~~`
この部分では`NullPointerException`というエラーの内容がわかります。
`at Main.main(Main.java:4)`
次に、この部分ではエラーが起きた箇所を明示しています。サンプルの場合だと、
「`Main`というクラスの`main`メソッドの中でエラーが発生してます。またそのエラーは`Main.java`というファイルの4行目にあります。」という意味です

エラーメッセージは次のような形を取ります。

``at クラス名.メソッド名(ファイル名.java: エラーが起きた行)``

``at パッケージ名.クラス名.メソッド名(ファイル名.java: エラーが起きた行)``
