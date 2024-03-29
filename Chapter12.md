# 12 修飾子

修飾子は、クラス、メソッド、フィールド、インターフェース、およびその他の要素の定義に使用されます。
使用方法は、要素の定義時に修飾子をキーワードとして指定することで行われます。

## 12.1. アクセス修飾子（Access Modifiers）

+ `public`: 他のクラスからアクセス可能
+ `protected`: 同一パッケージ内とサブクラスからアクセス可能
+ `default` (package-private): 同一パッケージ内からのみアクセス可能
+ `private`: 同一クラス内からのみアクセス可能

## 12.2. クラス・メソッド・フィールドのその他の修飾子

+ `static`: クラスレベルの修飾子。クラスに属し、インスタンスを生成せずに使用可能。
+ `final`: 変更不可。クラスの場合は継承不可、メソッドの場合はオーバーライド不可、フィールドの場合は再代入不可。
+ `abstract`: 抽象クラスまたは抽象メソッドを示す。インスタンス化不可で、派生クラスで具象化される必要がある。
+ `synchronized`: マルチスレッド環境での同期を保証するために使用される。
+ `transient`: シリアライズ（オブジェクトの状態を保存）時にフィールドの対象外とする。
+ `volatile`: マルチスレッド環境での変数のキャッシュを禁止し、直接メモリを読み書きする。
+ `native` : メソッド修飾子。cやcppで書かれた関数（ネイティブメソッド）を呼び出すことができる。

## 12.3. インターフェース関連の修飾子

+ `default`: インターフェース内のメソッドのデフォルト実装を提供する。
+ `static`: インターフェース内のメソッドを静的メソッドにする。
+ `private`: インターフェース内でのみ使用可能なプライベートメソッドを定義する。

## 12.4. メソッド引数の修飾子

+ `final`: メソッド内で引数の値を変更できなくする。

## 12.5. ジェネリクス関連の修飾子

+ `extends`: ジェネリクスの上限境界を定義する。クラスまたはインターフェースを指定して制約を設ける。
+ `super`: ジェネリクスの下限境界を定義する。クラスを指定して制約を設ける。

## 12.6. ファイナルクラスの修飾子

+ `strictfp`: 浮動小数点演算の正確性を保証する（通常の浮動小数点演算とは異なる場合がある）。

## 12.7. 一覧

|修飾子 | クラス| インターフェース | メソッド | コンストラクタ | ブロック | 変数 | 説明 | 
|---|---|---|---|---|---|---|---|
|public |○| ○| ○| ○| ×| ○| アクセス修飾子|
|protected |○| ○| ○| ○| ×| ○| アクセス修飾子|
|private |○| ○| ○| ○| ×| ○| アクセス修飾子|
|static |○| ○| ○| ×| ×| ○| スタティック修飾子|
|final |○| ×| ○| ×| ×| ○| ファイナル修飾子|
|abstract| ○| ○| ○| ×| ×| ×| 抽象修飾子|
|native |×| ×| ○| ×| ×| ×| ネイティブ修飾子|
|synchronized| ×| ×| ○| ×| ○| ×| 同期修飾子|
|transient |×| ×| ×| ×| ×| ○| 一時的修飾子|
|volatile| ×| ×| ×| ×| ×| ○| 揮発性修飾子|
|strictfp |○| ○| ○| ×| ×| ×| 厳密浮動小数修飾子|

>引用<https://www.tohoho-web.com/java/modifier.htm>
