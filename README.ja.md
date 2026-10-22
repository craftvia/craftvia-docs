# CraftVia Documentation

> [!IMPORTANT]
> **公開前ドキュメント**  
> CraftViaは初期ハードウェア開発段階です。Rev0の実装・検証結果により仕様が変更される可能性があります。英語版を正本とします。現在のRev0製品記述は凍結済み設計との照合結果であり、実機検証済みという意味ではありません。

[English](README.md) · [CraftVia](https://craftvia.org/ja/) · [GitHub Organization](https://github.com/craftvia)

このrepoでは、CraftVia全体に共通する公式公開文書を管理します。過去の日本語設計資料やロードマップは公開文書の入力資料であり、それ自体を公式仕様とはしません。

製品固有の編集可能な設計ソース、製造データ、Releaseノートは各ハードウェアrepoで管理します。

## ドキュメント一覧

| 公式公開文書 | 英語正本／日本語訳 |
| --- | --- |
| プロジェクト概要 | [`project/overview.md`](project/overview.md)／[`overview.ja.md`](project/overview.ja.md) |
| 用語集 | [`project/glossary.md`](project/glossary.md)／[`glossary.ja.md`](project/glossary.ja.md) |
| Versionと状態 | [`standards/versioning-and-status.md`](standards/versioning-and-status.md)／[`versioning-and-status.ja.md`](standards/versioning-and-status.ja.md) |
| Core-S Interface v1 | [`standards/core-s-interface-v1.md`](standards/core-s-interface-v1.md)／[`core-s-interface-v1.ja.md`](standards/core-s-interface-v1.ja.md) |
| Core-S共通デバッグ／書き込み／USBポート v1 | [`standards/core-s-debug-port-v1.md`](standards/core-s-debug-port-v1.md)／[`core-s-debug-port-v1.ja.md`](standards/core-s-debug-port-v1.ja.md) |
| 互換性方針・Matrix | [`standards/compatibility.md`](standards/compatibility.md)／[`compatibility.ja.md`](standards/compatibility.ja.md) |
| Rev0 Getting Started | [`guides/getting-started.md`](guides/getting-started.md)／[`getting-started.ja.md`](guides/getting-started.ja.md) |

製造データは、[Core-S G031](https://github.com/craftvia/craftvia-core-s-g031)、[Station-S](https://github.com/craftvia/craftvia-station-s)、[MakerCard-S](https://github.com/craftvia/craftvia-makercard-s)の各製品repoで管理します。

## 文書運用方針

- 英語を内容管理上の正本とする
- 日本語は英語版と同じディレクトリへ`.ja.md`付きで置き、正式な翻訳として管理する
- 技術仕様を`craftvia-web`へ重複掲載しない
- 製品固有の製造データは製品repoへ置く
- 構想、Draft、未検証仕様、検証済み仕様を明示する
- レビュー済み英語正本の公開後、内容に差異があれば英語版を優先する

## ステータス表記

| 状態 | 意味 |
| --- | --- |
| Concept | 方向性を示す資料。要求事項ではない |
| Draft | レビュー中であり変更される可能性がある |
| Unverified | 定義済みだが実機で未確認 |
| Verified | 対象ハードウェア、Revision、試験記録を特定して確認済み |
| Superseded | 履歴として保存されている旧版 |

## ライセンスとContribution

個別の表示がない限り、本リポジトリの文書は[CC BY 4.0](LICENSE)で提供します。ハードウェア設計にはCERN-OHL-P-2.0、ソフトウェアにはApache-2.0を、それぞれ対象として明示した場合に適用します。[ライセンス方針の正本（英語）](LICENSES/README.md)および[参考訳](LICENSES/README.ja.md)を参照してください。

CraftViaの名称・ロゴはこれらのオープンライセンスの対象外です。Kohei Ikedaが所有し、[CraftVia Trademark Policy（英語正本）](LICENSES/TRADEMARK_POLICY.md)および[参考訳](LICENSES/TRADEMARK_POLICY.ja.md)に従います。Contributionは、該当するリポジトリのライセンスで配布できることを前提として受け付けます。詳細な手続は別途Contributionポリシーで定めます。
