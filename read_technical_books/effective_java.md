## 目的
実装やコードレビューの際に何が正しいのか迷うことがあるため、ベストプラクティスを身につけたい。  
特に例外処理。

## 第10章 例外
### 項目70 回復可能な状態にはチェックされる例外を、プログラミングエラーには実行時例外を使う
3種類の例外
- チェックされる例外：catchしなければコンパイルエラーになるもの  
  RuntimeExceptionとそのサブタイプではないもの（IOExceptionやSQLExceptionなど）  
- チェックされない例外：try-catch不要
  - 実行時例外：RuntimeExceptionとそのサブタイプ（NullPointerExceptionやArrayIndexOutOfBoundsExceptionなど）  
    →判断がつかない場合はこちらを使う  
  - エラー：StackOverflowErrorやOutOfMemoryErrorなど  
    try-catchを記載しても、catchすることができないので例外ハンドリングする必要なし  
    →JVMが使うものなのでErrorとそのサブタイプは自作しない

### 項目71 チェックされる例外を不必要に使うのを避ける
- オプショナルを返す  
  →例外クラスのように詳細情報を持たせられない

### 項目73 抽象概念に適した例外をスローする
- 下位レイヤでスローした例外→上位レイヤでキャッチ（元の例外情報も渡す）  
  →しかし乱用すべきでない。そもそも例外を避けるべき（パラメータチェックをするなど）。

### 項目75 詳細メッセージにエラー記録情報を含める
- 例外の原因となった全てのパラメータ値とフィールドの値を含める

### 項目76 エラーアトミック性に努める
- エラーアトミック：失敗したメソッド呼び出しは、オブジェクトをそのメソッドの呼び出し前の状態にしておくべき
  - 不変オブジェクトを設計する
  - パラメータの正当性チェックをする、オブジェクト変更する前に失敗させる
  - オブジェクトの一時的コピーに対して操作を行い、操作が完了したら一時コピーの内容で置き換える

### 感想
初めて読んでみた。「つまりどういうこと？」っていう状態になった。  
基礎知識不足（勉強したが忘れてしまった）もあると思う。  
コードで具体例が示してあったりするのかなと思ったがない。  
標準APIなどで読んでみようと思った。  
Optionalを使っている例は記憶上見たことがなく初めて知った。

### 参考
[Effective Java 第３版 「ほぼ全章」を「読みやすい日本語」で説明してみました。](https://qiita.com/nyandora/items/3e5ec76ca3881bc17924)
