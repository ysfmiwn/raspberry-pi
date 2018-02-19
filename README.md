# [Mac]Raspberry Pi 3 事前準備設定

## 準備物
- [Raspberry Pi 3本体(ケース付き)](http://amzn.to/2o2kDyu)
- [Raspberry Pi用電源セット(5V 3.0A)](http://amzn.to/2EKAxao)
- [microSDカード 32GB Class10](http://amzn.to/2sze6zW)
- [Raspberry Pi用カメラモジュール](http://amzn.to/2o32ccO)
- [USB-シリアル変換ケーブル](http://amzn.to/2EHbNQm)

## 環境
- [Raspberry Pi 3](http://amzn.to/2o2kDyu)
- MacOS High Sierra 10.13.3

## ドライバのインストール
1. ドライバのインストール：SIO (Smart-IO)  > [USB to UART/Serial/Printer  > PL2303 Mac OS X Driver Download](http://www.prolific.com.tw/us/showproduct.aspx?p_id=229&pcid=41)
2. インストール後、Macの再起動が必須
3. Raspberry Pi3 のGPIOにUSB-シリアル変換ケーブルのメス型のピンを差し込み接続する
  - 黒 -> 6番(GND)
  - 白 -> 8番(UART0 TX)
  -  緑 -> 10番(UART0 RX)
  - 赤は接続しない

## Raspberry Pi3 の設定
1. OSのダウンロード
  - [RASPBIAN STRETCH WITH DESKTOP(Release date:2017-11-29)](http://ftp.jaist.ac.jp/pub/raspberrypi/raspbian/images/raspbian-2017-12-01/2017-11-29-raspbian-stretch.zip)
2. ダウンロードしたOSを解凍する
  - 解凍できない場合、「[The Unarchiver](https://itunes.apple.com/jp/app/the-unarchiver/id425424353?mt=12)」アプリをMac App Storeからダウンロードする
  - 解凍したOSイメージをSDカードにコピーする
  - OSイメージ書き込みツール：[Etcher](https://etcher.io/)
    - 参考サイト：[Etcher - 3ステップで簡単にイメージ書き込み}(https://www.moongift.jp/2017/10/etcher-3%E3%82%B9%E3%83%86%E3%83%83%E3%83%97%E3%81%A7%E7%B0%A1%E5%8D%98%E3%81%AB%E3%82%A4%E3%83%A1%E3%83%BC%E3%82%B8%E6%9B%B8%E3%81%8D%E8%BE%BC%E3%81%BF/)
3. SDカードにコピーした中の「config.txt」を開き、最終行以降に以下の2行を追記する。
  - `core_freq=250`
  - `enable_uart=1`
4. SDカードをパソコンから抜き、Raspberry Pi本体に挿し込む

##  Raspberry Pi3 起動確認
1. Raspberry Pi本体をHDMI端子接続可能な外部ディスプレイやテレビにつなげる
2. Raspberry Pi本体をUSB電源につなぐ

## UART通信で操作を行えるようにする接続手順
1. USB-シリアル変換ケーブル をパソコンと接続する
2. Macのターミナルを起動させる
3. `$ ls /dev/tty.*` を入力し、接続しているデバイスのシリアル名を確認する
4. シリアル名「tty.usbserial」の場合、`$ screen /dev/tty.usbserial 115200` を入力する
  - ターミナルの画面が固まるが、一度returnキーを押すとログインできるようになる。
  - 「Sorry, could not find a PTY」のエラーが出る場合、ドライバを正しくインストールしてもエラーが発生するならば、USB-シリアル変換ケーブルをMacから抜き再度挿すとエラーが発生しなくなることが多いです。

## 終了手順
1. `$ sudo shutdown -h now`で Raspberry Pi3 の電源を切る 
2. ターミナルのscreenのウィンドウを`Control+q`で完全終了する
3. 電源を切り、ケーブルを抜く
- この手順を行わない場合、Raspberry Pi3に再接続ができなくなるケースが発生します。私は2回ぐらいなってしまい、初めからやり直しました。


## 参考
- [yoshihiroo / programming-workshop/rpi_ai_handson/README.md](https://github.com/yoshihiroo/programming-workshop/blob/master/rpi_ai_handson/README.md#%E6%A9%9F%E6%9D%90%E8%B3%BC%E5%85%A5%E3%82%AC%E3%82%A4%E3%83%89)
- [激安USB-Serial アダプタを使って、Macと Raspberry Pi 3 をシリアル接続する](https://qiita.com/tmishina/items/612d7d1a7d76364a9e45)
- [Raspberry PiをUART通信で操作する](https://qiita.com/shishamo_dev/items/9735ce2fcdd26cf46577)
