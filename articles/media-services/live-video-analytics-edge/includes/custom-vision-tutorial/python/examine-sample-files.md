---
author: russell-cooks
ms.service: media-services
ms.topic: include
ms.date: 10/05/2020
ms.author: russellcooks
ms.openlocfilehash: 5dd823c618a0d49bef29c473e6c293762b859149
ms.sourcegitcommit: 0b9fe9e23dfebf60faa9b451498951b970758103
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2020
ms.locfileid: "94358300"
---
1. Visual Studio Code で src/edge に移動します。 作成した .env ファイルと、いくつかのデプロイ テンプレート ファイルを確認できます。

    展開テンプレートでは、いくつかのプレースホルダー値で、エッジ デバイスの配置マニフェストが参照されています。 それらの変数の値が .env ファイルに格納されています。
1. 次に、src/cloud-to-device-console-app フォルダーに移動します。 ここでは、作成した appsettings.json ファイルと、他のいくつかのファイルを確認できます。

   * operations.json - このファイルには、プログラムで実行するさまざまな操作がリストされます。
   * main.py - これは次の処理を実行するサンプル プログラムのコードです。
    
        * アプリ設定を読み込みます。
        * Live Video Analytics on IoT Edge モジュールのダイレクト メソッドを呼び出して、トポロジの作成、グラフのインスタンス作成、グラフのアクティブ化を実行します。
        * **[ターミナル]** ウィンドウでグラフ出力を、 **[出力]** ウィンドウで IoT ハブに送信されたイベントを調べるために一時停止します。
        * グラフ インスタンスを非アクティブ化し、グラフ インスタンスを削除して、グラフ トポロジを削除します。
