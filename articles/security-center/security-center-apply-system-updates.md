---
title: Azure Security Center でシステムの更新プログラムを適用する | Microsoft Docs
description: このドキュメントでは、Azure Security Center の推奨事項である "**システムの更新プログラムを適用する**" と "**システムの更新後に再起動する**" を実装する方法について説明します。
services: security-center
documentationcenter: na
author: memildin
manager: rkarlin
ms.assetid: e5bd7f55-38fd-4ebb-84ab-32bd60e9fa7a
ms.service: security-center
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/28/2018
ms.author: memildin
ms.openlocfilehash: 3f27753b0775f44cbdf9d4c478a19e423b8e1f19
ms.sourcegitcommit: 2ec4b3d0bad7dc0071400c2a2264399e4fe34897
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2020
ms.locfileid: "77604557"
---
# <a name="apply-system-updates-in-azure-security-center"></a>Azure Security Center でシステムの更新プログラムを適用する
Azure Security Center では、オペレーティング システムに不足している更新プログラムがないかどうかを確認するために、Windows および Linux 仮想マシン (VM) およびコンピューターの監視が毎日行われています。 Security Center は、Windows コンピューターに構成されているサービスに応じて、Windows Update または Windows Server Update Services (WSUS) から利用可能なセキュリティ更新プログラムと重要な更新プログラムの一覧を取得します。 また、Linux システムにおける最新の更新プログラムについても確認します。 VM またはコンピューターでシステムの更新プログラムが不足している場合、Security Center は、それらを適用することを推奨します。

## <a name="implement-the-recommendation"></a>推奨事項の実装
システムの更新プログラムの適用は、Security Center に推奨事項として表示されます。 VM またはコンピューターでシステムの更新プログラムが不足している場合、この推奨事項は、 **[推奨事項]** と **[コンピューティング]** に表示されます。  推奨事項を選択すると、 **[システムの更新プログラムを適用する]** ダッシュボードが開きます。

この例では、 **[コンピューティング]** を使用します。

1. Security Center のメイン メニューの **[コンピューティング]** を選択します。

   ![[コンピューティング] を選択する][1]

2. **[コンピューティング]** で、 **[不足しているシステムの更新]** を選択します。 **[システムの更新プログラムを適用する]** ダッシュボードが開きます。

   ![[システムの更新プログラムを適用する] ダッシュボード][2]

   ダッシュボードの上部には、次の情報が表示されます。

    - システムの更新が不足している Windows および Linux VM およびコンピューターの合計数。
    - VM とコンピューター全体で不足している重要な更新プログラムの合計数。
    - VM とコンピューター全体で不足しているセキュリティ更新プログラムの合計数。

   ダッシュボードの下部には、VM とコンピューターのすべての不足している更新プログラムと、インストールされていない更新プログラムの重要度が一覧表示されます。  一覧には次の項目が含まれています。

    - 名前: 不足している更新プログラムの名前。
    - なし [VM とコンピューターの数]\:この更新プログラムが適用されていない VM とコンピューターの合計台数です。
    - [状態]:推奨事項の現在の状態:

      - [オープン]\:推奨事項への対処がまだ行われていない。
      - [処理中]\:現在、リソースへの推奨事項の適用を進めており、ユーザーのアクションは不要。
      - [解決]\:推奨事項が既に完了済み (問題が解決されていると、エントリが灰色表示になります)。

    - 重大度: 特定の推奨事項の重要度を示します。

      - [高]\:重要なリソース (アプリケーション、仮想マシン、ネットワーク セキュリティ グループ) に脆弱性が存在しており、注意が必要。
      - 中程度:プロセスを完了または脆弱性を排除するために重大ではないまたは追加の手順が必要。
      - [低]\:対処する必要はあるものの、直ちに注意する必要はない脆弱性が存在する (既定では、重要度の低い推奨事項は表示されないが、重要度の低い推奨事項にフィルターを適用すると表示できる)。

3. 一覧で不足している更新プログラムを選択して詳細を表示します。

   ![不足しているセキュリティ更新プログラム][3]

4. 上部のリボンの **[検索]** アイコンをクリックします。  更新プログラムが不足しているコンピューターにフィルターされた Azure Monitor ログ検索クエリが開きます。

   ![Azure Monitor ログ検索][4]

5. 一覧でコンピューターを選択して詳細を確認します。 そのコンピューターだけを対象にフィルター処理された情報が含まれた別の検索結果が表示されます。

    ![Azure Monitor ログ検索][5]

## <a name="next-steps"></a>次のステップ
セキュリティ センターの詳細については、次を参照してください。

* [Azure Security Center でのセキュリティ ポリシーの設定](tutorial-security-policy.md) 」-- Azure サブスクリプションとリソース グループのセキュリティ ポリシーの構成方法について説明しています。
* [Azure セキュリティ センターでのセキュリティに関する推奨事項の管理](security-center-recommendations.md) 」 -- 推奨事項に従って Azure リソースを保護する方法について説明しています。
* [Azure Security Center でのセキュリティ ヘルスの監視](security-center-monitoring.md) 」-- Azure リソースの正常性を監視する方法について説明しています。
* [Azure Security Center でのセキュリティの警告の管理と対応](security-center-managing-and-responding-alerts.md) 」-- セキュリティの警告の管理と対応の方法について説明しています。
* [Azure Security Center を使用したパートナー ソリューションの監視](security-center-partner-solutions.md) 」-- パートナー ソリューションの正常性状態を監視する方法について説明しています。
* [Azure セキュリティ ブログ](https://blogs.msdn.com/b/azuresecurity/) -- Azure のセキュリティとコンプライアンスについてのブログ記事を確認できます。

<!--Image references-->
[1]: ./media/security-center-apply-system-updates/missing-system-updates.png
[2]:./media/security-center-apply-system-updates/apply-system-updates.png
[3]: ./media/security-center-apply-system-updates/detail-on-missing-update.png
[4]: ./media/security-center-apply-system-updates/log-search.png
[5]: ./media/security-center-apply-system-updates/search-details.png
