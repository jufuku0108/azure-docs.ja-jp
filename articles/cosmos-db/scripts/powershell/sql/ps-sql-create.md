---
title: Azure Cosmos DB SQL (Core) API のデータベースとコンテナーを作成する PowerShell スクリプト
description: Azure PowerShell script - Azure Cosmos DB SQL (Core) API のデータベースとコンテナーを作成する
author: markjbrown
ms.service: cosmos-db
ms.subservice: cosmosdb-sql
ms.topic: sample
ms.date: 09/20/2019
ms.author: mjbrown
ms.openlocfilehash: 5a57b8cb3e4e7076d3be73a9010d9a29a8b004a3
ms.sourcegitcommit: 0947111b263015136bca0e6ec5a8c570b3f700ff
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/24/2020
ms.locfileid: "75441358"
---
# <a name="create-a-database-and-container-for-azure-cosmos-db---sql-core-api"></a>Azure Cosmos DB - SQL (Core) API のデータベースとコンテナーを作成する

[!INCLUDE [updated-for-az](../../../../../includes/updated-for-az.md)]

[!INCLUDE [sample-powershell-install](../../../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a>サンプル スクリプト

このスクリプトは、2 つのリージョンにセッション レベルの一貫性を持つ SQL (Core) API 用の Cosmos アカウントを作成します。また、共有スループットを持つデータベースを作成します。さらに、パーティション キー、カスタム インデックス ポリシー、一意キー ポリシー、TTL、専用スループット、および `multipleWriteLocations=true` である場合に使用されるカスタム競合解決パスのある最終書き込み者優先競合解決ポリシーを持つコンテナーを作成します。

[!code-powershell[main](../../../../../powershell_scripts/cosmosdb/sql/ps-sql-create.ps1 "Create an account, database, and container for SQL (Core) API")]

## <a name="clean-up-deployment"></a>デプロイのクリーンアップ

スクリプト サンプルの実行後は、次のコマンドを使用してリソース グループとすべての関連リソースを削除することができます。

```powershell
Remove-AzResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a>スクリプトの説明

このスクリプトでは、次のコマンドを使用します。 表内の各コマンドは、それぞれのドキュメントにリンクされています。

| command | メモ |
|---|---|
|**Azure リソース**| |
| [New-AzResource](https://docs.microsoft.com/powershell/module/az.resources/new-azresource) | リソースを作成します。 |
|**Azure リソース グループ**| |
| [Remove-AzResourceGroup](https://docs.microsoft.com/powershell/module/az.resources/remove-azresourcegroup) | 入れ子になったリソースすべてを含むリソース グループを削除します。 |
|||

## <a name="next-steps"></a>次のステップ

Azure PowerShell の詳細については、[Azure PowerShell のドキュメント](https://docs.microsoft.com/powershell/)を参照してください。

Azure Cosmos DB のその他の PowerShell サンプル スクリプトについては、[Azure Cosmos DB の PowerShell スクリプト](../../../powershell-samples.md)に関する記事をご覧ください。
