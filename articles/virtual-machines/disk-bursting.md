---
title: マネージド ディスクのバースト
description: Azure ディスクと Azure 仮想マシンのディスク バーストについて説明します。
author: albecker1
ms.author: albecker
ms.date: 09/22/2020
ms.topic: conceptual
ms.service: virtual-machines
ms.subservice: disks
ms.custom: references_regions
ms.openlocfilehash: a8d1a69070628248fb710a614369ff9311252c05
ms.sourcegitcommit: 3bdeb546890a740384a8ef383cf915e84bd7e91e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2020
ms.locfileid: "93102709"
---
# <a name="managed-disk-bursting"></a>マネージド ディスクのバースト
[!INCLUDE [managed-disks-bursting](../../includes/managed-disks-bursting.md)]

## <a name="virtual-machine-level-bursting"></a>仮想マシン レベルでのバースト
サポートされている次のサイズでは、パブリック クラウド内のすべてのリージョンで、VM レベルでのバーストのサポートが有効になっています。 
- [Lsv2 シリーズ](lsv2-series.md)

サポートされている次のサイズについては、米国中西部でも VM レベルのバーストを利用できます。
- [Dsv3 シリーズ](dv3-dsv3-series.md)
- [Esv3 シリーズ](ev3-esv3-series.md)

バーストをサポートしている仮想マシンでは、バーストが既定で有効になっています。

## <a name="disk-level-bursting"></a>ディスク レベルでのバースト
バーストは、Azure パブリック クラウド、Azure Government クラウド、Azure China クラウドのすべてのリージョンで、ディスク サイズ P20 以下の[プレミアム SSD](disks-types.md#premium-ssd) でも利用できます。 ディスク バースティングは、サポートされているディスク サイズのすべての新しいデプロイと既存のデプロイでは既定で有効になっています。 

[!INCLUDE [managed-disks-bursting](../../includes/managed-disks-bursting-2.md)]