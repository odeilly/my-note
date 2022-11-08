---
title: "Debian GNU/Linux"
id: "my-note"

html:
 embed_local_images: false
 embed_svg: true
 offline: false
toc:
 depth_from: 2
 depth_to: 4
 ordered: false
print_background: false
export_on_save:
 html: true
---

<!-- @import "../less/common.less" -->

# Debian GNU/Linux

## キーボード設定

### CapsLock を Ctrl にする

参考：<https://lambdalisue.hatenablog.com/entry/2013/09/27/212118>

上記ページの通りですが、メモを残しておきます。

`/etc/default/keyboard` というファイルを編集し、`XKBOPTIONS` を設定することで CapsLock を Ctrl に変更することができます。

``` sh
XKBOPTIONS="ctrl:nocaps" # CapsLock を Ctrl に変更する
# XKBOPTIONS="ctrl:swapcaps" # 左 Ctrl と CapsLock を入れ替える
```

修正後に、下記コマンドを実行します。

``` sh
sudo dpkg-reconfigure -phigh console-setup
```

### Google Chrome のインストール

deb パッケージをダウンロードして、apt-get コマンドでインストールします。
相対パスまたは絶対パスで deb ファイルを指定します。

``` sh
sudo apt-get install ./google-chrome-stable_current_amd64.deb
```

`google-chrome` というコマンドで Google Chrome を起動できます。
