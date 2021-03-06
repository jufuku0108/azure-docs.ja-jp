---
title: チュートリアル:Azure Active Directory シングル サインオン (SSO) と Concur Travel and Expense の統合 | Microsoft Docs
description: Azure Active Directory と Concur Travel and Expense の間でシングル サインオンを構成する方法について説明します。
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: barbkess
ms.assetid: 6401ace4-71c0-4778-8b15-900f2f5f0c4c
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 03/10/2019
ms.author: jeedes
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9dddd9f6904aa5ef7840850792aeabf04666dddc
ms.sourcegitcommit: 0947111b263015136bca0e6ec5a8c570b3f700ff
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/24/2020
ms.locfileid: "72373407"
---
# <a name="tutorial-azure-active-directory-single-sign-on-sso-integration-with-concur-travel-and-expense"></a>チュートリアル:Azure Active Directory シングル サインオン (SSO) と Concur Travel and Expense の統合

このチュートリアルでは、Concur Travel and Expense と Azure Active Directory (Azure AD) を統合する方法について説明します。 Concur Travel and Expense と Azure AD を統合すると、次のことができます。

* Concur Travel and Expense にアクセスできるユーザーを Azure AD で制御できます。
* ユーザーが自分の Azure AD アカウントを使用して Concur Travel and Expense に自動的にサインインできるように設定できます。
* 1 つの中央サイト (Azure Portal) で自分のアカウントを管理します。

SaaS アプリと Azure AD の統合の詳細については、「[Azure Active Directory でのアプリケーションへのシングル サインオン](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis)」を参照してください。

## <a name="prerequisites"></a>前提条件

開始するには、次が必要です。

