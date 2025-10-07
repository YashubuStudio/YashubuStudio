# スキルシート

## 基本情報
- 肩書：フルスタックエンジニア／自律型システム開発者
- 経験年数：4年
- 勤務形態：完全リモート（成果物納品・非同期進行）
- 開発環境：Windowsメイン（Linux移行中）／Mac非対応
- GitHub：[@YashubuStudio](https://github.com/YashubuStudio)
- 配信中プロジェクト：[MultiIndex (Booth)](https://hisuiyk.booth.pm/items/7214613)

---

## サマリ
独立系エンジニアとして4年間、**AI分類・検索・Webフロント・プラグイン開発**を中心に実用的なシステムを開発。  
バックエンドはGo／PHP／Python、フロントエンドはReact／WebGLを中心に構築し、  
UIからサーバー・データ処理までを**単独で完結できるフルスタック設計力**を持つ。  
クラウド依存を避け、ローカル完結・軽量実行を重視した設計思想。

---

## 技術スキル（L1〜L5）

| 分野 | 技術 | レベル | 備考 |
|------|------|---------|------|
| 言語 | C / Basic / VBA / Python / Java / PHP / Go / GAS | L4 | 設計意図に応じた多言語連携が可能 |
| フロント | HTML / CSS / JavaScript / React / WebGL | L4 | UI構築・3D表示・インタラクション設計に対応 |
| バックエンド | PHP / Go / Python（Flask, FastAPI） / Node.js | L4 | API構築・データ処理・自動化スクリプト |
| DB | SQLite / MySQL | L3 | 軽量・組込型DB中心に利用 |
| CMS | WordPress（プラグイン開発） | L4 | React＋REST API連携プラグインの開発経験 |
| AI関連 | ONNX / NLP / テキスト分類 / 意味抽出 | L5 | Go＋ONNXによる分類エンジン実装経験あり |
| 環境構築 | Windows / Linux（実機構築） | L4 | Docker未使用、自前構築で汎用環境を再現 |

---

## 主な開発・研究プロジェクト

### 🧠 Categorizer-Go（Go＋ONNXによる文章分類エンジン）
- **概要**：Go言語からONNXを直接呼び出し、入力文を意味分類する軽量エンジン。  
  通常の「単語→文」検索ではなく、「文→単語」方向の分類を実現。
- **GitHub**：[Categorizer-Go-](https://github.com/YashubuStudio/Categorizer-Go-)  
- **技術**：Go, ONNXRuntime, Kagome  
- **特徴**：  
  - CPUのみで実行可能な高効率分類器  
  - 軽量実行環境向けに最適化されたGo実装  
  - LLM非依存の意味理解・分類ロジックを構築  
- **成果**：LLMなしで自然文を分類する分別エンジンを完成。

---

### 📂 MultiIndex（ローカル全文検索エンジン）
- **概要**：Go言語による軽量全文検索システム。  
  指定ディレクトリを自動走査し、PDF・HTML・TXT等をインデックス化して検索可能。
- **配信**：[Boothページ](https://hisuiyk.booth.pm/items/7214613)  
- **技術**：Go（Bleve＋Kagome）, SQLite, CLI／Web対応  
- **特徴**：  
  - CPUオンリーで高速動作  
  - フラグメント生成によるスニペット抽出  
  - 再検索機構（Top-N制御）による効率設計  
- **成果**：ローカル完結・軽量構成で動作する検索エンジンを実用化。

---

### 🌐 Vconf_webgl-glTF（WebGLによる3Dモデルビューア）
- **概要**：Three.jsをベースに、GLTFファイルをWeb上でプレビューする3Dビューア。  
  複数視点からの表示や自動キャプチャ機能を実装。
- **GitHub**：[Vconf_webgl-glTF](https://github.com/YashubuStudio/Vconf_webgl-glTF)  
- **技術**：React, Three.js, WebGL  
- **特徴**：  
  - 発表資料提出用の3Dアップローダー・ビューア構成  
  - マルチビュー表示・自動画像生成  
  - 軽量なUI設計でローカル実行にも対応  

---

### 🧰 vconf_editor（React製Webエディタ）
- **概要**：Web上で入力フォーム検証・表示結果を即座に確認できる2カラム構成のUI。  
  発表者番号＋パスコード入力など、シンプルで実用的な構成。
- **GitHub**：[vconf_editor](https://github.com/YashubuStudio/vconf_editor)  
- **技術**：React, TailwindCSS  
- **特徴**：  
  - 入力エリアと結果表示を左右に分離した直感的UI  
  - 検証・整形ツールのベースとして応用可能  

---

### 🔌 wp-react-db-plugin（WordPress＋Reactデータ管理プラグイン）
- **概要**：WordPress上でReactフロントを動作させ、DB管理・入力UIを拡張。  
  PHP＋REST APIを通じて双方向通信を実現。
- **GitHub**：[wp-react-db-plugin](https://github.com/YashubuStudio/wp-react-db-plugin)  
- **技術**：PHP, React, MySQL, REST API  
- **特徴**：  
  - WordPress内部で動作するSPA構成  
  - データ入力・管理のUIをReactで再構築  
  - 既存CMSの拡張に適した構成  

---

### 🌍 Amate（分散検索エンジン構想・開発継続中）
- **概要**：MultiIndexをベースに、分散ノード型検索＋トークン経済圏を目指した研究構想  
- **技術**：Go, Python, PHP(Lumen), Node.js, React  
- **進捗**：分散同期モデルを再設計中  
- **目的**：人・AI双方が利用できる非中央集権検索基盤の確立

---

## 強み
- **設計と実装の両立**：目的に応じて最小構成で動作するシステムを自作  
- **言語横断力**：Go・React・PHPなどを自在に組み合わせた設計が可能  
- **軽量志向**：LLM非搭載でも自然言語処理を行える独自エンジンを構築  
- **実機構築能力**：仮想化せず、Linux実環境での動作検証に強い  

---

## 課題・希望
- チーム開発（CI/CD・コードレビュー）は未経験  
- **完全リモート・非同期進行**のプロジェクトを希望  
- 成果物ベースの受託・共同開発・研究案件を志向  

---

## 対応可能領域
- 軽量AI分類・検索エンジン開発（Go＋ONNX）  
- 3Dモデル・WebGLビューア開発（React＋Three.js）  
- WordPress拡張プラグイン開発（React＋PHP）  
- 自動化ツール・ローカル完結型システムの設計
