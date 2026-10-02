# Version、Revision、文書ステータス

> [英語版](versioning-and-status.md)を正本とします。

## 製品識別子

CraftViaのReleaseハードウェアは次の2つで識別します。

- **Version (`v`)**：製品またはインターフェースの世代
- **Revision (`Rev`)**：同一Version内のPCB設計改訂

```text
v1 Rev0   製品世代1の最初のPCB
v1 Rev1   同じ世代内の後続PCB改訂
v2 Rev0   世代変更後の最初のPCB
```

Git tagは`v1-rev0`、`v1-rev1`、`v2-rev0`の形式とします。

## 変更基準

接続形状、共通電源、主要な製品役割など、公開済みの互換性契約を意図的に破る変更では新しい**Version**を作ります。

製品世代を変えずに、回路・配線修正、フットプリント変更、設計に影響する部品変更、ハードウェア識別用シルク変更などを行う場合は新しい**Revision**を作ります。

文書だけの訂正は、それ自体では新しいHardware Revisionを必要としません。ただし凍結済み設計の意味を黙って変更してはなりません。

## ステータス

| 状態 | 意味 |
| --- | --- |
| **Concept** | 方向性を示す資料。要求事項ではない。 |
| **Draft** | レビュー中で変更される可能性がある。 |
| **Frozen** | 特定した設計・製造成果物が固定済み。実機は未検証の場合がある。 |
| **Unverified** | 必要な実機検証を完了していない。 |
| **Verified** | 特定した実機と証拠に基づき検証済み。 |
| **Rejected** | 試験の結果、受入条件を満たさなかった。記録は保持する。 |
| **Superseded** | 履歴として保持するが、別の文書・Version・Revisionに置き換えられた。 |

`Frozen`は変更管理、`Unverified`と`Verified`は証拠の状態を表します。したがって凍結済みRev0でも未検証です。

## Branch、tag、Release

- `main`は原則として最新の検証済みハードウェアを表す
- `develop`は設計・製造・実装・検証中の最新版を表す
- 検証済みRevisionがない初期段階では、警告を明示して未検証Rev0を`main`で公開できる
- 製造に使用したcommitへ注釈付きVersion／Revision tagを付ける
- 検証前のGitHub ReleaseはPre-releaseとし、未検証範囲を記載する
- tagは移動・再利用しない。設計修正には新しいRevisionを使う
- 検証合格後はtagged designを置換せず、状態と証拠を更新する

## 文書の識別

Revision固有文書には、製品名、Version、PCB Revision、文書状態、対象Release/tag、検証状態、Reference文書の場合は正本を明記します。

英語を正本とし、日本語訳は`.ja.md`を付けて同じフォルダへ置きます。

