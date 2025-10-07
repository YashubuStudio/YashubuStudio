# 🧠 技術スキルシート - YashubuStudio

## 概要
短期Webシステム開発を中心に、設計〜実装・納品まで一貫対応できます。
最短1週間程度の小規模案件から、検索エンジンやAI連携を含む中規模開発まで対応可能です。

**得意分野**
- Webアプリケーション（Go / PHP / React）
- 検索・インデックス構築（Bleve, FAISS）
- AI連携（Ollama, Gemini, GPT系）
- 自動化スクリプト・CLIツール開発

---

## 👤 プロフィール
**氏名（ハンドル）**：Keito（YashubuStudio）  
**職種**：独立系エンジニア／技術研究者  
**活動歴**：4年（個人開発・受託・研究開発）  
**稼働形態**：フルリモート専業（委託・共同研究対応可）  
**拠点**：日本（愛知・豊橋）  
**開発環境**：自作PCを中心に構築（N100等の低消費電力機材でも動作検証可能）

---

## 対応可能な業務
- HP制作
- Webアプリの新規開発・既存システムの改修
- APIサーバー・バックエンド構築（Go / PHP / Node.js）
- 検索・RAG・LLM連携の導入
- データ処理・業務自動化ツールの開発
- 短期（1〜2週間）でのプロトタイプ・PoC開発

## 主な開発実績
- **Amate**：分散型検索エンジン＋トークン連携（Go / React / IPFS）
- **DataAgent**：社内情報共有AIシステム（Python / Lumen / FAISS）
- **MultiIndex**：全文検索エンジン（Go / Kagome / Bleve）

---

## 🧩 サマリ
独立系エンジニアとして、AIを含む多分野技術の**研究・基礎設計・実装**を行っています。  
保有している技術を柔軟に組み合わせ、**軽量・高効率・低コスト**なシステムを設計・構築。  
Go／PHP／React／Pythonなど複数言語を横断し、Web・ローカルアプリ・自動化など幅広く対応可能。  

単なる開発にとどまらず、  
「なぜこの技術を使うべきか」「どう組み合わせれば最も軽く動作するか」  
といった**設計思想・技術検証の領域**を得意としています。  

実用化と再現性を重視し、AIを駆使した開発環境・分類・最適化など、  
痒いところに届く小規模技術の研究開発を継続しています。

---

## 💪 強み（Strengths）

- **環境最適設計力**  
  - N100など低消費電力PCでも常時稼働できる設計を実現。  
  - 仮想化・ローカル両対応可能で、環境に合わせた最適な構成を判断可能。  

- **統合的な構築能力**  
  - フロントエンド・バックエンド・AI処理・CLIを単独で統合可能。  
  - 異言語間の設計統一と効率的データ連携を重視。  

- **設計思考 × 実装力**  
  - 動作するものを最短で作り上げつつ、軽量化・再現性・運用性を両立。  
  - クラウド依存を避けながらも必要な部分では柔軟に採用可能。  

- **吸収と適応の速さ**  
  - 要件・新技術・ライブラリを短期間で理解・検証。  
  - 試作段階から実装・評価までの一連を自走できる。  

- **AI／ローカルLLM環境への深い理解**  
  - Ollama、ONNX、FAISSなどを扱い、軽量環境でAI処理を実装可能。  
  - Go・Python間でモデル推論を統合するハイブリッド構成に精通。  

---

## 💻 技術スキル一覧（熟練度レベル付き）

| 分類 | 技術・ツール | 熟練度 | 備考 |
|------|---------------|--------|------|
| 言語 | **Go**, Python, PHP, JavaScript, React, HTML/CSS, VBA, GAS, C, Basic | L5〜L3 | フルスタック・CLI・Web・ローカルアプリ開発まで幅広く対応 |
| バックエンド | Go（Bleve全文検索, CLI構築）, PHP/Lumen, Python（AI連携, 自動化処理） | L5 | API設計・連携・軽量構築が得意 |
| フロントエンド | React, WebGL, Three.js, HTML5/CSS3 | L4 | UI/UX設計から3D表示・操作まで一貫対応 |
| データ処理 | SQLite, CSV, JSON, MySQL(一部) | L4 | 軽量DB・ローカル分析・統計推定まで対応 |
| AI関連 | ONNX推論, LLM統合（Ollama, GPT, Gemini）, FAISSベクトル検索 | L3 | モデル統合・最適化・推論試作可能 |
| 開発環境 | Windows / Linux / 仮想化(QEMU, WSL2, VirtualBox) | L4 | 実機構築派。クラウドに依存しない開発重視 |
| 制御・電子工作 | Arduino, シリアル通信, ローカルネットワーク制御 | L3 | 電流計測・センサー処理等の小規模実験系設計 |
| その他 | Git, Node.js, Firebase通知, AWS(基礎) | L3 | 継続開発・配布・通知などの自動化経験あり |

