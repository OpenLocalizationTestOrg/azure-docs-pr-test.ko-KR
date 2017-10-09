---
title: "Azure의 Windows Vm에 대 한 aaaResource 그룹 | Microsoft Docs"
description: "Hello 핵심 디자인 및 구현 지침 Azure 인프라 서비스에서 리소스 그룹을 배포 하기 위한 방법을 알아봅니다."
documentationcenter: 
services: virtual-machines-windows
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0fbcabcd-e96d-4d71-a526-431984887451
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 56b5670ec98bf3e80b7a622d5d760a57a7d20809
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-group-guidelines-for-windows-vms"></a><span data-ttu-id="d7be1-103">Windows VM에 대한 Azure 리소스 그룹 지침</span><span class="sxs-lookup"><span data-stu-id="d7be1-103">Azure resource group guidelines for Windows VMs</span></span>

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

<span data-ttu-id="d7be1-104">이 문서는 toologically 환경을 구축 하 고 리소스 그룹의 모든 hello 구성 요소를 그룹화 하는 방법을 이해에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="d7be1-104">This article focuses on understanding how toologically build out your environment and group all hello components in Resource Groups.</span></span>

## <a name="implementation-guidelines-for-resource-groups"></a><span data-ttu-id="d7be1-105">리소스 그룹에 대한 구현 지침</span><span class="sxs-lookup"><span data-stu-id="d7be1-105">Implementation guidelines for Resource Groups</span></span>
<span data-ttu-id="d7be1-106">의사 결정:</span><span class="sxs-lookup"><span data-stu-id="d7be1-106">Decisions:</span></span>

* <span data-ttu-id="d7be1-107">Hello 핵심 인프라 구성 요소에 의해 또는 완전 한 응용 프로그램 배포 하 여 리소스 그룹 아웃 toobuild 예정 입니까?</span><span class="sxs-lookup"><span data-stu-id="d7be1-107">Are you going toobuild out Resource Groups by hello core infrastructure components, or by complete application deployment?</span></span>
* <span data-ttu-id="d7be1-108">Toorestrict 액세스 tooResource 해야 역할 기반 액세스 제어를 사용 하 여 그룹화?</span><span class="sxs-lookup"><span data-stu-id="d7be1-108">Do you need toorestrict access tooResource Groups using Role-Based Access Controls?</span></span>

<span data-ttu-id="d7be1-109">작업:</span><span class="sxs-lookup"><span data-stu-id="d7be1-109">Tasks:</span></span>

* <span data-ttu-id="d7be1-110">필요한 핵심 인프라 구성 요소와 전용 리소스 그룹을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="d7be1-110">Define what core infrastructure components and dedicated Resource Groups you need.</span></span>
* <span data-ttu-id="d7be1-111">검토 방법 tooimplement 리소스 관리자 템플릿을 일치, 재현할 수 있는 배포에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7be1-111">Review how tooimplement Resource Manager templates for consistent, reproducible deployments.</span></span>
* <span data-ttu-id="d7be1-112">사용자 액세스 제어에 필요한 역할 액세스 tooResource 그룹 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7be1-112">Define what user access roles you need for controlling access tooResource Groups.</span></span>
* <span data-ttu-id="d7be1-113">명명 규칙을 사용 하 여 리소스 그룹의 hello 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d7be1-113">Create hello set of Resource Groups using your naming convention.</span></span> <span data-ttu-id="d7be1-114">Azure PowerShell 또는 hello 포털을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7be1-114">You can use Azure PowerShell or hello portal.</span></span>

