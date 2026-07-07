# Chibi-T Furoshiki Logger

M5Stack Basic / Core2 用の車両データロガー拡張基板（モジュール基板）です。

## 概要

本基板は M5Stack の M-BUS コネクタに接続するボトムモジュールとして動作し、以下のデータを収集・記録するためのロガー回路です。

- GNSS（GPS）モジュールからの位置情報（UART）
- 車両 ECU との UART 通信によるデータ
- BME280 センサーによる温湿度・気圧などの環境データ

## 特徴

- M5Stack M-BUS（2×15ピン）接続、Basic / Core2 の両方に対応した Module 基板
  - テンプレートは <https://github.com/botanicfields/KiCad6-Environment> の `M5Stack_module_fdm` を使用
- GNSS（GPS）モジュール接続用の UART 入力
- 車両 ECU との通信用 UART 入力
- Bosch BME280 搭載（I2C接続、アドレス `0x76`）による温湿度・気圧センシング
- MP1584EN-LF-Z による +12V → 5V / 3.3V 降圧レギュレータを内蔵
- ポリヒューズおよびショットキーダイオードによる電源保護

<!-- TODO: 基板写真・回路図スクリーンショットを追加 -->

## 主要部品

| Ref | 部品 | 役割 |
| --- | --- | --- |
| U1 | MP1584EN-LF-Z | 降圧DC-DCコンバータ（+12V → 5V/3.3V） |
| U2 | BME280 | 温湿度・気圧センサー（I2C） |
| J1 | M5Stack M-BUS | M5Stack Basic/Core2 との接続コネクタ |
| D1 | ショットキーダイオード | 電源保護 |
| F1 | ポリヒューズ | 電源保護 |

より詳細な部品表は、KiCad でプロジェクトを開き BOM を出力することで確認できます（後述）。

## リポジトリ構成

```txt
Chibi-T_Furoshiki_Logger.kicad_pro   KiCadプロジェクトファイル
Chibi-T_Furoshiki_Logger.kicad_sch   回路図
Chibi-T_Furoshiki_Logger.kicad_pcb   基板データ
C15051/                              MP1584EN-LF-Z用カスタムライブラリ（シンボル・フットプリント）
logos.pretty/                        シルク印刷用ロゴフットプリント
LICENSE.txt                          ライセンス
```

## 必要な環境

- KiCad 10.0 以降

## 使い方

1. `Chibi-T_Furoshiki_Logger.kicad_pro` を KiCad 10.0 以降で開きます。
2. 回路図・基板データを確認・編集できます。
3. ガーバーデータや部品表（BOM）、部品配置データ（CPL）の生成には、KiCad拡張「[Fabrication Toolkit](https://github.com/bennymeg/Fabrication-Toolkit)」を使用する想定で設定済みです（`fabrication-toolkit-options.json`）。  
   生成したデータは `production/` フォルダに出力されますが、このフォルダは `.gitignore` 対象のためリポジトリには含まれません。  
   各自の環境で生成してください。

## 免責事項

本プロジェクトは個人のホビープロジェクトです。車両への実装・使用は自己責任で行ってください。  
基板の動作および安全性について、いかなる保証も行いません。

## ライセンス

本プロジェクトは [MIT License](LICENSE.txt) の下で公開されています。

Copyright (c) 2026 Tomohiro Kusu
