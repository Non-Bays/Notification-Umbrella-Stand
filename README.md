# お知らせ傘立て

傘の取り違いや取り忘れの対策として、傘と傘立ての使用者を紐づける傘立てを製作しました。

ここでは、製作システムの仕組みや概要について取り上げています。
操作方法やプログラムについては以下のリンクを参照してください。
https://github.com/Non-Bays/SSH_2024/tree/main

## 1.システムについて

このシステムはセンサ内蔵傘立て、傘立て側カメラ、出口側カメラの3つの装置で成り立っています。

#### センサ内蔵傘立て
センサ内蔵傘立てには、赤外線LEDと赤外線センサを内蔵しています。
赤外線センサによって傘立てに傘が入っている状態を感知します。
3PinのXHコネクタで傘立て側カメラと接続しています。

#### 傘立て側カメラ
傘立て側カメラには、Spresenseボード、カメラ、スピーカ、モバイルバッテリーを内蔵しています。
センサ内蔵傘立てから傘の状態を取得し、状態が変化した際にカメラ画像から利用者の画像を取得します。
また、傘立ての利用状況の確認としてデータを取得しています。
これらの情報をボードに取り付けているWi-Fiモジュールを介してサーバに送信されます。

#### 出口側カメラ
出口側カメラには、Spresenseボード、カメラ、モバイルバッテリーを内蔵しています。
カメラで利用者の退出を感知しており、その情報がサーバに送信されます。

![devices](https://github.com/user-attachments/assets/c522c821-cca5-4f48-a9e9-43c4b908aeb9)

## 2.動作について

このシステムは各状況で次のように動作します。

#### 傘を置いたとき
センサ内蔵傘立てに傘を置いたときに、センサの変化と顔画像をサーバに送信します。
サーバではこの二つの情報を紐づけてデータベースに追加します。

#### 傘を取ったとき
傘立てから傘を取ったときに、カメラの映像からデータベース上に記録されている人物か照合を行います。
傘に紐づいている人物と同一人物であると確認された場合、そのまま取り出すことができます。
しかし、傘に紐づいている人物と別人であると確認された場合、スピーカからアラート音が通知されます。

#### 傘を取り忘れたとき
傘立てを利用した人が出口から出ることを確認したとき、センサの状態を確認します。
センサの状態が変化していないと判断するとアラート音が通知されます。

![systems](https://github.com/user-attachments/assets/e5a30d75-c9e6-499a-b7cb-2ff5ad55a1c0)

## 3.このシステムの特徴

#### Efficient Netを用いた顔認証
Spresenseから取得した顔画像を高速で処理し，データベースに格納します。
これにより顔画像のデータベースを変更することができるため、事前に顔画像を登録する必要はありません。

#### ワイヤレスによる導入のしやすさ
このシステムはWi-Fiモジュールを用いた通信、モバイルバッテリーを用いて駆動するよう設計しているため、様々な場所に置くことが可能です。
また、Spresenseの低消費電力という特徴からモバイルバッテリーでも長時間使用することができます。

## 4.使用機材

|使用機材|個数|
|----|----|
|Spresense メインボード (CXD5602PWBMAIN1)|2|
|​Spresense 拡張ボード (CXD5602PWBEXT1)|2|
|​Spresense カメラボード (CXD5602PWBCAM1)|2|
|microSDカード|2|
|薄型コンパクトモバイルバッテリー (DE-C45-5000DGY)|2|
|USBケーブル（A-MicroB）|2|
|赤外線受信モジュール TSSP58038|4|
|赤外線LED|4|

## 5.製作者
* チーム名  ：Non Bays
* メンバー  ：梁瀬琉真、田原俊、大塚凱、北岩隼人、劉樹鵬

## 6.謝辞
本プロジェクトは、田原氏をはじめとするNon Baysのチームメンバーの尽力により達成することができました。
また、本プロジェクトはSensing Solution ハッカソン 2024においてファイナリストとして選出されるという大変光栄な機会をいただきました。
チームメンバーおよび協力してくださった関係者の皆様に心より感謝申し上げます。
