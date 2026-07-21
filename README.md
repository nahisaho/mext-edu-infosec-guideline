# 文部科学省 教育情報セキュリティポリシーガイドライン 改訂案・実装比較レポート

本リポジトリは、**令和6年法律第65号**による地方自治法第244条の5・第244条の6 の新設、および**令和8年総務省令第80号**（地方自治法施行規則第16条の3 の新設、令和9年7月1日施行）を踏まえ、**文部科学省「教育情報セキュリティポリシーに関するガイドライン」の改訂案**と、その要求水準に対する**Microsoft 365 Education 5 ライセンス構成の対応比較レポート**を作成した成果物一式である。

## 主要成果物

| ファイル | 概要 |
| --- | --- |
| [`proposal/revision-proposal.md`](proposal/revision-proposal.md) | 文部科学省ガイドライン改訂案（全 6 章）。244条の5／244条の6／施行規則第16条の3 への準拠を目的とした条項別改訂指針 |
| [`reports/m365-5licensing-comparison.md`](reports/m365-5licensing-comparison.md) | Microsoft 365 Education 5 ライセンス構成（A1 for Device／A3／A3+A5 Sec／A3+A5 Comp／A3+SASE／A5）の 8 分野対応マトリクス、構成別詳細対応方針、選定ガイド、コスト比較、実装チェックリスト |
| [`research/mapping-8measures.md`](research/mapping-8measures.md) | 施行規則第16条の3 第1項の 8 分野 × 総務省 GL × 文部科学省 GL の対応表 |
| [`research/followup-research.md`](research/followup-research.md) | 法令・通知に関する追加調査結果（附則、経過措置、サプライチェーン対策等） |
| [`research/report-244-jouhou-system.md`](research/report-244-jouhou-system.md) | 244条の5・244条の6 の新設趣旨と要件に関する調査レポート |
| [`references.md`](references.md) | 参考文献一覧（一次情報 URL・PDF・関連通知） |
| [`research/sources/`](research/sources/) | 総務省・文部科学省・IPA 等の一次情報 PDF と docling による Markdown 変換版 |

## 成果物作成の手順

本成果物は以下の 5 段階のワークフローで作成した。各段階でユーザーからの指示を受け、必要な調査・分析・レビュー・修正を実施している。

### Step 1. 一次情報の収集と Markdown 化

対象法令・通知・ガイドラインの一次情報を収集し、docling を用いて PDF を Markdown へ変換した。

**収集対象**（`research/sources/` に格納）：

| ファイル | 出典 |
| --- | --- |
| `soumu-tuchi-r6-244.md` | 令和6年法律第65号 地方自治法改正（244条の5・244条の6）に関する総務省通知 |
| `soumu-reiwa8-shorei-80.md` | 令和8年総務省令第80号（地方自治法施行規則第16条の3 の新設） |
| `soumu-tuchi-r8-shorei.md` | 令和8年総務省令第80号 施行に関する総務省通知 |
| `soumu-gl-r7-3.md` | 総務省「地方公共団体における情報セキュリティポリシーに関するガイドライン」令和7年3月版 |
| `soumu-shishin-an-r7-3-4.md` | 総務大臣指針（令和7年4月1日発出） |
| `soumu-cyber-summary-r8.md` | 総務省 令和8年サイバーセキュリティ関連通知 |
| `mext-handbook-r7-3.md` | 文部科学省 教育情報セキュリティポリシーガイドラインハンドブック（令和7年3月版） |
| `20250325-mxt_jogai01-100003157_1.md` | 文部科学省 令和7年3月25日付関連資料 |
| `ipa-cyber-anzen-hosyo.md` | IPA サイバーセキュリティ関連資料（サプライチェーン対策・JC-STAR 等） |

**主な指示**：
- 「令和6年法律第65号による地方自治法第244条の5・第244条の6 の新設、および令和8年総務省令第80号を調査し、レポート作成しファイルに保存」
- 「収集した PDF は docling を使用して Markdown に変換し保存」
- 「他に集めたほうがよい一次情報がないかどうかを確認」

### Step 2. 対応表（分野措置 × 総務省 GL × 文科省 GL）の作成

施行規則第16条の3 第1項の 8 分野（組織体制／情報資産分類／物理／人的／技術／運用／業務委託・クラウド／評価見直し）を軸に、総務省 GL と文部科学省 GL の該当節を突き合わせる対応表を作成。

