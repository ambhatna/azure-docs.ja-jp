---
title: Cognitive Services コンテナー イメージ タグ
titleSuffix: Azure Cognitive Services
description: すべての Cognitive Service コンテナー イメージ タグの包括的一覧
services: cognitive-services
author: aahill
manager: nitinme
ms.service: cognitive-services
ms.topic: reference
ms.date: 11/17/2020
ms.author: aahi
ms.openlocfilehash: 09a83c28d07540b8ecd813e7ab2f10ceee891d7a
ms.sourcegitcommit: 6a770fc07237f02bea8cc463f3d8cc5c246d7c65
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/24/2020
ms.locfileid: "95792984"
---
# <a name="azure-cognitive-services-container-image-tags-and-release-notes"></a>Azure Cognitive Services コンテナー イメージ タグとリリース ノート

Azure Cognitive Services からはさまざまなコンテナー イメージが提供されます。 コンテナー レジストリとそれに対応するリポジトリは、コンテナー イメージによって異なります。 各コンテナー イメージ名にからは複数のタグが与えられます。 コンテナー イメージ タグは、コンテナー イメージのバージョンを管理するためのメカニズムです。 この記事は、Cognitive Services コンテナー イメージと利用できるタグをすべてリストアップする包括的リファレンスとして使用されることを意図して作成されています。

