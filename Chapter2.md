# 2. 演算子

**演算子を使う事で、主に基本データ型の値に対する計算を行うことができます。**
演算子には**算術演算子, 論理演算子, 比較演算子, 代入演算子, ビット演算子**の5つがあります

***

## 2.1 演算子の種類

### 算術演算子

算術演算子は数値を取り扱うときに使う演算子です
|演算子|記入例 | 説明|
|---|---| ---|
|+| x + y | xとyを加算|
|-| x - y | xとyを減算|
|*| x * y | xとyを乗算|
|%| x % y | xをyで割った余りを求める|
|++| x++ | xの値を1増やした後にaの値を返す|
|++| ++x | xの値を返した後にaの値を1増やす|
|--| y-- | yの値を1減らした後にaの値を返す|
|--| --y | yの値を返した後にaの値を1減らす|

++、--演算子はインクリメント、デクリメント演算子といいます
変数の前に置く事を前置と言い、変数の後ろに置く事を後置と言います

サンプルコード:

~~~java
int a = 1 + 3; // a = 4
int b = 4 - 2; // b = 2
int c = 2 * 3; // c = 6
int d = 4 / 2; // d = 2
int e = 4 % 3; // e = 1

int f = 5;
f++;
System.out.println(f); //6
~~~

***

### 論理演算子

論理演算子はboolean型の値に対する操作を行う演算子です。
**必ずboolean型の値を返します。**
|演算子|記入例 | 説明|
|---|---| ---|
|!| !a | xがfalse場合にtrueを返し、xがtrue場合はfalseを返す|
|&&| x && y | xとyの両方がtrueの場合にtrueを返す|
| \|\|| x \|\| y | xとyのいずれかがtrueの場合にtrueを返す|
サンプルコード:

~~~java
boolean x = true;
boolean y = true;
boolean z = false;
System.out.println(x);      //true
System.out.println(!x);     //false
System.out.println(x && y); //true
System.out.println(x && z); //false
System.out.println(x || y); //true
System.out.println(x || z); //true
~~~

***

### 比較演算子

|演算子|記入例 | 説明|
|---|---| ---|
|==| x == y | xとyが等しい場合にtrueを返す|
|!=| x != y | xとyが等しくない場合にtrueを返す|
| >| x > y | xがyよりも大きい場合にtrueを返す|
| <| x < y | xがyよりも小さい場合にtrueを返す|
|>=| x >= y| xがyよりも大きいか等しい場合にtrueを返す|
|<=| x <= y| xがyよりも小さいか等しい場合にtrueを返す|

サンプルコード:

~~~java
System.out.println(1 == 1); //true
System.out.println(1 == 2); //false
System.out.println(1 != 1); //false
System.out.println(1 >  0); //true
System.out.println(1 <  2); //true
System.out.println(1 <= 1); //true
System.out.println(0 >= 1); //false
~~~

***

### 代入演算子

|演算子|記入例 | 説明|
|---|---| ---|
|= | x = 100 | xに100を代入 |
|+=| x += 1  | xにx+1の値を代入|
|-=| x += 2  | xにx-2の値を代入|
|*=| x += 3  | xにx\*3の値を代入|
|/=| x += 4  | xにx/4の値を代入|

サンプルコード:

~~~java
int a = 100;
System.out.println(a); // 100
a = 200;
System.out.println(a); // 200
a += 50;
System.out.println(a); // 250
~~~

***

### ビット演算子

|演算子|記入例 | 説明|
|---|---| ---|
|& | x & y | xとyのビットAND |
|\| | x \| y | xとyのビットOR |
|^ | x ^ y | xとyのビットXOR |
|~ | ~x  | xのビットを反転させる |

サンプルコード:

~~~java
int a = 0b00011; // 3
int b = 0b01010; //10

System.out.println(a & b); // 2
System.out.println(a | b); //11
System.out.println(a ^ b); // 9
System.out.println(~a);    //-4

~~~

***

## 2.2. 演算子の優先順位

上から優先されます

1. `X++` `X--` 後置インクリメント/デクリメント

2. `++X` `--X` `~` 前置インクリメント/デクリメント  NOT

3. `*` `/` `%`　乗算 除算 剰余

4. `+` `-`　加算 減算

5. `<<` `>>`　ビットシフト

6. `<` `>` `<=` `>=`　比較演算子

7. `==` `!=`　比較演算子

8. `&` AND

9. `^` XOR

10. `|` OR

11. `&&` 論理演算子(AND)

12. `||`　論理演算子(OR)

13. `?:` 三項演算子

14. 代入演算子全般

また、`()`の中身から優先されます。

~~~java
System.out.println(3 + 1 * 2);
System.out.println(5.0 / 4.0 >= 2);
System.out.println((10 + 20) / 5);
~~~

~~~java
実行結果：
5
false
6
~~~
