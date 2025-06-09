# Git まとめ

## 使うアプリケーション

- Git Bash
- GitHub
- WinAuth.exe（パスワード認証）

---

## 概要

- チーム開発便利
- ローカルリポジトリとリモートリポジトリ（GitHub）の 2 部構成
- ブランチ → リモートの順番
- ローカルリポジトリの大枠はワークツリー・ステージ・リポジトリ
- `.gitignore`ファイルで GitHub へアップしないファイルなどを指定できる

---

## 基本的な使い方（最初のアップの流れ）

1. Git bash で GitHub にアップしたいフォルダを Current ディレクトリに指定
2. `git add .`→`git commit`でローカルリポジトリ内にデータをアップ  
   ※`i`でメッセージ入力、`Esc`の後、`:wq`で確定
   ```sh
   git add .
   git commit
   ```
3. GitHub で新しいリモートリポジトリを作成（例: Practice2）
4. リモートリポジトリと紐づけ（URL は `git remote -v` でも確認可能）
   ```sh
   git remote add origin https://github.com/Haruaki-Ikushima/Practice2.git
   ```
5. ローカルリポジトリからリモートリポジトリにデータをアップ
   （origin はリモート名、master はブランチ名、-u で次回以降 `git push` だけで OK）
   ```sh
   git push -u origin master
   ```

## 基本的な使い方（2 回目以降）

1. Git bash で GitHub にアップしたいフォルダを Current ディレクトリに指定

2. 現在のブランチを確認

   ```sh
   git branch
   ```

3. もし別のブランチにしたい場合は切り替え

   ```sh
   git checkout ブランチ名
   ```

4. add → commit → push
   ```sh
   git add .
   git commit
   git push
   ```

## ワークツリーで変更を加え、やっぱり変更前に戻したいとき

&emsp;特定ファイルの変更を取り消す

```sh
git checkout ブランチ名
```

&emsp;特定ディレクトリの変更を取り消す

```sh
git checkout ブランチ名
```

&emsp; 全変更を取り消す

```sh
git checkout ブランチ名
```

## ステージの変更を取り消したいとき（git add を解除したいとき）

&emsp; 特定ファイルのステージ解除

```sh
git reset HEAD ファイル名
```

&emsp; 特定ディレクトリのステージ解除

```sh
git reset HEAD ディレクトリ名
```

&emsp; 全てのステージを解除

```sh
git reset HEAD .
```

※ ワークツリー（作業ツリー）には影響を与えません

## リポジトリにコミットしたものを修正したいとき

&emsp; コミットメッセージを変更するだけの場合は、次のコマンドを使います。  
※リモートリポジトリに Push していた場合は使わないでください。

```sh
git commit --amend
```

## ブランチ作成＆切り替え＆リモートにアップ

&emsp; ブランチの作成・切り替え・リモートへのアップロードは以下のように行います。

1. ブランチ作成

   ```sh
   git branch ブランチ名
   ```

2. ブランチの一覧表示＆現在のブランチ確認

   ```sh
   git branch
   git branch -a
   ```

3. ブランチの切り替え

   ```sh
   git checkout ブランチ名
   ```

   補足として、作成と切り替えを同時に行う場合

   ```sh
   git checkout -b 新ブランチ名
   ```

4. 新ブランチをリモートにアップロード

   ```sh
   git push origin ver1  # ver1は新ブランチ名
   ```

## エイリアスによりショートカットキー作成

&emsp;よく使うコマンドにエイリアス（短縮名）を設定して効率化できます。

```sh
git config --global alias.ci commit
git config --global alias.st status
git config --global alias.br branch
git config --global alias.co checkout
```

## 他の人が追加したリモートリポジトリの内容を自分のワークツリーに取り込む方法

### 1. フェッチ＆マージ

リモート名 `origin`、ブランチ名 `master` で変更があった場合の手順です。

1. **リモートリポジトリからローカルリポジトリにデータを取得（ワークツリーには反映されません）**

   ```sh
   git fetch origin
   ```

2. **取得した内容も含めて全ブランチ一覧を表示**

   ```sh
   git branch -a
   ```

3. **自分の今いるブランチ（例：master）に、origin/master の変更内容を取り込む**
   ```sh
   git merge origin/master
   ```
   > ※ `origin/master` には他の人が加えた変更が含まれています。

---

### 2. プル（fetch + merge を一度に実行）

リモート名 `origin`、ブランチ名 `master` で変更があった場合の手順です。

1. **フェッチとマージをまとめて実行**
   ```sh
   git pull origin master
   ```
   > ※ 現在どのブランチにいるかを把握している必要があります。

---

### ⚠️ 注意

- 同じファイルを複数人で編集すると、コンフリクト（競合）が発生するため注意してください。

## その他よく使う Git コマンド

- **現在の状態を確認**

  ```bash
  git status
  ```

- **git add する前の変更差分を確認**

  ```bash
  git diff
  ```

- **git add した後の変更差分を確認**

  ```bash
  git diff --staged
  ```

- **コミット時に変更内容も見れる（-v オプション付き）**

  ```bash
  git commit -v
  ```

- **コミット履歴を詳細に見る（日付・作成者・メッセージ）**

  ```bash
  git log
  ```

- **コミット履歴を 1 行ずつ簡易表示**

  ```bash
  git log --oneline
  ```

- **ファイルやディレクトリを削除する**

  ```bash
  git rm ファイル名
  git rm ディレクトリ名
  ```

- **ファイル名やディレクトリ名を変更する**

  ```bash
  git mv 旧ファイル名 新ファイル名
  ```

- **リモートリポジトリの一覧を表示**

  ```bash
  git remote
  ```

- **リモートリポジトリとその URL の一覧を表示**

  ```bash
  git remote -v
  ```

- **リモートリポジトリの詳細情報（URL や追跡ブランチ）を表示**

  ```bash
  git remote show origin
  ```

- **カレントディレクトリのファイル一覧を表示（Linux コマンド）**

  ```bash
  ls
  ```

- **ファイルの中身を表示（Linux コマンド）**

  ```bash
  cat ファイル名
  ```

- **リモート名を変更（ローカル内のみ）**

  ```bash
  git remote rename 旧リモート名 新リモート名
  ```

- **リモートリポジトリを削除（ローカル内のみ）**

  ```bash
  git remote rm リモート名
  ```

- **ブランチ名を変更（ローカルのみ）**

  ```bash
  git branch -m 新ブランチ名
  ```

- **ブランチを削除（ローカルのみ）**

  ```bash
  git branch -d ブランチ名      # 通常削除
  git branch -D ブランチ名      # 強制削除
  ```

- **リモートリポジトリからブランチを削除**
  ```bash
  git push リモート名 --delete ブランチ名
  ```
