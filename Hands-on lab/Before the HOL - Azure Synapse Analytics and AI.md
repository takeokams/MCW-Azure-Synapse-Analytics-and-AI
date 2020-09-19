![マイクロソフト クラウド ワークショップ](https://github.com/Microsoft/MCW-Template-Cloud-Workshop/raw/master/Media/ms-cloud-workshop.png "マイクロソフト クラウド ワークショップ")

<div class="MCWHeader1">
Azure Synapse Analytics と AI
</div>
<div class="MCWHeader2">
「ハンズオン ラボの前に」設定ガイド
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

- [Azure Synapse Analytics と AI 「ハンズオン ラボの前に」設定ガイド](#azure-synapse-analytics-と-ai-ハンズオン-ラボの前に設定ガイド)
    - [必要条件](#必要条件)
    - [ハンズオン ラボの前に](#ハンズオン-ラボの前に)
        - [タスク 1: 最新のラボ アセットのダウンロード](#タスク-1-最新のラボ-アセットのダウンロード)
        - [タスク 2: Azure でのリソース グループの作成](#タスク-2-azure-でのリソース-グループの作成)
        - [タスク 3: Azure Synapse Analytics ワークスペースの作成](#タスク-3-azure-synapse-analytics-ワークスペースの作成)
        - [タスク 4: ラボの成果物のダウンロード](#タスク-4-ラボの成果物のダウンロード)
        - [タスク 5: ユーザー コンテキストの確立](#タスク-5-ユーザー-コンテキストの確立)
        - [タスク 6: 環境設定 PowerShell スクリプトの実行](#タスク-6-環境設定-powershell-スクリプトの実行)

<!-- /TOC -->
# Azure Synapse Analytics と AI 「ハンズオン ラボの前に」設定ガイド

## 必要条件

1. Azure Synapse ワークスペースを作成できる Azure アカウント

2. [Python v.3.7 以降](https://www.python.org/downloads/)

3. [PIP](https://pip.pypa.io/en/stable/installing/#do-i-need-to-install-pip)

4. [Visual Studio Code](https://code.visualstudio.com/)

5. [Visual Studio Code 向けの Python 拡張機能](https://marketplace.visualstudio.com/items?itemName=ms-python.python)

6. [Visual Studio Code 向けの Azure Functions 拡張機能](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)

7. [Postman](https://www.postman.com/downloads/)

## ハンズオン ラボの前に

**所要時間**: 20 分

### タスク 1: 最新のラボ アセットのダウンロード

1. [GitHub リポジトリ ページ](https://github.com/takeokams/MCW-Azure-Synapse-Analytics-and-AI)にアクセスします。

2. 画面の右側で、**\[Code\]** ボタン メニューを展開します。
   
   ![GitHub リポジトリ ページで、\[Code\] ボタンが強調表示されています。](media/githubcodebutton.png "GitHub リポジトリの [Code] ボタン")

3. 展開されたメニューから **\[Download ZIP\]** を選択します。
   
   ![\[Download ZIP\] オプションが、展開された \[Code\] メニューで選択されています。](media/githubdownloadzip.png "Github の [Code] メニュー")

4. ZIP ファイルをダウンロードし、ローカル マシン上の選択した場所にそのファイルを展開します。

### タスク 2: Azure でのリソース グループの作成

1. Azure 資格情報を使用して、[Azure Portal](https://portal.azure.com) にログインします。

2. Azure Portal ホーム画面で、**\[+ Create a resource\]** タイルを選択します。
   
   ![Azure Portal ホーム画面の一部が表示され、\[+ Create a resource\] タイルが強調表示されています。](media/bhol_createaresource.png "リソースの作成")

3. **マーケットプレイスを検索する虫眼鏡**ボックスに **「Resource group」** と入力して、**Enter** キーを押します。
   
   ![新しいリソース画面で、検索条件として「Resource group」が入力されています。](media/bhol_searchmarketplaceresourcegroup.png "リソース グループの検索")

4. **\[Resource group\]** 概要ページで **\[Create\]** を選択します。

5. **\[Create a resource group\]** 画面で、\[Subscription\] と \[Region\] を'westus2,eastus,northeurope,westeurope,southeastasia,australiaeast,westcentralus,southcentralus,eastus2,uksouth,westus,australiasoutheast'の中から選択します。\[Resource group\] に **「Synapse-MCW」**と入力し、**\[Review + Create\]** ボタンを選択します。
   
   ![\[Create a resource group\] フォームが表示され、リソース グループ名として「Synapse-MCW」が入力されています。](media/bhol_resourcegroupform.png "リソース グループの命名")

6. 検証に成功したら、**\[Create\]** ボタンを選択します。

### タスク 3: Azure Synapse Analytics ワークスペースの作成

1. 以下に示す Azure ARM テンプレート (下のボタンを押す) を使用してワークスペースを展開します。
   
   <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmicrosoft%2FMCW-Azure-Synapse-Analytics-and-AI%2Fmaster%2FHands-on%2520lab%2Fenvironment-setup%2Fautomation%2F00-asa-workspace-core.json" target="_blank"><img src="http://azuredeploy.net/deploybutton.png" /></a>

2. **\[Custom deployment\]** フォームで、目的のサブスクリプションを選択し、**\[Resource group\]** で **\[Synapse-MCW\]** を選択します。また、**\[Unique Suffix\]** に任意の値 (自分のイニシャルに誕生年を付加した値など) を入力します。最後に、**\[SQL Administrator Login Password\]** に強力なパスワードを入力します。後で必要になるので、このパスワードの値を覚えておいてください。
   
   ![\[Custom deployment\] フォームが表示され、サンプル データが入力されています。](media/bhol_customdeploymentform.png "カスタム展開の構成")

3. **\[I agree to the terms and conditions stated above\]** をオンにして、**\[Purchase\]** ボタンを選択します。
   
   > **注**: **\[作成\]** ボタンだけのことがあります。また、展開ステップがロールの割り当てで失敗する場合があります。このエラーは無視しても安全です。

### タスク 4: ラボの成果物のダウンロード

1. Azure Portal で上部のツールバーの右側にある Azure Cloud Shell アイコンを選択して、Azure Cloud Shell を開きます。
   
   ![Azure Portal のタスクバーの一部が表示され、Cloud Shell のアイコンが強調表示されています。](media/bhol_azurecloudshellmenu.png "Cloud Shell を開く")
   
   > **注**: Cloud Shell のストレージ アカウントを作成するように促されたら、同意して作成します。

2. \[Cloud Shell\] ウィンドウで、以下のコマンドを入力してリポジトリ ファイルのクローンを作成します。
   
   ```PowerShell
   git clone https://github.com/takeokams/MCW-Azure-Synapse-Analytics-and-AI.git Synapse-MCW
   ```

3. \[Cloud Shell\] は開いたままにします。

### タスク 5: ユーザー コンテキストの確立

1. \[Cloud Shell\] で、以下のコマンドを実行します。
   
   ```cli
   az login
   ```

2. メッセージが表示され、Web ブラウザーで新しいタブを開いて [https://microsoft.com/devicelogin](https://microsoft.com/devicelogin) に移動し、認証コードを入力するように要求されます。
   
   ![メッセージが表示され、デバイスのログイン ページで認証コードを入力するように指示しています。](media/bhol_devicelogin.png "認証メッセージ")
   
   ![ダイアログが表示され、コードの入力を要求しています。](media/bhol_clicodescreen.png "[Authentication] ダイアログ")

3. 認証コードの入力が完了したら、前のステップのタブを閉じて、\[Cloud Shell\] に戻ることができます。

### タスク 6: 環境設定 PowerShell スクリプトの実行

以下のスクリプトを実行する場合、スクリプトを完了まで実行することが重要です。一部のタスクは、他のタスクより時間がかかる場合があります。スクリプトの実行が完了すると、コマンド プロンプトに戻ります。

1. \[Cloud Shell\] で以下のコマンドを実行して、現在のディレクトリを、複製したリポジトリの **automation** フォルダーに変更します。
   
   ```PowerShell
   cd './Synapse-MCW/Hands-on lab/environment-setup/automation'
   ```

2. 以下のコマンドを実行して、**01-environment-setup.ps1** スクリプトを実行します。
   
   ```PowerShell
   ./01-environment-setup.ps1
   ```
   
   Azure Subscription の名前を入力するよう求められます。リストの値をコピーして貼り付けることによって名前を選択できます。また、このスクリプトの以下の情報を入力するよう求められます。
   
   | プロンプト
   |----------
   | Enter the desired Azure Subscription for this lab \[you will be able to copy and paste from a listing\] - このラボで必要な Azure サブスクリプションを入力します \[リストからコピーして貼り付けることができます\]
   | Enter the name of the resource group containing the Azure Synapse Analytics Workspace - Azure Synapse Analytics ワークスペースを含むリソース グループの名前を入力します
   | Enter the SQL Administrator password you used in the deployment - この展開で使用した SQL 管理者パスワードを入力します
   | Enter the unique suffix you used in the deployment - この展開で使用した一意のサフィックスを入力します

   ![\[Azure Cloud Shell\] ウィンドウが表示され、前述のコマンドの出力のサンプルが表示されています。](media/bhol_sampleshelloutput.png "Azure Cloud Shell の出力")

3. スクリプトの終了時に、 **Environment validation has succeeded.** とメッセージが表示されます。

このハンズオン ラボを実行する "前に"、指定されているすべてのステップに従う必要があります。