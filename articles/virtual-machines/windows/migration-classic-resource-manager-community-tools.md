---
title: "커뮤니티 도구 - 클래식 리소스를 Azure Resource Manager로 이동 | Microsoft 문서"
description: "이 문서에는 IaaS 리소스를 클래식에서 Azure Resource Manager 배포 모델로 마이그레이션하도록 지원하기 위해 커뮤니티에서 제공해온 도구가 설명되어 있습니다."
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 228b697b-3950-49f5-84bb-283bb56621b1
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: kasing
ms.openlocfilehash: d3fc0246088eddeb345bea0ffbd2c5247b218006
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="community-tools-to-migrate-iaas-resources-from-classic-to-azure-resource-manager"></a><span data-ttu-id="e3749-103">클래식에서 Azure Resource Manager로 IaaS 리소스를 마이그레이션하기 위한 커뮤니티 도구</span><span class="sxs-lookup"><span data-stu-id="e3749-103">Community tools to migrate IaaS resources from classic to Azure Resource Manager</span></span>
<span data-ttu-id="e3749-104">이 문서에는 IaaS 리소스를 클래식에서 Azure Resource Manager 배포 모델로 마이그레이션하도록 지원하기 위해 커뮤니티에서 제공해온 도구가 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3749-104">This article catalogs the tools that have been provided by the community to assist with migration of IaaS resources from classic to the Azure Resource Manager deployment model.</span></span>

> [!NOTE]
> <span data-ttu-id="e3749-105">이러한 도구는 Microsoft 지원을 통해 공식적으로 지원되지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e3749-105">These tools are not officially supported by Microsoft Support.</span></span> <span data-ttu-id="e3749-106">따라서 GitHub에 오픈 소스로 제공되며 수정 사항 또는 추가 시나리오에 대한 PR을 환영합니다.</span><span class="sxs-lookup"><span data-stu-id="e3749-106">Therefore they are open sourced on GitHub and we're happy to accept PRs for fixes or additional scenarios.</span></span> <span data-ttu-id="e3749-107">문제를 보고하려면 GitHub의 문제 기능을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e3749-107">To report an issue, use the GitHub issues feature.</span></span>
> 
> <span data-ttu-id="e3749-108">이러한 도구를 사용하여 마이그레이션을 수행하면 클래식 Virtual Machine의 가동이 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3749-108">Migrating with these tools will cause downtime for your classic Virtual Machine.</span></span> <span data-ttu-id="e3749-109">플랫폼에서 지원하는 마이그레이션 방법은 다음 페이지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e3749-109">If you're looking for platform supported migration, visit</span></span> 
> 
>   * [<span data-ttu-id="e3749-110">클래식에서 Azure Resource Manager 스택으로 IaaS 리소스의 플랫폼 지원 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="e3749-110">Platform supported migration of IaaS resources from Classic to Azure Resource Manager stack</span></span>](migration-classic-resource-manager-overview.md)
>   * [<span data-ttu-id="e3749-111">클래식에서 Azure Resource Manager로의 플랫폼 지원 마이그레이션에 대한 기술 정보</span><span class="sxs-lookup"><span data-stu-id="e3749-111">Technical Deep Dive on Platform supported migration from Classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-deep-dive.md)
>   * [<span data-ttu-id="e3749-112">Azure PowerShell을 사용하여 클래식에서 Azure Resource Manager로 IaaS 리소스 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="e3749-112">Migrate IaaS resources from Classic to Azure Resource Manager using Azure PowerShell</span></span>](migration-classic-resource-manager-ps.md)
> 
> 

## <a name="asmmetadataparser"></a><span data-ttu-id="e3749-113">AsmMetadataParser</span><span class="sxs-lookup"><span data-stu-id="e3749-113">AsmMetadataParser</span></span>
<span data-ttu-id="e3749-114">Azure 서비스 관리에서 Azure Resource Manager로의 엔터프라이즈 마이그레이션 과정에서 생성되는 도우미 도구의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="e3749-114">This is a collection of helper tools created as part of enterprise migrations from Azure Service Management to Azure Resource Manager.</span></span> <span data-ttu-id="e3749-115">이 도구를 사용하면 인프라를 마이그레이션 테스트에 사용할 수 있는 다른 구독으로 복제하고, 프로덕션 구독에서 마이그레이션을 실행하기 전에 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3749-115">This tool allows you to replicate your infrastructure into another subscription which can be used for testing migration and iron out any issues before running the migration on your Production subscription.</span></span>

[<span data-ttu-id="e3749-116">도구 설명서 링크</span><span class="sxs-lookup"><span data-stu-id="e3749-116">Link to the tool documentation</span></span>](https://github.com/Azure/classic-iaas-resourcemanager-migration/tree/master/AsmToArmMigrationApiToolset)

## <a name="migaz"></a><span data-ttu-id="e3749-117">migAz</span><span class="sxs-lookup"><span data-stu-id="e3749-117">migAz</span></span>
<span data-ttu-id="e3749-118">migAz는 전체 클래식 IaaS 리소스 집합을 Azure Resource Manager IaaS 리소스로 마이그레이션할 수 있는 추가 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="e3749-118">migAz is an additional option to migrate a complete set of classic IaaS resources to Azure Resource Manager IaaS resources.</span></span> <span data-ttu-id="e3749-119">동일한 구독 내에서 또는 서로 다른 구독 및 구독 형식(예: CSP 구독) 간에 마이그레이션을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3749-119">The migration can occur within the same subscription or between different subscriptions and subscription types (ex: CSP subscriptions).</span></span>

[<span data-ttu-id="e3749-120">도구 설명서 링크</span><span class="sxs-lookup"><span data-stu-id="e3749-120">Link to the tool documentation</span></span>](https://github.com/Azure/migAz)

## <a name="next-steps"></a><span data-ttu-id="e3749-121">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e3749-121">Next Steps</span></span>

* [<span data-ttu-id="e3749-122">클래식에서 Azure Resource Manager로 IaaS 리소스의 플랫폼 지원 마이그레이션 개요</span><span class="sxs-lookup"><span data-stu-id="e3749-122">Overview of platform-supported migration of IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="e3749-123">클래식에서 Azure Resource Manager로의 플랫폼 지원 마이그레이션에 대한 기술 정보</span><span class="sxs-lookup"><span data-stu-id="e3749-123">Technical deep dive on platform-supported migration from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="e3749-124">클래식에서 Azure Resource Manager로 IaaS 리소스의 마이그레이션 계획</span><span class="sxs-lookup"><span data-stu-id="e3749-124">Planning for migration of IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="e3749-125">PowerShell을 사용하여 클래식에서 Azure Resource Manager로 IaaS 리소스 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="e3749-125">Use PowerShell to migrate IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="e3749-126">CLI를 사용하여 클래식에서 Azure Resource Manager로 IaaS 리소스 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="e3749-126">Use CLI to migrate IaaS resources from classic to Azure Resource Manager</span></span>](../linux/migration-classic-resource-manager-cli.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="e3749-127">가장 일반적인 마이그레이션 오류 검토</span><span class="sxs-lookup"><span data-stu-id="e3749-127">Review most common migration errors</span></span>](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="e3749-128">클래식에서 Azure Resource Manager로의 IaaS 리소스 마이그레이션과 관련된 가장 자주 묻는 질문 검토</span><span class="sxs-lookup"><span data-stu-id="e3749-128">Review the most frequently asked questions about migrating IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

