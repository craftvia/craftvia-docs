# CraftVia 互換性方針・現行Matrix

> [!WARNING]
> 現行Matrixは設計意図を示すもので、実機検証完了を意味しません。Rev0の組み合わせは証拠公開まで未検証です。[英語版](compatibility.md)を正本とします。

## 互換性の層

1. **機械**：外形、接点、Key、スタック、クリアランス
2. **電源**：割り当て、電圧範囲、電流予算、GND、電源分離
3. **システム**：書き込み、Debug、RESET、BOOT、選択したUSB／Debugプロファイル
4. **用途信号**：実装固有ピンマップとPeripheral競合
5. **検証済み組み合わせ**：一緒に試験した正確なVersion／Revision

物理的に挿入できても安全に給電できるとは限らず、書き込み可能でも異なるCore間で用途信号が互換とは限りません。

## Rev0 Matrix

| 対象 | インターフェース関係 | 設計状態 | 検証状態 |
| --- | --- | --- | --- |
| Core-S G031 v1 Rev0 | Core-S v1およびSTM32システム端子プロファイルを実装 | Frozen | Unverified |
| Station-S v1 Rev0 DEV/DUT + Core-S G031 v1 Rev0 | 電源、SWD、RESET、BOOT、VCP、操作、計測を意図 | Frozen | Unverified |
| Station-S v1 Rev0 CTRL footprint + Core-S G031 v1 Rev0 | CTRL用。オンボードSTLINK SWDには未接続 | Frozen。CTRL socket部品はRev0正本BOM対象外 | Unverified |
| MakerCard-S v1 Rev0 | Core-S G031回路を統合し、接点マップを展開 | Frozen | Unverified |
| MakerCard-S v1 Rev0 + Station-S v1 Rev0 | 電気マップは対応予定。機械クリアランス・嵌合は未主張 | Frozen | Unverified |

## 今後の記録規則

- 製品VersionとPCB Revisionを両方記録する
- designed forとverified withを区別する
- 検証証拠と試験sampleを特定する
- 結果に影響するJumper、実装、Firmware、電源構成を記録する
- `Core-S`表記だけから互換性を推測しない
- 後続Revisionで修正しても、失敗記録をErrataまたはMatrixに残す

## Firmware移植性

Core-Sは物理統合と一部システム機能を共通化します。異なるMCU実装間でFirmwareが無変更で動くことは保証しません。

