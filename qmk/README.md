# QMKのビルド・書込み

Windowsでは[QMK MSYS](https://msys.qmk.fm/)を準備し、初回に`qmk setup`を実行する。

1. このリポジトリの`qmk/keyboards/9keytester`を、QMK本体の`keyboards/9keytester`へコピーする。
2. QMK本体のルートで次を実行する。ビルド後、USB書込み待ちになる。

   ```sh
   qmk flash -kb 9keytester -km via
   ```

3. 基板をUSB接続し、SW11（BOOT）を押したままSW10（RESET）を押して離し、最後にSW11を離す。書込み完了後、SW10だけを押して離す。

ビルドだけ行う場合は、`qmk compile -kb 9keytester -km via`を実行する。QMK本体のルートに`9keytester_via.bin`が生成される。`invalid keyboard_folder_or_all`が出たら、手順1のコピー先を確認する。

## 定義ファイルと仕様

[VIA用JSON](via/9keytester.json)と[Remap用JSON](remap/9keytester.json)は、共通の`via`ファームウェアで使用する。ボタン位置と設定手順は[プロジェクトのREADME](../README.md)を参照する。

初期配列は通常の数字列の1～9、レイヤーは4枚である。USB VID/PIDは通常動作時が`FEEC:0729`（正式取得していない暫定値）、DFU時が`0483:DF11`となる。

[ビルド記録](../firmware/BUILD.md)にQMKのバージョンと検証範囲を記載している。カスタムソースはGPL-2.0-or-laterであり、QMK本体と依存ライブラリにはそれぞれのライセンスが適用される。[LICENSE](LICENSE)を参照する。
