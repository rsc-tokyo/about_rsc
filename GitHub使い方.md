# GitHubの基本的な使い方
ここでは登録やセットアップ、初歩的な使い方について説明します。
  
下記の通り実行しても上手くいかないときはターミナルに表示されたメッセージをGoogle検索してみてください。
  
なお、ポリコネの関係で最近「master」が「main」に変更となりました。検索結果で「master」と解説されているコマンドは「main」と読み替えて実行すると上手くいくことを覚えておいてください。
参考：https://qiita.com/hikaru_/items/dc875b27a515f9ee9284

## GitHubを使う上での基礎知識
### 1.ローカルリポジトリとリモートリポジトリ
リポジトリとは、ファイルやディレクトリの状態を保存する場所です。
  
変更履歴を管理したいディレクトリなどをリポジトリの管理下に置くことで、そのディレクトリ内のファイルなどの変更履歴を記録することができます。
  
リポジトリは自分のマシン内にある「ローカルリポジトリ」とサーバなどネットワーク上にある「リモートリポジトリ」の2カ所にあります。
  
基本的にローカルリポジトリで作業を行い、その作業内容をリモートポジトリへプッシュする流れで行います。
### 2.コミット(commit)とプッシュ(push)
コミット(commit)
  
ファイルの追加や変更の履歴をリポジトリに保存すること
  
プッシュ(push)
  
ファイルの追加や変更の履歴をリモートリポジトリにアップロードするための操作
### 3.ブランチ（branch）
ソフトウェアの開発では、現在リリースしてるバージョンのメンテナンスをしながら新たな機能追加やバグ修正を行うことがあります。
  
このような、並行して行われる複数のバージョン管理を行うために、Gitにはブランチ（branch）という機能があります。
  
ブランチは履歴の流れを分岐して記録していくものです。
  
分岐したブランチは他のブランチの影響を受けないため、同じリポジトリ内でそれぞれの開発を行っていくことができます。
### 4.インデックス（index）
リポジトリ管理下にあるディレクトリの中には、一時的に使うファイルなど、Git管理が不要なものもあります。
  
そこでGitでは、バージョン管理する対象のファイルやフォルダを「インデックス」と呼ばれる台帳に登録することで、必要なもののみバージョン管理が行えるようになっています。
  
逆に言えば、新たにフォルダやファイルを作成した場合、コミットする前にインデックスに登録する必要があります。

## Gitをインストールする
https://git-scm.com/ からWindows用のインストーラをダウンロードする。
  
インストーラを実行する。
  
下部に Only show new options があればチェックを外してください
  
License は Next して頂きまして、
  
Select Component では [Git LSF (Large File Support)] と [Associate .git* ..... } のみにチェックを入れてください
  
Additional icons や Windows Explorer integration などは要らないかと思います
  
