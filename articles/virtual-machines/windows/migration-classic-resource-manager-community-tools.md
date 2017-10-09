---
title: "aaaCommunity 도구-이동 클래식 리소스 tooAzure 리소스 관리자 | Microsoft Docs"
description: "Hello 커뮤니티 toohelp에서 제공 하는이 문서 카탈로그 hello 도구 클래식 toohello Azure 리소스 관리자 배포 모델에서 IaaS 리소스를 마이그레이션합니다."
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
ms.openlocfilehash: 67d5624a14d12a2d9eb46eb12aef461b706d4589
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="community-tools-toomigrate-iaas-resources-from-classic-tooazure-resource-manager"></a><span data-ttu-id="03b3a-103">커뮤니티 도구 toomigrate 클래식 tooAzure 리소스 관리자에서에서 처리 되는 IaaS 리소스</span><span class="sxs-lookup"><span data-stu-id="03b3a-103">Community tools toomigrate IaaS resources from classic tooAzure Resource Manager</span></span>
<span data-ttu-id="03b3a-104">클래식 toohello Azure 리소스 관리자 배포 모델에서 IaaS 리소스에 대 한 마이그레이션을 사용 하 여 hello 커뮤니티 tooassist에서 제공 된이 문서 카탈로그 hello 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="03b3a-104">This article catalogs hello tools that have been provided by hello community tooassist with migration of IaaS resources from classic toohello Azure Resource Manager deployment model.</span></span>

> [!NOTE]
> <span data-ttu-id="03b3a-105">이러한 도구는 Microsoft 지원을 통해 공식적으로 지원되지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="03b3a-105">These tools are not officially supported by Microsoft Support.</span></span> <span data-ttu-id="03b3a-106">따라서 열려 있는 GitHub에 원본이 고 we're 수정 또는 추가 시나리오에 대 한 만족도 매우 tooaccept Pr 합니다.</span><span class="sxs-lookup"><span data-stu-id="03b3a-106">Therefore they are open sourced on GitHub and we're happy tooaccept PRs for fixes or additional scenarios.</span></span> <span data-ttu-id="03b3a-107">문제가 tooreport hello GitHub 문제점 기능을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="03b3a-107">tooreport an issue, use hello GitHub issues feature.</span></span>
> 
> <span data-ttu-id="03b3a-108">이러한 도구를 사용하여 마이그레이션을 수행하면 클래식 Virtual Machine의 가동이 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="03b3a-108">Migrating with these tools will cause downtime for your classic Virtual Machine.</span></span> <span data-ttu-id="03b3a-109">플랫폼에서 지원하는 마이그레이션 방법은 다음 페이지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="03b3a-109">If you're looking for platform supported migration, visit</span></span> 
> 
>   * [<span data-ttu-id="03b3a-110">플랫폼이는 클래식 tooAzure 리소스 관리자 스택에서 IaaS 리소스의 마이그레이션 지원</span><span class="sxs-lookup"><span data-stu-id="03b3a-110">Platform supported migration of IaaS resources from Classic tooAzure Resource Manager stack</span></span>](migration-classic-resource-manager-overview.md)
>   * [<span data-ttu-id="03b3a-111">플랫폼에 대 한 기술 고찰 클래식 tooAzure 리소스 관리자에서에서의 마이그레이션 지원</span><span class="sxs-lookup"><span data-stu-id="03b3a-111">Technical Deep Dive on Platform supported migration from Classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-deep-dive.md)
>   * [<span data-ttu-id="03b3a-112">IaaS 리소스 클래식 tooAzure Azure PowerShell을 사용 하 여 리소스 관리자에서 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="03b3a-112">Migrate IaaS resources from Classic tooAzure Resource Manager using Azure PowerShell</span></span>](migration-classic-resource-manager-ps.md)
> 
> 

