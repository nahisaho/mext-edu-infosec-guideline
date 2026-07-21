# 教育情報セキュリティ 8 分野対応 × 5 ライセンス構成 比較レポート

**対象読者**：教育委員会の情報担当者・CISO 補佐、都道府県教育委員会の指導主事、Microsoft パートナー営業

**目的**：施行規則第16条の3（令和9年7月1日施行）の 8 分野措置に対する 5 つのライセンス構成の対応可能性を比較し、各構成の下でどのようなアップグレード又は運用（オペレーション）対応が必要かを示す

**準拠する改訂指針**：`proposal/revision-proposal.md`

**作成日**：令和8年7月

> [!IMPORTANT]
> Microsoft のライセンス構成・機能は随時変更される。本レポートは令和8年7月時点の公式資料に基づく。実装前に最新の Microsoft 公式ドキュメント（Microsoft 365 Education Licensing、Product Terms、Service Description）および ISMAP クラウドサービスリストで確認すること。

---

## 目次

1. [前提と 5 構成の概要](#1-前提と-5-構成の概要)
2. [構成別 機能サマリ](#2-構成別-機能サマリ)
3. [8 分野措置対応マトリクス](#3-8-分野措置対応マトリクス)
4. [構成別 詳細対応方針](#4-構成別-詳細対応方針)
   - 4.1 [構成①：M365 A1 for Device（GIGA 端末／教員が利用しているケースを含む）](#41-構成m365-a1-for-devicegiga-端末教員が利用しているケースを含む)
   - 4.2 [構成②：M365 A3（教職員標準）](#42-構成m365-a3教職員標準)
   - 4.3 [構成③：M365 A3 + A5 Security 又は A5 Compliance Add-on](#43-構成m365-a3--a5-security-又は-a5-compliance-add-on)
   - 4.4 [構成④：M365 A3 + 3rd Party SASE](#44-構成m365-a3--3rd-party-sase)
   - 4.5 [構成⑤：M365 A5](#45-構成m365-a5)
5. [構成選定ガイド](#5-構成選定ガイド)
6. [コスト・実装複雑度比較](#6-コスト実装複雑度比較)
7. [実装チェックリスト（構成別）](#7-実装チェックリスト構成別)

---

## 1. 前提と 5 構成の概要

### 1.1 想定シナリオ

| # | 構成 | 主な想定 |
| --- | --- | --- |
| ① | **M365 A1 for Device** | GIGA 端末（デバイス単位）ライセンス（GIGA Promo の後継）。**児童生徒だけでなく教員が利用しているケースも実在**（自治体の予算制約・GIGA 整備時の一括調達等の事情による） |
| ② | **M365 A3** | 教職員標準。予算制約下で追加投資なし |
| ③ | **M365 A3 + A5 Security 又は A5 Compliance Add-on** | 教職員に高度セキュリティ又は高度コンプライアンスのいずれか一方を追加 |
| ④ | **M365 A3 + 3rd Party SASE** | 教職員に Zscaler／Netskope／Prisma Access／Cato／Cloudflare One 等の SASE を組合せ |
| ⑤ | **M365 A5** | 教職員フル装備。A3 + A5 Security + A5 Compliance の主要セキュリティ／コンプライアンス機能に相当し、加えて Power BI Pro、Teams Phone、Audio Conferencing 等を包含（Add-on の等式ではない） |

### 1.2 構成①〜⑤の位置付けの補足

- 構成①は「デバイス単位」ライセンスで、GIGA スクール構想の一斉調達等の経緯から児童生徒のみならず**教員が業務端末として利用している自治体も実在**する。教員が A1 for Device を利用しているケースでは、施行規則第16条の3 の技術的セキュリティ・運用要求への適合が特に厳しく、**教員側を②〜⑤にアップグレードすることが強く推奨**される。アップグレードが直ちに困難な場合は §4.1 の「教員が A1 for Device を利用しているケース」の代替策を参照
- なお、教員側を②〜⑤に切り替えた場合でも、GIGA 端末を教員が共有／代替利用するシナリオは残り得るため、**テナント設計（同一テナント内でユーザー別ライセンス割当）と Intune デバイス管理の運用整合**を確認する必要がある
- 構成③の「A5 Security **又は** A5 Compliance」は排他的選択（両方付ければ実質⑤に近づく）
- 構成④の SASE は選定するベンダー・エディションによって含む機能が異なる（本レポートでは代表的な「SWG + CASB + ZTNA + FWaaS + DLP」機能セットを想定）
- 構成⑤は最上位で、A5 Security／A5 Compliance の主要セキュリティ・コンプライアンス機能を包含（Power BI Pro、Teams Phone、Audio Conferencing 等も含むが、Add-on だけでは完全な等式にならない）

### 1.3 評価対象の 8 分野

施行規則第16条の3 第1項に基づき、以下 8 号を評価軸とする。

1. 組織体制の整備
2. 情報資産の分類・管理
3. 物理的セキュリティ
4. 人的セキュリティ
5. 技術的セキュリティ（**経過措置対象**）
6. 運用（監視・遵守確認・インシデント対応）
7. 業務委託・クラウド（**経過措置対象**）
8. 評価・見直し

---

## 2. 構成別 機能サマリ

### 2.1 主要セキュリティ・コンプライアンス機能の含有マトリクス

**凡例**：
- ●：標準含有
- ○：Add-on で含有
- ―：含まれない（別途調達要）
- ▲：一部機能のみ（詳細は §4 各節参照）

| 機能領域 | ① A1 for Device | ② A3 | ③ A3+A5 Sec | ③ A3+A5 Comp | ④ A3+SASE | ⑤ A5 |
| --- | :-: | :-: | :-: | :-: | :-: | :-: |
| **Office 365 サービス**（Exchange/SPO/OneDrive/Teams） | ● | ● | ● | ● | ● | ● |
| **M365 Apps for enterprise**（デスクトップ Office） | ● | ● | ● | ● | ● | ● |
| **Windows 11 Pro Education**（永続） | ● | ― | ― | ― | ― | ― |
| **Windows 11 Enterprise アップグレード権** | ― | ● | ● | ● | ● | ● |
| **Intune for Education / Intune** | ● | ● | ● | ● | ● | ● |
| **Entra ID P1**（条件付きアクセス、静的 AU 管理者、MFA P1、動的グループ） | ― | ● | ● | ● | ● | ● |
| **Entra ID P2**（Identity Protection、PIM、Identity Governance、リスクベース CA） | ― | ― | ● | ― | ― | ● |
| **Defender for Endpoint P1**（次世代 AV、ASR、Web 保護） | ― | ● | ● | ● | ● | ● |
| **Defender for Endpoint P2**（EDR、脅威ハンティング、自動調査・修復、コアの脅威・脆弱性管理） | ― | ― | ● | ― | ▲注1 | ● |
| **Defender for Office 365 P1**（Safe Links／Safe Attachments） | ― | ― | ● | ― | ▲注2 | ● |
| **Defender for Office 365 P2**（Attack Simulation Training、Threat Explorer 拡張） | ― | ― | ● | ― | ― | ● |
| **Defender for Identity**（オンプレ AD DS／AD FS／AD CS 等ハイブリッド ID 脅威検知） | ― | ― | ● | ― | ― | ● |
| **Defender for Cloud Apps** フル（CASB） | ― | ▲Discovery のみ | ● | ▲Discovery のみ | ▲注3 | ● |
| **Purview Information Protection**（手動・既定・必須ラベル、暗号化、基本 DLP） | ― | ● | ● | ● | ● | ● |
| **Purview 自動ラベル付け（Automatic labeling）** | ― | ― | ― | ● | ― | ● |
| **Purview DLP 拡張**（Endpoint DLP、Teams DLP） | ― | ▲一部 | ▲一部 | ● | ▲SASE 側 DLP | ● |
| **Purview Insider Risk Management** | ― | ― | ― | ● | ― | ● |
| **Purview eDiscovery Premium** | ― | ― | ― | ● | ― | ● |
| **Purview Communication Compliance** | ― | ― | ― | ● | ― | ● |
| **Purview Records Management** | ― | ― | ― | ● | ― | ● |
| **Purview Audit Standard**（180 日） | ● | ● | ● | ● | ● | ● |
| **Purview Audit Premium**（1 年保持。10 年保持は「10-Year Audit Log Retention Add-on」でユーザー単位に別売） | ― | ― | ― | ● | ― | ● |
| **Customer Lockbox** | ― | ― | ― | ● | ― | ● |
| **SWG（Web フィルタリング・マルウェア）** | ― | ▲Defender Web 保護 | ▲同左 | ▲同左 | ● SASE 側 | ▲同左 |
| **ZTNA（Zero Trust Network Access）** | ― | ▲条件付きアクセスで代替可 | ▲同左 | ▲同左 | ● SASE 側 | ▲同左 |
| **FWaaS**（クラウド型ファイアウォール） | ― | ― | ― | ― | ● SASE 側 | ― |
| **RBI（Remote Browser Isolation）** | ― | ― | ― | ― | ● SASE 側（要オプション） | ― |

**注1**：SASE 側でも一部エンドポイントエージェント・ML 検知を提供する製品あり（例：Palo Alto Cortex XDR、Netskope Endpoint DLP）が、Microsoft ネイティブの Defender for Endpoint P2 とは別  
**注2**：SASE 側の Email Security 機能を持つ製品（例：Cloudflare Area 1）を組み合わせれば代替可  
**注3**：SASE 側 CASB（Netskope、Zscaler ZIA CASB 等）で機能的に重なる。ただし M365 ネイティブ制御は Defender for Cloud Apps に限定

---

## 3. 8 分野措置対応マトリクス

**凡例**：
- ◎：標準機能で対応可能
- ○：機能＋運用整備で対応可能
- △：機能不足あり。運用強化・アドオン・SASE 補完等が必要
- ×：構成のみでは対応困難

### 3.1 8 分野 × 5 構成 サマリ

| 分野（施行規則第16条の3 第1項） | ① A1 for Device | ② A3 | ③ A3+A5 Sec | ③ A3+A5 Comp | ④ A3+SASE | ⑤ A5 |
| --- | :-: | :-: | :-: | :-: | :-: | :-: |
| **第1号 組織体制**（※注A） | △ | ○ | ○ | ○ | ○ | ○ |
| **第2号 情報資産の分類・管理** | × | △ | △ | ◎ | △ | ◎ |
| **第3号 物理的セキュリティ**（GIGA 端末含む）（※注A） | ○ | ○ | ○ | ○ | ○ | ○ |
| **第4号 人的セキュリティ**（研修・訓練含む）（※注A） | △ | △ | ○ | △ | △ | ○ |
| **第5号 技術的セキュリティ** ※経過措置 | × | △ | ◎ | △ | ○ | ◎ |
| **第6号 運用**（監視・遵守・インシデント） | △ | △ | ◎ | ○ | △ | ◎ |
| **第7号 業務委託・クラウド** ※経過措置（※注A） | ○ | ○ | ○ | ○ | ○ | ○ |
| **第8号 評価・見直し** | ○ | ○ | ○ | ◎ | ○ | ◎ |

**注A**：組織体制、物理的セキュリティ、人的セキュリティ、業務委託・クラウドは**制度・規程・運用体制で達成する分野**であり、ライセンス機能だけでは達成できない。上表は「製品機能による支援度」を示すもので、法令上の適合度そのものではない（実際には規程整備・研修実施・監査等の運用整備が必須）。

**総合評価**：構成⑤（A5）と構成③の A3+A5 Security の組合せが技術面では最も広くカバーする。構成③の A5 Compliance 単独ではコンプライアンス寄りで技術的検知に弱く、構成④は Network/Web 層で②を大きく補完するが Purview 系機能に届かない。

---

## 4. 構成別 詳細対応方針

以下、各構成について「①適合できる要求」「②不足事項」「③対応方針（アップグレード or オペレーション）」の三段構成で整理する。

### 4.1 構成①：M365 A1 for Device（GIGA 端末／教員が利用しているケースを含む）

> **本節の対象**：本節は児童生徒端末単独想定に加え、**教員が業務端末として A1 for Device を利用しているケース**（GIGA 一斉調達等で教員にも A1 for Device が割り当てられている自治体）についても扱う。教員利用は施行規則第16条の3 の要求上、児童生徒利用より厳しい適合性が求められるため、後半に**教員が A1 for Device を利用しているケース向けの追加対応**を独立させて記載する。
>
> **ライセンス上の前提**：A1 for Devices は **Faculty 用 SKU（M365 A1 for Devices Faculty）と Student 用 SKU（M365 A1 for Devices Student）が別 SKU**として存在する。教員に割り当てる場合は必ず Faculty SKU を用い、**教員専用端末**に割り当てる必要がある（Microsoft の Education Licensing FAQ 上、A1 for Devices は複数ユーザーの同時利用・共有端末用途は非対応）。GIGA 端末を教員と児童生徒が真に共用している場合はライセンス条件との整合を確認すること。

#### 適合できる要求
- 第3号（物理）：BitLocker 全端末暗号化、Intune Wipe、Autopilot Reset による廃棄時消去
- 第7号：Microsoft 365 は ISMAP 登録済み（言明範囲要確認）
- 基本的な Office 365 サービスの利用

#### 不足事項
- **Defender for Endpoint 非装備**（OS 標準 Microsoft Defender Antivirus のみ。ただしクラウド保護・自動サンプル送信・ASR ルールは Microsoft の公式ドキュメント上、**Defender for Endpoint P1 又は P2 のライセンスが必要**とされているため、A1 for Device 単独では正式サポート範囲外。Intune の設定項目自体は表示されるが、ライセンス要件を満たさない構成となる）
- **Entra ID P1 なし**：条件付きアクセス、静的 AU の学校別権限委譲不可
- **Purview 情報保護なし**：機密ラベル・DLP 不可
- 監査ログ Audit Standard 180 日のみ

#### 対応方針

**A. アップグレード推奨（技術的対応が困難な場合）**：
- 教員が A1 for Device を利用しているケースでは、**教員側に A3 以上（ユーザーライセンス）を追加割当**することを最優先で推奨。A1 for Devices（Faculty）はデバイス単位ライセンスであり、A3 ユーザーライセンスと同一テナント内で併存可能。A3 ユーザーライセンスを割当てられた教員は A3 の**ユーザー権利**（Entra ID P1、Defender for Endpoint P1、Purview IP、Intune ユーザー単位機能等）を利用可能となるが、実際に機能を有効化するには **Defender for Endpoint のオンボーディング、Intune/Purview ポリシー割当、Windows サブスクリプション認証等の別途構成**が必要（サインインだけで自動有効化されるわけではない）
- 児童生徒端末を教職員テナント経由で管理する場合は Entra ID P1 相当のライセンスを教職員に付与
- 重要な学習履歴を保管する場合は児童生徒側にも **Defender for Endpoint P1/P2 for Student**（Education 向け廉価版）の付与を検討

**B. オペレーション対応（アップグレードできない場合）**：

| 不足事項 | オペレーション対応 |
| --- | --- |
| EDR／AV クラウド保護 不足 | (1) **Microsoft Defender Antivirus のクラウド保護・自動サンプル送信・ASR ルールは公式にはライセンス要件として MDE P1/P2 を要求**するため、ライセンス整合性を保つには Defender for Endpoint P1（または P2）Add-on の追加購入が事実上必要（少額のためユーザー単位追加を推奨）<br>(2) 追加購入が困難な場合、**Windows Defender Application Control（WDAC / App Control for Business）**（Windows 11 Pro Education でも Intune 配布可能）による許可アプリ制限を軸とする<br>(3) ネットワーク境界（学校側 UTM/プロキシ）でマルウェア検知・ブロック |
| 条件付きアクセス不可 | (1) A1 for Device **単独では条件付きアクセスは実現不可**（要 Entra ID P1）。教員側にユーザー単位で Entra ID P1 相当を追加購入するか、児童生徒アカウント側にもユーザー単位で P1 を追加購入<br>(2) 補完策として、境界側（学校側 UTM／SASE／プロキシ）で IP アドレス・URL によるアクセス制御<br>(3) SCEP／PKCS 証明書を Intune で配布した「管理端末」のみを Wi-Fi/VPN 接続許可とするネットワーク層制御（ただしこれは「管理端末である」ことの識別であり、Entra 条件付きアクセスの「Intune 準拠状態」判定と同等ではない） |
| 情報保護なし | (1) OneDrive の**外部共有を全面無効化**（テナント設定）<br>(2) 転送・持出防止は Intune ポリシーで OneDrive/SharePoint の**同期禁止・ダウンロード制限**<br>(3) 分類は「重要性分類 Ⅳ 相当のみ扱う」運用ルール |
| 監査ログ短期 | (1) **Office 365 Management Activity API / Microsoft Graph API** を用いて外部 SIEM／Log Analytics に取得（Sentinel 用の M365 コネクタが利用可）<br>(2) 直接の診断設定転送はサポート外のため、収集遅延・API スロットリング・重複排除・保管コストを設計時に考慮<br>(3) 別途 SIEM 運用（学校側で運用する場合） |

**C. A1 for Device 単独では絶対にできない要求**：
- 第2号「情報資産の分類」の技術的統制（機密ラベル）
- 第4号「サイバー攻撃訓練」（Attack Simulation Training）
- 第5号「本格的な EDR・脅威ハンティング」

#### 【追加】教員が A1 for Device を利用しているケース向けの対応

**リスク認識**：
- 教員が扱う情報資産は児童生徒本人が扱うそれよりも重要性分類が高い場合が多い（成績、指導要録、児童生徒の家庭状況、健康診断結果、要保護対象者情報等が**重要性分類 Ⅰ〜Ⅱ相当**に該当し得る）
- A1 for Device では条件付きアクセス、機密ラベル、DLP、EDR、監査ログ長期保持がいずれも欠落しており、**現行の文部科学省ガイドラインの技術的セキュリティ要求（強度パスワード＋MFA、機密性の高いデータの暗号化・DLP、EDR 相当の検知等）に構造的に適合しない**
- 施行規則第16条の3 第1項第5号（技術的セキュリティ）は**令和9年7月1日以降**、附則第2項により「施行時に現に存する情報システム等・現に実施中の業務委託」については「なお従前の例による」経過措置が置かれるが、**新規システム・新規委託は令和9年7月1日から本則適用**となる。附則には期限が明示されておらず、「令和10年度以降本格適用」は法令上の期限ではなく、後述する本レポート独自の移行目標である

**最優先の対応（推奨順）**：

| 優先度 | 対応 | 補足 |
| --- | --- | --- |
| ★1 | **教員のみ A3 ユーザーライセンス（または A5）にアップグレード**し、既存の A1 for Device と併用 | デバイスライセンスは残し、ユーザーライセンスを追加する形。教員は A3 の**ユーザー権利**（Entra ID P1、Defender for Endpoint P1、Purview IP、Intune ユーザー単位機能等）を利用可能となるが、実際に機能を有効化するには MDE オンボーディング、Intune/Purview ポリシー割当、Windows サブスクリプション認証等の別途構成が必要 |
| ★2 | 予算制約でユーザーライセンス追加が困難な場合、**重要性分類 Ⅰ・Ⅱ の情報資産を扱う教員から段階的に**アップグレード（校長・教頭・情報担当・成績処理担当・特別支援担当を優先） | 全教員一斉が困難でも、リスクの高い教員から段階導入 |
| ★3 | それも困難な場合、**教員による重要性分類 Ⅰ・Ⅱ 情報資産の A1 端末での取扱いを規程で全面禁止**し、成績処理・指導要録処理等は**校内サーバ／別途整備した業務系端末（校務系ネットワーク側）で実施**する運用分離 | 令和9年施行規則対応では技術的統制の代替として運用統制の明文化・監査が必要 |

**教員が A1 for Device を継続利用する場合の必須オペレーション**：

| 分野 | オペレーション対応 |
| --- | --- |
| **認証** | (1) MFA を全教員に**強制**する。**Security Defaults はテナント全体設定で児童生徒を含む全ユーザーが対象となり教員のみへの適用は不可**、教員のみを対象とする場合は **per-user MFA（Legacy MFA）** を用いる。将来的な運用簡素化のため教員側に Entra ID P1 追加購入 → 条件付きアクセスへの移行を推奨<br>(2) パスワードポリシーを最強化、レガシー認証プロトコル無効化<br>(3) 教員アカウントは**児童生徒アカウントとテナントまたはドメイン分離**が理想（同一テナントの場合は AU ではなくロール割当と規程で分離） |
| **端末保護** | (1) BitLocker 強制、SCEP/PKCS 証明書を Intune で配布した「管理端末」のみに Wi-Fi/VPN 接続を許可する**ネットワーク層制御**（学校 UTM/SASE 側で証明書検証。ただし Entra 条件付きアクセスの「Intune 準拠状態」判定と同等ではない点に留意）<br>(2) **Microsoft Defender AV のクラウド保護・自動サンプル送信・ASR ルールは公式には Defender for Endpoint P1/P2 のライセンスが必要**（Microsoft Learn 明記）。ライセンス整合性を保つため、教員には最低限 **MDE P1 Add-on の追加購入**を推奨。追加購入不可の場合は WDAC（App Control for Business）による許可アプリ制限を軸とし、AV クラウド保護・ASR は「ライセンス上の正式サポートなし」を認識した上でリスク受容判断<br>(3) USB 大容量ストレージは **Intune Settings Catalog で既定拒否**（Endpoint DLP がないため機器レベルで抑止） |
| **情報保護** | (1) **重要性分類 Ⅰ・Ⅱ の情報は OneDrive/SharePoint 保存禁止**を規程化<br>(2) 教員 OneDrive の**外部共有を「特定のユーザーのみ」または全面無効**<br>(3) メール送信時の重要データ添付は **Exchange Online の Transport Rule（メールフロールール）で拒否・警告**（キーワード・添付ファイル種別・宛先ドメインで判定。テナント管理者が設定し、A1 メールボックスにも適用される）<br>(4) 教員間の機密共有はメンバー限定の **Teams プライベートチャネル**を活用しつつ、**外部共有無効化・メンバー管理・監査ログ確認を必ず併用**（プライベートチャネル自体は DLP や誤投稿防止機能ではない） |
| **監視・監査** | (1) Audit Standard（180 日）を **Management Activity API 経由**で SIEM/Log Analytics に転送し 1 年以上保持<br>(2) サインインログ・監査ログの**週次目視レビュー**（IP、失敗回数、権限変更、大量ダウンロード等）<br>(3) インシデント発生時の**外部フォレンジック契約**を事前締結 |
| **研修・訓練** | (1) Attack Simulation が使えないため、**教育委員会主催で年 2 回以上の対面フィッシング訓練**（人手による疑似メール送信、開封率・報告率記録）<br>(2) 情報セキュリティ研修を**教員層に必修化**（年 1 回以上、受講記録を保存） |
| **委託・クラウド** | (1) 教員が業務利用する SaaS は**教育委員会が事前承認したもののみ**（シャドー IT 防止、Defender for Cloud Apps がないため Web プロキシログの手動確認）<br>(2) 承認 SaaS は令和8年通知に基づき **ISMAP または DMP 登載サービス**を優先 |

**移行スケジュール（教員 A1 継続利用ケース）** ※法令上の期限ではなく本レポート独自の移行目標：

| 時期 | アクション |
| --- | --- |
| 令和9年3月まで | 教員の情報資産取扱状況を分類（重要性分類 Ⅰ〜Ⅳ）、A3 追加割当予算の要求 |
| 令和9年7月（施行規則施行） | 経過措置対象（施行時に現存するシステム・現に実施中の委託）以外は本則適用のため、新規調達・新規委託は本則準拠。既存分は経過措置適用中も規程整備・上記オペレーション対応の実装を進める |
| 令和10年度以降（推奨目標） | 附則第2項の経過措置は期限が法令上明示されていないが、リスク低減の観点から**教員全員の A3 以上への切替を完了**することを推奨（少なくとも重要性分類 Ⅰ・Ⅱ 取扱者は必須） |

---

### 4.2 構成②：M365 A3（教職員標準）

#### 適合できる要求
- 第1号：Entra ID P1 の Administrative Unit（静的）で学校単位委譲
- 第3号：BitLocker、Intune 全機能
- 第4号：MFA 強制、パスワードレス
- 第5号（部分）：Defender for Endpoint P1 の次世代 AV・ASR・Web 保護、Intune コンプライアンス連動条件付きアクセス
- 第7号：ISMAP 登録済み
- 第8号：Secure Score、Compliance Manager

#### 不足事項

| 分野 | 不足機能 |
| --- | --- |
| 第2号 | 自動ラベル付け、Endpoint DLP、Insider Risk |
| 第4号 | **Attack Simulation Training**（Defender for O365 P2 要）、フィッシング訓練 |
| 第5号 | **EDR・脅威ハンティング**（Defender for Endpoint P2 要）、**Defender Vulnerability Management 拡張機能**（P2 にコア機能は含まれるが、拡張インベントリ等は Add-on）、**Identity Protection**（Entra ID P2）、**Safe Links/Safe Attachments**（Defender for O365 P1 要） |
| 第6号 | 統合 XDR、Defender for Identity、Audit Premium |
| 第8号 | eDiscovery Premium、Records Management |

#### 対応方針

**A. アップグレード推奨（優先順位順）**：
1. **Defender for Office 365 P1 Add-on**（Safe Links/Attachments は最小限の予防策として必須級）
2. **Defender for Endpoint P2 Add-on**（EDR 装備）
3. **Entra ID P2 Add-on**（少なくとも特権 ID・管理者向け）
4. **Purview Audit Premium**（監査ログ 1 年保持）

**B. オペレーション対応（追加ライセンスなしで対応する場合）**：

| 不足事項 | オペレーション対応 |
| --- | --- |
| EDR なし | (1) Defender for Endpoint P1 の**ASR ルールを段階導入**（LSASS 認証情報保護、Office マクロブロック等）。**まず Audit/Warn モードで業務影響を評価**し、除外設計後に Block 移行する（全ルール一括 Block は業務アプリを停止させる恐れあり）<br>(2) **Windows イベントログを Log Analytics に集約**して手動でクエリ分析<br>(3) インシデント疑い時は Microsoft サポート（プレミアサポート契約時）に依存 |
| Safe Links/Attachments なし | (1) Exchange Online Protection（EOP、A3 標準）の**アンチスパム・アンチマルウェア**を最大限に設定<br>(2) 添付ファイルフィルタ（実行可能ファイル、Office マクロ）を **Transport Rule** で強化<br>(3) **送信ドメイン認証（SPF/DKIM/DMARC）を強制**することで送信元偽装を抑止（ただし URL 検査・クリック時再評価は行われないため、リンク経由の攻撃リスクは残存）<br>(4) URL 検査を必要とする重要業務は境界側 SWG/SASE 側で補完 |
| Identity Protection なし | (1) 条件付きアクセスの**「サインインの場所」「デバイスコンプライアンス」「クライアントアプリ」条件**で疑似的なリスクベース制御<br>(2) Entra ID **サインインログの日次目視レビュー**（IP、デバイス、失敗回数）<br>(3) MFA を全教職員に強制、レガシー認証プロトコル無効化 |
| Attack Simulation なし | (1) 総務省・IPA・NISC・JC3 が提供する**無償の教育資料・訓練プログラム**を活用<br>(2) 教育委員会レベルで実施する**年 1 回以上の情報セキュリティ研修**でメール開封訓練を実施（人手による疑似メール送信） |
| Vulnerability Management なし | (1) **総務省地方版 ASM システム**（提供予定）で外部露出資産を把握<br>(2) Microsoft Update for Business + Intune で**パッチ適用状況モニタ**<br>(3) IPA JVN 定期購読で脆弱性情報収集 |
| Insider Risk なし | (1) OneDrive/SharePoint の**外部共有ログの日次確認**<br>(2) Purview Content Search で**キーワード検索を月次実施**<br>(3) 大量ダウンロード等は監査ログから手動抽出 |

**C. A3 単独では絶対に難しい要求**：
- リアルタイム脅威検知・自動対応
- 児童生徒データの海外事業者クラウドでの高度な暗号化キー管理（BYOK/HYOK）
- FERPA 相当の詳細な閲覧監査（Audit Premium 要）

---

### 4.3 構成③：M365 A3 + A5 Security 又は A5 Compliance Add-on

#### A5 Security Add-on を選択した場合

**含まれる機能**（A3 に加えて）：
- Defender for Endpoint P2（フル EDR、コアの脅威・脆弱性管理）
- Defender for Office 365 P2（Safe Links、Attack Simulation Training）
- Defender for Identity（オンプレ AD DS/AD FS/AD CS 等ハイブリッド ID 脅威検知）
- Defender for Cloud Apps（フル CASB）
- Entra ID P2（Identity Protection、PIM）

**適合できる要求**：
- 第1号：Entra ID P2 の **PIM** で特権 ID の期限付き昇格
- 第4号：Attack Simulation Training で全教職員フィッシング訓練
- 第5号：**フル EDR による標的型攻撃検知**、Identity Protection によるリスクベース CA、Defender Vulnerability Management のコア機能（拡張インベントリ等の全機能は Add-on 別売）
- 第6号：**Defender XDR による統合インシデント調査**
- 第8号：**Secure Score 大幅向上**、Compliance Manager アクション拡充

**残る不足**：
- 自動ラベル付け（Purview Information Protection）
- Insider Risk Management、Communication Compliance
- eDiscovery Premium、Audit Premium、Records Management

#### A5 Compliance Add-on を選択した場合

**含まれる機能**（A3 に加えて）：
- Purview Information Protection 自動ラベル付け
- Purview Insider Risk Management
- Purview Communication Compliance
- Purview eDiscovery Premium
- Purview Audit Premium（監査ログ 1 年保持。10 年保持は「10-Year Audit Log Retention Add-on」でユーザー単位に別売）
- Purview Records Management
- Customer Lockbox
- Endpoint DLP、Teams DLP

**適合できる要求**：
- 第2号：**自動ラベル付けで児童生徒データを自動分類**、Endpoint DLP で USB 持出制限、Teams DLP
- 第6号：Audit Premium で監査ログ長期保持、Insider Risk で内部脅威検知
- 第8号：eDiscovery Premium で保護者・議会等からの開示請求に高度対応、Records Management で法定帳簿の保持ポリシー

**残る不足**：
- **フル EDR**（Defender for Endpoint P2）
- Attack Simulation Training
- Defender for Identity、フル CASB
- Entra ID P2

#### 対応方針

**A. どちらを選ぶかの判断基準**：

| 選択 | 適する自治体 |
| --- | --- |
| **A5 Security** | 標的型攻撃・ランサムウェア被害の懸念が高い／教育情報システムのインシデントが過去に発生／CSIRT 相当の体制構築を目指す |
| **A5 Compliance** | 児童生徒データの適正管理・議会や保護者への開示対応・監査対応を重視／個人情報保護委員会からの指導実績あり |

**B. 各選択の欠落分に対するオペレーション対応**：

**A5 Security を選んだ場合の Compliance 側補完**：

| 不足事項 | オペレーション対応 |
| --- | --- |
| 自動ラベル付け | 手動・既定ラベルの徹底適用、教職員向けラベル付与研修、SharePoint Site 単位の**既定ラベル**設定 |
| Insider Risk | Entra ID サインインログ・Purview Audit の**月次目視レビュー**、大量ダウンロード検知の自作 KQL クエリ |
| Audit Premium | 標準 Audit 180 日 + **Office 365 Management Activity API 経由で Log Analytics/SIEM に転送**して長期保持を確保（Azure 課金、API 制限・遅延・重複排除に留意） |
| eDiscovery Premium | Purview Content Search（標準）で対応、複雑ケースは外部弁護士・監査法人に委託 |

**A5 Compliance を選んだ場合の Security 側補完**：

| 不足事項 | オペレーション対応 |
| --- | --- |
| EDR なし | Defender for Endpoint P1 の ASR ルール、境界防御（プロキシ/UTM/SASE 別途）、疑い時の外部フォレンジック契約 |
| Attack Simulation | 無償教育資料・人手による疑似訓練、IPA/JPCERT の演習ツール |
| Identity Protection | 条件付きアクセス（IP・デバイス・場所）で疑似実装、サインインログ日次確認 |
| Defender for Identity | オンプレ AD がある場合は**イベントログを Sentinel 又は Log Analytics 転送**、UBA は限定的 |

---

### 4.4 構成④：M365 A3 + 3rd Party SASE

#### SASE で補完される機能（代表的）

| SASE 機能 | 対応する 8 分野要求 |
| --- | --- |
| **SWG**（Secure Web Gateway） | 第5号：Web フィルタリング、URL 分類、マルウェアスキャン。Defender for Endpoint Web 保護より広範 |
| **CASB**（Cloud Access Security Broker） | 第2号：シャドー IT 検出、SaaS DLP。**M365 の Defender for Cloud Apps 相当＋非 M365 SaaS もカバー** |
| **ZTNA**（Zero Trust Network Access） | 第5号：VPN 代替、アプリ単位アクセス制御。特に校務系オンプレシステムへの安全アクセス |
| **FWaaS**（Firewall as a Service） | 第5号：クラウド型ファイアウォール、東西トラフィック検査 |
| **DLP**（Data Loss Prevention） | 第2号：ネットワーク層 DLP。Purview DLP と補完関係 |
| **RBI**（Remote Browser Isolation） | 第5号：Web ベース攻撃の完全隔離 |
| **DNS Security** | 第5号：DNS レベルで C2 通信ブロック |

#### 適合できる要求（A3+SASE の相乗効果）
- 第5号：Web・ネットワーク層の防御が大幅強化。**EDR には至らない**が、感染前の予防に効果大
- 第2号：ネットワーク層 DLP + M365 Purview の二重防護
- 第6号：SASE 側ログ + M365 監査ログの**統合ログ分析**（SIEM 連携）
- 第7号：SASE の**細粒度な SaaS 制御**により、非承認クラウドサービスの利用を抑止

#### 残る不足
- **エンドポイント EDR は依然として不足**（SASE はネットワーク中心）
- Purview 高度機能（Insider Risk、eDiscovery Premium、自動ラベル）
- Identity Protection（Entra ID P2）
- Defender for Identity

#### 対応方針

**A. アップグレード推奨（SASE との重複回避）**：
- **Entra ID P2 Add-on**（Identity Protection は SASE でも代替不可）
- **Defender for Endpoint P2 Add-on**（SASE ではエンドポイント EDR は代替不可、ただし一部 SASE ベンダーは EDR 機能を持つ）
- **Purview Audit Premium**（監査ログ長期保持）

**B. オペレーション対応**：

| 不足事項 | オペレーション対応 |
| --- | --- |
| EDR なし | (1) SASE 側の**Endpoint Agent の脅威検知機能を最大活用**（Palo Alto Cortex、Netskope Endpoint 等）<br>(2) Defender for Endpoint P1 の ASR ルール＋SASE のネットワーク検知で二層防御<br>(3) 侵害時は SASE ログ・Windows イベントログを SIEM で相関分析 |
| Purview 高度なし | (1) SharePoint/OneDrive の外部共有制限徹底<br>(2) 手動ラベル運用 + SASE 側 DLP でネットワーク流出防止 |
| Identity Protection なし | (1) SASE の**ユーザー行動分析（UEBA）**（対応ベンダーの場合）を活用<br>(2) Entra ID サインインログを SASE の SIEM/UEBA モジュールに連携 |

**C. SASE 導入時の注意事項**：
- **M365 との重複機能の整理**（Defender for Endpoint Web 保護 vs SASE SWG 等）
- **SSL/TLS 復号のプライバシー影響評価**（児童生徒データを扱うため要慎重）
- **SASE ベンダーの ISMAP 登録状況**は「サービス名・言明範囲・登録番号・有効期限」の単位で確認する（ベンダー単位で「登録済み／未登録」と断定しない）。契約対象サービスが言明範囲に含まれているかを個別に照合する
- **国内データセンター利用**の契約明記
- **CLOUD Act 等外国法執行機関リスク**の評価（SASE ベンダーも米国系が多い）
- **総務省地方版 ASM システム**との整合（重複しないよう役割分担）
- Microsoft と SASE ベンダー**両方に対する令和8年通知のサプライチェーン評価**が必要

---

### 4.5 構成⑤：M365 A5

#### 含まれる機能（教職員向け最上位パッケージ）
- A3 の全機能
- A5 Security Add-on 相当のセキュリティ機能
- A5 Compliance Add-on 相当のコンプライアンス機能
- Power BI Pro、Teams Phone Standard、Audio Conferencing 等（通話プラン等の一部は別途）
- ※ 厳密な等式（A5 = A3 + A5 Sec + A5 Comp + Power BI Pro）ではなく、追加コンポーネントも含まれる

#### 適合できる要求
- **第2、5、6、8号を機能面で広くカバー可能**（第1、3、4、7号は運用・規程整備が別途必須）
- **フル EDR + 統合 XDR + Identity Protection + 自動ラベル + Insider Risk + eDiscovery Premium** が全て利用可能
- Microsoft Sentinel と組み合わせれば**フル SIEM/SOAR** も実現可能（別途 Azure 課金）

#### それでも残る不足・要検討事項

| 事項 | 対応 |
| --- | --- |
| **Microsoft Sentinel（SIEM）** | A5 に含まれない。Azure 従量課金で追加。ただし **Microsoft 365 E5/A5 契約者向けデータグラント**として、対象となる一部の Microsoft 365 データ（Office 365、Entra ID、Defender 系等）の Sentinel 取り込みに 5MB/ユーザー/日 相当の無料枠が提供される（EA/EAS/CSP 等の契約種別・対象データに条件あり、要ライセンスガイド確認） |
| **地方版 ASM** | Microsoft 外のインターネット露出資産可視化は総務省地方版 ASM を利用 |
| **CLOUD Act リスク** | A5 でも解消されない。Microsoft Cloud for Sovereignty 個別評価 |
| **サードパーティ製 SASE** | ネットワーク層防御を強化する場合は別途 SASE を組み合わせる価値あり（③ の代替として） |
| **児童生徒側 A1**  | 依然として A1 のまま。A5 は教職員のみ、児童生徒側は別建て |

#### 対応方針

**A. アップグレード**：これ以上の Microsoft 側アップグレードはほぼ不要。個別 Add-on としては：
- Microsoft Sentinel（Azure）
- Microsoft Cloud for Sovereignty
- Defender for Endpoint P2 for Student（児童生徒端末向け）

**B. オペレーション対応**：
- 全機能の**継続的な運用設定・チューニング**が必要（機能があっても未活用では意味がない）
- Secure Score 90% 以上を目標とした継続改善
- Purview Compliance Manager の全アクション遂行
- インシデント対応机上演習の年 2 回以上実施
- Insider Risk のプライバシー影響評価（教職員個人情報を扱うため慎重に）

**C. A5 でも解決しない教育分野固有の課題**：
- 児童生徒への情報モラル教育（カリキュラム対応）
- SNS 公式アカウント運用ガイドライン
- 学校施設の物理管理（サーバ室・GIGA 端末充電保管庫）
- 家庭持ち帰り運用時のリスク管理

---

## 5. 構成選定ガイド

### 5.1 判断フロー

```
Q1. 児童生徒端末と教職員端末を分けて論じるか？
├─ Yes → 児童生徒は①（＋必要に応じて Student 向け Add-on）、教職員は②〜⑤
└─ No → 実務上ほぼありえない（GIGA と校務は分離が原則）

Q2. 教職員側の予算余裕は？
├─ 追加投資ゼロ                          → 構成② （オペレーション対応で凌ぐ）
├─ 中程度（EDR 又はコンプライアンスどちらか）  → 構成③
├─ ネットワーク側で予算確保済み              → 構成④
└─ 最大限投資可能                        → 構成⑤

Q3. 最大の懸念は「標的型攻撃」か「データ管理・開示対応」か？
├─ 標的型攻撃・ランサムウェア    → ③ A5 Security 又は ⑤
├─ データ管理・監査・開示請求    → ③ A5 Compliance 又は ⑤
└─ ネットワーク境界防御          → ④

Q4. オンプレ AD が現存するか？
├─ Yes → Defender for Identity が有効 → ③ A5 Security 又は ⑤
└─ No  → 影響なし

Q5. 校務外部接続系の再構築（クラウド化）を予定しているか？
├─ Yes → SASE の ZTNA が有効 → ④
└─ No  → SASE の価値は Web/DLP に集中
```

### 5.2 教育委員会の規模別 推奨構成

| 規模 | 推奨基本構成 | 補足 |
| --- | --- | --- |
| 政令指定都市・大規模市 | 構成⑤ ＋ Sentinel | フル SIEM/SOAR、独自 CSIRT 保有 |
| 中規模市 | 構成③（A5 Security）＋ 補完運用 | 標的型対策優先、コンプライアンスは首長部局と連携 |
| 小規模市町村 | 構成② ＋ 都道府県教育委員会の共同運用 | 都道府県の共同 SOC/SIEM に加入 |
| 町村（人口 1 万人以下） | 構成② | 都道府県 or 一部事務組合の共同運用に完全依存 |

---

## 6. コスト・実装複雑度比較

### 6.1 相対コスト（教職員 500 名想定、A3 を基準 1.0）

| 構成 | ライセンス相対コスト | 実装工数 | 運用工数 |
| --- | :-: | :-: | :-: |
| ① A1 for Device（GIGA 端末、教員含む場合あり） | ― | 中 | 中（教員が利用しているケースでは高） |
| ② A3 | 1.0 | 中 | 高（不足を運用で補うため） |
| ③ A3 + A5 Security | 1.4〜1.6 | 中 | 中 |
| ③ A3 + A5 Compliance | 1.3〜1.5 | 中 | 中 |
| ④ A3 + SASE | 1.5〜2.5（SASE 単価に依存） | 高（M365 と SASE の統合） | 中〜高 |
| ⑤ A5 | 2.0〜2.5 | 中 | 中 |

**注**：具体的な金額は Microsoft の教育機関向け価格・パートナー割引・調達数量により大きく変動する。上記は Microsoft 教育機関公表価格のオーダー感。

### 6.2 実装フェーズ別 難易度

| フェーズ | ② A3 | ③ A5 Sec 追加 | ③ A5 Comp 追加 | ④ SASE 追加 | ⑤ A5 |
| --- | :-: | :-: | :-: | :-: | :-: |
| ライセンス調達 | 低 | 低 | 低 | 中 | 低 |
| Entra ID 設計変更 | 低 | 中（PIM 設定） | 低 | 中 | 中 |
| Intune ポリシー | 中 | 中 | 中 | 中 | 中 |
| Defender 展開 | 中 | 中（P2 チューニング） | 低 | 中（重複整理） | 中 |
| Purview 展開 | 中 | 低 | 高（Insider Risk 特に慎重） | 低 | 高 |
| SASE 統合 | ― | ― | ― | 高（PoC 必須） | ― |
| 運用体制構築 | 高 | 中 | 中 | 中〜高 | 中 |

---

## 7. 実装チェックリスト（構成別）

各構成に共通する基本チェックは `reports/m365-a1giga-a3-implementation.md` を参照。以下は構成別の**追加チェック**。

### 7.1 構成② A3 単独で施行に間に合わせる場合の最小実装

- [ ] Defender for Endpoint P1 の ASR ルール（15+ 全ルール）を有効化
- [ ] Exchange Online Protection のスパム・マルウェア・添付制限を Microsoft 推奨強度以上に設定
- [ ] 条件付きアクセスで IP 制限・デバイスコンプライアンス連動・レガシー認証ブロックを実装
- [ ] MFA 全員強制、パスワードレス（Authenticator）推奨
- [ ] Audit ログを **Office 365 Management Activity API 経由**で Log Analytics/SIEM に転送し 1 年以上保持（API 制限・遅延を考慮）
- [ ] Purview 手動ラベル 4 段階（重要性分類Ⅰ〜Ⅳ）を全教職員に周知
- [ ] Secure Score 目標 70% 以上を年 1 回見直し
- [ ] 有償訓練の代わりに年 1 回以上の対面研修（人手による疑似メール訓練）

### 7.2 構成③ A5 Security 追加時の追加実装

- [ ] Defender for Endpoint P2 の自動調査・修復レベル設定
- [ ] Defender for Office 365 P2 の Attack Simulation Training を四半期実施
- [ ] Defender for Identity センサーをオンプレ AD DC にデプロイ（該当時）
- [ ] Entra ID P2 PIM で全 Global Admin を期限付き昇格化
- [ ] Identity Protection のリスクポリシー（Sign-in Risk / User Risk）設定
- [ ] Defender XDR 統合ポータルでのインシデント対応フロー整備

### 7.3 構成③ A5 Compliance 追加時の追加実装

- [ ] 自動ラベル付けポリシー（SharePoint/OneDrive/Exchange）
- [ ] Insider Risk Management のポリシー策定と**プライバシー影響評価**
- [ ] Communication Compliance ポリシー（教職員・児童生徒間コミュニケーション監視）は**慎重な導入判断**
- [ ] Audit Premium で監査ログ 1 年保持を設定（10 年保持は「10-Year Audit Log Retention Add-on」を別途購入）
- [ ] eDiscovery Premium のケース管理手順を法務担当と共有
- [ ] Records Management で法定帳簿（指導要録等）の保持ポリシー

### 7.4 構成④ SASE 追加時の追加実装

- [ ] SASE ベンダーの ISMAP 登録・SOC 2 Type II 取得状況の確認
- [ ] SASE ベンダーの**国内 PoP／データセンター**利用の契約明記
- [ ] SSL/TLS 復号のプライバシー影響評価（児童生徒データ扱いのため必須）
- [ ] Microsoft ネイティブ機能との重複整理（Web 保護、CASB Discovery 等）
- [ ] 統合ログ収集基盤（SIEM）の設計
- [ ] SASE エージェント配布 → Intune 経由が原則
- [ ] SASE ベンダーに対する**令和8年通知のサプライチェーン評価**実施

### 7.5 構成⑤ A5 の場合の追加実装

- [ ] Microsoft Sentinel の要否判断（教育機関 A5 の取り込み無料枠を確認）
- [ ] Purview Compliance Manager の全アクションを段階的に遂行
- [ ] Insider Risk / Communication Compliance の**教職員代表・労働組合との事前協議**
- [ ] Secure Score 目標 90% 以上に引き上げ
- [ ] 年 2 回以上のインシデント対応机上演習
- [ ] 児童生徒端末側（A1）の追加補強（Student 向け Add-on 検討）

---

## 参照文書

- 改訂指針：`proposal/revision-proposal.md`
- 前回レポート（A1 GIGA Promo + A3 版）：`reports/m365-a1giga-a3-implementation.md`
- 8 分野対応表：`research/mapping-8measures.md`
- 施行規則第16条の3 逐語：`research/sources/soumu-reiwa8-shorei-80.md`
- 令和8年総務省通知：`research/sources/soumu-tuchi-r8-shorei.md`
- 参考文献：`references.md`

### Microsoft 公式リソース

- Microsoft 365 Education Licensing：https://learn.microsoft.com/ja-jp/microsoft-365/education/
- A5 Security / A5 Compliance Add-on：https://learn.microsoft.com/en-us/microsoft-365/education/guide/4-advanced/security/advanced-security-compliance-a5-addons
- Defender for Endpoint P1／P2 比較：https://learn.microsoft.com/en-us/defender-endpoint/defender-endpoint-plan-1
- Entra ID P1／P2 比較：https://learn.microsoft.com/ja-jp/entra/fundamentals/licensing
- Purview ライセンスガイダンス：https://www.microsoft.com/licensing/guidance/Microsoft-Purview
- ISMAP 対応：https://learn.microsoft.com/ja-jp/compliance/regulatory/offering-ismap
- Service Trust Portal：https://servicetrust.microsoft.com/

---

（本レポートは令和8年7月時点の Microsoft 365 Education ライセンスと施行規則第16条の3 の要求事項に基づく比較分析であり、実装前に最新の Microsoft 公式ドキュメントおよびパートナーの見積で確認すること。SASE ベンダー機能セットは代表的なもので、実際の製品選定時は個別評価が必要。）

---

## 改訂履歴

**2026-08-XX（教員 A1 for Device 利用ケースの rubber-duck ファクトチェック反映）**：
- A1 for Devices に **Faculty SKU / Student SKU の別 SKU** が存在すること、教員利用は Faculty SKU を教員専用端末に割当てる前提であることを §4.1 冒頭に追記
- **Microsoft Defender AV のクラウド保護・自動サンプル送信・ASR ルールは公式には Defender for Endpoint P1/P2 ライセンスが必要**（Microsoft Learn 明記）である旨を反映。「A1 for Device 単独で実施可能」との記述を修正し、MDE P1 Add-on 追加購入推奨、または WDAC を軸とする代替策に変更
- 「A3 ユーザーがサインインすれば A3 機能が有効化」を「A3 のユーザー権利を利用可能。MDE オンボーディング等の別途構成が必要」に修正
- Security Defaults はテナント全体設定で教員のみ対象にできない点を明記、教員のみ対象にする場合は per-user MFA を利用と修正
- Intune 準拠状態と証明書ベースの管理端末識別は同等ではない点を明記
- Teams プライベートチャネルは DLP や誤投稿防止機能ではないこと（メンバー限定アクセス機能に過ぎない）を明記
- **経過措置に関する記述を法令に忠実に修正**：附則第2項は期限を明示していないため「令和10年度以降本格適用」は法令上の期限ではなく本レポート独自の移行目標である旨を明記。新規システム・新規委託は令和9年7月1日から本則適用
- Exchange Online Transport Rule を「メールフロールール」の正式名称に補正
- USB 大容量ストレージ拒否は「Intune Settings Catalog」で実施と補正

**2026-08-XX（教員 A1 for Device 利用ケース追加）**：
- §1.1 表：A1 for Device の説明に「教員が利用しているケースも実在」を明記
- §1.2：教員 A1 利用シナリオの実在と、A3 以上へのアップグレード推奨、および §4.1 の追加サブセクションへの誘導を追加
- §4.1 タイトル変更：「（GIGA 端末／教員が利用しているケースを含む）」
- §4.1 に新規サブセクション「【追加】教員が A1 for Device を利用しているケース向けの対応」を追加。リスク認識、優先度付きアップグレード方針、必須オペレーション（認証・端末保護・情報保護・監視監査・研修・委託）、移行スケジュールを詳述
- §6.1 コスト表：A1 for Device の運用工数注記を「教員が利用しているケースでは高」に修正

**2026-08-XX（rubber-duck ファクトチェック反映）**：
- Audit Premium は 1 年保持、10 年保持は別売の「10-Year Audit Log Retention Add-on」（ユーザー単位）と明記
- 「A5 = A3 + A5 Sec + A5 Comp + Power BI Pro」の等式表現を「主要セキュリティ・コンプライアンス機能に相当」に修正（Teams Phone、Audio Conferencing 等が追加で含まれる）
- A1 for Device 単独では条件付きアクセスは実現不可（要 Entra ID P1）と修正、ネットワーク層制御・SASE 側制御を代替として明示
- 「SPF/DKIM/DMARC で Safe Links を代替」の記述を「送信元偽装抑止に限定、URL 検査は行われず残存リスクあり」に修正
- Defender for Identity の説明を「オンプレ AD DS/AD FS/AD CS 等ハイブリッド ID 脅威検知」に修正（Entra ID Protection と区別）
- Defender Vulnerability Management は「P2 にコア機能を含み、拡張機能は Add-on 別売」に修正
- A1 for Device は「デバイス単位ライセンス、教職員利用も禁止ではないが標準ライセンスとしては機能不足」に修正
- 監査ログ長期保持を「Office 365 Management Activity API 経由での SIEM/Log Analytics 取込」に修正（診断設定直接転送はサポート外）
- ASR ルールは「Audit/Warn モード → 除外設計 → 段階的 Block 移行」に修正（全ルール一括 Block は業務停止リスク）
- 8 分野マトリクスの「◎」評価を精査し、規程・運用で達成する分野（第1・3・4・7号）は「製品機能による支援度」であって法令適合度そのものではない旨の注記を追加。該当分野の評価は「◎」から「○」に引き下げ
- SASE ベンダーの ISMAP 記述を「サービス名・言明範囲・登録番号・有効期限単位で確認」に修正
- Sentinel の A5 データグラントは「対象となる Microsoft 365 データに限定、契約種別条件あり」と明記
