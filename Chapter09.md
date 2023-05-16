# 9. コレクション

List, Set, Mapについて説明します

+ `List`は、要素を順番に保存していくデータ構造です。

+ `Set`は要素の重複を許さないデータ構造です。

+ `Map`はキーと呼ばれる要素とそのキーに対応した値を保存するためのデータ構造です

## 9.1. List

`List`は、配列に似たデータ構造で、**動的**に要素数を変更することができます。
`List`に格納される要素は、インデックスによってアクセスすることができます。

Listは、`java.utilパッケージ`に属しているので、使用する際にはインポートする必要があります。
``List``には`ArrayList`、`LinkedList`などのクラスが実装されています。

+ ArrayList
    内部的に配列を使用したリストの実装クラス
    リスト中の要素へのアクセス処理を高速で行うことができる
    要素の追加や削除にコストが掛かる

+ LinkedList
    内部的に連結リストを使用したリストの実装クラス
    要素へのアクセス処理はコストが高い
    要素の追加や削除の処理は高速で行うことができる

それぞれのクラスには、`Listインターフェース`を実装しているため、同じような方法で使用することができます。

リストオブジェクトを作成するには以下のように宣言します

~~~java
new オブジェクト名<ジェネリクス>();

//例
new ArrayList<Integer>();
new LinkedList<String>();
~~~

以下は、`ArrayList`を使用したListの例です。
ArrayListは、**可変長の配列として実装されており**、**要素の追加や削除が高速に行えます。**

~~~java

import java.util.ArrayList;
import java.util.List;

public class Example {
    public static void main(String[] args) {
        // Listの作成
        List<String> language = new ArrayList<String>();
        // 要素の追加
        language.add("java");
        language.add("c++");
        language.add("python");
        language.add("scala");

        // 要素の取得
        String item = language.get(1);  // item に "c++" を代入
        System.out.println(item);   

        // 要素の削除
        language.remove(2);  // "python"を削除

        // 要素数を取得
        int size = language.size();  // 3

        // 要素のループ (拡張for文)
        for (String s : language) {
            System.out.println("Hello " + s);
        }

        // 要素の書き換え
        language.set(2,"kotlin"); // 要素(2)のscalaをkotolinに書き換え
        System.out.println(language);
    }
}

~~~

出力：

~~~text
c++
Hello java
Hello c++
Hello scala
[java, c++, kotlin]

~~~

宣言の仕方

~~~java

List<String> list = new ArrayList<String>();
~~~

上記の例では、Listはインターフェースであり、ArrayListはListインターフェースを実装した**クラス**です。`<String>`は、**Listに格納される要素の型**を示しています。
この場合、文字列を格納するために`String`を使用しています。

---

## 9.2. Set

`Set`は、集合論の概念に基づいており、要素の順序は保証されません。
また、`Set`は、要素の重複を許可しないため、同じ値を複数回格納することはできません。

JavaのSetには、`java.utilパッケージ`に含まれる`HashSet`、`TreeSet`、`LinkedHashSet`などがあります。
それぞれのクラスには、`Setインターフェース`を実装しているため、同じような方法で使用することができます。

以下は、`HashSet`を使用したSetの例です。`HashSet`は、**要素の追加や削除が高速に行えます。**

~~~java
import java.util.HashSet;
import java.util.Set;

public class Example {
    public static void main(String[] args) {
        // 宣言
        Set<String> set = new HashSet<String>();

        // 要素の追加 (要素数 = 4)
        set.add("java");
        set.add("c++");
        set.add("python");
        set.add("html");
        
        // 要素の取得
        String element = "c++";
        boolean contains = set.contains(element);  // true
        if(contains) { //true
            System.out.println(element + " is included in the set");
        }else{
            System.out.println(element + " is not included in the set");
        }

        // 要素の削除
        set.remove("python");

        // 要素の数を取得
        int size = set.size();  // removeしたので3
        System.out.println(size);
        
        boolean isE = set.isEmpty(); //false
        
        if(!isE) { // !false -> true
            // 要素のループ(拡張for文)
            for (String s : set) {
                System.out.println(s);
            }
        }
        
    }
}

~~~

~~~text
c++ is included in the set
3
c++
java
html

~~~

---

## 9.3. Map

Javaの`Map`は、キーと値のペアを格納するデータ構造であり、キーを使って値にアクセスすることができます。
`Map`は、`java.utilパッケージ`に含まれるクラスであり、`HashMap`、`TreeMap`、`LinkedHashMap`などがあります。
それぞれのクラスには、`Mapインターフェース`を実装しているため、同じような方法で使用することができます。

以下は`HashMap`を使用したMapの例です。HashMapは、**キーと値の追加、取得、削除が高速に行えます。**

~~~java

import java.util.HashMap;
import java.util.Map;

public class Example {
    public static void main(String[] args) {
        // 宣言
        Map<String, Integer> map = new HashMap<String, Integer>();

        // 要素の追加
        map.put("A", 100);
        map.put("B", 200);
        map.put("C", 300);

        // 要素の取得
        int value = map.get("A");  // 100

        // 要素の削除
        map.remove("B");

        // 要素の数を取得
        int size = map.size();  // 2

        // キーのループ
        for (String key : map.keySet()) {
            System.out.println(key + " : " + map.get(key));
        }
    }
}

~~~
