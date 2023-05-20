# 3　制御文

制御文はプログラムの動きをコントロールするためのものです

---

## 3.1 if文

~~~java
if(条件){
    処理1;
}else{
    処理2;
}
~~~

if文を使うとある**条件が満たされているかどうかによって処理を分岐させることができます**。
条件が満たされていれば処理1を行い、条件が満たされていなければ処理2を行います。

~~~java
if(条件1){
    処理1;
}else if(条件2){
    処理2;
}
~~~

`else if`は最初の条件が満たされていない場合、別のある条件(ここでは条件2)が満たされている場合、処理を行うことができます。
また、if文の条件部分には`boolean型`を返す式を書きます。この真偽値によって実行される文を切り替えることができます。

~~~java
boolean result = true;
int x = 3; 
int y = 3;
if(result){
    System.out.println("resultはtrueです");
}else{
    System.out.println("resultはfalseです");
}

if(x > 5){
    System.out.println("xは5より大きいです");
}else{
    System.out.println("xは5より小さいです");
}

if(x > y){
    System.out.println("xはyより大きいです");
}else if(x == y){
    System.out.println("xはyより等しいです");
}else{
    System.out.println("xはyより小さいです");
}
~~~

~~~text
resultはtrueです
xは5より小さいです
xはyより等しいです
~~~

---

## 3.2. switch文

~~~java
swicth(式){
    case 値1:
        値1にマッチした時の処理
        break;
    case 値2:
        値2にマッチした時の処理
        break;
    case 値3:
        値3にマッチした時の処理
        break;
    case default:
        どの値とも一致しなかったときに処理
        break;
}
~~~

switch文は処理を**値**で分岐させることができます。
switch文でマッチすることができる値の型は以下の通りです

+ char
+ byte
+ short
+ int
+ Integer
+ String

`default:`はswitch文に送られた整数が`case`のどの値とも一致しなかったときに処理されます。
また、caseの最後に`break;`を記述しない場合、次の`case`の中も処理してしまいます。

~~~java
int medal = 2;
switch(medal){
    case 1:
        System.out.println("Gold");
        break;
    case 2:
        System.out.println("Silver");
        break;
    case 3:
        System.out.println("Bronze");
        break;
    case default:
        System.out.println("None");
        break;
}
~~~

~~~text
Silver
~~~

上記のコードでは変数`medal`の値によって出力を変えています。
サンプルコードでは`medal = 2`なので、`case 2`の中の`System.out.println("Silver");`の処理を行います

### NullPointerException

switch文でマッチさせる値が`Null`だった場合、`NullPointerException`が投げられます。

---

## 3.3. 三項演算子

~~~java
条件式 ? マッチした場合の値 : マッチしなかった場合の値;
~~~

三項演算子はマッチするかどうかを判定する条件式とマッチした場合の値、マッチしなかった場合の値を指定する演算子です。
if-else文を簡略化した記述方法です。

if-else文を用いたサンプル:

~~~java
int a ;
int b = 20
if(b > 15){
    a = 10;
}else{
    a = -10;
}
System.out.println(a);
~~~

~~~java
10
~~~

三項演算子を用いたサンプル:

~~~java
int b = 20
int a = b > 15 ? 10 : -10;
System.out.println(a);
~~~

~~~java
実行結果：
10
~~~

## 3.4. switch式

Java 12から入った新しい要素としてswitch式というものがあります。
switch文とswitch式の違いはswitch式は値を返さないのに対し、switch式は値を返すというものです。`->`を使用することで、`:`と`break`の記述を省略できます。

~~~java

var n = swicth(式){
    case 値1 -> nに代入する値;
    case 値2 -> nに代入する値;
    case 値3 -> nに代入する値;
    case 値4 -> nに代入する値;
    default -> どの値とも一致しなかったときにnに代入する値;
}
~~~
