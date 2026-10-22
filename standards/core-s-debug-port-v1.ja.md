# CraftVia Core-S 共通デバッグ／書き込み／USBポート v1

> [!WARNING]
> **状態：未検証仕様**
> Native USB対応Core-Sと適合Station-Sの組合せでは未検証です。[英語版](core-s-debug-port-v1.md)を正本とします。

## 1. 適用範囲

本書はCore-S北側N1～N8に配置する共通開発ポートのProfileを定義します。基本Debug／Download、任意JTAG／Trace、Native USBを分離し、Target USB接続によって主Recovery経路が置き換わらない構成とします。

Coreは実装するProfileだけを宣言します。宣言しないProfileの端子は実装固有GPIOまたはNCです。Stationは端子位置だけからProfileを仮定して駆動してはなりません。

## 2. 共通端子

信号方向はCore基準です。

| 端子 | 共通機能名 | 基本用途 | Profile依存機能 |
| --- | --- | --- | --- |
| N1 | `DBG_RESET` | Reset／Enable | 極性、pull、電気方式はCore Profileで定義 |
| N2 | `DBG_DATA0` | 双方向Data／Core受信 | SWDIO、UART RXD（Probe TX→Core RX）、JTAG TMS |
| N3 | `DBG_DATA1` | Clock／Core送信 | SWCLK、UART TXD（Core TX→Probe RX）、JTAG TCK |
| N4 | `DBG_BOOT` | Boot／Download mode選択 | Stationは通常High-Z。極性とReset sequenceはProfile依存 |
| N5 | `DBG_AUX0` | 拡張Debug入力 | JTAG TDI。非対応Coreでは実装固有GPIOまたはNC |
| N6 | `DBG_AUX1` | 拡張Debug出力 | JTAG TDOまたはSWO。非対応Coreでは実装固有GPIOまたはNC |
| N7 | `USB_DM` | Target USB D- | Native USB Profile宣言時だけUSB。非対応CoreではGPIOまたはNC |
| N8 | `USB_DP` | Target USB D+ | Native USB Profile宣言時だけUSB。非対応CoreではGPIOまたはNC |

N7/N8は隣接差動pairです。N8に隣接するK-NE/GNDはStationのGND planeへ短く接続します。N7/N8間へGND配線を挟みません。

## 3. Profile

### 3.1 `CVDBG-SWD`

| 端子 | 割り当て |
| --- | --- |
| N1 | nRESET／NRST |
| N2 | SWDIO |
| N3 | SWCLK |
| N4 | BOOTまたは論理Boot要求 |

N2は双方向です。StationはCoreが定めるBoot操作時以外N4をHigh-Zにします。N3/N4が同じMCU nodeへ到達する場合、Core個別仕様は分離方法を定め、競合駆動を禁止します。

### 3.2 `CVDBG-SWD-TRACE`

`CVDBG-SWD`へ`N6=SWO`を追加します。Traceを宣言しないCoreに対してStationはN6を接続しません。

### 3.3 `CVDBG-UART-DL`

| 端子 | 割り当て |
| --- | --- |
| N1 | RESET／EN |
| N2 | Core RXD、Probe TXから入力 |
| N3 | Core TXD、Probe RXへ出力 |
| N4 | BOOT／Download mode選択 |
| N5/N6 | 任意Handshakeまたは未使用 |

Station未接続時もCoreが通常起動できることを必須とします。UART Download対応だけではBreakpoint Debug対応を意味しません。

### 3.4 `CVDBG-JTAG`

| 端子 | 割り当て |
| --- | --- |
| N1 | Target Reset |
| N2 | TMS |
| N3 | TCK |
| N4 | BOOTまたはProfile固有制御 |
| N5 | TDI |
| N6 | TDO |

nTRSTは共通Profileへ割り当てません。nTRSTを必要とするCoreは実装方法を明記するかJTAG非対応を宣言します。MCUのpin remap、Security、Option byte、ErrataはCore固有条件です。

### 3.5 `CVDBG-USB`

| 端子 | 割り当て |
| --- | --- |
| N7 | USB_DM |
| N8 | USB_DP |

N7/N8はTargetのNative USBです。ROM Bootloader、Firmware更新、Console、内蔵USB Serial/JTAG、Application USB等の対応範囲はCore個別仕様で定めます。USB接続だけではSWD/JTAG相当のDebug対応を意味しません。

## 4. 電気条件と責任分界

### 4.1 Core-S側

- MCU／USB PHY固有のD+/D-直列終端、pull、bias
- PHY電源のdecouplingとClock条件
- Station未接続時のRESET、EN、BOOT安全状態
- MCUから接点までの配線とReset／未給電時状態の公開
- Option byte、pin remap、Security、Errata条件

MCUが必要なterminationやpull-upを内蔵する場合、一般化したUSB抵抗回路を重複して追加しません。

### 4.2 Station-S／Carrier側

- USB Connectorと、USB-Cの場合はCC／Port role回路
- VBUS保護とPower switch
- Connector直近の低容量ESD保護
- USB経路の選択／分離
- Debug Probe／UART経路の選択
- 未選択driverのHigh-Z安全状態

USB VBUSをCore-Sの+3V3へ直結しません。装着Coreが`CVDBG-USB`を宣言しない場合はUSB回路をN7/N8から分離し、JTAG／Traceを宣言しない場合はDebug driverをN5/N6から分離します。

## 5. Host動作

- Driver有効化前に装着CoreのProfileを検出または明示選択する
- 識別失敗時は全開発ポートdriver切離しを既定とする
- N2/N3へUSB信号を接続しない
- N7/N8へSWD、UART、JTAG driverを接続しない
- 1端子へ複数Probeまたは独立電源出力を同時接続しない
- USB切替にはUSB 2.0対応低容量switchを使用する
- USB stubを短くし、N7/N8を連続reference plane上で90 Ohm differentialを目標に配線する
- Core挿抜は電源OFF時だけ行う

## 6. Coreの宣言事項

Core個別仕様は次を公開します。

- 対応Profile名
- N1～N8のnet、MCU pin、Package pin
- 方向、電圧、pull、Reset／未給電時状態
- RESET／ENとBOOTの極性・操作手順
- 書き込み、Breakpoint Debug、Console、Trace、USB機能の対応範囲
- Recovery手順と必要Tool
- USB PHY固有部品とStation要求
- GPIO、Clock、Option byte、Securityとの競合

## 7. 旧N2/N3 USB Draft

過去の未検証Draftでは`N2=USB_D-`、`N3=USB_D+`を許可していました。このProfileを宣言したRelease済みCore-Sは存在しません。旧Profileは撤回し、新規Coreへ使用しません。

Station-S v1 Rev0は旧N2/N3 USB経路を物理実装しています。主目的のST-LINK／SWDには使用できますが、文書化されたReworkなしでは`CVDBG-USB`に適合しません。凍結済み設計ファイルはRev0実装の正本として保持します。

## 8. 適合と検証

宣言Profileを対象実機で確認するまでVerified適合を主張しません。最低限、次を確認します。

- Reset、Boot、書き込み、Recovery、未選択driver分離
- 信号電圧とTarget voltage検出
- 宣言時のUART方向
- 宣言時のJTAG／SWO経路
- USB宣言時のN7/N8極性、Enumeration、連続転送、SWD Recovery
- 非対応Profile経路を分離した安全状態
