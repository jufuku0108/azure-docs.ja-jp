---
title: チュートリアル:Visual Studio Code 拡張機能を設定する
titleSuffix: Azure Machine Learning
description: Visual Studio Code の Azure Machine Learning 拡張機能を設定する方法について説明します。
services: machine-learning
ms.service: machine-learning
ms.subservice: core
ms.topic: tutorial
author: luisquintanilla
ms.author: luquinta
ms.date: 02/24/2020
ms.openlocfilehash: 583071ee22e4fb9cffc741520b1583790002a5bf
ms.sourcegitcommit: 0947111b263015136bca0e6ec5a8c570b3f700ff
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/24/2020
ms.locfileid: "77604886"
---
# <a name="set-up-azure-machine-learning-visual-studio-code-extension"></a>Visual Studio Code の Azure Machine Learning 拡張機能を設定する

Visual Studio Code の Azure Machine Learning 拡張機能を使用して、スクリプトをインストールして実行する方法について説明します。

このチュートリアルでは、以下のタスクについて学習します。

> [!div class="checklist"]
> * Visual Studio Code の Azure Machine Learning 拡張機能をインストールする
> * Visual Studio Code から Azure アカウントにサインインする
> * Azure Machine Learning 拡張機能を使用してサンプル スクリプトを実行する

## <a name="prerequisites"></a>前提条件

