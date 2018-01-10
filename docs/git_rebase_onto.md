# Git rebase --onto の使い方
## 使用するケース
ある程度大きな機能を開発する際に

- 機能のためのベースブランチを master(develop) から切った
- ベースブランチからtopicブランチを複数切って、ベースブランチに対してPRを出す

のような開発の進め方はよくあると思います。

その際に、master(develop)に対する変更を内容が新機能のブランチに
必要になった場合に、`git rebase --onto` はとても役に立ちます。

### 初期状態

```
A --- B --- C --- D develop
       \
        E --- F base
               \
                G --- H topic
```

はじめの状態のコミットツリーです。
今回は、Dの変更がbase以下のブランチにも必要になったとします。

### base を rebase
base以下のブランチにDを取り込むためには色々方法がありますが、
今回は`git rebase` を使用します。

```
git rebase develop base
```

↑のコマンドを実行すると、コミットツリーは↓のようになります。

```
A --- B --- C --- D develop
       \           \
        \           E' --- F' base
         \
          E --- F --- G --- H topic
```

EとFのコミットの代わりにE'とF'が作成されて、E'はDをポイントします。
この際に、コンフリクトが発生して、解消しているとします。

#### topic をrebase

topicブランチにもDの変更が必要です、また、topicブランチはbaseブランチから
派生する必要があるので、baseブランチに対してrebaseを行います。

```
git rebase base topic
```

topicブランチのコミットEは、developブランチのBから派生しているので、
E, F, G, Hのコミットを作り直す必要があります。
その際に、baseブランチをdevelopmentブランチにリベースする際に発生したコンフリクト
と同様のコンフリクトを再度解消する必要があります。
(E', F'を作り直すため)

たくさんtopicブランチが合った場合はこれは大変です。
そこで `git rebase --onto` を使用します。

```
git rebase --onto base F topic
# git rebase --onto base HEAD~2 topic
```

↑のコマンドを実行すると、GとHのコミットの代わりに、
G'とH'のコミットが作成されて、G'はF'を参照します。
ポイントは、2つ目に渡している引数のF ( または HEAD~2 )です。
これは、コミットFから先をbaseに紐付けるということを表しています。
その為、EとFのコミットは作り直されないので、コンフリクトも発生しない
ということです。

```
A --- B --- C --- D develop
                   \
                    E' --- F' base
                            \
                             G' --- H' topic
```


### まとめ
新機能を作成するときのbaseブランチに対するrebaseは`git rebase --onto`を使うと便利