> **Lレベル目安**  
> L5：設計・実装を単独完結可能（プロジェクトリード相当）  
> L4：商用レベルでの安定構築・改善が可能  
> L3：日常運用・改修・調整に即応可能  
> L2：短期習得・応用可能  
> L1：基礎理解・研究段階

---

## 🚀 代表プロジェクト

### 🔹 [MultiIndex](https://hisuiyk.booth.pm/items/7214613)
Go製の軽量全文検索エンジン。  
特定ディレクトリを自動インデックス化し、ローカル環境で高速検索を実現。  
クラウドを使わずCPUのみで動作可能。  
キーワード＋スコアによるハイブリッド検索機能を搭載。  

### 🔹 [Categorizer-Go-](https://github.com/YashubuStudio/Categorizer-Go-)
GoからONNXモデルを呼び出し、テキスト分類を行う軽量AI分類エンジン。  
LLM統合を見据えた構造で、推論サンプル・チューニング実験に適用可能。  

### 🔹 [Vconf_webgl-glTF](https://github.com/YashubuStudio/Vconf_webgl-glTF)
React＋Three.js＋WebGLによるGLTF/ZIPファイルビューワー。  
マルチビュー・自動キャプチャ・アップロード機能を搭載し、学会発表・共有用途にも対応。  

### 🔹 [vconf_editor](https://github.com/YashubuStudio/vconf_editor)
設定ファイル編集・保存をWebUIで行える軽量ツール。  
Electronライクなローカルアプリ化も想定。  

### 🔹 [wp-react-db-plugin](https://github.com/YashubuStudio/wp-react-db-plugin)
WordPress × ReactによるDB連携プラグイン。  
軽量なSPA構成を既存環境に無理なく統合可能。  

### 🔹 バーチャル学会Web班（システム開発部門）
学会提出・審査システムの開発およびUI/UX調整を担当。  
セキュアかつ簡易な運用を重視した設計を実現。  

---

## ⚙️ 開発環境
- **OS**：Windows 11 / Ubuntu 24.04 LTS  
- **仮想環境**：QEMU / VirtualBox / WSL2（N100クラスで軽量運用）  
- **エディタ**：VS Code, nano  
- **主要ツール**：Git / Node.js / Go CLI / Python / React / WebGL  
- **AI実験環境**：Ollama / ONNX / local LLMサーバー / FAISS  

---

## 🧠 開発スタイル・思想
- **目的駆動・軽量設計**：必要な技術を最短で吸収し、最適な形で活用  
- **再現性重視**：研究〜実装間のギャップを最小化  
- **シンプル構造主義**：依存を減らし、ローカルでも動作可能な仕組みを好む  
- **一人完結型**：設計・実装・UI構築・AI実験まで一気通貫で対応  
- **可搬性設計**：仮想化・クラウド・実機いずれでも動作する構成を意識  

---

## 💼 受託・公開実績

### 🏢 クライアント案件（受注開発）
- [mfc.ne.jp](https://mfc.ne.jp)  
  企業向けWebサイト構築・運用を担当。  
  静的生成＋最適化による軽量化を重視。  
  サーバー環境構築〜デザイン・実装まで一貫して対応。  

### ⚡ 技術試作・電子制御
- Arduino＋ローカルネットを用いた電流計測システム  
  - 回路設計・通信・コードを自作し、安価・独立動作を実現。  
  - データ収集のローカル自動化を実装。  

---

### 📁 ポートフォリオ・記録
- [YashubuStudio Portfolio / record.html](https://portfolio.yashubustudioetc.com/record/record.html)  
  個人・法人案件を含む受注・開発記録を掲載。  
  Web／AI／制御系問わず、要件定義から納品まで対応。  

---

## 📄 稼働条件
- **勤務形態**：フルリモートのみ  
- **対応時間**：柔軟（納期優先・タスク駆動）  
- **得意分野**：軽量アプリ化・AI統合・技術検証・Webシステム設計  
- **苦手分野**：定期MTG・常駐業務中心の体制  
- **対応範囲**：研究協力／システム設計支援／試作段階の技術実装など  

---

## 🛰️ GitHub / 配信リンク
- **GitHub**：[https://github.com/YashubuStudio](https://github.com/YashubuStudio)  
- **Booth配信**：[https://hisuiyk.booth.pm/items/7214613](https://hisuiyk.booth.pm/items/7214613)  
- **Portfolio**：[https://portfolio.yashubustudioetc.com](https://portfolio.yashubustudioetc.com)

---

> 📘 詳細・経歴更新版：[skillsheet.md](https://github.com/YashubuStudio/YashubuStudio/blob/main/skillsheet.md)
