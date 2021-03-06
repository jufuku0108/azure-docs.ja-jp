---
title: 接続アーキテクチャ - Azure Database for MariaDB
description: Azure Database for MariaDB サーバーの接続アーキテクチャについて説明します。
author: kummanish
ms.author: manishku
ms.service: mariadb
ms.topic: conceptual
ms.date: 3/18/2020
ms.openlocfilehash: 4fd6cc2133c6910bace6c36d153085956419b22a
ms.sourcegitcommit: 2ec4b3d0bad7dc0071400c2a2264399e4fe34897
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2020
ms.locfileid: "79532368"
---
# <a name="connectivity-architecture-in-azure-database-for-mariadb"></a>Azure Database for MariaDB の接続アーキテクチャ
この記事では、Azure Database for MariaDB 接続アーキテクチャと、Azure 内外の両方のクライアントからトラフィックがどのように Azure Database for MariaDB インスタンスに転送されるかについて説明します。

## <a name="connectivity-architecture"></a>接続のアーキテクチャ

Azure Database for MariaDB への接続は、受信接続を Microsoft のクラスター内にあるお客様のサーバーの物理的な場所にルーティングする役割を果たすゲートウェイを介して確立されます。 次の図に、そのトラフィック フローを示します。

![接続アーキテクチャの概要](./media/concepts-connectivity-architecture/connectivity-architecture-overview-proxy.png)

クライアントでは、データベースに接続するときに、ゲートウェイに接続する接続文字列を取得します。 このゲートウェイは、ポート 3306 をリッスンするパブリック IP アドレスを持っています。 データベース クラスター内では、トラフィックは適切な Azure Database for MariaDB に転送されます。 そのため、企業ネットワークなどからサーバーに接続するには、クライアント側のファイアウォールを開いて送信トラフィックがゲートウェイに到達できるようにする必要があります。 リージョンごとに Microsoft のゲートウェイで使用されている IP アドレスの完全な一覧を次に示します。

## <a name="azure-database-for-mariadb-gateway-ip-addresses"></a>Azure Database for MariaDB ゲートウェイの IP アドレス

次の表は、すべてのデータ リージョンの Azure Database for MariaDB ゲートウェイのプライマリ IP とセカンダリ IP を一覧にまとめたものです。 プライマリ IP アドレスはゲートウェイの現行 IP アドレスであり、セカンダリ IP アドレスはプライマリでエラーが発生した場合のフェールオーバー IP アドレスになります。 前述のように、お客様が両方の IP アドレスへの送信を許可する必要があります。 セカンダリ IP アドレスは、接続を受け入れるために Azure Database for MariaDB によりアクティブにされるまで、いかなるサービスでもリッスンしません。

| **リージョン名** | **ゲートウェイ IP アドレス** |
|:----------------|:-------------|
| オーストラリア中部| 20.36.105.0     |
| オーストラリア中部 2     | 20.36.113.0     |
| オーストラリア東部 | 13.75.149.87、40.79.161.1     |
| オーストラリア東南部 |191.239.192.109、13.73.109.251     |
| ブラジル南部 | 104.41.11.5、191.233.201.8、191.233.200.16     |
| カナダ中部 |40.85.224.249     |
| カナダ東部 | 40.86.226.166     |
| 米国中部 | 23.99.160.139、13.67.215.62     |
| 中国東部 2 | 40.73.82.1     |
| 中国北部 2 | 40.73.50.0     |
| 東アジア | 191.234.2.139、52.175.33.150、13.75.33.20、13.75.33.21     |
| East US | 40.121.158.30、191.238.6.43     |
| 米国東部 2 |40.79.84.180、191.239.224.107、52.177.185.181     |
| フランス中部 | 40.79.137.0、40.79.129.1     |
| ドイツ中部 | 51.4.144.100     |
| ドイツ北東部 | 51.5.144.179     |
| インド中部 | 104.211.96.159     |
| インド南部 | 104.211.224.146     |
| インド西部 | 104.211.160.80     |
| 東日本 | 13.78.61.196、191.237.240.43     |
| 西日本 | 104.214.148.156、191.238.68.11、40.74.96.6、40.74.96.7     |
| 韓国中部 | 52.231.32.42     |
| 韓国南部 | 52.231.200.86     |
| 米国中北部 | 23.96.178.199、23.98.55.75、52.162.104.35、52.162.104.36     |
| 北ヨーロッパ | 40.113.93.91、191.235.193.75     |
| 南アフリカ北部  | 102.133.152.0     |
| 南アフリカ西部    | 102.133.24.0     |
| 米国中南部 |13.66.62.124、23.98.162.75、20.45.120.0、104.214.16.39     |
| 東南アジア | 104.43.15.0、23.100.117.95、40.78.233.2、23.98.80.12     |
| アラブ首長国連邦中部 | 20.37.72.64     |
| アラブ首長国連邦北部 | 65.52.248.0     |
| 英国南部 | 51.140.184.11     |
| 英国西部 | 51.141.8.11     |
| 米国中西部 | 13.78.145.25     |
| 西ヨーロッパ | 40.68.37.158、191.237.232.75     |
| 米国西部 | 104.42.238.205、23.99.34.75     |
| 米国西部 2 | 13.66.226.202     |
||||

## <a name="next-steps"></a>次のステップ

* [Azure portal を使用した Azure Database for MariaDB ファイアウォール規則の作成と管理](./howto-manage-firewall-portal.md)
* [Azure CLI を使用した Azure Database for MariaDB ファイアウォール規則の作成と管理](./howto-manage-firewall-cli.md)
