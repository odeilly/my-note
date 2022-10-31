---
title: "Windows"
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

# Windows

Windowsに関するメモ。

[toc]

## 完全シャットダウン

参考：<https://jp.ext.hp.com/techdevice/windows10sc/60/>

### 常時完全シャットダウンにする方法

1. 「コントロールパネル」→「電源オプション」を開き、「電源ボタンの動作を選択する」をクリックする。
   ![電源ボタンの動作を選択する](image/2021-03-29-15-55-10.png)

2. 「現在利用可能ではない設定を変更します」をクリックする。
   ![現在利用可能ではない設定を変更します](image/2021-03-29-15-57-25.png)

3. 「高速スタートアップを有効にする(推奨)」のチェックを外す。
   ![高速スタートアップを有効にする(推奨)](image/2021-03-29-15-58-47.png)

4. 「変更の保存」をクリックする。

## 便利なコマンド

### 拡張子の表示・非表示

参考：<https://win2012r2.com/2022/05/19/enable-file-extention-using-powershell/>

コマンドプロンプトで、拡張子の表示・非表示を切り替えることが出来ます。

- 拡張子を表示する

``` {.cmd}
reg add "HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\Advanced" /v "HideFileExt" /d "0" /t  REG_DWORD /f
```

- 拡張子を非表示にする

``` {.cmd}
 reg add "HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\Advanced" /v "HideFileExt" /d "1" /t  REG_DWORD /f
```

### 隠しフォルダの表示・非表示

参考：<https://automationlabo.com/wat/?p=1861>

コマンドプロンプトで、隠しファイルの表示・非表示を切り替えることが出来ます。

- 隠しファイルを表示する

``` {.cmd}
reg add "HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Advanced" /v "Hidden" /t REG_DWORD /d "1" /f
```

- 隠しファイルを非表示にする

``` {.cmd}
reg add "HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Advanced" /v "Hidden" /t REG_DWORD /d "2" /f
```

### 画面ロックまでの時間の設定

参考：<https://4thsight.xyz/24367>

コマンドプロンプトを管理者権限で起動します。
`/d` オプションでロックされるまでの待機時間 (秒) を設定します。
以下のコマンドでは、300秒 (5分) を指定しています。

``` {.cmd}
reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System" /v InactivityTimeoutSecs /t REG_DWORD /d 300 /f
```

コマンド実行後、Windows の再起動が必要です。

### wmic コマンド

wmic コマンドを使うと、PC の情報を表示することが出来ます。

- 参考
  - <https://www.intel.co.jp/content/www/jp/ja/support/articles/000025060/intel-nuc.html>
  - <https://genchan.net/it/pc/windows/12535/>

#### PC のシリアル番号

``` {.cmd}
wmic bios get serialnumber
```

``` {.cmd}
wmic csproduct get identifyingnumber
```

#### PC の製品名

``` {.cmd}
wmic baseboard get product
```

### アカウント管理

参考：<https://atmarkit.itmedia.co.jp/ait/articles/0609/02/news014.html>

net user コマンドを使うことで、アカウントの作成/削除/更新などが可能です。

#### net user コマンドのヘルプ

``` {.cmd}
net user /?
```

#### アカウントの表示

``` {.cmd}
net user
```

各アカウントの詳細場をは、以下のコマンドで表示できます。

``` {.cmd}
net user <アカウント名>
```

自分がどのアカウントでサインインしているかは、set user コマンドで確認出来ます。

``` {.cmd}
set user
```

#### アカウントの作成

コマンドプロンプトを管理者で起動します。

``` {.cmd}
net user <アカウント名> /add
```

すると、パスワードなしのローカルユーザが作成されます。

``` {.cmd}
net user <アカウント名> <パスワード> /add
```

このコマンドでは、同時にパスワードも設定します。

#### アカウントのパスワード変更

コマンドプロンプトを管理者で起動します。

``` {.cmd}
net user <アカウント名> <パスワード>
```

#### 管理者権限の付与

コマンドプロンプトを管理者で起動します。

``` {.cmd}
net local group administrators <アカウント名> /add
```

#### アカウントの削除

コマンドプロンプトを管理者で起動します。

``` {.cmd}
net user <アカウント名> /delete
```

ただし、ユーザープロファイルなどは自動で削除されないので、必要なら手動で削除します。
