---
title: "Azure에서 Linux VM의 가용성 관리 | Microsoft Docs"
description: "Azure에서 여러 가상 컴퓨터를 사용하여 Linux 응용 프로그램의 고가용성을 유지하는 방법에 대해 알아봅니다."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: 891c852a-84c0-4940-a61e-ada6e185bf37
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/21/2017
ms.author: cynthn
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f153a740e4814e2573e53b9c051d24c30ff9088f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-the-availability-of-linux-virtual-machines"></a><span data-ttu-id="904a7-103">Linux 가상 컴퓨터의 가용성 관리</span><span class="sxs-lookup"><span data-stu-id="904a7-103">Manage the availability of Linux virtual machines</span></span>

<span data-ttu-id="904a7-104">Azure에서 여러 가상 컴퓨터를 설정하고 관리하여 Linux 응용 프로그램의 고가용성을 유지하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="904a7-104">Learn ways to set up and manage multiple virtual machines to ensure high availability for your Linux application in Azure.</span></span> <span data-ttu-id="904a7-105">[Windows 가상 컴퓨터의 가용성을 관리](../windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="904a7-105">You can also [manage the availability of Windows virtual machines](../windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="904a7-106">Resource Manager 배포 모델에서 CLI를 사용하여 가용성 집합을 만들기 위한 지침은 [azure availset: 가용성 집합을 관리하는 명령](../azure-cli-arm-commands.md#azure-availset-commands-to-manage-your-availability-sets)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="904a7-106">For instructions on creating an availability set using CLI in the Resource Manager deployment model, see [azure availset: commands to manage your availability sets](../azure-cli-arm-commands.md#azure-availset-commands-to-manage-your-availability-sets).</span></span>

[!INCLUDE [virtual-machines-common-manage-availability](../../../includes/virtual-machines-common-manage-availability.md)]

## <a name="next-steps"></a><span data-ttu-id="904a7-107">다음 단계</span><span class="sxs-lookup"><span data-stu-id="904a7-107">Next steps</span></span>
<span data-ttu-id="904a7-108">가상 컴퓨터 부하 분산에 대한 자세한 내용은 [가상 컴퓨터 부하 분산](../virtual-machines-linux-load-balance.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="904a7-108">To learn more about load balancing your virtual machines, see [Load Balancing virtual machines](../virtual-machines-linux-load-balance.md).</span></span>

