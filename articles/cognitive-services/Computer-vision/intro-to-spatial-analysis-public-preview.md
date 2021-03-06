---
title: Computer Vision 空間分析の概要
titleSuffix: Azure Cognitive Services
description: このドキュメントでは、Computer Vision 空間分析コンテナーの基本概念と機能について説明します。
services: cognitive-services
author: tchristiani
manager: nitinme
ms.author: terrychr
ms.service: cognitive-services
ms.subservice: computer-vision
ms.topic: conceptual
ms.date: 12/14/2020
ms.openlocfilehash: 402ee6d5efdd489914cb7d283c7c46d4f7d175f6
ms.sourcegitcommit: 9514d24118135b6f753d8fc312f4b702a2957780
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/07/2021
ms.locfileid: "97968060"
---
# <a name="introduction-to-computer-vision-spatial-analysis"></a>Computer Vision 空間分析の概要

Computer Vision 空間分析は、Azure Cognitive Services Computer Vision の新機能であり、組織はこの機能を使用して、特定の領域内でのユーザーの動きとプレゼンスを理解することで、物理的な空間の価値を最大限に高めることができます。 CCTV または監視カメラからビデオを取り込み、AI スキルを実行してビデオ ストリームから分析情報を抽出し、他のシステムで使用するイベントを生成することができます。 AI スキルでは、カメラ ストリームからの入力を使用して、空間に入ってくるユーザーの人数を数えたり、ソーシャル ディスタンスのガイドラインに対するコンプライアンスを測定したりする処理を行えます。

## <a name="the-basics-of-spatial-analysis"></a>空間分析の基本

現在、空間分析の中核となる操作はすべて、ビデオを取り込み、ビデオ内のユーザーを検出し、時間の経過に伴って動き回るユーザーを追跡し、ユーザーが関心領域を操作したときにイベントを生成するパイプライン上に構築されています。

## <a name="spatial-analysis-terms"></a>空間分析の用語

| 項目 | 定義 |
|------|------------|
| 人物検出 | このコンポーネントでは、"人物がこの画像のどこにいるか" という質問に答えます。 画像内の人間を見つけ、それぞれの人物の場所を示す境界ボックスが、人物追跡コンポーネントに渡されます。 |
| 人物追跡 | このコンポーネントでは、人物がカメラの前を動き回るときに時間の経過に伴って人物検出が接続されます。 これは、人が一般的にどのように動くかに関する通常の移動方法に関するテンポラル ロジックと、このように動いている人物の全体的な外観に関する基本情報を使用します。 複数のカメラ間で人物を追跡したり、約 1 分以上視界から消えた人物を再識別したりすることはできません。 人物追跡では、顔認識や歩行追跡などの生体認証マーカーは使用しません。 |
| 関心領域 | これは、構成の一部として入力ビデオ内で定義されたゾーンまたは線です。 ある人物がビデオの領域を操作すると、システムによってイベントが生成されます。 たとえば、PersonCrossingLine スキルの場合、ビデオ内には線が定義されています。 人物がその線を越えると、イベントが生成されます。 |
| イベント | イベントは、空間分析の主要な出力です。 各スキルは、定期的に (毎分 1 回など)、または特定のトリガーが生じたときのどちらかで特定のイベントを生成します。 once per minute) or when a specific trigger occurs. このイベントには、入力ビデオで起きたことに関する情報は含まれますが、画像やビデオは含まれません。 たとえば、PeopleCount スキルでは、人々の数が変化するたびに (トリガー)、または 1 分ごとに (定期的に)、更新された数を含んだイベントを生成できます。 |

## <a name="example-use-cases-for-spatial-analysis"></a>空間分析のユース ケースの例

次に、空間分析を設計およびテストした際に考慮したユース ケースの例を示します。

**ソーシャル ディスタンス コンプライアンス** - オフィス空間には、空間分析を使用した複数のカメラがあり、人々の間の距離を測定することにより、ソーシャル ディスタンス コンプライアンスを監視しています。 設備マネージャーは、時間の経過に伴うソーシャル ディスタンス コンプライアンスの集計情報を示したヒートマップを使用して、ワークスペースを調整し、ソーシャル ディスタンスを簡単に実現することができます。

**買い物客分析** - 食料品店では、製品に向けられたカメラを使用して、販売促進の変更が来店客数に及ぼす影響を測定します。 ストア マネージャーはこのシステムにより、どの新製品がエンゲージメントを最も大きく変化させるかを特定できます。