次にエディタを選択しますが、ここは [ Use Visual Studio Code as Git's dafault editor ] で良いかと思います
  
次はデフォルトのブランチ名を設定します。[ Override the default... ] にして、 main と入れておくといいかと思います。
  
次に 3 つの選択肢があります
  
[ Git from the command line and also from 3rd-party software ] を選択してください
  
VS Code や Powershell から使えるようになります。
  
[ Choosing HTTPS transport backend ] の画面ではどちらを選択してもいいです。
  
Git に付属する OpenSSL を使うか、 Windows 内蔵の Windows Secure Channel のどちらか。おすすめはWindows に入っている証明書などがそのまま使えるので Windows Secure Channel。
  
次は改行コードの設定ですが、ここは一番下の [ Checkout as-is, commit as-is ] で良いかと思います。
  
チェックアウト時コミット時に改行コードを変換するかどうかですが、何もしないのが無難かと思います。
  
次は Git Bash のコンソールウィンドウの設定です。ここは [ Use Windows' default console window ] で良いです。
  
次は git pull の扱いですが、そのまま [ Default ] で良いです
  
次は資格情報ヘルパーの選択、[ Git Credential Manager Core ] で。
  
次は追加設定、 [ Enable file system caching ] のみチェックを入れてください。
  
次の Experimental はチェックなしのままでいいです
  
それで [ Install ] しちゃってください
  
インストールが完了したら、新しく Powershell か コマンドプロンプト を開いてgit --versionでバージョン情報が表示されればイケる感じ
```PowerShell
PS C:\Users\user\Documents\git\rsc_test_repository> git --version
git version 2.32.0.windows.1
```
## GitHubのアカウント登録
GitHubのトップページにアクセスします。
  
メールアドレスを入力し、緑色の「Sign up for GitHub」ボタンをクリックします。
  
次の画面でUsername（ユーザー名）やPassword（パスワード）を入力します。
  
登録したメールアドレスに認証のメールが届きます。
  
メールの内容に従いユーザー認証を行ってください。
  
以上でGitHubのアカウント登録は完了です。

## GitHubの基本的な使い方(リポジトリの作成と同期)
「1」の作成は初回のみ行い、「2」から「5」を繰り返します。
  
基本的に小さい作業の単位でコミットを行い、ある程度作業がひと段落した時にプッシュをするのが一般的です。
  
コミットの作業がわかりやすいように、コミットメッセージを残しておくと、ログを追っていく時に役立ちますので覚えておきましょう。
### 1.Githubでリポジトリを作成（git init）
まずはリポジトリを作成します。
  
GitHubにログインした状態で以下にアクセスします。
  
https://github.com/new
  
次に表示される画面では、「Repository name」の入力のあと、必要に応じて「Description」も入力します。
  
また、リポジトリの種類を「Public」か「Private」を選択します。
  
ソースコードを公開したくない場合は「Private」を選択すると良いでしょう。
  
最後に、リポジトリの中にあらかじめREADMEファイルを作成しておく場合は「Initialize this repository with a README」にチェックを入れます。
  
.gitignoreやlicenseについては後で追加や変更ができるので、Noneを選択します。
  
必要項目の入力が終わり「Create repository」ボタンをクリックするとリポジトリの作成は完了です。
  
次の画面で、リモートリポジトリのアドレスが表示されますので、控えておいてください。

はじめに、ローカルのPC上にローカルリポジトリを作成します。
  
今回は「hogehoge」というディレクトリを作成することにします。
  
以下の操作はWindowsであればPowerShell、Macであればターミナルで行います。
  
コマンドは1行ずつ、最後にEnterキーを押して入力しましょう。
mkdir hogehoge
実行結果
```PowerShell
PS C:\Users\user\Documents\git> mkdir hogehoge


    ディレクトリ: C:\Users\user\Documents\git


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
d-----        2021/10/24     15:47                hogehoge
```
cd hogehoge
実行結果
```PowerShell
PS C:\Users\user\Documents\git> cd hogehoge
PS C:\Users\user\Documents\git\hogehoge>
```
git init
実行結果
```PowerShell
PS C:\Users\user\Documents\git\hogehoge> git init
Initialized empty Git repository in C:/Users/user/Documents/git/hogehoge/.git/
```
「mkdir」は新しくディレクトリを作成するコマンド。ここではhogehogeというディレクトリを作成している。
  
「cd」はディレクトリを移動するコマンド。ここではhogehogeというディレクトリに移動している。
  
「git init」コマンドはGitリポジトリを新たに作成するコマンドです。バージョン管理を行っていない既存のプロジェクトをGitリポジトリに変換する場合や、空の新規リポジトリを作成して初期化する場合に使用します。git initコマンドを実行するとカレントディレクトリをGitリポジトリに変換します。

git pullしてGitHub上のリモートリポジトリをローカルリポジトリと同期させる
  
参考：https://qiita.com/Takao_/items/5e563d5ea61d2829e497
```PowerShell
PS C:\Users\user\Documents\git\hogehoge> git pull origin main
From https://github.com/example-user/hogehoge
 * branch            main       -> FETCH_HEAD
fatal: refusing to merge unrelated histories
```
git mergeして同期させる
  
参考：https://qiita.com/mei28/items/85bc881ac1f26332ac15
```PowerShell
PS C:\Users\user\Documents\git\hogehoge> git merge --allow-unrelated-histories origin/main
Merge made by the 'recursive' strategy.
 README.md | 2 ++
 1 file changed, 2 insertions(+)
 create mode 100644 README.md
```
### 2.ファイルの作成/変更/削除をgitのインデックスに追加する（git add）
メモ帳等でhogehoge.txtというテキストファイルをhogehogeに作成する。
そしてaddコマンドで追加する。
実行結果
```PowerShell
PS C:\Users\user\Documents\git\hogehoge> git add hogehoge.txt
```
現在の状態を確認しましょう。
git status
実行結果
```PowerShell
PS C:\Users\user\Documents\git\hogehoge> git status
On branch main

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   hogehoge.txt
```
addせずにstatusを実行すると下記のようになる
```PowerShell
PS C:\Users\user\Documents\git\rsc_test_repository> git status
On branch main

No commits yet

nothing to commit (create/copy files and use "git add" to track)
```
### 3.変更結果をローカルリポジトリにコミットする（git commit）
まずはメールアドレスと名前を下記コマンドで登録する。
"example-user@hogehoge.com"と"example-user"は自分のものに読み替えてください。
```PowerShell
PS C:\Users\user\Documents\git\hogehoge> git config --global user.email "example-user@hogehoge.com"
```
```PowerShell
PS C:\Users\user\Documents\git\hogehoge> git config --global user.name "example-user"
```
登録を怠ると、コミット実行時に下記のようなエラーが出る
  
参考：https://yutaka-gakushu.com/tips/git/author-identity-unknown-error
```PowerShell
PS C:\Users\user\Documents\git\hogehoge> git commit -m "add new file"
Author identity unknown

*** Please tell me who you are.

Run

  git config --global user.email "you@example.com"
  git config --global user.name "Your Name"

to set your account's default identity.
Omit --global to set the identity only in this repository.

fatal: unable to auto-detect email address (got '【ユーザー名】@【コンピューター名】.(none)')
```
次に、インデックスに追加されたファイルをコミットします。
  
※コミットとは、ファイルやディレクトリの追加や変更をリポジトリに記録する操作のことです。
```PowerShell
PS C:\Users\user\Documents\git\hogehoge> git commit -m "add new file"
[main (root-commit) 3a7b40a] add new file
 1 file changed, 9 insertions(+)
 create mode 100644 hogehoge.txt
```
これで、リポジトリに対してファイルの追加が記録されました。
  
再度状況を確認します。結果は以下のようになります。
  
これはすべてのファイルがコミット済みの状態を表しています。
```PowerShell
PS C:\Users\user\Documents\git\hogehoge> git status
On branch main
nothing to commit, working tree clean
```
さらに、リモートリポジトリに反映させる前に、リモートリポジトリの情報を追加します。この情報は、先ほどGitHub上に表示された、リモートリポジトリのアドレスです。今回は例を示していますので「https://github.com/example-user/hogehoge.git」 の部分をご自身のリモートリポジトリのものに置き換えて実行しましょう。
  
リモートリポジトリのアドレスの確認方法は次ページの通り
  
参考：https://reasonable-code.com/github-collaborators/

git remote add origin https://github.com/example-user/hogehoge.git
### 4.ローカルリポジトリをプッシュしてリモートリポジトリへ反映させる（git push）
まずfetchを実行する
```PowerShell
PS C:\Users\user\Documents\git\hogehoge> git fetch
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), 621 bytes | 47.00 KiB/s, done.
From https://github.com/example-user/hogehoge
 * [new branch]      main       -> origin/main
```
ローカルリポジトリの変更を、GitHub上にあるリモートリポジトリに反映させるため、以下のコマンドを実行します。
初回実行時はGitHubへのログインが必要となる。
ここでは「1」を入力しエンターキーを押すとブラウザにジャンプし、ログインボタンが表示されるのでログインする。
```PowerShell
PS C:\Users\user\Documents\git\hogehoge> git push origin main
Select an authentication method for 'https://github.com/':
  1. Web browser (default)
  2. Personal access token
option (enter for default): 1
info: please complete authentication in your browser...
Enumerating objects: 6, done.
Counting objects: 100% (6/6), done.
Delta compression using up to 16 threads
Compressing objects: 100% (4/4), done.
Writing objects: 100% (5/5), 578 bytes | 578.00 KiB/s, done.
Total 5 (delta 0), reused 0 (delta 0), pack-reused 0
To https://github.com/example-user/hogehoge.git
   4af5fd0..fa45540  main -> main
```
下記のようにリジェクトされた場合は1で説明したgit pullとgit mergeを実行しGitHub上のリモートリポジトリをローカルリポジトリと同期させる
```PowerShell
PS C:\Users\user\Documents\git\rsc_test_repository> git push origin main
To https://github.com/example-user/hogehoge.git
 ! [rejected]        main -> main (fetch first)
error: failed to push some refs to 'https://github.com/example-user/hogehoge.git'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```
これで、GitHubへプッシュしてリモートリポジトリへ反映させることができました。
### 5.ファイルの変更/削除をgitのインデックスに追加する（git add）
リモートリポジトリに存在するファイルをローカルで編集した場合、コメントを追記しないとpushできない。
まずはコメントを追加する。
```PowerShell
PS C:\Users\user\Documents\git\hogehoge> git commit -a -m "２行目にコメントを追加"
[main c8e3665] ２行目にコメントを追加
 1 file changed, 19 insertions(+), 1 deletion(-)
 ```
次にプッシュする。
```PowerShell
PS C:\Users\user\Documents\git\hogehoge> git push origin main
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 16 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 647 bytes | 647.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
To https://github.com/example-user/hogehoge.git
   fa45540..c8e3665  main -> main
```
コメントを追記していないとプッシュしても下記のようになる。
```PowerShell
PS C:\Users\user\Documents\git\hogehoge> git push origin main
Everything up-to-date
```
## GitHubの基本的な使い方(ブランチの使い方)
基本的な使い方が分かったところで、実際の開発現場でよく利用されているブランチ（branch）の使い方について見ていきましょう。
  
ブランチは並行して行われる複数のバージョン管理を行うための仕組みです。
  
基本的には以下のような手順で利用します。
  
ブランチの作成、移動
  
ブランチ内での開発作業
  
ブランチにプッシュ
  
ブランチからプル
  
ブランチのマージ
  
ブランチの削除

### ブランチの作成、移動
まずはgit branchで現在のブランチ一覧を見ていきましょう。
実行結果は以下のようになります。
```PowerShell
PS C:\Users\user\Documents\git\hogehoge> git branch
* main
```
作業中のブランチには「*」が付きます。
これで、現在のブランチが master だけであり、作業中のブランチもmasterであることが分かります。

それではブランチを作成してみましょう。
今回は「sub1」というブランチを作成します。
```PowerShell
PS C:\Users\user\Documents\git\hogehoge> git branch sub1
```
ブランチの移動は、checkoutコマンドで行います。
```PowerShell
PS C:\Users\user\Documents\git\hogehoge> git checkout sub1
Switched to branch 'sub1'
```
なお、ブランチの作成と移動は、以下のコマンドでまとめて行うこともできます。
```PowerShell
PS C:\Users\user\Documents\git\hogehoge> git checkout sub1
```
ここで再び、現在のブランチ一覧を見てみましょう。
```PowerShell
PS C:\Users\user\Documents\git\hogehoge> git branch
  main
* sub1
```
sub1ブランチが追加され、作業中であることが分かります。

### ブランチ内での開発作業
次にブランチ内で開発作業を行っていきます。
とは言ってもなんら変わることはありません。
例として、hogehoge2.txtというファイルを作成してみます。

### ブランチにプッシュ
作成したファイルをgitに追加します。
```PowerShell
PS C:\Users\user\Documents\git\hogehoge> git add hogehoge2.txt
```
確認します。この操作は省略できます。
```PowerShell
PS C:\Users\user\Documents\git\hogehoge> git status
On branch sub1
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   hogehoge2.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        "GitHub\344\275\277\343\201\204\346\226\271.md"
```
作成したファイルをgitにコミットします。
```PowerShell
PS C:\Users\user\Documents\git\hogehoge> git commit -m "add file hogehoge2.txt"
[sub1 79f788b] add file hogehoge2.txt
 1 file changed, 9 insertions(+)
 create mode 100644 hogehoge2.txt
```
確認します。この操作は省略できます。
```PowerShell
PS C:\Users\user\Documents\git\hogehoge> git status
On branch sub1
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        "GitHub\344\275\277\343\201\204\346\226\271.md"

nothing added to commit but untracked files present (use "git add" to track)
```
これで、ローカルリポジトリに対してファイルの追加が記録されました。
  
では、リモートリポジトリに反映させてみましょう。
  
リモートリポジトリの情報は登録済みですので、ブランチ名を指定するだけで、プッシュできます。
```PowerShell
PS C:\Users\user\Documents\git\hogehoge> git push origin sub1
Enumerating objects: 4, done.
Counting objects: 100% (4/4), done.
Delta compression using up to 16 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 389 bytes | 389.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
remote:
remote: Create a pull request for 'sub1' on GitHub by visiting:
remote:      https://github.com/example-user/hogehoge/pull/new/sub1
remote:
To https://github.com/example-user/hogehoge.git
 * [new branch]      sub1 -> sub1
```
GitHubで確認してみると、現在2つのブランチが存在し、sub1ブランチがプッシュされていることが分かりますね。

### ブランチからプル
それでは、他の開発者がsub1リポジトリで開発するにはどうしたら良いでしょうか。

このような共同開発でこそ、gitは威力を発揮します。

この場合、プルコマンドを使って簡単に実現できます。

※以下、他の開発者が、同じGitHubで共同開発しており、masterブランチをチェックアウトしているとします。

まずは、リポジトリsub1にチェックアウトします。
```PowerShell
git checkout sub1
```
実行結果は以下のようになります。

チェックアウトしたブランチsub1が、リモートブランチのsub1に対応していることが分かります。

次にリモートブランチsub1のコードを取得します。
```PowerShell
git pull
```

ローカルファイルの一覧を見ていきましょう。
```PowerShell
ls
```
実行結果は以下のようになります。

たったこれだけで、複数の開発者による共同開発をはじめることができます。

### ブランチのマージ
実際の開発現場では、新機能をブランチを作って開発を行い、テストが完了したら、メインのmasterブランチに取り込む、という流れで開発作業を行います。

このブランチに取り込む作業のことをマージといいます。

具体的な手順は以下のとおりです。

まず、作業中のブランチをmasterに切り替えます。
```PowerShell
PS C:\Users\user\Documents\git\hogehoge> git checkout main
Switched to branch 'main'
```
```PowerShell
PS C:\Users\user\Documents\git\hogehoge> git branch
* main
  sub1
```
次に、sub1ブランチの作業結果をマージします。実行結果は以下のようになります。
  
sub1ブランチで作成したhogehoge2.txtファイルが追加されたことが分かりますね。
```PowerShell
PS C:\Users\user\Documents\git\hogehoge> git merge sub1
Updating f8d3777..79f788b
Fast-forward
 hogehoge2.txt | 9 +++++++++
 1 file changed, 9 insertions(+)
 create mode 100644 hogehoge2.txt
```
GitHubにプッシュしてみましょう。
```PowerShell
PS C:\Users\user\Documents\git\hogehoge> git push origin main
Total 0 (delta 0), reused 0 (delta 0), pack-reused 0
To https://github.com/example-user/hogehoge.git
   f8d3777..79f788b  main -> main
```
これで、ブランチsub1の内容がmasterにマージされました。

### ブランチの削除
使わなくなったブランチは削除することができます。
  
ただし、実際の開発現場では、間違って作成してしまった場合を除き、作業が完了したブランチであっても残しておくことが一般的です。
  
ブランチの削除は以下のコマンドで行います。
```PowerShell
PS C:\Users\user\Documents\git\hogehoge> git branch -d sub1
Deleted branch sub1 (was 79f788b).
```
結果を見てみましょう。
  
実行結果は以下のようになります。
ブランチsub1が削除され、masterだけが存在していることが分かります。
```PowerShell
PS C:\Users\user\Documents\git\hogehoge> git branch
* main
```