* Azure AD サブスクリプション。 サブスクリプションがない場合は、[無料アカウント](https://azure.microsoft.com/free/)を取得できます。
* Concur Travel and Expense のサブスクリプション。
* Concur ユーザー アカウントの "社内管理者" ロール。 適切なアクセス権があるかどうかは、[Concur SSO セルフサービス ツール](https://www.concursolutions.com/nui/authadmin/ssoadmin)に移動して調べることができます。 アクセス権がなかった場合は、Concur サポートまたは導入プロジェクト マネージャーに問い合わせてください。 

## <a name="scenario-description"></a>シナリオの説明

このチュートリアルでは、Azure AD の SSO を構成してテストします。

* Concur Travel and Expense では、**IDP Initiated SSO** と **SP Initiated SSO** がサポートされます
* Concur Travel and Expense では、運用環境と導入環境の両方で SSO のテストがサポートされます 

> [!NOTE]
> このアプリケーションの識別子は、3 つのリージョンのそれぞれについて固定された文字列値です。それらのリージョンは、米国、EMEA、および中国です。 そのため、1 つのテナントで構成できるインスタンスは、各リージョンにつき 1 つだけです。 

## <a name="adding-concur-travel-and-expense-from-the-gallery"></a>ギャラリーからの Concur Travel and Expense の追加

Azure AD への Concur Travel and Expense の統合を構成するには、ギャラリーからマネージド SaaS アプリの一覧に Concur Travel and Expense を追加する必要があります。

1. 職場または学校アカウントか、個人の Microsoft アカウントを使用して、[Azure portal](https://portal.azure.com) にサインインします。
1. 左のナビゲーション ウィンドウで **[Azure Active Directory]** サービスを選択します。
1. **[エンタープライズ アプリケーション]** に移動し、 **[すべてのアプリケーション]** を選択します。
1. 新しいアプリケーションを追加するには、 **[新しいアプリケーション]** を選択します。
1. **[ギャラリーから追加する]** セクションで、検索ボックスに、「**Concur Travel and Expense**」と入力します。
1. 結果のパネルから **[Concur Travel and Expense]** を選択し、アプリを追加します。 お使いのテナントにアプリが追加されるのを数秒待機します。

## <a name="configure-and-test-azure-ad-single-sign-on-for-concur-travel-and-expense"></a>Concur Travel and Expense の Azure AD シングル サインオンの構成とテスト

**B.Simon** というテスト ユーザーを使用して、Concur Travel and Expense に対する Azure AD SSO を構成してテストします。 SSO を機能させるために、Azure AD ユーザーと Concur Travel and Expense の関連ユーザーとの間にリンク関係を確立する必要があります。

Concur Travel and Expense に対する Azure AD SSO を構成してテストするには、次の構成要素を完了します。

1. **[Azure AD SSO の構成](#configure-azure-ad-sso)** - ユーザーがこの機能を使用できるようにします。
    1. **[Azure AD のテスト ユーザーの作成](#create-an-azure-ad-test-user)** - B.Simon で Azure AD のシングル サインオンをテストします。
    1. **[Azure AD テスト ユーザーの割り当て](#assign-the-azure-ad-test-user)** - B.Simon が Azure AD シングル サインオンを使用できるようにします。
1. **[Concur Travel and Expense の SSO の構成](#configure-concur-travel-and-expense-sso)** - アプリケーション側でシングル サインオン設定を構成します。
    1. **[Concur Travel and Expense のテスト ユーザーの作成](#create-concur-travel-and-expense-test-user)** - Concur Travel and Expense で B.Simon に対応するユーザーを作成し、Azure AD の B.Simon にリンクさせます。
1. **[SSO のテスト](#test-sso)** - 構成が機能するかどうかを確認します。

## <a name="configure-azure-ad-sso"></a>Azure AD SSO の構成

これらの手順に従って、Azure portal で Azure AD SSO を有効にします。

1. [Azure portal](https://portal.azure.com/) の **Concur Travel and Expense** アプリケーション統合ページで、 **[管理]** セクションを見つけて、 **[シングル サインオン]** を選択します。
1. **[シングル サインオン方式の選択]** ページで、 **[SAML]** を選択します。
1. **[SAML でシングル サインオンをセットアップします]** ページで、 **[基本的な SAML 構成]** の編集 (ペン) アイコンをクリックして設定を編集します。

   ![基本的な SAML 構成を編集する](common/edit-urls.png)

1. **[基本的な SAML 構成]** セクションでは、アプリケーションは **IDP** 開始モードで事前に構成されており、必要な URL は既に Azure で事前に設定されています。 構成を保存するには、 **[保存]** ボタンをクリックします。

    > [!NOTE]
    > 識別子 (エンティティ ID) と応答 URL (Assertion Consumer Service URL) はリージョン固有です。 Concur エンティティのデータセンターに基づいて選択してください。 Concur エンティティのデータセンターがわからない場合は、Concur サポートにお問い合わせください。 

5. **[SAML でシングル サインオンをセットアップします]** ページで、 **[ユーザー属性]** の編集 (ペン) アイコンをクリックして設定を編集します。 [一意のユーザー ID] は、Concur のユーザーのログイン ID と一致している必要があります。 通常、**user.userprincipalname** は **user.mail** に変更する必要があります。

    ![ユーザー属性の編集](common/edit-attribute.png)

6. **[SAML でシングル サインオンをセットアップします]** ページの **[SAML 署名証明書]** セクションで、 **[フェデレーション メタデータ XML]** を探して **[ダウンロード]** を選択し、メタデータをダウンロードしてコンピューターに保存します。

    ![証明書のダウンロードのリンク](common/metadataxml.png)

### <a name="create-an-azure-ad-test-user"></a>Azure AD のテスト ユーザーの作成

このセクションでは、Azure portal 内で B.Simon というテスト ユーザーを作成します。

1. Azure portal の左側のウィンドウから、 **[Azure Active Directory]** 、 **[ユーザー]** 、 **[すべてのユーザー]** の順に選択します。
1. 画面の上部にある **[新しいユーザー]** を選択します。
1. **[ユーザー]** プロパティで、以下の手順を実行します。
   1. **[名前]** フィールドに「`B.Simon`」と入力します。  
   1. **[ユーザー名]** フィールドに「username@companydomain.extension」と入力します。 たとえば、「 `B.Simon@contoso.com` 」のように入力します。
   1. **[パスワードを表示]** チェック ボックスをオンにし、 **[パスワード]** ボックスに表示された値を書き留めます。
   1. **Create** をクリックしてください。

### <a name="assign-the-azure-ad-test-user"></a>Azure AD テスト ユーザーの割り当て

このセクションでは、B.Simon に Concur Travel and Expense へのアクセスを許可することで、このユーザーが Azure シングル サインオンを使用できるようにします。

1. Azure portal で **[エンタープライズ アプリケーション]** を選択し、 **[すべてのアプリケーション]** を選択します。
1. アプリケーションの一覧で **[Concur Travel and Expense]** を選択します。
1. アプリの概要ページで、 **[管理]** セクションを見つけて、 **[ユーザーとグループ]** を選択します。

   ![[ユーザーとグループ] リンク](common/users-groups-blade.png)

1. **[ユーザーの追加]** を選択し、 **[割り当ての追加]** ダイアログで **[ユーザーとグループ]** を選択します。

    ![[ユーザーの追加] リンク](common/add-assign-user.png)

1. **[ユーザーとグループ]** ダイアログの [ユーザー] の一覧から **[B.Simon]** を選択し、画面の下部にある **[選択]** ボタンをクリックします。
1. SAML アサーション内に任意のロール値が必要な場合、 **[ロールの選択]** ダイアログでユーザーに適したロールを一覧から選択し、画面の下部にある **[選択]** をクリックします。
1. **[割り当ての追加]** ダイアログで、 **[割り当て]** をクリックします。

## <a name="configure-concur-travel-and-expense-sso"></a>Concur Travel and Expense の SSO の構成

1. **Concur Travel and Expense** 側でシングル サインオンを構成するには、ダウンロードした**フェデレーション メタデータ XML** を [Concur SSO セルフ サービス ツール](https://www.concursolutions.com/nui/authadmin/ssoadmin)にアップロードし、"社内管理者" ロールがあるアカウントでログインする必要があります。 

1. **[追加]** をクリックします。
1. IdP のカスタム名を入力します (例: "Azure AD (US)")。 
1. **[Upload XML File]\(XML ファイルのアップロード\)** をクリックし、先ほどダウンロードした**フェデレーション メタデータ XML** を添付します。
1. **[Add Metadata]\(メタデータの追加\)** をクリックして変更を保存します。

    ![Concur SSO セルフ サービス ツールのスクリーンショット](./media/concur-travel-and-expense-tutorial/add-metadata-concur-self-service-tool.png)

### <a name="create-concur-travel-and-expense-test-user"></a>Concur Travel and Expense のテスト ユーザーの作成

このセクションでは、Concur Travel and Expense で B.Simon というユーザーを作成します。 Concur サポート チームと連携し、Concur Travel and Expense プラットフォームにユーザーを追加してください。 シングル サインオンを使用する前に、ユーザーを作成し、有効化する必要があります。 

> [!NOTE]
> B.Simon の Concur ログイン ID は、Azure AD における B.Simon の一意識別子と一致している必要があります。 たとえば、Azure AD における B.Simon の一意識別子が `B.Simon@contoso.com` である場合、 Concur における B.Simon のログイン ID も `B.Simon@contoso.com` である必要があります。 

## <a name="configure-concur-mobile-sso"></a>Concur Mobile の SSO の構成
Concur Mobile の SSO を有効にするには、Concur サポート チームに**ユーザーのアクセス URL** を提供する必要があります。 次の手順に従って、Azure AD から**ユーザーのアクセス URL** を入手してください。
1. **[エンタープライズ アプリケーション]** に移動します。
1. **[Concur Travel and Expense]** をクリックします。
1. **[プロパティ]** をクリックします。
1. **[ユーザーのアクセス URL]** をコピーして、その URL を Concur サポートに提供します。

> [!NOTE]
> SSO をセルフ サービスで構成するオプションは用意されていません。Concur サポート チームと連携して Mobile の SSO を有効にしてください。 

## <a name="test-sso"></a>SSO のテスト 

このセクションでは、アクセス パネルを使用して Azure AD のシングル サインオン構成をテストします。

アクセス パネル上で [Concur Travel and Expense] タイルをクリックすると、SSO を設定した Concur Travel and Expense に自動的にサインインします。 アクセス パネルの詳細については、[アクセス パネルの概要](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)に関する記事を参照してください。

## <a name="additional-resources"></a>その他のリソース

- [SaaS アプリと Azure Active Directory を統合する方法に関するチュートリアルの一覧](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list)

- [Azure Active Directory でのアプリケーション アクセスとシングル サインオンとは](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis)

- [Azure Active Directory の条件付きアクセスとは](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)

- [Azure AD で Concur Travel and Expense を試す](https://aad.portal.azure.com/)

