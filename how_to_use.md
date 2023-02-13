[![Twitter](https://img.shields.io/twitter/follow/ot_inc?style=flat&logo=twitter)](https://twitter.com/ot_inc)
[![GitHub](https://img.shields.io/github/followers/reindex-ot?style=flat&logo=github)](https://github.com/reindex-ot)
[![YouTube](https://img.shields.io/youtube/channel/subscribers/UCE5tVfXXLSonqBJ1GZmLuyw?style=flat&logo=youtube)](https://www.youtube.com/channel/UCE5tVfXXLSonqBJ1GZmLuyw)
[![Copano Rickey](https://raw.githubusercontent.com/reindex-ot/reindex-ot.github.io/main/image/copanorickey.jpg)](https://umamusume.jp/character/detail/?name=copanorickey)
<br>
# How to use
### 📱<b>Fastboot ROMの使い方</b>
Fastboot ROMは容量を抑える為にあえてfastboot.exeなどのファイルを入れていません。<br>
そもそも環境を構築していると想定しているので普通に使えるだろうと言う理由もあります。<br>
使い方は単純でFastbootの画面を開いた状態で各種Fastboot ROMのbatファイルを実行でROMがFlashされるようになっています。<br>
Nothing Phone(1)はCritical PartitionをUnlockしていないとFlashできない物が存在します。しかし必ずやる必要はないので普通にMagiskなどを使う位であれば拘る必要はありません。<br>
もしもCritical PartitionをUnlockしたい場合は、「fastboot flashing unlock_critical」を実行でUnlockできます。<br>

### 📱<b>How to use Fastboot ROM (Translation DeepL)</b>
Fastboot ROM does not include files such as fastboot.exe to save space.<br>
There is also the reason that it is assumed that the environment is being built in the first place, so it can be used normally.<br>
The usage is simple, and ROM is made to flash by executing various Fastboot ROM bat files with the Fastboot screen opened.<br>
Nothing Phone(1) has a thing that cannot be flashed if Critical Partition is not Unlocked. However, it is not necessary to do it, so there is no need to be concerned about it if you use Magisk normally.<br>
If you want to unlock the Critical Partition, you can do so by executing "fastboot flashing unlock_critical".<br>

### 🌐<b>ローカルでOTAを行なう場合</b>
Nothing OSをローカルでOTAを行なう場合は、各バージョンに適合したOTAのzipファイルを用意してください。<br>
Nothing OSのOTAは内部のチェックを行なう仕組みになっている為、Magiskを使用している場合は一旦通常のboot.imgをFlashしてからOTAを行なってください。<br>
戻さなかった場合、チェックで弾かれてしまい更新が失敗してしまいます。<br>
ファイルを指定しても良いですが内部ストレージに「ota」と言うフォルダを作成し、OTAのzipを入れると自動的にファイルを認識します。<br>

### 🌐<b>When OTA is performed locally (Translation DeepL)</b>
If you want to OTA Nothing OS locally, please prepare the appropriate OTA zip file for each version.<br>
The OTA for Nothing OS is designed to perform an internal check, so if you are using Magisk, please flash the normal boot.img file and then perform the OTA.<br>
If you do not revert, the check will be rejected and the update will fail.<br>
You can specify the file, but if you create a folder called "ota" in the internal storage and put the OTA zip file in it, it will automatically recognize the file.<br>


# 👤この人について
私は、日本人です。<br>
アプリケーションの日本語化とか色々やってますが、英語の能力はそれ程高くないです。詳細はGitHubのプロフィールをどうぞ。<br>
[GitHubのプロフィール](https://github.com/reindex-ot)<br>

# 👤About (Translation DeepL)
I am Japanese.<br>
I do a lot of things like making applications Japanese, but my English skills are not that great. For more information, please visit my GitHub profile.<br>
[GitHub Profile](https://github.com/reindex-ot)<br>
