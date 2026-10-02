# CraftVia プロジェクト概要

> [!IMPORTANT]
> **公開前ドキュメント — 未検証ハードウェア**  
> CraftVia v1 Rev0ハードウェアは設計凍結・発注済みですが、未実装・未通電・未検証です。本書はプラットフォームの意図と凍結済みRev0設計を説明するもので、実機動作を保証するものではありません。[英語版](overview.md)を正本とします。

## 目的

CraftViaは、マイコン回路を次の実用的な開発経路で移行するためのオープンな組み込み開発プラットフォームです。

```text
Station上で開発・書き込み・測定
    → Coreを試作基板または用途固有Carrierへ移設
    → 必要に応じて検証済みCore回路を専用PCBへ統合
```

マイコンの動作に必要な最小回路と、デバッガ、USB、操作部、ブレイクアウト、計測などの開発専用機能を分離します。

## プラットフォーム要素

### Core

Coreは、MCUと宣言された動作構成に必要な回路を含む小型MCU回路です。Core-S実装はCore-Sの機械・電気インターフェースに従い、実装固有のピンマップを公開します。

最初の実装はSTM32G031K8T6を搭載する[CraftVia Core-S G031](https://github.com/craftvia/craftvia-core-s-g031)です。

### Station

Stationは、Coreの開発・検証に使用する電源、書き込み・デバッグ、通信、ブレイクアウト、操作、計測機能を提供します。Station-S Rev0はCore-S G031 Rev0を主対象とし、将来のCoreプロファイル用に手動選択経路も備えます。

[CraftVia Station-S](https://github.com/craftvia/craftvia-station-s)を参照してください。

### Carrier

Carrierは、Coreを搭載する用途固有の基板、配線、治具または最終機器です。Core-Sは接続形状と共通の電気条件を定めますが、異なるCore実装間で用途信号が同じであることは保証しません。

### MakerCard

MakerCardは、Station上の開発から専用CarrierまたはMCU直載せ基板へ進む間のReference形式です。MakerCard-S Rev0はCore-S G031回路とブレイクアウト・試作領域を、配布可能なカード形状へ統合します。

[CraftVia MakerCard-S](https://github.com/craftvia/craftvia-makercard-s)を参照してください。

## 共通化する内容

CraftVia共通文書では次を規定します。

- 用語と文書ステータス
- Core、Station、Carrier、MakerCardの関係
- Core-Sの機械インターフェース、端子ID、Key、共通電源条件
- 互換性と適合表示
- 製品VersionとPCB RevisionによるRelease識別

製品repoでは、実装固有の回路、MCU割り当て、オプション、製造成果物、検証証拠を規定します。

## 現在の公開ハードウェア

| ハードウェア | Version／Revision | 設計状態 | 実機状態 |
| --- | --- | --- | --- |
| Core-S G031 | v1 Rev0 | 試作製造向けに凍結済み | 発注済み・未実装・未検証 |
| Station-S | v1 Rev0 | 試作製造向けに凍結済み | 発注済み・未実装・未検証 |
| MakerCard-S | v1 Rev0 | 試作製造向けに凍結済み | 発注済み・未実装・未検証 |

## 文書モデル

英語文書を正本とし、日本語訳は同じディレクトリへ`.ja.md`付きで置きます。共通要件は本repo、Revision固有要件と試験証拠は各ハードウェアrepoで管理します。

文書間に差異がある場合の優先順位は次のとおりです。

1. 対象Revisionの凍結済み設計ソースと製造Release
2. 製品repoのRevision固有仕様書
3. 共通インターフェース仕様
4. 解説ガイドおよび過去の設計メモ

差異は記録し修正します。優先順位は矛盾を放置する理由にはなりません。