- Azure のサブスクリプション。 お持ちでない場合は、[無料版または有料版の Azure Machine Learning](https://aka.ms/AMLFree) にサインアップしてお試しください。
- Visual Studio Code。 インストールしていない場合は、[インストール](https://code.visualstudio.com/docs/setup/setup-overview)します。
- [Python 3](https://www.python.org/downloads/)

## <a name="install-the-extension"></a>拡張機能をインストールする

1. Visual Studio Code を開きます。
1. **アクティビティ バー**の**拡張機能**アイコンを選択して、拡張機能ビューを開きます。
1. 拡張機能ビューで、「Azure Machine Learning」を検索します。
1. **[インストール]** を選択します。

    > [!div class="mx-imgBorder"]
    > ![Azure Machine Learning VS Code 拡張機能をインストールする](./media/tutorial-setup-vscode-extension/install-aml-vscode-extension.PNG)

> [!NOTE]
> または、[インストーラーを直接ダウンロード](https://aka.ms/vscodetoolsforai)して、Visual Studio Marketplace 経由で Azure Machine Learning 拡張機能をインストールすることもできます。 

このチュートリアルの残りの手順は、拡張機能の**バージョン 0.6.8** を使用してテストされています。

## <a name="sign-in-to-your-azure-account"></a>Azure アカウントにサインインする

Azure でリソースをプロビジョニングし、ワークロードを実行するには、Azure アカウントの資格情報でサインインする必要があります。 アカウント管理を支援するために、Azure Machine Learning では Azure アカウント拡張機能が自動的にインストールされます。 Azure アカウント拡張機能の詳細については、[こちらのサイト](https://marketplace.visualstudio.com/items?itemName=ms-vscode.azure-account)を参照してしてください。

1. メニュー バーから **[表示]、[コマンド パレット]** の順に選択して、コマンド パレットを開きます。 
1. コマンド パレットに「Azure: Sign In」コマンドを入力して、サインイン プロセスを開始します。

## <a name="run-a-machine-learning-model-training-script-in-azure"></a>機械学習モデルのトレーニング スクリプトを Azure で実行する

これで、ご自分のアカウント資格情報を使用して Azure にサインインできました。次に、このセクションの手順に従い、拡張機能を使用して機械学習モデルをトレーニングする方法を説明します。

1. [VS Code Tools for AI リポジトリ](https://github.com/microsoft/vscode-tools-for-ai/archive/master.zip)をダウンロードし、お使いのコンピューターの任意の場所に解凍します。
1. Visual Studio Code で `mnist-vscode-docs-sample` ディレクトリを開きます。
1. アクティビティ バーの **Azure** アイコンを選択します。
1. Azure Machine Learning ビューの上部にある**実験の実行**アイコンを選択します。

    > [!div class="mx-imgBorder"]
    > ![実験の実行](./media/tutorial-setup-vscode-extension/run-experiment.PNG)

1. コマンド パレットが展開されたら、画面の指示に従います。

    1. Azure サブスクリプションを選択します。
    1. **[Create a new Azure ML workspace]\(新しい Azure ML ワークスペースを作成する\)** を選択します
    1. ジョブの種類として **[TensorFlow Single-Node Training]\(TensorFlow 単一ノード トレーニング\)** を選択します。
    1. トレーニングするスクリプトとして「`train.py`」を入力します。 これは、手書き数字の画像を分類する機械学習モデルのコードを含むファイルです。
    1. 実行するための要件として、次のパッケージを指定します。

        ```text
        pip: azureml-defaults; conda: python=3.6.2, tensorflow=1.15.0
        ```

1. この時点で、次のような構成ファイルがテキスト エディターに表示されます。 構成には、トレーニング ジョブを実行するために必要な情報が含まれています。ここには、モデルをトレーニングするためのコードや、前の手順で指定した Python の依存関係を含むファイルなどが指定されています。

    ```json
    {
        "workspace": "WS01311608",
        "resourceGroup": "WS01311608-rg1",
        "location": "South Central US",
        "experiment": "WS01311608-exp1",
        "compute": {
            "name": "WS01311608-com1",
            "vmSize": "Standard_D1_v2, Cores: 1; RAM: 3.5GB;"
        },
        "runConfiguration": {
            "filename": "WS01311608-com1-rc1",
            "condaDependencies": [
                "python=3.6.2",
                "tensorflow=1.15.0"
            ],
            "pipDependencies": [
                "azureml-defaults"
            ]
        }
    }
    ```

1. その構成に問題がなければ、コマンド パレットを開き、次のコマンドを入力して実験を送信してください。

    ```text
    Azure ML: Submit Experiment
    ```

    これにより、`train.py` と構成ファイルが Azure Machine Learning ワークスペースに送信されます。 その後、Azure のコンピューティング リソース上でトレーニング ジョブが開始されます。

### <a name="track-the-progress-of-the-training-script"></a>トレーニング スクリプトの進行状況を追跡する

スクリプトの実行には数分かかる場合があります。 進行状況を追跡するには、次の手順に従います。

1. アクティビティ バーから **Azure** アイコンを選択します。
1. ご利用のサブスクリプションのノードを展開します。
1. 現在実行している実験のノードを展開します。 その場所は `{workspace}/Experiments/{experiment}` ノード内で、ワークスペースや実験の値は、構成ファイルに定義されているプロパティと同じです。
1. 実験のすべての実行とその状態が一覧表示されます。 最新の状態を取得するには、Azure Machine Learning ビューの上部にある更新アイコンをクリックします。

    > [!div class="mx-imgBorder"]
    > ![実験の進行状況を追跡する](./media/tutorial-setup-vscode-extension/track-experiment-progress.PNG)

### <a name="download-the-trained-model"></a>トレーニング済みのモデルをダウンロードする

実験が完了すると、トレーニング済みのモデルが出力として得られます。 その出力をローカルにダウンロードするには、次の手順に従います。

1. 最新の実行を右クリックし、 **[Download Outputs]\(出力のダウンロード\)** を選択します。

    > [!div class="mx-imgBorder"]
    > ![トレーニング済みのモデルをダウンロードする](./media/tutorial-setup-vscode-extension/download-trained-model.PNG)

1. 出力の保存先を選択します。
1. 実行の名前のフォルダーがローカルにダウンロードされます。 そこに移動します。
1. モデル ファイルは、`outputs/outputs/model` ディレクトリに格納されています。

## <a name="next-steps"></a>次のステップ

* [チュートリアル:Visual Studio Code の Azure Machine Learning 拡張機能を使用して、画像分類 TensorFlow モデルをトレーニングおよびデプロイする](tutorial-train-deploy-image-classification-model-vscode.md)。
