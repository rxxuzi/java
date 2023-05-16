# 10. 継承

Javaではすでに存在しているクラスをもとにして、新しいメソッドやフィールドを追加したり、上書きしたりして、新しいクラスを宣言する事ができます。

## 10.1. クラスの継承

javaにおけるクラスの継承とは、あるクラスが別のクラスのメンバー（フィールドやメソッド）を受け継ぐことができるオブジェクト指向の特徴の一つです。継承元のクラスを**スーパークラス**、継承先のクラスを**サブクラス**と呼びます

クラスの継承を行う場合には下記のように記述します

~~~java
class サブクラスの名前 extends スーパークラスの名前{

}
~~~

Javaでは多重継承をサポートしていないのでクラスの継承は一度に1つしか出来ません。

---
例として次のようなコードがあったとします。

~~~java
class calculatorA{
    int i = 100;
    public void add(){
        i ++;
    }
    public void view(){
        System.out.println(i);
    }
    public void delete(){
        i = 0;
    }
}

class calculatorB {
    int i = 100;
    public void add(){
        i++
    }
    public void view(){
        System.out.println(i);
    }
    public void set(){
        i = 10000;
    }
}
~~~

`calculatorA`と`calculatorB`ではそれぞれ異なる特徴があるとします。
ただ、この例ではフィールド変数`i`と`add`メソッドと`view`メソッドの基本的な機能はどちらも同じです。
2つのクラスをそれぞれ別々に設計すれば同じ機能があるにも関わらずどちらも同じ記述をしなければいけない部分が出てきてしまいます。

そこで`calculator`としての基本的な設計部分は共通して、異なる部分だけをそれぞれのクラスで追加して設計すれば便利です。
このような場合に、基本となるクラスを**スーパークラス**と言います。例えば下記のようなスーパークラス`calculatorS`を作成してみます。

~~~java
class calculatorS{
    int i = 100;
    public void add(){
        i ++;
    }
    public void view(){
        System.out.println(i);
    }
}

class calculatorA extends calculatorS{
    public void delete(){
        i = 0;
    }
}

class calculatorB extends calculatorS {
    public void set(){
        i = 10000;
    }
}
~~~

結構スッキリしましたね。
継承を使用することで、スーパークラスで定義されたプロパティやメソッドをそのまま受け継ぎつつ、サブクラスで独自の**プロパティ**や**メソッド**を追加することができます。これにより、コードの再利用性が高まり、効率的な開発が可能になります

## 10.2. Override

`Override`とは、サブクラスがスーパークラスから継承したメソッドを**再定義**することを指します。これにより、**サブクラス固有の振る舞いを実装することができます。**

Javaでは、`@Override`アノテーションを使用して、メソッドがオーバーライドされていることを明示的に示すことができます。このアノテーションは、コンパイラによってチェックされ、オーバーライドされるべきメソッドが存在しない場合は、コンパイルエラーが発生します。

メソッドをオーバーライドするには、サブクラスで**メソッドの名前が等しく、引数列の型が等しいメソッド**を宣言する必要があります。
メソッド名と引数列の型の事をメソッドの**シグニチャ**といいます

~~~java
class S {
    public void print() {
        System.out.println("I am the superclass");
    }
}

class A extends S {
    @Override
    public void print() {
        System.out.println("I am class A");
    }
}

A a = new A();
a.print(); // prints "I am class A"
~~~

### 10.2.a Overload

また、オーバーライドと似ている単語としてJavaにオーバーロード(Overload)というものがあります。
オーバーライドはスーパークラスのメソッド定義を上書きする事ですが、オーバーロードは同じ名前と異なる引数を持つメソッドを多数宣言する事です。

~~~java
class A {
    public void print(int x) {   //   (1)
        System.out.println(x);
    }
    public void print(String s) { //   (2)
        System.out.println(s);
    }
    public void print(String s1 , String s2) {  //   (3)
        System.out.println(s1 + s2);
    }
}

A a = new A();
//int型の引数を受け取っているので(1)のふるまいをする
a.print(1);  
//String型の引数を受け取っているので(2)のふるまいをする
a.print("hello"); 
~~~

