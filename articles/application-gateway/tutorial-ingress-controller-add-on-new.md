---
title: チュートリアル:新しい Azure Application Gateway インスタンスを使用して新しい AKS クラスターのイングレス コントローラー アドオンを有効にする
description: このチュートリアルでは、Azure CLI を使用して、新しい Application Gateway インスタンスで新しい AKS クラスターのイングレス コントローラー アドオンを有効にする方法を学習します。
services: application-gateway
author: caya
ms.service: application-gateway
ms.topic: tutorial
ms.date: 09/24/2020
ms.author: caya
ms.openlocfilehash: 627d5b15a861c3d564cb4db33b366d3227092d37
ms.sourcegitcommit: 192f9233ba42e3cdda2794f4307e6620adba3ff2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2020
ms.locfileid: "96296252"
---
# <a name="tutorial-enable-the-ingress-controller-add-on-preview-for-a-new-aks-cluster-with-a-new-application-gateway-instance"></a>チュートリアル:新しい Application Gateway インスタンスを使用して新しい AKS クラスターのイングレス コントローラー アドオン (プレビュー) を有効にする

Azure CLI を使用して、[Azure Kubernetes Services (AKS)](https://azure.microsoft.com/services/kubernetes-service/) クラスターの [Application Gateway イングレス コントローラー (AGIC)](ingress-controller-overview.md) アドオンを有効にすることができます。 このアドオンは現在、プレビュー段階です。

このチュートリアルでは、AGIC アドオンが有効になっている AKS クラスターを作成します。 クラスターを作成すると、使用する Azure Application Gateway インスタンスが自動的に作成されます。 その後、アドオンを使用して、Application Gateway を介してアプリケーションを公開するサンプル アプリケーションをデプロイします。 

このアドオンでは、[Helm を使用する以前の方法](ingress-controller-overview.md#difference-between-helm-deployment-and-aks-add-on)よりもはるかに高速な方法で AKS クラスターに AGIC をデプロイできます。 また、フル マネージド エクスペリエンスが提供されます。    

このチュートリアルでは、以下の内容を学習します。

> [!div class="checklist"]
> * リソース グループを作成する。 
> * AGIC アドオンが有効になっている新しい AKS クラスターを作成する。 
> * AKS クラスターで AGIC をイングレスに使用してサンプル アプリケーションをデプロイする。
> * アプリケーションが Application Gateway を介して到達可能であることを確認する。

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [azure-cli-prepare-your-environment.md](../../includes/azure-cli-prepare-your-environment.md)]

 - このチュートリアルには、Azure CLI のバージョン 2.0.4 以降が必要です。 Azure Cloud Shell を使用している場合は、最新バージョンが既にインストールされています。 Azure CLI を使用する場合は、次のコマンドを使用して、CLI にプレビュー拡張機能をインストールする必要があります (まだインストールしていない場合)。
    ```azurecli-interactive
    az extension add --name aks-preview
    ```

 - 次の例に示すように、[az feature register](/cli/azure/feature#az-feature-register) コマンドを使用して、*AKS-IngressApplicationGatewayAddon* 機能フラグを登録します。 アドオンはまだプレビュー段階ですが、サブスクリプションごとに 1 回だけ、これを行う必要があります。
    ```azurecli-interactive
    az feature register --name AKS-IngressApplicationGatewayAddon --namespace Microsoft.ContainerService
    ```

   状態が `Registered` と表示されるまでに数分かかる場合があります。 [az feature list](/cli/azure/feature#az-feature-register) コマンドを使用して登録状態を確認できます。
    ```azurecli-interactive
    az feature list -o table --query "[?contains(name, 'Microsoft.ContainerService/AKS-IngressApplicationGatewayAddon')].{Name:name,State:properties.state}"
    ```

 - 準備ができたら、[az provider register](/cli/azure/provider#az-provider-register) コマンドを使用して、Microsoft.ContainerService リソース プロバイダーの登録を更新します。
    ```azurecli-interactive
    az provider register --namespace Microsoft.ContainerService
    ```

## <a name="create-a-resource-group"></a>リソース グループを作成する

Azure で、関連するリソースをリソース グループに割り当てます。 [az group create](/cli/azure/group#az-group-create) を使用してリソース グループを作成します。 次の例では、*myResourceGroup* という名前のリソース グループを *canadacentral* の場所 (リージョン) に作成します。 

```azurecli-interactive
az group create --name myResourceGroup --location canadacentral
```

## <a name="deploy-an-aks-cluster-with-the-add-on-enabled"></a>アドオンが有効になっている AKS クラスターをデプロイする

ここで、AGIC アドオンが有効になっている新しい AKS クラスターをデプロイします。 このプロセスで使用する既存の Application Gateway インスタンスが指定されていない場合は、AKS クラスターへのトラフィックを処理する新しい Application Gateway インスタンスを自動的に作成して設定します。  

> [!NOTE]
> Application Gateway イングレス コントローラー アドオンでは、Application Gateway v2 SKU (Standard および WAF) "*のみ*" がサポートされ、Application Gateway v1 SKU はサポート "*されません*"。 AGIC アドオンを使用して新しい Application Gateway インスタンスをデプロイする場合は、Application Gateway Standard_v2 SKU のみをデプロイできます。 Application Gateway WAF_v2 SKU でアドオンを有効にする場合は、これらの方法のいずれかを使用します。
>
> - ポータルを使用して Application Gateway で WAF を有効にします。 
> - まず、WAF_v2 Application Gateway インスタンスを作成してから、[既存の AKS クラスターと既存の Application Gateway インスタンスを使用して AGIC アドオンを有効にする](tutorial-ingress-controller-add-on-existing.md)方法に関する指示に従います。 

次の例では、[Azure CNI](../aks/concepts-network.md#azure-cni-advanced-networking) と [マネージド ID](../aks/use-managed-identity.md) を使用して、*myCluster* という名前の新しい AKS クラスターをデプロイします。 作成したリソース グループ (*myResourceGroup*) で AGIC アドオンが有効になります。 

既存の Application Gateway インスタンスを指定せずに AGIC アドオンを有効にした新しい AKS クラスターをデプロイすると、Standard_v2 SKU Application Gateway インスタンスが自動的に作成されます。 そのため、Application Gateway インスタンスの名前とサブネットのアドレス空間も指定します。 Application Gateway インスタンスの名前は *myApplicationGateway* となり、使用するサブネットのアドレス空間は 10.2.0.0/16 です。 このチュートリアルの最初に、aks-preview 拡張機能を追加または更新したことを確認します。 

```azurecli-interactive
az aks create -n myCluster -g myResourceGroup --network-plugin azure --enable-managed-identity -a ingress-appgw --appgw-name myApplicationGateway --appgw-subnet-prefix "10.2.0.0/16" --generate-ssh-keys
```

`az aks create` コマンドの追加パラメーターを構成する場合は、[これらのリファレンス](/cli/azure/aks?view=azure-cli-latest#az-aks-create)を参照してください。 

> [!NOTE]
> 作成した AKS クラスターは、作成したリソース グループ (*myResourceGroup*) に表示されます。 しかし、自動的に作成された Application Gateway インスタンスは、エージェント プールがある、ノード リソース グループに配置されます。 ノード リソース グループの名前は、既定では *MC_resource-group-name_cluster-name_location* になりますが、変更することはできます。 

## <a name="deploy-a-sample-application-by-using-agic"></a>AGIC を使用してサンプル アプリケーションをデプロイする

ここで、作成した AKS クラスターにサンプル アプリケーションをデプロイします。 アプリケーションによって、イングレスに AGIC アドオンが使用され、Application Gateway インスタンスが AKS クラスターに接続されます。 

まず、`az aks get-credentials` コマンドを実行して、AKS クラスターの資格情報を取得します。 

```azurecli-interactive
az aks get-credentials -n myCluster -g myResourceGroup
```

これで資格情報を取得したので、次のコマンドを実行して、クラスターへのイングレスに AGIC を使用するサンプル アプリケーションを設定します。 AGIC によって、前に設定した Application Gateway インスタンスが、対応するルーティング規則で、デプロイした新しいサンプル アプリケーションに更新されます。  

```azurecli-interactive
kubectl apply -f https://raw.githubusercontent.com/Azure/application-gateway-kubernetes-ingress/master/docs/examples/aspnetapp.yaml 
```

## <a name="check-that-the-application-is-reachable"></a>アプリケーションに到達可能であることを確認する

これで、Application Gateway インスタンスが AKS クラスターへのトラフィックを処理するように設定されたので、アプリケーションに到達可能であることを確認してみましょう。 最初に、イングレスの IP アドレスを取得します。 

```azurecli-interactive
kubectl get ingress
```

作成したサンプル アプリケーションが、次のいずれかの方法で実行されていることを確認します。

- 上記のコマンドを実行して取得した、Application Gateway インスタンスの IP アドレスにアクセスする。
- `curl` を使用する。 

Application Gateway で更新プログラムを取得するのに 1 分ほどかかることがあります。 ポータルの Application Gateway の状態が **[更新中]** のままになっている場合は、IP アドレスへの到達を試みる前に完了するようにしてください。 

## <a name="clean-up-resources"></a>リソースをクリーンアップする

必要がなくなったら、リソース グループ、Application Gateway インスタンス、およびすべての関連リソースを削除します。

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [AGIC アドオンの無効化の詳細を確認する](./ingress-controller-disable-addon.md)