> [!TIP]
> [`docker pull`](https://docs.docker.com/engine/reference/commandline/pull/) を使用する場合、コンテナー レジストリ、リポジトリ、コンテナー イメージ名、それらに対応するタグの大文字/小文字の違いに注意してください。これらでは **大文字と小文字が区別されます**。

## <a name="anomaly-detector"></a>Anomaly Detector

[Anomaly Detector][ad-containers] コンテナー イメージは `mcr.microsoft.com` コンテナー レジストリ シンジケートで見つけることができます。 `azure-cognitive-services/decision` リポジトリ内にあり、`anomaly-detector` という名前が付いています。 完全修飾コンテナー イメージ名は `mcr.microsoft.com/azure-cognitive-services/decision/anomaly-detector` です。

このコンテナー イメージでは、次のタグを利用できます。 また、[MCR でタグ](https://mcr.microsoft.com/v2/azure-cognitive-services/decision/anomaly-detector/tags/list)の完全な一覧を確認することもできます。

# <a name="latest-version"></a>[最新バージョン](#tab/current)

| イメージ タグ                    | Notes |
|-------------------------------|:------|
| `latest`                      |       |
| `1.1.013560003-amd64-preview` |      |

# <a name="previous-versions"></a>[以前のバージョン](#tab/previous)

| イメージ タグ                    | Notes |
|-------------------------------|:------|
| `1.1.012300001-amd64-preview` |       |

---

## <a name="read-ocr-optical-character-recognition"></a>Read OCR (光学式文字認識) 

[Computer Vision][cv-containers] Read OCR コンテナー イメージは `mcr.microsoft.com` コンテナー レジストリ シンジケートにあります。 `azure-cognitive-services` リポジトリ内にあり、`read` という名前が付いています。 完全修飾コンテナー イメージ名は `mcr.microsoft.com/azure-cognitive-services/vision/read` です。

このコンテナー イメージでは、次のタグを利用できます。 また、[MCR でタグ](https://mcr.microsoft.com/v2/azure-cognitive-services/vision/read/tags/list)の完全な一覧を確認することもできます。

# <a name="latest-version"></a>[最新バージョン](#tab/current)

`3.2-preview.1` のリリース ノート:

* 新しい v3.2 コンテナー

| イメージ タグ                    | Notes |
|-------------------------------|:------|
| `latest`                      |       |
| `3.2-preview.1` |  |

# <a name="previous-versions"></a>[以前のバージョン](#tab/previous)

`v2.0.013250001-amd64-preview` のリリース ノート:

* コンテナーのメモリ使用量をさらに減らします。
* マルチポッド セットアップには外部キャッシュが必要です。 たとえば、キャッシュ用に Redis を設定します。
* Redis キャッシュが設定されており、`ResultExpirationPeriod` が 0 に設定されている場合に結果が欠落する問題を修正しました。
* 要求本文サイズの 26MB の制限を取り除きます。 コンテナーでは 26MB を超えるファイルを受け取れるようになります。
* タイム スタンプとビルド バージョンをコンソール ログに追加します。

`1.1.013050001-amd64-preview` のリリース ノート

* システムで認識結果を消去するタイミングを指定するために、`ReadEngineConfig:ResultExpirationPeriod` コンテナー初期化構成を追加しました。 
    * 設定は時間単位であり、既定値は 48 時間です。
    * この設定により、結果格納時のメモリ使用量を減らすことができます。特に、コンテナーのメモリ内ストレージが使用されるときに効果があります。
    * 例 1. ReadEngineConfig:ResultExpirationPeriod=1、プロセスから 1 時間後に認識結果が消去されます。
    * この構成が 0 に設定されている場合、結果が取得された後にシステムで認識結果が消去されます。

* 無効なイメージ形式がシステムに渡されたときの 500 内部サーバー エラーを修正しました。 400 エラーが返されるようになりました。

    ```json
    {
        "error": {
        "code": "InvalidImageSize",
        "message": "Image must be between 1024 and 209715200 bytes."
        }
    }
    ```

| イメージ タグ                    | Notes |
|-------------------------------|:------|
| `2.0.013250001-amd64-preview` |       |
| `1.1.013050001-amd64-preview` |       |
| `1.1.011580001-amd64-preview` |       |
| `1.1.009920003-amd64-preview` |       |
| `1.1.009910003-amd64-preview` |       |

---


## <a name="form-recognizer"></a>Form Recognizer

[Form Recognizer][fr-containers] コンテナー イメージは `mcr.microsoft.com` コンテナー レジストリ シンジケートにあります。 `azure-cognitive-services/custom-form` リポジトリ内にあり、`labeltool` という名前が付いています。 完全修飾コンテナー イメージ名は `mcr.microsoft.com/azure-cognitive-services/custom-form/labeltool` です。

このコンテナー イメージには次のタグを利用できます。 また、[MCR でタグ](https://mcr.microsoft.com/v2/azure-cognitive-services/custom-form/labeltool/tags/list)の完全な一覧を確認することもできます。

# <a name="latest-version"></a>[最新バージョン](#tab/current)

| イメージ タグ                    | Notes |
|-------------------------------|:------|
| `latest`                      |       |
| `1.1.009301-amd64-preview`    |       |


# <a name="previous-versions"></a>[以前のバージョン](#tab/previous)

| イメージ タグ                    | Notes |
|-------------------------------|:------|
| `1.1.008640001-amd64-preview` |       |
| `1.1.008510001-amd64-preview` |       |

---

## <a name="language-understanding-luis"></a>Language Understanding (LUIS)

[LUIS][lu-containers] コンテナー イメージは `mcr.microsoft.com` コンテナー レジストリ シンジケートにあります。 `azure-cognitive-services/language` リポジトリ内にあり、`luis` という名前が付いています。 完全修飾コンテナー イメージ名は `mcr.microsoft.com/azure-cognitive-services/language/luis` です。

このコンテナー イメージには次のタグを利用できます。 また、[MCR でタグ](https://mcr.microsoft.com/v2/azure-cognitive-services/language/luis/tags/list)の完全な一覧を確認することもできます。

# <a name="latest-version"></a>[最新バージョン](#tab/current)

| イメージ タグ                    | Notes |
|-------------------------------|:------|
| `latest`                      |       |
| `1.1.012280003-amd64-preview` |       |


# <a name="previous-version"></a>[以前のバージョン](#tab/previous)

| イメージ タグ                    | Notes |
|-------------------------------|:------|
| `1.1.012130003-amd64-preview` |       |

---

## <a name="custom-speech-to-text"></a>カスタム音声変換

[カスタム音声変換][sp-cstt]コンテナー イメージは `mcr.microsoft.com` コンテナー レジストリ シンジケートにあります。 `azure-cognitive-services/speechservices/` リポジトリ内にあり、`custom-speech-to-text` という名前が付いています。 完全修飾コンテナー イメージ名は `mcr.microsoft.com/azure-cognitive-services/speechservices/custom-speech-to-text` です。 また、[MCR でタグ](https://mcr.microsoft.com/v2/azure-cognitive-services/speechservices/custom-speech-to-text/tags/list)の完全な一覧を確認することもできます。


# <a name="latest-version"></a>[最新バージョン](#tab/current)

`2.7.0-amd64` のリリース ノート:

**機能**
* 句読点は、既定で有効に設定されています。

フレーズ リストが含まれているため、このコンテナー イメージのサイズが大きくなっていることに注意してください。

| イメージ タグ                    | Notes | ダイジェスト                                                                  |
|-------------------------------|:------|:------------------------------------------------------------------------|
| `latest`                      |       | `sha256:d1573c2543cb7afedb0122da0995f345767b02f9c5f181950acf1509ca65726` |
| `2.7.0-amd64`                 |       | `sha256:d1573c2543cb7afedb0122da0995f345767b02f9c5f181950acf1509ca65726` |


# <a name="previous-version"></a>[以前のバージョン](#tab/previous)
`2.6.0-amd64` のリリース ノート:

**機能**
* Phraselist v2 のサポート 
* フレーズ リストは次のロケールでサポートされています。
    * en-au
    * en-ca
    * en-gb
    * en-in
    * ja-JP
    * zh-cn
* カスタムベース モデルのダウンロードのサポート。 
    * `docker run` コマンドで `BaseModelLocale=<locale>` を使用する
* .NET 3.1 に完全に移行しました

**修正**
* 信頼スコアがダイアライゼーション モードで常に 1 になるという問題を修正しました
* TextAnalytics 3.0 API に移行しました

フレーズ リストが含まれているため、このコンテナー イメージのサイズが大きくなっていることに注意してください。

`2.5.0-amd64` のリリース ノート:

**機能**
* カスタム モデルでのカスタム発音のサポート
* Azure および Azure US Government Cloud のサポート

**修正**
* ダイアライゼーション モードで非 root ユーザーとして実行する場合の問題を修正しました

| イメージ タグ                    | Notes               |
|-------------------------------|:--------------------|
| `2.6.0-amd64`                 |                     |
| `2.5.0-amd64`                 |   最初の GA バージョン    |

---

## <a name="custom-text-to-speech"></a>カスタム テキスト読み上げ

[カスタム テキスト読み上げ][sp-ctts]コンテナー イメージは `mcr.microsoft.com` コンテナー レジストリ シンジケートにあります。 `azure-cognitive-services/speechservices/` リポジトリ内にあり、`custom-text-to-speech` という名前が付いています。 完全修飾コンテナー イメージ名は `mcr.microsoft.com/azure-cognitive-services/speechservices/custom-text-to-speech` です。 また、[MCR でタグ](https://mcr.microsoft.com/v2/azure-cognitive-services/speechservices/custom-text-to-speech/tags/list)の完全な一覧を確認することもできます。


# <a name="latest-version"></a>[最新バージョン](#tab/current)

`1.9.0-amd64` のリリース ノート:

定期的な毎月のリリース

| イメージ タグ                    | Notes | ダイジェスト                                                                  |
|-------------------------------|:------|:------------------------------------------------------------------------|
| `latest`                      |       | `sha256:e0397cf12d1367b13dd258f782bb513c93afcd5ee4b897794fe533205336355` |
| `1.9.0-amd64`                 |       | `sha256:e0397cf12d1367b13dd258f782bb513c93afcd5ee4b897794fe533205336355` |


# <a name="previous-version"></a>[以前のバージョン](#tab/previous)
`1.8.0-amd64` のリリース ノート:

**機能**
* .NET 3.1 に完全に移行しました

`1.7.0-amd64` のリリース ノート:

**機能**
* .NET 3.1 に部分的に移行されました

| イメージ タグ                    | Notes               |
|-------------------------------|:--------------------|
| `1.8.0-amd64`                 |                     |
| `1.7.0-amd64`                 |   最初の GA バージョン    |

---

## <a name="speech-to-text"></a>音声テキスト変換

[音声テキスト変換][sp-stt]コンテナー イメージは `mcr.microsoft.com` コンテナー レジストリ シンジケートにあります。 `azure-cognitive-services/speechservices/` リポジトリ内にあり、`speech-to-text` という名前が付いています。 完全修飾コンテナー イメージ名は `mcr.microsoft.com/azure-cognitive-services/speechservices/speech-to-text` です。 [MCR でタグ](https://mcr.microsoft.com/v2/azure-cognitive-services/speechservices/speech-to-text/tags/list)の完全な一覧を確認することができます。

音声テキスト変換 v2.5.0 以降、イメージは "*米国政府バージニア*" リージョンでサポートされています。 このリージョンを使う場合は、"*米国政府バージニア*" の課金エンドポイントと API キーを使用してください。

# <a name="latest-version"></a>[最新バージョン](#tab/current)

`2.7.0-amd64-<locale>` のリリース ノート:

**機能**
* 次の新しいロケールのサポート:
    * ar-bh、ar-iq、ar-jo、ar-lb、ar-om、ar-sy
    * bg-bg
    * el-gr
    * en-hk、en-ie、en-ph、en-sg、en-za
    * es-ar、es-bo、es-cl、es-co、es-cr、es-cu、es-do、es-ec、es-gt、es-pa、es-pe、es-pr、es-py、es-sv、es-us、es-uy、es-ve
    * et-ee
    * ga-ie
    * hr-hr
    * hu-hu
    * lt-lt
    * lv-lv
    * mt-mt
    * ro-ro
    * sk-sk
    * sl-sl
* 句読点は、既定で有効です。

フレーズ リストが含まれているため、このコンテナー イメージのサイズが大きくなっていることに注意してください。 

| イメージ タグ                    | Notes                                                                                                |
|-------------------------------|:-----------------------------------------------------------------------------------------------------|
| `latest`                      | `en-US` ロケールのコンテナー イメージ。                                                             |
| `2.7.0-amd64-<locale>`        | `<locale>` を、以下に一覧表示されている使用可能なロケールのいずれかに置き換えます。 たとえば、「 `2.7.0-amd64-en-us` 」のように指定します。 |

このコンテナー イメージには次のロケールを使用できます。

| v2.7.0 のロケール           | Notes                                    | ダイジェスト                                                                  |
|-----------------------------|:-----------------------------------------|:------------------------------------------------------------------------|
| `ar-ae`                     | `ar-AE` ロケールのコンテナー イメージ。 | `sha256:c8e99e71e6740cf671f3bf79de8b7dd890122cb674eedd2440e71e7cbc4c66b` |
| `ar-bh`                     | `ar-BH` ロケールのコンテナー イメージ。 | `sha256:5a2c140661f50d0c95587121ec1ab8895289f4dda5b3ad14074413e869e6bd4` |
| `ar-eg`                     | `ar-EG` ロケールのコンテナー イメージ。 | `sha256:783bb8321fcfb7890b0c99935099f7e84c85a698c2fe0031c661e265358d79c` |
| `ar-iq`                     | `ar-IQ` ロケールのコンテナー イメージ。 | `sha256:abd0101f73c1cf71f30da7b11b93d2a7ac8877dbfcfc2d34553d20705aca7a2` |
| `ar-jo`                     | `ar-JO` ロケールのコンテナー イメージ。 | `sha256:d4c7fd2a1637e163aa106c23b6a759e8c78366c60ece83b3aabfe93ebabae07` |
| `ar-kw`                     | `ar-KW` ロケールのコンテナー イメージ。 | `sha256:c8e99e71e6740cf671f3bf79de8b7dd890122cb674eedd2440e71e7cbc4c66b` |
| `ar-lb`                     | `ar-LB` ロケールのコンテナー イメージ。 | `sha256:20e5c9105e86625c72de54290a6eb07630d35c3760f729c4b855e3661583dfe` |
| `ar-om`                     | `ar-OM` ロケールのコンテナー イメージ。 | `sha256:97f1b44f2cbb837a2ef86441a0a52a07f706240edb6ef6618ee4db8cbbe1c19` |
| `ar-qa`                     | `ar-QA` ロケールのコンテナー イメージ。 | `sha256:c8e99e71e6740cf671f3bf79de8b7dd890122cb674eedd2440e71e7cbc4c66b` |
| `ar-sa`                     | `ar-SA` ロケールのコンテナー イメージ。 | `sha256:c8e99e71e6740cf671f3bf79de8b7dd890122cb674eedd2440e71e7cbc4c66b` |
| `ar-sy`                     | `ar-SY` ロケールのコンテナー イメージ。 | `sha256:51980a2e2c3dd3548deedcedaf5fc688db602a5eced1a4b7df7d10750393623` |
| `bg-bg`                     | `bg-BG` ロケールのコンテナー イメージ。 | `sha256:1c1acf0fbb353ebb04692f37eb4d4cdf0b4e309720dd7e709001dada0d1ea81` |
| `ca-es`                     | `ca-ES` ロケールのコンテナー イメージ。 | `sha256:c60baa0007f61c7652b97b49645215de63411125d627c974c09222e316df204` |
| `cs-cz`                     | `cs-CZ` ロケールのコンテナー イメージ。 | `sha256:3fa09fc3a6bde6b77df2444aae8fc78b5f25fb9010171d1682db116ea5801f5` |
| `da-dk`                     | `da-DK` ロケールのコンテナー イメージ。 | `sha256:4b26dbba50c2771943880b68e0e4ea0713d0e3bb8bad884454849bccc9e94a3` |
| `de-de`                     | `de-DE` ロケールのコンテナー イメージ。 | `sha256:5109ed80b1fecf4db0328adcd50528d0aa9e726b5fc84587c40aaea4e91256d` |
| `el-gr`                     | `el-GR` ロケールのコンテナー イメージ。 | `sha256:fc8b466c588bf097efac2b79454d5ac0df5c6990398f07ede9be7e1d536e4bd` |
| `en-au`                     | `en-AU` ロケールのコンテナー イメージ。 | `sha256:3461892a27fc3eb3f9610b2def00bc15f380c6b9797c90ceca19e6abb55f6a6` |
| `en-ca`                     | `en-CA` ロケールのコンテナー イメージ。 | `sha256:a0509be39785f1e869bd96ab10e7c07d3f4e61c9aa17ff5900076e7bd64ba11` |
| `en-gb`                     | `en-GB` ロケールのコンテナー イメージ。 | `sha256:1b976fc7ac109e61dcf74af3652c12535e3db92931d2d0bb2ea59bd46f9efed` |
| `en-hk`                     | `en-HK` ロケールのコンテナー イメージ。 | `sha256:0b1e1df101f978869c98f6e50632712016b8311fc89b334e7f44e968d64bf2f` |
| `en-ie`                     | `en-IE` ロケールのコンテナー イメージ。 | `sha256:c5ba0d3c7219ce39f0b918a51a7cae8a65c277f564279cad920e068725aa39f` |
| `en-in`                     | `en-IN` ロケールのコンテナー イメージ。 | `sha256:e907f07be498f024103f6fe6abffa23e242bf3585724741b29a2f3f41d0899c` |
| `en-nz`                     | `en-NZ` ロケールのコンテナー イメージ。 | `sha256:66845f6ce20ae71d609867c6eb4772366ce042499e4bcdce4c1b579daf7fad7` |
| `en-ph`                     | `en-PH` ロケールのコンテナー イメージ。 | `sha256:e7874653bf66b1a1ab344b3391eb8767be34260b7f11b62fd057cbe17b805b2` |
| `en-sg`                     | `en-SG` ロケールのコンテナー イメージ。 | `sha256:827cdb158280e6f4037f4815410c7aa78abf9c6467876c1504aecfef787bdd7` |
| `en-us`                     | `en-US` ロケールのコンテナー イメージ。 | `sha256:248d17340055e3e137219ddc234c605e6a53ceead136ea55c9697c352da6a8d` |
| `en-za`                     | `en-ZA` ロケールのコンテナー イメージ。 | `sha256:a8abc99f498db7088bb25acec47da81e90b6a5eaa1c6f78e0f9a314d839d0ae` |
| `es-ar`                     | `es-AR` ロケールのコンテナー イメージ。 | `sha256:edf78429630851b6eb01f54f8a8a1aeeda9971c6a834403a204662eda22b3b9` |
| `es-bo`                     | `es-BO` ロケールのコンテナー イメージ。 | `sha256:5832b44f1da2f6b9a097c99babfbc370d8d0eabe1ff8daabec2c3f482dc9d63` |
| `es-cl`                     | `es-CL` ロケールのコンテナー イメージ。 | `sha256:409a712b96235e154472134f96ff9272265f1e5b555e00ad03c2260b0781009` |
| `es-co`                     | `es-CO` ロケールのコンテナー イメージ。 | `sha256:99792bc083dc16e0edf15491e6a840d786c9140b747551563a8d98f66f0b415` |
| `es-cr`                     | `es-CR` ロケールのコンテナー イメージ。 | `sha256:21fe14a538e5b8b2d288b00b8f5a02d87469e285f32e725155042079f336ac9` |
| `es-cu`                     | `es-CU` ロケールのコンテナー イメージ。 | `sha256:05d40eae01cec4c42c4febd379cd61373eb43d0aacfd47b988bb95e6a6ad216` |
| `es-do`                     | `es-DO` ロケールのコンテナー イメージ。 | `sha256:73dd0e0d4f39a259563ee7cc18c2e72c9ab20c52905fe343e0413ca7c4b3f0d` |
| `es-ec`                     | `es-EC` ロケールのコンテナー イメージ。 | `sha256:c3e69139ef365fe9332b5b68b43458242c7dad9d9f2b557431272306e81cb9e` |
| `es-es`                     | `es-ES` ロケールのコンテナー イメージ。 | `sha256:bd83fcfc116ba645a0e12a7a93b6ada74a8f701172f826a91c5f223a1dbaa61` |
| `es-gt`                     | `es-GT` ロケールのコンテナー イメージ。 | `sha256:5bb9b18b91b74e123e3720893d88bfcb0a87dac31a1f7171d23c7cb1fa09fee` |
| `es-hn`                     | `es-HN` ロケールのコンテナー イメージ。 | `sha256:941d108a4b76eb554e8f13cf5090665a702de3ebf35b75e4350f0916dfccd72` |
| `es-mx`                     | `es-MX` ロケールのコンテナー イメージ。 | `sha256:cebea03732781b4425500d162ae6580bbd7ce9b5f4ede988c4570fe311d8567` |
| `es-ni`                     | `es-NI` ロケールのコンテナー イメージ。 | `sha256:8ba165f94ad840936ebd0af17a0a63aa08a6292e7ad9029f5b93eef41165eb9` |
| `es-pa`                     | `es-PA` ロケールのコンテナー イメージ。 | `sha256:c61b7f1b6801a03c3eab0dd1aede87017a86bc7368ded2f8bad8d9e5f60d0d3` |
| `es-pe`                     | `es-PE` ロケールのコンテナー イメージ。 | `sha256:447a3ab3f302aba24d201d9f5b2877ffcd64dfd5e9d6b88d9924847160b2de2` |
| `es-pr`                     | `es-PR` ロケールのコンテナー イメージ。 | `sha256:a53b3295c986e91ee8cf93ebe1057b997c76ef7f99913508b859311a194fdd4` |
| `es-py`                     | `es-PY` ロケールのコンテナー イメージ。 | `sha256:85b3f75e75e63e29521daf772ee68a59ac2428579512501aa81dc51a2315652` |
| `es-sv`                     | `es-SV` ロケールのコンテナー イメージ。 | `sha256:db5ece7ba536e38d5de59cd37807630ab76589dcf1c97e253f98d7f44d9424e` |
| `es-us`                     | `es-US` ロケールのコンテナー イメージ。 | `sha256:99f2743725bb71e25543484f49bcfde14584ccbbaaa912678938d69d965075a` |
| `es-uy`                     | `es-UY` ロケールのコンテナー イメージ。 | `sha256:a3e11c16a97a1ae76408d812b2fee1e4b3ba07160bbcb62a22814523568ee5d` |
| `es-ve`                     | `es-VE` ロケールのコンテナー イメージ。 | `sha256:8cb431aafd84263ead8de946377c1d3f2ddfa7e172b8a4c5aa7ba477c5b41f0` |
| `et-ee`                     | `et-EE` ロケールのコンテナー イメージ。 | `sha256:943e7cf894e9d75341a58993104824c1c8cd8da1322cc5a732e9d53882c6523` |
| `fi-fi`                     | `fi-FI` ロケールのコンテナー イメージ。 | `sha256:35658e9dce796cb96a1371f250398e86351ea1b5ada080da7ce8471b30c7cae` |
| `fr-ca`                     | `fr-CA` ロケールのコンテナー イメージ。 | `sha256:62256cad671e8baa03fdd4c5f4eca7d5c5effedd64cafd9020ba72c9c4210e0` |
| `fr-fr`                     | `fr-FR` ロケールのコンテナー イメージ。 | `sha256:b385993232d9daa327d1a7b067268927b17f36eed3e8d423748794544c62746` |
| `ga-ie`                     | `ga-IE` ロケールのコンテナー イメージ。 | `sha256:ab9abdb993b0f7487edda8200f1393ac44ba4888c0f444a02afb6c85ca3e393` |
| `gu-in`                     | `gu-IN` ロケールのコンテナー イメージ。 | `sha256:328e69488f2948722d7ccc97e266071f61a8c9f65cd671688490955806526de` |
| `hi-in`                     | `hi-IN` ロケールのコンテナー イメージ。 | `sha256:b9b0bfec80aa53d06ea2cbd9097f753ec5caaf00ac2f00321ae7ad916fd7fa6` |
| `hr-hr`                     | `hr-HR` ロケールのコンテナー イメージ。 | `sha256:ab849cd2eeea682f8958bba8986fe90f0f7bb3b447512a10cf464e8e1ce4ea5` |
| `hu-hu`                     | `hu-HU` ロケールのコンテナー イメージ。 | `sha256:30f239b155d91523442cf74a1f2732304fa2b50ae7b786833bb6a020b982621` |
| `it-it`                     | `it-IT` ロケールのコンテナー イメージ。 | `sha256:288f95413870eb9d33bf1dabfa6fbd6b55b0faa52e4d5face3171d1dd4ddbdd` |
| `ja-jp`                     | `ja-JP` ロケールのコンテナー イメージ。 | `sha256:e3ab37a80c215dec565eca212f57eb81887fc2894452868dff92e3bd42c4bb9` |
| `ko-kr`                     | `ko-KR` ロケールのコンテナー イメージ。 | `sha256:c1208b8459333b606af516cd7806e9d4d5e002247bb1225e1f246563b356890` |
| `lt-lt`                     | `lt-LT` ロケールのコンテナー イメージ。 | `sha256:8dec331161d3c29fc65ba6651fcc6cfe69fa314519f408b5f9f8eb27da09830` |
| `lv-lv`                     | `lv-LV` ロケールのコンテナー イメージ。 | `sha256:7cf31282910b339666bb2b0a555caa7fc6ae414eea4423a41f35c3527f83235` |
| `mr-in`                     | `mr-IN` ロケールのコンテナー イメージ。 | `sha256:9cb012bd58ef7723d4905d6fa3c1fde96e33c354b3d96d4e3ff69cf6e1bfe3a` |
| `mt-mt`                     | `mt-MT` ロケールのコンテナー イメージ。 | `sha256:a0094c032ea555b168ec5751ab3257337d902d526e9ae335671fb751a352378` |
| `nb-no`                     | `nb-NO` ロケールのコンテナー イメージ。 | `sha256:6bbc326e20a6a785b1ca33143b42a060858efb67b863a267d6efb7aebb48f87` |
| `nl-nl`                     | `nl-NL` ロケールのコンテナー イメージ。 | `sha256:94b4ddf4cc80fa666e422f8416aea3f98ebe4842dfe9b1f4bfea7c47eb61127` |
| `pl-pl`                     | `pl-PL` ロケールのコンテナー イメージ。 | `sha256:58e5f78bf772c3c8cbd5f0c5d6e67f5348e04e3f893d84738a2a3e964bab256` |
| `pt-br`                     | `pt-BR` ロケールのコンテナー イメージ。 | `sha256:f500ef956bd28807f40df1f9f0520e437c5084f61a3be6d1379e746887d5b7c` |
| `pt-pt`                     | `pt-PT` ロケールのコンテナー イメージ。 | `sha256:c841d2dbe5f40adf6039242c106985febb1a44212feb55d9769fe31134ec116` |
| `ro-ro`                     | `ro-RO` ロケールのコンテナー イメージ。 | `sha256:93271c39c0a134e987a069c2a65289acff9869ae0d90fdcb39928c9ef0fd86b` |
| `ru-ru`                     | `ru-RU` ロケールのコンテナー イメージ。 | `sha256:8d6b3c600e56cc96813b8c14b7916c5539a20ba561dc1c6d5bbef6285d6eef6` |
| `sk-sk`                     | `sk-SK` ロケールのコンテナー イメージ。 | `sha256:6d604092cc6c964663a1c97d91c8f1c8cf4b46d07427d03f7041c0cc55eb521` |
| `sl-si`                     | `sl-SI` ロケールのコンテナー イメージ。 | `sha256:f237ed58fedefcc749e74be1258cc70e5a690ee6c5a6b6388bd24075faa61da` |
| `sv-se`                     | `sv-SE` ロケールのコンテナー イメージ。 | `sha256:da4233e6658b00eefdadb9d4acd889c6550a5e2a4a7af7a9f915c878abd4c9c` |
| `ta-in`                     | `ta-IN` ロケールのコンテナー イメージ。 | `sha256:22b77606d25e9c2f52bf3cad6218782b4719f6a9dcfadc770468d266758a56c` |
| `te-in`                     | `te-IN` ロケールのコンテナー イメージ。 | `sha256:7f4d11372862ca1d65fc9b868e2d775701b8e6eabd786c90c4e9ab82ba86e88` |
| `th-th`                     | `th-TH` ロケールのコンテナー イメージ。 | `sha256:69033bcd7c0f59d31bafec6c2b7a9ff343928cdd58c16105415c291d555d37b` |
| `tr-tr`                     | `tr-TR` ロケールのコンテナー イメージ。 | `sha256:4b7d339846a0d371dfe25aa2e626f131003c01329c9a1da468eb3703ef176ea` |
| `zh-cn`                     | `zh-CN` ロケールのコンテナー イメージ。 | `sha256:a428459830fb766083212f71c5638a65ce30d8dd84f6c624ae22768e8a76976` |
| `zh-hk`                     | `zh-HK` ロケールのコンテナー イメージ。 | `sha256:7a2903462b67336a6ce4c8e2faac42052f0a4392d1d5eb3839758cc8d0429f1` |
| `zh-tw`                     | `zh-TW` ロケールのコンテナー イメージ。 | `sha256:30fd2b3660e047d24a46fbba14ba282f15bc0339ec93f49afd0d02ff4069146` |


# <a name="previous-version"></a>[以前のバージョン](#tab/previous)

`2.6.0-amd64-<locale>` のリリース ノート:

**機能**
* 最新のモデルにアップグレードし、.NET 3.1 に完全に移行しました
* Phraselist v2 のサポート
* フレーズ リストは次のロケールでサポートされています。
    * en-au
    * en-ca
    * en-gb
    * en-in
    * ja-JP
    * zh-cn
* 新しいロケール `cs-CZ` のサポート 
    * 大文字と小文字の区別と句読点は現在サポートされていません。

**修正**
* 信頼スコアがダイアライゼーション モードで常に 1 になるという問題を修正しました
* TextAnalytics 3.0 API を使用するように移行しました

フレーズ リストが含まれているため、このコンテナー イメージのサイズが大きくなっていることに注意してください。 

`2.5.0-amd64-<locale>` のリリース ノート:

**機能**
* Azure US Government Cloud のサポート

**修正**
* ダイアライゼーション モードで非 root ユーザーとして実行する場合の問題を修正しました

| イメージ タグ                  | Notes                                    |
|-----------------------------|:-----------------------------------------|
| `2.6.0-amd64-<locale>`      | `<locale>` を、以下に一覧表示されている使用可能なロケールのいずれかに置き換えます。 たとえば、「 `2.6.0-amd64-en-us` 」のように指定します。 |
| `2.5.0-amd64-<locale>`      | `<locale>` を、以下に一覧表示されている使用可能なロケールのいずれかに置き換えます。 たとえば、「 `2.5.0-amd64-en-us` 」のように指定します。 |


このコンテナー イメージには次のロケールを使用できます。

| v2.6.0 のロケール           | Notes                                    |
|-----------------------------|:-----------------------------------------|
| `ar-ae`                     | `ar-AE` ロケールのコンテナー イメージ。 |
| `ar-eg`                     | `ar-EG` ロケールのコンテナー イメージ。 |
| `ar-kw`                     | `ar-KW` ロケールのコンテナー イメージ。 |
| `ar-qa`                     | `ar-QA` ロケールのコンテナー イメージ。 |
| `ar-sa`                     | `ar-SA` ロケールのコンテナー イメージ。 |
| `ca-es`                     | `ca-ES` ロケールのコンテナー イメージ。 |
| `cs-cz`                     | `cs-CZ` ロケールのコンテナー イメージ。 |
| `da-dk`                     | `da-DK` ロケールのコンテナー イメージ。 |
| `de-de`                     | `de-DE` ロケールのコンテナー イメージ。 |
| `en-au`                     | `en-AU` ロケールのコンテナー イメージ。 |
| `en-ca`                     | `en-CA` ロケールのコンテナー イメージ。 |
| `en-gb`                     | `en-GB` ロケールのコンテナー イメージ。 |
| `en-in`                     | `en-IN` ロケールのコンテナー イメージ。 |
| `en-nz`                     | `en-NZ` ロケールのコンテナー イメージ。 |
| `en-us`                     | `en-US` ロケールのコンテナー イメージ。 |
| `es-es`                     | `es-ES` ロケールのコンテナー イメージ。 |
| `es-mx`                     | `es-MX` ロケールのコンテナー イメージ。 |
| `fi-fi`                     | `fi-FI` ロケールのコンテナー イメージ。 |
| `fr-ca`                     | `fr-CA` ロケールのコンテナー イメージ。 |
| `fr-fr`                     | `fr-FR` ロケールのコンテナー イメージ。 |
| `gu-in`                     | `gu-IN` ロケールのコンテナー イメージ。 |
| `hi-in`                     | `hi-IN` ロケールのコンテナー イメージ。 |
| `it-it`                     | `it-IT` ロケールのコンテナー イメージ。 |
| `ja-jp`                     | `ja-JP` ロケールのコンテナー イメージ。 |
| `ko-kr`                     | `ko-KR` ロケールのコンテナー イメージ。 |
| `mr-in`                     | `mr-IN` ロケールのコンテナー イメージ。 |
| `nb-no`                     | `nb-NO` ロケールのコンテナー イメージ。 |
| `nl-nl`                     | `nl-NL` ロケールのコンテナー イメージ。 |
| `pl-pl`                     | `pl-PL` ロケールのコンテナー イメージ。 |
| `pt-br`                     | `pt-BR` ロケールのコンテナー イメージ。 |
| `pt-pt`                     | `pt-PT` ロケールのコンテナー イメージ。 |
| `ru-ru`                     | `ru-RU` ロケールのコンテナー イメージ。 |
| `sv-se`                     | `sv-SE` ロケールのコンテナー イメージ。 |
| `ta-in`                     | `ta-IN` ロケールのコンテナー イメージ。 |
| `te-in`                     | `te-IN` ロケールのコンテナー イメージ。 |
| `th-th`                     | `th-TH` ロケールのコンテナー イメージ。 |
| `tr-tr`                     | `tr-TR` ロケールのコンテナー イメージ。 |
| `zh-cn`                     | `zh-CN` ロケールのコンテナー イメージ。 |
| `zh-hk`                     | `zh-HK` ロケールのコンテナー イメージ。 |
| `zh-tw`                     | `zh-TW` ロケールのコンテナー イメージ。 |

| v2.5.0 のロケール           | Notes                                    |
|-----------------------------|:-----------------------------------------|
| `ar-ae`                     | `ar-AE` ロケールのコンテナー イメージ。 |
| `ar-eg`                     | `ar-EG` ロケールのコンテナー イメージ。 |
| `ar-kw`                     | `ar-KW` ロケールのコンテナー イメージ。 |
| `ar-qa`                     | `ar-QA` ロケールのコンテナー イメージ。 |
| `ar-sa`                     | `ar-SA` ロケールのコンテナー イメージ。 |
| `ca-es`                     | `ca-ES` ロケールのコンテナー イメージ。 |
| `da-dk`                     | `da-DK` ロケールのコンテナー イメージ。 |
| `de-de`                     | `de-DE` ロケールのコンテナー イメージ。 |
| `en-au`                     | `en-AU` ロケールのコンテナー イメージ。 |
| `en-ca`                     | `en-CA` ロケールのコンテナー イメージ。 |
| `en-gb`                     | `en-GB` ロケールのコンテナー イメージ。 |
| `en-in`                     | `en-IN` ロケールのコンテナー イメージ。 |
| `en-nz`                     | `en-NZ` ロケールのコンテナー イメージ。 |
| `en-us`                     | `en-US` ロケールのコンテナー イメージ。 |
| `es-es`                     | `es-ES` ロケールのコンテナー イメージ。 |
| `es-mx`                     | `es-MX` ロケールのコンテナー イメージ。 |
| `fi-fi`                     | `fi-FI` ロケールのコンテナー イメージ。 |
| `fr-ca`                     | `fr-CA` ロケールのコンテナー イメージ。 |
| `fr-fr`                     | `fr-FR` ロケールのコンテナー イメージ。 |
| `gu-in`                     | `gu-IN` ロケールのコンテナー イメージ。 |
| `hi-in`                     | `hi-IN` ロケールのコンテナー イメージ。 |
| `it-it`                     | `it-IT` ロケールのコンテナー イメージ。 |
| `ja-jp`                     | `ja-JP` ロケールのコンテナー イメージ。 |
| `ko-kr`                     | `ko-KR` ロケールのコンテナー イメージ。 |
| `mr-in`                     | `mr-IN` ロケールのコンテナー イメージ。 |
| `nb-no`                     | `nb-NO` ロケールのコンテナー イメージ。 |
| `nl-nl`                     | `nl-NL` ロケールのコンテナー イメージ。 |
| `pl-pl`                     | `pl-PL` ロケールのコンテナー イメージ。 |
| `pt-br`                     | `pt-BR` ロケールのコンテナー イメージ。 |
| `pt-pt`                     | `pt-PT` ロケールのコンテナー イメージ。 |
| `ru-ru`                     | `ru-RU` ロケールのコンテナー イメージ。 |
| `sv-se`                     | `sv-SE` ロケールのコンテナー イメージ。 |
| `ta-in`                     | `ta-IN` ロケールのコンテナー イメージ。 |
| `te-in`                     | `te-IN` ロケールのコンテナー イメージ。 |
| `th-th`                     | `th-TH` ロケールのコンテナー イメージ。 |
| `tr-tr`                     | `tr-TR` ロケールのコンテナー イメージ。 |
| `zh-cn`                     | `zh-CN` ロケールのコンテナー イメージ。 |
| `zh-hk`                     | `zh-HK` ロケールのコンテナー イメージ。 |
| `zh-tw`                     | `zh-TW` ロケールのコンテナー イメージ。 |

---

## <a name="text-to-speech"></a>テキスト読み上げ

[テキスト読み上げ][sp-tts]コンテナー イメージは `mcr.microsoft.com` コンテナー レジストリ シンジケートにあります。 `azure-cognitive-services/speechservices/` リポジトリ内にあり、`text-to-speech` という名前が付いています。 完全修飾コンテナー イメージ名は `mcr.microsoft.com/azure-cognitive-services/speechservices/text-to-speech` です。

このコンテナー イメージには次のタグを利用できます。 また、[MCR でタグ](https://mcr.microsoft.com/v2/azure-cognitive-services/speechservices/text-to-speech/tags/list)の完全な一覧を確認することもできます。


# <a name="latest-version"></a>[最新バージョン](#tab/current)

`1.9.0-amd64-<locale-and-voice>` のリリース ノート:

* 定期的な毎月のリリース

| イメージ タグ                                  | Notes                                                                                                         |
|---------------------------------------------|:--------------------------------------------------------------------------------------------------------------|
| `latest`                                    | `en-US` ロケールと `en-US-AriaRUS` 音声のコンテナー イメージ。                                            | 
| `1.9.0-amd64-<locale-and-voice>`            | `<locale>` を、以下に一覧表示されている使用可能なロケールのいずれかに置き換えます。 たとえば、「 `1.9.0-amd64-en-us-ariarus` 」のように指定します。  |


| v1.9.0 のロケール                          | Notes                                                                      | ダイジェスト                         |
|---------------------------------------------|:---------------------------------------------------------------------------|:-------------------------------|
| `ar-eg-hoda`                                | `ar-EG` ロケールと `ar-EG-Hoda` 音声のコンテナー イメージ。            | `sha256:2b19cfd2212d6517b286aa18617d2f9d1dd1520078b559cbbf9240599270d10` | 
| `ar-sa-naayf`                               | `ar-SA` ロケールと `ar-SA-Naayf` 音声のコンテナー イメージ。           | `sha256:6063aae5fb15c62b234cf945220916516a06ca81354c5311dee02af4d8cb0d3` |
| `bg-bg-ivan`                                | `bg-BG` ロケールと `bg-BG-Ivan` 音声のコンテナー イメージ。            | `sha256:c6786916464755e64ffa64e69e8f3e7ef16115bac00bb6ea1e45368c42c58d1` |
| `ca-es-herenarus`                           | `ca-ES` ロケールと `ca-ES-HerenaRUS` 音声のコンテナー イメージ。       | `sha256:2a8a1accbf99e2746c9345b77e2f261e0111227312c402cc2e1cd8760cdc82a` |
| `cs-cz-jakub`                               | `cs-CZ` ロケールと `cs-CZ-Jakub` 音声のコンテナー イメージ。           | `sha256:3e464356bb08c9c966af2b28a88ccafd591aecd2e37a0fedb356bd443720e8d` |
| `da-dk-hellerus`                            | `da-DK` ロケールと `da-DK-HelleRUS` 音声のコンテナー イメージ。        | `sha256:b85c43080804103673ff99dddea644a516c4103e8b1f11fa3dd34857492cd40` |
| `de-at-michael`                             | `de-AT` ロケールと `de-AT-Michael` 音声のコンテナー イメージ。         | `sha256:87b57ee61f964e4d72e75d860c499fa3b3d8dbda6a96c97d696beb20aa8b2a9` |
| `de-ch-karsten`                             | `de-CH` ロケールと `de-CH-Karsten` 音声のコンテナー イメージ。         | `sha256:ab1385b9746f4f054204302b9d564a433ae03748021b8ed71b4a3a224af1e9b` |
| `de-de-heddarus`                            | `de-DE` ロケールと `de-DE-Hedda` 音声のコンテナー イメージ。           | `sha256:82185a710c87f9dde678d88036867559ab3bf5f08f234d60d1548d3e106db57` |
| `de-de-hedda`                               | `de-DE` ロケールと `de-DE-Hedda` 音声のコンテナー イメージ。           | `sha256:82185a710c87f9dde678d88036867559ab3bf5f08f234d60d1548d3e106db57` |
| `de-de-stefan-apollo`                       | `de-DE` ロケールと `de-DE-Stefan-Apollo` 音声のコンテナー イメージ。   | `sha256:56a1c63e7e6a0f5623ddc1f6a44ac6e51471d073e02e14e8c8b1e577930d816` |
| `el-gr-stefanos`                            | `el-GR` ロケールと `el-GR-Stefanos` 音声のコンテナー イメージ。        | `sha256:ccbbb09f29ff8f276e246037183c7a3e9a3eb5bf33a942b22205cce3c6857f2` |
| `en-au-catherine`                           | `en-AU` ロケールと `en-AU-Catherine` 音声のコンテナー イメージ。       | `sha256:0c7374890f963e1ae9507e89dc9965a94723bd57802826c0677cd5262189783` |
| `en-au-hayleyrus`                           | `en-AU` ロケールと `en-AU-HayleyRUS` 音声のコンテナー イメージ。       | `sha256:7430bf8eace8294ca085f36ea56399261b2b4f69027e86649e8f3868fc3d811` |
| `en-ca-heatherrus`                          | `en-CA` ロケールと `en-CA-HeatherRUS` 音声のコンテナー イメージ。      | `sha256:0166ce1de3d669ea4ad80738c63369b7032125a54ecabade07241d740a94cfe` |
| `en-ca-linda`                               | `en-CA` ロケールと `en-CA-Linda` 音声のコンテナー イメージ。           | `sha256:50bed6a7bde9b793d307bcc3ace4c0f28d4a33c7a4dad9b3a394dc39a3e1c28` |
| `en-gb-george-apollo`                       | `en-GB` ロケールと `en-GB-George-Apollo` 音声のコンテナー イメージ。   | `sha256:50b800c0018a39609ddb1cee1b10062bf38a907644c393d20786db7c3ade748` |
| `en-gb-hazelrus`                            | `en-GB` ロケールと `en-GB-HazelRUS` 音声のコンテナー イメージ。        | `sha256:2aa79394dfeac8cec0cc1704a5199949cfccf347fe61161d02c7000c4ffcfa6` |
| `en-gb-susan-apollo`                        | `en-GB` ロケールと `en-GB-Susan-Apollo` 音声のコンテナー イメージ。    | `sha256:7a3174b3aae5f10241e731d392b56f124808cdd506f881ced919ced73d836c0` |
| `en-ie-sean`                                | `en-IE` ロケールと `en-IE-Sean` 音声のコンテナー イメージ。            | `sha256:2457202fadb2354fc8d3666432096bd87c07760a4e3f4dbcc49853fff658577` |
| `en-in-heera-apollo`                        | `en-IN` ロケールと `en-IN-Heera-Apollo` 音声のコンテナー イメージ。    | `sha256:e4068cd7ca4272ea94819e2ba8743d2a76c8710b162db5e9ecbde6c92c12877` |
| `en-in-priyarus`                            | `en-IN` ロケールと `en-IN-PriyaRUS` 音声のコンテナー イメージ。        | `sha256:9d63a0ed53ac06178ab84588551421c0e1d04b8bad3321410ebb99c3ca2a9e8` |
| `en-in-ravi-apollo`                         | `en-IN` ロケールと `en-IN-Ravi-Apollo` 音声のコンテナー イメージ。     | `sha256:67049c9ce591336655943f5030afcfdaa150a8aace7b372425a69cc33a6b7b9` |
| `en-us-aria24krus`                          | `en-US` ロケールと `en-US-Aria24kRUS` 音声のコンテナー イメージ。      | `sha256:a95acf6874bf3df7ae8e96be779f80cb5405d21250227b0c4b3ddbcb3014082` |
| `en-us-ariarus`                             | `en-US` ロケールと `en-US-AriaRUS` 音声のコンテナー イメージ。         | `sha256:a95acf6874bf3df7ae8e96be779f80cb5405d21250227b0c4b3ddbcb3014082` |
| `en-us-benjaminrus`                         | `en-US` ロケールと `en-US-BenjaminRUS` 音声のコンテナー イメージ。     | `sha256:93cd49adaaa2a1bdfb06ab655be164ae66f206cb7c03a2cbd59e5fba70610ab` |
| `en-us-guy24krus`                           | `en-US` ロケールと `en-US-Guy24kRUS` 音声のコンテナー イメージ。       | `sha256:7b788bfcaae4c63c274ca15924bfd861cfcafd5fec13f685d80babc25b2949d` |
| `en-us-zirarus`                             | `en-US` ロケールと `en-US-ZiraRUS` 音声のコンテナー イメージ。         | `sha256:bfc87a77df5695ad43481348500fba8f6a7b495708fba200706049469b5ba97` |
| `es-es-helenarus`                           | `es-ES` ロケールと `es-ES-HelenaRUS` 音声のコンテナー イメージ。       | `sha256:0b6c17aca75efb64aa9bfc0d83303038fe58d4b2fb1fc94c9380a4335b80796` |
| `es-es-laura-apollo`                        | `es-ES` ロケールと `es-ES-Laura-Apollo` 音声のコンテナー イメージ。    | `sha256:d6fcffc944c37a2dd0de29c39b82f3f8cce3a95ad925d2814ed7538335d5d4f` |
| `es-es-pablo-apollo`                        | `es-ES` ロケールと `es-ES-Pablo-Apollo` 音声のコンテナー イメージ。    | `sha256:a460bc53d9083d3c3770129995cf96cc1069ae4e8101f1739d304fe210f0af0` |
| `es-mx-hildarus`                            | `es-MX` ロケールと `es-MX-HildaRUS` 音声のコンテナー イメージ。        | `sha256:5b7578fc5b00158dfa674d95a3f1d57f22eb285e8333b4006d1fe1808bda7ba` |
| `es-mx-raul-apollo`                         | `es-MX` ロケールと `es-MX-Raul-Apollo` 音声のコンテナー イメージ。     | `sha256:03922fb017783c86d788c72e01c7ede440f8f3c913c86cab19bad4dfc2e4a2b` |
| `fi-fi-heidirus`                            | `fi-FI` ロケールと `fi-FI-HeidiRUS` 音声のコンテナー イメージ。        | `sha256:146c1f98d6fa061016eba41db6e7b654eef222d37f35406d4b43477bb2ff897` |
| `fr-ca-caroline`                            | `fr-CA` ロケールと `fr-CA-Caroline` 音声のコンテナー イメージ。        | `sha256:1ee2e53f12ad1c72665d2aef64e9d4a7f9ea05670cad84dcae5e75409494f32` |
| `fr-ca-harmonierus`                         | `fr-CA` ロケールと `fr-CA-HarmonieRUS` 音声のコンテナー イメージ。     | `sha256:a21d25d3ac699af4e9ba9194aadd9b45f35fd9205224f3429a4c7da41fc38fe` |
| `fr-ch-guillaume`                           | `fr-CH` ロケールと `fr-CH-Guillaume` 音声のコンテナー イメージ。       | `sha256:216125a9bd89a95d3c4dc2d7e031398659427b3aa7d4663d23a65737972e42b` |
| `fr-fr-hortenserus`                         | `fr-FR` ロケールと `fr-FR-HortenseRUS` 音声のコンテナー イメージ。     | `sha256:795a698120eecbd80c48e738f73300739c1698ca859130ddb4236317bcdf70f` |
| `fr-fr-julie-apollo`                        | `fr-FR` ロケールと `fr-FR-Julie-Apollo` 音声のコンテナー イメージ。    | `sha256:f6eb70d523c435c2e3a713b32a8af4a781df7ec043caad2fc7f458ee341eb2f` |
| `fr-fr-paul-apollo`                         | `fr-FR` ロケールと `fr-FR-Paul-Apollo` 音声のコンテナー イメージ。     | `sha256:28864c662a20f459b3051b1da2967a605e06267e6408285f7c2552748cf4eed` |
| `he-il-asaf`                                | `he-IL` ロケールと `he-IL-Asaf` 音声のコンテナー イメージ。            | `sha256:eaa834bac6b69abef096b36a8baead741db78fe438af3d30f60abde3631d639` |
| `hi-in-hemant`                              | `hi-IN` ロケールと `hi-IN-Hemant` 音声のコンテナー イメージ。          | `sha256:cfea0fa7cce9cc512f2fbb8b76f1c00fe5c32fad853c90b15934cf4ee6262fa` |
| `hi-in-kalpana-apollo`                      | `hi-IN` ロケールと `hi-IN-Kalpana-Apollo` 音声のコンテナー イメージ。  | `sha256:afbd6cc0413f3a3c9f6df044b6df6d9dac9e8e888c2cb619fefbdc3e105c644` |
| `hi-in-kalpana`                             | `hi-IN` ロケールと `hi-IN-Kalpana` 音声のコンテナー イメージ。         | `sha256:afbd6cc0413f3a3c9f6df044b6df6d9dac9e8e888c2cb619fefbdc3e105c644` |
| `hr-hr-matej`                               | `hr-HR` ロケールと `hr-HR-Matej` 音声のコンテナー イメージ。           | `sha256:86683597c62752b4d769b69e5294979fafd4c277aaef1536e1cb19f9f06c0bf` |
| `hu-hu-szabolcs`                            | `hu-HU` ロケールと `hu-HU-Szabolcs` 音声のコンテナー イメージ。        | `sha256:aa64eed28ca2ad060e2e02188e0401bf34e4caf7e2182b70a30ce33b3c11c9c` |
| `id-id-andika`                              | `id-ID` ロケールと `id-ID-Andika` 音声のコンテナー イメージ。          | `sha256:0e1394d231a57a1df8163ccb634dc2ef2f8103b10608a40ab3efc5c0fbe9ded` |
| `it-it-cosimo-apollo`                       | `it-IT` ロケールと `it-IT-Cosimo-Apollo` 音声のコンテナー イメージ。   | `sha256:eef97f2817fc24405823a5fe4e825244db32279b44c0e6631e8ad9a5c1acf40` |
| `it-it-luciarus`                            | `it-IT` ロケールと `it-IT-LuciaRUS` 音声のコンテナー イメージ。        | `sha256:ebc331b0685f482d2f55619fa81fd451fd7c8f107f9cd7ad159bc6213ae4e33` |
| `ja-jp-ayumi-apollo`                        | `ja-JP` ロケールと `ja-JP-Ayumi-Apollo` 音声のコンテナー イメージ。    | `sha256:e9cb7dfd2eec154c8f3d530c16b66e8558c5955a2edaede69740067f00e43cf` |
| `ja-jp-harukarus`                           | `ja-JP` ロケールと `ja-JP-HarukaRUS` 音声のコンテナー イメージ。       | `sha256:93ce2ef6177c0d8ac70b61df8b11fcbcdfd3c0be0cc51cd8644f26679a741c2` |
| `ja-jp-ichiro-apollo`                       | `ja-JP` ロケールと `ja-JP-Ichiro-Apollo` 音声のコンテナー イメージ。   | `sha256:6a18bae69ac63b42ba992b8b74d8d31d91ca984d61b5f62f38be988cf38645e` |
| `ko-kr-heamirus`                            | `ko-KR` ロケールと `ko-KR-HeamiRUS` 音声のコンテナー イメージ。        | `sha256:7a48252d4ada2af43f9266a70113426d330bac192348cbdc929022295a0e727` |
| `ms-my-rizwan`                              | `ms-MY` ロケールと `ms-MY-Rizwan` 音声のコンテナー イメージ。          | `sha256:90e2ecac14f8e960934fd013d208fc2a0afe1bfff037d5648d422bda8d8a76e` |
| `nb-no-huldarus`                            | `nb-NO` ロケールと `nb-NO-HuldaRUS` 音声のコンテナー イメージ。        | `sha256:217b61bd6244b5effda8f12a2c563ce1b4572e9c5b8a08df143665f9ff754e4` |
| `nl-nl-hannarus`                            | `nl-NL` ロケールと `nl-NL-HannaRUS` 音声のコンテナー イメージ。        | `sha256:fbff48dfc9dfadadf377867b28f6e3a3bd605e59da20f77a531efcc7d85d16e` |
| `pl-pl-paulinarus`                          | `pl-PL` ロケールと `pl-PL-PaulinaRUS` 音声のコンテナー イメージ。      | `sha256:856a033a09925773fa4b4531e199ab7c03c537f366acecbda60f8d21735725e` |
| `pt-br-daniel-apollo`                       | `pt-BR` ロケールと `pt-BR-Daniel-Apollo` 音声のコンテナー イメージ。   | `sha256:2d1ec975f1aee56a6fc6039d154fb3f2fbeb4636f7078c5dfe99aeddb6a3634` |
| `pt-br-heloisarus`                          | `pt-BR` ロケールと `pt-BR-HeloisaRUS` 音声のコンテナー イメージ。      | `sha256:b7d629f37ab3305274764264dc08fab5236e60ef18d40e987618115db67ce44` |
| `pt-pt-heliarus`                            | `pt-PT` ロケールと `pt-PT-HeliaRUS` 音声のコンテナー イメージ。        | `sha256:8b380ae7e4aac9d4ada4d15fa9e667387bc9ca038796d9b6999953bfbc97259` |
| `ro-ro-andrei`                              | `ro-RO` ロケールと `ro-RO-Andrei` 音声のコンテナー イメージ。          | `sha256:b00ca7f1411169a5baf7263a8d7e5eed1a72084d9489eaf458429dfc338564a` |
| `ru-ru-ekaterinarus`                        | `ru-RU` ロケールと `ru-RU-EkaterinaRUS` 音声のコンテナー イメージ。    | `sha256:31c588c31e3ac67305af66091e7756dfc4ca454317d0228116ea0b2fedf5d71` |
| `ru-ru-irina-apollo`                        | `ru-RU` ロケールと `ru-RU-Irina-Apollo` 音声のコンテナー イメージ。    | `sha256:e76437f8da7c279b38d2643defc997a13b4a364e9a212895cdb33a9a3f6457f` |
| `ru-ru-pavel-apollo`                        | `ru-RU` ロケールと `ru-RU-Pavel-Apollo` 音声のコンテナー イメージ。    | `sha256:461c1efa6cce0b10a87f338bc637aca76aef8458061a688870fb3343d682da0` |
| `sk-sk-filip`                               | `sk-SK` ロケールと `sk-SK-Filip` 音声のコンテナー イメージ。           | `sha256:7fb0cfab4c0fe2913eb20f28a25c6663015d62f82e7e7864d9f7fac2d27697b` |
| `sl-si-lado`                                | `sl-SI` ロケールと `sl-SI-Lado` 音声のコンテナー イメージ。            | `sha256:5336173d410e10ffeb5dc211a583887e33754319c757914955057d398dfbb0a` |
| `sv-se-hedvigrus`                           | `sv-SE` ロケールと `sv-SE-HedvigRUS` 音声のコンテナー イメージ。       | `sha256:5dc8cdcc3054386bf69596707d9d261d4db5bfd09f1882ceb4e29238a34b24e` |
| `ta-in-valluvar`                            | `ta-IN` ロケールと `ta-IN-Valluvar` 音声のコンテナー イメージ。        | `sha256:74ea485f23e4c1fe0029e06894860aa0188c36c0e14ea3584a06d4216ccef56` |
| `te-in-chitra`                              | `te-IN` ロケールと `te-IN-Chitra` 音声のコンテナー イメージ。          | `sha256:ff2977a98ef691da543db08be9cfe04d7fc3bf8f78b29310c163e47303b2ddd` |
| `th-th-pattara`                             | `th-TH` ロケールと `th-TH-Pattara` 音声のコンテナー イメージ。         | `sha256:ba7e2c0e5e75d9f2b52aa50c97728616c43e81f48c15e24665e4c2ea5770a8f` |
| `tr-tr-sedarus`                             | `tr-TR` ロケールと `tr-TR-SedaRUS` 音声のコンテナー イメージ。         | `sha256:375a8ceae89ea1f0dda551feff30ae3679231189b527992edbc49988d042d66` |
| `vi-vn-an`                                  | `vi-VN` ロケールと `vi-VN-An` 音声のコンテナー イメージ。              | `sha256:b6f82148295b38b4039c45c48695ec50b4e97cd02b18d49c39bf9fca3bec958` |
| `zh-cn-huihuirus`                           | `zh-CN` ロケールと `zh-CN-HuihuiRUS` 音声のコンテナー イメージ。       | `sha256:3e773931f3adaac92cba43773a241692a2b471ebe73ec51c475df8ff63b7ee1` |
| `zh-cn-kangkang-apollo`                     | `zh-CN` ロケールと `zh-CN-Kangkang-Apollo` 音声のコンテナー イメージ。 | `sha256:05fc0d5075a1094caf70d98b4a9469952be52cb6eb4d9f7b9ff4ae961100c7b` |
| `zh-cn-yaoyao-apollo`                       | `zh-CN` ロケールと `zh-CN-Yaoyao-Apollo` 音声のコンテナー イメージ。   | `sha256:d7613bcefc48e85b9d6f07c8cd223c16d4958bcf7f24087575250e97c593ac1` |
| `zh-hk-danny-apollo`                        | `zh-HK` ロケールと `zh-HK-Danny-Apollo` 音声のコンテナー イメージ。    | `sha256:efe22bc123dac9312dcaeb859a377d81f61fbb25ef46e4678d36ec6bebc5d32` |
| `zh-hk-tracy-apollo`                        | `zh-HK` ロケールと `zh-HK-Tracy-Apollo` 音声のコンテナー イメージ。    | `sha256:802c60bc65012c03ffe96268dca79b8c6dcd0c5cc6180ec271c50ef5c9ba132` |
| `zh-hk-tracyrus`                            | `zh-HK` ロケールと `zh-HK-TracyRUS` 音声のコンテナー イメージ。        | `sha256:802c60bc65012c03ffe96268dca79b8c6dcd0c5cc6180ec271c50ef5c9ba132` |
| `zh-tw-hanhanrus`                           | `zh-TW` ロケールと `zh-TW-HanHanRUS` 音声のコンテナー イメージ。       | `sha256:95d58922463d577d4c4722ab722a5768af35fb62236d47f6709717dea758909` |
| `zh-tw-yating-apollo`                       | `zh-TW` ロケールと `zh-TW-Yating-Apollo` 音声のコンテナー イメージ。   | `sha256:33eec6e3aaaedafaf3969746eeaf97a1760e763505decfe2abaa03f5054bfd2` |
| `zh-tw-zhiwei-apollo`                       | `zh-TW` ロケールと `zh-TW-Zhiwei-Apollo` 音声のコンテナー イメージ。   | `sha256:456db2898b2e5a9c30b7071ce6ea3f141438cbf1aa4899c7ffccfc2f0dde5bd` |


# <a name="previous-version"></a>[以前のバージョン](#tab/previous)

`1.8.0-amd64-<locale-and-voice>` のリリース ノート:

**機能**

* .NET 3.1 に完全に移行しました

`1.7.0-amd64-<locale-and-voice>` のリリース ノート:

**機能**

* コンポーネントを .NET 3.1 にアップグレードしました

| イメージ タグ                                  | Notes                                                                                                         |
|---------------------------------------------|:--------------------------------------------------------------------------------------------------------------|
| `1.8.0-amd64-<locale-and-voice>`            | `<locale>` を、以下に一覧表示されている使用可能なロケールのいずれかに置き換えます。 たとえば、「 `1.8.0-amd64-en-us-ariarus` 」のように指定します。  |
| `1.7.0-amd64-<locale-and-voice>`            | 最初の GA バージョン。 `<locale>` を、以下に一覧表示されている使用可能なロケールのいずれかに置き換えます。 たとえば、「 `1.7.0-amd64-en-us-ariarus` 」のように指定します。  |


| v1.8.0 のロケール                          | Notes                                                                      |
|---------------------------------------------|:---------------------------------------------------------------------------|
| `ar-eg-hoda`                                | `ar-EG` ロケールと `ar-EG-Hoda` 音声のコンテナー イメージ。            |
| `ar-sa-naayf`                               | `ar-SA` ロケールと `ar-SA-Naayf` 音声のコンテナー イメージ。           |
| `bg-bg-ivan`                                | `bg-BG` ロケールと `bg-BG-Ivan` 音声のコンテナー イメージ。            |
| `ca-es-herenarus`                           | `ca-ES` ロケールと `ca-ES-HerenaRUS` 音声のコンテナー イメージ。       |
| `cs-cz-jakub`                               | `cs-CZ` ロケールと `cs-CZ-Jakub` 音声のコンテナー イメージ。           |
| `da-dk-hellerus`                            | `da-DK` ロケールと `da-DK-HelleRUS` 音声のコンテナー イメージ。        |
| `de-at-michael`                             | `de-AT` ロケールと `de-AT-Michael` 音声のコンテナー イメージ。         |
| `de-ch-karsten`                             | `de-CH` ロケールと `de-CH-Karsten` 音声のコンテナー イメージ。         |
| `de-de-hedda`                               | `de-DE` ロケールと `de-DE-Hedda` 音声のコンテナー イメージ。           |
| `de-de-heddarus`                            | `de-DE` ロケールと `de-DE-Hedda` 音声のコンテナー イメージ。           |
| `de-de-stefan-apollo`                       | `de-DE` ロケールと `de-DE-Stefan-Apollo` 音声のコンテナー イメージ。   |
| `el-gr-stefanos`                            | `el-GR` ロケールと `el-GR-Stefanos` 音声のコンテナー イメージ。        |
| `en-au-catherine`                           | `en-AU` ロケールと `en-AU-Catherine` 音声のコンテナー イメージ。       |
| `en-au-hayleyrus`                           | `en-AU` ロケールと `en-AU-HayleyRUS` 音声のコンテナー イメージ。       |
| `en-ca-heatherrus`                          | `en-CA` ロケールと `en-CA-HeatherRUS` 音声のコンテナー イメージ。      |
| `en-ca-linda`                               | `en-CA` ロケールと `en-CA-Linda` 音声のコンテナー イメージ。           |
| `en-gb-george-apollo`                       | `en-GB` ロケールと `en-GB-George-Apollo` 音声のコンテナー イメージ。   |
| `en-gb-hazelrus`                            | `en-GB` ロケールと `en-GB-HazelRUS` 音声のコンテナー イメージ。        |
| `en-gb-susan-apollo`                        | `en-GB` ロケールと `en-GB-Susan-Apollo` 音声のコンテナー イメージ。    |
| `en-ie-sean`                                | `en-IE` ロケールと `en-IE-Sean` 音声のコンテナー イメージ。            |
| `en-in-heera-apollo`                        | `en-IN` ロケールと `en-IN-Heera-Apollo` 音声のコンテナー イメージ。    |
| `en-in-priyarus`                            | `en-IN` ロケールと `en-IN-PriyaRUS` 音声のコンテナー イメージ。        |
| `en-in-ravi-apollo`                         | `en-IN` ロケールと `en-IN-Ravi-Apollo` 音声のコンテナー イメージ。     |
| `en-us-benjaminrus`                         | `en-US` ロケールと `en-US-BenjaminRUS` 音声のコンテナー イメージ。     |
| `en-us-guy24krus`                           | `en-US` ロケールと `en-US-Guy24kRUS` 音声のコンテナー イメージ。       |
| `en-us-aria24krus`                          | `en-US` ロケールと `en-US-Aria24kRUS` 音声のコンテナー イメージ。      |
| `en-us-ariarus`                             | `en-US` ロケールと `en-US-AriaRUS` 音声のコンテナー イメージ。         |
| `en-us-zirarus`                             | `en-US` ロケールと `en-US-ZiraRUS` 音声のコンテナー イメージ。         |
| `es-es-helenarus`                           | `es-ES` ロケールと `es-ES-HelenaRUS` 音声のコンテナー イメージ。       |
| `es-es-laura-apollo`                        | `es-ES` ロケールと `es-ES-Laura-Apollo` 音声のコンテナー イメージ。    |
| `es-es-pablo-apollo`                        | `es-ES` ロケールと `es-ES-Pablo-Apollo` 音声のコンテナー イメージ。    |
| `es-mx-hildarus`                            | `es-MX` ロケールと `es-MX-HildaRUS` 音声のコンテナー イメージ。        |
| `es-mx-raul-apollo`                         | `es-MX` ロケールと `es-MX-Raul-Apollo` 音声のコンテナー イメージ。     |
| `fi-fi-heidirus`                            | `fi-FI` ロケールと `fi-FI-HeidiRUS` 音声のコンテナー イメージ。        |
| `fr-ca-caroline`                            | `fr-CA` ロケールと `fr-CA-Caroline` 音声のコンテナー イメージ。        |
| `fr-ca-harmonierus`                         | `fr-CA` ロケールと `fr-CA-HarmonieRUS` 音声のコンテナー イメージ。     |
| `fr-ch-guillaume`                           | `fr-CH` ロケールと `fr-CH-Guillaume` 音声のコンテナー イメージ。       |
| `fr-fr-hortenserus`                         | `fr-FR` ロケールと `fr-FR-HortenseRUS` 音声のコンテナー イメージ。     |
| `fr-fr-julie-apollo`                        | `fr-FR` ロケールと `fr-FR-Julie-Apollo` 音声のコンテナー イメージ。    |
| `fr-fr-paul-apollo`                         | `fr-FR` ロケールと `fr-FR-Paul-Apollo` 音声のコンテナー イメージ。     |
| `he-il-asaf`                                | `he-IL` ロケールと `he-IL-Asaf` 音声のコンテナー イメージ。            |
| `hi-in-hemant`                              | `hi-IN` ロケールと `hi-IN-Hemant` 音声のコンテナー イメージ。          |
| `hi-in-kalpana-apollo`                      | `hi-IN` ロケールと `hi-IN-Kalpana-Apollo` 音声のコンテナー イメージ。  |
| `hi-in-kalpana`                             | `hi-IN` ロケールと `hi-IN-Kalpana` 音声のコンテナー イメージ。         |
| `hr-hr-matej`                               | `hr-HR` ロケールと `hr-HR-Matej` 音声のコンテナー イメージ。           |
| `hu-hu-szabolcs`                            | `hu-HU` ロケールと `hu-HU-Szabolcs` 音声のコンテナー イメージ。        |
| `id-id-andika`                              | `id-ID` ロケールと `id-ID-Andika` 音声のコンテナー イメージ。          |
| `it-it-cosimo-apollo`                       | `it-IT` ロケールと `it-IT-Cosimo-Apollo` 音声のコンテナー イメージ。   |
| `it-it-luciarus`                            | `it-IT` ロケールと `it-IT-LuciaRUS` 音声のコンテナー イメージ。        |
| `ja-jp-ayumi-apollo`                        | `ja-JP` ロケールと `ja-JP-Ayumi-Apollo` 音声のコンテナー イメージ。    |
| `ja-jp-harukarus`                           | `ja-JP` ロケールと `ja-JP-HarukaRUS` 音声のコンテナー イメージ。       |
| `ja-jp-ichiro-apollo`                       | `ja-JP` ロケールと `ja-JP-Ichiro-Apollo` 音声のコンテナー イメージ。   |
| `ko-kr-heamirus`                            | `ko-KR` ロケールと `ko-KR-HeamiRUS` 音声のコンテナー イメージ。        |
| `ms-my-rizwan`                              | `ms-MY` ロケールと `ms-MY-Rizwan` 音声のコンテナー イメージ。          |
| `nb-no-huldarus`                            | `nb-NO` ロケールと `nb-NO-HuldaRUS` 音声のコンテナー イメージ。        |
| `nl-nl-hannarus`                            | `nl-NL` ロケールと `nl-NL-HannaRUS` 音声のコンテナー イメージ。        |
| `pl-pl-paulinarus`                          | `pl-PL` ロケールと `pl-PL-PaulinaRUS` 音声のコンテナー イメージ。      |
| `pt-br-daniel-apollo`                       | `pt-BR` ロケールと `pt-BR-Daniel-Apollo` 音声のコンテナー イメージ。   |
| `pt-br-heloisarus`                          | `pt-BR` ロケールと `pt-BR-HeloisaRUS` 音声のコンテナー イメージ。      |
| `pt-pt-heliarus`                            | `pt-PT` ロケールと `pt-PT-HeliaRUS` 音声のコンテナー イメージ。        |
| `ro-ro-andrei`                              | `ro-RO` ロケールと `ro-RO-Andrei` 音声のコンテナー イメージ。          |
| `ru-ru-ekaterinarus`                        | `ru-RU` ロケールと `ru-RU-EkaterinaRUS` 音声のコンテナー イメージ。    |
| `ru-ru-irina-apollo`                        | `ru-RU` ロケールと `ru-RU-Irina-Apollo` 音声のコンテナー イメージ。    |
| `ru-ru-pavel-apollo`                        | `ru-RU` ロケールと `ru-RU-Pavel-Apollo` 音声のコンテナー イメージ。    |
| `sk-sk-filip`                               | `sk-SK` ロケールと `sk-SK-Filip` 音声のコンテナー イメージ。           |
| `sl-si-lado`                                | `sl-SI` ロケールと `sl-SI-Lado` 音声のコンテナー イメージ。            |
| `sv-se-hedvigrus`                           | `sv-SE` ロケールと `sv-SE-HedvigRUS` 音声のコンテナー イメージ。       |
| `ta-in-valluvar`                            | `ta-IN` ロケールと `ta-IN-Valluvar` 音声のコンテナー イメージ。        |
| `te-in-chitra`                              | `te-IN` ロケールと `te-IN-Chitra` 音声のコンテナー イメージ。          |
| `th-th-pattara`                             | `th-TH` ロケールと `th-TH-Pattara` 音声のコンテナー イメージ。         |
| `tr-tr-sedarus`                             | `tr-TR` ロケールと `tr-TR-SedaRUS` 音声のコンテナー イメージ。         |
| `vi-vn-an`                                  | `vi-VN` ロケールと `vi-VN-An` 音声のコンテナー イメージ。              |
| `zh-cn-huihuirus`                           | `zh-CN` ロケールと `zh-CN-HuihuiRUS` 音声のコンテナー イメージ。       |
| `zh-cn-kangkang-apollo`                     | `zh-CN` ロケールと `zh-CN-Kangkang-Apollo` 音声のコンテナー イメージ。 |
| `zh-cn-yaoyao-apollo`                       | `zh-CN` ロケールと `zh-CN-Yaoyao-Apollo` 音声のコンテナー イメージ。   |
| `zh-hk-danny-apollo`                        | `zh-HK` ロケールと `zh-HK-Danny-Apollo` 音声のコンテナー イメージ。    |
| `zh-hk-tracy-apollo`                        | `zh-HK` ロケールと `zh-HK-Tracy-Apollo` 音声のコンテナー イメージ。    |
| `zh-hk-tracyrus`                            | `zh-HK` ロケールと `zh-HK-TracyRUS` 音声のコンテナー イメージ。        |
| `zh-tw-hanhanrus`                           | `zh-TW` ロケールと `zh-TW-HanHanRUS` 音声のコンテナー イメージ。       |
| `zh-tw-yating-apollo`                       | `zh-TW` ロケールと `zh-TW-Yating-Apollo` 音声のコンテナー イメージ。   |
| `zh-tw-zhiwei-apollo`                       | `zh-TW` ロケールと `zh-TW-Zhiwei-Apollo` 音声のコンテナー イメージ。   |

| V 1.7.0 のロケール                          | Notes                                                                      |
|---------------------------------------------|:---------------------------------------------------------------------------|
| `ar-eg-hoda`                                | `ar-EG` ロケールと `ar-EG-Hoda` 音声のコンテナー イメージ。            |
| `ar-sa-naayf`                               | `ar-SA` ロケールと `ar-SA-Naayf` 音声のコンテナー イメージ。           |
| `bg-bg-ivan`                                | `bg-BG` ロケールと `bg-BG-Ivan` 音声のコンテナー イメージ。            |
| `ca-es-herenarus`                           | `ca-ES` ロケールと `ca-ES-HerenaRUS` 音声のコンテナー イメージ。       |
| `cs-cz-jakub`                               | `cs-CZ` ロケールと `cs-CZ-Jakub` 音声のコンテナー イメージ。           |
| `da-dk-hellerus`                            | `da-DK` ロケールと `da-DK-HelleRUS` 音声のコンテナー イメージ。        |
| `de-at-michael`                             | `de-AT` ロケールと `de-AT-Michael` 音声のコンテナー イメージ。         |
| `de-ch-karsten`                             | `de-CH` ロケールと `de-CH-Karsten` 音声のコンテナー イメージ。         |
| `de-de-hedda`                               | `de-DE` ロケールと `de-DE-Hedda` 音声のコンテナー イメージ。           |
| `de-de-heddarus`                            | `de-DE` ロケールと `de-DE-Hedda` 音声のコンテナー イメージ。           |
| `de-de-stefan-apollo`                       | `de-DE` ロケールと `de-DE-Stefan-Apollo` 音声のコンテナー イメージ。   |
| `el-gr-stefanos`                            | `el-GR` ロケールと `el-GR-Stefanos` 音声のコンテナー イメージ。        |
| `en-au-catherine`                           | `en-AU` ロケールと `en-AU-Catherine` 音声のコンテナー イメージ。       |
| `en-au-hayleyrus`                           | `en-AU` ロケールと `en-AU-HayleyRUS` 音声のコンテナー イメージ。       |
| `en-ca-heatherrus`                          | `en-CA` ロケールと `en-CA-HeatherRUS` 音声のコンテナー イメージ。      |
| `en-ca-linda`                               | `en-CA` ロケールと `en-CA-Linda` 音声のコンテナー イメージ。           |
| `en-gb-george-apollo`                       | `en-GB` ロケールと `en-GB-George-Apollo` 音声のコンテナー イメージ。   |
| `en-gb-hazelrus`                            | `en-GB` ロケールと `en-GB-HazelRUS` 音声のコンテナー イメージ。        |
| `en-gb-susan-apollo`                        | `en-GB` ロケールと `en-GB-Susan-Apollo` 音声のコンテナー イメージ。    |
| `en-ie-sean`                                | `en-IE` ロケールと `en-IE-Sean` 音声のコンテナー イメージ。            |
| `en-in-heera-apollo`                        | `en-IN` ロケールと `en-IN-Heera-Apollo` 音声のコンテナー イメージ。    |
| `en-in-priyarus`                            | `en-IN` ロケールと `en-IN-PriyaRUS` 音声のコンテナー イメージ。        |
| `en-in-ravi-apollo`                         | `en-IN` ロケールと `en-IN-Ravi-Apollo` 音声のコンテナー イメージ。     |
| `en-us-benjaminrus`                         | `en-US` ロケールと `en-US-BenjaminRUS` 音声のコンテナー イメージ。     |
| `en-us-guy24krus`                           | `en-US` ロケールと `en-US-Guy24kRUS` 音声のコンテナー イメージ。       |
| `en-us-aria24krus`                          | `en-US` ロケールと `en-US-Aria24kRUS` 音声のコンテナー イメージ。      |
| `en-us-ariarus`                             | `en-US` ロケールと `en-US-AriaRUS` 音声のコンテナー イメージ。         |
| `en-us-zirarus`                             | `en-US` ロケールと `en-US-ZiraRUS` 音声のコンテナー イメージ。         |
| `es-es-helenarus`                           | `es-ES` ロケールと `es-ES-HelenaRUS` 音声のコンテナー イメージ。       |
| `es-es-laura-apollo`                        | `es-ES` ロケールと `es-ES-Laura-Apollo` 音声のコンテナー イメージ。    |
| `es-es-pablo-apollo`                        | `es-ES` ロケールと `es-ES-Pablo-Apollo` 音声のコンテナー イメージ。    |
| `es-mx-hildarus`                            | `es-MX` ロケールと `es-MX-HildaRUS` 音声のコンテナー イメージ。        |
| `es-mx-raul-apollo`                         | `es-MX` ロケールと `es-MX-Raul-Apollo` 音声のコンテナー イメージ。     |
| `fi-fi-heidirus`                            | `fi-FI` ロケールと `fi-FI-HeidiRUS` 音声のコンテナー イメージ。        |
| `fr-ca-caroline`                            | `fr-CA` ロケールと `fr-CA-Caroline` 音声のコンテナー イメージ。        |
| `fr-ca-harmonierus`                         | `fr-CA` ロケールと `fr-CA-HarmonieRUS` 音声のコンテナー イメージ。     |
| `fr-ch-guillaume`                           | `fr-CH` ロケールと `fr-CH-Guillaume` 音声のコンテナー イメージ。       |
| `fr-fr-hortenserus`                         | `fr-FR` ロケールと `fr-FR-HortenseRUS` 音声のコンテナー イメージ。     |
| `fr-fr-julie-apollo`                        | `fr-FR` ロケールと `fr-FR-Julie-Apollo` 音声のコンテナー イメージ。    |
| `fr-fr-paul-apollo`                         | `fr-FR` ロケールと `fr-FR-Paul-Apollo` 音声のコンテナー イメージ。     |
| `he-il-asaf`                                | `he-IL` ロケールと `he-IL-Asaf` 音声のコンテナー イメージ。            |
| `hi-in-hemant`                              | `hi-IN` ロケールと `hi-IN-Hemant` 音声のコンテナー イメージ。          |
| `hi-in-kalpana-apollo`                      | `hi-IN` ロケールと `hi-IN-Kalpana-Apollo` 音声のコンテナー イメージ。  |
| `hi-in-kalpana`                             | `hi-IN` ロケールと `hi-IN-Kalpana` 音声のコンテナー イメージ。         |
| `hr-hr-matej`                               | `hr-HR` ロケールと `hr-HR-Matej` 音声のコンテナー イメージ。           |
| `hu-hu-szabolcs`                            | `hu-HU` ロケールと `hu-HU-Szabolcs` 音声のコンテナー イメージ。        |
| `id-id-andika`                              | `id-ID` ロケールと `id-ID-Andika` 音声のコンテナー イメージ。          |
| `it-it-cosimo-apollo`                       | `it-IT` ロケールと `it-IT-Cosimo-Apollo` 音声のコンテナー イメージ。   |
| `it-it-luciarus`                            | `it-IT` ロケールと `it-IT-LuciaRUS` 音声のコンテナー イメージ。        |
| `ja-jp-ayumi-apollo`                        | `ja-JP` ロケールと `ja-JP-Ayumi-Apollo` 音声のコンテナー イメージ。    |
| `ja-jp-harukarus`                           | `ja-JP` ロケールと `ja-JP-HarukaRUS` 音声のコンテナー イメージ。       |
| `ja-jp-ichiro-apollo`                       | `ja-JP` ロケールと `ja-JP-Ichiro-Apollo` 音声のコンテナー イメージ。   |
| `ko-kr-heamirus`                            | `ko-KR` ロケールと `ko-KR-HeamiRUS` 音声のコンテナー イメージ。        |
| `ms-my-rizwan`                              | `ms-MY` ロケールと `ms-MY-Rizwan` 音声のコンテナー イメージ。          |
| `nb-no-huldarus`                            | `nb-NO` ロケールと `nb-NO-HuldaRUS` 音声のコンテナー イメージ。        |
| `nl-nl-hannarus`                            | `nl-NL` ロケールと `nl-NL-HannaRUS` 音声のコンテナー イメージ。        |
| `pl-pl-paulinarus`                          | `pl-PL` ロケールと `pl-PL-PaulinaRUS` 音声のコンテナー イメージ。      |
| `pt-br-daniel-apollo`                       | `pt-BR` ロケールと `pt-BR-Daniel-Apollo` 音声のコンテナー イメージ。   |
| `pt-br-heloisarus`                          | `pt-BR` ロケールと `pt-BR-HeloisaRUS` 音声のコンテナー イメージ。      |
| `pt-pt-heliarus`                            | `pt-PT` ロケールと `pt-PT-HeliaRUS` 音声のコンテナー イメージ。        |
| `ro-ro-andrei`                              | `ro-RO` ロケールと `ro-RO-Andrei` 音声のコンテナー イメージ。          |
| `ru-ru-ekaterinarus`                        | `ru-RU` ロケールと `ru-RU-EkaterinaRUS` 音声のコンテナー イメージ。    |
| `ru-ru-irina-apollo`                        | `ru-RU` ロケールと `ru-RU-Irina-Apollo` 音声のコンテナー イメージ。    |
| `ru-ru-pavel-apollo`                        | `ru-RU` ロケールと `ru-RU-Pavel-Apollo` 音声のコンテナー イメージ。    |
| `sk-sk-filip`                               | `sk-SK` ロケールと `sk-SK-Filip` 音声のコンテナー イメージ。           |
| `sl-si-lado`                                | `sl-SI` ロケールと `sl-SI-Lado` 音声のコンテナー イメージ。            |
| `sv-se-hedvigrus`                           | `sv-SE` ロケールと `sv-SE-HedvigRUS` 音声のコンテナー イメージ。       |
| `ta-in-valluvar`                            | `ta-IN` ロケールと `ta-IN-Valluvar` 音声のコンテナー イメージ。        |
| `te-in-chitra`                              | `te-IN` ロケールと `te-IN-Chitra` 音声のコンテナー イメージ。          |
| `th-th-pattara`                             | `th-TH` ロケールと `th-TH-Pattara` 音声のコンテナー イメージ。         |
| `tr-tr-sedarus`                             | `tr-TR` ロケールと `tr-TR-SedaRUS` 音声のコンテナー イメージ。         |
| `vi-vn-an`                                  | `vi-VN` ロケールと `vi-VN-An` 音声のコンテナー イメージ。              |
| `zh-cn-huihuirus`                           | `zh-CN` ロケールと `zh-CN-HuihuiRUS` 音声のコンテナー イメージ。       |
| `zh-cn-kangkang-apollo`                     | `zh-CN` ロケールと `zh-CN-Kangkang-Apollo` 音声のコンテナー イメージ。 |
| `zh-cn-yaoyao-apollo`                       | `zh-CN` ロケールと `zh-CN-Yaoyao-Apollo` 音声のコンテナー イメージ。   |
| `zh-hk-danny-apollo`                        | `zh-HK` ロケールと `zh-HK-Danny-Apollo` 音声のコンテナー イメージ。    |
| `zh-hk-tracy-apollo`                        | `zh-HK` ロケールと `zh-HK-Tracy-Apollo` 音声のコンテナー イメージ。    |
| `zh-hk-tracyrus`                            | `zh-HK` ロケールと `zh-HK-TracyRUS` 音声のコンテナー イメージ。        |
| `zh-tw-hanhanrus`                           | `zh-TW` ロケールと `zh-TW-HanHanRUS` 音声のコンテナー イメージ。       |
| `zh-tw-yating-apollo`                       | `zh-TW` ロケールと `zh-TW-Yating-Apollo` 音声のコンテナー イメージ。   |
| `zh-tw-zhiwei-apollo`                       | `zh-TW` ロケールと `zh-TW-Zhiwei-Apollo` 音声のコンテナー イメージ。   |

---

## <a name="neural-text-to-speech"></a>ニューラル テキスト読み上げ

[ニューラル テキスト読み上げ][sp-ntts]コンテナー イメージは、`mcr.microsoft.com` コンテナー レジストリ シンジケートにあります。 `azure-cognitive-services/speechservices/` リポジトリ内にあり、`neural-text-to-speech` という名前が付いています。 完全修飾コンテナー イメージ名は `mcr.microsoft.com/azure-cognitive-services/speechservices/neural-text-to-speech` です。

このコンテナー イメージには次のタグを利用できます。 また、[MCR でタグ](https://mcr.microsoft.com/v2/azure-cognitive-services/speechservices/neural-text-to-speech/tags/list)の完全な一覧を確認することもできます。


# <a name="latest-version"></a>[最新バージョン](#tab/current)

`v1.3.0` のリリース ノート:
* ニューラル テキスト読み上げコンテナーの一般提供を開始しました。 

| イメージ タグ                                  | Notes                                                                      |
|---------------------------------------------|:---------------------------------------------------------------------------|
| `latest`                                    | `en-US` ロケールと `en-US-AriaNeural` 音声のコンテナー イメージ。      |
| `1.3.0-amd64-<locale-and-voice>`    | `<locale>` を、以下に一覧表示されている使用可能なロケールのいずれかに置き換えます。 たとえば、「 `1.3.0-amd64-en-us-arianeural` 」のように指定します。 |


| v1.3.0 のロケールと音声           | Notes                                                                      |
|---------------------------------------------|:---------------------------------------------------------------------------|
| `de-de-katjaneural`                 | `de-DE` ロケールと `de-DE-KatjaNeural` 音声のコンテナー イメージ。     |
| `en-au-natashaneural`               | `en-AU` ロケールと `en-AU-NatashaNeural` 音声のコンテナー イメージ。   |
| `en-ca-claraneural`                 | `en-CA` ロケールと `en-CA-ClaraNeural` 音声のコンテナー イメージ。     |
| `en-gb-libbyneural`                 | `en-GB` ロケールと `en-GB-LibbyNeural` 音声のコンテナー イメージ。     |
| `en-gb-mianeural`                   | `en-GB` ロケールと `en-GB-MiaNeural` 音声のコンテナー イメージ。       |
| `en-us-arianeural`                  | `en-US` ロケールと `en-US-AriaNeural` 音声のコンテナー イメージ。      |
| `en-us-guyneural`                   | `en-US` ロケールと `en-US-GuyNeural` 音声のコンテナー イメージ。       |
| `es-es-elviraneural`                | `es-ES` ロケールと `es-ES-ElviraNeural` 音声のコンテナー イメージ。    |
| `es-mx-dalianeural`                 | `es-MX` ロケールと `es-MX-DaliaNeural` 音声のコンテナー イメージ。     |
| `fr-ca-sylvieneural`                | `fr-CA` ロケールと `fr-CA-SylvieNeural` 音声のコンテナー イメージ。    |
| `fr-fr-deniseneural`                | `fr-FR` ロケールと `fr-FR-DeniseNeural` 音声のコンテナー イメージ。    |
| `it-it-elsaneural`                  | `it-IT` ロケールと `it-IT-ElsaNeural` 音声のコンテナー イメージ。      |
| `ja-jp-nanamineural`                | `ja-JP` ロケールと `ja-JP-NanamiNeural` 音声のコンテナー イメージ。    |
| `ko-kr-sunhineural`                 | `ko-KR` ロケールと `ko-KR-SunHiNeural` 音声のコンテナー イメージ。     |
| `pt-br-franciscaneural`             | `pt-BR` ロケールと `pt-BR-FranciscaNeural` 音声のコンテナー イメージ。 |
| `zh-cn-xiaoxiaoneural`              | `zh-CN` ロケールと `zh-CN-XiaoxiaoNeural` 音声のコンテナー イメージ。  |

# <a name="previous-version"></a>[以前のバージョン](#tab/previous)

| イメージ タグ                                  | Notes                                                                      |
|---------------------------------------------|:---------------------------------------------------------------------------|
| `latest`                                    | `en-US` ロケールと `en-US-AriaNeural` 音声のコンテナー イメージ。      |
| `1.2.0-amd64-<locale-and-voice>-preview`    | `<locale>` を、以下に一覧表示されている使用可能なロケールのいずれかに置き換えます。 たとえば、「 `1.2.0-amd64-en-us-arianeural-preview` 」のように指定します。 |


| v 1.2.0 Preview のロケールと音声           | Notes                                                                      |
|---------------------------------------------|:---------------------------------------------------------------------------|
| `latest`                                    | `en-US` ロケールと `en-US-AriaNeural` 音声のコンテナー イメージ。      |
| `de-de-katjaneural-preview`                 | `de-DE` ロケールと `de-DE-KatjaNeural` 音声のコンテナー イメージ。     |
| `en-au-natashaneural-preview`               | `en-AU` ロケールと `en-AU-NatashaNeural` 音声のコンテナー イメージ。   |
| `en-ca-claraneural-preview`                 | `en-CA` ロケールと `en-CA-ClaraNeural` 音声のコンテナー イメージ。     |
| `en-gb-libbyneural-preview`                 | `en-GB` ロケールと `en-GB-LibbyNeural` 音声のコンテナー イメージ。     |
| `en-gb-mianeural-preview`                   | `en-GB` ロケールと `en-GB-MiaNeural` 音声のコンテナー イメージ。       |
| `en-us-arianeural-preview`                  | `en-US` ロケールと `en-US-AriaNeural` 音声のコンテナー イメージ。      |
| `en-us-guyneural-preview`                   | `en-US` ロケールと `en-US-GuyNeural` 音声のコンテナー イメージ。       |
| `es-es-elviraneural-preview`                | `es-ES` ロケールと `es-ES-ElviraNeural` 音声のコンテナー イメージ。    |
| `es-mx-dalianeural-preview`                 | `es-MX` ロケールと `es-MX-DaliaNeural` 音声のコンテナー イメージ。     |
| `fr-ca-sylvieneural-preview`                | `fr-CA` ロケールと `fr-CA-SylvieNeural` 音声のコンテナー イメージ。    |
| `fr-fr-deniseneural-preview`                | `fr-FR` ロケールと `fr-FR-DeniseNeural` 音声のコンテナー イメージ。    |
| `it-it-elsaneural-preview`                  | `it-IT` ロケールと `it-IT-ElsaNeural` 音声のコンテナー イメージ。      |
| `ja-jp-nanamineural-preview`                | `ja-JP` ロケールと `ja-JP-NanamiNeural` 音声のコンテナー イメージ。    |
| `ko-kr-sunhineural-preview`                 | `ko-KR` ロケールと `ko-KR-SunHiNeural` 音声のコンテナー イメージ。     |
| `pt-br-franciscaneural-preview`             | `pt-BR` ロケールと `pt-BR-FranciscaNeural` 音声のコンテナー イメージ。 |
| `zh-cn-xiaoxiaoneural-preview`              | `zh-CN` ロケールと `zh-CN-XiaoxiaoNeural` 音声のコンテナー イメージ。  |

---

## <a name="speech-language-detection"></a>音声言語検出

[音声言語検出][sp-lid]コンテナー イメージは `mcr.microsoft.com` コンテナー レジストリ シンジケートにあります。 `azure-cognitive-services/speechservices/` リポジトリ内にあり、`language-detection` という名前が付いています。 完全修飾コンテナー イメージ名は `mcr.microsoft.com/azure-cognitive-services/speechservices/language-detection` です。

このコンテナー イメージには次のタグを利用できます。 また、[MCR でタグ](https://mcr.microsoft.com/v2/azure-cognitive-services/speechservices/language-detection/tags/list)の完全な一覧を確認することもできます。

| イメージ タグ                                  | Notes                                                                      |
|---------------------------------------------|:---------------------------------------------------------------------------|
| `latest`                       |      |
| `1.1.0-amd64-preview`                       |      |

## <a name="key-phrase-extraction"></a>キー フレーズ抽出

コンテナー イメージは `mcr.microsoft.com` コンテナー レジストリ シンジケートにあります。 `azure-cognitive-services/textanalytics/` リポジトリ内にあり、`keyphrase` という名前が付いています。 完全修飾コンテナー イメージ名は `mcr.microsoft.com/azure-cognitive-services/textanalytics/keyphrase` です。

このコンテナー イメージには次のタグを利用できます。 また、[MCR でタグ](https://mcr.microsoft.com/v2/azure-cognitive-services/textanalytics/keyphrase/tags/list)の完全な一覧を確認することもできます。

# <a name="latest-version"></a>[最新バージョン](#tab/current)


| イメージ タグ                    | Notes |
|-------------------------------|:------|
| `latest`                      |       |
| `1.1.013570001-amd64` |       |

# <a name="previous-versions"></a>[以前のバージョン](#tab/previous)

| イメージ タグ                    | Notes |
|-------------------------------|:------|
| `1.1.012840001-amd64` |       |
| `1.1.012830001-amd64`    |       |

---

## <a name="text-language-detection"></a>テキスト言語の検出

[言語検出][ta-la]コンテナー イメージは `mcr.microsoft.com` コンテナー レジストリ シンジケートにあります。 `azure-cognitive-services/textanalytics/` リポジトリ内にあり、`language` という名前が付いています。 完全修飾コンテナー イメージ名は `mcr.microsoft.com/azure-cognitive-services/textanalytics/language` です


このコンテナー イメージには次のタグを利用できます。 また、[MCR でタグ](https://mcr.microsoft.com/v2/azure-cognitive-services/textanalytics/language/tags/list)の完全な一覧を確認することもできます。

# <a name="latest-versions"></a>[最新バージョン](#tab/current)

| イメージ タグ                    | Notes |
|-------------------------------|:------|
| `latest`                      |       |
| `1.1.013570001-amd64` | |
   

# <a name="previous-versions"></a>[以前のバージョン](#tab/previous)


| イメージ タグ                    | Notes |
|-------------------------------|:------|
| `latest`                      |       |
| `1.1.012840001-amd64` |   |
| `1.1.012830001-amd64` |   |

---

## <a name="sentiment-analysis"></a>センチメント分析

[感情分析][ta-se]コンテナー イメージは `mcr.microsoft.com` コンテナー レジストリ シンジケートにあります。 `azure-cognitive-services/textanalytics/` リポジトリ内にあり、`sentiment` という名前が付いています。 完全修飾コンテナー イメージ名は `mcr.microsoft.com/azure-cognitive-services/textanalytics/sentiment` です

このコンテナー イメージには次のタグを利用できます。 また、[MCR でタグ](https://mcr.microsoft.com/v2/azure-cognitive-services/textanalytics/sentiment/tags/list)の完全な一覧を確認することもできます。

| イメージ タグ | Notes                                         |
|------------|:----------------------------------------------|
| `latest`   |                                               |
| `3.0-en`   | 感情分析 v3 (英語)               |
| `3.0-es`   | 感情分析 v3 (スペイン語)               |
| `3.0-fr`   | 感情分析 v3 (フランス語)                |
| `3.0-it`   | 感情分析 v3 (イタリア語)               |
| `3.0-de`   | 感情分析 v3 (ドイツ語)                |
| `3.0-zh`   | 感情分析 v3 (簡体字中国語)  |
| `3.0-zht`  | 感情分析 v3 (繁体字中国語) |
| `3.0-ja`   | 感情分析 v3 (日本語)              |
| `3.0-pt`   | 感情分析 v3 (ポルトガル語)            |
| `3.0-nl`   | 感情分析 v3 (オランダ語)                 |
| `2.1`    | 感情分析 v2      |

[ad-containers]: ../anomaly-Detector/anomaly-detector-container-howto.md
[cv-containers]: ../computer-vision/computer-vision-how-to-install-containers.md
[fa-containers]: ../face/face-how-to-install-containers.md
[fr-containers]: ../form-recognizer/form-recognizer-container-howto.md
[lu-containers]: ../luis/luis-container-howto.md
[sp-stt]: ../speech-service/speech-container-howto.md?tabs=stt
[sp-cstt]: ../speech-service/speech-container-howto.md?tabs=cstt
[sp-tts]: ../speech-service/speech-container-howto.md?tabs=tts
[sp-ctts]: ../speech-service/speech-container-howto.md?tabs=ctts
[sp-ntts]: ../speech-service/speech-container-howto.md?tabs=ntts
[sp-lid]: ../speech-service/speech-container-howto.md?tabs=lid
[ta-kp]: ../text-analytics/how-tos/text-analytics-how-to-install-containers.md?tabs=keyphrase
[ta-la]: ../text-analytics/how-tos/text-analytics-how-to-install-containers.md?tabs=language
[ta-se]: ../text-analytics/how-tos/text-analytics-how-to-install-containers.md?tabs=sentiment
