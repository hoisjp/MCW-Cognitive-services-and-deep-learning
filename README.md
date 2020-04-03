<!--
# Cognitive services and deep learning

In this workshop, you will help Contoso Ltd. build a proof of concept that shows how they can build a solution that amplifies the claims processing capabilities of their agents.

They would like to start by automatically classifying each claim detail a customer types in as either home or auto based on the text. This classification would be displayed in the claim summary, so an agent can quickly assess whether they are dealing with purely a home claim, an auto claim or a claim that has a mixture of the two.

They would also like to experiment applying sentiment analysis to the claim text. They know most customers are either factual in their description (a neutral sentiment) or slightly unhappy (a more negative sentiment), but believe that a negative sentiment can be an indicator to claim text that involves a more severe situation, which might warrant an expedited review by an agent.

Next, they would like to automatically summarize long claim text. This summarization would enable the agent to get the gist before having to read the full claim and can quickly remind themselves of the claim when revisiting it.

Finally, they would like to automatically extract information from the photos submitted with the claims to increase their searchability.

December 2019

## Target audience

- [AI Engineers](https://docs.microsoft.com/en-us/learn/certifications/azure-ai-engineer)
- [Data scientist](https://docs.microsoft.com/en-us/learn/certifications/azure-data-scientist)

## Abstracts

### Workshop

In this workshop, you will learn to combine both pre-built artificial intelligence (AI) in the form of various Cognitive Services, with custom AI in the form of services built and deployed with Azure Machine Learning service. You will learn to create intelligent solutions atop unstructured text data by designing and implementing a text analytics pipeline. You will also learn how to build a binary classifier using a recurrent neural network that can be used to classify the textual data. Also, you will learn how to deploy multiple kinds of predictive services using Azure Machine Learning and learn to integrate with the Computer Vision API and the Text Analytics API from Cognitive Services.

At the end of this workshop, you will be better able to present solutions leveraging Azure Machine Learning service, Azure Notebooks and Cognitive Services.

### Whiteboard design session

In this whiteboard design session, you will work with a group to design a solution which combines both pre-built artificial intelligence (AI) in the form of various Cognitive Services, with custom AI in the form of services built and deployed with Azure Machine Learning services. You will learn to create intelligent solutions atop unstructured text data by designing and implementing a text analytics pipeline. You will discover how to build a binary classifier using a recurrent neural network that can be used to classify the textual data, as well as how to deploy multiple kinds of predictive services using Azure Machine Learning and learn to integrate with the Computer Vision API and the Text Analytics API from Cognitive Services.

At the end of this whiteboard design session, you will be better able to design solutions leveraging Azure Machine Learning services and Cognitive Services.

### Hands-on lab

In this hands-on lab, you will implement a solution which combines both pre-built artificial intelligence (AI) in the form of various Cognitive Services, with custom AI in the form of services built and deployed with Azure Machine Learning services. You will learn to create intelligent solutions atop unstructured text data by designing and implementing a text analytics pipeline. You will discover how to build a binary classifier using a recurrent neural network that can be used to classify the textual data, as well as how to deploy multiple kinds of predictive services using Azure Machine Learning and learn to integrate with the Computer Vision API and the Text Analytics API from Cognitive Services.

At the end of this hands-on lab, you will be better able to present solutions leveraging Azure Machine Learning service, Azure Notebooks and Cognitive Services.

## Azure services and related products

- Azure Machine Learning service
- Azure Notebooks
- Cognitive Services
- Computer Vision API
- Text Analytics API
- TensorFlow
- Keras
- ONNX

## Azure solutions

Machine Learning

## Related references

- [MCW](https://github.com/Microsoft/MCW)

## Help & Support

We welcome feedback and comments from Microsoft SMEs & learning partners who deliver MCWs.  

***Having trouble?***

- First, verify you have followed all written lab instructions (including the Before the Hands-on lab document).
- Next, submit an issue with a detailed description of the problem.
- Do not submit pull requests. Our content authors will make all changes and submit pull requests for approval.  

If you are planning to present a workshop, *review and test the materials early*! We recommend at least two weeks prior.

### Please allow 5 - 10 business days for review and resolution of issues
-->

# Cognitive Services と深層学習

Contoso Ltd. は、エージェントのクレーム処理の能力を強化するソリューションを構築するために、その方法を探る概念実証 (PoC) を実施します。このワークショップでは、この PoC をサポートします。

Contoso Ltd. ではまず、顧客がシステムに入力した個々のクレームの情報を自動的に分類したいと考えています。クレームのテキストの内容に応じて、住宅に関するクレームであるのか、自動車に関するクレームであるのかを区別するといったような分類です。分類された情報は、クレームのサマリーに表示します。扱っているクレームの内容が、住宅関連のクレーム、自動車関連のクレーム、両者の混合のクレームのいずれであるのかを、エージェントがすぐに判断できるようにするためです。

Contoso Ltd. では、クレームのテキストの文面から顧客の感情を読み取る実験も実施したいと考えています。ほとんどの顧客は、ただ事実を淡々と述べており、ポジティブな感情もネガティブな感情も抱いていないか、あるいは、いくらか不満を感じており、ネガティブな感情を持っているかのどちらかであることがわかっています。ネガティブな感情を抱いている場合、クレームの内容が深刻であることを知らせる役割を果たしているのは間違いありません。そしてそのような状況を把握できれば、エージェントの確認作業を速められます。

次に、長文のクレームのテキストを自動的に要約する機能を検証します。このような機能があれば、クレームの全文を読まなくても、エージェントはその要点を理解できるようになるほか、対応を離れたクレームに後でもう一度戻ったときにクレームの内容をすぐに思い出すことができます。

そして最後は、クレームに添付された写真から自動的に情報を抽出してクレーム検索の能力を高める機能を検証します。

2019 年 12 月

## 対象となるお客様

- [AI エンジニア](https://docs.microsoft.com/ja-jp/learn/certifications/azure-ai-engineer)
- [データ サイエンティスト](https://docs.microsoft.com/ja-jp/learn/certifications/azure-data-scientist)

## 要約

### ワークショップ

このワークショップでは、事前構築済の人工知能 (AI) とカスタムの AI を組み合わせる方法を学習します。事前構築済の AI は、さまざまな Cognitive Services のかたちで利用し、カスタムの AI は、Azure Machine Learning サービスで開発および展開するサービスとして利用します。テキスト分析パイプラインを設計、実装して、非構造化テキスト データに基づくインテリジェント ソリューションを構築するスキルが身に付きます。また、テキスト データの分類に使用できる回帰型ニューラル ネットワークでバイナリ分類子を構築する方法や、Azure Machine Learning でさまざまな予防保全サービスを展開する方法、Cognitive Services の Computer Vision API や Text Analytics API と連携を行う方法についてもご説明します。

このワークショップを修了すると、Azure Machine Learning サービスや Azure Notebooks、Cognitive Services を活用したソリューションを構築できるようになります。

### ホワイトボード設計セッション

このホワイトボード設計セッションでは、事前構築済の人工知能 (AI) とカスタムの AI を組み合わせたソリューションを、グループでの共同作業を通じて設計します。事前構築済の AI は、さまざまな Cognitive Services のかたちで利用し、カスタムの AI は、Azure Machine Learning サービスで開発および展開するサービスとして利用します。テキスト分析パイプラインを設計、実装して、非構造化テキスト データに基づくインテリジェント ソリューションを構築するスキルが身に付きます。また、テキスト データの分類に使用できる回帰型ニューラル ネットワークでバイナリ分類子を構築する方法や、Azure Machine Learning でさまざまな予防保全サービスを展開する方法、Cognitive Services の Computer Vision API や Text Analytics API と連携を行う方法についてもご説明します。

このホワイトボード設計セッションを修了すると、Azure Machine Learning サービスや Cognitive Services を活用したソリューションを設計できるようになります。

### ハンズオン ラボ

このハンズオン ラボでは、事前構築済の人工知能 (AI) とカスタムの AI を組み合わせたソリューションを実装します。事前構築済の AI は、さまざまな Cognitive Services のかたちで利用し、カスタムの AI は、Azure Machine Learning サービスで開発および展開するサービスとして利用します。テキスト分析パイプラインを設計、実装して、非構造化テキスト データに基づくインテリジェント ソリューションを構築するスキルが身に付きます。また、テキスト データの分類に使用できる回帰型ニューラル ネットワークでバイナリ分類子を構築する方法や、Azure Machine Learning でさまざまな予防保全サービスを展開する方法、Cognitive Services の Computer Vision API や Text Analytics API と連携を行う方法についてもご説明します。

このハンズオン ラボを修了すると、Azure Machine Learning サービスや Azure Notebooks、Cognitive Services を活用したソリューションを構築できるようになります。

## Azure のサービスと関連製品

- Azure Machine Learning サービス
- Azure Notebooks
- Cognitive Services
- Computer Vision API
- Text Analytics API
- TensorFlow
- Keras
- ONNX

## Azure のソリューション

機械学習

## 関連資料

- [MCW (英語)](https://github.com/Microsoft/MCW)

## ヘルプとサポート

MCW を提供されているマイクロソフトの SME パートナー様やラーニング パートナー様からのフィードバックやコメントをお待ちしています。  

***問題が発生した場合には***

- まずはじめに、ハンズオン ラボの事前セットアップ ガイドの内容を含め、ラボの指示書のすべての記述に従っていることを確認します。
- 次に、詳しい説明を添えて、問題の報告を行います。
- プル リクエストは送信しないでください。コンテンツの作成者が、変更作業をすべて完了してから、承認申請のプル リクエストを送信します。  

ワークショップの開催を計画している場合は、*事前にワークショップの環境をチェックおよびテストしてください。*2 週間以上前に実施されることをお勧めします。

### 問題の確認と解決には、5 ～ 10 営業日がかかりますので、あらかじめご了承ください。