## <a name="resource-groups"></a><span data-ttu-id="d7be1-115">리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="d7be1-115">Resource Groups</span></span>
<span data-ttu-id="d7be1-116">Azure에서 하면 논리적으로 저장소 계정, 가상 네트워크 및 가상 컴퓨터 (Vm) toodeploy 같이 관련된 리소스를 그룹화, 관리 및 단일 엔터티로 유지 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7be1-116">In Azure, you logically group related resources such as storage accounts, virtual networks, and virtual machines (VMs) toodeploy, manage, and maintain them as a single entity.</span></span> <span data-ttu-id="d7be1-117">이러한 방식을 통해 toodeploy 응용 프로그램을 더 쉽게 모든 hello 유지 관련 정보 이지만 리소스 함께 toogrant 또는 관리 측면에서 다른 사용자의 리소스 액세스 toothat 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="d7be1-117">This approach makes it easier toodeploy applications while keeping all hello related resources together from a management perspective, or toogrant others access toothat group of resources.</span></span> <span data-ttu-id="d7be1-118">리소스 그룹 이름은 90자까지 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7be1-118">Resource group names can be a maximum of 90 characters in length.</span></span> <span data-ttu-id="d7be1-119">리소스 그룹을 보다 포괄적인 이해 hello 읽을 [Azure 리소스 관리자 개요](../../azure-resource-manager/resource-group-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d7be1-119">For a more comprehensive understanding of Resource Groups, read hello [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="d7be1-120">핵심 기능은 tooResource 그룹 템플릿을 사용 하 여 사용자 환경 자세히 toobuild 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="d7be1-120">A key feature tooResource Groups is ability toobuild out your environment using templates.</span></span> <span data-ttu-id="d7be1-121">서식 파일은 JSON 파일 단순히 hello 저장소, 네트워킹, 선언 및 계산 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="d7be1-121">A template is simply a JSON file that declares hello storage, networking, and compute resources.</span></span> <span data-ttu-id="d7be1-122">모든 관련된 사용자 지정 스크립트 또는 구성 tooapply 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7be1-122">You can also define any related custom scripts or configurations tooapply.</span></span> <span data-ttu-id="d7be1-123">이러한 템플릿을 사용하여 응용 프로그램에 대해 일관되고 재현 가능한 배포를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d7be1-123">By using these templates, you create consistent, reproducible deployments for your applications.</span></span> <span data-ttu-id="d7be1-124">해당 동일한 템플릿 toocreate 프로덕션 배포를 사용 하 여 개발 환경으로 쉽게 toobuild는이 방법을 사용 하거나 그 반대로 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7be1-124">This approach makes it easy toobuild out an environment in development and then use that same template toocreate a production deployment, or vice versa.</span></span> <span data-ttu-id="d7be1-125">템플릿을 사용 하 여 이해를 참조 하세요 [템플릿 연습 hello](../../azure-resource-manager/resource-manager-template-walkthrough.md) 하는 과정을 안내해 hello 구축 서식 파일의 각 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="d7be1-125">For a better understanding using templates, read [hello template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md) that guides you through each step of hello building out a template.</span></span>

<span data-ttu-id="d7be1-126">리소스 그룹을 사용하여 환경을 디자인할 때 다음 두 가지 방식을 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7be1-126">There are two different approaches you can take when designing your environment with Resource Groups:</span></span>

* <span data-ttu-id="d7be1-127">리소스 그룹 hello 저장소 계정, 가상 네트워크 및 서브넷으로 Vm 결합 하는 각 응용 프로그램 배포에 대 한 분산 장치 등을 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7be1-127">Resource Groups for each application deployment that combines hello storage accounts, virtual networks, and subnets, VMs, load balancers, etc.</span></span>
* <span data-ttu-id="d7be1-128">핵심 가상 네트워킹과 서브넷 또는 저장소 계정이 포함된 중앙 집중식 리소스 그룹.</span><span class="sxs-lookup"><span data-stu-id="d7be1-128">Centralized Resource Groups that contain your core virtual networking and subnets or storage accounts.</span></span> <span data-ttu-id="d7be1-129">사용자의 응용 프로그램은 VM, 부하 분산 장치, 네트워크 인터페이스 등만을 포함하는 자체 리소스 그룹에 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7be1-129">Your applications are then in their own Resource Groups that only contain VMs, load balancers, network interfaces, etc.</span></span>

<span data-ttu-id="d7be1-130">가상 네트워킹에 대 한 중앙 집중식된 리소스 그룹을 만드는 out, 확장 및 서브넷을 통해 보다 쉽게 toobuild 것 처럼 크로스-프레미스 하이브리드 연결 옵션에 대 한 연결 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="d7be1-130">As you scale out, creating centralized Resource Groups for your virtual networking and subnets makes it easier toobuild cross-premises network connections for hybrid connectivity options.</span></span> <span data-ttu-id="d7be1-131">hello 또 다른 방법은 각 응용 프로그램 toohave에 대 한 자체 가상 네트워크에 필요한 구성 및 유지 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7be1-131">hello alternative approach is for each application toohave their own virtual network that requires configuration and maintenance.</span></span>  <span data-ttu-id="d7be1-132">[역할 기반 액세스 제어](../../active-directory/role-based-access-control-what-is.md) tooResource 그룹 구체적으로 toocontrol 액세스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7be1-132">[Role-Based Access Controls](../../active-directory/role-based-access-control-what-is.md) provide a granular way toocontrol access tooResource Groups.</span></span> <span data-ttu-id="d7be1-133">프로덕션 응용 프로그램에 대 한 해당 리소스에 액세스할 수 있는 hello 사용자가 제어할 수 있습니다 또는 hello 핵심 인프라 리소스에 대 한 이러한 엔지니어 toowork만 인프라를 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7be1-133">For production applications, you can control hello users that may access those resources, or for hello core infrastructure resources you can limit only infrastructure engineers toowork with them.</span></span> <span data-ttu-id="d7be1-134">응용 프로그램 소유자에 하나만 리소스 그룹 하지 hello 핵심 Azure 인프라의 사용자 환경 내에서 액세스 toohello 응용 프로그램 구성 요소.</span><span class="sxs-lookup"><span data-stu-id="d7be1-134">Your application owners only have access toohello application components within their Resource Group and not hello core Azure infrastructure of your environment.</span></span> <span data-ttu-id="d7be1-135">환경을 디자인할 때 hello 사용자를 toohello 리소스에 액세스 해야 하 고 그에 따라 리소스 그룹을 디자인 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d7be1-135">As you design your environment, consider hello users that require access toohello resources and design your Resource Groups accordingly.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="d7be1-136">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d7be1-136">Next steps</span></span>
[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-windows-infrastructure-guidelines-next-steps.md)]

