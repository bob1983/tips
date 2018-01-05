# Vimの操作に関するメモ

## 編集
### テキストオブジェクト
ノーマルモードで`viw`や`via`などを入力すると、
現在カーソルがある単語が選択された状態になる

```
# 例
users = [ { name: 'Taro', age: 10 }, { name: 'Jiro', age: 7 } ]
# Taroの上のどこかにカーソルを合わせた状態で
# vi'を入力するとTaroが選択された状態になる
# va'を入力すると'Taro'が選択された状態になる
# iはテキストオブジェクト内部, aはテキストオブジェクト全体を表す

# { }の間で vi{を入力すると` name: 'Taro', age: 10 `が選択された状態に
# { }の間で va{を入力すると`{ name: 'Taro', age: 10 }`が選択された状態になる

```

#### vim-surround [plugin](https://github.com/tpope/vim-surround)

### Indent

```
# insert mode
Ctrl-t             # インデントを一段階上げる
Ctrl-d             # インデントを一段階上げる

# normal mode
>>                 # インデントを一段階上げる
<<                 # インデントを一段階下げる

# visual mode
>                  # インデントを一段階上げる
<                  # インデントを一段階下げる
```

## バッファ

```
:ls                # buffer一覧の表示
:b <buffer_name>   # 対象のバッファに移動
:b <buffer_number> # 対象のバッファに移動
# ※buffer_nameにはタブ補完も使える
:b#                # 以前に編集していたバッファに移動
```

### kill buffer [plugin](https://github.com/qpkorr/vim-bufkill)
vim-bufkillでウィンドウの状態を保持しつつバッファをクリアできる

```
:BUN               # 対象のファイルをHiddenに
:BD                # 対象のファイルをバッファから削除
```

## Ctags

```
Ctrl-]             # 定義元へ移動
Ctrl-t             # 前の場所に戻る (vimの機能)
:tag <filename>    # 対象のファイルを開く <tab>補完あり
```