~~~java
出力：
1
Hello
~~~

## 10.3. 継承時のアクセス制御

メンバ変数やメンバメソッドに対するアクセス制限に関しては`public`を付けた場合(又はアクセスに関する修飾子を省略した場合)は、クラス外からでも直接アクセスが可能です。また`private`を付けた場合はクラス内からしかアクセスが出来ません。
従って`private`修飾子を付けたメソッドや変数はサブクラスで継承できません

~~~java
class S{
    private int i = 100;// class Aで継承できない
    public int j = 200; // class Aで継承できる
    int k = 300;        // class Aで継承できる
}

class A extends S {
    /*
        code
    */
}

~~~

## 10.4. Super

`super`は、Javaにおいて、サブクラスからスーパークラスのメンバー（フィールドやメソッド）にアクセスするために使用されるキーワードです。

サブクラス内では、`super`を使用して、スーパークラスのメソッドを呼び出すこともできます。これは、サブクラスが継承したメソッドをオーバーライドした場合に特に便利です。

~~~java
class S {
    public void print() {
        System.out.println("I am the superclass");
    }
}

class A extends S {
    @Override
    public void print() {
        super.print(); // class Sのprint()を実行
        System.out.println("I am class A");
    }
}

A a = new A();
a.print();

~~~

~~~text
出力；
I am the superclass
I am class A
~~~

上記の例では、`class A`は、継承した`print()`メソッドをオーバーライドしています。その中で、`super.print()`を使用して、スーパークラスのメソッドを呼び出しています。そのため、`class A`のインスタンスでは、オーバーライドされたメソッドが呼び出されると同時に、スーパークラスのメソッドも呼び出されます。

## 10.5. サンプル

~~~java
public class Example02 {
    public static void main(String[] args) {
        A1 a1 = new A1(); //インスタンス化
        B1 b1 = new B1(); //インスタンス化
        System.out.println("Before");

        System.out.println("a1.i = " + a1.i); //class A1のint i
        System.out.println("a1.s = " + a1.s); //class A1のString s
        System.out.println("a1.j = " + a1.j); //class A1のint j

        System.out.println("b1.i = " + b1.i); //class B1のint i
        System.out.println("b1.s = " + b1.s); //class B1のString s
        System.out.println("b1.k = " + b1.k); //class B1のint k

        a1.add(50); // i += 50;
        a1.add("I'm A"); // s = "I'm A";
        a1.add(); // j += 100;

        b1.add(1000); // i += 100;
        b1.add("I'm B"); // s = "I'm B";
        b1.remove(); // k -= 100;

        System.out.println("After");
        System.out.println("a1.i = " + a1.i);
        System.out.println("a1.s = " + a1.s);
        System.out.println("a1.j = " + a1.j);
        System.out.println("b1.i = " + b1.i);
        System.out.println("b1.s = " + b1.s);
        System.out.println("b1.k = " + b1.k);

        a1.print(); // Override していないので　"Super Class"と出力される
        b1.print(); // Override しているので　"Sub Class"と出力される

    }
}
class S1{
    //スーパークラスのフィールド
    int i = 0;
    String s = "nothing";

    public void add(int i){
        this.i += i;
    }
    public void add(String s){ 
        this.s = s;
    }
    public void print(){
        System.out.println("I'm Super Class");
    }
}
class A1 extends S1{
    //サブクラスのフィールド
    int j = 0; //継承されていない
    public void add(){ //オーバーロード
        j += 100;
    }
}

class B1 extends S1{
    //サブクラスのフィールド
    int k = 0;
    public void remove(){
        k -= 100;
    }
    //Overrideしてprintメソッドを書き換えている
    @Override
    public void print() {
        System.out.println("I'm Sub Class");
    }
}
~~~

出力:

~~~text
Before
a1.i = 0
a1.s = nothing
a1.j = 0
b1.i = 0
b1.s = nothing
b1.k = 0
After
a1.i = 50
a1.s = I'm A
a1.j = 100
b1.i = 1000
b1.s = I'm B
b1.k = -100
I'm Super Class
I'm Sub Class
~~~
