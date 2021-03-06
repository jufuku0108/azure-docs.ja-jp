---
title: SSL - Azure Database for PostgreSQL - 単一サーバー
description: Azure Database for PostgreSQL - 単一サーバーの SSL 接続を構成する方法について説明します。
author: rachel-msft
ms.author: raagyema
ms.service: postgresql
ms.topic: conceptual
ms.date: 03/10/2020
ms.openlocfilehash: 303da4dcb68a79e69254f6610afc0003bf0aa22c
ms.sourcegitcommit: 2ec4b3d0bad7dc0071400c2a2264399e4fe34897
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2020
ms.locfileid: "79477002"
---
# <a name="configure-ssl-connectivity-in-azure-database-for-postgresql---single-server"></a>Azure Database for PostgreSQL (単一サーバー) で SSL 接続を構成する

Azure Database for PostgreSQL では、クライアント アプリケーションを PostgreSQL サービスに接続する際、Secure Sockets Layer (SSL) の使用が優先されます。 データベース サーバーとクライアント アプリケーション間に SSL 接続を適用すると、サーバーとアプリケーション間のデータ ストリームが暗号化されて、中間者 (man in the middle) 攻撃から保護されます。

既定では、PostgreSQL データベース サービスは SSL 接続を要求するように構成されます。 クライアント アプリケーションで SSL 接続がサポートされていない場合は、SSL の要求を無効にすることもできます。

## <a name="enforcing-ssl-connections"></a>SSL 接続の適用

Azure Portal や CLI を使用してプロビジョニングされたすべての Azure Database for PostgreSQL サーバーで、SSL 接続の適用が既定で有効になります。 

同様に、Azure Portal のサーバー下にある [接続文字列] 設定で事前定義された接続文字列には、SSL を使用してデータベース サーバーに接続するための一般的な言語の必須パラメーターが含まれます。 SSL パラメーターはコネクタによって異なります ("ssl=true"、"sslmode=require"、"sslmode=required" など)。

## <a name="configure-enforcement-of-ssl"></a>SSL 適用の構成

必要に応じて、SSL 接続の適用を無効にできます。 Microsoft Azure では、セキュリティ強化のため **[Enforce SSL connection (SSL 接続の適用)]** 設定は常に有効にしておくことをお勧めします。

### <a name="using-the-azure-portal"></a>Azure ポータルの使用

Azure Database for PostgreSQL サーバーにアクセスし、 **[接続のセキュリティ]** をクリックします。 トグル ボタンを使用して、 **[Enforce SSL connection] \(SSL 接続の適用)** 設定を有効または無効にします。 その後、 **[保存]** をクリックします。

![接続のセキュリティ ‐ SSL 適用の無効化](./media/concepts-ssl-connection-security/1-disable-ssl.png)

この設定は、 **[概要]** ページの **SSL 適用ステータス** インジケーターで確認できます。

### <a name="using-azure-cli"></a>Azure CLI の使用

**ssl-enforcement** パラメーターを有効または無効にするには、Azure CLI でそれぞれ `Enabled` 値と `Disabled` 値を使用します。

```azurecli
az postgres server update --resource-group myresourcegroup --name mydemoserver --ssl-enforcement Enabled
```

## <a name="ensure-your-application-or-framework-supports-ssl-connections"></a>アプリケーションまたはフレームワークが SSL 接続をサポートしているかどうかの確認

データベース サービスに PostgreSQL を使用しているアプリケーション フレームワークの中には、インストール時に既定で SSL が有効にならないものもあります。 PostgreSQL サーバーが SSL 接続を適用していても、アプリケーションで SSL が構成されていない場合、アプリケーションはデータベース サーバーに接続できない可能性があります。 SSL 接続を有効にする方法については、使用しているアプリケーションのドキュメントを参照してください。

## <a name="applications-that-require-certificate-verification-for-ssl-connectivity"></a>SSL 接続で証明書検証を必要とするアプリケーション

安全に接続するために、信頼された証明機関 (CA) 証明書ファイル (.cer) から生成されたローカルの証明書ファイルがアプリケーションに必要な場合があります。 Azure Database for PostgreSQL サーバーに接続するための証明書は、 https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem にあります。 証明書ファイルをダウンロードし、希望の場所に保存します。

### <a name="connect-using-psql"></a>psql を使用した接続

次の例は、psql コマンド ライン ユーティリティを使用して PostgreSQL サーバーに接続する方法を示しています。 `sslmode=verify-full` 接続文字列設定を使用して、SSL 証明書の検証を適用します。 ローカルの証明書ファイルのパスを `sslrootcert` パラメーターに渡します。

次のコマンドは、psql 接続文字列の例です。

```shell
psql "sslmode=verify-full sslrootcert=BaltimoreCyberTrustRoot.crt host=mydemoserver.postgres.database.azure.com dbname=postgres user=myusern@mydemoserver"
```

> [!TIP]
> `sslrootcert` に渡された値が、保存済みの証明書のファイル パスと一致することを確認します。

## <a name="next-steps"></a>次のステップ

[Azure Database for PostgreSQL の接続ライブラリ](concepts-connection-libraries.md)に関する記事で、さまざまなアプリケーション接続オプションを確認します。
