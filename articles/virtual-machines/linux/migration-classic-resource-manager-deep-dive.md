---
title: "클래식에서 Azure Resource Manager로의 플랫폼 지원 마이그레이션에 대한 기술 정보 | Microsoft Docs"
description: "이 문서에서는 플랫폼 지원 방식으로 클래식에서 Azure Resource Manager로 리소스를 마이그레이션하는 과정의 기술적 측면을 설명합니다."
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 29267453-f894-4180-bb67-dce2a0e062bb
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: kasing
ms.openlocfilehash: 557a61f266c494cb6b8003cff945fa1a14348898
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="technical-deep-dive-on-platform-supported-migration-from-classic-to-azure-resource-manager"></a><span data-ttu-id="4e0a8-103">클래식에서 Azure Resource Manager로의 플랫폼 지원 마이그레이션에 대한 기술 정보</span><span class="sxs-lookup"><span data-stu-id="4e0a8-103">Technical deep dive on platform-supported migration from classic to Azure Resource Manager</span></span>

<span data-ttu-id="4e0a8-104">Azure 클래식 배포 모델에서 Azure Resource Manager 배포 모델로 마이그레이션하는 방법을 자세하게 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="4e0a8-104">Let's take a deep-dive on migrating from the Azure classic deployment model to the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="4e0a8-105">Azure 플랫폼에서 두 가지 배포 모델 간에 리소스를 마이그레이션하는 방법을 더욱 잘 이해할 수 있도록 리소스 및 기능 수준에서 리소스를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="4e0a8-105">We look at resources at a resource and feature level to help you understand how the Azure platform migrates resources between the two deployment models.</span></span> <span data-ttu-id="4e0a8-106">자세한 내용은 서비스 발표 문서 [클래식에서 Azure Resource Manager로 IaaS 리소스의 플랫폼 지원 마이그레이션](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)을 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="4e0a8-106">For more information, please read the service announcement article: [Platform-supported migration of IaaS resources from classic to Azure Resource Manager](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-migration-deep-dive](../../../includes/virtual-machines-common-classic-resource-manager-migration-deep-dive.md)]

## <a name="next-steps"></a><span data-ttu-id="4e0a8-107">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4e0a8-107">Next steps</span></span>

* [<span data-ttu-id="4e0a8-108">클래식에서 Azure Resource Manager로 IaaS 리소스의 플랫폼 지원 마이그레이션 개요</span><span class="sxs-lookup"><span data-stu-id="4e0a8-108">Overview of platform-supported migration of IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="4e0a8-109">클래식에서 Azure Resource Manager로 IaaS 리소스의 마이그레이션 계획</span><span class="sxs-lookup"><span data-stu-id="4e0a8-109">Planning for migration of IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="4e0a8-110">PowerShell을 사용하여 클래식에서 Azure Resource Manager로 IaaS 리소스 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="4e0a8-110">Use PowerShell to migrate IaaS resources from classic to Azure Resource Manager</span></span>](../windows/migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="4e0a8-111">CLI를 사용하여 클래식에서 Azure Resource Manager로 IaaS 리소스 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="4e0a8-111">Use CLI to migrate IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="4e0a8-112">클래식에서 Azure Resource Manager로의 IaaS 리소스 마이그레이션을 지원하기 위한 커뮤니티 도구</span><span class="sxs-lookup"><span data-stu-id="4e0a8-112">Community tools for assisting with migration of IaaS resources from classic to Azure Resource Manager</span></span>](../windows/migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="4e0a8-113">가장 일반적인 마이그레이션 오류 검토</span><span class="sxs-lookup"><span data-stu-id="4e0a8-113">Review most common migration errors</span></span>](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="4e0a8-114">클래식에서 Azure Resource Manager로의 IaaS 리소스 마이그레이션과 관련된 가장 자주 묻는 질문 검토</span><span class="sxs-lookup"><span data-stu-id="4e0a8-114">Review the most frequently asked questions about migrating IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
