# Mysqlのインストール時に、Rootユーザのパスワードのプロンプトを出ないようにする。

Shellscriptなどでサーバをセットアップする際に
mysqlのインストール中に、rootユーザのパスワードを問い合わせるプロンプトが表示されると
そこで処理が終わってしまいます。

`debconf-set-selections`を使用することで、パスワードを事前に設定し、
インストール時に、インタラクティブなプロンプトを表示しないようにすることができます。

## debconf-set-selections とは

> debconf-set-selections can be used to pre-seed the debconf database
with answers, or to change answers in the database. Each question will
be marked as seen to prevent debconf from asking the question
interactively.

manをみると、事前に、deb packageのインストールの際に聞かれる質問に対する、答えを入力
しておくためのデータベースのようなもののようです。

## 使い方
> Reads from a file if a filename is given, otherwise from stdin.
`debconf-set-selections`はファイル名か標準入力を入力にもちます。

入力のフォーマットは

```
<package_name> <question_name> <question_type> <answer>
```

mysqlの場合は、mysql-server/root_password と mysql-server/root_password_again の2種類を
登録しておく必要があります。

```
# mysql-server-5.7の例
echo "mysql-server-5.7 mysql-server/root_password password my_password" | sudo debconf-set-selections
echo "mysql-server-5.7 mysql-server/root_password_again password my_password" | sudo debconf-set-selections
```

これで、mysql-serverのインストール時にrootのパスワードを問い合わせるプロンプト
を表示させずにインストールするようにできます。

```
sudo apt-get install -y \
  mysql-server-5.7 mysql-client-5.7 libmysqlclient-dev
```

