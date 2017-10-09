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
# <a name="gpu-linux-vm-sizes"></a><span data-ttu-id="28313-103">GPU Linux VM 크기</span><span class="sxs-lookup"><span data-stu-id="28313-103">GPU Linux VM sizes</span></span>

[!INCLUDE [virtual-machines-common-sizes-gpu](../../../includes/virtual-machines-common-sizes-gpu.md)]


[!INCLUDE [virtual-machines-common-sizes-table-defs](../../../includes/virtual-machines-common-sizes-table-defs.md)]

[!INCLUDE [virtual-machines-n-series-linux-support](../../../includes/virtual-machines-n-series-linux-support.md)]

<span data-ttu-id="28313-104">드라이버 설치 및 확인 단계에 대해서는 [Linux용 N 시리즈 드라이버 설치](n-series-driver-setup.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="28313-104">For driver installation and verification steps, see [N-series driver setup for Linux](n-series-driver-setup.md).</span></span>

[!INCLUDE [virtual-machines-n-series-considerations](../../../includes/virtual-machines-n-series-considerations.md)]

* <span data-ttu-id="28313-105">설치 권장 하지 않는 서버 또는 Ubuntu NC Vm에서 hello nouveau 드라이버를 사용 하는 다른 시스템.</span><span class="sxs-lookup"><span data-stu-id="28313-105">We don't recommend installing X server or other systems that use hello nouveau driver on Ubuntu NC VMs.</span></span> <span data-ttu-id="28313-106">NVIDIA GPU 드라이버를 설치 하기 전에 toodisable hello nouveau 드라이버가 필요.</span><span class="sxs-lookup"><span data-stu-id="28313-106">Before installing NVIDIA GPU drivers, you need toodisable hello nouveau driver.</span></span>  

## <a name="other-sizes"></a><span data-ttu-id="28313-107">기타 크기</span><span class="sxs-lookup"><span data-stu-id="28313-107">Other sizes</span></span>
- [<span data-ttu-id="28313-108">범용</span><span class="sxs-lookup"><span data-stu-id="28313-108">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="28313-109">Compute에 최적화</span><span class="sxs-lookup"><span data-stu-id="28313-109">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="28313-110">메모리에 최적화</span><span class="sxs-lookup"><span data-stu-id="28313-110">Memory optimized</span></span>](sizes-memory.md)
- [<span data-ttu-id="28313-111">Storage에 최적화</span><span class="sxs-lookup"><span data-stu-id="28313-111">Storage optimized</span></span>](sizes-storage.md)
- [<span data-ttu-id="28313-112">고성능 계산</span><span class="sxs-lookup"><span data-stu-id="28313-112">High performance compute</span></span>](sizes-hpc.md)

## <a name="next-steps"></a><span data-ttu-id="28313-113">다음 단계</span><span class="sxs-lookup"><span data-stu-id="28313-113">Next steps</span></span>
<span data-ttu-id="28313-114">[ACU(Azure Compute 단위)](acu.md)가 Azure SKU 간의 Compute 성능을 비교하는 데 어떻게 도움을 줄 수 있는지 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="28313-114">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>