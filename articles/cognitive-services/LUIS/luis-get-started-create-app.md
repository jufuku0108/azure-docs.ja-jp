---
title: 'クイックスタート: アプリの作成 - LUIS'
description: このクイックスタートでは、照明やアプライアンスの電源をオンにしたりオフにしたりする用途を想定し、事前構築済みのドメイン `HomeAutomation` を使用した LUIS アプリを作成する方法について説明します。 この事前構築済みのドメインによって、意図、エンティティ、発話例が得られます。 完成すると、クラウド内で LUIS エンドポイントが実行されるようになります。
ms.topic: quickstart
ms.date: 03/24/2020
ms.openlocfilehash: de6cf5e95ee63fc9500cf1b5edab78597bdb18af
ms.sourcegitcommit: 9ee0cbaf3a67f9c7442b79f5ae2e97a4dfc8227b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/27/2020
ms.locfileid: "80287800"
---
# <a name="quickstart-use-prebuilt-home-automation-app"></a>クイック スタート:事前構築済みの Home Automation アプリを使用する

このクイック スタートでは、照明やアプライアンスの電源をオンにしたりオフにしたりする用途を想定し、事前構築済みのドメイン `HomeAutomation` を使用した LUIS アプリを作成します。 この事前構築済みのドメインによって、意図、エンティティ、発話例が得られます。 完成すると、クラウド内で LUIS エンドポイントが実行されるようになります。

[!INCLUDE [Sign in to LUIS](./includes/sign-in-process.md)]

[!INCLUDE [Select authoring resource](./includes/select-authoring-resource.md)]

## <a name="create-a-new-app"></a>新しいアプリの作成
アプリケーションは、 **[My Apps]** で作成および管理できます。

1. [マイアプリ] の一覧で、 **[+ New app for conversation]** \(+ 会話用の新しいアプリ\) を選択します。

1. ダイアログ ボックスで、お使いのアプリケーションに `Home Automation` という名前を付けます。 カルチャとして **[英語]** を選択します。 説明は省略可能です。作成や予測には使用されません。 LUIS アプリを作成するときには、予測リソースも省略可能です。 **[Done]** を選択します。

    LUIS によってアプリが作成されます。 運用環境にアプリを公開するときは、アプリが多くの要求を処理できるよう予測のリソースを割り当てる必要があります。

    ![ダイアログ ボックスで、アプリケーションに "Home Automation" という名前を付ける](./media/create-new-app-details.png)

    >[!NOTE]
    >カルチャは、アプリケーションを作成した後に変更できません。

## <a name="add-prebuilt-domain"></a>事前構築済みのドメインの追加

**[Prebuilt domains]** を選択し、 **[HomeAutomation]** を検索します。 [HomeAutomation] カードで、 **[Add domain]** を選択します。

![[Prebuilt domains] を選択し、[HomeAutomation] を検索します。 [HomeAutomation] カードで、[Add domain] を選択します。](media/luis-quickstart-new-app/home-automation.png)

ドメインが正常に追加されると、事前構築済みドメインのボックスに、 **[Remove domain]\(ドメインの削除\)** ボタンが表示されます。

## <a name="intents-and-entities"></a>意図とエンティティ

HomeAutomation ドメインの意図を確認するには、 **[Intents]** を選択します。 事前構築済みドメインの意図にはサンプル発話があります。

![HomeAutomation の意図の一覧のスクリーンショット](media/luis-quickstart-new-app/home-automation-intents.png "HomeAutomation の意図の一覧のスクリーンショット")

> [!NOTE]
> **[None]\(なし\)** は、すべての LUIS アプリに用意されている意図です。 これは自分のアプリの機能に対応しない発話を処理する目的で使用されます。

**[HomeAutomation.TurnOff]** 意図を選択します。 意図には、エンティティでラベル付けされている発話の一覧が含まれていることがわかります。

[![HomeAutomation.TurnOff 意図のスクリーンショット](media/luis-quickstart-new-app/home-automation-turnoff.png "HomeAutomation.TurnOff 意図のスクリーンショット")](media/luis-quickstart-new-app/home-automation-turnoff.png)

## <a name="train-the-luis-app"></a>LUIS アプリをトレーニングする

[!INCLUDE [LUIS How to Train steps](includes/howto-train.md)]

## <a name="test-your-app"></a>アプリをテストする
アプリのトレーニング後、そのテストを行うことができます。

