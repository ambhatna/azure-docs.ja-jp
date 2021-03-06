---
title: Machine Learning Studio (classic) でできること - Azure
description: Machine Learning Studio (クラシック) は、そのまま使うことのできるアルゴリズムやモジュールのライブラリから、ドラッグ アンド ドロップでモデルをすばやく構築できるツールです。
services: machine-learning
author: likebupt
ms.author: keli19
ms.custom: seodec18
ms.assetid: e65c8fe1-7991-4a2a-86ef-fd80a7a06269
ms.service: machine-learning
ms.subservice: studio
ms.topic: overview
ms.date: 08/19/2020
ms.openlocfilehash: 0a18f9adb8c3723619b44b30bfa334edf4300c0d
ms.sourcegitcommit: b8eba4e733ace4eb6d33cc2c59456f550218b234
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2020
ms.locfileid: "95509486"
---
# <a name="what-can-i-do-with-machine-learning-studio-classic"></a>Machine Learning Studio (classic) でできること

**適用対象:** ![これはチェック マークです。つまり、この記事は Machine Learning Studio (クラシック) を対象としています。](../../../includes/media/aml-applies-to-skus/yes.png)Machine Learning Studio (クラシック)   ![これは x 印です。つまり、この記事は Azure Machine Learning を対象としています。](../../../includes/media/aml-applies-to-skus/no.png)[Azure Machine Learning](../overview-what-is-machine-learning-studio.md#ml-studio-classic-vs-azure-machine-learning-studio)

[!INCLUDE [Designer notice](../../../includes/designer-notice.md)]

Machine Learning Studio (classic) は、機械学習モデルを構築、テスト、デプロイする際に使用できるドラッグ アンド ドロップ ツールです。 Studio (classic) でモデルを Web サービスとして公開すれば、カスタム アプリや BI ツール (Excel など) からそのモデルを簡単に利用することができます。


## <a name="studio-classic--interactive-workspace"></a>Studio (classic) の対話型ワークスペース

一般的な予測分析モデルの作成では、1 種類以上のソースからデータを入手し、さまざまなデータ操作と統計関数を使用してデータを変換および分析することにより、一連の結果を生成します。 このようなモデルの作成プロセスは対話型プロセスになります。 十分にトレーニングされた有効なモデルが作成されるまで、さまざまな特徴とパラメーターを繰り返し調整します。

Machine Learning Studio (classic) では、予測分析モデルの作成、テスト、反復作業を支援する、視覚的操作に対応した対話型ワークスペースが提供されます。 "**_データセット_* _" と分析 "_*_モジュール_*_" を対話型のキャンバスにドラッグ アンド ドロップし、それらを相互に接続して "_*_実験_*_" を完成させ、Machine Learning Studio (クラシック) で実行できます。 モデルのさまざまな設計を試す際は、実験を編集して必要に応じて保存し、再度実行できます。 準備が整ったら、"_*_トレーニング実験_*_" を "_*_予測実験_*_" に変換します。さらに、"_*_Web サービス_*_" として発行し、第三者が利用できるようにそのモデルを公開します。

データセットとモジュールを視覚的に接続すれば予測分析モデルが完成するため、プログラミングは必要ありません。

![Machine Learning Studio (classic) の図: 実験の作成、各種ソースのデータの読み取り、スコア付けされたデータの書き込み、モデルの書き込み](./media/what-is-ml-studio/azure-ml-studio-diagram.jpg)

## <a name="download-the-ml-studio-classic-overview-diagram"></a>ML Studio (classic) の概要図をダウンロードする
_ *Microsoft ML Studio (クラシック) 機能の概要**図をダウンロードして、Machine Learning Studio (クラシック) の機能の概要を確認します。 図をタブロイド サイズ (11 x 17 インチ) で印刷し、手元に置いておくことができます。

**ここから図をダウンロード:[Microsoft Machine Learning Studio (クラシック) の機能の概要](https://download.microsoft.com/download/C/4/6/C4606116-522F-428A-BE04-B6D3213E9E52/ml_studio_overview_v1.1.pdf)** 
![Microsoft Machine Learning Studio (クラシック) の機能の概要](./media/what-is-ml-studio/ml_studio_overview_v1.1.png)


## <a name="components-of-a-studio-classic--experiment"></a>Studio (クラシック) 実験のコンポーネント
実験にはデータセットが含まれます。データセットからデータが分析モジュールに提供され、分析モジュールを接続することで予測分析モデルが完成します。 有効な実験に求められる具体的な条件を以下に示します。

* 実験には少なくとも 1 つのデータセットと 1 つのモジュールがある。
* データセットはモジュールにのみ接続できる。
* モジュールはデータセットにも別のモジュールにも接続できる。
* モジュールのすべての入力ポートが、何らかの形でデータ フローに接続されている。
* モジュールの必須パラメーターがすべて設定されている。

実験を最初から作成するか、既にあるサンプル実験をテンプレートとして使用してください。 詳細については、「[サンプル実験をコピーして新しい機械学習実験を作成する](sample-experiments.md)」を参照してください。

実験の作成例については、[Machine Learning Studio (classic) での実験の作成](create-experiment.md)に関するページを参照してください。

予測分析ソリューションのより詳しいチュートリアルについては、[Machine Learning Studio (classic) を使用した予測ソリューションの開発](tutorial-part1-credit-risk.md)に関するページを参照してください。

### <a name="datasets"></a>データセット
データセットを Machine Learning Studio (クラシック) にアップロードすることで、これらのデータセットをモデル作成プロセスで使用できるようになります。 Machine Learning Studio (クラシック) には数多くのサンプル データセットが既に含まれているため、これらを実験で試すことができます。また、必要に応じてさらにデータセットをアップロードできます。 提供されるデータセットには以下のようなものがあります。

* **さまざまな自動車の燃費データ** - シリンダー数や馬力などによって分類された、自動車の燃費値 (MPG) です。
* **乳がんデータ** - 乳がんの診断データです。
* **森林火災データ** - ポルトガル北東地域を対象とする森林火災の規模データです。

利用可能なデータセットは、実験を作成するときにキャンバスの左側の一覧から選択できます。

Machine Learning Studio (classic) に含まれているサンプル データセットの一覧については、[Machine Learning Studio (classic) でのサンプル データ セットの使用](use-sample-datasets.md)に関するページを参照してください。

### <a name="modules"></a>モジュール
モジュールとは、データに対して実行できるアルゴリズムのことです。 Machine Learning Studio (classic) には、データのイングレス機能からトレーニング、スコア付け、および検証プロセスに至るまでのさまざまなモジュールが用意されています。 提供されるモジュールには以下のようなものがあります。

* [ARFF への変換][convert-to-arff] - .NET のシリアル化されたデータセットを属性関係ファイル形式 (ARFF) に変換します。
* [基本統計値の計算][elementary-statistics] - 平均や標準偏差などの基本的な統計値を計算します。
* [線形回帰][linear-regression] - オンライン傾斜降下に基づく線形回帰モデルを作成します。
* [モデルのスコア付け][score-model] - トレーニングされた分類または回帰モデルをスコア付けします。

利用可能なモジュールは、実験を作成するときにキャンバスの左側の一覧から選択できます。

モジュールに一連のパラメーターが含まれている場合、これらを使用してモジュールの内部アルゴリズムを構成することができます。 モジュールのパラメーターは、キャンバスでモジュールを選択するとキャンバス右側の **[プロパティ]** ウィンドウに表示されます。 このウィンドウでパラメーターを変更することにより、モデルを微調整できます。

大規模な機械学習アルゴリズムのライブラリを利用する際のヒントについては、[Microsoft Machine Learning Studio (classic) のアルゴリズムの選択方法](../how-to-select-algorithms.md)に関するページを参照してください。

## <a name="deploying-a-predictive-analytics-web-service"></a>予測分析 Web サービスのデプロイ
予測分析モデルの準備が整ったら、それを Machine Learning Studio (クラシック) から Web サービスとしてデプロイすることができます。 このプロセスの詳細については、「[Azure Machine Learning Web サービスをデプロイする](deploy-a-machine-learning-web-service.md)」を参照してください。

## <a name="next-steps"></a>次のステップ
[ステップ バイ ステップ クイック スタート](create-experiment.md)を使用し、[サンプル上に構築](sample-experiments.md)することによって、予測分析と機械学習の基礎について学習できます。

<!-- Module References -->
[convert-to-arff]: /azure/machine-learning/studio-module-reference/convert-to-arff
[elementary-statistics]: /azure/machine-learning/studio-module-reference/compute-elementary-statistics
[linear-regression]: /azure/machine-learning/studio-module-reference/linear-regression
[score-model]: /azure/machine-learning/studio-module-reference/score-model