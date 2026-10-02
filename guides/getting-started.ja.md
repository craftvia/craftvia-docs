# CraftVia Rev0 Getting Started

> [!WARNING]
> 現在のCraftVia Rev0は未検証のEngineering Prototypeです。公開ファイルを量産認定済みハードウェアとして扱わないでください。[英語版](getting-started.md)を正本とします。

## Repoを選ぶ

- [Core-S G031](https://github.com/craftvia/craftvia-core-s-g031)：STM32G031 Core設計
- [Station-S](https://github.com/craftvia/craftvia-station-s)：開発、Debug、Breakout、電源、計測
- [MakerCard-S](https://github.com/craftvia/craftvia-makercard-s)：G031回路とBreakout・試作領域を統合

製造データを使用する前にREADME、Revision仕様書、検証計画、Release Notesを確認してください。

## Release成果物

| 成果物 | 役割 |
| --- | --- |
| `source/`のEasyEDA project | 編集可能な設計正本 |
| `fabrication/`のGerber ZIP | 対象ReleaseのPCB製造upload正本 |
| `assembly/`のBOM CSV | 実装部品正本 |
| CPL／Pick and Place | DNP・非BOM行を含む場合があり、BOMとの照合が必要 |
| `docs/`の回路図PDF | 人が確認するためのReference。製造正本ではない |
| PCB／Assembly PDF | BOM・Gerberを置き換えないReference |
| `SHA256SUMS.txt` | 凍結済みReleaseの整合性manifest |

## 発注前

1. 正確なVersion／Revision Releaseを選ぶ
2. `RELEASE_NOTES.md`の警告と既知条件を読む
3. `SHA256SUMS.txt`でhashを確認する
4. Gerber ZIPを編集・再圧縮せず全体をuploadする
5. 製造業者previewで外形、層数、drill、mask、silkを確認する
6. CPLを正本BOMと照合する
7. Through-hole connectorと機械stackを実装前に確認する

## 初回通電前

1. 製品検証計画に従う
2. 向き、はんだ、短絡、DNP、Jumperを確認する
3. 各電源railとGND間の抵抗を測定する
4. 電流制限付き電源を使用する
5. Board ID、構成、測定器、測定値、証拠を記録する
6. 受入条件を外れた場合は停止し、電流制限を上げて続行しない

## 結果の報告

製品、Version、Revision、実装状態、Test IDを明記します。写真、測定値、Firmware／command version、Jumper状態、Pass／Fail／Blockedを含めてください。

