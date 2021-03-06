---
title: Azure Security Center での ID とアクセスの監視 | Microsoft Docs
description: Azure Security Center の ID とアクセス機能を使用して、ユーザーのアクセス アクティビティと ID 関連の問題を監視する方法を説明します。
services: security-center
documentationcenter: na
author: memildin
manager: rkarlin
ms.assetid: 9f04e730-4cfa-4078-8eec-905a443133da
ms.service: security-center
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/06/2020
ms.author: memildin
ms.openlocfilehash: 183b81134b2fe72a539cc6460a05d828342aafbb
ms.sourcegitcommit: 20429bc76342f9d365b1ad9fb8acc390a671d61e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/11/2020
ms.locfileid: "79086498"
---
# <a name="monitor-identity-and-access"></a>ID とアクセスを監視する

> [!TIP]
> 2020 年 3 月以降、Azure Security Center の IDとアクセスの推奨事項は、Free 価格レベルのすべてのサブスクリプションに含まれています。 Free レベルのサブスクリプションをお持ちの場合は、これまで ID およびアクセス セキュリティについて評価されていなかったため、セキュリティ スコアが影響を受けます。 

Security Center によって潜在的なセキュリティの脆弱性が識別されると、リソースを堅牢化および保護するために必要な管理を構成するプロセスを説明する推奨事項が作成されます。

セキュリティ境界は、ネットワーク境界から ID 境界へと発展してきました。 セキュリティにおいては、ネットワークの保護よりもデータの保護、アプリとユーザーのセキュリティ管理が重要になってきています。 最近では、クラウドに移行するデータやアプリが増加しているため、ID が新たな境界線となっています。

ID アクティビティを監視することにより、インシデントが発生する前に事前対応型のアクションを実行するか、攻撃が試みられた場合にそれを阻止する事後対応型のアクションを実行することができます。 Azure Security Center の **[Id とアクセス]** リソース セキュリティ セクションに表示される推奨事項の例を次に示します。

- サブスクリプションで所有者アクセス許可を持つアカウントに対して MFA を有効にする必要がある
- 最大 3 人の所有者をサブスクリプションに対して指定する必要がある
- 非推奨のアカウントをサブスクリプションから削除する必要がある
- 読み取りアクセス許可を持つ外部アカウントをサブスクリプションから削除する必要がある

ここに記載されている推奨事項の完全な一覧については、「[ID とアクセスの推奨事項](recommendations-reference.md#recs-identity)」を参照してください。

> [!NOTE]
> サブスクリプションのアカウント数が 600 を超える場合、Security Center はサブスクリプションに対して ID の推奨事項を実行できません。 実行されない推奨事項については、後述する「利用できない評価」を参照してください。
Security Center は、クラウド ソリューション プロバイダー (CSP) パートナーの管理者エージェントに対して ID の推奨事項を実行できません。
>


すべての ID とアクセスの推奨事項は、 **[推奨事項]** ページの 2 つのセキュリティ コントロール内で利用できます。

- アクセスおよびアクセス許可の管理 
- MFA の有効化

![ID とアクセスに関連する推奨事項がある 2 つのセキュリティ コントロール](media/security-center-identity-access/two-security-controls-for-identity-and-access.png)


## <a name="enable-multi-factor-authentication-mfa"></a>多要素認証 (MFA) を有効にする

MFA を有効にするには、[Azure Active Directory (AD) テナントのアクセス許可](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles)が必要です。 

- AD の Premium Edition を使用している場合は、[条件付きアクセス](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)を使用して MFA を有効にします。

- AD Free Edition のユーザーは、[AD のドキュメント](https://docs.microsoft.com/azure/active-directory/fundamentals/concept-fundamentals-security-defaults)に記載されているように、Azure Active Directory 内で**セキュリティの既定値群**を有効にできますが、MFA を有効にするための Security Center 推奨事項は引き続き表示されます。


## <a name="next-steps"></a>次のステップ
その他の Azure リソースの種類に適用される推奨事項の詳細については、次の記事をご覧ください。

- [Azure Security Center でのマシンとアプリケーションの保護](security-center-virtual-machine-protection.md)
- [Azure Security Center でのネットワークの保護](security-center-network-recommendations.md)
- [Azure Security Center での Azure SQL サービスとデータの保護](security-center-sql-service-recommendations.md)