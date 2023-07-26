# 12 スレッド

Javaはマルチスレッドプログラミングをサポートしており、複数のスレッドを同時に実行できるようになっています。

スレッドは、**プロセス内で独立した実行フローを持つ軽量のタスク**です。複数のスレッドを使用することで、マルチコアプロセッサの性能を最大限に活用し、タスクを並列で実行することができます。

## 12.1.　実装

Javaでスレッドを操作するためには、主に`Thread`クラスを使う方法と`Runnable`インターフェースを使うの2つの方法があります：

### 12.1.1. `Thread`クラスを直接使用する方法

Javaでは`Thread`クラスを拡張して新しいスレッドを作成します。以下は、この方法でスレッドを作成する例です。

```java
public class MyThread extends Thread {
    @Override
    public void run() {
        // スレッドで実行したい処理を記述
    }
}
// スレッドの起動
MyThread thread = new MyThread();
thread.start(); // スレッドの実行開始
```

この方法では、`run()`メソッドにスレッドで実行したい処理を記述します。`start()`メソッドを呼び出すことで、新しいスレッドが作成されて`run()`メソッドが実行されます。

### 12.1.2. `Runnable`インタフェースを実装する方法

`Runnable`インタフェースは、スレッドが実行するためのタスクを表すために使用されます。以下は、この方法でスレッドを作成する例です。

```java
public class MyRunnable implements Runnable {
    @Override
    public void run() {
        // スレッドで実行したい処理を記述
    }
}

// スレッドの起動
MyRunnable myRunnable = new MyRunnable();
Thread thread = new Thread(myRunnable);
thread.start(); // スレッドの実行開始
```

この方法では、`run()`メソッドにスレッドで実行したい処理を記述します。そして、`Thread`クラスのコンストラクタに`Runnable`インタフェースを実装したオブジェクトを渡して新しいスレッドを作成します。

## 12.2.　注意点

- スレッドは並行処理を行うため、同じリソースに対して複数のスレッドからアクセスされる可能性があります。そのため、適切な同期処理を行わないとデータの競合や不整合が発生することがあります。
- `Thread`クラスの`run()`メソッドではなく、`start()`メソッドを使用してスレッドを実行する必要があります。`run()`メソッドを直接呼び出すと、新しいスレッドが作成されず、単なるメソッド呼び出しになってしまいます。
- スレッドはリソースを消費するため、過剰にスレッドを作成するとパフォーマンスが低下する可能性があります。必要な数のスレッドを適切に管理することが重要です。

## 12.3.サンプルコード

以下のサンプルコードは1から100までの数を2つのスレッドで同時に合計するプログラムです。

```java
public class ParallelProcessingSample {
   private static final int MAX_NUMBER = 100; // 上限
   private static final int HALF_NUMBER = MAX_NUMBER / 2;
   private static volatile int sum = 0; // volatileキーワードを使ってスレッド間の可視性を保証

   public static void main(String[] args) {
      // 2つのスレッドを作成して処理を並列実行
      Thread thread1 = new Thread(() -> sumNumbersInRange(1, HALF_NUMBER));
      Thread thread2 = new Thread(() -> sumNumbersInRange((HALF_NUMBER + 1),  MAX_NUMBER));

      thread1.start(); // スレッド1の実行開始
      thread2.start(); // スレッド2の実行開始

      // 両スレッドの終了を待つ
      try {
         thread1.join();
         thread2.join();
      } catch (InterruptedException e) {
         e.printStackTrace();
      }

      // 合計値を表示
      System.out.println("合計: " + sum); //5050
   }

   private static void sumNumbersInRange(int start, int end) {
      int localSum = 0;
      for (int i = start; i <= end; i++) {
         localSum += i;
      }
      // 各スレッドの合計値を全体の合計値に追加
      synchronized (ParallelProcessingSample.class) {
         sum += localSum;
      }
   }
}
``````