## <a name="asmmetadataparser"></a><span data-ttu-id="03b3a-113">AsmMetadataParser</span><span class="sxs-lookup"><span data-stu-id="03b3a-113">AsmMetadataParser</span></span>
<span data-ttu-id="03b3a-114">Azure 서비스 관리 tooAzure 리소스 관리자에서에서 엔터프라이즈 마이그레이션의 일부로 만들어진 도우미 도구의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="03b3a-114">This is a collection of helper tools created as part of enterprise migrations from Azure Service Management tooAzure Resource Manager.</span></span> <span data-ttu-id="03b3a-115">이 도구는 tooreplicate hello 마이그레이션 프로덕션 구독에 대해 실행 하기 전에 강철 있는 문제 및 마이그레이션 테스트에 사용할 수 있는 다른 구독으로 인프라입니다.</span><span class="sxs-lookup"><span data-stu-id="03b3a-115">This tool allows you tooreplicate your infrastructure into another subscription which can be used for testing migration and iron out any issues before running hello migration on your Production subscription.</span></span>

[<span data-ttu-id="03b3a-116">링크 toohello 도구 설명서</span><span class="sxs-lookup"><span data-stu-id="03b3a-116">Link toohello tool documentation</span></span>](https://github.com/Azure/classic-iaas-resourcemanager-migration/tree/master/AsmToArmMigrationApiToolset)

## <a name="migaz"></a><span data-ttu-id="03b3a-117">migAz</span><span class="sxs-lookup"><span data-stu-id="03b3a-117">migAz</span></span>
<span data-ttu-id="03b3a-118">migAz는 옵션이 추가로 toomigrate 클래식 IaaS 리소스 tooAzure 리소스 관리자 IaaS 리소스의 전체 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="03b3a-118">migAz is an additional option toomigrate a complete set of classic IaaS resources tooAzure Resource Manager IaaS resources.</span></span> <span data-ttu-id="03b3a-119">hello 마이그레이션 내에서 발생할 수 hello 동일 구독 간이나 서로 다른 구독 및 구독 유형 (예: CSP 구독).</span><span class="sxs-lookup"><span data-stu-id="03b3a-119">hello migration can occur within hello same subscription or between different subscriptions and subscription types (ex: CSP subscriptions).</span></span>

[<span data-ttu-id="03b3a-120">링크 toohello 도구 설명서</span><span class="sxs-lookup"><span data-stu-id="03b3a-120">Link toohello tool documentation</span></span>](https://github.com/Azure/migAz)

## <a name="next-steps"></a><span data-ttu-id="03b3a-121">다음 단계</span><span class="sxs-lookup"><span data-stu-id="03b3a-121">Next Steps</span></span>

* [<span data-ttu-id="03b3a-122">클래식 tooAzure 리소스 관리자에서에서 리소스를 IaaS 플랫폼에서 지 원하는 마이그레이션 개요</span><span class="sxs-lookup"><span data-stu-id="03b3a-122">Overview of platform-supported migration of IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="03b3a-123">클래식 tooAzure 리소스 관리자에서에서 마이그레이션 플랫폼 지원에 기술 심층 분석</span><span class="sxs-lookup"><span data-stu-id="03b3a-123">Technical deep dive on platform-supported migration from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="03b3a-124">클래식 tooAzure 리소스 관리자에서에서 IaaS 리소스의 마이그레이션 계획</span><span class="sxs-lookup"><span data-stu-id="03b3a-124">Planning for migration of IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="03b3a-125">클래식 tooAzure 리소스 관리자에서에서 PowerShell toomigrate IaaS 리소스를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="03b3a-125">Use PowerShell toomigrate IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="03b3a-126">CLI toomigrate IaaS 리소스 클래식 tooAzure 리소스 관리자를에서 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="03b3a-126">Use CLI toomigrate IaaS resources from classic tooAzure Resource Manager</span></span>](../linux/migration-classic-resource-manager-cli.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="03b3a-127">가장 일반적인 마이그레이션 오류 검토</span><span class="sxs-lookup"><span data-stu-id="03b3a-127">Review most common migration errors</span></span>](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="03b3a-128">클래식 tooAzure 리소스 관리자에서에서 마이그레이션 IaaS 리소스에 대 한 가장 자주 묻는 질문 검토 hello</span><span class="sxs-lookup"><span data-stu-id="03b3a-128">Review hello most frequently asked questions about migrating IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

