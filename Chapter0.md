# 0. はじめに

このテキストはjavaに少しでも興味を持った人が気軽に触れられるようにしたテキストです
少しC言語を触れたことがある人や、電算テキストを読破した人なら多分余裕です。

***

## 0.1. Hello World

まずはjavaを動かしてみましょう
まず```Main.java```というファイルを作って、その``Main.java``のファイルの中に次のコードを書いてみましょう

~~~java
class Main{
    public static void main(String[] args){
        System.out.println("Hello World");//java
    }
}
~~~

次に先ほど書いたコードをコンパイルすると、コマンドラインに

~~~text
Hello World
~~~

と実行結果が出ると思います。
これがざっくりとしたjavaでのHello Worldのやり方になります。
***

## 0.2. 構造

この項では先ほど書いたコードの意味を説明していきたいと思います。
`package`については後ほど説明します。

~~~java
class Main{

}
~~~

この``class 名前{}``で囲まれた部分の事を**クラス**といいます。

~~~java
public static void main(String[] args){
    
}
~~~

次に``public static ~``で囲まれた部分を**メソッド**といい、
メソッドで囲まれた部分にやりたい処理を書きます
*この後の内容ではクラス部分とメソッド部分は省略します。

上記のコードでは``System.out.println("Hello World");``が処理にあたります
また、コードの中で ``//``とバックスラッシュを2つ入れることによって、**コメント**することができます。
(コメントとはプログラムに影響を与えずにかける注釈のことです)

**また、javaの決まりとして文末には必ずセミコロン``;``が必要となります**

```System.out.println()```は``()``の中身を出力せよという意味です。C言語の``printf()``と似たような物と考えていいです。
()の中は、文字列であれば``""``ダブルコーテーションで囲み、数値ならそのまま入れることができます。また、`()`の中に文字列が入っていれば``+``記号を使って連結することができます。
そして``()``の中では計算をすることができます。

`System.out.print()`と記述する事で、改行せずに出力をすることができます。

サンプルコード：

~~~java
System.out.print("Hello ");
System.out.println("world");
System.out.println("Hello " + "Java!");
System.out.println("Number :" + 10);
System.out.println("20" + "23");
System.out.println(20 + 23);
~~~

出力：

~~~java
Hello world
Hello Java!
Number : 10
2023
43
~~~

上記のコードの5行目と6行目の違いは20と23が文字列か数値であるかの違いです。
5行目は数字が``""``で囲まれているので文字列となります。よって``()``の中では文字列の連結として処理されます。
6行目は数字がそのまま書かれているので数値扱いとなります。よって``()``の中では数値の計算処理が行われます。
数値と文字列の違いは常に意識してコードを書いていきましょう。
***

## 0.3. mainメソッドの構造

この項はmainメソッドの構造について説明します。
~mainメソッドはおまじないのようなものなので、最初はこの構造の事をしらなくても良いと思います~

~~~java
public static void main(String args[]){
}
~~~

Javaの mainメソッドの宣言では、これらの条件をすべて満たしている必要があります。

+ アクセス修飾子
+ static修飾子
+ 戻り値
+ メソッド名
+ 引数

### アクセス修飾子

**<span style="color: red; ">public</span>** _static void main(String[] args)_
ここは必ず``public``である必要があり、publicはプログラムの公開範囲を意味していおり、public修飾子を付けたメソッドは、メソッドの定義元のクラスの外部、外側のコードからアクセスできるようになります。

### static修飾子

_public_ **<span style="color: red; ">static</span>** _void main(String[] args)_
static修飾子を付けたメソッドは、クラスを**インスタンス化**[^1]するこ
となくアクセスできるようになります。
static修飾子が付いているメソッドの事を静的メソッドと言います

### 戻り値

_public static_ **<span style="color: red; ">void</span>** _main(String[] args)_
mainメソッドの戻り値は必ず**void**[^2]でなければなりません。

### メソッド名

_public static void_ **<span style="color: red; ">main</span>** _(String[] args)_
メソッド名は必ず全小文字の`main`でなければなりません。
JVMが参照する識別子です。

### 引数

_public static void main_ **<span style="color: red; ">(String[] args)</span>**
メソッドの引数には`String型の配列`、または`String型の可変長引数`であることが必要です。
また、`args`はプログラムが実行されるときに渡される情報を意味しています。
***

## 0.4. javaファイルとclassファイル

前の項で`Main.java`内で`helloworld`を実行したと思いますが、コンパイルをした際に`Main.java`を作成したフォルダの中に`Main.class`が作成されたかと思います。Javaのプログラムを実行するために必要な処理だからです。
**Javaは<span style="color: #ff00ff; ">オブジェクト指向プログラミング言語</span>で、オブジェクトというものを定義して使います。オブジェクトはclassで定義されます。**

***
**Javaのプログラミングの基本的な流れは以下のようになります。**

1. ソースファイル（`.java`）を作成する
2. コンパイラ（`javac`）を使ってソースファイルをバイトコード（`.class`）に変換する
3. JVM[^3]を使ってバイトコード(`.class`)を実行する

[^1]: new演算子などを使いインスタンスを生成すること
[^2]: メソッドの処理結果を呼び出し元へ返す必要がない場合につける戻り値の型
[^3]: JavaVirtualMachineの略で、Javaで作成されたアプリケーションをWindowsやMacOSなどで動かすために必要となるアプリケーション
