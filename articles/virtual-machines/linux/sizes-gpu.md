---
title: "Linux VM aaaAzure 크기-GPU | Microsoft Docs"
description: "Hello 서로 다른 액세스에 최적화 된 GPU에 사용 가능한 크기 Azure에서 Linux 가상 컴퓨터를 나열합니다."
services: virtual-machines-linux
documentationcenter: 
author: jonbeck7
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 07/28/2017
ms.author: jonbeck
ms.openlocfilehash: e98f720499be37df4048aeb513aa4f6b187b7335
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="gpu-linux-vm-sizes"></a>GPU Linux VM 크기

[!INCLUDE [virtual-machines-common-sizes-gpu](../../../includes/virtual-machines-common-sizes-gpu.md)]


[!INCLUDE [virtual-machines-common-sizes-table-defs](../../../includes/virtual-machines-common-sizes-table-defs.md)]

[!INCLUDE [virtual-machines-n-series-linux-support](../../../includes/virtual-machines-n-series-linux-support.md)]

드라이버 설치 및 확인 단계에 대해서는 [Linux용 N 시리즈 드라이버 설치](n-series-driver-setup.md)를 참조하세요.

[!INCLUDE [virtual-machines-n-series-considerations](../../../includes/virtual-machines-n-series-considerations.md)]

* 설치 권장 하지 않는 서버 또는 Ubuntu NC Vm에서 hello nouveau 드라이버를 사용 하는 다른 시스템. NVIDIA GPU 드라이버를 설치 하기 전에 toodisable hello nouveau 드라이버가 필요.  

## <a name="other-sizes"></a>기타 크기
- [범용](sizes-general.md)
- [Compute에 최적화](sizes-compute.md)
- [메모리에 최적화](sizes-memory.md)
- [Storage에 최적화](sizes-storage.md)
- [고성능 계산](sizes-hpc.md)

## <a name="next-steps"></a>다음 단계
[ACU(Azure Compute 단위)](acu.md)가 Azure SKU 간의 Compute 성능을 비교하는 데 어떻게 도움을 줄 수 있는지 알아봅니다.