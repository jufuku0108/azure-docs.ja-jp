---
title: オートパイロット モードで Azure Cosmos のコンテナーとデータベースを作成します。
description: オートパイロット モードでの Azure Cosmos のデータベースとコンテナーの利点、ユース ケース、およびプロビジョニング方法について説明します。
author: kirillg
ms.author: kirillg
ms.service: cosmos-db
ms.topic: conceptual
ms.date: 11/04/2019
ms.openlocfilehash: 89af30788fe5129cddc6a3607b8c722549b610d1
ms.sourcegitcommit: 2ec4b3d0bad7dc0071400c2a2264399e4fe34897
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2020
ms.locfileid: "79225679"
---
# <a name="create-azure-cosmos-containers-and-databases-in-autopilot-mode-preview"></a>オートパイロット モードで Azure Cosmos のコンテナーとデータベースを作成する (プレビュー)

Azure Cosmos DB を使用すると、手動モードまたはオートパイロット モードでコンテナーにスループットをプロビジョニングできます。 この記事では、オートパイロット モードの利点とユース ケースについて説明します。

> [!NOTE]
> 現在、オートパイロット モードはパブリック プレビューで利用できます。 [オートパイロットは、新しいデータベースおよびコンテナーに対してのみ有効にできます](#create-a-database-or-a-container-with-autopilot-mode)。 既存のコンテナーおよびデータベースでは使用できません。

スループットの手動プロビジョニングに加えて、オートパイロット モードでも Azure Cosmos のコンテナーを構成できるようになりました。 オートパイロット モードで構成されたコンテナーとデータベースは、**ワークロードの可用性、待機時間、スループット、またはパフォーマンスに影響を与えることなく、アプリケーションのニーズに基づいて、プロビジョニングされているスループットを自動的かつ即座にスケーリングします。**

オートパイロット モードでコンテナーとデータベースを構成するときは、超えてはならない最大スループット `Tmax` を指定する必要があります。 コンテナーは、`0.1*Tmax < T < Tmax` するようにスループットをスケーリングできます。 つまり、コンテナーとデータベースは、構成した最大スループット値の 10% から、構成した最大スループット値までの範囲で、ワークロードのニーズに基づいて瞬時にスケーリングされます。 オートパイロットのデータベースまたはコンテナーでの最大スループット (`Tmax`) の設定は、いつでも変更できます。 オートパイロット オプションでは、コンテナーまたはデータベースごとに 400 RU/秒の最小スループットが適用されなくなりました。

オートパイロットのプレビュー中、コンテナーまたはデータベースに指定された最大スループットについて、システムは計算されたストレージの制限内で操作を許可します。 ストレージの上限を超えた場合、最大スループットは自動的に、より高い値に調整されます。 オートパイロット モードでデータベース レベルのスループットを使用する場合、データベース内で許可されるコンテナーの数は `0.001*TMax` として計算されます。 たとえば、20,000 オートパイロット RU/秒をプロビジョニングする場合、データベースは 20 個のコンテナーを持つことができます。

## <a name="benefits-of-autopilot-mode"></a>オートパイロット モードの利点

オートパイロット モードで構成されている Azure Cosmos コンテナーには、次の利点があります。

* **Simple の場合:** オートパイロット モードのコンテナーでは、さまざまなコンテナーに対するプロビジョニング済みスループット (RU) と容量を手動で管理する複雑さがなくなります。

* **スケーラブル:** オートパイロット モードのコンテナーでは、必要に応じて、プロビジョニング済みスループットの容量がシームレスにスケーリングされます。 クライアント接続やアプリケーションが中断されることはなく、既存の SLA が影響を受けることもありません。

* **コスト効率:** オートパイロット モードで構成されたコンテナーを使用する場合は、ワークロードで必要とされるリソースに対してのみ、時間単位で課金されます。

* **高可用性:** オートパイロット モードのコンテナーでは、グローバルに分散されたフォールト トレラントな高可用性の同じバックエンドが使用され、データの持続性と高可用性が保証されます。

## <a name="use-cases-of-autopilot-mode"></a>オートパイロット モードのユース ケース

オートパイロット モードで構成された Azure Cosmos コンテナーには、次のようなユース ケースがあります。

* **変動するワークロード:** 使用のピークが 1 時間から数時間で 1 日または 1 年に数回という使用量の少ないアプリケーションを実行している場合。 たとえば、人事、予算、運用レポートのためのアプリケーションなどです。 そのようなシナリオでは、オートパイロット モードで構成されたコンテナーを使用でき、ピーク時または平均の容量に対して手動でプロビジョニングする必要がなくなります。

* **予測できないワークロード:** 1 日を通してデータベースが使用されるが、アクティビティのピークを予測するのが困難なワークロードを実行している場合。 たとえば、天気予報が変化したときにアクティビティが急増する交通情報サイトなどです。 オートパイロット モードで構成されたコンテナーでは、アプリケーションのピーク時の負荷のニーズに合わせて容量が調整され、アクティビティの急増が終わるとスケールダウンして戻されます。

* **新しいアプリケーション:** 新しいアプリケーションをデプロイしていて、必要なプロビジョニング済みスループットの量 (RU の数) がわからない場合。 オートパイロット モードで構成されたコンテナーを使用すると、容量のニーズとアプリケーションの要件に合わせて自動的にスケーリングできます。

* **使用頻度の低いアプリケーション:** 1 日、1 週間、または 1 か月の間に数回、数時間だけ使用されるアプリケーションがある場合 (低ボリュームのアプリケーション/Web/ブログ サイトなど)。

* **開発およびテスト用データベース:** 勤務時間中にコンテナーを使用するが、夜間や週末には不要な開発者がいる場合。 オートパイロット モードで構成されたコンテナーでは、使用されていないときは最小容量にスケールダウンされます。

* **スケジュールされた運用ワークロード/クエリ:** 1 つのコンテナーに対して一連のスケジュールされた要求/操作/クエリがあり、完全に低スループットで実行するアイドル期間がある場合は、これを簡単に行うことができます。 スケジュールされたクエリ/要求が、オートパイロット モードで構成されたコンテナーに送信されると、コンテナーは必要に応じて自動的にスケールアップされ、操作が実行されます。

このような問題に対する以前の解決策では、実装に膨大な時間が必要になるだけでなく、構成やコードの複雑さが増し、対処するために手動で介入することが頻繁に必要です。 オートパイロット モードでは、何もしなくても上のようなシナリオが実現されるので、これらの問題について心配する必要がなくなります。

## <a name="comparison--containers-configured-in-manual-mode-vs-autopilot-mode"></a>比較 – 手動モードで構成されたコンテナーとオートパイロット モードで構成されたコンテナー

|  | 手動モードで構成されたコンテナー  | オートパイロット モードで構成されたコンテナー |
|---------|---------|---------|
| **プロビジョニング済みスループット** | 手動でプロビジョニングします。 | ワークロードの使用パターンに基づいて、自動的に瞬時にスケーリングされます。 |
| **要求/操作のレート制限 (429)**  | 使用量がプロビジョニング済みの容量を超えた場合、発生する可能性があります。 | 使用されたスループットが、オートパイロット モードで選択した最大スループット以下である場合、発生しません。   |
| **容量計画** |  初期容量計画を行い、必要なスループットをプロビジョニングする必要があります。 |    容量計画について心配する必要はありません。 容量計画と容量管理は、システムによって自動的に行われます。 |
| **料金** | 手動でプロビジョニングされた 1 時間あたりの RU/秒。 | 単一書き込みリージョン アカウントでは、1 時間あたりのオートパイロット RU/秒レートを使用して、時間単位でスループット使用量に対して支払います。 <br/><br/>複数の書き込みリージョンがあるアカウントの場合、オートパイロットに対する追加料金は発生しません。 1 時間あたりの同じマルチマスター RU/秒レートを使用して、時間単位でスループット使用量に対して支払います。 |
| **最適なワークロードの種類** |  予測可能で安定したワークロード|   予測不可能で変動するワークロード  |

## <a name="create-a-database-or-a-container-with-autopilot-mode"></a>オートパイロット モードでデータベースまたはコンテナーを作成する

Azure portal を使用して新しいデータベースまたはコンテナーを作成するときに、それらに対してオートパイロットを構成できます。 次の手順を使用して、新しいデータベースまたはコンテナーを作成し、オートパイロットを有効にして、最大スループット (RU/秒) を指定します。

1. [Azure portal](https://portal.azure.com) または [Azure Cosmos DB Explorer](https://cosmos.azure.com/) にサインインします。

1. Azure Cosmos DB アカウントに移動して、 **[データ エクスプローラー]** タブを開きます。

1. **[新しいコンテナー]** を選択します。 データベース、コンテナー、およびパーティション キーの名前を入力します。 **[スループット]** で **[オートパイロット]** オプションを選択し、オートパイロット オプション使用時にデータベースまたはコンテナーが超えてはならない最大スループット (RU/秒) を指定します。

   ![コンテナーの作成とオートパイロット スループットの構成](./media/provision-throughput-autopilot/create-container-autopilot-mode.png)

1. **[OK]** を選択します。

**[Provision database throughput]\(データベース スループットのプロビジョニング\)** オプションを選択すると、オートパイロット モードで共有スループット データベースを作成できます。

## <a name="throughput-and-storage-limits-for-autopilot"></a><a id="autopilot-limits"></a> オートパイロットのスループットとストレージ制限

次の表は、オートパイロット モードでのさまざまなオプションの最大スループットとストレージ制限を示しています。

|最大スループット制限  |最大ストレージ制限  |
|---------|---------|
|4000 RU/秒  |   50 GB    |
|20,000 RU/秒  |  200 GB  |
|100,000 RU/秒    |  1 TB (テラバイト)   |
|500,000 RU/秒    |  5 TB  |

## <a name="next-steps"></a>次のステップ

* [オートパイロットの FAQ](autopilot-faq.md)を確認する。
* [論理パーティション](partition-data.md)の詳細を確認する。
* [Azure Cosmos コンテナーのスループットをプロビジョニングする](how-to-provision-container-throughput.md)方法を確認する。
* [Azure Cosmos データベースのスループットをプロビジョニングする](how-to-provision-database-throughput.md)方法を確認する。