**成果物**：[`research/mapping-8measures.md`](research/mapping-8measures.md)

**rubber-duck ファクトチェック（同一セッション内で別モデル gpt-5.6-sol サブエージェント）**：
- 文部科学省 GL 6.3・6.5・7.7・10.3 節の欠落を追記
- 7.8 節の SIEM 連携誤記、9.5 節の SNS 対象過大、7.9 節の捏造記述を修正
- 重要性分類 Ⅳ の扱い、サプライチェーン対策未反映断定の過大表現を是正
- 定義用語独立表、章再編案（2 案比較）注記を追加（計 8 件の誤り修正）

### Step 3. 文部科学省ガイドライン改訂案の作成

Step 2 の対応表を根拠に、条項別の改訂指針を全 6 章構成で作成。

**成果物**：[`proposal/revision-proposal.md`](proposal/revision-proposal.md)

**構成**：
1. 改訂の背景と目的
2. 法令の新設内容の要旨
3. 対応が必要な GL 章節と改訂方針
4. 経過措置・スケジュール
5. サプライチェーン対策（JC-STAR／ISMAP／DMP）の峻別
6. 附則・付録案

**rubber-duck ファクトチェック（gpt-5.6-sol）で反映した主要修正（12 件）**：
- 244条の5 を第1項（努力義務）／第2項（義務）に分記
- 244条の6 の主体を「議会及び長その他の執行機関がそれぞれ」に修正（教育委員会は独立主体）
- DMP を「Digital Marketplace（カタログ調達）」に修正
- 経過措置対象（附則第2項）を「第5号・第7号のみ」に限定明記
- スケジュールを R8.4.1 既施行（244条の6）を考慮して修正
- 総務大臣指針を「R7.4.1 付発出」に修正

### Step 4. Microsoft 365 5 ライセンス構成 対応レポートの作成

Step 3 の改訂案（要求水準）に対して、実自治体で導入されている代表的な 5 つのライセンス構成でどこまで適合可能か、不足事項に対するアップグレード or 運用対応の方針を全 7 章で整理。

**成果物**：[`reports/m365-5licensing-comparison.md`](reports/m365-5licensing-comparison.md)

**対象構成**：
| # | 構成 | 想定 |
| --- | --- | --- |
| ① | M365 A1 for Device | GIGA 端末（**教員が利用しているケースも含む**） |
| ② | M365 A3 | 教職員標準 |
| ③ | M365 A3 + A5 Security **又は** A5 Compliance Add-on | 一方向強化 |
| ④ | M365 A3 + 3rd party SASE | ネットワーク層補強 |
| ⑤ | M365 A5 | 教職員最上位 |

**構成**：
1. スコープ・前提
2. 構成別 機能サマリ（含有マトリクス）
3. 8 分野措置対応マトリクス
4. 構成別 詳細対応方針（適合／不足／アップグレード or オペレーション対応）
5. 構成選定ガイド
6. コスト・実装複雑度比較
7. 構成別 実装チェックリスト

**rubber-duck ファクトチェック（gpt-5.6-sol）で反映した主要修正**：

第 1 回（14 件、A1 GIGA + A3 版レポートで洗い出し）：
- Defender for Endpoint P1 は EDR ではない（EDR は P2）
- Defender for O365 P1／Defender Vulnerability Management は A3 に非含・アドオン
- Audit Standard は 180 日
- Entra ID P1 に Identity Protection なし（P2 が必要）
- Multi-Geo は日本固定機能ではない
- Cloud for Sovereignty は主に Azure 向け
- Attack Simulation Training は Defender for O365 P2 の機能

第 2 回（5 ライセンス比較版で追加、7 件）：
- Audit Premium は 1 年保持、10 年は別売 Add-on
- 「A5 = A3 + A5 Sec + A5 Comp + Power BI Pro」は厳密には成立しない
- A1 for Device 単独では条件付きアクセス実現不可
- SPF/DKIM/DMARC は Safe Links の代替ではない
- Defender for Identity はハイブリッド ID 脅威検知（Entra ID Protection と別）
- ASR ルールは Audit/Warn → Block の段階導入
- Sentinel A5 データグラントは対象データ・契約種別の条件あり

### Step 5. 教員が A1 for Device を利用しているケースの追記と再レビュー

