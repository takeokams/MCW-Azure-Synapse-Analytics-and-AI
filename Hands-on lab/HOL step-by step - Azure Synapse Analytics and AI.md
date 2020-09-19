![マイクロソフト クラウド ワークショップ](https://github.com/Microsoft/MCW-Template-Cloud-Workshop/raw/master/Media/ms-cloud-workshop.png "マイクロソフト クラウド ワークショップ")

<div class="MCWHeader1">
Azure Synapse Analytics と AI
</div>
<div class="MCWHeader2">
段階的ハンズオン ラボ
</div>
<div class="MCWHeader3">
2020 年 7 月
</div>
このドキュメントに記載されている情報 (URL 等のインターネット Web サイトに関する情報を含む) は、将来予告なしに変更されることがあります。特に断りがない限り、ここで使用している会社、組織、製品、ドメイン名、電子メール アドレス、ロゴ、人物、場所、イベントの例は、架空のものであり、実在する会社、組織、製品、ドメイン名、電子メール アドレス、ロゴ、人物、場所、イベントなどとは一切関係ありません。お客様ご自身の責任において、適用されるすべての著作権関連法規に従ったご使用を願います。このドキュメントのいかなる部分も、米国 Microsoft Corporation の書面による許諾を受けることなく、その目的を問わず、どのような形態であっても、複製または譲渡することは禁じられています。ここでいう形態とは、複写や記録など、電子的な、または物理的なすべての手段を含みます。ただしこれは、著作権法上のお客様の権利を制限するものではありません。

マイクロソフトは、このドキュメントに記載されている内容に関し、特許、特許申請、商標、著作権、またはその他の無体財産権を有する場合があります。別途マイクロソフトのライセンス契約上に明示の規定のない限り、このドキュメントはこれらの特許、商標、著作権、またはその他の無体財産権に関する権利をお客様に許諾するものではありません。

製造元や製品の名前、URL は情報の提供のみを目的としており、マイクロソフトは、これらの製造元、またはマイクロソフトの技術での製品の使用について、明示的、黙示的、または法的にいかなる表示または保証も行いません。製造元または製品の使用は、マイクロソフトによるその製造元または製品の推奨を意味するものではありません。サード パーティのサイトへのリンクが提供されている場合があります。このようなサイトはマイクロソフトの管理下にはなく、マイクロソフトは、リンクされたサイトの内容またはリンクされたサイトに含まれるリンク、あるいはこのようなサイトの変更または更新について責任を負いません。マイクロソフトは、リンクされたサイトから受信された Web キャストまたは他のいかなる形態の転送にも責任を負いません。マイクロソフトは、これらのリンクを便宜のみを目的として提供しており、いかなるリンクの使用も、マイクロソフトによるサイトまたはそこに含まれる製品の推奨を意味するものではありません。

© 2020 Microsoft Corporation.All rights reserved.

Microsoft および <https://www.microsoft.com/en-us/legal/intellectualproperty/Trademarks/Usage/General.aspx> に記載されている商標は、Microsoft グループの商標です。その他すべての商標は、該当する各社が所有しています。

**目次**

<!-- TOC -->

- [Azure Synapse Analytics と AI 段階的ハンズオン ラボ](#azure-synapse-analytics-と-ai-段階的ハンズオン-ラボ)
    - [要約と学習目的](#要約と学習目的)
    - [概要](#概要)
    - [ソリューションのアーキテクチャ](#ソリューションのアーキテクチャ)
    - [必要条件](#必要条件)
    - [ハンズオン ラボの前に](#ハンズオン-ラボの前に)
    - [このラボ全体で使用するリソースの名前付け規則](#このラボ全体で使用するリソースの名前付け規則)
    - [演習 1: Azure Synapse Analytics ワークスペースへのアクセス](#演習-1-azure-synapse-analytics-ワークスペースへのアクセス)
        - [タスク 1: Synapse Studio の起動](#タスク-1-synapse-studio-の起動)
    - [演習 2: SQL プールでのサポート用テーブルの作成とデータの読み込み](#演習-2-sql-プールでのサポート用テーブルの作成とデータの読み込み)
        - [タスク 1: 販売テーブルの作成](#タスク-1-販売テーブルの作成)
        - [タスク 2: 販売テーブルへのデータの読み込み](#タスク-2-販売テーブルへのデータの読み込み)
        - [タスク 3: 顧客情報テーブルの作成](#タスク-3-顧客情報テーブルの作成)
        - [タスク 4: 顧客情報テーブルへのデータの読み込み](#タスク-4-顧客情報テーブルへのデータの読み込み)
        - [タスク 5: キャンペーン分析テーブルの作成](#タスク-5-キャンペーン分析テーブルの作成)
        - [タスク 6: キャンペーン分析テーブルへのデータの読み込み](#タスク-6-キャンペーン分析テーブルへのデータの読み込み)
        - [タスク 7: 製品テーブルへのデータの読み込み](#タスク-7-製品テーブルへのデータの読み込み)
    - [演習 3: 生 Parquet の調査](#演習-3-生-parquet-の調査)
        - [タスク 1: Synapse SQL サーバーレスによる販売 Parquet データに対するクエリの実行](#タスク-1-synapse-sql-サーバーレスによる販売-parquet-データに対するクエリの実行)
        - [タスク 2: Azure Synapse Spark による販売 Parquet データに対するクエリの実行](#タスク-2-azure-synapse-spark-による販売-parquet-データに対するクエリの実行)
    - [演習 4: Azure Synapse SQL サーバーレスによるテキストベースの生データの調査](#演習-4-azure-synapse-sql-サーバーレスによるテキストベースの生データの調査)
        - [タスク 1: CSV データに対するクエリの実行](#タスク-1-csv-データに対するクエリの実行)
        - [タスク 2: JSON データに対するクエリの実行](#タスク-2-json-データに対するクエリの実行)
    - [演習 5: Synapse パイプラインと Cognitive Search](#演習-5-synapse-パイプラインと-cognitive-search)
        - [タスク 1: 請求書のストレージ コンテナーの作成](#タスク-1-請求書のストレージ-コンテナーの作成)
        - [タスク 2: Azure Forms Recognizer モデルの作成およびトレーニングと Cognitive Search のセットアップ](#タスク-2-azure-forms-recognizer-モデルの作成およびトレーニングと-cognitive-search-のセットアップ)
        - [タスク 3: Form Recognizer でのスキルセットの構成](#タスク-3-form-recognizer-でのスキルセットの構成)
        - [タスク 4: Synapse パイプラインの作成](#タスク-4-synapse-パイプラインの作成)
    - [演習 6: セキュリティ](#演習-6-セキュリティ)
        - [タスク 1: 列レベルのセキュリティ](#タスク-1-列レベルのセキュリティ)
        - [タスク 2: 行レベルのセキュリティ](#タスク-2-行レベルのセキュリティ)
        - [タスク 3: 動的データ マスク](#タスク-3-動的データ-マスク)
    - [演習 7: 機械学習](#演習-7-機械学習)
        - [タスク 1: モデルのトレーニング、利用、および展開](#タスク-1-モデルのトレーニング利用および展開)
    - [演習 8: 監視](#演習-8-監視)
        - [タスク 1: ワークロードの重要度](#タスク-1-ワークロードの重要度)
        - [タスク 2: ワークロードの分離](#タスク-2-ワークロードの分離)
        - [タスク 3: 動的管理ビューによる監視](#タスク-3-動的管理ビューによる監視)
        - [タスク 4: \[Monitor\] ハブによるオーケストレーションの監視](#タスク-4-\monitor\-ハブによるオーケストレーションの監視)
        - [タスク 5: \[Monitor\] ハブによる SQL 要求の監視](#タスク-5-\monitor\-ハブによる-sql-要求の監視)
    - [ハンズオン ラボの後に](#ハンズオン-ラボの後に)
        - [タスク 1: リソース グループの削除](#タスク-1-リソース-グループの削除)

<!-- /TOC -->
# Azure Synapse Analytics と AI 段階的ハンズオン ラボ

## 要約と学習目的

このハンズオン ラボでは、Azure Synapse Analytics を使用する機械学習ソリューションによりエンドツーエンドのデータ分析を構築します。この情報は、小売シナリオのコンテキストで提示されます。ここで多用する Azure Synapse Studio は、取り込み、変換、クエリ、および視覚化から最も一般的なデータ操作を使いやすく統合するツールです。

## 概要

このラボでは、Azure Synapse Analytics のさまざまな機能について説明します。Azure Synapse Analytics Studio は、全チーム メンバーが共同で使用できる単独のツールです。Synapse Studio は、データの取り込み、クリーニング、および生ファイルの変換からノートブックを使用した機械学習モデルのトレーニング、登録、および使用まで、このラボ全体で使用する唯一のツールです。ラボでは、データ関連のワークロードを監視して優先順位を付けるハンズオンエクスペリエンスも提供します。

## ソリューションのアーキテクチャ

![アーキテクチャ図については、次の段落で説明します。](media/archdiagram.png "アーキテクチャ図")

このラボでは、さまざまな種類の生データ ファイルを取り込むコールド データ シナリオについて説明します。これらのファイルはあらゆる場所に存在する可能性があります。このラボで使用するファイルの種類は、CSV、Parquet、および JSON です。このデータは、パイプライン経由で Synapse Analytics に取り込まれます。その後は、データ フロー、Synapse Spark、Synapse SQL (プロビジョニング済みとサーバーレスの両方) などのさまざまなツールを使用して、データを変換および強化できます。処理後のデータには、Synapse SQL ツールを使用してクエリを実行できます。Azure Synapse Studio は、ノートブックを作成してさらにデータの処理、データセットの作成、および機械学習モデルのトレーニングと作成を行う機能も備えています。その後、これらのモデルは、ストレージ アカウントや、SQL テーブルにも保存できます。保存したモデルはさらに、T-SQL などのさまざまな方法で使用できます。ADLS Gen 2 Data Lake は、Azure Synapse Analytics のあらゆる側面を支える基盤コンポーネントです。

## 必要条件

1. Microsoft Azure のサブスクリプション

2. Azure Synapse ワークスペース/Studio

## ハンズオン ラボの前に

ラボの演習に進む前に、「ハンズオン ラボの前に」設定ガイドを参照してください。

## このラボ全体で使用するリソースの名前付け規則

このラボの残りの部分では、さまざまな ASA (Azure Synapse Analytics) 関連のリソースに以下の用語を使用します (必ず各自の環境の実際の名前と値に置き換えてください)。

| Azure Synapse Analytics リソース| 参照名
|----------|----------
| Azure サブスクリプション| `WorkspaceSubscription`
| Azure リージョン| `WorkspaceRegion`
| ワークスペース リソース グループ| `WorkspaceResourceGroup`
| ワークスペース/ワークスペース名| `asaworkspace{suffix}`
| プライマリ ストレージ アカウント| `asadatalake{suffix}`
| 既定ファイル システム コンテナー| `DefaultFileSystem`
| SQL プール| `SqlPool01`
| SQL サーバーレス エンドポイント| `SqlServerless01`
| Azure Key Vault| `asakeyvault{suffix}`

## 演習 1: Azure Synapse Analytics ワークスペースへのアクセス

**所要時間**: 5 分

このラボでは、すべての演習でワークスペース Synapse Studio ユーザー インターフェイスを利用します。この演習では、Synapse Studio を起動するステップの概要を示します。別途指定されない限り、メニュー操作を含むすべての手順は Synapse Studio で実行します。

### タスク 1: Synapse Studio の起動

1. [Azure Portal](https://portal.azure.com) にログインします。

2. 左側のメニューを展開して、**\[Resource groups\]** 項目を選択します。
   
   ![Azure Portal の左側メニューが展開され、\[Resource groups\] 項目が強調表示されています。](media/azureportal_leftmenu_resourcegroups.png "Azure Portal の [Resource Groups] メニュー項目")

3. リソース グループのリストから `WorkspaceResourceGroup` を選択します。

4. リソースのリストから **\[Synapse Workspace\]** リソースの `asaworkspace{suffix}` を選択します。
   
   ![リソース リストで \[Synapse Workspace\] 項目が選択されています。](media/resourcelist_synapseworkspace.png "リソース グループのリスト")

5. \[Synapse Workspace\] ページの **\[Overview\]** タブで、上部のツールバーから **\[Launch Synapse Studio\]** 項目を選択します。代わりに \[Workspace web URL\] リンクを選択することもできます。
   
   ![\[Synapse workspace\] リソース画面の \[Overview\] ペインが表示され、上部のツールバーの \[Launch Synapse Studio\] が強調表示されています。\[Workspace web URL\] の値も強調表示されています。](media/workspaceresource_launchsynapsestudio.png "Synapse Studio の起動")

## 演習 2: SQL プールでのサポート用テーブルの作成とデータの読み込み

**所要時間**: 120 分

有意義なデータのクエリを実行する最初のステップは、データを格納するテーブルを作成することです。ここでは、SaleSmall、CustomerInfo、CampaignAnalytics、および Sales の 4 つのテーブルを作成します。Azure Synapse Analytics でテーブルを設計する場合、各テーブルのデータの予想量および各テーブルの使用方法を考慮する必要があります。テーブルを設計する際は以下のガイダンスを利用して、ベスト エクスペリエンスと最大のパフォーマンスを確保します。

テーブル設計におけるパフォーマンスの考慮事項

| テーブルのインデックス作成方法| 推奨される用途
|----------|----------
| クラスター化列ストア| 1 億行を超えるテーブルにお勧めします。データ圧縮および全体的なクエリ パフォーマンスが最も優れています。
| ヒープ テーブル| 1 億行未満の小規模なテーブル。通常は変換前のステージング テーブルとして使用されます。
| クラスター化インデックス| クエリ実行結果として 1 行のみを返す大規模な (1 億行を超える) ルックアップ テーブル。
| クラスター化インデックス + 非クラスター化セカンダリ インデックス| クエリ実行結果として 1 つ (または非常に少ない数) のレコードを返す大規模な (1 億行を超える) テーブル。

| テーブル分散/パーティション タイプ| 推奨される用途
|----------|----------
| ハッシュ分散| 挿入/更新/削除の各操作の頻度が低い 2 GB を超えるテーブル。スター スキーマの大規模なファクト テーブルに適しています。
| ラウンド ロビンによる分散| 既定の分散。データまたは使用方法に関する情報が少ない場合に使用します。この分散はステージング テーブルに使用します。
| レプリケート テーブル| サイズが 1.5 GB 未満の小規模なルックアップ テーブル。

### タスク 1: 販売テーブルの作成

Wide World Importers は、過去 5 年間に 30 億行を超える販売データを収集しています。この量のデータで消費するストレージは 2 GB を超えます。ラボで使用するのはこのデータの一部のみですが、設計するテーブルは運用環境を想定します。この演習の説明で大まかに示したガイダンスを使用して、**クラスター化列ストア** テーブルと、ほとんどのクエリで使用する **CustomerId** フィールドに基づく **ハッシュ** テーブル分散が必要なことを確認できます。さらにパフォーマンスを向上するために、テーブルをトランザクション日でパーティション分割して、日付または日付演算を含むクエリが確実に、良好な時間で結果を返せるようにします。

1. 左側のメニューを展開して、**\[Develop\]** 項目を選択します。**\[Develop\]** ブレードで **\[+\]** を展開して、**\[SQL script\]** 項目を選択します。
   
   ![左側メニューが展開され、\[Develop\] 項目が選択されています。\[Develop\] ブレードで \[+\] が展開され、\[SQL script\] 項目が強調表示されています。](media/develop_newsqlscript_menu.png "[Develop] ハブ")

2. クエリ タブのツールバー メニューで、SQL プールの `SQLPool01` に接続していることを確認します。
   
   ![クエリ タブのツールバー メニューが表示され、\[Connect to\] が SQL プールに設定されています。](media/querytoolbar_connecttosqlpool.png "SQL プールへの接続")

3. 以下のクエリをコピーしてクエリ ウィンドウに貼り付けて、顧客情報テーブルを作成します。クエリ タブのツールバーで **\[Run\]** を選択します。
   
   ```sql
     CREATE TABLE [wwi_mcw].[SaleSmall]
     (
       [TransactionId] [uniqueidentifier]  NOT NULL,
       [CustomerId] [int]  NOT NULL,
       [ProductId] [smallint]  NOT NULL,
       [Quantity] [tinyint]  NOT NULL,
       [Price] [decimal](9,2)  NOT NULL,
       [TotalAmount] [decimal](9,2)  NOT NULL,
       [TransactionDateId] [int]  NOT NULL,
       [ProfitAmount] [decimal](9,2)  NOT NULL,
       [Hour] [tinyint]  NOT NULL,
       [Minute] [tinyint]  NOT NULL,
       [StoreId] [smallint]  NOT NULL
     )
     WITH
     (
       DISTRIBUTION = HASH ( [CustomerId] ),
       CLUSTERED COLUMNSTORE INDEX,
       PARTITION
       (
         [TransactionDateId] RANGE RIGHT FOR VALUES (
           20180101, 20180201, 20180301, 20180401, 20180501, 20180601, 20180701, 20180801, 20180901, 20181001, 20181101, 20181201,
           20190101, 20190201, 20190301, 20190401, 20190501, 20190601, 20190701, 20190801, 20190901, 20191001, 20191101, 20191201)
       )
     );
   ```

4. このクエリは保存しないので、上部のツールバーから **\[Discard all\]** を選択します。確認を求められたら **\[Discard changes\]** を選択します。
   
   ![上部のツールバー メニューが表示され、\[Discard all\] が強調表示されています。](media/toptoolbar_discardall.png "すべての変更の破棄")

### タスク 2: 販売テーブルへのデータの読み込み

販売テーブルに読み込むために取得するデータは、現在はデータ レイク (Azure Data Lake Storage Gen 2) の **asadatalake{SUFFIX}** に一連の Parquet ファイルとして保存されています。このストレージ アカウントは、環境をプロビジョニングした際に、Azure Synapse Analytics で、リンクされたサービスとしてすでに追加されています。Azure Synapse Analytics では、リンクされたサービスは接続文字列と同義です。Azure Synapse Analytics のリンクされたサービスは、Azure Storage Accounts、Amazon S3 など、100 種類近い外部サービスに接続する機能を提供します。

1. 左側メニューから **\[Manage\]** を選択し、ブレード メニューから **\[Linked services\]** を選択することによって、**asadatalake{SUFFIX}** というリンクされたサービスが存在することを確認します。リンクされたサービスを条件 **「asadatalake」** でフィルターして、**asadatalake{SUFFIX}** 項目を見つけます。この項目を詳細に調査すると、それがストレージ アカウント キーを使用してストレージ アカウントに接続していることがわかります。
   
   ![左側メニューで \[Manage\] 項目が選択されています。ブレードで \[Linked services\] メニュー項目が選択されています。\[Linked services\] 画面の検索ボックスに条件「asadatalake{SUFFIX}」が入力され、フィルター済み結果リストで \[asadatalake{SUFFIX} Azure Blob Storage\] 項目が選択されています。](media/manage_linkedservices_solliancepublicdata.png "リンクされたサービスの検索")

2. 各日の販売データは、既知の名前付け規則に従ってストレージに配置されている個別の Parquet ファイルに保存されています。このラボでは、2018 年と 2019 年のデータだけを販売テーブルに読み込むことを考えています。**\[Data\]** タブを選択して、**\[Data\]** ペインで **\[Linked\]** タブを選択して、`asadatalake{SUFFIX}` ストレージ アカウントを展開することによって、データの構造を調査します。
   
   > **注**: 日次販売データの現在のフォルダー構造は、/wwi-02/sale-small/Year=`YYYY`/Quarter=`Q#`/Month=`M`/Day=`YYYYMMDD` となっています。ここで、`YYYY` は 4 桁の年 (例: 2019)、`Q#` は四半期 (例: Q1)、`M` は月を表す数値 (例: 1 月の場合は 1)、`YYYYMMDD` は数値の日付形式表現 (例: 2019 年 5 月 16 日の場合は `20190516`) をそれぞれ表しています。個別の Parquet ファイルは、日毎のフォルダーに、**sale-small-YYYYMMDD-snappy.parquet** (`YYYYMMDD` は数値の日付表現で置換) という名前で保存されています。
   
   ```text
   Sample path to the parquet folder for January 1, 2019:
   /wwi-02/sale-small/Year=2019/Quarter=Q1/Month=1/Day=20190101/sale-small-20190101-snappy.parquet
   ```

3. 左側メニューから **\[Data\]** を選択し、\[Data\] ブレードで **\[+\]** を展開して **\[Dataset\]** を選択することによって、新しいデータセットを作成します。作成するのは、データ レイクの販売データのルート フォルダーを参照するデータセットです。

4. **\[New dataset\]** ブレードで **\[All\]** タブが選択されている状態で、**\[Azure Data Lake Storage Gen2\]** 項目を選択します。**\[Continue\]** を選択します。
   
   ![\[New dataset\] ブレードで \[All\] タブが選択され、リストで \[Azure Data Lake Storage Gen2\] 項目が選択されています。](media/new_dataset_type_selection.png "新しいデータセットの定義")

5. **\[Select format\]** 画面で **\[Parquet\]** 項目を選択します。**\[Continue\]** を選択します。
   
   ![\[Select format\] 画面で \[Parquet\] 項目が強調表示されています。](media/dataset_format_parquet.png "Parquet の選択")

6. **\[Set properties\]** ブレードでフォームに以下の情報を入力して、**\[OK\]** を選択します。
   
   | フィールド| 値
   |----------|----------
   | Name|  **「asamcw\_sales\_parquet」** と入力
   | Linked service| **asadatalake{SUFFIX}**
   | File path - コンテナー|  **「wwi-02」** と入力
   | File path - フォルダー| **「sale-small」** と入力
   | Import schema| **From connection/store**

   ![\[Set properties\] ブレードが表示され、フィールドに前述の表の値が入力されています。](media/dataset_salesparquet_propertiesform.png "[Dataset] フォーム")

7. 次に、データの保存先データセットを定義する必要があります。ここでは、販売データを SQL プールに保存します。**\[Data\]** ブレードで **\[+\]** を展開して **\[Dataset\]** を選択することによって、新しいデータセットを作成します。

8. **\[New dataset\]** ブレードで **\[Azure\]** タブが選択されている状態で、検索条件として **「synapse」**と入力し、**\[Azure Synapse Analytics (formerly SQL DW)\]** 項目を選択します。**\[Continue\]** を選択します。

9. **\[Set properties\]** ブレードでフィールドに以下の値を設定して、**\[OK\]** を選択します。
   
   | フィールド| 値
   |----------|----------
   | Name| **「asamcw\_sale\_asa」** と入力
   | Linked service| **SQLPool01**
   | Table name| **wwi\_mcw.SaleSmall**
   | Import schema| **\[From connection/store\]**

   ![\[Set properties\] ブレードに前述の表で指定されている値が入力されています。](media/dataset_saleasaform.png "[Dataset] フォーム")

10. 上部のツールバーで **\[Publish all\]** を選択して、新しいデータセット定義を公開します。確認を求められたら **\[Publish\]** を選択して、変更をワークスペースに展開します。
    
    ![上部のツールバーが表示され、\[Publish all\] が強調表示されています。](media/publishall_toolbarmenu.png "変更の発行")

11. 複数の販売年フォルダー (Year=2018 および Year=2019) をフィルターして、2018 年と 2019 年の販売データだけをコピーしたいので、ソース データセットから取得する特定のデータを定義するデータ フローを作成する必要があります。新しいデータ フローを作成するには、まず左側メニューから **\[Develop\]** を選択し、**\[Develop\]** ブレードで **\[+\]** を展開して **\[Data flow\]** を選択します。
    
    ![左側メニューから \[Develop\] 項目が選択されています。\[Develop\] ブレードで \[+\] が展開され、\[Data flow\] 項目が強調表示されています。](media/develop_newdataflow_menu.png "データ フローの作成")

12. 作業ウィンドウの **\[General\]** タブで、**\[Name\]** フィールドに **「ASAMCW\_Exercise\_2\_2018\_and\_2019\_Sales」** と入力して、データ フローに名前を付けます。
    
    ![\[General\] タブが表示され、データ フローの名前として「ASAMCW\_Exercise\_2\_2018\_and\_2019\_Sales」と入力されています。](media/dataflow_generaltab_name.png "データ フローの命名")

13. データ フロー デザイナー ウィンドウで **\[Add Source\]** ボックスを選択します。
    
    ![データ フロー デザイナー ウィンドウで \[Add source\] ボックスが強調表示されています。](media/dataflow_addsourcebox.png "データ フロー ソースの追加")

14. デザイナーで追加したソースが選択されている状態で、下方のペインで **\[Source settings\]** タブを選択し、フィールドに以下の値を設定します。
    
    | フィールド| 値
    |----------|----------
    | Output stream name| 「**salesdata**」と入力
    | Source type| **Dataset**
    | Dataset| **asamcw\_sales\_parquet**

    ![\[Source settings\] タブが選択され、\[Output stream name\] に \[salesdata\] が設定されているのと、\[Dataset\] で \[asamcw\_sales\_parquet\] が選択されているのが表示されています。](media/dataflow_source_sourcesettings.png "ソースの定義")

15. **\[Source options\]** タブを選択して、**\[Wildcard paths\]** に以下の値を追加します。これにより、確実に販売年が 2018 年と 2019 年の Parquet ファイルのデータだけを取得できます。
    
    1. sale-small/Year=2018/\*/\*/\*/\*
    
    2. sale-small/Year=2019/\*/\*/\*/\*
    
    ![\[Source options\] タブが選択され、上記のワイルドカード パスが強調表示されています。](media/dataflow_source_sourceoptions.png "ソースでのワイルドカード パスの設定")

16. **\[salesdata\]** ソースの右下の **\[+\]** を展開して、メニューの **\[Destination\]** セクションにある **\[Sink\]** 項目を選択します。
    
    ![データ フロー デザイナーのソース要素の右下にある \[+\] ボタンが強調表示されています。](media/dataflow_source_additem.png "別のデータ フロー アクティビティの追加")

17. デザイナーで新しく追加した **\[Sink\]** 要素を選択し、下方のペインで **\[Sink\]** タブが選択されている状態で以下のようにフォームに値を入力します。
    
    | フィールド| 値
    |----------|----------
    | Output stream name| **「sale」** と入力
    | Incoming stream| **salesdata**
    | Sink type| **データセット**
    | Dataset| **asamcw\_sale\_asa**

    ![\[Sink\] タブが表示され、フォームに前述の表の値が入力されています。](media/dataflow_sink_sinktab.png "データ フロー シンクの定義")

18. **\[Mapping\]** タブを選択して、**\[Auto mapping\]** 設定をオフの位置に切り替えます。以下の入力列を選択する必要があります。
    
    | 入力列| 出力列
    |----------|----------
    | Quantity| Quantity
    | TransactionDate| TransactionDateId
    | Hour| Hour
    | Minute| Minute

    ![\[Mapping\] タブが選択され、\[Auto mapping\] トグルがオフの位置に設定されています。\[+ Add mapping\] が、前述の表で指定されているマッピング エントリとともに強調表示されています。](media/dataflow_sink_mapping.png "列のマッピング")

19. 上部のツールバーで **\[Publish all\]** を選択して、新しいデータセット定義を公開します。確認を求められたら **\[Publish\]** を選択して、新しいデータ フローをワークスペースに展開します。
    
    ![上部のツールバーが表示され、\[Publish all\] が強調表示されています。](media/publishall_toolbarmenu.png "変更の公開")

20. これで、このデータ フローをパイプラインでアクティビティとして使用できるようになりました。左側メニューから **\[Orchestrate\]** を選択し、**\[Orchestrate\]** ブレードで **\[+\]** を展開して **\[Pipeline\]** を選択することによって、新しいパイプラインを作成します。

21. **\[Properties\]** ブレードで、パイプラインの名前として **「ASAMCW - Exercise 2 - Copy Sale Data」** と入力します。

22. **\[Activities\]** メニューで **\[Move \& transform\]** セクションを展開して、**\[Data flow\]** のインスタンスをパイプラインのデザイン サーフェイスにドラッグします。
    
    ![パイプラインの \[Activities\] メニューが表示され、\[Move and transform\] セクションが展開されています。ドラッグ操作を示す矢印によって、\[Data flow\] アクティビティをパイプラインのデザイン サーフェイスに追加する操作が示されています。](media/pipeline_sales_dataflowactivitymenu.png "データ フロー アクティビティのドラッグ アンド ドロップ")

23. **\[Adding data flow\]** ブレードで、**\[Use existing data flow\]** が選択されていることを確認します。選択リストから **\[ASAMCW\_Exercise\_2\_2018\_and\_2019\_Sales\]** を選択して **\[OK\]** を選択します。
    
    ![\[Adding data flow\] ブレードが表示され、適切な値が入力されています。](media/pipeline_dataflowactivity_addingblade.png "データ フロー アクティビティの構成")

24. **\[Settings\]** タブを選択して、フォームのフィールドに以下の値を設定します。
    
    | フィールド| 値
    |----------|----------
    | Data flow| **ASAMCW\_Exercise\_2\_2018\_and\_2019\_Sales**
    | Staging linked service| `asadatalake{SUFFIX}`
    | Staging storage folder - コンテナー| **「staging」** と入力
    | Staging storage folder - フォルダー| **「mcwsales」** と入力

    ![データ フロー アクティビティの \[Settings\] タブが表示され、前述の表で指定されているフィールドが強調表示されています。](media/pipeline_sales_dataflowsettings.png "データ フロー アクティビティの設定")

25. 上部のツールバーで **\[Publish all\]** を選択して、新しいデータセット定義を公開します。確認を求められたら **\[Publish\]** を選択して、変更をコミットします。
    
    ![上部のツールバーが表示され、\[Publish all\] が強調表示されています。](media/publishall_toolbarmenu.png "変更の公開")

26. 公開されたら、パイプライン デザイナーのツールバーで **\[Add trigger\]** 項目を展開して、**\[Trigger now\]** を選択します。**\[Pipeline run\]** ブレードで **\[OK\]** を選択して、最後に公開した構成で先に進みます。パイプラインが動作していることおよびパイプラインの完了時を示すトースト通知ウィンドウが表示されます。

27. \[Orchestrate\] ブレードで **\[ASAMCW - Exercise 2 - Copy Sale Data\]** パイプラインを特定して、パイプラインの実行のステータスを表示します。アクション メニューを展開して、**\[Monitor\]** 項目を選択します。
    
    ![\[Orchestrate\] ブレードで、\[ASAMCW - Exercise 2 - Copy Sale Data\] パイプラインのアクション メニューが表示され、\[Monitor\] 項目が選択されています。](media/orchestrate_pipeline_monitor_copysaledata.png "パイプラインの監視")

28. **\[Pipeline runs\]** テーブルで、作成したパイプラインの実行が進行中と表示されます。このパイプライン操作は、完了するのに約 45 分かかります。最新の進行状況を確認するには、ときどきこのテーブルを最新の情報に更新する必要があります。パイプライン操作が完了したら、パイプラインの実行の \[Status\] が **\[Succeeded\]** と表示されます。このパイプラインを実行している間、遠慮なくこの演習の次のタスクに進んでください。
    
    ![\[Pipeline runs\] 画面で、正常終了したパイプラインの実行がテーブルで強調表示されています。](media/pipeline_run_sales_successful.png "正常終了したパイプラインのインジケーター")

29. 新しいクエリを作成することによって、テーブルにデータが読み込まれていることを検証します。左側メニューから **\[Develop\]** 項目を選択し、**\[Develop\]** ブレードで **\[+\]** を展開して **\[SQL script\]** を選択します。クエリ ウィンドウで、SQL プール データベース (`SQLPool01`) に接続していることを確認して、以下のクエリを貼り付けて実行します。完了したら、上部のツールバーから **\[Discard all\]** を選択します。

```sql
  select count(TransactionId) from wwi_mcw.SaleSmall;
```

### タスク 3: 顧客情報テーブルの作成

Wide World Importers は、過去 5 年間に 30 億行を超える販売データを収集しています。このデータ量から、顧客情報ルックアップ テーブルは 1 億行を超えることが予想されますが、使用するストレージは 1.5 GB 未満です。ラボで使用するのはこのデータの一部のみですが、設計するテーブルは運用環境を想定します。この演習の説明で大まかに説明したガイダンスを使用して、**クラスター化列ストア** テーブルと、顧客データを保持する**レプリケート** テーブル分散が必要なことを確認できます。

1. 左側のメニューを展開して、**\[Develop\]** 項目を選択します。**\[Develop\]** ブレードで **\[+\]** を展開して、**\[SQL script\]** 項目を選択します。
   
   ![左側メニューが展開され、\[Develop\] 項目が選択されています。\[Develop\] ブレードで \[+\] が展開され、\[SQL script\] 項目が強調表示されています。](media/develop_newsqlscript_menu.png "SQL スクリプトの追加")

2. クエリ タブのツールバー メニューで、SQL プールの `SQLPool01` に接続していることを確認します。
   
   ![クエリ タブのツールバー メニューが表示され、\[Connect to\] が SQL プールに設定されています。](media/querytoolbar_connecttosqlpool.png "SQL プールへの接続")

3. 以下のクエリをコピーしてクエリ ウィンドウに貼り付けて、顧客情報テーブルを作成します。クエリ タブのツールバーで **\[Run\]** を選択します。
   
   ```sql
    CREATE TABLE [wwi_mcw].[CustomerInfo]
    (
      [UserName] [nvarchar](100)  NULL,
      [Gender] [nvarchar](10)  NULL,
      [Phone] [nvarchar](50)  NULL,
      [Email] [nvarchar](150)  NULL,
      [CreditCard] [nvarchar](21)  NULL
    )
    WITH
    (
      DISTRIBUTION = REPLICATE,
      CLUSTERED COLUMNSTORE INDEX
    )
    GO
   ```
   
   ![クエリ タブのツールバーが表示され、\[Run\] が選択されています。](media/querytoolbar_run.png "クエリの実行")

4. このクエリは保存しないので、上部のツールバーから **\[Discard all\]** を選択します。確認を求められたら **\[Discard changes\]** を選択します。
   
   ![上部のツールバー メニューが表示され、\[Discard all\] が強調表示されています。](media/toptoolbar_discardall.png "すべての変更の破棄")

### タスク 4: 顧客情報テーブルへのデータの読み込み

1. 顧客情報テーブルに読み込むために取得するデータは、現在はデータ レイク (Azure Data Lake Storage Gen 2 アカウント) に CSV 形式で保存されています。このデータを所有するストレージ アカウントは、環境をプロビジョニングした際に、Azure Synapse Analytics でリンクされたサービスとしてすでに追加されています。

2. 前のステップと同様に、データの保存先も、リンクされたサービスとして追加されています。ここでは、データの保存先は SQL プールの `SQLPool01` です。前のステップを繰り返しますが、今回は条件 **「sqlpool」** でフィルターして、リンクされたサービスの存在を確認します。

3. 次に実行する必要があるのは、コピーする情報を表すソース データセットを定義することです。このデータセットは、顧客情報を含む CSV ファイルを参照します。左側メニューから **\[Data\]** を選択します。**\[Data\]** ブレードで **\[+\]** を展開して、**\[Dataset\]** を選択します。
   
   ![左側メニューで \[Data\] 項目が選択されています。\[Data\] ブレードで \[+\] が展開され、\[Dataset\] 項目が強調表示されています。](media/data_newdatasetmenu.png "新しいデータセットの作成")

4. **\[New dataset\]** ブレードで **\[Azure\]** タブが選択されている状態で、**\[Azure Data Lake Storage Gen2\]** 項目を選択します。**\[Continue\]** を選択します。
   
   ![\[New dataset\] ブレードで \[All\] タブが選択され、\[Azure Data Lake Gen2\] 項目が強調表示されています。](media/newdataset_azuredatalakegen2.png "データセット タイプとして [Azure Data Lake Gen2] を選択")

5. **\[Select format\]** ブレードで **\[CSV Delimited Text\]** を選択します。**\[Continue\]** を選択します。
   
   ![\[Select format\] ブレードで \[CSV Delimited Text\] 項目が強調表示されています。](media/newdataset_selectfileformat_csv.png "データセット形式を CSV として定義")

6. **\[Set properties\]** ブレードでフィールドに以下の値を設定して、**\[OK\]** を選択します。
   
   | フィールド| 値
   |----------|----------
   | Name| **「asamcw\_customerinfo\_csv」** と入力
   | Linked service| **asadatalake{SUFFIX}**
   | File Path - コンテナー| **「wwi-02」** と入力
   | File Path - ディレクトリ| 「**customer-info**」と入力
   | File Path - ファイル| **「customerinfo.csv」** と入力
   | First row as header| オン
   | Import schema| **\[From connection/store\]** を選択

   ![\[Set properties\] フォームが表示され、前述の表で指定されている値が入力されています。](media/customerinfodatasetpropertiesform.png "データセットの構成")

7. 次に、データの保存先データセットを定義する必要があります。ここでは、顧客情報データを SQL プールに保存します。**ステップ 3** と同様に、**\[Data\]** ブレードで **\[+\]** を展開します。

8. **\[New dataset\]** ブレードで **\[Azure\]** タブが選択されている状態で、検索条件として **「synapse」** と入力し、**\[Azure Synapse Analytics (formerly SQL DW)\]** 項目を選択します。**\[Continue\]** を選択します。
   
   ![\[New dataset\] ブレードで検索条件として「synapse」が入力され、フィルター結果から \[Azure Synapse Analytics (formerly SQL DW)\] が選択されています。](media/newdataset_synapseitem.png "データセット タイプとして [Azure Synapse Analytics] を選択")

9. **\[Set properties\]** ブレードでフィールドに以下の値を設定して、**\[OK\]** を選択します。
   
   | フィールド| 値
   |----------|----------
   | Name| **「asamcw\_customerinfo\_asa」** と入力
   | Linked service| **SQLPool01**
   | Table name| **wwi\_mcw.CustomerInfo**
   | Import schema| **\[From connection/store\]**

   ![\[Set properties\] ブレードに前述の表で指定されている値が入力されています。](media/dataset_customerinfoasaform.png "データセットの [Configuration] フォーム")

10. 上部のツールバーで **\[Publish all\]** を選択して、新しいデータセット定義を公開します。確認を求められたら **\[Publish\]** を選択して、変更をコミットします。
    
    ![上部のツールバーが表示され、\[Publish all\] が強調表示されています。](media/publishall_toolbarmenu.png "変更の公開")

11. 次に、データを CustomerInfo テーブルに読み込むパイプラインを定義します。左側メニューから **\[Orchestrate\]** を選択します。\[Orchestrate\] ブレードで **\[+\]** を展開して、**\[Pipeline\]** 項目を選択します。
    
    ![左側メニューで \[Orchestrate\] メニュー項目が選択されています。\[Orchestrate\] ブレードで \[+\] が展開され、\[Pipeline\] 項目が強調表示されています。](media/orchestrate_newpipelinemenu.png "[Orchestrate] ハブ")

12. **\[Properties\]** ブレードで、**\[Name\]** フィールドに **「ASAMCW - Exercise 2 - Copy Customer Information」** と入力します。
    
    ![\[General\] タブが表示され、\[Name\] フィールドに前述の値が入力されています。](media/pipeline_customerinfo_generaltab.png "パイプラインの命名")

13. **\[Activities\]** メニューで **\[Move \& transform\]** 項目を展開します。**\[Copy data\]** アクティビティのインスタンスをパイプラインのデザイン サーフェイスにドラッグします。
    
    ![\[Activities\] メニューで \[Move and transform\] セクションが展開されています。矢印が、\[Copy data\] アクティビティのインスタンスをパイプラインのデザイン サーフェイスにドラッグすることを示しています。](media/pipeline_addcopydataactivity.png "パイプラインに対するコピー アクティビティの追加")

14. パイプライン デザイン サーフェイスで **\[Copy data\]** アクティビティを選択します。下側の **\[General\]** タブで、**\[Name\]** フィールドに **「Copy Customer Information Data」** と入力します。
    
    ![\[General\] が選択され、\[Name\] フィールドが「Copy Customer Information Data」に設定されています。](media/pipeline_copycustomerinformation_general.png "データのコピー アクティビティの命名")

15. 下側で **\[Source\]** タブを選択します。**\[Source dataset\]** フィールドで **\[asamcw\_customerinfo\_csv\]** を選択します。
    
    ![\[Source\] タブが選択され、\[Source dataset\] フィールドが \[asamcw\_customerinfo\_csv\] に設定されています。](media/pipeline_copycustomerinformation_source.png "ソース データセットの選択")

16. 下側で **\[Sink\]** タブを選択します。**\[Sink dataset\]** フィールドで **\[asamcw\_customerinfo\_asa\]** を選択し、**\[Copy method\]** フィールドで **\[Bulk insert\]** を選択し、**\[Pre-copy script\]** に以下のテキストを入力します。
    
    ```sql
      truncate table wwi_mcw.CustomerInfo
    ```
    
    ![\[Sink\] タブが選択され、\[Sink dataset\] フィールドが \[asamcw\_customerinfo\_asa\] に設定され、\[Copy method\] が \[Bulk insert\] に設定され、\[Pre-copy script\] フィールドが前述のクエリに設定されています。](media/pipeline_copycustomerinformation_sink.png "シンク データセットの選択")

17. 下側で **\[Mapping\]** タブを選択します。**\[Import schemas\]** を選択します。フィールドの名前と型が一致しているので、Azure Synapse Analytics がマッピングを自動実行したことがわかります。
    
    ![下側で \[Mapping\] タブが選択されています。ソースから保存先へのフィールド マッピングが表示されています。](media/pipeline_copycustomerinformation_mapping.png "ソースから保存先へのフィールド マッピング")

18. 上部のツールバーで **\[Publish all\]** を選択して、新しいデータセット定義を公開します。確認を求められたら **\[Publish\]** を選択して、変更をコミットします。
    
    ![上部のツールバーが表示され、\[Publish all\] が強調表示されています。](media/publishall_toolbarmenu.png "変更の公開")

19. 公開されたら、パイプライン デザイナーのツールバーで **\[Add trigger\]** 項目を展開して、**\[Trigger now\]** を選択します。**\[Pipeline run\]** ブレードで **\[OK\]** を選択して、最後に公開した構成で先に進みます。パイプラインが動作していることおよびパイプラインの完了時を示すトースト通知ウィンドウが表示されます。

20. \[Orchestrate\] ブレードで **\[ASAMCW - Exercise 2 - Copy Customer Information\]** パイプラインを特定して、完了した実行のステータスを表示します。アクション メニューを展開して、**\[Monitor\]** 項目を選択します。
    
    ![\[Orchestrate\] ブレードで、\[ASAMCW - Exercise 2 - Copy Customer Information\] パイプラインのアクション メニューが表示され、\[Monitor\] 項目が選択されています。](media/pipeline_copycustomerinformation_monitormenu.png "パイプラインの監視")

21. **\[Pipeline runs\]** テーブルで、作成したパイプラインの実行が正常終了したことが表示されます。
    
    ![\[Pipeline runs\] 画面で、正常終了したパイプラインの実行がテーブルで強調表示されています。](media/pipeline_run_customerinfo_successful.png "正常終了したパイプライン実行のインジケーター")

22. 新しいクエリを作成することによって、テーブルにデータが読み込まれていることを検証します。**タスク 1** と同様に、左側メニューから **\[Develop\]** 項目を選択し、**\[Develop\]** ブレードで **\[+\]** を展開して **\[SQL script\]** を選択します。クエリ ウィンドウで、SQL プール データベース (`SQLPool01`) に接続していることを確認して、以下のクエリを貼り付けて実行します。完了したら、上部のツールバーから **\[Discard all\]** を選択します。

```sql
  select * from wwi_mcw.CustomerInfo;
```

### タスク 5: キャンペーン分析テーブルの作成

キャンペーン分析テーブルに対するクエリは、主にダッシュボードと KPI で実行されます。このテーブルを設計するにあたってパフォーマンスは重要な要素です。したがって、**クラスター化列ストア** テーブルと、極めて均等にデータを分散する **Region** フィールドに基づく**ハッシュ** テーブル分散が必要なことを確認できます。

1. 左側のメニューを展開して、**\[Develop\]** 項目を選択します。**\[Develop\]** ブレードで **\[+\]** を展開して、**\[SQL script\]** 項目を選択します。
   
   ![左側メニューが展開され、\[Develop\] 項目が選択されています。\[Develop\] ブレードで \[+\] が展開され、\[SQL script\] 項目が強調表示されています。](media/develop_newsqlscript_menu.png "新しい SQL スクリプトの作成")

2. クエリ タブのツールバー メニューで、SQL プールの `SQLPool01` に接続していることを確認します。
   
   ![クエリ タブのツールバー メニューが表示され、\[Connect to\] が SQL プールに設定されています。](media/querytoolbar_connecttosqlpool.png "SQL プールへの接続")

3. 以下のクエリをコピーしてクエリ ウィンドウに貼り付けて、キャンペーン分析テーブルを作成します。クエリ タブのツールバーで **\[Run\]** を選択します。
   
   ```sql
   CREATE TABLE [wwi_mcw].[CampaignAnalytics]
   (
       [Region] [nvarchar](50)  NULL,
       [Country] [nvarchar](30)  NOT NULL,
       [ProductCategory] [nvarchar](50)  NOT NULL,
       [CampaignName] [nvarchar](500)  NOT NULL,
       [Analyst] [nvarchar](25) NULL,
       [Revenue] [decimal](10,2)  NULL,
       [RevenueTarget] [decimal](10,2)  NULL,
       [City] [nvarchar](50)  NULL,
       [State] [nvarchar](25)  NULL
   )
   WITH
   (
       DISTRIBUTION = HASH ( [Region] ),
       CLUSTERED COLUMNSTORE INDEX
   );  
   ```
   
   ![クエリ タブのツールバーが表示され、\[Run\] が選択されています。](media/querytoolbar_run.png "クエリの実行")

4. このクエリは保存しないので、上部のツールバーから **\[Discard all\]** を選択します。確認を求められたら **\[Discard changes\]** を選択します。
   
   ![上部のツールバー メニューが表示され、\[Discard all\] が強調表示されています。](media/toptoolbar_discardall.png "すべての変更の破棄")

### タスク 6: キャンペーン分析テーブルへのデータの読み込み

顧客情報テーブルと同様に、キャンペーン分析テーブルも、データ レイクにある CSV ファイルからデータを読み込みます。そのために、ストレージにある CSV ファイルを参照するソース データセットとシンク データセット、および SQL プールに作成したキャンペーン分析テーブルが必要です。受け取ったソース CSV ファイルは適切にフォーマットされていなかったので、データ ウェアハウスにインポートする前にこのデータを調整するためのデータ変換を追加する必要があります。

1. ソース データセットは、キャンペーン分析情報を含む CSV ファイルを参照します。左側メニューから **\[Data\]** を選択します。**\[Data\]** ブレードで **\[+\]** を展開して、**\[Dataset\]** を選択します。
   
   ![左側メニューで \[Data\] 項目が選択されています。\[Data\] ブレードで \[+\] が展開され、\[Dataset\] 項目が強調表示されています。](media/data_newdatasetmenu.png "新しいデータセットの作成")

2. **\[New dataset\]** ブレードで **\[All\]** タブが選択されている状態で、**\[Azure Data Lake Storage Gen2\]** 項目を選択します。**\[Continue\]** を選択します。
   
   ![\[New dataset\] ブレードで \[All\] タブが選択され、リストで \[Azure Data Lake Storage Gen2\] 項目が選択されています。](media/new_dataset_type_selection.png "データセット タイプの選択")

3. **\[Select format\]** ブレードで **\[CSV Delimited Text\]** を選択します。**\[Continue\]** を選択します。
   
   ![\[Select format\] ブレードで \[CSV Delimited Text\] 項目が強調表示されています。](media/newdataset_selectfileformat_csv.png "データセット形式の選択")

4. **\[Set properties\]** ブレードでフィールドに以下の値を設定して、**\[OK\]** を選択します。データのプレビューを選択して、CSV ファイルのサンプルを表示できます。先頭行をヘッダーとして設定していないので、ヘッダー列が先頭行として表示されることがわかります。また、市と州の値が表示されないことがわかります。これは、ヘッダー行の列数が、ファイルの残りの部分と一致していないためです。このあとすぐに、データ変換で先頭行を除外します。
   
   | フィールド| 値
   |----------|----------
   | Name| **「asamcw\_campaignanalytics\_csv」** と入力
   | Linked service| **\[asadatalake{SUFFIX}\]** を選択
   | File Path - コンテナー| **「wwi-02」** と入力
   | File Path - ディレクトリ| 「**campaign-analytics**」と入力
   | File Path - ファイル| 「**campaignanalytics.csv**」と入力
   | First row as header| オフ
   | Import schema| **\[From connection/store\]** を選択

   ![\[Set properties\] フォームが表示され、前述の表で指定されている値が入力されています。](media/campaignanalyticsdatasetpropertiesform.png)

5. 中央のペインにある **\[asamcw\_campainganalytics\_csv\]** データセットの **\[Connection\]** タブで、以下のフィールド値を確実に設定します。
   
   | フィールド| 値
   |----------|----------
   | エスケープ文字| **バックスラッシュ (\\)**
   | 引用符文字| **二重引用符 (")**


6. 次に、データの保存先データセットを定義する必要があります。ここでは、キャンペーン分析データを SQL プールに保存します。**\[Data\]** ブレードで **\[+\]** を展開して、**\[Dataset\]** を選択します。

7. **\[New dataset\]** ブレードで **\[Azure\]** タブが選択されている状態で、検索条件として **「synapse」** と入力し、**\[Azure Synapse Analytics (formerly SQL DW)\]** 項目を選択します。**\[Continue\]** を選択します。
   
   ![\[New dataset\] ブレードで検索条件として「synapse」が入力され、フィルター結果から \[Azure Synapse Analytics (formerly SQL DW)\] が選択されています。](media/newdataset_synapseitem.png "データセット タイプの選択")

8. **\[Set properties\]** ブレードでフィールドに以下の値を設定して、**\[OK\]** を選択します。
   
   | フィールド| 値
   |----------|----------
   | Name| **「asamcw\_campaignanalytics\_asa」** と入力
   | Linked service| **SQLPool01**
   | Table name| **wwi\_mcw.CampaignAnalytics**
   | Import schema| **\[From connection/store\]** を選択

   ![\[Set properties\] ブレードに前述の表で指定されている値が入力されています。](media/dataset_campaignanalyticsasaform.png "[dataset configuration] フォーム")

9. 上部のツールバーで **\[Publish all\]** を選択して、新しいデータセット定義を公開します。確認を求められたら **\[Publish\]** を選択して、変更をコミットします。
   
   ![上部のツールバーが表示され、\[Publish all\] が強調表示されています。](media/publishall_toolbarmenu.png "変更の発行")

10. ソース データのフォーマットが適切ではなく、Analyst の列が含まれていないので、ソース データを変換するデータ フローを作成する必要があります。データ フローを使用すると、コードを記述することなく、グラフィカルにデータセット フィルターと変換を定義できます。これらのデータ フローは、オーケストレーション パイプラインでアクティビティとして利用できます。まず左側メニューから **\[Develop\]** を選択し、**\[Develop\]** ブレードで **\[+\]** を展開して **\[Data flow\]** を選択することによって、新しいデータ フローを作成します。
    
    ![左側メニューから \[Develop\] 項目が選択されています。\[Develop\] ブレードで \[+\] が展開され、\[Data flow\] 項目が強調表示されています。](media/develop_newdataflow_menu.png "新しいデータフローの作成")

11. **\[Properties\]** ブレードで、**\[Name\]** フィールドに **「ASAMCW\_Exercise\_2\_Campaign\_Analytics\_Data」** と入力して、データ フローに名前を付けます。
    
    ![\[Properties\] ブレードが表示され、データ フローの名前として「ASAMCW\_Exercise\_2\_Campaign\_Analytics\_Data」と入力されています。](media/dataflow_campaignanalytics_propertiesblade.png "データ フローの命名")

12. データ フロー デザイナー ウィンドウで **\[Add Source\]** ボックスを選択します。
    
    ![データ フロー デザイナー ウィンドウで \[Add source\] ボックスが強調表示されています。](media/dataflow_addsourcebox.png "データ フロー ソースの追加")

13. **\[Source settings\]** で、以下のように構成します。
    
    | フィールド| 値
    |----------|----------
    | Output stream name| 「**campaignanalyticscsv**」と入力
    | Source type| **Dataset**
    | Dataset| **asamcw\_campaignanalytics\_csv**
    | Skip line count| **「1」** と入力

    ![\[Source settings\] タブが表示され、フォームに前述の表で定義されている値が入力されています。](media/dataflow_campaignanalytics_sourcesettings.png "[data flow configuration] フォーム")

14. データ フローを作成する際、デバッグをオンにすることによって、データのプレビュー、スキーマのインポート (プロジェクション) など、一部の機能が有効になります。このオプションを有効にするためにかかる時間およびラボの環境上の制約により、これらの機能は回避します。データ ソースのスキーマを設定する必要があります。それには、データフロー デザイナーのツールバー メニューの右側にある**スクリプト** アイコンを選択します。
    
    ![データフロー デザイナーのツールバーの一部が表示され、スクリプト アイコンが強調表示されています。](media/dataflow_toolbarscriptmenu.png "データ フローのスクリプト アイコン")

15. スクリプトを以下のテキストで置き換えて列マッピング (`output`) を指定して、**\[OK\]** を選択します。
    
    ```json
        source(output(
            {_col0_} as string,
            {_col1_} as string,
            {_col2_} as string,
            {_col3_} as string,
            {_col4_} as string,
            {_col5_} as double,
            {_col6_} as string,
            {_col7_} as double,
            {_col8_} as string,
            {_col9_} as string
        ),
        allowSchemaDrift: true,
        validateSchema: false,
        skipLines: 1) ~> campaignanalyticscsv
    ```
    
    > **注**: ソース ファイルはヘッダーが間違っていて壊れているので、マッピングを変更しています。

16. **\[campaignanalyticscsv\]** データ ソースを選択して、**\[Projection\]** を選択します。プロジェクトにより、以下のスキーマが表示されます。
    
    ![\[Projection\] タブが表示され、列マッピング スクリプトの記述に従って列が定義されています。](media/dataflow_campaignanalytics_projectiontab.png "ソースの列マッピング")

17. **\[campaignanalyticscsv\]** ソースの右下の **\[+\]** を選択して、コンテキスト メニューから **\[Select\]** スキーマ修飾子を選択します。
    
    ![\[campaignanalyticscsv\] ソースの右下の \[+\] が強調表示されています。](media/dataflow_campaignanalytics_addstep.png "[Select] スキーマ修飾子の追加")

18. 下側の **\[Select settings\]** で、以下のように構成します。
    
    | フィールド| 値
    |----------|----------
    | Output stream name| **「mapcampaignanalytics」** と入力

    **\[Input Columns\]** の **\[Name as\]** 列に、以下のリストの値をこの順序で入力します。
    
    - Region
    - Country
    - ProductCategory
    - CampaignName
    - RevenuePart1
    - Revenue
    - RevenueTargetPart1
    - RevenueTarget
    - City
    - State
    
    ![\[Select settings\] タブが表示され、フォームに前述の表で記述されている値が入力されています。](media/dataflow_mapcampaignanalytics_selectsettings.png "Select スキーマ修飾子の構成")

19. **\[mapCampaignAnalytics**\] ソースの右側の \[+\] を選択して、コンテキスト メニューから **\[Derived Column\]** スキーマ修飾子を選択します。

20. **\[**Derived column's settings**\]** で、以下のように構成します。
    
    | フィールド| 値
    |----------|----------
    | Output stream name| 「**convertandaddcolumns**」と入力

    **\[Columns\]** で以下の値を追加します (**「Analyst」** 列を入力する必要があることに注意してください)。
    
    | 列| 式| 説明
    |----------|----------|----------
    | Revenue| **toDecimal(replace(concat(toString(RevenuePart1), toString(Revenue)), '\\\\', ''), 10, 2, '$###,###.##')**| **RevenuePart1** フィールドと **Revenue** フィールドを連結して無効な `\` 文字を置き換え、データを decimal 型に変換およびフォーマットします。
    | RevenueTarget| **toDecimal(replace(concat(toString(RevenueTargetPart1), toString(RevenueTarget)), '\\\\', ''), 10, 2, '$###,###.##')**| **RevenueTargetPart1** フィールドと **RevenueTarget** フィールドを連結して無効な `\` 文字を置き換え、データを decimal 型に変換およびフォーマットします。
    | Analyst| **iif(isNull(City), '',  replace('DataAnalyst'+ City,' ',''))**| City フィールドが null の場合、空文字列を Analyst フィールドに代入します。それ以外の場合、DataAnalyst と City 値を連結して、すべてのスペースを削除します。

    ![派生列の設定が、記述されたとおりに表示されています。](media/dataflow_campaignanalytics_derivedcolumns.png "式に基づく列の派生")

21. **\[convertandaddcolumns\]** ステップの右側の **\[+\]** を選択して、コンテキスト メニューから **\[Select\]** スキーマ修飾子を選択します。

22. **\[Select settings\]** で、以下のように構成します。
    
    | フィールド| 値
    |----------|----------
    | Output stream name| **「selectcampaignanalyticscolumns」** と入力
    | Input columns| **\[RevenuePart1\]** 列と **\[RevenueTargetPart1\]** 列を削除

    ![\[Select settings\] が表示され、更新された列マッピングが表示されています。](media/dataflow_campaignanalytics_select2.png "Select スキーマ修飾子の構成")

23. **\[selectcampaignanalyticscolumns\]** ステップの右側の **\[+\]** を選択して、コンテキスト メニューから **\[**Sink**\]** 保存先を選択します。

24. 下側の **\[Sink\]** タブで、以下のように構成します。
    
    | フィールド| 値
    |----------|----------
    | Output stream name| **「campaignanlyticsasa」** と入力
    | Dataset| **asamcw\_campaignanalytics\_asa**

    ![\[Sink settings\] フォームが表示され、前述の表で定義されている値が入力されています。](media/dataflow_campaignanalytics_sink.png "データ フロー シンクの構成")

25. **\[Settings\]** タブを選択して、**\[Table action\]** で **\[Truncate table\]** を選択します。
    
    ![\[sink Settings\] タブが表示され、\[Table action\] が \[Truncate table\] に設定されています。](media/dataflow_campaignanalytics_sinksettings.png "[Truncate table] アクション")

26. 完成したデータ フローは、以下のようになります。
    
    ![完成したデータ フローが表示されています。](media/dataflow_campaignanalytics_complete.png "完成したデータ フロー")

27. **\[Publish all\]** を選択して、新しいデータ フローを保存します。
    
    ![\[Publish all\] が強調表示されています。](media/publishall_toolbarmenu.png "Publish all")

28. データ フローが公開されたので、それをパイプラインで使用できます。左側メニューから **\[Orchestrate\]** を選択し、**\[Orchestrate\]** ブレードで **\[+\]** を展開して **\[Pipeline\]** を選択することによって、新しいパイプラインを作成します。

29. パイプライン デザイナーの右側にある **\[Properties\]** ペインで、**\[Name\]** フィールドに **「ASAMCW - Exercise 2 - Copy Campaign Analytics Data」** と入力します。
    
    ![パイプライン プロパティ ブレードが表示され、\[Name\] フィールドに「ASAMCW - Exercise 2 - Copy Campaign Analytics Data」と入力されています。](media/pipeline_properties_blade.png "パイプラインの命名")

30. **\[Activities\]** メニューで **\[Move \& transform\]** セクションを展開して、**\[Data flow\]** のインスタンスをパイプラインのデザイン サーフェイスにドラッグします。
    
    ![パイプラインの \[Activities\] メニューが表示され、\[Move and transform\] セクションが展開されています。ドラッグ操作を示す矢印によって、\[Data flow\] アクティビティをパイプラインのデザイン サーフェイスに追加する操作が示されています。](media/pipeline_sales_dataflowactivitymenu.png "パイプラインに対するデータ フロー アクティビティの追加")

31. **\[Adding data flow\]** ブレードで、データ フローの **\[ASAMCW\_Exercise\_2\_Campaign\_Analytics\_Data\]** を選択し、**\[OK\]** を選択します。デザイン サーフェイスで \[Mapping Data Flow\] アクティビティを選択します。

32. 下側で **\[Settings\]** タブを選択して、フォームのフィールドに以下の値を設定します。
    
    | フィールド| 値
    |----------|----------
    | Data flow| **ASAMCW\_Exercise\_2\_Campaign\_Analytics\_Data**
    | Staging linked service| **asadatalake{SUFFIX}**
    | Staging storage folder - コンテナー| **「staging」** と入力
    | Staging storage folder - ディレクトリ| **「mcwcampaignanalytics」** と入力

    ![データ フロー アクティビティの \[Settings\] タブが表示され、前述の表で指定されているフィールドが強調表示されています。](media/pipeline_campaigndata_dataflowsettings.png "データ フロー アクティビティの構成")

33. 上部のツールバーで **\[Publish all\]** を選択して、新しいパイプラインを公開します。確認を求められたら **\[Publish\]** を選択して、変更をコミットします。
    
    ![上部のツールバーが表示され、\[Publish all\] が強調表示されています。](media/publishall_toolbarmenu.png "変更の発行")

34. 公開されたら、パイプライン デザイナーのツールバーで **\[Add trigger\]** 項目を展開して、**\[Trigger now\]** を選択します。**\[Pipeline run\]** ブレードで **\[OK\]** を選択して、最後に公開した構成で先に進みます。パイプラインが動作していることおよびパイプラインの完了時を示すトースト通知ウィンドウが表示されます。

35. \[Orchestrate\] ブレードで **\[**ASAMCW - Exercise 2 - Copy Campaign Analytics Data**\]** パイプラインを特定して、パイプラインの実行のステータスを表示します。アクション メニューを展開して、**\[Monitor\]** 項目を選択します。
    
    ![\[Orchestrate\] ブレードで、\[ASAMCW - Exercise 2 - Copy Campaign Analytics Data\] パイプラインのアクション メニューが表示され、\[Monitor\] 項目が選択されています。](media/orchestrate_pipeline_monitor_copycampaigndata.png "パイプライン実行の監視")

36. **\[Pipeline runs\]** テーブルで、作成したパイプラインの実行が進行中と表示されます。最新の進行状況を確認するには、ときどきこのテーブルを最新の情報に更新する必要があります。パイプライン操作が完了したら、パイプラインの実行の \[Status\] が **\[Succeeded\]** と表示されます。

37. 新しいクエリを作成することによって、テーブルにデータが読み込まれていることを検証します。左側メニューから **\[Develop\]** 項目を選択し、**\[Develop\]** ブレードで **\[+\]** を展開して **\[SQL script\]** を選択します。クエリ ウィンドウで、SQL プール データベース (`SQLPool01`) に接続していることを確認して、以下のクエリを貼り付けて実行します。完了したら、上部のツールバーから **\[Discard all\]** を選択します。

```sql
  select count(Region) from wwi_mcw.CampaignAnalytics;
```

### タスク 7: 製品テーブルへのデータの読み込み

ラボの環境をプロビジョニングしたときに、**wwi\_mcw.Product** テーブルおよびそのデータの読み込みに必要なデータセットを作成済みです。この演習を通じて、データセット、データ フロー、およびパイプラインの作成を経験しました。製品テーブルへのデータの読み込みは繰り返しになるので、ここでは単に、既存のパイプラインをトリガーしてこのテーブルにデータを読み込みます。

1. 左側メニューから **\[Orchestrate\]** を選択します。**\[Orchestrate\]** ブレードで **\[Pipelines\]** セクションを展開し、**\[ASAMCW - Exercise 2 - Copy Product Information\]** パイプラインを特定して選択します。

2. パイプライン デザイナーのツールバーで **\[Add trigger\]** 項目を展開して、**\[Trigger now\]** を選択します。**\[Pipeline run\]** ブレードで **\[OK\]** を選択して、最後に公開した構成で先に進みます。パイプラインが動作していることおよびパイプラインの完了時を示すトースト通知ウィンドウが表示されます。

3. \[Orchestrate\] ブレードで **\[**ASAMCW - Exercise 2 - Copy Product Information**\]** パイプラインを特定して、パイプラインの実行のステータスを表示します。アクション メニューを展開して、**\[Monitor\]** 項目を選択します。

4. **\[Pipeline runs\]** テーブルで、作成したパイプラインの実行が進行中 (または正常終了) と表示されます。パイプライン操作が完了したら、パイプラインの実行の \[Status\] が **\[Succeeded\]** と表示されます。

5. 新しいクエリを作成することによって、テーブルにデータが読み込まれていることを検証します。左側メニューから **\[Develop\]** 項目を選択し、**\[Develop\]** ブレードで **\[+\]** を展開して **\[SQL script\]** を選択します。クエリ ウィンドウで、SQL プール データベース (`SQLPool01`) に接続していることを確認して、以下のクエリを貼り付けて実行します。完了したら、上部のツールバーから **\[Discard all\]** を選択します。

```sql
  select * from wwi_mcw.Product;
```

## 演習 3: 生 Parquet の調査

**所要時間**: 30 分

データ調査を通じてデータを理解することは、データ エンジニアとデータ サイエンティストが今日直面している大きな課題の 1 つです。データの基本構造および調査プロセスの特定の要件に応じて、さまざまなデータ処理エンジンがさまざまなレベルのパフォーマンス、複雑さ、および柔軟性を示します。

Azure Synapse Analytics では、Synapse SQL サーバーレス エンジンまたはビッグデータ Spark エンジンの一方または両方を使用する可能性があります。

この演習では、両方のオプションを使用して、データ レイクを調査します。

### タスク 1: Synapse SQL サーバーレスによる販売 Parquet データに対するクエリの実行

Synapse SQL サーバーレスを使用して Parquet ファイルに対してクエリを実行する際、T-SQL 構文を使用してデータを調査できます。

1. 左側メニューから **\[Data\]** を選択します。

2. **\[Data\]** ブレードで、**\[Linked\]** タブを選択します。

3. **\[Storage accounts\]** を展開します。\[`asadatalake{SUFFIX}`\] ADLS Gen2 アカウントを展開して、**\[wwi-02\]** を選択します。

4. **\[wwi-02/sale-small/Year=2010/Quarter=Q4/Month=12/Day=20101231\]** フォルダーに移動します。**\[sale-small-20101231-snappy.parquet\]** ファイルを右クリックして、**\[New SQL script\]**、**\[Select TOP 100 rows\]** の順に選択します。
   
   ![\[Storage accounts\] セクションが展開され、\[asadatalake{SUFFIX}\] アカウントのコンテキスト メニューの \[Select TOP 100 rows\] オプションが強調表示されています。](media/data-hub-parquet-select-rows.png "SQL サーバーレス内の Parquet データのクエリ")

5. クエリ ウィンドウの上の **\[Connect to\]** ドロップダウン リストで **\[SQL on-demand\]** が選択されていることを確認して、クエリを実行します。Synapse SQL サーバーレス エンドポイントによってデータが読み込まれ、標準のリレーショナル データベースからの読み込みのように処理されます。
   
   ![クエリ ウィンドウのツールバーで \[SQL on-demand\] 接続が強調表示されています。](media/sql-on-demand-selected.png "SQL on-demand")

6. データの理解を深めるために、集計操作とグループ化操作を実行するように SQL クエリを変更します。クエリを以下のテキストで置き換えて、**OPENROWSET** のファイル パスが各自の現在のファイル パスと一致していることを確認します。必ず `asadatalake{SUFFIX}` を各自の環境に適した値に置き換えてください。
   
   ```sql
   SELECT
       TransactionDate, ProductId,
       CAST(SUM(ProfitAmount) AS decimal(18,2)) AS [(sum) Profit],
       CAST(AVG(ProfitAmount) AS decimal(18,2)) AS [(avg) Profit],
       SUM(Quantity) AS [(sum) Quantity]
   FROM
       OPENROWSET(
           BULK 'https://asadatalake{SUFFIX}.dfs.core.windows.net/wwi-02/sale-small/Year=2010/Quarter=Q4/Month=12/Day=20101231/sale-small-20101231-snappy.parquet',
           FORMAT='PARQUET'
       ) AS [r] GROUP BY r.TransactionDate, r.ProductId;
   ```
   
   ![クエリ ウィンドウ内に上記の T-SQL クエリが表示されています。](media/sql-serverless-aggregates.png "クエリ ウィンドウ")

7. 次に、2019 年のデータの Parquet ファイルに含まれるレコード数を調べます。この情報は、Azure Synapse Analytics へのデータのインポートを最適化する方法を計画するために重要です。それには、クエリを以下のテキストで置き換えます (必ず `asadatalake{SUFFIX}` を置き換えて、BULK ステートメントの自分のデータ レイクの名前を更新してください)。
   
   ```sql
   SELECT
       COUNT_BIG(*)
   FROM
       OPENROWSET(
           BULK 'https://asadatalake{SUFFIX}.dfs.core.windows.net/wwi-02/sale-small/Year=2019/*/*/*/*',
           FORMAT='PARQUET'
       ) AS [r];
   ```
   
   > `sale-small/Year=2019` のすべてのサブフォルダーのすべての Parquet ファイルを含めるためのパスの更新方法に注意してください。
   
   レコード数は **339507246** と出力されます。

### タスク 2: Azure Synapse Spark による販売 Parquet データに対するクエリの実行

1. 左側メニューから **\[Data\]** を選択し、**\[Linked\]** タブを選択し、データ レイク ストレージ アカウント `asadatalake{SUFFIX}` の **wwi-02/sale-small/Year=2010/Quarter=Q4/Month=12/Day=20101231** を参照します。Parquet ファイルを右クリックして、\[New notebook\] を選択します。
   
   ![Parquet ファイルが表示され、\[New notebook\] メニュー項目が強調表示されています。](media/new-spark-notebook-sales.png "New notebook")

2. これにより、データフレームにデータを読み込んでヘッダー付きで 100 行を表示する PySpark コードを含むノートブックが生成されます。

3. このノートブックを Spark プールにアタッチします。
   
   ![Spark プール リストが表示されています。](media/attach-spark-pool.png "Spark プールへのアタッチ")

4. ノートブックのツールバーで **\[Run all\]** を選択して、ノートブックを実行します。
   
   > **注:** Spark プールで初めてノートブックを実行する際、Synapse が新しいセッションを作成します。これには約 5 分かかる可能性があります。
   
   > **注:** 特定のセルだけを実行するには、そのセルをポイントして、セルの左側の "セルの実行" アイコンを選択するか、またはセルを選択してキーボードで **Ctrl + Enter** キーを押します。

5. ノートブックの下方の空白スペースをポイントして **\[{} Add code\]** を選択することによって、すぐ下に新しいセルを作成します。
   
   ![\[Add Code\] メニュー オプションが強調表示されています。](media/new-cell.png "Add code")

6. Spark エンジンは、Parquet ファイルを解析して、そのスキーマを推測できます。それには、新しいセルに以下のテキストを入力します。
   
   ```python
   data_path.printSchema()
   ```
   
   以下のような出力が得られます。
   
   ```text
   root
       |-- TransactionId: string (nullable = true)
       |-- CustomerId: integer (nullable = true)
       |-- ProductId: short (nullable = true)
       |-- Quantity: short (nullable = true)
       |-- Price: decimal(29,2) (nullable = true)
       |-- TotalAmount: decimal(29,2) (nullable = true)
       |-- TransactionDate: integer (nullable = true)
       |-- ProfitAmount: decimal(29,2) (nullable = true)
       |-- Hour: byte (nullable = true)
       |-- Minute: byte (nullable = true)
       |-- StoreId: short (nullable = true)
   ```

7. 次に、データフレームを使用して、SQL サーバーレス プールを使用して実行したのと同じグループ化と集計のクエリを実行します。新しいセルを作成して、以下のテキストを入力します。
   
   ```python
   from pyspark.sql import SparkSession
   from pyspark.sql.types import *
   from pyspark.sql.functions import *
   
   profitByDateProduct = (data_path.groupBy("TransactionDate", "ProductId")
   .agg(
   round(sum("ProfitAmount"),2).alias("(sum)Profit"),
   round(avg("ProfitAmount"),2).alias("(avg)Profit"),
   sum("Quantity").alias("(sum)Quantity")
   ).orderBy("TransactionDate", "ProductId")
   )
   profitByDateProduct.show(100)
   ```

> クエリを正常に実行するために、スキーマで定義されている集計関数と型を使用するために必要な Python ライブラリをインポートしています。

## 演習 4: Azure Synapse SQL サーバーレスによるテキストベースの生データの調査

**所要時間**: 15 分

データをエクスポートおよび保存するための共通フォーマットは、テキストベースのファイルです。たとえば、CSV ファイルや JSON 構造化データ ファイルなどの区切り記号付きテキスト ファイルです。Azure Synapse Analytics は、これらの種類の生ファイルに対してクエリを実行する方法も提供しており、それらのファイルが処理されるのを待つことなく、データに対する価値ある洞察を得られます。

### タスク 1: CSV データに対するクエリの実行

1. 左側メニューから **\[Develop\]** を選択し、**\[Develop\]** ブレードで **\[+\]** を展開して **\[SQL script\]** を選択することによって、新しい SQL スクリプトを作成します。

2. クエリ ウィンドウの上の **\[Connect to\]** ドロップダウン リストで **\[SQL on-demand\]** が選択されていることを確認します。
   
   ![クエリ ウィンドウのツールバーで \[SQL on-demand\] 接続が強調表示されています。](media/sql-on-demand-selected.png "SQL on-demand")

3. このシナリオでは、製品テーブルへのデータの読み込みに使用した CSV ファイルに対してクエリを実行します。このファイルは、`asadatalake{SUFFIX}` アカウントの **wwi-02/data-generators/generator-product.csv** にあります。このファイルからすべてのデータを選択します。以下のクエリをコピーしてクエリ ウィンドウに貼り付けて、クエリ ウィンドウのツールバー メニューで **\[Run\]** を選択します。必ず `asadatalake{SUFFIX}` を各自のストレージ アカウント名で置き換えてください。
   
   ```sql
   SELECT
      csv.*
   FROM
       OPENROWSET(
           BULK 'https://asadatalake{SUFFIX}.dfs.core.windows.net/wwi-02/data-generators/generator-product/generator-product.csv',
           FORMAT='CSV',
           FIRSTROW = 1
       ) WITH (
           ProductID INT,
           Seasonality INT,
           Price DECIMAL(10,2),
           Profit DECIMAL(10,2)
       ) as csv
   ```
   
   > **注**: このクエリでは、1 つのファイルに対してのみクエリを実行しています。Azure Synapse Analytics では、ファイルのパスにワイルドカードを使用することによって、(一様に構造化された) 一連の CSV ファイルにわたってクエリを実行できます。

4. このデータに対して集計を実行することもできます。クエリを以下のテキストで置き換えて、ツールバー メニューで **\[Run\]** を実行します。必ず `asadatalake{SUFFIX}` を各自のストレージ アカウント名で置き換えてください。
   
   ```sql
   SELECT
       Seasonality,
       SUM(Price) as TotalSalesPrice,
       SUM(Profit) as TotalProfit
   FROM
       OPENROWSET(
           BULK 'https://asadatalake{SUFFIX}.dfs.core.windows.net/wwi-02/data-generators/generator-product/generator-product.csv',
           FORMAT='CSV',
           FIRSTROW = 1
       ) WITH (
           ProductID INT,
           Seasonality INT,
           Price DECIMAL(10,2),
           Profit DECIMAL(10,2)
       ) as csv
   GROUP BY
       csv.Seasonality
   ```

5. 前出のクエリを実行した後で、**\[Results\]** タブでビューを **\[Chart\]** に切り替えて、このデータの集計を可視化したものを表示します。最適な可視化が得られるように、遠慮なくチャート設定を試してください。
   
   ![前出の集計クエリの結果が、\[Results\] ペインでチャートとして表示されています。](media/querycsv_serverless_chart.png "集計クエリの結果")

6. このクエリは保存しないので、上部のツールバーから **\[Discard all\]** を選択します。確認を求められたら **\[Discard changes\]** を選択します。
   
   ![上部のツールバー メニューが表示され、\[Discard all\] が強調表示されています。](media/toptoolbar_discardall.png "変更の破棄")

### タスク 2: JSON データに対するクエリの実行

1. 左側メニューから **\[Develop\]** を選択し、**\[Develop\]** ブレードで **\[+\]** を展開して **\[SQL script\]** を選択することによって、新しい SQL スクリプトを作成します。

2. クエリ ウィンドウの上の **\[Connect to\]** ドロップダウン リストで **\[SQL on-demand\]** が選択されていることを確認します。
   
   ![クエリ ウィンドウのツールバーで \[SQL on-demand\] 接続が強調表示されています。](media/sql-on-demand-selected.png "SQL on-demand")

3. クエリを以下のテキストで置き換えます。必ず `asadatalake{SUFFIX}` を各自のストレージ アカウントの名前で置き換えてください。
   
   ```sql
   SELECT
       products.*
   FROM
       OPENROWSET(
           BULK 'https://asadatalake{SUFFIX}.dfs.core.windows.net/wwi-02/product-json/json-data/*.json',
           FORMAT='CSV',
           FIELDTERMINATOR ='0x0b',
           FIELDQUOTE = '0x0b',
           ROWTERMINATOR = '0x0b'
       )
       WITH (
           jsonContent NVARCHAR(200)
       ) AS [raw]
   CROSS APPLY OPENJSON(jsonContent)
   WITH (
       ProductId INT,
       Seasonality INT,
       Price DECIMAL(10,2),
       Profit DECIMAL(10,2)
   ) AS products
   ```

4. このクエリは保存しないので、上部のツールバーから **\[Discard all\]** を選択します。確認を求められたら **\[Discard changes\]** を選択します。
   
   ![上部のツールバー メニューが表示され、\[Discard all\] が強調表示されています。](media/toptoolbar_discardall.png "変更の破棄")

## 演習 5: Synapse パイプラインと Cognitive Search

**所要時間**: 45 分

この演習では、サプライヤーの請求書から部品価格の更新を調整する Synapse パイプラインを作成します。これは、カスタム スキルとして、Form Recognizer サービスを呼び出す Azure Cognitive Search スキルセットと Synapse パイプラインを組み合わせることによって達成されます。このパイプラインは、以下のように動作します。

- 請求書が、Azure Storage にアップロードされます。
- Azure Cognitive Search インデックスが開始されます。
- 新しい請求書または更新された請求書のインデックスによって、Azure Cognitive Search スキルセットが呼び出されます。
- スキルセット内の最初のスキルは、Azure Function を呼び出し、それに PDF 請求書の URL を渡します。
- Azure Function は、Form Recognizer サービスを呼び出し、それに PDF 請求書の URL と SAS トークンを渡します。Forms Recognizer は、OCR の結果をこの関数に返します。
- Azure Function は、その結果をスキルセットに返します。次に、そのスキルセットは、製品名とコストのみを抽出し、それを構成ナレッジ ストアに送信します。このナレッジ ストアは、Azure Blob Storage の JSON ファイルに、抽出されたデータを書き込みます。
- Synapse パイプラインは、データ フロー アクティビティで Azure Storage からこれらの JSON ファイルを読み取り、Synapse SQL プール内の製品カタログ テーブルに対して更新/挿入 (upsert) を実行します。

### タスク 1: 請求書のストレージ コンテナーの作成

1. Azure Portal で、ラボ リソース グループに移動し、**asastore{suffix}** ストレージ アカウントを選択します。
   
   ![ラボ リソース リストが表示され、asastore ストレージ アカウントが強調表示されています。](media/ex5-task1a-000.png "Lab リソース グループのリスト")

2. 左側メニューから、**\[Blob service\]** の下にある **\[Containers\]** を選択します。**\[Containers\]** 画面の上部のツールバー メニューから **\[+ Container\]** を選択します。
   
   ![\[Containers\] 画面が表示され、左側メニューで \[Containers\] が選択され、ツールバーで \[+ Container\] が選択されています。](media/ex5-task1a-001.png "Azure Storage Container 画面")

3. **\[New container\]** ブレードで、コンテナーに **invoices** という名前を付け、**\[Create\]** を選択します。残りのフィールドは、既定値のままにします。

4. ステップ 2 と 3 を繰り返し、**invoices-json** および **invoices-staging** という名前の 2 つの追加コンテナーを作成します。

5. 左側メニューから **\[Storage Explorer (preview)\]** を選択します。次に、階層メニューで **\[BLOB CONTAINERS\]** 項目を展開します。

6. **\[BLOB CONTAINERS\]** の下で、**\[invoices\]** コンテナーを選択し、タスクバー メニューから **\[+ New Folder\]** を選択します。
   
   ![左側メニューから \[Storage Explorer\] が選択された状態で、\[Storage Explorer (preview)\] 画面が表示されています。階層メニューで \[BLOB CONTAINERS\] 項目が展開され、請求書項目が選択されています。タスクバー メニューの \[+ New Folder\] ボタンが強調表示されています。](media/storageexplorer_invoicesnewfolder.png "Azure Storage Explorer")

7. **\[Create New Virtual Directory\]** ブレードで、ディレクトリに **Test** という名前を付け、**\[OK\]** を選択します。これにより、新しい **\[Test\]** フォルダーに自動的に移動します。
   
   ![\[Create New Virtual Directory\] フォームが表示され、\[name\] フィールドに「Test」が入力されています。](media/storageexplorer_createnewvirtualdirectoryblade.png "[Create New Virtual Directory] フォーム")

8. タスクバーから **\[Upload\]** を選択します。**Hands-on lab/artifacts/sample\_invoices/Test** にあるすべての請求書をアップロードします。ファイル名は、Invoice\_6.pdf と Invoice\_7.pdf です。

9. タスクバーの下にある \[location\] テキストボックスから **\[invoices\]** ブレッドクラムを選択して、**invoices** ルート フォルダーに戻ります。
   
   ![\[Storage Explorer\] ウィンドウの一部が、\[location\] テキストボックスから選択した \[invoices\] ブレッドクラムとともに表示されています。](media/storageexplorer_breadcrumbnav.png "[Storage Explorer] ブレッドクラムのナビゲーション")

10. タスクバーから **\[+ New Folder\]** を再び選択します。今回は、**Train** という名前のフォルダーを作成します。これにより、新しい **\[Train\]** フォルダーに自動的に移動します。

11. タスクバーから **\[Upload\]** を選択します。**Hands-on lab/artifacts/sample\_invoices/Train** にあるすべての請求書をアップロードします。これらのファイルの名前は、Invoice\_1.pdf、Invoice\_2.pdf、Invoice\_3.pdf, Invoice\_4.pdf および Invoice\_5.pdf です。

12. 左側メニューから **\[Access keys\]** を選択します。
    
    ![左側メニューが表示され、\[Access keys\] リンクが強調表示されています。](media/ex5-task1a-003.png "[Access keys] メニュー項目")

13. **\[Key1\]** の接続文字列をコピーします。その文字列をメモ帳、Visual Studio Code、またはその他のテキスト ファイルに保存します。これは何度も使用します。
    
    ![key1 接続文字列の横にある \[copy\] ボタンが選択されています。](media/ex5-task1a-004.png "key1 接続文字列値のコピー")

14. 左側メニューの **\[Settings\]** の下で、**\[Shared access signature\]** を選択します。

15. すべてのチェック ボックスがオンになっていることを確認し、**\[Generate SAS and connection string\]** を選択します。
    
    ![SAS の生成のための \[configuration\] フォームが表示されています。](media/ex5-task1a-012.png "SAS の [Configuration] フォーム")

16. 上記と同じテキスト ファイルに、生成された **Blob service SAS URL** をコピーします。
    
    ![SAS フォームが表示され、共有アクセス署名の Blob service SAS URL が強調表示されています。](media/ex5-task1a-013.png "SAS URL")

17. コピーした SAS URL を修正し、**?** 文字の直前に **invoices** コンテナー名を追加します。
    
    > **例**: https://asastore{{suffix}.blob.core.windows.net/**invoices**?sv=2019-12-12\&ss=bfqt\&srt ...

### タスク 2: Azure Forms Recognizer モデルの作成およびトレーニングと Cognitive Search のセットアップ

1. Azure Portal ホームページに移動し、**\[+ Create a resource\]** を選択し、「**Form Recognizer**」を検索し、その検索結果から **\[Form Recognizer\]** を選択します。
   
   ![\[New\] リソース画面が表示され、「Form Recognizer」が検索テキストボックスに入力され、検索結果から選択されています。](media/ex5-task2a-01.png "[New] リソース検索フォーム")

2. **\[Create\]** を選択します。
   
   ![\[Form Recognizer overview\] 画面が表示され、\[Create\] ボタンが強調表示されています。](media/ex5-task2a-02.png "[Form Recognizer overview] フォーム")

3. 以下の構成設定を入力し、**\[Create\]** を選択します。
   
   | フィールド| 値
   |----------|----------
   | Name| フォーム認識サービスに対して一意の名前 (緑のチェック マーク インジケーターによって示されます) を入力します。
   | Subscription| ラボ サブスクリプションを選択します。
   | Location| ラボ リージョンを選択します。
   | Pricing| **\[Free F0\]** を選択します。
   | \[Confirmation\] チェックボックス| オン

   ![Form Recognizer の構成画面が表示され、前述の値が入力されています。](media/ex5-task2a-03.png "Form Recognizer の構成画面")

4. サービスのプロビジョニングを待機し、リソースに移動します。

5. 左側メニューから **\[Keys and Endpoint\]** を選択します。
   
   ![左側のナビゲーションが表示され、\[Keys and Endpoint\] 項目が強調表示されています。](media/ex5-task2a-04.png "左側メニューのナビゲーション")

6. KEY 1 と ENDPOINT の両方の値をコピーして貼り付けます。以前にコピーしたストレージ接続文字列と同じ場所にこれらの値を貼り付けます。
   
   ![\[Keys and Endpoint\] 画面が表示され、KEY 1 と ENDPOINT の値が強調表示されています。](media/ex5-task2a-05.png "[Keys and Endpoint] 画面")

7. Azure Portal ホームページに移動し、**\[+ Create a new resource\]** を選択し、**Azure Cognitive Search** の新しいインスタンスを検索し、作成します。
   
   ![\[Azure Cognitive Search overview\] 画面が表示されています。](media/ex5-task1-006.png "[Azure Cognitive Search Overview] 画面")

8. このラボで使用しているサブスクリプションとリソース グループを選択します。検索に関連して、Cognitive Search Service の URL を一意の値に設定します。次に、価格レベルを **\[Free\]** に切り替えます。
   
   ![Cognitive Search の構成画面が表示され、前述のように値が入力されています。](media/ex5-task1-007.png "Cognitive Search サービスの構成")

9. \[**Review + create**\] を選択します。
   
   ![\[Review + create\] ボタンが表示されています。](media/ex5-task1-008.png "[Review and create] ボタン")

10. **\[Create\]** を選択します。

11. Search サービスのプロビジョニングを待機し、リソースに移動します。

12. 左側メニューから **\[Keys\]** を選択し、**\[Primary admin key\]** をコピーしてテキスト ドキュメントに貼り付けます。Search サービス リソースの名前もメモしてください。
    
    ![Search サービス リソースの \[Keys\] ページが表示され、\[Primary admin key\] 値が強調表示されています。](media/ex5-task3-010.png "Cognitive Search キー")

13. Search サービスの名前もテキスト ドキュメントにメモしてください。
    
    ![Search サービス名が \[Keys\] 画面で強調表示されています。](media/ex5-task3-011.png "Search サービス名")

14. Visual Studio Code を開きます。

15. **\[File\]** メニューから **\[Open file\]** を選択し、**Hands-on lab/artifacts/pocformreader.py** を開きます。

16. 以下に示す適切な値で行 7、9、および 17 を更新します。
    
    - 行 7: Azure Cognitive Services (Form Recognizer) のエンドポイント。
    
    - 行 9: Blob Service SAS URL ストレージ アカウントと Train および Test の各請求書フォルダー。
    
    - 行 17: Azure Cognitive Service (Form Recognizer) エンドポイントのキー。
    
    ![pocformreader.py のソース コード リストが表示され、前述の行が強調表示されています。](media/ex5-task2a-06.png "Pocofrmreader.py のソース リスト")

17. ファイルを保存します。

18. \[Run\]、\[Start Debugging\] の順に選択します。
    
    ![\[VS Code File\] メニューが表示され、\[Run\] が選択され、\[Start Debugging\] が強調表示されています。](media/ex5-task2a-07.png "[VS Code File] メニュー")

19. **\[Debug Configuration\]** で、**Python File - Debug the currently active Python File** 値のデバッグを選択します。
    
    ![\[Debug Configuration\] での選択が表示され、Python File - Debug the currently active Python File が強調表示されています。](media/ex5-task2a-08.png "[Debug Configuration] での選択")

20. 完了すると、以下のスクリーンショットに似ている出力が表示されます。出力には、modelID も含まれます。後で使用するために、これをコピーして、テキスト ファイルに貼り付けてください。
    
    ![Python スクリプトのサンプル出力が表示され、modelID 値が強調表示されています。](media/ex5-task2a-09.png "Visual Studio Code 出力ウィンドウ")
    
    > **注**: **requests** モジュールが見つかりませんというエラーが表示された場合は、Visual Studio Code のターミナル ウィンドウで、**pip install requests** を実行してください。

### タスク 3: Form Recognizer でのスキルセットの構成

1. Visual Studio Code の新しいインスタンスを開きます。

2. Visual Studio Code で、フォルダー **Hands-on lab/environment-setup/functions** を開きます。
   
   ![/environment-setup/functions フォルダーのファイル構造が表示されています。](media/ex5-task1-001.png "functions フォルダーのファイル構造")

3. **GetInvoiceData/\_\_init\_\_.py** ファイル内で、行 66、68、70、および 73 を、環境に適した値で更新します。置き換える必要がある値は、**\<\<** と **>>** の値の間にあります。
   
   ![__Init.py__. コードのリストが表示されています。](media/ex5-task1-step2.png "__init__.py コードのリスト")

4. Azure Functions 拡張機能を使用して、新しい Azure 関数を公開します。\[Azure Functions\] パネルが表示されない場合は、**\[View\]** メニューで、**\[Open View...\]** を選択してから **\[Azure\]** を選択します。パネルに **\[Sign-in to Azure\]** リンクが表示されたら、そのリンクを選択して、Azure にログインします。パネルの上部にある **\[Publish\]** ボタンを選択します。
   
   ![VS Code に \[Azure Functions\] 拡張機能パネルが表示され、関数を公開するボタンが強調表示されています。](media/ex5-task1-002.png "[Azure Function] パネル")
   
   - Synapse ワークスペースと同じサブスクリプションを選択します。
   
   - **\[Create new Function App in Azure...\]** を選択します。
   
   - フォーム認識に関連して、この関数に一意の名前を付けます。
     
     ![\[Create new function App in Azure\] ダイアログが表示され、名前が入力されています。](media/ex5-task1-003.png "[Create new function App in Azure] ダイアログ")
   
   - ランタイムに対して、Python 3.7 を選択します。
     
     ![Python ランタイム バージョンの選択ダイアログが表示され、Python 3.7 が強調表示されています。](media/ex5-task1-004.png "Python ランタイム バージョンの設定")
   
   - Synapse ワークスペースと同じリージョンに関数を展開します。
     
     ![リージョン選択ダイアログが表示されています。](media/ex5-task1-005.png "リージョン選択ダイアログ")

5. 公開が完了したら、Azure Portal に戻り、Azure Function App と同じ名前で作成されたリソース グループを検索します。

6. このリソース グループ内で、同じ名前の **App Service** リソースを開きます。
   
   ![リソース リストが表示され、App Service が強調表示されています。](media/formrecognizerresourcelist.png "リソース グループのリスト")

7. 左側メニューから、**\[Functions\]** という見出しの下にある **\[Functions\]** を選択します。

8. Functions リストから **\[GetInvoiceData\]** を選択します。

9. **\[GetInvoiceData\]** 画面のツールバー メニューから **\[Get Function Url\]** 項目を選択し、後で参照するためにテキスト ドキュメントにこの値をコピーします。
   
   ![\[GetInvoiceData function\] 画面が表示され、\[Get Function Url\] ボタンがタスクバーで強調表示され、URL がテキスト ボックスに表示されています。](media/azurefunctionurlvalue.png "[GetInvoiceData function] 画面")

10. 関数を公開し、すべてのリソースを作成したため、次にスキルセットを作成できます。これは、**Postman** を使用して実行できます。Postman を開きます。

11. **\[File\]** メニューで **\[Import\]** を選択し、**Hands-on lab/environment-setup/skillset** から Postman コレクションのインポートを選択します。
    
    ![Postman の \[File\] メニューが展開され、\[Import\] オプションが選択されています。](media/ex5-task3-004.png "Postman の [File] メニュー")
    
    ![Postman の \[file import\] 画面が表示され、\[Upload files\] ボタンが強調表示されています。](media/ex5-task3-005.png "Postman のインポート画面")
    
    ![ファイル選択ダイアログが表示され、skillset フォルダーにあるファイルが強調表示されています。](media/ex5-task3-006.png "ファイル選択ダイアログ")

12. \[Import\] を選択します。

13. Postman では、インポートしたコレクションによって、**Create a KnowledgeStore** コレクション内に 4 つの項目が生じます。Create Index、Create Datasource、Create the skillset、および Create the Indexer です。
    
    ![\[Collections\] ペインが表示され、\[Create a KnowledgeStore\] コレクションが展開されて、前述の 4 つの項目が表示されます。](media/ex5-task3-007.png "Postman の [Collections] ペイン")

14. 初めに、コレクション内の各呼び出しに影響を及ぼす一部のプロパティを編集する必要があります。**Create a KnowledgeStore** コレクションをポイントして、省略記号ボタン **\[...\]** を選択してから **\[Edit\]** を選択します。
    
    ![Postman で、Create a KnowledgeStore コレクションの横にある省略記号が展開され、\[Edit\] メニュー オプションが選択されています。](media/ex5-task3-008.png "Postman コレクションの編集")

15. \[Edit Collection\] 画面で、**\[Variables\]** タブを選択します。
    
    ![\[Edit Collection\] 画面で、\[Variables\] タブが選択されています。](media/ex5-task3-009.png "[Edit Collection] 変数画面")

16. 以下に合わせて、各変数を編集する必要があります。
    
    | 変数| 値
    |----------|----------
    | admin-key| 作成した検索サービスのキー
    | search-service-name| 検索サービスの名前
    | Storage account name| asastore{{suffix}}
    | storage-connection-string| asastore{{suffix}} ストレージ アカウントの接続文字列
    | datasourcename| **「invoices」** を入力
    | indexer-name| **「invoice-indexer」** を入力
    | index-name| **「invoice-index」** を入力
    | skillset-name| **「invoice-skillset」** を入力
    | storage-container-name| **「invoices」** を入力
    | skillset-function| 公開した関数の関数 URL を入力


17. **\[Update\]** を選択して、修正した値でコレクションを更新します。
    
    ![\[Edit Collection Variables\] 画面が表示され、修正した値のサンプリングが示されています。](media/ex5-task3-014.png "[Edit Collection Variables] 画面")

18. コレクションから **Create Index** の呼び出しを選択し、**\[Body\]** タブを選択して、コンテンツをレビューします。
    
    ![コレクションから Create Index の呼び出しが選択され、\[Body\] タブが強調表示されています。](media/ex5-task3-015.png "Create Index の呼び出し")

19. \[Send\] を選択します。
    
    ![Postman の \[Send\] ボタンが選択されています。](media/ex5-task3-016.png "[Send] ボタン")

20. インデックスが作成されたというレスポンスを受け取ります。
    
    ![Create Index レスポンスが Postman に表示され、201 Created のステータスが強調表示されています。](media/ex5-task3-017.png "Create Index の呼び出しのレスポンス")

21. **Create Datasource、Create the Skillset、および Create the indexer** の呼び出しに対して同じステップを実行します。

22. インデクサー リクエストの送信後に検索サービスに移動すると、インデクサーが実行中で、進行中インジケーターが表示されていることを確認できます。その実行には数分かかります。
    
    ![invoice-indexer が表示され、進行中のステータスが示されています。](media/ex5-task3-018.png "invoice-indexer のステータス")

23. インデクサーの実行が終了すると、成功したことを示す 2 つのドキュメントが表示されます。Blob ストレージ アカウント、**asastore{suffix}** に移動し、**invoices-json** コンテナー内を確認すると、.json ドキュメントが含まれている 2 つのフォルダーがあります。
    
    ![invoice-indexer の実行履歴に、成功したことが表示されています。](media/ex5-task3-019.png "invoice-indexer の実行履歴")
    
    ![Invoices-json コンテナーが、2 つのフォルダーとともに表示されています。JSON ファイルが、\[Blob\] ウィンドウに表示されています。](media/ex5-task3-020.png "Invoices-json コンテナーの内容")

### タスク 4: Synapse パイプラインの作成

1. Synapse ワークスペースを開きます。
   
   ![\[Azure Synapse Workspace resource\] 画面が表示され、\[Launch Synapse Studio\] ボタンが強調表示されています。](media/ex5-task4-001.png)

2. 左側のメニューを展開して、**\[Develop\]** 項目を選択します。**\[Develop\]** ブレードで **\[+\]** ボタンを展開して、**\[SQL script\]** 項目を選択します。
   
   ![左側メニューが展開され、\[Develop\] 項目が選択されています。\[Develop\] ブレードで \[+\] ボタンが展開され、\[SQL script\] 項目が強調表示されています。](media/develop_newsqlscript_menu.png "新しい SQL スクリプトの作成")

3. クエリ タブのツールバー メニューで、SQL プールの `SQLPool01` に接続していることを確認します。
   
   ![クエリ タブのツールバー メニューが表示され、\[Connect to\] が SQL プールに設定されています。](media/querytoolbar_connecttosqlpool.png "SQL プールへの接続")

4. 以下のクエリをコピーしてクエリ ウィンドウに貼り付けて、請求書情報テーブルを作成します。クエリ タブのツールバーで **\[Run\]** を選択します。
   
   ```sql
     CREATE TABLE [wwi_mcw].[Invoices]
     (
       [TransactionId] [uniqueidentifier]  NOT NULL,
       [CustomerId] [int]  NOT NULL,
       [ProductId] [smallint]  NOT NULL,
       [Quantity] [tinyint]  NOT NULL,
       [Price] [decimal](9,2)  NOT NULL,
       [TotalAmount] [decimal](9,2)  NOT NULL
     );
   ```

5. このクエリは保存しないので、上部のツールバーから **\[Discard all\]** を選択します。確認を求められたら **\[Discard changes\]** を選択します。
   
   ![上部のツールバー メニューが表示され、\[Discard all\] が強調表示されています。](media/toptoolbar_discardall.png "変更の破棄")

6. 左側のナビゲーションから **\[Orchestrate\]** ハブを選択します。
   
   ![左側のナビゲーションで \[Orchestrate\] ハブが選択されています。](media/ex5-task4-012.png "[Orchestrate] ハブ")

7. \[Orchestrate\] ブレードで、**\[+\]** ボタンを展開し、**\[Pipeline\]** を選択して、新しいパイプラインを作成します。
   
   ![\[+\] ボタンが展開され、\[pipelines\] オプションが選択されています。](media/ex5-task4-013.png "新しいパイプラインの作成")

8. パイプラインに **「InvoiceProcessing」** という名前を付けます。
   
   ![新しいパイプラインのプロパティが表示され、パイプラインの名前として「InvoiceProcessing」が入力されています。](media/ex5-task4-014.png "パイプラインの命名")

9. パイプライン タスクバーで **\[Add trigger\]** を選択してから **\[New/Edit\]** を選択して、パイプラインを開始するイベントを作成します。
   
   ![\[Add trigger\] ボタンが展開され、\[New/Edit\] オプションが選択されています。](media/ex5-task4-015.png "[New Trigger] メニュー項目")

10. \[Add triggers\] フォームで、**\[Choose trigger\]** ドロップダウンから **\[+New\]** を選択します。
    
    ![\[Add triggers\] フォームが表示され、\[Choose trigger\] ドロップダウンが展開され、\[+New\] 項目が選択されています。](media/ex5-task4-016.png "新しいトリガーの作成の選択")

11. この演習では、スケジュールを使用します。しかし、今後、Blob ストレージに追加された新しい JSON ファイルを起動するイベントベースのトリガーも使用できるようになります。5 分ごとに起動するようにトリガーを設定し、**\[OK\]** を選択します。
    
    ![\[new trigger\] フォームが表示され、5 分ごとに起動するようにトリガーが設定されています。](media/ex5-task4-017.png "[New trigger] フォーム")

12. \[Run Parameters\] フォームで **\[OK\]** を選択します。ここでは何も実行する必要がありません。

13. 次に、パイプラインにデータ フローを追加する必要があります。\[Activities\] の下で **\[Move \& transform\]** を展開し、デザイナー キャンバスに **\[Data flow\]** をドラッグ アンド ドロップします。
    
    ![パイプライン デザイナーが、データ フロー アクティビティのドラッグ アンド ドロップ操作のインジケーターとともに表示されています。](media/ex5-task4-018.png "データ フロー アクティビティ")

14. **\[Adding data flow\]** フォームで、**\[Create new data flow\]** を選択し、それに **「NewInvoicesProcessing」** という名前を付けます。
    
    ![\[Adding data flow\] フォームが表示され、前述の値が入力されています。](media/ex5-task4-019.png)

15. **\[NewInvoicesProcessing\]** データ フロー デザイン キャンバスで、**\[Add source\]** ボックスを選択します。
    
    ![NewInvoicesProcessing デザイナーが表示され、\[Add source\] ボックスが選択されています。](media/ex5-task4-020.png "NewInvoicesProcessing デザイナー")

16. 下側で出力ストリームに **「jsonInvoice」** という名前を付け、ソース タイプを **\[Dataset\]** のままにし、すべての他のオプションを既定値に設定されたままにします。\[Dataset\] フィールドの横にある **\[+New\]** を選択します。
    
    ![\[Source settings\] タブが表示され、「jsonInvoice」という名前が入力され、\[Dataset\] フィールドの横にある \[+New\] ボタンが選択されています。](media/ex5-task4-021.png "ソースの設定")

17. **\[New dataset\]** ブレードで、**\[Azure Blob Storage\]** を選択ししてから **\[Continue\]** を選択します。
    
    ![\[New dataset\] ブレードが表示され、\[Azure Blob Storage\] が選択されています。](media/ex5-task4-022.png "Azure Blob Storage データセット")

18. **\[Select format\]** ブレードで、**\[Json\]** を選択してから **\[Continue\]** を選択します。
    
    ![\[select format\] 画面が表示され、タイプとして \[Json\] が選択されています。](media/ex5-task4-023.png "[Select format] フォーム")

19. **\[Set properties\]** 画面で、データセットに **「InvoicesJson」** という名前を付けます。次に、\[linked service\] フィールドで、Azure Storage にリンクされたサービス **asastore{suffix}** を選択します。
    
    ![\[Set properties\] フォームの一部が表示され、前述の値が入力されています。](media/ex5-task4-024.png "データセットの [Set properties] フォーム")

20. \[file path\] フィールドに **「invoices-json」** と入力し、\[import schema\] フィールドを **\[From sample file\]** に設定します。
    
    ![\[set properties\] フォームが表示され、前述のように \[file path\] フィールドと \[import schema\] フィールドに前述の値が入力されています。](media/ex5-task4-025.png "データの [Set properties] フォーム")

21. **\[Browse\]** を選択し、**Hands-on lab/environment-setup/synapse/sampleformrecognizer.json** のファイルを選択してから **\[OK\]** を選択します。
    
    ![\[Set properties\] フォームが表示され、選択されたファイルとして sampleformrecognizer.json が選択されています。](media/ex5-task4-026.png "データの [Set properties] フォーム")

22. 下側で **\[Source options\]** タブを選択します。\[Wildcard paths\] フィールドに「\*/\*」を追加します。
    
    ![\[Source options\] タブが表示され、\[Wildcard paths\] フィールドに指定した文字が入力されています。](media/ex5-task4-048.png "[Source options] タブ")

23. データ フロー デザイナー サーフェイスで、ソース アクティビティの右下にある **\[+\]** を選択し、データ フローに別のステップを追加します。
    
    ![ソース アクティビティの右下にある \[+\] ボタンが強調表示されています。](media/ex5-task4-028.png "データ フロー ステップの追加")

24. オプションのリストから **\[Schema modifier\]** セクションの下で **Derived Column**を選択します。
    
    ![\[+\] ボタンが展開され、オプションのリストから Derived 列が選択されています。](media/ex5-task4-029.png "Derived 列のアクティビティの追加")

25. **\[Derived column's settings\]** タブで、出力ストリーム名として **\[RemoveCharFromStrings\]** を指定します。次に、\[Columns\] フィールドで、3 つの列を追加し、以下のように構成します。
    
    | 列| 式
    |----------|----------
    | productprice| toDecimal(replace(productprice,'$',''))
    | totalcharges| toDecimal(replace(replace(totalcharges,'$',''),',',''))
    | quantity| toInteger(replace(quantity,',',''))

    ![Derived 列の \[settings\] タブが表示され、前述のようにフィールドに前述の値が入力されています。](media/ex5-task4-030.png "Derived 列の [settings] タブ")

26. データ フロー デザイナーに戻り、derived columnのアクティビティの横にある **\[+\]** を選択して、データ フローに別のステップを追加します。

27. 今回は、**\[Row modifier\]** セクションの下で **\[Alter Row\]** を選択します。
    
    ![\[Row modifier\] セクションで、\[Alter Row\] オプションが選択されています。](media/ex5-task4-031.png "[Alter row] アクティビティ")

28. 下側の **\[Alter row settings\]** タブで、出力ストリームに **「AlterTransactionID」**という名前を付け、着信ストリームの設定は既定値のままにします。**\[Alter row conditions\]** フィールドを **\[Upsert If\]** に変更し、式を **「notEquals(transactionid,"")」** に設定します。
    
    ![\[Alter row settings\] タブが表示され、前述の値が入力されています。](media/ex5-task4-032.png "[Alter row settings] タブ")

29. データ フロー デザイナーに戻り、**\[**Alter Row**\]** アクティビティの右下にある **\[+\]** を選択し、データ フローに別のステップを追加します。

30. **\[Destination\]** セクション内で **\[Sink\]** を選択します。
    
    ![アクティビティ リストで、\[Destination\] セクション内の \[Sink\] オプションが選択されています。](media/ex5-task4-033.png "シンク アクティビティ")

31. 下側で **\[Sink\]** タブを選択し、出力ストリーム名に **「SQLDatabase」**という名前を付け、他のすべての設定は既定値のままにします。**\[Dataset\]** フィールドの横にある **\[+New\]** を選択して、新しいデータセットを追加します。
    
    ![\[sink\] タブが表示され、出力ストリーム名が「SQLDatabase」に設定され、\[Dataset\] フィールドの横にある \[+New\] ボタンが選択されています。](media/ex5-task4-034.png "[Sink] タブ")

32. **\[New dataset\]** ブレードで **\[Azure\]** タブを選択します。**\[Azure Synapse Analytics\] (旧称 SQL DW)** を選択してから **\[Continue\]** を選択します。
    
    ![データセット タイプのリストで \[Azure Synapse Analytics\] が選択されています。](media/ex5-task4-035.png "[Azure Synapse Analytics] データセット タイプの選択")

33. データセットの名前を **「InvoiceTable」**に設定し、リンクされたサービス **sqlpool01** を選択します。**\[Select from existing table\]** を選択してから **wwi\_mcw.Invoices** テーブルを選択します。テーブル名のリストにこのテーブルが表示されない場合は、**\[Refresh\]** ボタンを選択すると表示されます。**\[OK\]** を選択します。
    
    ![データセットの \[Set properties\] フォームが表示され、前述のように値が入力されています。](media/ex5-task4-036.png "[Set properties] フォーム")

34. 下側のデータ フロー デザイナーでシンク アクティビティを選択し、**\[Settings\]** タブを選択して **\[Allow upsert\]** ボックスをオンにします。**\[Key columns\]** フィールドを **\[transactionid\]** に設定します。
    
    ![シンク アクティビティの \[Settings\] タブが表示され、前述のように値が入力されています。](media/ex5-task4-037.png "シンクの [Settings] タブ")

35. **\[Mapping\]** タブを選択し、**\[Auto mapping\]** 設定を無効にし、json ファイルとデータベース間のマッピングを構成します。**\[+ Add mapping\]** を選択してから **\[Fixed mapping\]** を選択して、以下のマッピングを追加します。もし既存のものがあり警告が表示されている場合は、いったん既存のマッピングを削除してから作り直すとうまくいく場合があります。
    
    | 入力列| 出力列
    |----------|----------
    | transactionid| TransactionId
    | productid| ProductId
    | customerid| CustomerId
    | productprice| Price
    | quantity| Quantity
    | totalcharges| TotalAmount

    ![\[Mapping\] タブが表示され、\[Auto Mapping\] が無効になり、前述の表の列マッピングが定義されています。](media/ex5-task4-038.png "[Mapping] タブ")

36. ワークスペースの上部にあるタブを選択して、**\[InvoiceProcessing\]** パイプラインに戻ります。
    
    ![ワークスペースの上部で \[InvoiceProcessing\] タブが選択されています。](media/ex5-task4-039.png "[InvoiceProcessing] パイプライン タブ")

37. パイプライン デザイナー サーフェイスでデータ フロー アクティビティを選択し、下側で **\[Settings\]** タブを選択します。
    
    ![データ フロー アクティビティの \[Settings\] タブが表示されています。](media/ex5-task4-040.png "[Settings] タブ")

38. **\[PolyBase\]** 設定の下で、**\[Staging linked service\]** をリンクされたサービス **asastore{suffix}** に設定します。**Storage staging フォルダー**として **「invoices-staging」** と入力します。
    
    ![データ フロー アクティビティの \[Settings\] タブが表示され、前述のようにそのフォームに値が入力されています。](media/ex5-task4-041.png "[Settings] タブ")

39. 上部のツールバーで \[**Publish All**\] を選択します。
    
    ![上部のツールバーで \[Publish All\] ボタンが選択されています。](media/ex5-task4-042.png "[Publish all] ボタン")

40. **\[Publish\]** を選択します。

41. 数分以内に、公開が完了したことを示す通知が表示されます。
    
    ![公開完了通知が表示されています。](media/ex5-task4-043.png "公開完了通知")

42. 左側メニューから **\[Monitor\]** ハブを選択し、ハブ メニューから **\[Pipeline runs\]** オプションを確実に選択します。
    
    ![左側メニューで \[Monitor\] ハブが選択されています。](media/ex5-task4-044.png "[Monitor] ハブ メニューのオプション")

43. 約 5 分で、**InvoiceProcessing** パイプライン処理が開始されます。このリストを表示するために、更新が必要になることがあります。更新ボタンはツールバーにあります。
    
    ![パイプライン実行リストで、InvoiceProcessing パイプラインが実行中として表示されています。](media/ex5-task4-045.png "パイプライン実行リスト")

44. これは約 3 ～ 4 分後に完了します。パイプラインの完了を確認するために、リストの更新が必要になることがあります。
    
    ![パイプライン実行リストが表示され、InvoiceProcessing パイプラインが成功したことが示されています。](media/ex5-task4-046.png "パイプライン実行リスト")

45. 左側メニューから **\[Develop\]** ハブを選択し、**\[+\]** ボタンを展開して **\[SQL Script\]** を選択します。適切なデータベースを確実に選択し、以下のクエリを実行して、2 つのテスト請求書からのデータを検証してください。
    
    ```SQL
    SELECT * FROM wwi_mcw.Invoices
    ```
    
    ![データベース内のデータの表示](media/ex5-task4-047.png)

## 演習 6: セキュリティ

**所要時間**: 30 分

### タスク 1: 列レベルのセキュリティ

機密情報を保持するデータ列を特定することは重要です。機密情報の種類には、社会保障番号、電子メール アドレス、クレジット カード番号、財務合計などがあります。Azure Synapse Analytics では、特定の列に対するユーザーまたはロールの select 権限を阻止するアクセス許可を定義できます。

1. 左側メニューから **\[Develop\]** を選択し、**\[Develop\]** ブレードで **\[+\]** を展開して **\[SQL script\]** を選択することによって、新しい SQL スクリプトを作成します。

2. 以下のクエリをコピーしてクエリ ウィンドウに貼り付けます。クエリ ウィンドウで各コメント ブロック間のすべてのクエリを強調表示して、クエリ ウィンドウのツールバー メニューで **\[Run\]** を選択することによって、各ステートメント グループを実行します。クエリは、インラインで記述されています。クエリを実行する場合は、**SQLPool01** に確実に接続してください。
   
   ```sql
       /*  Column-level security feature in Azure Synapse simplifies the design and coding of security in applications.
       It ensures column level security by restricting column access to protect sensitive data. */
   
   /* Scenario: In this scenario we will be working with two users. The first one is the CEO, he has access to all
       data. The second one is DataAnalystMiami, this user doesn't have access to the confidential Revenue column
       in the CampaignAnalytics table. Follow this lab, one step at a time to see how Column-level security removes access to the
       Revenue column to DataAnalystMiami */
   
   --Step 1: Let us see how this feature in Azure Synapse works. Before that let us have a look at the Campaign Analytics table.
   select  Top 100 * from wwi_mcw.CampaignAnalytics
   where City is not null and state is not null
   
   /*  Consider a scenario where there are two users.
       A CEO, who is an authorized  personnel with access to all the information in the database
       and a Data Analyst, to whom only required information should be presented.*/
   
   -- Step:2 Verify the existence of the “CEO” and “DataAnalystMiami” users in the Datawarehouse.
   SELECT Name as [User1] FROM sys.sysusers WHERE name = N'CEO';
   SELECT Name as [User2] FROM sys.sysusers WHERE name = N'DataAnalystMiami';
   
   
   -- Step:3 Now let us enforcing column level security for the DataAnalystMiami.
   /*  The CampaignAnalytics table in the warehouse has information like ProductID, Analyst, CampaignName, Quantity, Region, State, City, RevenueTarget and Revenue.
       The Revenue generated from every campaign is classified and should be hidden from DataAnalystMiami.
   */
   
   REVOKE SELECT ON wwi_mcw.CampaignAnalytics FROM DataAnalystMiami;
   GRANT SELECT ON wwi_mcw.CampaignAnalytics([Analyst], [CampaignName], [Region], [State], [City], [RevenueTarget]) TO DataAnalystMiami;
   -- This provides DataAnalystMiami access to all the columns of the Sale table but Revenue.
   
   -- Step:4 Then, to check if the security has been enforced, we execute the following query with current User As 'DataAnalystMiami', this will result in an error
   --  since DataAnalystMiami doesn't have select access to the Revenue column
   EXECUTE AS USER ='DataAnalystMiami';
   select TOP 100 * from wwi_mcw.CampaignAnalytics;
   ---
   -- The following query will succeed since we are not including the Revenue column in the query.
   EXECUTE AS USER ='DataAnalystMiami';
   select [Analyst],[CampaignName], [Region], [State], [City], [RevenueTarget] from wwi_mcw.CampaignAnalytics;
   
   -- Step:5 Whereas, the CEO of the company should be authorized with all the information present in the warehouse.To do so, we execute the following query.
   Revert;
   GRANT SELECT ON wwi_mcw.CampaignAnalytics TO CEO;  --Full access to all columns.
   
   -- Step:6 Let us check if our CEO user can see all the information that is present. Assign Current User As 'CEO' and the execute the query
   EXECUTE AS USER ='CEO'
   select * from wwi_mcw.CampaignAnalytics
   Revert;
   ```
   
   ![クエリ タブのツールバーが表示され、\[Run\] が選択されています。](media/querytoolbar_run.png "SQL クエリの実行")

3. このクエリは保存しないので、上部のツールバーから **\[Discard all\]** を選択します。確認を求められたら **\[Discard changes\]** を選択します。
   
   ![上部のツールバー メニューが表示され、\[Discard all\] が強調表示されています。](media/toptoolbar_discardall.png "変更の破棄")

### タスク 2: 行レベルのセキュリティ

多くの組織では、ユーザー別に特定のデータ行をフィルターすることが重要です。WWI は、データ アナリストに、各自のデータのみが表示されるようにしたいと考えています。キャンペーン分析テーブルには、各データ行が属するアナリストを示す Analyst 列があります。以前は、組織はアナリストごとのビューを作成していましたが、作業量が多く、不要なオーバーヘッドになっていました。Azure Synapse Analytics を使用すると、クエリを実行したユーザーを Analyst 列と比較して、そのユーザーに属するデータのみが表示されるようにデータをフィルターする、行レベルのセキュリティを定義できます。

1. 左側メニューから **\[Develop\]** を選択し、**\[Develop\]** ブレードで **\[+\]** を展開して **\[SQL script\]** を選択することによって、新しい SQL スクリプトを作成します。

2. 以下のクエリをコピーしてクエリ ウィンドウに貼り付けます。クエリ ウィンドウで各コメントブロック間のすべてのクエリを強調表示して、クエリ ウィンドウのツールバー メニューで **\[Run\]** を選択することによって、各ステートメント グループを実行します。クエリは、インラインで記述されています。
   
   ```sql
   /* Row level Security (RLS) in Azure Synapse enables us to use group membership to control access to rows in a table.
   Azure Synapse applies the access restriction every time the data access is attempted from any user.
   Let see how we can implement row level security in Azure Synapse.*/
   
   -- Row-Level Security (RLS), 1: Filter predicates
   -- Step:1 The Sale table has two Analyst values: DataAnalystMiami and DataAnalystSanDiego.
   --     Each analyst has jurisdiction across a specific Region. DataAnalystMiami on the South East Region
   --      and DataAnalystSanDiego on the Far West region.
   SELECT DISTINCT Analyst, Region FROM wwi_mcw.CampaignAnalytics order by Analyst ;
   
   /* Scenario: WWI requires that an Analyst only see the data for their own data from their own region. The CEO should see ALL data.
       In the Sale table, there is an Analyst column that we can use to filter data to a specific Analyst value. */
   
   /* We will define this filter using what is called a Security Predicate. This is an inline table-valued function that allows
       us to evaluate additional logic, in this case determining if the Analyst executing the query is the same as the Analyst
       specified in the Analyst column in the row. The function returns 1 (will return the row) when a row in the Analyst column is the same as the user executing the query (@Analyst = USER_NAME()) or if the user executing the query is the CEO user (USER_NAME() = 'CEO')
       whom has access to all data.
   */
   
   -- Review any existing security predicates in the database
   SELECT * FROM sys.security_predicates
   
   --Step:2 Create a new Schema to hold the security predicate, then define the predicate function. It returns 1 (or True) when
   --  a row should be returned in the parent query.
   GO
   CREATE SCHEMA Security
   GO
   CREATE FUNCTION Security.fn_securitypredicate(@Analyst AS sysname)  
       RETURNS TABLE  
   WITH SCHEMABINDING  
   AS  
       RETURN SELECT 1 AS fn_securitypredicate_result
       WHERE @Analyst = USER_NAME() OR USER_NAME() = 'CEO'
   GO
   -- Now we define security policy that adds the filter predicate to the Sale table. This will filter rows based on their login name.
   CREATE SECURITY POLICY SalesFilter  
   ADD FILTER PREDICATE Security.fn_securitypredicate(Analyst)
   ON wwi_mcw.CampaignAnalytics
   WITH (STATE = ON);
   
   ------ Allow SELECT permissions to the Sale Table.------
   GRANT SELECT ON wwi_mcw.CampaignAnalytics TO CEO, DataAnalystMiami, DataAnalystSanDiego;
   
   -- Step:3 Let us now test the filtering predicate, by selecting data from the Sale table as 'DataAnalystMiami' user.
   EXECUTE AS USER = 'DataAnalystMiami'
   SELECT * FROM wwi_mcw.CampaignAnalytics;
   revert;
   -- As we can see, the query has returned rows here Login name is DataAnalystMiami
   
   -- Step:4 Let us test the same for  'DataAnalystSanDiego' user.
   EXECUTE AS USER = 'DataAnalystSanDiego';
   SELECT * FROM wwi_mcw.CampaignAnalytics;
   revert;
   -- RLS is working indeed.
   
   -- Step:5 The CEO should be able to see all rows in the table.
   EXECUTE AS USER = 'CEO';  
   SELECT * FROM wwi_mcw.CampaignAnalytics;
   revert;
   -- And he can.
   
   --Step:6 To disable the security policy we just created above, we execute the following.
   ALTER SECURITY POLICY SalesFilter  
   WITH (STATE = OFF);
   
   DROP SECURITY POLICY SalesFilter;
   DROP FUNCTION Security.fn_securitypredicate;
   DROP SCHEMA Security;
   ```
   
   ![クエリ タブのツールバーが表示され、\[Run\] が選択されています。](media/querytoolbar_run.png "クエリの実行")

3. このクエリは保存しないので、上部のツールバーから **\[Discard all\]** を選択します。確認を求められたら **\[Discard changes\]** を選択します。
   
   ![上部のツールバー メニューが表示され、\[Discard all\] が強調表示されています。](media/toptoolbar_discardall.png "変更の破棄")

### タスク 3: 動的データ マスク

SQL 管理者は、列レベルのセキュリティの代用として、機密データをマスクするオプションも使用できます。この場合、クエリで返されたデータが難読化されます。しかし、テーブル自体には、データが元の状態のままで保存されています。SQL 管理者は、このデータを表示するアクセス許可を持つユーザーに、マスク解除権限を付与できます。

1. 左側メニューから **\[Develop\]** を選択し、**\[Develop\]** ブレードで **\[+\]** を展開して **\[SQL script\]** を選択することによって、新しい SQL スクリプトを作成します。

2. 以下のクエリをコピーしてクエリ ウィンドウに貼り付けます。クエリ ウィンドウで各コメントブロック間のすべてのクエリを強調表示して、クエリ ウィンドウのツールバー メニューで **\[Run\]** を選択することによって、各ステートメント グループを実行します。クエリは、インラインで記述されています。
   
   ```sql
   ----- Dynamic Data Masking (DDM) ---------
   /*  Dynamic data masking helps prevent unauthorized access to sensitive data by enabling customers
       to designate how much of the sensitive data to reveal with minimal impact on the application layer.
       Let see how */
   
   /* Scenario: WWI has identified sensitive information in the CustomerInfo table. They would like us to
       obfuscate the CreditCard and Email columns of the CustomerInfo table to DataAnalysts */
   
   -- Step:1 Let's first get a view of CustomerInfo table.
   SELECT TOP (100) * FROM wwi_mcw.CustomerInfo;
   
   -- Step:2 Let's confirm that there are no Dynamic Data Masking (DDM) applied on columns.
   SELECT c.name, tbl.name as table_name, c.is_masked, c.masking_function  
   FROM sys.masked_columns AS c  
   JOIN sys.tables AS tbl
       ON c.[object_id] = tbl.[object_id]  
   WHERE is_masked = 1
       AND tbl.name = 'CustomerInfo';
   -- No results returned verify that no data masking has been done yet.
   
   -- Step:3 Now let's mask 'CreditCard' and 'Email' Column of 'CustomerInfo' table.
   ALTER TABLE wwi_mcw.CustomerInfo  
   ALTER COLUMN [CreditCard] ADD MASKED WITH (FUNCTION = 'partial(0,"XXXX-XXXX-XXXX-",4)');
   GO
   ALTER TABLE wwi_mcw.CustomerInfo
   ALTER COLUMN Email ADD MASKED WITH (FUNCTION = 'email()');
   GO
   -- The columns are successfully masked.
   
   -- Step:4 Let's see Dynamic Data Masking (DDM) applied on the two columns.
   SELECT c.name, tbl.name as table_name, c.is_masked, c.masking_function  
   FROM sys.masked_columns AS c  
   JOIN sys.tables AS tbl
       ON c.[object_id] = tbl.[object_id]  
   WHERE is_masked = 1
       AND tbl.name ='CustomerInfo';
   
   -- Step:5 Now, let's grant SELECT permission to 'DataAnalystMiami' on the 'CustomerInfo' table.
   GRANT SELECT ON wwi_mcw.CustomerInfo TO DataAnalystMiami;  
   
   -- Step:6 Logged in as  'DataAnalystMiami' let's execute the select query and view the result.
   EXECUTE AS USER = 'DataAnalystMiami';  
   SELECT * FROM wwi_mcw.CustomerInfo;
   
   -- Step:7 Let's remove the data masking using UNMASK permission
   GRANT UNMASK TO DataAnalystMiami;
   EXECUTE AS USER = 'DataAnalystMiami';  
   SELECT *
   FROM wwi_mcw.CustomerInfo;
   revert;
   REVOKE UNMASK TO DataAnalystMiami;  
   
   ----step:8 Reverting all the changes back to as it was.
   ALTER TABLE wwi_mcw.CustomerInfo
   ALTER COLUMN CreditCard DROP MASKED;
   GO
   ALTER TABLE wwi_mcw.CustomerInfo
   ALTER COLUMN Email DROP MASKED;
   GO
   ```
   
   ![クエリ タブのツールバーが表示され、\[Run\] が選択されています。](media/querytoolbar_run.png "クエリの実行")

3. このクエリは保存しないので、上部のツールバーから **\[Discard all\]** を選択します。確認を求められたら **\[Discard changes\]** を選択します。
   
   ![上部のツールバー メニューが表示され、\[Discard all\] が強調表示されています。](media/toptoolbar_discardall.png "変更の破棄")

## 演習 7: 機械学習

**所要時間**: 60 分

Azure Synapse Analytics を使用すると、データ サイエンティストは機械学習モデルを作成し、展開するために、別のツールを使用する必要がなくなります。

この演習では、複数の機械学習モデルを作成します。ノートブックでこれらのモデルを利用する方法についても学習します。また、Azure Synapse Analytics ワークスペースを離れる必要なく、Web サービスとして Azure Container Instance にモデルを展開し、そのサービスを利用します。

### タスク 1: モデルのトレーニング、利用、および展開

1. **\[ASAMCW - Exercise 7 - Machine Learning\]** ノートブックを開きます (左側メニューから **\[Develop\]** を選択して、**\[Develop\]** メニューの **\[Notebooks\]** セクションを展開してノートブックを選択します)。

2. ノートブックを段階的に実行 (\[`RUN ALL`\] を選択しないでください) して、この演習を完了します。この後で実行する最も重要なタスクの一部を以下に示します。

- 探索的データ分析 (基本的統計データ)
- PCA による次元縮退
- ツリーによる分類子群のトレーニング (XGBoost を使用)
- Auto ML による分類子のトレーニング
- 最適な実行モデルの登録
- Web サービスとしてモデルを Azure Container Instances に展開
- サンプル データに基づいて予測を行うための Web サービスの利用

> **注**: これらのタスクはそれぞれ、ノートブックの複数のセルを通じて対処されることに注意してください。

## 演習 8: 監視

**所要時間**: 45 分

Azure Synapse Analytics は、Azure Portal 内で充実した監視エクスペリエンスを提供して、データ ウェアハウスのワークロードに関する洞察を明らかにします。

\[Monitor\] ハブの SQL 要求領域を使用して、アクティブな SQL 要求を監視できます。監視内容には、プール、送信者、所要時間、キューに入れられている時間、割り当てられているワークロード グループ、重要度、要求コンテンツなどの詳細が含まれます。

パイプラインの実行は、\[Monitor\] ハブでパイプラインの実行を選択することで監視できます。そこで、特定のパイプラインの実行に関連付けられているアクティビティの実行を表示するために複数のパイプラインの実行をフィルターして掘り下げることや、進行中のパイプラインの実行を監視することができます。

### タスク 1: ワークロードの重要度

混合ワークロードを実行すると、ビジー状態のシステムでリソースの問題が発生する可能性があります。ソリューション アーキテクトは、従来のデータ ウェアハウス アクティビティ (データの読み込み、変換、クエリなど) を分離して、SLA の準拠に十分なリソースが確保されるようにするための方法を模索しています。

Azure Synapse の Synapse SQL プール ワークロード管理は、ワークロードの分類、ワークロードの重要度、およびワークロードの分離の 3 つの上位概念で構成されています。これらの機能により、ワークロードによるシステム リソースの活用方法をより細かく制御できます。

ワークロードの重要度は、要求がリソースにアクセスする順序に影響します。ビジー状態のシステムでは、重要度の高い要求がリソースに最初にアクセスします。重要度によって、ロックへの順次アクセスも保証されます。

Azure Synapse の Synapse SQL で重要度を設定すると、クエリのスケジュール設定に影響を与えることができます。重要度の高いクエリが、重要度の低いクエリよりも先に実行されるようスケジュールされます。重要度をクエリに割り当てるには、ワークロード分類子を作成する必要があります。

1. **\[Develop\]** ハブに移動します。
   
   ![\[Develop\] メニュー項目が強調表示されています。](media/develop-hub.png "[Develop] ハブ")

2. **\[Develop\]** メニューから \[+\] を選択して、コンテキスト メニューから **\[SQL Script\]** を選択します。
   
   ![\[SQL script\] コンテキスト メニュー項目が強調表示されています。](media/synapse-studio-new-sql-script.png "新しい SQL スクリプト")

3. ツールバー メニューで、クエリを実行する **SQL Pool** データベースに接続します。
   
   ![クエリのツールバーで \[connect to\] オプションが強調表示されています。](media/synapse-studio-query-toolbar-connect.png "クエリのツールバー")

4. クエリ ウィンドウでスクリプトを以下のテキストで置き換えて、組織の CEO を表す `asa.sql.workload01` またはプロジェクトに取り組んでいるデータ アナリストを表す `asa.sql.workload02` としてログインしているユーザーが現在実行しているクエリが存在しないことを確認します。
   
   ```sql
   --First, let's confirm that there are no queries currently being run by users logged in as CEONYC or AnalystNYC.
   
   SELECT s.login_name, r.[Status], r.Importance, submit_time,
   start_time ,s.session_id FROM sys.dm_pdw_exec_sessions s
   JOIN sys.dm_pdw_exec_requests r ON s.session_id = r.session_id
   WHERE s.login_name IN ('asa.sql.workload01','asa.sql.workload02') and Importance
   is not NULL AND r.[status] in ('Running','Suspended')
   --and submit_time>dateadd(minute,-2,getdate())
   ORDER BY submit_time ,s.login_name
   ```

5. ツールバー メニューから **\[Run\]** を選択して SQL コマンドを実行します。
   
   ![クエリのツールバーで \[run\] が強調表示されています。](media/synapse-studio-query-toolbar-run.png "Run")

6. 次に、システムで大量にクエリを実行して、`asa.sql.workload01` と `asa.sql.workload02` に何が起こるかを確認します。そのために、多数のクエリを実行する Azure Synapse パイプラインを実行します。

7. \[`Orchestrate`\] タブを選択します。

8. **\[Exercise 8 - Execute Data Analyst and CEO Queries\]** パイプラインを実行します。このパイプラインは、`asa.sql.workload01` と `asa.sql.workload02` のクエリを実行します。統合ランタイムのインスタンスを実行している場合、デバッグ オプション付きでパイプラインを実行できます。

9. **\[Add trigger\]**、**\[Trigger now\]** の順に選択します。表示されるダイアログで **\[OK\]** を選択します。**このパイプラインを 30 秒から 1 分間実行し、次のステップに進みます**。
   
   ![\[add trigger\] メニュー項目と \[trigger now\] メニュー項目が強調表示されています。](media/trigger-data-analyst-and-ceo-queries-pipeline.png "Add trigger")

10. 左側メニューから **\[Monitor\]** ハブを選択します。進行中のパイプラインのリンクをポイントし、表示される **\[Cancel recursive\]** アイコンを選択します。
    
    ![\[Monitor Hub\] アイコンが左側メニューから選択され、\[Cancel recursive\] ボタンが進行中のパイプラインで選択されています。](media/cancel_running_pipeline_monitor_hub.png)

11. 左側メニューから **\[Develop\]** ハブを選択し、SQL スクリプトに戻ります。システムで大量に動作しているすべてのクエリに何が起きているかを確認してみましょう。クエリ ウィンドウのスクリプトを以下のテキストで置き換えます。
    
    ```sql
    SELECT s.login_name, r.[Status], r.Importance, submit_time, start_time ,s.session_id FROM sys.dm_pdw_exec_sessions s
    JOIN sys.dm_pdw_exec_requests r ON s.session_id = r.session_id
    WHERE s.login_name IN ('asa.sql.workload01','asa.sql.workload02') and Importance
    is not NULL AND r.[status] in ('Running','Suspended') and submit_time>dateadd(minute,-4,getdate())
    ORDER BY submit_time ,status
    ```

12. ツールバー メニューから **\[Run\]** を選択して SQL コマンドを実行します。以下のような出力が表示されます。
    
    ![SQL クエリの結果。](media/sql-query-2-results.png "SQL スクリプト")

13. すべてのクエリが実行され、結果が返されなくなるまで、前述のクエリを断続的に実行します。

14. **ワークロードの重要度**機能を実装して、`asa.sql.workload01` ユーザーのクエリの優先度を設定します。クエリ ウィンドウのスクリプトを以下のテキストで置き換えます。
    
    ```sql
    IF EXISTS (SELECT * FROM sys.workload_management_workload_classifiers WHERE name = 'CEO')
    BEGIN
        DROP WORKLOAD CLASSIFIER CEO;
    END
    CREATE WORKLOAD CLASSIFIER CEO
      WITH (WORKLOAD_GROUP = 'largerc'
      ,MEMBERNAME = 'asa.sql.workload01',IMPORTANCE = High);
    ```

15. ツールバー メニューから **\[Run\]** を選択して SQL コマンドを実行します。

16. 再度システムで大量にクエリを実行して、`asa.sql.workload01` と `asa.sql.workload02` のクエリに今度は何が起こるかを確認します。そのために、多数のクエリを実行する Azure Synapse パイプラインを実行します。**前回と同様に、このパイプラインを約 30 秒から 1 分間実行します**。
    
    - \[`Orchestrate`\] タブを**選択**します。
    
    - **\[Run\]** を選択して **\[Exercise 8 - Execute Data Analyst and CEO Queries\]** パイプラインを実行します。このパイプラインは、`asa.sql.workload01` と `asa.sql.workload02` のクエリを実行します。

17. クエリ ウィンドウのスクリプトを以下のテキストで置き換えて、`asa.sql.workload01` のクエリに今度は何が起きるかを確認します。
    
    ```sql
    SELECT s.login_name, r.[Status], r.Importance, submit_time, start_time ,s.session_id FROM sys.dm_pdw_exec_sessions s
    JOIN sys.dm_pdw_exec_requests r ON s.session_id = r.session_id
    WHERE s.login_name IN ('asa.sql.workload01','asa.sql.workload02') and Importance
    is not NULL AND r.[status] in ('Running','Suspended') and submit_time>dateadd(minute,-2,getdate())
    ORDER BY submit_time ,status desc
    ```

18. ツールバー メニューから **\[Run\]** を選択して SQL コマンドを実行します。以下のような出力が表示されます。`asa.sql.workload01` ユーザーのクエリ実行の重要度が **\[high\]** になっています。‘asa.sql.workload02’ クエリは、優先度の高いクエリが実行されている間、**Suspended** ステータスになることにも注意してください。
    
    ![Asa.sql.workload02 からのクエリよりも重要性の高い asa.sql.workload01 クエリを表示している SQL クエリ結果。](media/sql-query-4-results.png "SQL スクリプト")

### タスク 2: ワークロードの分離

ワークロードの分離とは、リソースがワークロード グループ専用で予約されることを意味します。ワークロード グループは、一連の要求のコンテナーであり、ワークロードの分離などのワークロードの管理をシステム上で構成するための基礎となります。単純なワークロード管理構成では、データの読み込みとユーザー クエリを管理できます。

ワークロードの分離がされない場合、要求はリソースの共有プールで動作します。共有プール内のリソースへのアクセスは保証されず、重要度基準で割り当てられます。

ワークロード グループにアクティブな要求がない場合でもワークロード グループにはリソースが割り当てられるため、ワークロードの分離の構成は慎重に行う必要があります。必要以上に分離するよう構成すると、システム全体の使用率が低下する可能性があります。

100% のワークロードの分離を構成するワークロード管理ソリューションは使用しないでください。100% の分離は、すべてのワークロード グループで構成されている `min_percentage_resource` の合計が 100% である状態です。この種類の構成は非常に限定的で厳格であり、誤って分類されたリソース要求を扱う余裕がほとんどなくなってしまいます。分離用に構成されていないワークロード グループから要求を 1 つ実行することを許可するプロビジョニングがあります。

1. **\[Develop\]** ハブに移動します。
   
   ![\[Develop\] メニュー項目が強調表示されています。](media/develop-hub.png "[Develop] ハブ")

2. **\[Develop\]** メニューから \[+\] を選択して、コンテキスト メニューから **\[SQL Script\]** を選択します。
   
   ![\[SQL script\] コンテキスト メニュー項目が強調表示されています。](media/synapse-studio-new-sql-script.png "新しい SQL スクリプト")

3. ツールバー メニューで、クエリを実行する **SQL Pool** データベースに接続します。
   
   ![クエリのツールバーで \[connect to\] オプションが強調表示されています。](media/synapse-studio-query-toolbar-connect.png "クエリのツールバー")

4. クエリ ウィンドウのスクリプトを以下のテキストで置き換えます。
   
   ```sql
   IF NOT EXISTS (SELECT * FROM sys.workload_management_workload_groups where name = 'CEODemo')
   BEGIN
       Create WORKLOAD GROUP CEODemo WITH  
       ( MIN_PERCENTAGE_RESOURCE = 50        -- integer value
       ,REQUEST_MIN_RESOURCE_GRANT_PERCENT = 25 --  
       ,CAP_PERCENTAGE_RESOURCE = 100
       )
   END
   ```
   
   このコードは、`CEODemo` という名前のワークロード グループを作成して、このワークロード グループ専用にリソースを予約します。この例では、`MIN_PERCENTAGE_RESOURCE` が 50%、`REQUEST_MIN_RESOURCE_GRANT_PERCENT` が 25% に設定されているワークロード グループは同時クエリが 2 であることが保証されます。

5. ツールバー メニューから **\[Run\]** を選択して SQL コマンドを実行します。

6. クエリ ウィンドウのスクリプトを以下のテキストで置き換えて、受信要求にワークロード グループと重要度を割り当てる `CEODreamDemo` という名前のワークロード分類子を作成します。
   
   ```sql
   IF NOT EXISTS (SELECT * FROM sys.workload_management_workload_classifiers where  name = 'CEODreamDemo')
   BEGIN
       Create Workload Classifier CEODreamDemo with
       ( Workload_Group ='CEODemo',MemberName='asa.sql.workload02',IMPORTANCE = BELOW_NORMAL);
   END
   ```

7. ツールバー メニューから **\[Run\]** を選択して SQL コマンドを実行します。

8. クエリ ウィンドウのスクリプトを以下のテキストで置き換えて、`asa.sql.workload02` が実行しているアクティブなクエリが存在しないことを確認します。
   
   ```sql
   SELECT s.login_name, r.[Status], r.Importance, submit_time,
   start_time ,s.session_id FROM sys.dm_pdw_exec_sessions s
   JOIN sys.dm_pdw_exec_requests r ON s.session_id = r.session_id
   WHERE s.login_name IN ('asa.sql.workload02') and Importance
   is not NULL AND r.[status] in ('Running','Suspended')
   ORDER BY submit_time, status
   ```

9. システムで大量にクエリを実行して、`asa.sql.workload02` に何が起こるかを確認してみましょう。そのために、多数のクエリを実行する Azure Synapse パイプラインを実行します。\[`Orchestrate`\] タブを選択します。**\[Run\]** を選択して **\[Exercise 8 - Execute Business Analyst Queries\]** パイプラインを実行します。このパイプラインは、`asa.sql.workload02` のクエリを実行します。**このパイプラインを 30 秒から 1 分間実行し、実行を再帰的にキャンセルします**。

10. クエリ ウィンドウのスクリプトを以下のテキストで置き換えて、システムで大量に動作していたすべての `asa.sql.workload02` クエリに何が起きるかを確認します。
    
    ```sql
    SELECT s.login_name, r.[Status], r.Importance, submit_time,
    start_time ,s.session_id FROM sys.dm_pdw_exec_sessions s
    JOIN sys.dm_pdw_exec_requests r ON s.session_id = r.session_id
    WHERE s.login_name IN ('asa.sql.workload02') and Importance
    is not NULL AND r.[status] in ('Running','Suspended')
    ORDER BY submit_time, status
    ```

11. ツールバー メニューから **\[Run\]** を選択して SQL コマンドを実行します。以下のような出力が表示されます。これは、各セッションの重要度が `below_normal` に設定され、2 つのクエリが並列に実行されていることを示しています。
    
    ![スクリプトの結果で、各セッションが通常以下の重要度で実行され、2 つのクエリが並列に実行されていることが示されています。](media/sql-result-below-normal.png "SQL スクリプト")

12. クエリ ウィンドウのスクリプトを以下のテキストで置き換えて、要求あたりの最小リソースを 3.25% に設定します。
    
    ```sql
    IF  EXISTS (SELECT * FROM sys.workload_management_workload_classifiers where group_name = 'CEODemo')
    BEGIN
        Drop Workload Classifier CEODreamDemo
        DROP WORKLOAD GROUP CEODemo
        --- Creates a workload group 'CEODemo'.
            Create  WORKLOAD GROUP CEODemo WITH  
        (MIN_PERCENTAGE_RESOURCE = 26 -- integer value
            ,REQUEST_MIN_RESOURCE_GRANT_PERCENT = 3.25 -- factor of 26 (guaranteed more than 4 concurrencies)
        ,CAP_PERCENTAGE_RESOURCE = 100
        )
        --- Creates a workload Classifier 'CEODreamDemo'.
        Create Workload Classifier CEODreamDemo with
        (Workload_Group ='CEODemo',MemberName='asa.sql.workload02',IMPORTANCE = BELOW_NORMAL);
    END
    ```
    
    > **注**: ワークロードの包含の構成では、コンカレンシーの最大レベルが暗黙的に定義されます。CAP\_PERCENTAGE\_RESOURCE を 60% に設定し、REQUEST\_MIN\_RESOURCE\_GRANT\_PERCENT を 1% に設定した場合、ワークロード グループにレベル 60 までのコンカレンシーが許容されます。コンカレンシーの最大数を決定するには、以下の方法を検討してください。
    > 
    > \[Max Concurrency\] = \[CAP\_PERCENTAGE\_RESOURCE\] / \[REQUEST\_MIN\_RESOURCE\_GRANT\_PERCENT\]

13. 再度システムで大量にクエリを実行して、`asa.sql.workload02` に何が起こるかを確認してみましょう。そのために、多数クエリを実行する Azure Synapse パイプラインを実行します。\[`Orchestrate`\] タブを選択します。**\[Run\]** を選択して **\[Exercise 8 - Execute Business Analyst Queries\]** パイプラインを実行します。このパイプラインは、`asa.sql.workload02` のクエリを実行します。

14. クエリ ウィンドウのスクリプトを以下のテキストで置き換えて、システムで大量に動作しているすべての `asa.sql.workload02` クエリに何が起きるかを確認します。現在、asa.sql.workload02 に対して、さらに多くのクエリが並列に実行されていることに注意してください。
    
    ```sql
    SELECT s.login_name, r.[Status], r.Importance, submit_time,
    start_time ,s.session_id FROM sys.dm_pdw_exec_sessions s
    JOIN sys.dm_pdw_exec_requests r ON s.session_id = r.session_id
    WHERE s.login_name IN ('asa.sql.workload02') and Importance
    is  not NULL AND r.[status] in ('Running','Suspended')
    ORDER BY submit_time, status
    ```

15. ツールバー メニューから **\[Run\]** を選択して SQL コマンドを実行します。

![SQL 結果ペインに、並列に実行されている複数のクエリが表示されています。](media/multiple_parallel_queries_workload02.png "並列に実行されている複数のクエリ")

### タスク 3: 動的管理ビューによる監視

T-SQL を使用して SQL Analytics を監視する場合のプログラミングを経験するために、一連の動的管理ビュー (DMV) が提供されています。これらのビューは、積極的にトラブルシューティングする場合やワークロードのパフォーマンスのボトルネックを特定する場合に役に立ちます。

データ ウェアハウスへのすべてのログインは、`sys.dm_pdw_exec_sessions` に記録されます。この DMV には、過去 10,000 件のログインが含まれています。主キーである `session_id` が、新規ログオンのたびに順次割り当てられます。

1. **\[Develop\]** ハブに移動します。
   
   ![\[Develop\] メニュー項目が強調表示されています。](media/develop-hub.png "[Develop] ハブ")

2. **\[Develop\]** メニューから \[+\] を選択して、コンテキスト メニューから **\[SQL Script\]** を選択します。
   
   ![\[SQL script\] コンテキスト メニュー項目が強調表示されています。](media/synapse-studio-new-sql-script.png "新しい SQL スクリプト")

3. ツールバー メニューで、クエリを実行する **SQL プール** データベースに接続します。
   
   ![クエリのツールバーで \[connect to\] オプションが強調表示されています。](media/synapse-studio-query-toolbar-connect.png "クエリのツールバー")

4. クエリ ウィンドウのスクリプトを以下のテキストで置き換えます。
   
   ```sql
   SELECT * FROM sys.dm_pdw_exec_sessions where status <> 'Closed' and session_id <> session_id();
   ```
   
   SQL プールで実行されるすべてのクエリは、`sys.dm_pdw_exec_requests` に記録されます。この DMV には、実行された過去 10,000 件のクエリが含まれています。`request_id` により各クエリが一意に識別されます。これはこの DMV の主キーです。`request_id` は、新しいクエリごとに順番に割り当てられ、クエリ ID を表す `QID` がプレフィックスとして付加されます。特定の `session_id` を指定してこの DMV に対してクエリを実行すると、特定のログオンのすべてのクエリが表示されます。

5. ツールバー メニューから **\[Run\]** を選択して SQL コマンドを実行します。

6. システムで大量にクエリを実行して、監視する操作を作成しましょう。そのために、クエリをトリガーする Azure Synapse パイプラインを実行します。\[`Orchestrate`\] タブを選択します。**\[Run\]** を選択して **\[Exercise 8 - Execute Business Analyst Queries\]** パイプラインを実行します。このパイプラインは、`asa.sql.workload02` のクエリを実行/トリガーします。**このパイプラインを 30 秒から 1 分間実行し、実行を再帰的にキャンセルします**。

7. クエリ ウィンドウのスクリプトを以下のテキストで置き換えます。
   
   ```sql
   SELECT *
   FROM sys.dm_pdw_exec_requests
   WHERE status not in ('Completed','Failed','Cancelled')
     AND session_id <> session_id()
   ORDER BY submit_time DESC;
   ```

8. ツールバー メニューから **\[Run\]** を選択して SQL コマンドを実行します。クエリ結果に、以下のようなセッションのリストが表示されます。この結果で調査する**クエリの `Request_ID` に注目します** (この値は後のステップで使用するのでテキスト エディターに書き留めてください)。
   
   ![アクティブなクエリの結果。](media/query-active-requests-results.png "クエリ結果")

9. 代わりに、以下の SQL コマンドを実行して、長時間動作しているクエリの上位 10 件を見つけることもできます。
   
   ```sql
   SELECT TOP 10 *
   FROM sys.dm_pdw_exec_requests
   ORDER BY total_elapsed_time DESC;
   ```

10. `sys.dm_pdw_exec_requests` テーブルでクエリを検索しやすくするために、`LABEL` を使用してクエリにコメントを割り当てます。このコメントで、`sys.dm_pdw_exec_requests` ビューを検索できます。ラベルを使用してテストするために、クエリ ウィンドウのスクリプトを以下のテキストで置き換えます。
    
    ```sql
    SELECT *
    FROM sys.tables
    OPTION (LABEL = 'My Query');
    ```

11. ツールバー メニューから **\[Run\]** を選択して SQL コマンドを実行します。

12. クエリ ウィンドウのスクリプトを以下のテキストで置き換えて、結果をラベル `My Query` でフィルターします。
    
    ```sql
    -- Find a query with the Label 'My Query'
    -- Use brackets when querying the label column, as it is a key word
    SELECT  *
    FROM sys.dm_pdw_exec_requests
    WHERE [label] = 'My Query';
    ```

13. ツールバー メニューから **\[Run\]** を選択して SQL コマンドを実行します。結果ビューに、1 つ前に実行したクエリが表示されます。

14. クエリ ウィンドウのスクリプトを以下のテキストで置き換えて、`sys.dm_pdw_request_steps` からクエリの分散 SQL (DSQL) プランを取得します。`QID#####` をステップ 8 で書き留めた `Request_ID` で**置き換えることを忘れないでください。**
    
    ```sql
    SELECT * FROM sys.dm_pdw_request_steps
    WHERE request_id = 'QID####'
    ORDER BY step_index;
    ```

15. ツールバー メニューから **\[Run\]** を選択して SQL コマンドを実行します。指定した要求の分散クエリ プランのステップを示す結果が表示されます。
    
    ![クエリ結果が表示されています。](media/sql-dsql-plan-results.png "クエリ結果")
    
    > DSQL プランに予想以上に時間がかかっている場合、多数の DSQL ステップが存在する複雑なプランであること、または 1 つのステップに長時間かかっていることが原因である可能性があります。プランに複数の移動操作を含む多数のステップが存在する場合、テーブル分散を最適化してデータ移動を減らすことを検討してください。

### タスク 4: \[Monitor\] ハブによるオーケストレーションの監視

1. パイプラインを実行して、その実行を次のステップで監視してみましょう。それには、\[`Orchestrate`\] タブを選択します。**\[Run\]** を選択して **\[Exercise 8 - Execute Business Analyst Queries\]** パイプラインを実行します。
   
   ![\[add trigger\] メニュー項目と \[trigger now\] メニュー項目が強調表示されています。](media/ex7-task4-01.png "Add trigger")

2. \[`Monitor`\] ハブに移動します。**\[Pipeline runs\]** を選択して、過去 24 時間に実行されたパイプラインのリストを取得します。パイプラインのステータスを監視します。
   
   ![\[Monitor\] ハブで \[pipeline runs\] ブレードが表示されています。](media/ex7-task4-02.png "[Monitor] - [Pipeline runs]")

3. 実行中のパイプラインをポイントして **\[Cancel\]** を選択し、そのパイプラインの現在のインスタンスの実行をキャンセルします。
   
   ![\[Cancel\] オプションが強調表示されています。](media/ex7-task4-03.png "キャンセル")

### タスク 5: \[Monitor\] ハブによる SQL 要求の監視

1. パイプラインを実行して、その実行を次のステップで監視してみましょう。それには、\[`Orchestrate`\] タブを選択します。**\[Run\]** を選択して **\[Exercise 8 - Execute Business Analyst Queries\]** パイプラインを実行します。
   
   ![\[add trigger\] メニュー項目と \[trigger now\] メニュー項目が強調表示されています。](media/ex7-task5-01.png "Add trigger")

2. \[`Monitor`\] ハブに移動します。**\[**SQL requests**\]** を選択して、過去 24 時間に実行された SQL 要求のリストを取得します。

3. **\[Pool\]** フィルターを選択して、SQL プールを選択します。`Request Submitter`、`Submit Time`、`Duration`、および `Queued Duration` の値を監視します。
   
   ![\[Monitor\] ハブで \[SQL requests\] ブレードが表示されています。](media/ex7-task5-02.png "[Monitor] - [SQL requests]")

4. SQL 要求のログをポイントして `Request Content` を選択し、SQL 要求の一部として実行された実際の T-SQL コマンドにアクセスします。
   
   ![SQL 要求の上に要求コンテンツ リンクが表示されています。](media/ex7-task5-03.png "SQL requests")

5. 次に、**\[Monitor\]** ハブに戻り、進行中のパイプラインの実行をキャンセルすることができます。

## ハンズオン ラボの後に

**所要時間**: 5 分

### タスク 1: リソース グループの削除

1. Azure Portal で、このラボのリソース グループを開きます。上部のツールバー メニューから **\[Delete\]** を選択します。

2. Azure Portal で、Function App と同じ名前のリソース グループを開きます。上部のツールバー メニューから **\[Delete\]** を選択します。

3. \[Cloud Shell\] を開き、以下のコマンドを発行してラボのファイルを削除します。
   
   ```PowerShell
   Remove-Item -Path .\Synapse-MCW -recurse -force  
   ```

ここで挙げられた手順のすべては、ハンズオン ラボの "参加後" に行う必要があります。