**行列管理** - レジの行列に向けられているカメラは、待機時間が長くなりすぎると、マネージャーにアラートを発し、さらにレジを開けられるようにします。 行列の放置に関する履歴データを使用すると、消費者の行動に関する分析情報が得られます。

**建物の占有率および分析** - オフィス ビルでは、主要な空間への入り口に焦点を当てたカメラを使用して、足取りを測定し、人々がどのように職場を使用しているかを測定します。 ビルのマネージャーは分析情報を使用して、入居者により適切に応えられるようにサービスやレイアウトを調整できます。

**スタッフの最低人数の検出** - データセンターでは、カメラはサーバー周囲の活動を監視します。 従業員が機密性の高い機器を物理的に修理する場合、セキュリティ上の理由から、修復中は常に 2 人の従業員が必要になります。 カメラは、このガイドラインに従っていることを確認するために使用されます。

**職場の最適化** - ファースト フード店では、キッチン内のカメラは、従業員の仕事の流れに関する集計情報を生成するために使用されます。 これは、チームのプロセスとトレーニングを改善するために、マネージャーによって使用されます。

## <a name="considerations-when-choosing-a-use-case"></a>ユース ケース選択時の考慮事項

**クリティカルなセキュリティのアラートを避ける** - 空間分析は、クリティカルなセキュリティのリアルタイム アラート向けには設計されていません。 人がいるときには大型機械をオフにするなど、けがを防止する操作をトリガーするためにリアルタイム アラートが必要なシナリオでは、これを使用しないでください。 これは、統計や介入を使用して、制限区域や禁止区域への人の侵入など、危険を伴う行動を抑えるリスク削減に使用できます。

**雇用関連の意思決定での使用を避ける** - 空間分析では、空間内の人々の位置と動きに関する確率的メトリックがもたらされます。 このデータは、集計プロセスの改善に役立つ場合がありますが、個々の作業員のパフォーマンスを示す適切な指標ではないので、雇用関連の意思決定には使用しないでください。

**医療関連の意思決定での使用を避ける** - 空間分析では、人々の動きに関連した確率的な部分データがもたらされます。 このデータは、医療関連の意思決定には適していません。

**保護された空間での使用を避ける** - 手洗所などの保護された区域を見渡すことのないように、カメラの場所と位置を評価し、角度と関心領域を調整することによって、個人のプライバシーを保護します。

**学校や高齢者福祉施設での使用は慎重に検討する** - 空間分析では、18 歳未満の未成年者や 65 歳を超える成人を含んだデータを使用したテストはあまり行われませんでした。 これらの年齢の人々が多数を占める環境では、お客様が自身のシナリオのエラー率を徹底的に評価することをお勧めします。

**公共の空間での使用は慎重に検討する** - 公共の空間からの収集を最小限に抑えるように、カメラの場所と位置を評価し、角度と関心領域を調整します。 道路や公園などの公共の空間での照明や気象は、空間分析システムのパフォーマンスに大きく影響するので、公共の空間で効果的な開示をもたらすのは非常に困難です。

## <a name="spatial-analysis-gating-for-public-preview"></a>空間分析のパブリック プレビューの制限

空間分析向けに設計されたシナリオで空間分析を使用してもらえるように、Microsoft では、お客様がアプリケーション プロセスを通じてこのテクノロジを利用できるようにしています。 空間分析にアクセスするには、最初にオンラインの受付フォームに入力する必要があります。 [アプリケーションはこちらから開始します](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbRyQZ7B8Cg2FEjpibPziwPcZUNlQ4SEVORFVLTjlBSzNLRlo0UzRRVVNPVy4u)。

空間分析パブリック プレビューへのアクセスは、この制限プレビュー期間中に限られた数のお客様をサポートするための Microsoft の資格基準、審査プロセス、および可用性に基づき、Microsoft の独自の判断によって決定されます。 パブリック プレビューでは、Microsoft と重要な関係を持ち、推奨のユース ケースと、責任ある AI へのコミットメントに従った追加シナリオに関して Microsoft と協力することに関心があるお客様を求めています。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [空間分析の特性と制限](https://docs.microsoft.com/legal/cognitive-services/computer-vision/accuracy-and-limitations?context=%2fazure%2fcognitive-services%2fComputer-vision%2fcontext%2fcontext)
