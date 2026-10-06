# 配布ファームウェアのビルド条件

対応するカスタムソースは[qmk/keyboards/9keytester](../qmk/keyboards/9keytester/)に同梱。QMK本体・依存ライブラリは次のソースを使用する。

- [QMK 0.34.4](https://github.com/qmk/qmk_firmware/tree/08c662f286ddfd12a985f57b584b02eca5af0ae6)
- [ChibiOS](https://github.com/qmk/ChibiOS/tree/6170ddf92d55be54c89b708d1882eea229edeb2c)
- [ChibiOS-Contrib](https://github.com/qmk/ChibiOS-Contrib/tree/5a9ad82b6ba4f649cdb800e8c2bbc9be2d3ce767)
- [printf](https://github.com/qmk/printf/tree/c2e3b4e10d281e7f0f694d3ecbd9f320977288cc)

QMK本体を上記コミットで取得し、`git submodule update --init --recursive`で依存ソースを取得する。同梱の`qmk/keyboards/9keytester`をQMK本体の`keyboards/9keytester`へコピーし、`qmk compile -c -kb 9keytester -km via`でビルドする。[通常のビルド手順](../qmk/README.md)を参照。

ビルド環境はQMK CLI 1.2.0、arm-none-eabi-gcc 15.2.0（QMK toolchains `a55a2b0`）。メーカー名はNamekee、製品名は9KeyTester。通常動作時のVID/PIDは`FEEC:0729`（正式取得していない暫定値）。配列・GPIO割当ては変更せず、1・3・7・9の同時押し機能は無効。

QMK本体と依存ソースの著作権・ライセンスは各ソースに記載されている。ファームウェアはMITライセンスの対象外。

ファイルサイズ：21,292 bytes。SHA-256：`8f09e404f2a8984ccef3bd727794b202d8e1f7e8aa446ad38202217504a1acfc`。

ビルド成功、生成物とのSHA-256一致、USBメーカー名Namekeeを確認した。今回のバイナリの実機書込み・動作確認は未実施。