1. 右上のナビゲーションから **[テスト]** を選択します。 1. 対話型のテスト ウィンドウに `Turn off the lights` などのテスト発話を入力し、Enter キーを押します。

    ```
    Turn off the lights
    ```

    それぞれのテスト発話について、最もスコアの高い意図が、想定された意図と対応していることを確認します。

    この例では、**HomeAutomation.TurnOff** に対する最もスコアの高い意図として `Turn off the lights` が正しく識別されています。

    ![発話が強調表示されたテスト パネルのスクリーンショット](media/luis-quickstart-new-app/review-test-inspection-pane-in-portal.png)

1. **[検査]** を選択して、その予測の詳細を確認します。

    ![検査情報を含むテスト パネルのスクリーンショット](media/luis-quickstart-new-app/test.png)

1. テスト ウィンドウを閉じます。

<a name="publish-your-app"></a>

## <a name="publish-the-app-to-get-the-endpoint-url"></a>アプリを公開してエンドポイント URL を取得する

[!INCLUDE [LUIS How to Publish steps](./includes/howto-publish.md)]

<a name="query-the-v2-api-prediction-endpoint"></a>

## <a name="query-the-v3-api-prediction-endpoint"></a>V3 API 予測エンドポイントに対してクエリを実行する

[!INCLUDE [LUIS How to get endpoint first step](./includes/v3-prediction-endpoint.md)]

2. ブラウザーのアドレス バーで、クエリ文字列について、URL に次の名前と値のバーが含まれていることを確認します。 それらがクエリ文字列に含まれていない場合は、追加してください。

    |名前と値のペア|
    |--|
    |`verbose=true`|
    |`show-all-intents=true`|

3. ブラウザーのアドレス バーで、URL の最後に移動し、_クエリ_ 値に「`turn off the living room light`」と入力して Enter キーを押します。

    ```json
    {
        "query": "turn off the living room light",
        "prediction": {
            "topIntent": "HomeAutomation.TurnOff",
            "intents": {
                "HomeAutomation.TurnOff": {
                    "score": 0.984315455
                },
                "HomeAutomation.QueryState": {
                    "score": 0.009912962
                },
                "HomeAutomation.TurnDown": {
                    "score": 0.00626645749
                },
                "HomeAutomation.TurnUp": {
                    "score": 0.00572059769
                },
                "HomeAutomation.SetDevice": {
                    "score": 0.00379381469
                },
                "HomeAutomation.TurnOn": {
                    "score": 0.00366983772
                },
                "None": {
                    "score": 0.000623856
                }
            },
            "entities": {
                "HomeAutomation.Location": [
                    "living room"
                ],
                "HomeAutomation.DeviceName": [
                    [
                        "living room light"
                    ]
                ],
                "HomeAutomation.DeviceType": [
                    [
                        "light"
                    ]
                ],
                "$instance": {
                    "HomeAutomation.Location": [
                        {
                            "type": "HomeAutomation.Location",
                            "text": "living room",
                            "startIndex": 13,
                            "length": 11,
                            "score": 0.907323956,
                            "modelTypeId": 1,
                            "modelType": "Entity Extractor",
                            "recognitionSources": [
                                "model"
                            ]
                        }
                    ],
                    "HomeAutomation.DeviceName": [
                        {
                            "type": "HomeAutomation.DeviceName",
                            "text": "living room light",
                            "startIndex": 13,
                            "length": 17,
                            "modelTypeId": 5,
                            "modelType": "List Entity Extractor",
                            "recognitionSources": [
                                "model"
                            ]
                        }
                    ],
                    "HomeAutomation.DeviceType": [
                        {
                            "type": "HomeAutomation.DeviceType",
                            "text": "light",
                            "startIndex": 25,
                            "length": 5,
                            "modelTypeId": 5,
                            "modelType": "List Entity Extractor",
                            "recognitionSources": [
                                "model"
                            ]
                        }
                    ]
                }
            }
        }
    }
    ```

    [V3 予測エンドポイント](luis-migration-api-v3.md)の詳細について学習します。


## <a name="clean-up-resources"></a>リソースをクリーンアップする

[!INCLUDE [LUIS How to clean up resources](../../../includes/cognitive-services-luis-tutorial-how-to-clean-up-resources.md)]

## <a name="next-steps"></a>次のステップ

エンドポイントはコードから呼び出すことができます。

> [!div class="nextstepaction"]
> [コードを使って LUIS エンドポイントを呼び出す](luis-get-started-cs-get-intent.md)
