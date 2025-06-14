# JUnit まとめ

## 概要

- **JUnit**は、Java 専用のテスティングフレームワークです。
- アノテーションを使い、クラスの関数や例外処理が正しく行えるか簡単に評価できます。
- @Test アノテーションをつけ、戻り型は void

---

## カバレッジ（網羅率）について

- **命令網羅**

  - すべての処理（命令）を 1 回以上実行すること

- **分岐網羅**

  - すべての分岐（if や switch）について、真と偽の両方を試すこと
  - 例: `if(A||B)` なら、A||B が真になる場合と偽になる場合の両パターンをテスト

- **条件網羅**
  - 各条件の真偽を個別に試すこと
  - 例: `if(A||B)` なら、A の真・偽、B の真・偽をそれぞれテスト

<div align="center">
  <img src="../../image/JUnit/代表的なカバレッジ.png" alt="カバレッジの説明" style="width:70%;">
</div>

## テスト用フォルダの場所

<div align="center">
  <img src="../../image/JUnit/テスト用フォルダの場所.png" alt="テスト用フォルダの場所" style="width:70%;">
</div>

## テスト作成手順

1. **パッケージ・エクスプローラーで新規ソースフォルダ作成**

   - パッケージ・エクスプローラー上で右クリック
   - 「新規」→「ソースフォルダー」を選択
   - フォルダ名に `test` を入力して作成

2. **テストクラスの作成**

   - 作成した `test` フォルダを右クリック
   - 「新規」→「クラス」でテスト用クラスを作成

3. **テストメソッドのひな形をテンプレートで作成**

   - エディタ上で `Ctrl + 9` を押す
   - テストメソッドのひな形が自動で挿入される
   - 「スーパークラス」の入力欄は空白のままで OK

4. **テストコードを記述**

   - `@Test` アノテーションをつけてテストメソッドを作成
   - 例：

     ```java
     import org.junit.jupiter.api.Test;

     class SampleTest {
         @Test
         void testSample() {
             // テストコードを書く
         }
     }
     ```

5. **テストの実行**
   - パッケージ・エクスプローラーでテストクラスを右クリック
   - 「実行」→「JUnit テスト」を選択

---

## 有名なテスト用のアサーション

&emsp;JUnit には、テスト結果を判定するためのアサーションメソッドがいくつかあります。ここでは代表的なものをまとめます。

---

## assertEquals(期待値、実測値)

&emsp;期待値と実測値が等しいときにテスト成功

<div align="center">
  <img src="../../image/JUnit/assertEquals.png" alt="assertEquals" style="width:50%;">
</div>

---

## assertThrows(発生するであろう例外のクラス名、テスト対象の処理をラムダ式で書く)

&emsp;指定した例外が発生することを確認したい場合に使います

<div align="center">
  <img src="../../image/JUnit/assertThrows.png" alt="assertThrows" style="width:50%;">
</div>

---

## fail("失敗時のメッセージ"※任意)

&emsp;強制的に失敗させたいとき、例外が発生しているか確認する用途などで使います

<div align="center">
  <img src="../../image/JUnit/fail.png" alt="fail" style="width:50%;">
</div>

---

## ほかにも以下のようなアサーションメソッドあるよ

<div align="center">
  <img src="../../image/JUnit/other_assert.png" alt="other_assert" style="width:50%;">
</div>

## テストケースの構造化

- `@Nested`を付与することで、テストクラス内にネストされたクラスを作成し、テストケースを階層的に整理できます。
- 同じメソッドに対して条件分岐やパターンごとに複数のテストを行いたいときに便利です。

<div align="center">
  <img src="../../image/JUnit/Nested.png" alt="Nested" style="width:50%;">
</div>

---

## タグ付け

- `@Tag`アノテーションを使うことで、テストにラベル（タグ）をつけることができます。
- 実行時にタグでフィルタリングし、特定のテストだけを選んで実行することが可能です。
- Eclipse の場合は、テストクラスを右クリック →「実行」→「実行の構成」→「タグの包含・除外」でカテゴライズできます。

<div align="center">
  <img src="../../image/JUnit/Tag.png" alt="Tag" style="width:50%;">
</div>

---

## 共有フィクスチャ

- `@BeforeEach`を付与したメソッドは「セットアップメソッド」と呼ばれます。
- 各テストメソッドの実行前に毎回自動で呼び出され、テストの準備処理（初期化など）を共通化できます。

<div align="center">
  <img src="../../image/JUnit/BeforeEach.png" alt="BeforeEach" style="width:50%;">
</div>

## 事前条件の記述

&emsp;JUnit では、特定の条件下でのみテストを実行したい場合や、一時的にテストを無効化したい場合に便利な仕組みが用意されています。

---

### assumeTrue

- `assumeTrue` は、指定した条件が **true** の場合のみテストを続行します。
- 条件が **false** になると、後続のテスト処理はスキップされます。

<div align="center">
  <img src="../../image/JUnit/assumeTrue.png" alt="assumeTrue" style="width:50%;">
</div>

---

### assumingThat

- `assumingThat` は、第一引数の条件が **true** の場合のみ、第二引数（ラムダ式）内の処理を実行します。
- 条件が **false** の場合は、第二引数の処理は実行されませんが、テスト自体はスキップされません。

<div align="center">
  <img src="../../image/JUnit/assumingThat.png" alt="assumingThat" style="width:50%;">
</div>

---

### @Disabled

- `@Disabled` アノテーションを使うと、そのテストメソッド（またはクラス）を実行時に無効化（スキップ）できます。
- 一時的にテストを実行したくない場合などに便利です。

<div align="center">
  <img src="../../image/JUnit/Disabled.png" alt="Disabled" style="width:50%;">
</div>

### パラメータ化テスト

#### @ParameterizedTest

&emsp;パラメータ化テスト用のメソッドに付与します。

#### @ValueSource

&emsp;`String`、`int`、`long`、`double`などの配列を指定し、配列の要素を先頭から順番にテストメソッドへ渡します。

#### @CsvSource 　　

&emsp;カンマ区切り文字列の配列を指定し、配列の前から順番にテスト

<div align="center">
  <img src="../../image/JUnit/CsvSource.png" alt="CsvSource" style="width:50%;">
</div>
