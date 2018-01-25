# Let's encryptの証明書を、新しいサーバに移行する
## はじめに
Let's encryptで証明書を運用している場合に、
あるサーバから別のサーバに証明書を移したいケースがあります。
その際に、必要なファイルを移行する方法です。

## 1. 現在運用中のサーバにログインして、/etc/letsencryptをtarに固める

```
cd /etc/letsencrypt
tar pzcvf /tmp/letsencrypt.tar.gz ./*
```

`p`: パーミッションを保持する設定です。


## 2. 固めたファイルをローカルにコピーする

```
scp <old host>:/tmp/letsencrypt.tar.gz ./
```

## 3. ローカルにコピーしたファイルを新しいサーバにアップロードする

```
scp ./letsencrypt.tar.gz <new host>:/tmp/
```

## 4. アップロードしたファイルを /etc配下に移動する

```
sudo mv /tmp/letsencrypt.tar.gz /etc/
```

## 5. tarを解凍する


```
sudo tar pxvf letsencrypt.tar.gz
```

`tree`コマンドで結果を確認できます。

```
sudo tree letsencrypt
```

## 6. 不要な設定は削除する

例えば以前のサーバで複数の証明書を使用していた場合は、それらの設定も一緒に
移行されているので、必要な証明書の設定だけ残します。


```
sudo rm -fr /etc/letsencrypt/live/<domain to be removed>/
sudo rm -fr /etc/letsencrypt/archived/<domain to be removed>/
sudo rm -fr /etc/letsencrypt/renewal/<domain to be removed>.conf
```

## 7. 証明書の自動更新の設定をする

```
sudo crontab -e
```

※ certbotにはroot権限が必要なので、rootのcrontabを編集します
1ヶ月毎くらいに更新するようにしておけば良いと思います。

```
30 2 * * 1 <certbotのフルパス> renew >> /var/log/le-renew.log
35 2 * * 1 <nginxなどのパス> reload
```

※ 設定内容は環境によって異なります
<certbotのフルパス>は `/usr/bin/certbot` など
<nginxなどのフルパス>は `/etc/init.d/nginx` など

