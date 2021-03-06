---
title: Azure Cosmos DB のマルチマスターの利点
description: Azure Cosmos DB のマルチマスターの利点を紹介し、1 つの書き込み場所と複数の書き込み場所における待ち時間と SLA 要件を比較します。
author: markjbrown
ms.service: cosmos-db
ms.topic: conceptual
ms.date: 12/02/2019
ms.author: mjbrown
ms.openlocfilehash: b21b6ba82ba1ada0103501b8beeca270df86abd9
ms.sourcegitcommit: 2ec4b3d0bad7dc0071400c2a2264399e4fe34897
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/27/2020
ms.locfileid: "74872011"
---
# <a name="understand-multi-master-benefits-in-azure-cosmos-db"></a>Azure Cosmos DB のマルチマスターの利点を理解する

Cosmos DB アカウント オペレーターは、アプリケーションの待機時間、可用性、および RTO 要件を保証するために、適切なグローバル分散構成を選択する必要があります。 複数の書き込み場所で構成されている Azure Cosmos アカウントには、1 つの書き込み場所で構成されているアカウントに比べて大きな利点があります。たとえば、99.999% 書き込みの可用性 SLA、99 パーセンタイルの書き込み待機時間が 10 ミリ秒未満、リージョン内障害時に RTO = 0 などです。

## <a name="comparison-of-features"></a>機能の比較

|アプリケーションの要件|複数の書き込み場所|1 つの書き込み場所|Note|
|---|---|---|---|
|P99 の書き込み待機時間 SLA が 10 ミリ秒未満|**はい**|いいえ|1 つの書き込み場所を持つアカウントでは、すべてのリージョンにまたがるネットワーク待機時間が書き込みごとに追加で発生します。|
|P99 の読み取り待機時間 SLA が 10 ミリ秒未満|**はい**|はい| |
|99.999% の書き込み SLA|**はい**|いいえ|1 つの書き込み場所を持つアカウントは、99.99% の SLA を保証しています。|
|RTO = 0|**はい**|いいえ|リージョン内で障害が発生した場合の書き込みのダウン タイムが 0。 1 つの書き込み場所を持つアカウントの RTO は 15 分です。|

## <a name="next-steps"></a>次の手順

それでも Azure Cosmos アカウントで EnableMultipleWriteLocations を無効にしたい場合は、[サポート チケットを開きます](https://azure.microsoft.com/support/create-ticket/)。
