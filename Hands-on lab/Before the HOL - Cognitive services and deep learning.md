<!--
![Microsoft Cloud Workshops](https://github.com/Microsoft/MCW-Template-Cloud-Workshop/raw/master/Media/ms-cloud-workshop.png 'Microsoft Cloud Workshops')

<div class="MCWHeader1">
Cognitive services and deep learning
</div>

<div class="MCWHeader2">
Before the hands-on lab setup guide
</div>

<div class="MCWHeader3">
December 2019
</div>

Information in this document, including URL and other Internet Web site references, is subject to change without notice. Unless otherwise noted, the example companies, organizations, products, domain names, e-mail addresses, logos, people, places, and events depicted herein are fictitious, and no association with any real company, organization, product, domain name, e-mail address, logo, person, place or event is intended or should be inferred. Complying with all applicable copyright laws is the responsibility of the user. Without limiting the rights under copyright, no part of this document may be reproduced, stored in or introduced into a retrieval system, or transmitted in any form or by any means (electronic, mechanical, photocopying, recording, or otherwise), or for any purpose, without the express written permission of Microsoft Corporation.

Microsoft may have patents, patent applications, trademarks, copyrights, or other intellectual property rights covering subject matter in this document. Except as expressly provided in any written license agreement from Microsoft, the furnishing of this document does not give you any license to these patents, trademarks, copyrights, or other intellectual property.

The names of manufacturers, products, or URLs are provided for informational purposes only and Microsoft makes no representations and warranties, either expressed, implied, or statutory, regarding these manufacturers or the use of the products with any Microsoft technologies. The inclusion of a manufacturer or product does not imply endorsement of Microsoft of the manufacturer or product. Links may be provided to third party sites. Such sites are not under the control of Microsoft and Microsoft is not responsible for the contents of any linked site or any link contained in a linked site, or any changes or updates to such sites. Microsoft is not responsible for webcasting or any other form of transmission received from any linked site. Microsoft is providing these links to you only as a convenience, and the inclusion of any link does not imply endorsement of Microsoft of the site or the products contained therein.

© 2019 Microsoft Corporation. All rights reserved.

Microsoft and the trademarks listed at <https://www.microsoft.com/en-us/legal/intellectualproperty/Trademarks/Usage/General.aspx> are trademarks of the Microsoft group of companies. All other trademarks are property of their respective owners.

**Contents**
-->
<!-- TOC -->
<!--
- [Cognitive services and deep learning before the hands-on lab setup guide](#cognitive-services-and-deep-learning-before-the-hands-on-lab-setup-guide)
  - [Requirements](#requirements)
  - [Before the hands-on lab](#before-the-hands-on-lab)
- [Cognitive Services と深層学習に関するハンズオン ラボの事前セットアップ ガイド<a name="cognitive-services-と深層学習に関するハンズオン-ラボの事前セットアップ-ガイド"></a>](#cognitive-services-%e3%81%a8%e6%b7%b1%e5%b1%a4%e5%ad%a6%e7%bf%92%e3%81%ab%e9%96%a2%e3%81%99%e3%82%8b%e3%83%8f%e3%83%b3%e3%82%ba%e3%82%aa%e3%83%b3-%e3%83%a9%e3%83%9c%e3%81%ae%e4%ba%8b%e5%89%8d%e3%82%bb%e3%83%83%e3%83%88%e3%82%a2%e3%83%83%e3%83%97-%e3%82%ac%e3%82%a4%e3%83%89)
  - [前提条件<a name="前提条件"></a>](#%e5%89%8d%e6%8f%90%e6%9d%a1%e4%bb%b6)
  - [ハンズオン ラボを始める前に<a name="ハンズオン-ラボを始める前に"></a>](#%e3%83%8f%e3%83%b3%e3%82%ba%e3%82%aa%e3%83%b3-%e3%83%a9%e3%83%9c%e3%82%92%e5%a7%8b%e3%82%81%e3%82%8b%e5%89%8d%e3%81%ab)
-->
<!-- /TOC -->
<!--
# Cognitive services and deep learning before the hands-on lab setup guide

## Requirements

1. Microsoft Azure subscription must be pay-as-you-go or MSDN

 - Trial subscriptions will not work. You will run into issues with Azure resource quota limits.

 - Subscriptions with access limited to a single resource group will not work. You will need the ability to deploy multiple resource groups.

2. Azure Notebooks account

 - In your browser, navigate to <https://notebooks.azure.com>.

 - Select Sign In from the top, right corner and sign in using your Microsoft Account credentials. After a successful login, you will have implicitly created the account and are ready to continue.

## Before the hands-on lab

This lab does not have any additional setup that needs to be completed before the lab.
-->


![Microsoft Cloud Workshops](https://github.com/Microsoft/MCW-Template-Cloud-Workshop/raw/master/Media/ms-cloud-workshop.png 'Microsoft Cloud Workshops')

<div class="MCWHeader1">
Cognitive Services と深層学習
</div>

<div class="MCWHeader2">
ハンズオン ラボの事前セットアップ ガイド
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

<!-- TOC -->

- [Cognitive Services と深層学習に関するハンズオン ラボの事前セットアップ ガイド](#cognitive-services-と深層学習に関するハンズオン-ラボの事前セットアップ-ガイド)
  - [前提条件](#前提条件)
  - [ハンズオン ラボを始める前に](#ハンズオン-ラボを始める前に)

<!-- /TOC -->

# Cognitive Services と深層学習に関するハンズオン ラボの事前セットアップ ガイド<a name="cognitive-services-と深層学習に関するハンズオン-ラボの事前セットアップ-ガイド"></a>

## 前提条件<a name="前提条件"></a>

1. Microsoft Azure サブスクリプションが従量課金制または MSDN であること

 - 試用版のサブスクリプションは使用できません。Azure のリソースのクォータ制限に関連した問題が発生します。

 - 単一のリソース グループだけにしかアクセスできないサブスクリプションは使用できません。複数のリソース グループを展開できる必要があります。

2. Azure Notebooks のアカウント

 - ブラウザーで、<https://notebooks.azure.com> (英語) に移動します。

 - 右上の [Sign In (サインイン)] を選択し、Microsoft アカウントの資格情報でサインインします。ログインが完了すると、ユーザーが意識することなくアカウントが作成され、作業の準備が整います。

## ハンズオン ラボを始める前に<a name="ハンズオン-ラボを始める前に"></a>

このラボには、事前にセットアップしておくべきことは他にありません。