---
title: "Linux VM 할당 오류 문제 해결 | Microsoft Docs"
description: "Azure에서 Linux VM을 만들거나 재시작하거나 크기를 조정하는 경우 할당 오류 해결"
services: virtual-machines-linux, azure-resource-manager
documentationcenter: 
author: JiangChen79
manager: felixwu
editor: 
tags: top-support-issue,azure-resourece-manager,azure-service-management
ms.assetid: 1ef41144-6dd6-4a56-b180-9d8b3d05eae7
ms.service: virtual-machines-linux
ms.workload: na
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2016
ms.author: cjiang
ms.openlocfilehash: c65ede134971c034006781e058c05a82ffb68a19
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-allocation-failures-when-you-create-restart-or-resize-linux-vms-in-azure"></a><span data-ttu-id="5c3aa-103">Azure에서 Linux VM을 만들거나 재시작하거나 크기를 조정하는 경우 할당 오류 해결</span><span class="sxs-lookup"><span data-stu-id="5c3aa-103">Troubleshoot allocation failures when you create, restart, or resize Linux VMs in Azure</span></span>
<span data-ttu-id="5c3aa-104">VM을 만들거나 중지된(할당이 취소된) VM을 재시작하거나 VM의 크기를 조정하는 경우 Microsoft Azure에서 구독에 계산 리소스를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="5c3aa-104">When you create a VM, restart stopped (deallocated) VMs, or resize a VM, Microsoft Azure allocates compute resources to your subscription.</span></span> <span data-ttu-id="5c3aa-105">이러한 작업을 수행하면서 오류를 수신하는 경우도 있습니다. Azure 구독 제한에 도달하기 전에도 그렇습니다.</span><span class="sxs-lookup"><span data-stu-id="5c3aa-105">You may occasionally receive errors when performing these operations -- even before you reach the Azure subscription limits.</span></span> <span data-ttu-id="5c3aa-106">이 문서는 일부 일반적인 할당 오류의 이유를 설명하고 가능한 수정을 제안합니다.</span><span class="sxs-lookup"><span data-stu-id="5c3aa-106">This article explains the causes of some of the common allocation failures and suggests possible remediation.</span></span> <span data-ttu-id="5c3aa-107">서비스 배포를 계획하는 사용자에게 이 정보가 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c3aa-107">The information may also be useful when you plan the deployment of your services.</span></span> <span data-ttu-id="5c3aa-108">[Azure에서 Windows VM을 만들거나 재시작하거나 크기를 조정하는 경우 할당 오류를 해결](../windows/allocation-failure.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c3aa-108">You can also [troubleshoot allocation failures when you create, restart, or resize Windows VMs in Azure](../windows/allocation-failure.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-allocation-failure](../../../includes/virtual-machines-common-allocation-failure.md)]

