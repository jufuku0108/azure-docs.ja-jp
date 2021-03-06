---
title: Power BI アプリ オファーの技術情報 | Azure Marketplace
description: Microsoft AppSource Marketplace 用に Power BI アプリ オファーに技術情報フィールドを構成する。
author: dsindona
ms.service: marketplace
ms.subservice: partnercenter-marketplace-publisher
ms.topic: conceptual
ms.date: 04/24/2019
ms.author: dsindona
ms.openlocfilehash: ab84cc2f4910d1186e842758df7814ca5dd6464d
ms.sourcegitcommit: 2ec4b3d0bad7dc0071400c2a2264399e4fe34897
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2020
ms.locfileid: "80281648"
---
# <a name="power-bi-apps-technical-info-tab"></a>Power BI アプリの [技術的情報] タブ

**[新しいオファー]** ページ上の **[技術情報]** タブを使用して、Power BI インストーラー パッケージの URL と新しいオファーを検証するために必要なその他の情報を指定します。  初期リリースでは、すべての Power BI アプリは無料で、AppSource からのダウンロードが可能です。 このため、このオファーの種類に対して Stock Keeping Unit (SKU) を定義することはできません。

![[技術情報] タブ](./media/technical-info-tab.png)


## <a name="technical-info-fields"></a>技術情報のフィールド 

**[技術情報]** タブ上で、次の表に示したフィールドを入力します。 フィールド ラベルの末尾のアスタリスク (*) は、そのフィールドが必須であることを意味しています。

|        フィールド          |  説明                                                                 |
|    ---------------    |  ----------------------------------------------------------------------------|
| **Installer URL\(インストーラー URL\)\***     | Power BI では、アプリを発行して運用環境に昇格するときに、この URL を生成します。  詳しくは、「[Power BI でダッシュボードとレポートを含むアプリを発行する](https://docs.microsoft.com/power-bi/service-create-distribute-apps)」をご覧ください。  |
|  **Validation instructions\(検証手順\)**  |  Microsoft 検証チームがアプリを構成、接続、テストできるように、必要に応じて手順 (最大 3,000 文字) を追加します。 [データに接続] オプションをテストするために使用できる一般的な構成設定、アカウント、パラメーター、またはその他の情報を含めます。 この情報は、検証チームだけに表示され、検証目的のみに使用されます。  |
| **Is this app created as a Power BI content pack?\(このアプリは、Power BI コンテンツ パックとして作成されていますか?\)** | 現時点では、このフィールドは内部のみで使用されています。 既定の設定である **[いいえ]** のままにしておきます。 設定を **[はい]** に変更すると、発行プロセスが停止される可能性があります。  |  
|  |  |


## <a name="next-steps"></a>次のステップ

[[電子店舗の詳細]](./cpp-storefront-details-tab.md) タブ上で、アプリに関するマーケティングおよび法的な情報を入力します。

