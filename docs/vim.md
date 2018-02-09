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

### インデント
ノーマルモード、挿入モード、ヴィジュアルモードそれぞれでのインデントの操作

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
Ctrl-^             # 以前に編集していたバッファに移動
```

### バッファの削除
[vim-bufkill](https://github.com/qpkorr/vim-bufkill)でウィンドウの状態を保持しつつバッファをクリアできる

```
:BUN               # 対象のファイルをHiddenに
:BD                # 対象のファイルをバッファから削除
```

## Ctags
[Ctags](https://github.com/universal-ctags/ctags)でtagsファイルを作成しておくことで、
関数などの定義元にジャンプすることができるようになる。

```
Ctrl-]             # 定義元へ移動
Ctrl-t             # 前の場所に戻る (vimの機能)
:tag <filename>    # 対象のファイルを開く <tab>補完あり
```

## ファイル名
編集しているファイルが sample_dir/my.txt の場合

```
%                     # sample_dir/my.txt
Ctrl-r %              # (挿入モードで)sample_dir/my.txt が挿入される
Ctrl-r %              # (コマンドモードで)sample_dir/my.txt が挿入される
:! git add %          # sample_dir/my.txt を git add
:! git add Ctrl-r %   # sample_dir/my.txt を git add
```

## 折りたたみ

```
zc                    # 折りたたむ
zo                    # 開く
```

## ウインドウ

```
Ctrl-w =              # サイズを揃える
Ctrl-w _              # 縦方向に最大化
Ctrl-w |              # 横方向に最大化
```
