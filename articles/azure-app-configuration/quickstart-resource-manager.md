---
title: Azure Resource Manager テンプレート (ARM テンプレート) を使用して Azure App Configuration ストアを作成する
titleSuffix: Azure App Configuration
description: Azure Resource Manager テンプレート (ARM テンプレート) を使用して Azure App Configuration ストアを作成する方法について説明します。
author: ZhijunZhao
ms.author: zhijzhao
ms.date: 10/16/2020
ms.service: azure-resource-manager
ms.topic: quickstart
ms.custom: subject-armqs
ms.openlocfilehash: 56505c95e65911cafbaaa403cd09332695439d97
ms.sourcegitcommit: e7179fa4708c3af01f9246b5c99ab87a6f0df11c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/30/2020
ms.locfileid: "97825662"
---
# <a name="quickstart-create-an-azure-app-configuration-store-by-using-an-arm-template"></a>クイックスタート: ARM テンプレートを使用して Azure App Configuration ストアを作成する

このクイックスタートでは、以下の方法について説明します。

- Azure Resource Manager テンプレート (ARM テンプレート) を使用して App Configuration ストアをデプロイする。
- ARM テンプレートを使用して App Configuration ストアにキー値を作成する。
- ARM テンプレートから App Configuration ストア内のキー値を読み取る。

[!INCLUDE [About Azure Resource Manager](../../includes/resource-manager-quickstart-introduction.md)]

環境が前提条件を満たしていて、ARM テンプレートの使用に慣れている場合は、 **[Azure へのデプロイ]** ボタンを選択します。 Azure portal でテンプレートが開きます。

[![Azure へのデプロイ](../media/template-deployments/deploy-to-azure.svg)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-app-configuration-store-kv%2Fazuredeploy.json)

## <a name="prerequisites"></a>前提条件

Azure サブスクリプションをお持ちでない場合は、開始する前に [無料アカウント](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) を作成してください。

## <a name="review-the-template"></a>テンプレートを確認する

