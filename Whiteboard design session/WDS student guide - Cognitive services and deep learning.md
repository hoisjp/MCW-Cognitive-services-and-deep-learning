<!--
![Microsoft Cloud Workshops](https://github.com/Microsoft/MCW-Template-Cloud-Workshop/raw/master/Media/ms-cloud-workshop.png "Microsoft Cloud Workshops")

<div class="MCWHeader1">
Cognitive services and deep learning
</div>

<div class="MCWHeader2">
Whiteboard design session student guide
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

-->
<!-- TOC -->
<!--

- [Cognitive services and deep learning whiteboard design session student guide](#cognitive-services-and-deep-learning-whiteboard-design-session-student-guide)
  - [Abstract and learning objectives](#abstract-and-learning-objectives)
  - [Step 1: Review the customer case study](#step-1-review-the-customer-case-study)
    - [Customer situation](#customer-situation)
    - [Customer needs](#customer-needs)
    - [Customer objections](#customer-objections)
    - [Infographic for common scenarios](#infographic-for-common-scenarios)
  - [Step 2: Design a proof of concept solution](#step-2-design-a-proof-of-concept-solution)
  - [Step 3: Present the solution](#step-3-present-the-solution)
  - [Wrap-up](#wrap-up)
  - [Additional references](#additional-references)

-->
<!-- /TOC -->
<!--

# Cognitive services and deep learning whiteboard design session student guide

## Abstract and learning objectives

In this whiteboard design session, you will work with a group to design a solution which combines both pre-built artificial intelligence (AI) in the form of various Cognitive Services, with custom AI in the form of services built and deployed with Azure Machine Learning service. You will learn to create intelligent solutions atop unstructured text data by designing and implementing a text analytics pipeline. You will discover how to build a binary classifier using a recurrent neural network that can be used to classify the textual data, as well as how to deploy multiple kinds of predictive services using Azure Machine Learning service and learn to integrate with the Computer Vision API and the Text Analytics API from Cognitive Services.

At the end of this whiteboard design session, you will be better able to design solutions leveraging the Azure Machine Learning service and Cognitive Services.

## Step 1: Review the customer case study

**Outcome**

Analyze your customer's needs.

Timeframe: 15 minutes

Directions: With all participants in the session, the facilitator/SME presents an overview of the customer case study along with technical tips.

1. Meet your table participants and trainer.

2. Read all of the directions for steps 1-3 in the student guide.

3. As a table team, review the following customer case study.

### Customer situation

Contoso Ltd is a large corporation, headquartered in the United States that provides insurance packages for U.S. consumers. Its products include accident and health insurance, life insurance, travel, home, and auto coverage.

Contoso is looking to build a next-generation platform for its insurance products and had identified claims processing as the first area in which they would like to focus their efforts. Currently customers submit a claim using either the website, their mobile app or by speaking with a live agent.

A claim includes the following information:

- Information about the insured (contact information, policy number, etc.)

- Free text responses describing the claim (details of what happened, what was affected, the conditions in which it occurred)

- Photographs that support the claim (photos of the insured object before the event, photos of the damage or stolen items, etc.)

When an agent (an employee or contractor of Contoso) is processing a claim, there are multiple challenges that add significantly to the cost, including the significant time it takes for an agent to read through and process the content submitted with each claim, as well as the difficulty they have in finding particular claim artifacts when returning to a claim after a while. While each claim is stored in a database, the details about the claim, including the free text responses and supporting photos, are stored as opaque attachments that are not searchable - meaning agents typically pull up the claim by the claim number or the insured's contact information and then must manually read through the attachments.

Also, there are some common challenges that Contoso is hoping they could automate away. According to Francine Fischer, CIO, there are two sets of issues where they envision amplifying the capabilities of their agents with AI.

One set of such issues deals with the free text responses. The first issue Contoso identified is that each claim detail should be automatically classified as either home or auto based on the text. This classification would be displayed in the claim summary, so an agent can quickly assess whether they are dealing with purely a home claim, an auto claim or a claim that has a mixture of the two.

The second issue is Contoso would like to experiment applying sentiment analysis to the claim text. They know most customers are either  factual in their description (a neutral sentiment) or slightly unhappy (a more negative sentiment), but believe that a negative sentiment can be an indicator to claim text that involves a more severe situation, which might warrant an expedited review by an agent.

The third issue with the free text is that some of the responses are long. When agents are shifting between claims, it can be hard for them to recall which response had the details for which they are looking. Contoso would like to experiment with an automatic summarization of long claims that produces a summary of about 30 words in length. This summarization would enable the agent to get the gist before having to read the full claim and can quickly remind themselves of the claim when revisiting it.

The next set of issues where they would like to amplify the capabilities of their agents have to deal with extracting information from the photos submitted to increase their searchability. The first item they would like to address is providing automatic captions describing the contents of the photo. Second, they would like to automatically apply tags that describe the content of the photo. Third, the solution should try to pull out any text that appears in the image. Taken together, solving these items can reduce the amount of data entry an agent has to do, while simultaneously increasing the searchability for content present in photos.

As a final step, they would like to organize the information extracted from photos, tying it together with the results of processing the free text responses into a solution that is easily searchable and stays up to date as new claim information surfaces.

As a first step towards their bigger goals, Contoso would like to build a proof of concept (PoC) for an intelligent solution that could automate all the above. They would like to build this PoC to build upon their claims submission solution they already have running in Azure (which consists of a Web App for claims submission and a SQL Database for claim storage). They believe this might be possible using AI, machine learning or deep learning and would like to build a proof of concept to understand just how far they can go using these technologies.

### Customer needs

1. We receive a lot of useful information in the free text responses, but because they can be long, agents sometimes skip over them and miss vital details or spend too much time looking for a particular detail when returning to a claim. We aren't certain this can be automated, but we would like to have a standardized process that identifies the key entities in a claim and pulls them out into a separate list that agents can more easily review, and then view the entity in the context of the claim.

2. We need a solution that can "look" at a photo and give us a description of the photos contents and tag the photos with keywords, so agents can more easily find and refer to the photo later.

3. We are looking to amplify the capabilities of our agents and improve their claims processing capabilities - not replace them. We want a solution that does the same.

### Customer objections

1. We are skeptical about all the hype surrounding these "AI" solutions. It's hard to know what is feasible versus what is not possible with today's technology and Azure.

2. We know that are both pre-built AI and custom AI options available. We are confused as to when to choose one over the other.

3. We expect some part of our solution would require deep learning. Do you have any prescriptive guidance on how we might choose between investing in learning and using TensorFlow or the Microsoft Cognitive Toolkit (CNTK)?

### Infographic for common scenarios

![In the Training a classification model with text diagram, Document labels points to Supervised ML or DL Algorithm, which points to Classification Model. Documents points to Text Normalization, which points to Feature Extraction, which points to Supervised ML or DL Algorithm. Vectors points to a table of words and percentages.](images/Whiteboarddesignsessiontrainerguide-CognitiveServicesanddeeplearningimages/media/image2.png "Training a classification model with text diagram")

![The Predicting a classification from text diagram has Documents, which points to Text Normalization, which points to Feature Extraction, which points to Classification Model, which points to Document Labels. Vectors points to a table of words and percentages.](images/Whiteboarddesignsessiontrainerguide-CognitiveServicesanddeeplearningimages/media/image3.png "Predicting a classification from text diagram")

## Step 2: Design a proof of concept solution

**Outcome**

Design a solution and prepare to present the solution to the target customer audience in a 15-minute chalk-talk format.

Timeframe: 60 minutes

**Business needs**

Directions:  With all participants at your table, answer the following questions and list the answers on a flip chart:

1. Who should you present this solution to? Who is your target customer audience? Who are the decision makers?

2. What customer business needs do you need to address with your solution?

**Design**

Directions: With all participants at your table, respond to the following questions on a flip chart:

_High-level architecture_

1. Without getting into the details (the following sections will address the details), diagram your initial vision for handling the top-level requirements for processing the claims textual data, photos, and enabling search. You will refine this diagram as you proceed.

_Classifying claim-text data_

1. What is the general pipeline for approaching the training of text analytic models such as this? What are the general steps you need to take to prepare the text data for performing tasks like classification?

2. What data would they need to train the model?

3. Contoso want to understand some of the common approaches to handle texts for machine learning? Is there a recommended approach to dealing with long descriptive texts that are typically found in claims data?

4. Contoso understands they should use a classification algorithm for this problem. They have asked if a Deep Neural Network could be trained against the text to recognize home or auto classifications. Could they use a DNN for this?

5. For this scenario, Contoso has indicated an interest in using TensorFlow, but is concerned about the complexity of jumping right in. They are wondering if Keras would provide an easier framework they could use as a stepping stone to the full blown TensorFlow, that would enable them to build TensorFlow compatible models so that they can "graduate" to using TensorFlow when the team is ready?

6. What would a LSTM recurrent neural network that performs this classification look like? Show a snippet of a single layer of an unrolled LSTM network, and the binary classification output at the last step of the network.

7. Assuming they will be using a LSTM recurrent neural network to train the classifier using Keras, pseudo code the code you would write to construct the network you just illustrated.

8. Next, pseudo code how they would define the optimizer, loss function and fit the model to the vectorized data and the labels.

9. With the trained model in hand, pseudo code how the model would be used to predict the class of a given claim text. What would the output of the prediction be? How would you interpret the value?

10. Describe at a high level, how you would deploy this trained model, so it is available as a web service that can be integrated with the rest of the solution.

_Identifying free-text sentiment_

1. How would you recommend Contoso identify the sentiment in the free-response text provided associated with a claim? Would this require you to build a custom AI model? Is there a pre-built AI service you could use?

2. For the solution you propose, what is the range of value of the sentiment score and how would you interpret that value?

_Summarizing claim text_

1. The team at Contoso has heard about a Python library called Gensim that has a summarize function. Given an input of text, it can extract a summary of the desired length. Contoso would like their PoC to implement its summarization functionality initially using Gensim. However, the process they follow to deploy the summarization capability should also enable them to replace the use of Gensim with another library or with the use of their own custom trained models if desired down the road. Describe how Contoso should deploy the summarization service to meet these requirements?

2. Can they deploy a predictive web service to Azure Machine Learning service that does not utilize an external model (as in the case with Gensim) or would support an unsupervised approach?

_Captions, tags and "reading" images_

1. How would you recommend Contoso implement support for automatically creating captions for the claim photos? Similarly, how would they automatically generate tags? Would this require you to build a custom AI model? Is there a pre-built AI service you could use?

2. Describe the flow of processing of an image as input; what value is returned by each component in your proposed solution for captioning and tagging images?

3. How would you recommend Contoso implement support for "reading" any text that appears within an image, so that it could be searched later? Would this require you to build a custom AI model? Is there a pre-built AI service you could use?

4. Describe the flow of processing of an image as input; what value is returned by each component in your proposed solution for "reading" images?

_Enabling search_

1. What service would you recommend Contoso leverage to enable greater searchability over the claim data, inclusive of the new data fields created by your text processing and image processing components?

2. Would they be able to keep their claims data in the existing database and layer in this search capability? If so, explain how.

**Prepare**

Directions: With all participants at your table:

1. Identify any customer needs that are not addressed with the proposed solution.

2. Identify the benefits of your solution.

3. Determine how you will respond to the customer's objections.

Prepare a 15-minute chalk-talk style presentation to the customer.

## Step 3: Present the solution

**Outcome**

Present a solution to the target customer audience in a 15-minute chalk-talk format.

Timeframe: 30 minutes

**Presentation**

Directions:

1. Pair with another table.

2. One table is the Microsoft team and the other table is the customer.

3. The Microsoft team presents their proposed solution to the customer.

4. The customer makes one of the objections from the list of objections.

5. The Microsoft team responds to the objection.

6. The customer team gives feedback to the Microsoft team.

7. Tables switch roles and repeat Steps 2-6.

## Wrap-up

Timeframe: 15 minutes

Directions: Tables reconvene with the larger group to hear the facilitator/SME share the preferred solution for the case study.

## Additional references

|                                                       |                                                                                                   |
| ----------------------------------------------------- | ------------------------------------------------------------------------------------------------- |
| **Description**                                       | **Links**                                                                                         |
| Azure Machine Learning service                        | <https://docs.microsoft.com/en-us/azure/machine-learning/service/overview-what-is-azure-ml>       |  |
| Deploying Web Services                                | <https://docs.microsoft.com/en-us/azure/machine-learning/service/how-to-deploy-and-where> |
| Overview of Keras                                   | <https://keras.io/> |
| Overview of TensorFlow                                | <https://www.tensorflow.org/> |
| Term Frequency-Inverse Document Frequency (TF-IDF) vectorization | <https://en.wikipedia.org/wiki/Tf-idf> |
| GloVe: Global Vectors for Word Representation | <https://nlp.stanford.edu/projects/glove/>  |
| Research Paper: "GloVe: Global Vectors for Word Representation" | <https://nlp.stanford.edu/pubs/glove.pdf>  |
| Word2vec word embeddings | <https://en.wikipedia.org/wiki/Word2vec>  |
| Overview of the Computer Vision API Cognitive Service | <https://docs.microsoft.com/en-us/azure/cognitive-services/computer-vision/home>                  |
| Overview of the Text Analytics API Cognitive Service  | <https://docs.microsoft.com/en-us/azure/cognitive-services/text-analytics/overview>               |
-->

![Microsoft Cloud Workshop](https://github.com/Microsoft/MCW-Template-Cloud-Workshop/raw/master/Media/ms-cloud-workshop.png "Microsoft Cloud Workshop")

<div class="MCWHeader1">
Cognitive Services と深層学習
</div>

<div class="MCWHeader2">
ホワイトボード設計セッション生徒用ガイド
</div>

<div class="MCWHeader3">
2019 年 12 月
</div>

このドキュメントに記載されている情報 (URL や他のインターネット Web サイト参照を含む) は、将来予告なしに変更することがあります。別途記載されていない場合、このソフトウェアおよび関連するドキュメントで使用している会社、組織、製品、ドメイン名、電子メール アドレス、ロゴ、人物、場所、出来事などの名称は架空のものです。実在する商品名、団体名、個人名などとは一切関係ありません。お客様ご自身の責任において、適用されるすべての著作権関連法規に従ったご使用をお願いいたします。著作権法による制限に関係なく、マイクロソフトの書面による許可なしに、このドキュメントの一部または全部を複製したり、検索システムに保存または登録したり、別の形式に変換したりすることは、手段、目的を問わず禁じられています。ここでいう手段とは、複写や記録など、電子的、または物理的なすべての手段を含みます。

マイクロソフトは、このドキュメントに記載されている内容に関し、特許、特許申請、商標、著作権、またはその他の無体財産権を有する場合があります。別途マイクロソフトのライセンス契約上に明示の規定のない限り、このドキュメントはこれらの特許、商標、著作権、またはその他の知的財産権に関する権利をお客様に許諾するものではありません。

製造元名、製品名、URL は、情報提供のみを目的としており、これらの製造元またはマイクロソフトのテクノロジを搭載した製品の使用について、マイクロソフトは、明示的、黙示的、または法令によるいかなる表明も保証もいたしません。製造元または製品に対する言及は、マイクロソフトが当該製造元または製品を推奨していることを示唆するものではありません。掲載されているリンクは、外部サイトへのものである場合があります。これらのサイトはマイクロソフトの管理下にあるものではなく、リンク先のサイトのコンテンツ、リンク先のサイトに含まれているリンク、または当該サイトの変更や更新について、マイクロソフトは一切責任を負いません。リンク先のサイトから受信した Web キャストまたはその他の形式での通信について、マイクロソフトは責任を負いません。マイクロソフトは受講者の便宜を図る目的でのみ、これらのリンクを提供します。また、リンクの掲載は、マイクロソフトが当該サイトまたは当該サイトに掲載されている製品を推奨していることを示唆するものではありません。

© 2019 Microsoft Corporation. All rights reserved.

Microsoft および <https://www.microsoft.com/en-us/legal/intellectualproperty/Trademarks/Usage/General.aspx> (英語) に掲載されているその他の商標は、マイクロソフト グループ各社の商標です。その他すべての商標は、その所有者に帰属します。

**目次**

<!-- TOC -->

- [Cognitive Services と深層学習ホワイトボード設計セッション生徒用ガイド](#cognitive-services-とディープ-ラーニングホワイトボード設計セッション生徒用ガイド)
  - [概要と学習の目的](#概要と学習の目的)
  - [ステップ 1: 顧客事例の確認](#ステップ-1:-顧客事例の確認)
    - [顧客の状況](#顧客の状況)
    - [顧客のニーズ](#顧客のニーズ)
    - [顧客の反論](#顧客の反論)
    - [一般的なシナリオのインフォグラフィック](#一般的なシナリオのインフォグラフィック)
  - [ステップ 2: 概念実証ソリューションの設計](#ステップ-2:-概念実証ソリューションの設計)
  - [ステップ 3: ソリューションのプレゼンテーション](#ステップ-3:-ソリューションのプレゼンテーション)
  - [まとめ](#まとめ)
  - [参考資料](#参考資料)

<!-- /TOC -->

# Cognitive Services と深層学習ホワイトボード設計セッション生徒用ガイド<a name="cognitive-services-とディープ-ラーニングホワイトボード設計セッション生徒用ガイド"></a>

## 概要と学習の目的<a name="概要と学習の目的"></a>

このホワイトボード設計セッションでは、各種 Cognitive Services として提供されている事前構築済みの人工知能 (AI) と Azure Machine Learning サービスで構築およびデプロイされたカスタム AI サービスの両方を組み合わせたソリューションをグループで設計します。テキスト分析パイプラインの設計と実装を通じて、非構造化テキスト データを処理するインテリジェントなソリューションを作成する方法を学びます。テキスト データの分類に使用されるリカレント ニューラル ネットワークを使用して二項分類器を構築する方法、Azure Machine Learning サービスを使用して複数の種類の予測サービスをデプロイする方法、Cognitive Services の Computer Vision API および Text Analytics API と統合する方法を習得できます。

このホワイトボード設計セッションを修了すると、Azure Machine Learning サービスと Cognitive Services を利用したソリューションを設計するスキルが向上します。

## ステップ 1: 顧客事例の確認<a name="ステップ-1:-顧客事例の確認"></a>

**成果**

顧客のニーズを分析する。

時間: 15 分

指示: セッション参加者全員が集まり、進行役または SME が顧客事例の概要と技術的なヒントを提示します。

1. 自班の参加者とトレーナーが集まります。

2. 生徒用ガイドのステップ 1 ～ 3 の指示をすべて読みます。

3. 班全体で下記の顧客事例を確認します。

### 顧客の状況<a name="顧客の状況"></a>

Contoso Ltd は米国に本社を置く大企業で、米国の一般消費者向けに保険商品を提供しています。同社の商品には傷害健康保険、生命保険、旅行保険、火災保険、自動車保険などがあります。

Contoso では自社保険商品用の次世代プラットフォームの構築を検討しており、その中でも特にクレーム処理に重点的に取り組みたいと考えています。現在、同社では顧客からのクレームを Web サイト、モバイル アプリ、エージェントへの相談により受け付けています。

クレームには以下のような情報が含まれます。

- 保険契約者の情報 (連絡先情報や保険証券番号など)

- クレームの内容を表すフリー テキストの回答 (事故の詳細、その影響、発生時の状況)

- クレームの説明を補完する写真 (事故発生前の保険対象の写真、損害を受けたり盗難に遭った物の写真など)

エージェント (Contoso の従業員や請負業者) がクレーム処理を行う際、提出された個々のクレームの内容を読んで処理するのに時間がかかる、しばらくしてからクレームに返信するときに特定のクレーム成果物を見つけるのが難しいなど、大幅なコスト上昇につながる問題が複数あります。個々のクレームはデータベースに格納されており、フリー テキストの回答やそれを補完する写真などを含むクレームの詳細はわかりづらい添付ファイルとして検索できない形で保管されています。このため、エージェントがクレーム番号や保険契約者の連絡先情報を基にクレームを特定してから手作業で添付ファイルを読み取らなければならないことも珍しくありません。

また、一般的な課題の一部を自動化して解決したいと考えています。CIO の Francine Fischer は、2 つの課題群を AI で解決し、エージェントの能力を強化したいと考えています。

1 つ目の課題群は、フリー テキストの回答への対応に関するものです。最初の課題は、テキストから判断してそれぞれのクレームが火災保険、あるいは自動車保険に関するものかを自動的に分類することです。この分類はクレームの概要に表示されるため、クレームの内容が火災保険だけに関するものなのか、自動車保険だけに関するものなのか、またはその両方を含むものなのかをエージェントがすばやく判断できます。

2 つ目の課題は、クレームのテキストに感情分析を適用できるかどうかをテストすることです。顧客の大部分は冷静 (中立的な感情) であるか多少不機嫌 (比較的悪い感情) であり、クレームのテキストに悪い感情が含まれている場合は状況が特に深刻で、エージェントが迅速に確認することを保証しなければならない場合もあります。

3 つ目の課題は、長文のフリー テキストがあるということです。エージェントが複数のクレームを扱っているときに、探しているクレームの内容がどのようなものだったかを思い出すことが難しい場合があります。そこで Contoso は、長文のクレームを 30 ワード程度の文に要約する自動要約機能をテストしたいと考えています。エージェントは、クレームの処理を再開するときにこの要約を読んで大まかな内容をつかめば、全文を読まなくてもすばやく思い出すことができます。

次の課題群は、提出された写真から情報を抽出するエージェントの能力を強化し、検索の機能を向上させることです。1 つ目の課題は、写真の内容を示すキャプションを自動生成することです。2 つ目は、写真の内容を示すタグを自動で適用することです。3 つ目は、写真の中に含まれるあらゆるテキストを抽出することです。これらの課題を解決すると、エージェントが入力するデータの量を削減しながら、同時に写真が検索しやすくなります。

最後に、写真から抽出された情報を整理し、フリー テキストの回答の処理結果と併せてソリューションと連携させ、簡単に検索できるようにすると共に新しいクレーム情報の取得に対応して常に最新の状態になるようにします。

この大きな目標に向けた第一歩として、上記のすべてを自動化するインテリジェントなソリューションの概念実証版 (PoC) を構築します。同社では、既に Azure で実行しているクレーム提出ソリューション (クレーム提出は Web App で、クレームの保管は SQL Database で構築) の PoC 版を作成したいと考えています。上記の課題は AI、機械学習、ディープ ラーニングを活用すれば解決できると予想しており、これらのテクノロジでどの程度まで実現できるかを PoC 版の構築を通じて把握します。

### 顧客のニーズ<a name="顧客のニーズ"></a>

1. フリー テキストの回答からは有益な情報が大量に得られるが、長文のものもあるため、エージェントが読み飛ばしてきわめて重要な詳細を見落としたり、クレームに返信するときにそのクレームを探すのに長い時間を要したりすることがある。これを自動化できるかどうかはまだ不明だが、標準化されたプロセスでクレーム内の主なエンティティを認識し、エージェントが容易に確認できるように独立したリストに抽出して、クレームの文脈に含まれるエンティティを簡単に見られるようにしたい。

2. 写真を「見て」、その内容を説明し、キーワードを含むタグを付与して、後でその写真が必要なときに容易に探して参照できるようにするソリューションを求めている。

3. エージェントを廃止するわけではなく、エージェントの能力を向上させてクレーム処理能力を強化したい。エージェントと同じ処理を実行できるソリューションを求めている。

### 顧客の反論<a name="顧客の反論"></a>

1. このような「AI」ソリューションに関する過大な評価には疑問がある。現在のテクノロジと Azure で実現可能なことと不可能なことを区別するのが難しい。

2. 事前構築済みの AI を使用する方法とカスタム AI を使用する方法があるが、そのどちらを選べばよいかわかりづらい。

3. ソリューションの一部にはディープ ラーニングの使用が必要になると予想している。TensorFlow や Microsoft Cognitive Toolkit (CNTK) の習得と使用に投資すべきか否かの判断基準となるガイドはないか。

### 一般的なシナリオのインフォグラフィック<a name="一般的なシナリオのインフォグラフィック"></a>

![テキストの分類モデルのトレーニングの図では、ドキュメントのラベルから教師あり ML/DL アルゴリズムに、そこから分類モデルに矢印が伸びる。ドキュメントからテキスト正規化に、そこから特徴抽出に、そこから教師あり ML/DL アルゴリズムに矢印が伸びる。ベクトルから単語一覧とそのパーセンテージの表に矢印が伸びる。](images/Whiteboarddesignsessiontrainerguide-CognitiveServicesanddeeplearningimages/media/image2.png "テキストの分類モデルのトレーニングの図")

![テキストの分類予測の図では、ドキュメントからテキスト正規化に、そこから特徴抽出に、そこから分類モデルに、そこからドキュメントのラベルに矢印が伸びる。ベクトルから単語一覧とそのパーセンテージの表に矢印が伸びる。](images/Whiteboarddesignsessiontrainerguide-CognitiveServicesanddeeplearningimages/media/image3.png "テキストの分類予測の図")

## ステップ 2: 概念実証ソリューションの設計<a name="ステップ-2:-概念実証ソリューションの設計"></a>

**成果**

ソリューションを設計し、15 分の講義形式で提供先の顧客の担当者に行うソリューションのプレゼンテーションに向けて準備する。

時間: 60 分

**ビジネス ニーズ**

指示: 班の参加者全員で以下の質問に回答し、フリップ チャートに回答の一覧を記載します。

1. ソリューションを提案する相手は? 提案先の顧客の担当者は? 意思決定者は?

2. このソリューションで解決が必要な顧客のビジネス ニーズは?

**設計**

指示: 班の参加者全員でフリップ チャートに記載された以下の質問に回答します。

_アーキテクチャの概要_

1. 詳細には触れずに (詳細については後のセクションで扱います)、クレームのテキスト データや写真を処理し検索可能にするための大まかな要件に対応する初期構想を図示します。この図の内容は、進行に合わせて修正します。

_クレーム テキスト データの分類_

1. このようなテキスト分析モデルのトレーニングを実施する場合の一般的な手順、および分類などのタスクを実行するために必要なテキスト データを準備する方法を把握します。

2. モデルのトレーニングに必要なデータの種類を把握します。

3. Contoso が機械学習でテキストを処理する場合の代表的な手法を理解したいと考えているかどうかを確認します。また、クレーム テキスト データでよく見られる長文の説明的なテキストを処理する際に推奨される手法があるかどうかを把握します。

4. Contoso では分類アルゴリズムがこの問題に使用されることを理解していて、火災保険と自動車保険の分類に使用するテキストに対してディープ ニューラル ネットワーク (DNN) をトレーニングできないかという質問を同社から受けました。実際に DNN を使用できるかどうか検討します。

5. このシナリオでは、Contoso は TensorFlow の使用に興味を示していますが、急に使用を開始する場合の煩雑さについて憂慮しています。同社はまず Keras の比較的簡単なフレームワークを使用し、その後充実した機能を備える TensorFlow にステップ アップすることを検討しています。TensorFlow 互換モデルを構築し、チームの準備が整ったら「卒業」して TensorFlow に移行することが可能かどうか検討します。

6. このような分類を実行する LSTM リカレント ニューラル ネットワークについて理解します。展開された LSTM ネットワークの単一層のスニペット、およびネットワークの最後のステップで出力される二項分類の結果を提示します。

7. Keras で LSTM リカレント ニューラル ネットワークを使用して分類器をトレーニングすると仮定して、図のとおりにネットワークを構築するためのコードを擬似コード形式で作成します。

8. 次に、最適化手法と損失関数を定義する方法、およびベクトル化されたデータやラベルにモデルを適合させる方法の擬似コードを作成します。

9. トレーニング済みモデルが得られたら、そのモデルを特定のクレーム テキストのクラスの予測に使用する方法の擬似コードを作成します。どのような予測結果が得られるか、値をどのように解釈するかを理解します。

10. トレーニング済みモデルをデプロイする方法、および Web サービスとしてソリューションの中に統合する方法を大まかに説明します。

_フリー テキストの感情の認識_

1. クレームに対するフリー テキストの回答の感情認識を Contoso に推奨する方法を検討します。カスタム AI モデルが必要かどうか、この課題に使用できる事前構成済みの AI サービスの有無についても検討します。

2. 提案するソリューションにおけるセンチメント スコアの値の範囲、およびその値をどのように解釈するかを決定します。

_クレーム テキストの要約_

1. Contoso チームは、要約関数が実装された Gensim という Python ライブラリの名前は聞いたことがありました。この関数は、テキストを入力すると要約を指定した長さで抽出します。まずは、Gensim を使用してこの要約関数を PoC 版に実装します。しかし、後にデプロイする要約機能では Gensim 以外のライブラリを使用し、将来的には独自開発のカスタマイズされたトレーニング済みモデルの使用も検討しています。要件を満たす要約サービスをデプロイする方法を説明します。

2. 外部モデル (Gensim など) を使用していない Azure Machine Learning サービスに予測 Web サービスをデプロイできるか、教師なし学習をサポートするかどうかを検討します。

_画像のキャプション、タグ、「読み取り」_

1. クレームの写真のキャプションを自動生成する機能の実装を推奨する方法を検討します。同様に、タグの自動生成機能についても検討します。カスタム AI モデルが必要かどうか、この課題に使用できる事前構成済みの AI サービスの有無についても検討します。

2. 画像が入力されたときの処理の流れ、およびチームが提案した、画像のキャプション生成とタグ付与を行うソリューションの各コンポーネントが返す値を説明します。

3. 画像内のあらゆるテキストを「読み取り」、後から検索できるようにする機能の実装を Contoso に推奨する方法を検討します。カスタム AI モデルが必要かどうか、この課題に使用できる事前構成済みの AI サービスの有無についても検討します。

4. 画像が入力されたときの処理の流れ、およびチームが提案した画像「読み取り」ソリューションの各コンポーネントが返す値を説明します。

_検索の機能向上_

1. テキスト処理や画像処理のコンポーネントで作成された新規データ フィールドを含むクレーム データの検索の機能を向上させるサービスについて、どのサービスを Contoso に推奨するかを検討します。

2. クレーム データを既存のデータベースで維持しながらこの検索機能を追加することができるかどうかを確認します。可能であるならば、その方法を説明します。

**準備**

指示: 班の参加者全員と以下を行います。

1. 提案したソリューションでは解決されない顧客のニーズを把握します。

2. ソリューションのメリットを把握します。

3. 顧客の反論に対応する方法を検討します。

15 分の講義形式で顧客に行うソリューションのプレゼンテーションに向けて準備します。

## ステップ 3: ソリューションのプレゼンテーション<a name="ステップ-3:-ソリューションのプレゼンテーション"></a>

**成果**

15 分の講義形式で提供先の顧客の担当者にソリューションのプレゼンテーションを行う。

時間: 30 分

**プレゼンテーション**

指示:

1. 他の班と組みます。

2. 一方の班はマイクロソフト チームを、もう一方の班は顧客を担当します。

3. マイクロソフト チームは、提案するソリューションのプレゼンテーションを顧客に向けて行います。

4. 顧客側は、反論リストの中からいずれかの反論を行います。

5. マイクロソフト チームは反論に対応します。

6. 顧客側はマイクロソフト チームにフィードバックを提供します。

7. 役割を入れ替えてステップ 2 ～ 6 を繰り返します。

## まとめ<a name="まとめ"></a>

時間: 15 分

指示: 各班が集まり、進行役や SME が事例に適したソリューションを発表します。

## 参考資料<a name="参考資料"></a>

|                                                       |                                                                                                   |
| ----------------------------------------------------- | ------------------------------------------------------------------------------------------------- |
| **説明**                                       | **リンク**                                                                                         |
| Azure Machine Learning サービス                        | <https://docs.microsoft.com/ja-jp/azure/machine-learning/overview-what-is-azure-ml>       |  |
| Web サービスのデプロイ                                | <https://docs.microsoft.com/ja-jp/azure/machine-learning/how-to-deploy-and-where> |
| Keras の概要                                   | <https://keras.io/> (英語) |
| TensorFlow の概要                               | <https://www.tensorflow.org/> (英語) |
| 単語出現頻度 - 逆文書頻度 (TF-IDF) ベクトル化 | <https://ja.wikipedia.org/wiki/Tf-idf> |
| GloVe: Global Vectors for Word Representation | <https://nlp.stanford.edu/projects/glove/> (英語)  |
| 研究論文: "GloVe: Global Vectors for Word Representation" | <https://nlp.stanford.edu/pubs/glove.pdf> (英語)  |
| Word2vec 単語埋め込み | <https://en.wikipedia.org/wiki/Word2vec> (英語)  |
| Cognitive Service の Computer Vision API の概要 | <https://docs.microsoft.com/ja-jp/azure/cognitive-services/computer-vision/home>                  |
| Cognitive Service の Text Analytics API の概要  | <https://docs.microsoft.com/ja-jp/azure/cognitive-services/text-analytics/overview>               |