「教員が A1 for Device を利用しているケースが実在する」というユーザーからの指摘を受け、§4.1 に専用サブセクションを追加。リスク認識・優先度付きアップグレード方針・必須オペレーション（認証／端末保護／情報保護／監視監査／研修／委託）・移行スケジュールを詳述。

**rubber-duck ファクトチェック（gpt-5.6-sol）で反映した重要修正**：
- A1 for Devices の Faculty SKU／Student SKU の区別と教員専用端末割当の前提を明記
- **Microsoft Defender AV のクラウド保護・自動サンプル送信・ASR ルールは Defender for Endpoint P1/P2 ライセンスが公式要件**であるため、A1 単独では正式サポート外である旨を反映（MDE P1 Add-on 追加購入推奨、又は WDAC 中心の代替へ変更）
- 附則第2項の経過措置は法令上期限を明示していないため、「令和10年度以降本格適用」を「本レポート独自の移行目標」と明示
- Security Defaults はテナント全体設定で教員のみ対象不可、per-user MFA を利用と修正
- Teams プライベートチャネルは DLP ではなくメンバー限定アクセス機能に過ぎない旨を明記

## 品質保証プロセス

すべての成果物は以下のフローで品質保証している：

1. **一次情報を必ず参照**（`research/sources/` の docling 変換 Markdown を根拠に記述）
2. **同一セッション内で別モデル（gpt-5.6-sol）による rubber-duck ファクトチェック**を必ず実施
3. **指摘事項を全て反映**した上で、末尾の**改訂履歴**に反映内容を明記
4. スタイル指摘は行わず、事実誤り・論理欠陥のみを対象とする

この「別モデルによる相互検証」プロセスにより、単一 LLM の思い込み・幻覚・古い知識に基づく誤りを機械的に検出・是正している。

## 用語・略称

| 略称 | 意味 |
| --- | --- |
| GL | ガイドライン |
| ISMAP | 政府情報システムのためのセキュリティ評価制度 |
| DMP | Digital Marketplace（総務省カタログ調達） |
| JC-STAR | IPA の IoT 製品セキュリティラベリング制度 |
| MDE | Microsoft Defender for Endpoint |
| MDO | Microsoft Defender for Office 365 |
| ASR | Attack Surface Reduction |
| WDAC | Windows Defender Application Control（現 App Control for Business） |
| AU | Administrative Unit（Entra ID 管理単位） |
| SASE | Secure Access Service Edge（SWG／CASB／ZTNA／FWaaS／DLP 統合） |
| PIM | Privileged Identity Management |

## 関連法令・通知

- 令和6年法律第65号（地方自治法改正／244条の5・244条の6 新設、R6.9.26 施行）
- 令和8年総務省令第80号（地方自治法施行規則第16条の3 新設、R9.7.1 施行）
- 総務大臣指針（R7.4.1 発出）
- 総務省「地方公共団体における情報セキュリティポリシーに関するガイドライン」令和7年3月版
- 文部科学省「教育情報セキュリティポリシーに関するガイドライン」（現行版）

詳細な出典 URL は [`references.md`](references.md) を参照。

## ライセンス・利用条件

本リポジトリの成果物（Markdown ドキュメント・レポート・図表等）は、[Creative Commons **表示 - 非営利 - 継承 4.0 国際（CC BY-NC-SA 4.0）**](https://creativecommons.org/licenses/by-nc-sa/4.0/deed.ja) ライセンスの下で提供する。全文は [`LICENSE`](LICENSE) を参照。

- **表示（BY）**：適切なクレジット表示、ライセンスへのリンク、変更の明示が必要
- **非営利（NC）**：営利目的での利用は禁止
- **継承（SA）**：改変・改作した派生物も同一ライセンス（CC BY-NC-SA 4.0）で頒布する必要がある

なお、本リポジトリは文部科学省向けの検討資料として作成されたものであり、内容は令和8年7月時点の情報に基づく。実際の施策・実装判断に用いる際は、最新の法令・Microsoft 公式ドキュメント・パートナー見積等で必ず追確認すること。

## 更新履歴

- 2026-07-21：LICENSE（CC BY-NC-SA 4.0）追加。README にライセンス条項を反映
- 2026-07-21：README 初版作成。Step 1〜5 のワークフロー、各成果物、rubber-duck 検証プロセスを整理
