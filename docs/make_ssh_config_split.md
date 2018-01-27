# SSHのコンフィグを複数OSで使い分ける

先日 OSXが HightSierraにアップグレードした後に
sshの設定ファイルに、`UseKeychain yes` を追加したわけですが
(参考: [macOS SierraでSSH鍵のパスフレーズの件](https://qiita.com/d6rkaiz/items/efb085b1a2eb3fddd70e))
その後で、LINUXも使い始めました。

sshの設定ファイルはLINUXとOSXで共有したかったのですが、どうも
この`UseKeychain`のオプションが ssh configにあると、LINUX側では
エラーが出てしまいます。
そこで、SSHのconfigを共通部分と、OS固有な部分に分けて、OS毎に
使い分けましょう。


## ssh configの Include を使用して複数ファイルに分離する
ssh configでは、 Include を使用して他のファイルを読み込むことができるみたいです。
そこで、`~/.ssh/config.Linux` と `~/.ssh/config.Darwin` を作成しましょう。

### config.Linux

```
Include common_conf
Include hosts/*
```

### config.Darwin

```
Hosts *
  UseKeychain yes
Include common_conf
Include hosts/*
```

違いは、`config.Darwin`には、`UseKeychain yes` が入っているところです。

### common_conf
`AddKeysToAgent yes`や、`TCPKeepAlive yes`などの共通で使用する設定を入れておきます。

### hosts/*
host毎にファイルを作っても良いですし、project毎とかでファイルを作っても良いです。

## 分離したconfigを読み込んでsshできるか確認する
ssh には -F という configを指定するためのオプションがあるので、
それを使用して、分離したあとも設定が壊れていないことを確認します。

```
ssh -F ~/.ssh/config.Linux <some_host>
```

自分は `IdentityFile`のパスを 絶対パスで書いており、OSXだと`/Users/bob`
LINUXだと `/home/bob` なので、はじめ失敗しました :-(
相対パスに書き換えて対応できます。

## sshコマンドにaliasを貼って、configを指定しなくても良いように変更する
このままだと、sshコマンドを実行する際に、毎回 `-F`のオプションを指定しなければなりませんが、
それは不便です。そこで、aliasを設定しておきます。

```
alias ssh="ssh -F ~/.ssh/config.$(uname)"
```

`uname`コマンドは、オプションを渡さない場合 OSXだと`Darwin` LINUXだと `Linux` になるので、
上のaliasを用意しておくだけで対応可能です。

これで、SSHのコンフィグを複数OSで使いまわすことができるようになりました。

## 参考
[Includeキーワードでssh_configを分割できるようになった件](https://qiita.com/masa0x80/items/ecb692ad93f7d06a07b0)