このクイックスタートで使用されるテンプレートは [Azure クイックスタート テンプレート](https://azure.microsoft.com/resources/templates/101-app-configuration-store-kv/)からのものです。 2 つのキー値を含む新しい App Configuration ストアを作成します。 その後、`reference` 関数を使用して、2 つのキー値リソースの値を出力します。 このようにしてキーの値を読み取ることで、それをテンプレート内の他の場所で使用することができます。

このクイックスタートでは、`copy` 要素を使用して、キー値リソースのインスタンスを複数作成します。 `copy` 要素の詳細については、「[ARM テンプレートでのリソースの反復処理](../azure-resource-manager/templates/copy-resources.md)」を参照してください。

> [!IMPORTANT]
> このテンプレートには、App Configuration リソース プロバイダー バージョン `2020-07-01-preview` 以降が必要です。 このバージョンでは、キー値の読み取りに `reference` 関数が使用されます。 以前のバージョンでキー値の読み取りに使用されていた `listKeyValue` 関数は、バージョン `2020-07-01-preview` 以降では使用できません。

:::code language="json" source="~/quickstart-templates/101-app-configuration-store-kv/azuredeploy.json":::

テンプレートでは、次の 2 つの Azure リソースが定義されています。

- [Microsoft.AppConfiguration/configurationStores](/azure/templates/microsoft.appconfiguration/2020-07-01-preview/configurationstores): App Configuration ストアを作成します。
- [Microsoft.AppConfiguration/configurationStores/keyValues](/azure/templates/microsoft.appconfiguration/2020-07-01-preview/configurationstores/keyvalues): App Configuration ストア内にキー値を作成します。

> [!TIP]
> `keyValues` リソースの名前は、キーとラベルの組み合わせです。 キーとラベルが、`$` という区切り記号で結合されます。 ラベルは省略可能です。 上の例では、`myKey` という名前の `keyValues` リソースによって、ラベルなしのキー値が作成されます。
>
> ARM テンプレートのリソース名に許可されていない文字については、パーセント エンコード (URL エンコード) を使用することでキーまたはラベルに含めることができます。 `%` は、許可された文字ではないため、`~` で代用されます。 名前を正しくエンコードするには、次の手順に従います。
>
> 1. URL エンコードを適用します。
> 2. `~` を `~7E` に置き換えます。
> 3. `%` を `~` に置き換えます。
>
> たとえば、キー名が `AppName:DbEndpoint` で、ラベル名が `Test` であるキーと値のペアを作成するには、リソース名を `AppName~3ADbEndpoint$Test` とする必要があります。

> [!NOTE]
> App Configuration を使用すると、仮想ネットワークから[プライベート リンク](concept-private-endpoint.md)経由でキー値データにアクセスできます。 この機能が有効になっている場合、既定では、パブリック ネットワーク上の App Configuration データに対するすべての要求が拒否されます。 ARM テンプレートは仮想ネットワークの外部で実行されるため、ARM テンプレートからのデータ アクセスは許可されません。 プライベート リンクの使用中に ARM テンプレートからのデータ アクセスを許可するには、次の Azure CLI コマンドを使用して、パブリック ネットワーク アクセスを有効にすることができます。 このシナリオでは、パブリック ネットワーク アクセスを有効にすることによるセキュリティへの影響を考慮する必要があります。
>
> ```azurecli-interactive
> az appconfig update -g MyResourceGroup -n MyAppConfiguration --enable-public-network true
> ```

## <a name="deploy-the-template"></a>テンプレートのデプロイ

Azure にサインインし、テンプレートを開くには次のイメージを選択します。 このテンプレートでは、2 つのキー値を含む App Configuration ストアが作成されます。

[![Azure へのデプロイ](../media/template-deployments/deploy-to-azure.svg)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-app-configuration-store-kv%2Fazuredeploy.json)

次の PowerShell コマンドレットを使用してテンプレートをデプロイすることもできます。 キー値は、PowerShell コンソールの出力に表示されます。

```azurepowershell-interactive
$projectName = Read-Host -Prompt "Enter a project name that is used for generating resource names"
$location = Read-Host -Prompt "Enter the location (i.e. centralus)"
$templateUri = "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-app-configuration-store-kv/azuredeploy.json"

$resourceGroupName = "${projectName}rg"

New-AzResourceGroup -Name $resourceGroupName -Location "$location"
New-AzResourceGroupDeployment -ResourceGroupName $resourceGroupName -TemplateUri $templateUri

Read-Host -Prompt "Press [ENTER] to continue ..."
```

## <a name="review-deployed-resources"></a>デプロイされているリソースを確認する

1. [Azure portal](https://portal.azure.com) にサインインします。
1. Azure portal の検索ボックスに「**App Configuration**」と入力します。 一覧から **[App Configuration]** を選択します。
1. 新しく作成した App Configuration リソースを選択します。
1. **[Operations]\(操作\)** の **[構成エクスプローラー]** をクリックします。
1. 2 つのキー値が存在することを確認します。

## <a name="clean-up-resources"></a>リソースをクリーンアップする

必要がなくなったら、リソース グループ、App Configuration ストア、および関連するすべてのリソースを削除します。 App Configuration ストアを今後使用する予定がある場合は、削除をスキップできます。 このストアを今後使用しない場合には、次のコマンドレットを実行して、このクイックスタートで作成したすべてのリソースを削除してください。

```azurepowershell-interactive
$resourceGroupName = Read-Host -Prompt "Enter the Resource Group name"
Remove-AzResourceGroup -Name $resourceGroupName
Write-Host "Press [ENTER] to continue..."
```

## <a name="next-steps"></a>次のステップ

Azure App Configuration を使用して他のアプリケーションを作成する方法については、次の記事に進んでください。

> [!div class="nextstepaction"]
> [クイック スタート: Azure App Configuration を使用して ASP.NET Core アプリを作成する](quickstart-aspnet-core-app.md)
