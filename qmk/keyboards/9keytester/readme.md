# 9KeyTester

STM32F072CBT6を使用した3 × 3配列のキーボードである。SW1～SW9をPA0～PA8へ接続し、初期配列は通常の数字列の1～9としている。

```sh
qmk flash -kb 9keytester -km via
```

`via`版はVIA／Remapに対応する。`default`版は対応しない。ビルドだけ行う場合は`flash`を`compile`に置き換える。

USB書込み待ちになったら、SW11（BOOT）を押したままSW10（RESET）を押して離し、最後にSW11を離す。完了後、SW10だけを押して離す。
