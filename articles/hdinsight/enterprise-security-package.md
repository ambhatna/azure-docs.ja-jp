---
title: Azure HDInsight 用の Enterprise セキュリティ パッケージ
description: Azure HDInsight 内の Enterprise セキュリティ パッケージのコンポーネントとバージョンについて説明します。
author: hrasheed-msft
ms.author: hrasheed
ms.reviewer: jasonh
ms.service: hdinsight
ms.topic: conceptual
ms.date: 05/08/2020
ms.openlocfilehash: d77d9877fbc49fbb147965b30e299b75b60ccce3
ms.sourcegitcommit: d767156543e16e816fc8a0c3777f033d649ffd3c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/26/2020
ms.locfileid: "92546655"
---
# <a name="enterprise-security-package-for-azure-hdinsight"></a>Azure HDInsight 用の Enterprise セキュリティ パッケージ

Enterprise セキュリティは、クラスターの作成のワークフローの一部として HDInsight クラスターに追加できるオプションのパッケージです。 Enterprise セキュリティ パッケージでは以下の機能がサポートされます。

* 認証のための Active Directory との統合。

    以前は、ローカル管理者ユーザーとローカル SSH ユーザーと共に HDInsight クラスターを作成しました。 ローカル管理者ユーザーは、すべてのファイル、フォルダー、テーブル、列にアクセスできます。  Enterprise セキュリティ パッケージを使用すると、HDInsight を Azure Active Directory Domain Services と統合することで、Azure ロールベースのアクセス制御を有効にすることができます。

    詳細については、次を参照してください。

    * [ドメイン参加済み HDInsight クラスターでの Apache Hadoop セキュリティの概要](./domain-joined/hdinsight-security-overview.md)

    * [HDInsight で Azure のドメイン参加済み Apache Hadoop クラスターを計画する](./domain-joined/apache-domain-joined-architecture.md)

    * [ドメイン参加済みサンドボックス環境の構成](./domain-joined/apache-domain-joined-configure-using-azure-adds.md)

    * [Azure Active Directory Domain Services を使用してドメイン参加済み HDInsight クラスターを構成する](./domain-joined/apache-domain-joined-configure-using-azure-adds.md)

* データの承認

  * Hive、Spark SQL、Yarn Queues の承認のための Apache Ranger との統合。
  * ファイルとフォルダーのアクセスの制御を設定できます。

    詳細については、[ドメイン参加済み HDInsight で Apache Hive ポリシーを構成する](./domain-joined/apache-domain-joined-run-hive.md)方法に関するページを参照してください。

* アクセスや構成済みポリシーを監視するための監査ログの表示。

## <a name="supported-cluster-types"></a>サポートされているクラスターの種類

現時点では、次のクラスターの種類のみが Enterprise セキュリティ パッケージをサポートしています。

* Hadoop (HDInsight 3.6 のみ)
* Spark
* Kafka
* hbase
* Interactive Query

## <a name="support-for-azure-data-lake-storage"></a>Azure Data Lake Storage のサポート

Enterprise セキュリティ パッケージでは、プライマリ ストレージとアドオン ストレージの両方として Azure Data Lake Storage の使用がサポートされます。

## <a name="pricing-and-service-level-agreement-sla"></a>価格とサービス レベル アグリーメント (SLA)

Enterprise セキュリティ パッケージの価格と SLA について詳しくは、[HDInsight の価格](https://azure.microsoft.com/pricing/details/hdinsight/)に関するページをご覧ください。

## <a name="next-steps"></a>次のステップ

* [HDInsight で Apache Hadoop、Spark、その他のクラスターをセットアップする](hdinsight-hadoop-provision-linux-clusters.md)
* [Windows PC から HDInsight の Apache Hadoop で作業する](hdinsight-hadoop-windows-tools.md)
* [Azure HDInsight バージョンに対応する Hortonworks リリース ノート](./hortonworks-release-notes.md)
* [HDInsight の Apache コンポーネント](./hdinsight-component-versioning.md)