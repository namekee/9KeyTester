# 9KeyTester

長尾製作所の9キースイッチテスター台に対応したUSBキーボード（マクロパッド）基板です。STM32F072CBT6とMXホットスワップソケットを搭載。QMK・VIA・Remapでキー割当てを変更できます。

初期配列（キーを押す表面から見て、USB-C端子を上にした向き）：

```text
  USB-C
  1 2 3
  4 5 6
  7 8 9
```

## 配布ファイル

- [ファームウェア](firmware/9keytester_via.bin)：VIA／Remap共通の書込み用バイナリ。
- [VIA用JSON](qmk/via/9keytester.json)／[Remap用JSON](qmk/remap/9keytester.json)：キーボードの形状・接続先を指定する定義ファイル。
- [QMKソースとビルド手順](qmk/README.md)：配列や機能をコードで変更する場合に使用する。

## RESET・BOOTボタン

ファームウェア書込み用の操作ボタン。

| 印字 | 役割 | 操作 |
| --- | --- | --- |
| SW10 | RESET（再起動） | 単独で押して離す。 |
| SW11 | BOOT（書込みモード選択） | SW11を押したままSW10を押して離し、最後にSW11を離す。単独で押しても通常何も起こらない。 |

## ファームウェア書き込み

1. [QMK Toolbox](https://github.com/qmk/qmk_toolbox/releases)を起動し、`Open`から`firmware/9keytester_via.bin`を選ぶ。
2. データ通信対応USB-Cケーブルで接続する。**SW11を押したままSW10を押して離し、SW11を離す。**
3. `STM32 BOOTLOADER`（`0483:DF11`）の接続を確認し、`Flash`を押す。完了するまでUSBを抜かない。
4. SW10だけを押して離し、再起動する。

WindowsでDFUが認識されない場合は、[QMK公式のドライバー手順](https://docs.qmk.fm/driver_installation_zadig)に従い、**STM32 BOOTLOADERだけ**へWinUSBを設定する。通常動作中の9KeyTesterのドライバーは変更しない。[書込み方式の詳細](https://docs.qmk.fm/flashing#stm32-apm32-dfu)はQMK公式を参照する。

## キー割当ての変更

### VIA

1. ChromeまたはEdgeを使い、基板を通常動作モードで接続する。
2. [VIA](https://www.usevia.app/)のSettingsで`Show Design tab`を有効にする。
3. Designで`Use V2 definitions`を**オフ**にし、`Load`から`qmk/via/9keytester.json`を読み込む。
4. Configureで`Authorize device`を押し、`9KeyTester`を選んで接続する。
5. 変更するキーを選び、割り当てたいキーコードを選ぶ。変更は基板へ保存される。

### Remap

1. ChromeまたはEdgeで[Remap](https://remap-keys.app/)を開き、`START REMAP`から`9KeyTester`を接続する。
2. 定義ファイルを求められたら、`qmk/remap/9keytester.json`を読み込む。
3. キーを選んで割当てを変更し、画面の`Flash`で基板へ保存する。

## 初期化

- 配列を初期化するには、USBを抜き、表面左上のキー（初期配列の1）を押したまま再接続する。キーを離してSW10を押すと再起動する。保存したキー割当て・マクロは消える。

## ライセンス

- 文書・VIA／Remap定義：[MIT](LICENSE)。著作権者：Namekee。
- QMKカスタムソース：[GPL-2.0-or-later](qmk/LICENSE)。QMK本体と依存ライブラリには、それぞれのライセンスが適用される。

配布ファームウェアにはQMKと依存ライブラリのライセンスが適用されます。[対応ソースとビルド条件](firmware/BUILD.md)を参照。
