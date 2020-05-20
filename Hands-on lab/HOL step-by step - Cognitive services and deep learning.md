<!--
![Microsoft Cloud Workshops](https://github.com/Microsoft/MCW-Template-Cloud-Workshop/raw/master/Media/ms-cloud-workshop.png 'Microsoft Cloud Workshops')

<div class="MCWHeader1">
Cognitive services and deep learning
</div>

<div class="MCWHeader2">
Hands-on lab step-by-step
</div>

<div class="MCWHeader3">
December 2019
</div>

Information in this document, including URL and other Internet Web site references, is subject to change without notice. Unless otherwise noted, the example companies, organizations, products, domain names, e-mail addresses, logos, people, places, and events depicted herein are fictitious, and no association with any real company, organization, product, domain name, e-mail address, logo, person, place or event is intended or should be inferred. Complying with all applicable copyright laws is the responsibility of the user. Without limiting the rights under copyright, no part of this document may be reproduced, stored in or introduced into a retrieval system, or transmitted in any form or by any means (electronic, mechanical, photocopying, recording, or otherwise), or for any purpose, without the express written permission of Microsoft Corporation.

Microsoft may have patents, patent applications, trademarks, copyrights, or other intellectual property rights covering subject matter in this document. Except as expressly provided in any written license agreement from Microsoft, the furnishing of this document does not give you any license to these patents, trademarks, copyrights, or other intellectual property.

The names of manufacturers, products, or URLs are provided for informational purposes only, and Microsoft makes no representations and warranties, either expressed, implied, or statutory, regarding these manufacturers or the use of the products with any Microsoft technologies. The inclusion of a manufacturer or product does not imply endorsement of Microsoft of the manufacturer or product. Links may be provided to third-party sites. Such sites are not under the control of Microsoft and Microsoft is not responsible for the contents of any linked site or any link contained in a linked site, or any changes or updates to such sites. Microsoft is not responsible for webcasting or any other form of transmission received from any linked site. Microsoft is providing these links to you only as a convenience, and the inclusion of any link does not imply endorsement of Microsoft of the site or the products contained therein.

© 2019 Microsoft Corporation. All rights reserved.

Microsoft and the trademarks listed at <https://www.microsoft.com/en-us/legal/intellectualproperty/Trademarks/Usage/General.aspx> are trademarks of the Microsoft group of companies. All other trademarks are the property of their respective owners.

**Contents**

- [Cognitive services and deep learning hands-on lab step-by-step](#cognitive-services-and-deep-learning-hands-on-lab-step-by-step)
  - [Abstract and learning objectives](#abstract-and-learning-objectives)
  - [Overview](#overview)
  - [Solution architecture](#solution-architecture)
  - [Requirements](#requirements)
  - [Exercise 1: Setup Azure Notebooks Project](#exercise-1-setup-azure-notebooks-project)
    - [Task 1: Upload project files](#task-1-upload-project-files)
    - [Task 2: Start the Notebook Server](#task-2-start-the-notebook-server)
  - [Exercise 2: Create and Deploy an Unsupervised Model](#exercise-2-create-and-deploy-an-unsupervised-model)
    - [Task 1: Install libraries](#task-1-install-libraries)
    - [Task 2: Read through and execute the Summarization notebook](#task-2-read-through-and-execute-the-summarization-notebook)
    - [Task 3: Provision the Azure Machine Learning Workspace and Create the Summarization service](#task-3-provision-the-azure-machine-learning-workspace-and-create-the-summarization-service)
  - [Exercise 3: Create and Deploy a Keras Model](#exercise-3-create-and-deploy-a-keras-model)
    - [Task 1: Create a simple Keras based model](#task-1-create-a-simple-keras-based-model)
    - [Task 2: Deploy the Keras model](#task-2-deploy-the-keras-model)
  - [Exercise 4: Completing the solution](#exercise-4-completing-the-solution)
    - [Task 1: Deploy the Computer Vision API](#task-1-deploy-the-computer-vision-api)
    - [Task 2: Deploy the Text Analytics API](#task-2-deploy-the-text-analytics-api)
    - [Task 3: Completing the solution](#task-3-completing-the-solution)
  - [After the hands-on lab](#after-the-hands-on-lab)
    - [Task 1: Clean up lab resources](#task-1-clean-up-lab-resources)

# Cognitive services and deep learning hands-on lab step-by-step

## Abstract and learning objectives

In this hands-on lab, you will implement a solution which combines both pre-built artificial intelligence (AI) in the form of various Cognitive Services, with custom AI in the form of services built and deployed with Azure Machine Learning service. You will learn to create intelligent solutions atop unstructured text data by designing and implementing a text analytics pipeline. You will discover how to build a binary classifier using a simple neural network that can be used to classify the textual data, as well as how to deploy multiple kinds of predictive services using Azure Machine Learning and learn to integrate with the Computer Vision API and the Text Analytics API from Cognitive Services.

At the end of this hands-on lab, you will be better able to implement solutions leveraging Azure Machine Learning service and Cognitive Services.

## Overview

In this workshop, you will help Contoso Ltd. build a proof of concept that shows how they can build a solution that amplifies the claims processing capabilities of their agents.

## Solution architecture

The high-level architecture of the solution is illustrated in the diagram. The lab is performed within the context of a notebook running within Azure Notebooks. Various notebooks are built to test the integration with the Cognitive Services listed, to train custom ML services, and to integrate the results in a simple user interface that shows the result of processing the claim with all of the AI services involved.

![The High-level architectural solution begins with a Claim, which us submitted for processing using a notebook in Azure Databricks. This notebook coordinates the calls to Computer Vision, Text Analytics, and Containerized Services, which includes a Classification Service and a Summary Service that both processes claim text.](media/image2.jpg 'High-level architectural solution')

## Requirements

1. Microsoft Azure subscription must be pay-as-you-go or MSDN

    - Trial subscriptions will not work. You will run into issues with Azure resource quota limits.

    - Subscriptions with access limited to a single resource group will not work. You will need the ability to deploy multiple resource groups.

## Exercise 1: Setup Azure Notebooks Project

Duration: 20 minutes

In this exercise, you will set up your Azure Notebooks Project.

### Task 1: Upload project files

1. Log in to [Azure Notebooks](https://notebooks.azure.com/).

2. Navigate to **My Projects** page.

3. Select **Upload GitHub Repo**.

4. In the Upload GitHub Repository dialog, for the GitHub repository provide **`https://github.com/microsoft/MCW-Cognitive-services-and-deep-learning.git`** and select **Import**. Allow the import a few moments to complete. The dialog will dismiss once the import has completed.

    ![In the dialog the GitHub URL to upload the project repository is shown.](images/az_nb_setup/01.png 'Upload GitHub Repository dialog box')

### Task 2: Start the Notebook Server

1. Navigate to your project: `MCW-Cognitive-services-and-deep-learning`.

2. Start your Notebook server on `Free Compute` by selecting the **Play** icon in the toolbar as shown:

    ![The image shows the Start Notebook Server Icon and highlights the area to select.](images/az_nb_setup/02.png 'Start Notebook Server Icon')

3. Navigate to the `> MCW-Cognitive-services-and-deep-learning > Hands-on lab > notebooks` folder where you will find all your lab files.

    ![Jupyter notebook interface showing the folder where the lab files are present.](images/az_nb_setup/03.png 'Jupyter Notebooks Folder')

## Exercise 2: Create and Deploy an Unsupervised Model

Duration: 60 minutes

In this exercise, you will create and deploy a web service that uses a pre-trained model to summarize long paragraphs of text.

### Task 1: Install libraries

The notebooks you will run depends on certain Python libraries like Keras, and TensorFlow. The following steps walk you through adding these dependencies.

1. Within the `notebooks` folder, select the notebook called `00 init`. This will open the notebook so you can read and execute the code it contains.

2. Run each cell in the notebook to install the required libraries.

### Task 2: Read through and execute the Summarization notebook

1. Within the `notebooks` folder, select the notebook called `01 Summarize`. This will open the notebook so you can read and execute the code it contains.

2. Read the instructions at the top of the notebook, and execute the cells as instructed.

### Task 3: Provision the Azure Machine Learning Workspace and Create the Summarization service

1. Within the `notebooks` folder, select the notebook called `02 Deploy Summarizer Web Service`. This will open the notebook so you can read and execute the code it contains.

2. Read the instructions at the top of the notebook, and execute the cells as instructed.

## Exercise 3: Create and Deploy a Keras Model

Duration: 60 minutes

In this exercise, you will use Keras to construct and train a DNN called the Long Short-Term Memory (LSTM) recurrent neural network. LSTM is shown to work well for text classification problems, especially when used in conjunction with word embedding such as GloVe for word vectorization. In this notebook you will also learn how GloVe word embeddings perform on word analogy tasks.

### Task 1: Create a simple Keras based model

1. Within the `notebooks` folder, select the notebook called `03 Claim Classification`. This will open the notebook so you can read and execute the code it contains.

2. Read the instructions at the top of the notebook, and execute the cells as instructed.

   >**Note**: Pay attention to the top of the notebook and check the version of TensorFlow and Keras libraries. TensorFlow version should be == 1.13.1 and Keras version should be == 2.3.1.

### Task 2: Deploy the Keras model

1. Within the `notebooks` folder, select the notebook called `04 Deploy Classifier Web Service`. This will open the notebook so you can read and execute the code it contains.

2. Read the instructions at the top of the notebook, and execute the cells as instructed.

## Exercise 4: Completing the solution

Duration: 45 minutes

In this exercise, you will perform the final integration with the Computer Vision API and the Text Analytics API along with the Azure Machine Learning service you previously deployed to deliver the completed proof of concept solution.

### Task 1: Deploy the Computer Vision API

1. Navigate to the Azure Portal in your browser.

2. Select **Create a resource**.

3. Select **AI + Machine Learning** and then **Computer Vision**.\
    ![In the New blade, the AI + Machine Learning option is selected.](media/image19.png 'New blade')

4. On the **Create** blade, provide the following:

    - **Name:** Provide a unique name for this instance.

    - **Subscription:** Select your Azure subscription.

    - **Location**: Select a location nearest your other deployed services.

    - **Pricing tier**: Select S1.

    - **Resource group**: Select the existing mcwailab resource group.

    ![The Create blade fields display the previously defined settings.](media/image60.png 'Create blade')

5. Select **Create**.

6. When the notification appears that the deployment succeeded, select **Go to resource**.

    ![A Deployment succeeded notification displays.](media/image61.png 'Notification')

7. Select **Quick start** and then copy the value of **Key 1** and **Endpoint** into notepad or something similar as you will need this value later in the lab.

    ![In the Cognitive Services blade, under Resource Management, Quick start is selected. ](media/image62.png 'Cognitive Services blade')

### Task 2: Deploy the Text Analytics API

1. Navigate to the Azure Portal in your browser.

2. Select **Create a resource**.

3. Select **AI + Machine Learning** and then **Text Analytics**.

    ![In the New blade, both AI + Cognitive Services and Text Analytics API are selected.](media/image64.png 'New blade')

4. On the **Create** blade, provide the following:

    a. **Name**: Provide a unique name for this instance.

    b. **Subscription**: Select your Azure subscription.

    c. **Location**: Select a location nearest your other deployed services.

    d. **Pricing tier**: Select S0.

    e. **Resource group**: Select the existing mcw-ai-lab resource group.

    ![The Create blade fields are set to the previously defined settings.](media/image65.png 'Create blade')

5. Select **Create**.

6. When the notification appears that the deployment succeeded, select **Go to resource**.

    ![A Deployment succeeded notification displays.](media/image66.png 'Notification')

7. Select **Quick start** and then copy the value of **Key 1** and **Endpoint** into notepad or something similar as you will need this value later in the lab.

    ![In the Cognitive Services blade, under Resource Management, Quick start is selected. ](media/image67.png 'Cognitive Services blade')

### Task 3: Completing the solution

1. Return to your Azure Notebooks Project. Within the `notebooks` folder, select the notebook called `05 Cognitive Services`. This will open the notebook so you can read and execute the code it contains.

2. Follow the steps within the notebook to complete the lab and view the result of combining Cognitive Services with your Azure Machine Learning Services.

## After the hands-on lab

Duration: 5 minutes

To avoid unexpected charges, it is recommended that you clean up all of your lab resources when you complete the lab.

### Task 1: Clean up lab resources

1. Navigate to the Azure Portal and locate the `mcwailab` Resource Group you created for this lab.

2. Select **Delete resource group** from the command bar.

    ![Screenshot of the Delete resource group button.](media/image71.png 'Delete resource group button')

3. In the confirmation dialog that appears, enter the name of the resource group and select **Delete**.

4. Wait for the confirmation that the Resource Group has been successfully deleted. If you don't wait, and the delete fails for some reason, you may be left with resources running that were not expected. You can monitor using the Notifications dialog, which is accessible from the Alarm icon.

    ![The Notifications dialog box has a message stating that the resource group is being deleted.](media/image72.png 'Notifications dialog box')

5. When the Notification indicates success, the cleanup is complete.

    ![The Notifications dialog box has a message stating that the resource group has been deleted.](media/image73.png 'Notifications dialog box')

You should follow all steps provided _after_ attending the Hands-on lab.
-->
![Microsoft Cloud Workshops](https://github.com/Microsoft/MCW-Template-Cloud-Workshop/raw/master/Media/ms-cloud-workshop.png 'Microsoft Cloud Workshops')

<div class="MCWHeader1">
Cognitive Services と深層学習
</div>

<div class="MCWHeader2">
ステップバイステップ式ハンズオン ラボ
</div>

<div class="MCWHeader3">
2019 年 12 月
</div>

このドキュメントに記載されている情報 (URL や他のインターネット Web サイト参照を含む) は、将来予告なしに変更することがあります。別途記載されていない場合、このソフトウェアおよび関連するドキュメントで使用している会社、組織、製品、ドメイン名、電子メール アドレス、ロゴ、人物、場所、出来事などの名称は架空のものです。実在する商品名、団体名、個人名などとは一切関係ありません。お客様ご自身の責任において、適用されるすべての著作権関連法規に従ったご使用をお願いいたします。著作権法による制限に関係なく、マイクロソフトの書面による許可なしに、このドキュメントの一部または全部を複製したり、検索システムに保存または登録したり、別の形式に変換したりすることは、手段、目的を問わず禁じられています。ここでいう手段とは、複写や記録など、電子的、または物理的なすべての手段を含みます。

マイクロソフトは、このドキュメントに記載されている内容に関し、特許、特許申請、商標、著作権、またはその他の無体財産権を有する場合があります。別途マイクロソフトのライセンス契約上に明示の規定のない限り、このドキュメントはこれらの特許、商標、著作権、またはその他の知的財産権に関する権利をお客様に許諾するものではありません。

製造元名、製品名、URL は、情報提供のみを目的としており、これらの製造元またはマイクロソフトのテクノロジを搭載した製品の使用について、マイクロソフトは、明示的、黙示的、または法令によるいかなる表明も保証もいたしません。製造元または製品に対する言及は、マイクロソフトが当該製造元または製品を推奨していることを示唆するものではありません。掲載されているリンクは、外部サイトへのものである場合があります。これらのサイトはマイクロソフトの管理下にあるものではなく、リンク先のサイトのコンテンツ、リンク先のサイトに含まれているリンク、または当該サイトの変更や更新について、マイクロソフトは一切責任を負いません。リンク先のサイトから受信した Web キャストまたはその他の形式での通信について、マイクロソフトは責任を負いません。マイクロソフトは受講者の便宜を図る目的でのみ、これらのリンクを提供します。また、リンクの掲載は、マイクロソフトが当該サイトまたは当該サイトに掲載されている製品を推奨していることを示唆するものではありません。

© 2019 Microsoft Corporation. All rights reserved.

Microsoft および <https://www.microsoft.com/en-us/legal/intellectualproperty/Trademarks/Usage/General.aspx> (英語) に掲載されているその他の商標は、マイクロソフト グループ各社の商標です。その他すべての商標は、その所有者に帰属します。

**このドキュメントの内容**

- [Cognitive Services と深層学習に関するステップバイステップ式ハンズオン ラボ](#cognitive-services-と深層学習に関するステップバイステップ式ハンズオン-ラボ)
  - [要約と学習目標](#要約と学習目標)
  - [概要](#概要)
  - [ソリューションのアーキテクチャ](#ソリューションのアーキテクチャ)
  - [前提条件](#前提条件)
  - [演習 1: Azure Notebooks プロジェクトのセットアップ](#演習-1-azure-notebooks-プロジェクトのセットアップ)
    - [タスク 1: プロジェクト ファイルのアップロード](#タスク-1-プロジェクト-ファイルのアップロード)
    - [タスク 2: Notebook Server の起動](#タスク-2-notebook-server-の起動)
  - [演習 2: 教師なしモデルの作成と展開](#演習-2-教師なしモデルの作成と展開)
    - [タスク 1: ライブラリのインストール](#タスク-1-ライブラリのインストール)
    - [タスク 2: Summarization ノートブックの内容の確認と処理の実行](#タスク-2-summarization-ノートブックの内容の確認と処理の実行)
    - [タスク 3: Azure Machine Learning ワークスペースのプロビジョニングと Summarization サービスの作成](#タスク-3-azure-machine-learning-ワークスペースのプロビジョニングと-summarization-サービスの作成)
  - [演習 3: Keras モデルの作成と展開](#演習-3-keras-モデルの作成と展開)
    - [タスク 1: Keras ベースのシンプルなモデルの作成](#タスク-1-keras-ベースのシンプルなモデルの作成)
    - [タスク 2: Keras モデルの展開](#タスク-2-keras-モデルの展開)
  - [演習 4: ソリューションを完成する](#演習-4-ソリューションを完成する)
    - [タスク 1: Computer Vision API の展開](#タスク-1-computer-vision-api-の展開)
    - [タスク 2: Text Analytics API の展開](#タスク-2-text-analytics-api-の展開)
    - [タスク 3: ソリューションを完成する](#タスク-3-ソリューションを完成する)
  - [ハンズオン ラボの後に](#ハンズオン-ラボの後に)
    - [タスク 1: ラボのリソースのクリーンアップ](#タスク-1-ラボのリソースのクリーンアップ)

# Cognitive Services と深層学習に関するステップバイステップ式ハンズオン ラボ<a name="cognitive-services-と深層学習に関するステップバイステップ式ハンズオン-ラボ"></a>

## 要約と学習目標<a name="要約と学習目標"></a>

このハンズオン ラボでは、事前構築済の人工知能 (AI) とカスタムの AI を組み合わせたソリューションを実装します。事前構築済の AI は、さまざまな Cognitive Services のかたちで利用し、カスタムの AI は、Azure Machine Learning サービスで開発および展開するサービスとして利用します。テキスト分析パイプラインを設計、実装して、非構造化テキスト データに基づくインテリジェント ソリューションを構築するスキルが身に付きます。また、テキスト データの分類に使用できるシンプルなニューラル ネットワークでバイナリ分類子を構築する方法や、Azure Machine Learning でさまざまな予防保全サービスを展開する方法、Cognitive Services の Computer Vision API や Text Analytics API と連携を行う方法についてもご説明します。

このハンズオン ラボを修了すると、Azure Machine Learning サービスや Cognitive Services を活用したソリューションを実装できるようになります。

## 概要<a name="概要"></a>

Contoso Ltd. は、エージェントのクレーム処理の能力を強化するソリューションを構築するために、その方法を探る概念実証 (PoC) を実施します。このワークショップでは、この PoC をサポートします。

## ソリューションのアーキテクチャ<a name="ソリューションのアーキテクチャ"></a>

ソリューションのアーキテクチャの概要を以下の図に示します。このラボは、Azure Notebooks で実行するノートブックのコンテキスト内で実施されます。ラボでは、さまざまなノートブックを作成して、個々の Cognitive Services との連携のテストや、カスタムの機械学習サービスのトレーニングを行います。また、すべての AI サービスで処理したクレームの処理の結果をシンプルなユーザー インターフェイスで表示できるよう結果を集約する場合にも、ノートブックを使用します。

![ソリューションのアーキテクチャの概要。Azure Databricks のノートブックでクレームを提出するところから処理が始まります。このノートブックでは、Computer Vision や Text Analytics、コンテナー化されたサービス (分類サービスおよび要約サービス) へのコールを調整します。これらのサービスはどちらもクレームのテキストを処理します。](media/image2.jpg 'High-level architectural solution')

## 前提条件<a name="前提条件"></a>

1. Microsoft Azure サブスクリプションが従量課金制または MSDN であること

    - 試用版のサブスクリプションは使用できません。Azure のリソースのクォータ制限に関連した問題が発生します。

    - 単一のリソース グループだけにしかアクセスできないサブスクリプションは使用できません。複数のリソース グループを展開できる必要があります。

## 演習 1: Azure Notebooks プロジェクトのセットアップ<a name="演習-1-azure-notebooks-プロジェクトのセットアップ"></a>

所要時間: 20 分

この演習では、Azure Notebooks プロジェクトをセットアップします。

### タスク 1: プロジェクト ファイルのアップロード<a name="タスク-1-プロジェクト-ファイルのアップロード"></a>

1. [Azure Notebooks (英語)](https://notebooks.azure.com/) にログインします。

2. [**My Projects (マイ プロジェクト)**] ページへ移動します。

3. [**Upload GitHub Repo (GitHub リポジトリをアップロード)**] を選択します。

4. [Upload GitHub Repository (GitHub リポジトリのアップロード)] ダイアログで、[GitHub repository (GitHub リポジトリ)] に 「**`https://github.com/microsoft/MCW-Cognitive-services-and-deep-learning.git`**」と入力し、[**Import (インポート)**] を選択します。しばらくすると、インポートが完了します。インポートが完了すると、ダイアログが閉じます。※ネットワークの環境によって、Internal Server Error が表示される場合がありますが、その場合は何度かインポートを試してみてください。

    ![プロジェクト リポジトリのアップロード先となる GitHub の URL がダイアログに表示されています。](images/az_nb_setup/01.png 'Upload GitHub Repository dialog box')

### タスク 2: Notebook Server の起動<a name="タスク-2-notebook-server-の起動"></a>


1. プロジェクトの `MCW-Cognitive-services-and-deep-learning` に移動します。

2. 以下のツールバーに示す [**Play**] アイコンを選択し、`無料のコンピューティング`で Notebook Server を起動します。

    ![この画像では、Notebook Server の起動アイコンが表示されており、選択する領域が強調表示されています。](images/az_nb_setup/02.png 'Start Notebook Server Icon')

3. `MCW-Cognitive-services-and-deep-learning、[Hands-on lab (ハンズオン ラボ)]、ノートブック`のフォルダーの順に移動します。このフォルダーにラボのファイルがすべて格納されています。

    ![Jupyter Notebook のインターフェース。ラボのファイルを格納しているフォルダーが表示されています。](images/az_nb_setup/03.png 'Jupyter Notebooks Folder')

## 演習 2: 教師なしモデルの作成と展開<a name="演習-2-教師なしモデルの作成と展開"></a>

所要時間: 60 分

この演習では、訓練済のモデルでパラグラフの長いテキストを要約する Web サービスを作成、展開します。

### タスク 1: ライブラリのインストール<a name="タスク-1-ライブラリのインストール"></a>

ノートブックは、Keras や TensorFlow をはじめとする、Python の特定のライブラリに依存して動作します。以下の手順に従い、この依存関係を追加します。

1. [`notebooks`] フォルダーで、「`00 init`」というノートブックを選択します。ノートブックが開くので、中のコードをチェックして実行します。

2. ノートブックの個々のセルを実行して、必要なライブラリをインストールします。

### タスク 2: Summarization ノートブックの内容の確認と処理の実行<a name="タスク-2-summarization-ノートブックの内容の確認と処理の実行"></a>


1. [`notebooks`] フォルダーで、「`01 Summarize`」というノートブックを選択します。ノートブックが開くので、中のコードをチェックして実行します。

2. ノートブックの先頭にある指示を読み、その内容に従ってセルを実行します。

### タスク 3: Azure Machine Learning ワークスペースのプロビジョニングと Summarization サービスの作成<a name="タスク-3-azure-machine-learning-ワークスペースのプロビジョニングと-summarization-サービスの作成"></a>

1. [`notebooks`] フォルダーで、「`02 Deploy Summarizer Web Service`」というノートブックを選択します。ノートブックが開くので、中のコードをチェックして実行します。

2. ノートブックの先頭にある指示を読み、その内容に従ってセルを実行します。

## 演習 3: Keras モデルの作成と展開<a name="演習-3-keras-モデルの作成と展開"></a>

所要時間: 60 分

この演習では、Keras を使用して、長・短期記憶 (LSTM) 回帰型ニューラル ネットワークと呼ばれる DNN の構築とトレーニングを行います。LSTM は、テキストの分類に関する問題の解決に大いに威力を発揮します。単語のベクトル化に使用する GloVe などの単語埋め込み機能と組み合わせて使用すると特に大きな効果を期待できます。GloVe による単語の埋め込みを単語類推のタスクで実行する方法についてもこのノートブックで学習します。

### タスク 1: Keras ベースのシンプルなモデルの作成<a name="タスク-1-keras-ベースのシンプルなモデルの作成"></a>

1. [`notebooks`] フォルダーで、「`03 Claim Classification`」というノートブックを選択します。ノートブックが開くので、中のコードをチェックして実行します。

2. ノートブックの先頭にある指示を読み、その内容に従ってセルを実行します。

   >**注**: ノートブックの先頭にある指示によく目を通し、TensorFlow と Keras の各ライブラリのバージョンをチェックしてください。TensorFlow のバージョンは 1.13.1 を、また、Keras のバージョンは 2.3.1 を使用されるようお勧めします。

### タスク 2: Keras モデルの展開<a name="タスク-2-keras-モデルの展開"></a>

1. [`notebooks`] フォルダーで、「`04 Deploy Classifier Web Service`」というノートブックを選択します。ノートブックが開くので、中のコードをチェックして実行します。

2. ノートブックの先頭にある指示を読み、その内容に従ってセルを実行します。

## 演習 4: ソリューションを完成する<a name="演習-4-ソリューションを完成する"></a>

所要時間: 45 分

この演習では、前に展開した Azure Machine Learning サービスに加え、Computer Vision API や Text Analytics API とも連携を行います。この作業により、PoC ソリューションが完成します。

### タスク 1: Computer Vision API の展開<a name="タスク-1-computer-vision-api-の展開"></a>

1. ブラウザーで、Azure ポータルに移動します。

2. [**Create a resource (リソースを作成)**] を選択します。

3. [**AI + Machine Learning (AI + 機械学習)**]、[**Computer Vision**] の順に選択します。\
    ![この新規のブレードでは、[AI + Machine Learning (AI + 機械学習)] オプションが選択されています。](media/image19.png 'New blade')

4. [**Create (作成)**] ブレードで、以下の値を入力します。

    - **Name (名前)**: このインスタンスの一意の名前を入力します。

    - **Subscription (サブスクリプション)**: お使いの Azure のサブスクリプションを選択します。

    - **Location (拠点)**: 展開している他のサービスの最も近くにある拠点を選択します。

    - **Pricing tier (料金レベル)**: S1 を選択します。

    - **Resource group (リソース グループ)**: 既存の mcw-ai-lab リソース グループを選択します。

    ![この [Create (作成)] ブレード フィールドには、事前定義された設定が表示されています。](media/image60.png 'Create blade')

5. [**Create (作成)**] を選択します。

6. 展開が正常に完了したことを知らせる通知が表示されたら、[**Go to resource (リソースへ移動)**] を選択します。

    ![展開が正常に完了したことを知らせる通知。](media/image61.png 'Notification')

7. [**Quick start (クイック スタート)**] を選択します。[**Key 1 (キー 1)**] と [**Endpoint (エンドポイント)**] の値は後で必要になるので、メモ帳などのソフトにコピーします。

    ![この [Cognitive Services] ブレードでは、[Resource Management (リソースの管理)] で [Quick start (クイック スタート)] が選択されています。](media/image62.png 'Cognitive Services blade')

### タスク 2: Text Analytics API の展開<a name="タスク-2-text-analytics-api-の展開"></a>


1. ブラウザーで、Azure ポータルに移動します。

2. [**Create a resource (リソースを作成)**] を選択します。

3. [**AI + Machine Learning (AI + 機械学習)**]、[**Text Analytics**] の順に選択します。

    ![この [New (新規)] ブレードでは、[AI + Machine Learning (AI + 機械学習)] と [Text Analytics API] が選択されています。](media/image64.png 'New blade')

4. [**Create (作成)**] ブレードで、以下の値を入力します。

    a. **Name (名前)**: このインスタンスの一意の名前を入力します。

    b. **Subscription (サブスクリプション)**: お使いの Azure のサブスクリプションを選択します。

    c. **Location (拠点)**: 展開している他のサービスの最も近くにある拠点を選択します。

    d. **Pricing tier (料金レベル)**: S0 を選択します。

    e. **Resource group (リソース グループ)**: 既存の mcw-ai-lab リソース グループを選択します。

    ![Create (作成)] ブレード フィールドは、事前定義された設定に設定されています。](media/image65.png 'Create blade')

5. [**Create (作成)**] を選択します。

6. 展開が正常に完了したことを知らせる通知が表示されたら、[**Go to resource (リソースへ移動)**] を選択します。

    ![展開が正常に完了したことを知らせる通知。](media/image66.png 'Notification')

7. [**Quick start (クイック スタート)**] を選択します。[**Key 1 (キー 1)**] と [**Endpoint (エンドポイント)**] の値は後で必要になるので、メモ帳などのソフトにコピーします。

    ![この [Cognitive Services] ブレードでは、[Resource Management (リソースの管理)] で [Quick start (クイック スタート)] が選択されています。](media/image67.png 'Cognitive Services blade')

### タスク 3: ソリューションを完成する<a name="タスク-3-ソリューションを完成する"></a>

1. Azure Notebooks プロジェクトに戻ります。[`notebooks`] フォルダーで、「`05 Cognitive Services`」というノートブックを選択します。ノートブックが開くので、中のコードをチェックして実行します。

2. ノートブック内にある手順に従い、ラボを完了し、Cognitive Services と Azure Machine Learning サービスを組み合わせた結果を表示します。

## ハンズオン ラボの後に<a name="ハンズオン-ラボの後に"></a>

所要時間: 5 分

予想外の料金が発生するのを避けるため、ラボを完了するときにラボのリソースすべてをクリーンアップするようお勧めします。

### タスク 1: ラボのリソースのクリーンアップ<a name="タスク-1-ラボのリソースのクリーンアップ"></a>
1. Azure ポータルへ移動し、このラボ用に作成した「`mcwailab`」リソース グループを特定します。

2. コマンド バーで [**Delete resource group (リソース グループを削除)**] を選択します。

    ![リソース グループを削除するボタンのスクリーンショット。](media/image71.png 'Delete resource group button')

3. 表示される確認のダイアログでリソース グループの名前を入力し、[**Delete (削除)**] を選択します。

4. リソース グループが正常に削除されるのを待ちます。確認を待つことなく、何らかの理由で削除が失敗した場合は、想定外のリソースが実行されたままになっている可能性があります。[Notifications (通知)] ダイアログを使用すると削除の状況を監視できます。このダイアログには、アラーム アイコンからアクセスできます。

    ![リソース グループを削除中であることを知らせるメッセージが、[Notifications (通知)] ダイアログ ボックスに表示されています。](media/image72.png 'Notifications dialog box')

5. 処理が正常に完了したことを知らせる通知が表示されたら、クリーンアップは完了です。

    ![リソース グループの削除が完了したことを知らせるメッセージが、[Notifications (通知)] ダイアログ ボックスに表示されています。](media/image73.png 'Notifications dialog box')

ハンズオン ラボの終了後に、この手順すべてを実行してください。