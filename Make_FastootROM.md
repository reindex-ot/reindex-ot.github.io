# Fastboot ROMの作り方
Fastboot ROMを作る方法をこちらに記しておきます。
英語に訳す能力は皆無なので海外圏のユーザーは翻訳サービスを使って翻訳をしてください。

**用意をする物**

 - [ ] Bootloader Unlockがされたデバイス
 - [ ] adbとfastbootの環境を構築したPC
 - [ ] バッチやシェルスクリプトを作る能力
 - [ ] GKI対応のデバイスならば「KernelSU」
 - [ ] GKI非対応のデバイスならば「DSU Sideloader」と「SUが入ったGSI」

Bootloader Unlockは必須項目になります。これができないと作成はまずできません。次にFastboot ROMの作成には一時的なroot権限が必要となります。

## DSUならばGSIのSideload、KSUならfastboot boot
SUが入ったGSIか、KSUで一時rootを取得します。
手軽な方法はKSUになります。

**KernelSUを使う場合**
 1. 対象のデバイスに適したKSUのimg(GKI)をダウンロード
 2. KSUManagerをインストール
 3. fastbootで再起動を行ない、コマンドで`fastboot boot XXX.img`を実行する (絶対に`fastboot flash boot`は実行しないでください)
 4. デバイスが起動する、KSUManagerで動作中が表示されていれば一時rootになっています

**DSU SideloaderとGSIを使う場合**
 1. DSU Sideloaderをインストール、SUの入ったGSIを用意する
 2. 操作を行なうとDSUのセットアップが開始されます
 3. 再起動後にSideloadをしたGSIが起動されます
 4. コマンドでrootになっている事を確認します

DSUとGSIの方法は汎用性が高いですが、処理に時間がかかるデメリットがあります。GKIに対応しているのであればKSUを使う事を推奨します。

## imgを抽出する為の操作

 1. root権限で実行するため`su`にする (adb shell→su)
 2. 各イメージがあるパスへ移動する (MediaTekなどでは` /dev/block/by-name/` の場合もあります)
`cd /dev/block/bootdevice/by-name/`
3. バックアップ保存用ディレクトリを作成
`mkdir /sdcard/backup_img`
4. cacheとuserdata以外すべてを/sdcard/backup_imgへバックアップするコマンドをコピー&ペーストしてください

    `for file in *; do`
    
    `if [[ "${file}" = cache* || "${file}" = userdata* ]]; then continue ; else dd if=/dev/block/bootdevice/by-name/"${file}" of=/sdcard/backup_img/"${file}".img ; fi`
    
    `done`

5. MD5 のリストをチェック用に作成します。以下のコマンドをコピー&ペーストしてください。

    `echo "" > /sdcard/backup_img/md5.txt`
    `for file in *; do
        if [[ "${file}" = cache* || "${file}" = userdata* ]]; then continue ; else
    	echo "${file}" >> /sdcard/backup_img/md5.txt
    	md5sum /dev/block/bootdevice/by-name/"${file}" >> /sdcard/backup_img/md5.txt
    	md5sum /sdcard/backup_img/"${file}".img >> /sdcard/backup_img/md5.txt
    	echo "" >> /sdcard/backup_img/md5.txt
        fi`
    `done`

これを行なう事でsdcard内にbackup_imgのフォルダが作成され、各種imgが保存されています。DSUを使用する場合はストレージ容量の設定を16GBに設定した方が良いでしょう。

## backup_imgをPCにコピーする&不要なファイル削除する

数分でimgが抜けているので保存されたフォルダをPCへコピーします。内部には固有情報などのファイルが存在するのでそれを除外する作業を行ないます。同時に目的のROMが格納されているアクティブスロットも確認します。fastbootで

    fastboot getvar all
を実行してactive-slotを確認しましょう。大量なログの最後の箇所にアクティブになっているスロットが表示されています。

    (bootloader) current-slot: 

a/bのどちらかが表示されています。active-slotは覚えておきましょう。
これがaであればAのスロット上、bであればBのスロット上でROMが稼働しています。imgはaとb両方を保存しているのでアクティブになっている物だけ(aであればboot_a.img)を残して削除と固有情報などのファイル削除をやりましょう…(バッチ作れたら早いと思います)

## バッチファイルの作成
手作業でimgを焼くのは面倒なのでバッチを作成しましょう
物によってはアクティブスロットを切り替えないと起動ができなかったりと性格が変わった物も存在します。Xiaomiの場合は、`fastboot flash boot_ab`と書くと両方のスロットに焼ける事もあるようです。ここで補足ですが、vbmetaの箇所に`fastboot flash vbmeta --disable-verity --disable-verification`のオプションを付ける事はオススメしません。それを行なうとOTAが失敗する事が起きる可能性があります。GSIを使う事がない限りはオプションは外しておきましょう。

## Fastboot ROMの完成
作ったROMを試しに焼いて起動をしたのであれば完全に成功です。boot.imgをパッチをしてMagiskでのrootやモジュールも使えるようになります。バージョンごとにこの作業を行なえばダウングレードも可能になります。ダウングレード時は「fastboot -w」か「リカバリーからwipe userdata」を実行しないと起動をしない場合があります。後はアーカイブにしてネットの海に流すなり個人で管理など好きにしてください。

## Option: super.imgのスパースイメージ化
super.img(systemやvendorなどがまとまった奴)をスパースイメージ(simg)化するとSuperのFlash時の処理時間が短縮できたりします。WSLやVirtualBoxの仮想環境で「img2simg」を使用してsuper.imgをスパースイメージに変換する事ができます。余裕がある人はやっておくと捗るかもしれません。
