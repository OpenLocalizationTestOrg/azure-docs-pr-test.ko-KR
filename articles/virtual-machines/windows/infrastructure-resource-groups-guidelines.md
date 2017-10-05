---
title: "Windows VM에 대한 Azure 리소스 그룹 | Microsoft Docs"
description: "Azure 인프라 서비스에서 리소스 그룹을 배포하기 위한 핵심 디자인 및 구현 지침에 대해 알아봅니다."
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
ms.openlocfilehash: c0aca77af04f895d516f4943188d7890ae9586b7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-resource-group-guidelines-for-windows-vms"></a><span data-ttu-id="7ecf5-103">Windows VM에 대한 Azure 리소스 그룹 지침</span><span class="sxs-lookup"><span data-stu-id="7ecf5-103">Azure resource group guidelines for Windows VMs</span></span>

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

<span data-ttu-id="7ecf5-104">이 문서에서는 작업 환경을 논리적으로 구축하고 리소스 그룹의 모든 구성 요소를 함께 그룹화하는 방법을 집중적으로 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7ecf5-104">This article focuses on understanding how to logically build out your environment and group all the components in Resource Groups.</span></span>

## <a name="implementation-guidelines-for-resource-groups"></a><span data-ttu-id="7ecf5-105">리소스 그룹에 대한 구현 지침</span><span class="sxs-lookup"><span data-stu-id="7ecf5-105">Implementation guidelines for Resource Groups</span></span>
<span data-ttu-id="7ecf5-106">의사 결정:</span><span class="sxs-lookup"><span data-stu-id="7ecf5-106">Decisions:</span></span>

* <span data-ttu-id="7ecf5-107">리소스 그룹을 핵심 인프라 구성 요소를 통해 구축하려고 하나? 아니면 전체 응용 프로그램 배포를 통해 구축하려고 하나?</span><span class="sxs-lookup"><span data-stu-id="7ecf5-107">Are you going to build out Resource Groups by the core infrastructure components, or by complete application deployment?</span></span>
* <span data-ttu-id="7ecf5-108">역할 기반 액세스 제어를 사용하여 리소스 그룹에 대한 액세스를 제한해야 하나?</span><span class="sxs-lookup"><span data-stu-id="7ecf5-108">Do you need to restrict access to Resource Groups using Role-Based Access Controls?</span></span>

<span data-ttu-id="7ecf5-109">작업:</span><span class="sxs-lookup"><span data-stu-id="7ecf5-109">Tasks:</span></span>

* <span data-ttu-id="7ecf5-110">필요한 핵심 인프라 구성 요소와 전용 리소스 그룹을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="7ecf5-110">Define what core infrastructure components and dedicated Resource Groups you need.</span></span>
* <span data-ttu-id="7ecf5-111">일관되고 재현 가능한 배포를 위해 Resource Manager 템플릿을 구현하는 방법을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="7ecf5-111">Review how to implement Resource Manager templates for consistent, reproducible deployments.</span></span>
* <span data-ttu-id="7ecf5-112">리소스 그룹에 대한 액세스를 제어하는 데 필요한 사용자 액세스 역할을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="7ecf5-112">Define what user access roles you need for controlling access to Resource Groups.</span></span>
* <span data-ttu-id="7ecf5-113">명명 규칙을 사용하여 리소스 그룹 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7ecf5-113">Create the set of Resource Groups using your naming convention.</span></span> <span data-ttu-id="7ecf5-114">Azure PowerShell 또는 포털을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ecf5-114">You can use Azure PowerShell or the portal.</span></span>

## <a name="resource-groups"></a><span data-ttu-id="7ecf5-115">리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="7ecf5-115">Resource Groups</span></span>
<span data-ttu-id="7ecf5-116">Azure에서 저장소 계정, 가상 네트워크 및 가상 컴퓨터(VM)와 같은 관련된 리소스를 논리적으로 그룹화하여 단일 엔터티로 배포, 관리 및 유지 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="7ecf5-116">In Azure, you logically group related resources such as storage accounts, virtual networks, and virtual machines (VMs) to deploy, manage, and maintain them as a single entity.</span></span> <span data-ttu-id="7ecf5-117">이 방법을 통해 관리 관점에서 관련된 모든 리소스를 함께 유지하면서 응용 프로그램을 보다 배포할 수도 있고, 다른 사용자에게 해당 리소스 그룹에 대한 액세스 권한을 부여할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ecf5-117">This approach makes it easier to deploy applications while keeping all the related resources together from a management perspective, or to grant others access to that group of resources.</span></span> <span data-ttu-id="7ecf5-118">리소스 그룹 이름은 90자까지 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ecf5-118">Resource group names can be a maximum of 90 characters in length.</span></span> <span data-ttu-id="7ecf5-119">리소스 그룹을 보다 포괄적으로 이해하려면 [Azure Resource Manager 개요](../../azure-resource-manager/resource-group-overview.md)를 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="7ecf5-119">For a more comprehensive understanding of Resource Groups, read the [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="7ecf5-120">리소스 그룹의 주요 기능은 템플릿을 사용하여 사용자 환경을 구축하는 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="7ecf5-120">A key feature to Resource Groups is ability to build out your environment using templates.</span></span> <span data-ttu-id="7ecf5-121">템플릿은 저장소, 네트워킹 및 계산 리소스를 선언하는 JSON 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="7ecf5-121">A template is simply a JSON file that declares the storage, networking, and compute resources.</span></span> <span data-ttu-id="7ecf5-122">관련된 모든 사용자 지정 스크립트 또는 적용할 구성을 정의할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ecf5-122">You can also define any related custom scripts or configurations to apply.</span></span> <span data-ttu-id="7ecf5-123">이러한 템플릿을 사용하여 응용 프로그램에 대해 일관되고 재현 가능한 배포를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7ecf5-123">By using these templates, you create consistent, reproducible deployments for your applications.</span></span> <span data-ttu-id="7ecf5-124">이 방법을 통해 개발 환경을 쉽게 구축한 다음 동일한 템플릿을 사용하여 프로덕션 배포를 만들 수도 있고 그 반대도 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="7ecf5-124">This approach makes it easy to build out an environment in development and then use that same template to create a production deployment, or vice versa.</span></span> <span data-ttu-id="7ecf5-125">템플릿 사용 방식을 더욱 잘 이해하기 위해 템플릿 작성의 각 단계를 안내하는 [템플릿 연습](../../azure-resource-manager/resource-manager-template-walkthrough.md) 을 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="7ecf5-125">For a better understanding using templates, read [the template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md) that guides you through each step of the building out a template.</span></span>

<span data-ttu-id="7ecf5-126">리소스 그룹을 사용하여 환경을 디자인할 때 다음 두 가지 방식을 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ecf5-126">There are two different approaches you can take when designing your environment with Resource Groups:</span></span>

* <span data-ttu-id="7ecf5-127">저장소 계정, 가상 네트워크 및 서브넷, VM, 부하 분산 장치 등을 결합하는 각 응용 프로그램 배포를 위한 리소스 그룹.</span><span class="sxs-lookup"><span data-stu-id="7ecf5-127">Resource Groups for each application deployment that combines the storage accounts, virtual networks, and subnets, VMs, load balancers, etc.</span></span>
* <span data-ttu-id="7ecf5-128">핵심 가상 네트워킹과 서브넷 또는 저장소 계정이 포함된 중앙 집중식 리소스 그룹.</span><span class="sxs-lookup"><span data-stu-id="7ecf5-128">Centralized Resource Groups that contain your core virtual networking and subnets or storage accounts.</span></span> <span data-ttu-id="7ecf5-129">사용자의 응용 프로그램은 VM, 부하 분산 장치, 네트워크 인터페이스 등만을 포함하는 자체 리소스 그룹에 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ecf5-129">Your applications are then in their own Resource Groups that only contain VMs, load balancers, network interfaces, etc.</span></span>

<span data-ttu-id="7ecf5-130">가상 네트워킹 및 서브넷에 대한 중앙 집중식 리소스 그룹을 만드는 방식이 규모 확장 시 하이브리드 연결 옵션에 맞는 크로스-프레미스 네트워크 연결을 보다 쉽게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ecf5-130">As you scale out, creating centralized Resource Groups for your virtual networking and subnets makes it easier to build cross-premises network connections for hybrid connectivity options.</span></span> <span data-ttu-id="7ecf5-131">또 다른 방법은 각 응용 프로그램이 구성 및 유지 관리가 필요한 자체 가상 네트워크를 포함하도록 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7ecf5-131">The alternative approach is for each application to have their own virtual network that requires configuration and maintenance.</span></span>  <span data-ttu-id="7ecf5-132">[역할 기반 액세스 제어](../../active-directory/role-based-access-control-what-is.md) 는 리소스 그룹에 대한 액세스를 보다 세밀하게 제어할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ecf5-132">[Role-Based Access Controls](../../active-directory/role-based-access-control-what-is.md) provide a granular way to control access to Resource Groups.</span></span> <span data-ttu-id="7ecf5-133">프로덕션 응용 프로그램에서는 이러한 리소스에 액세스할 수 있는 사용자를 제어할 수 있고, 핵심 인프라 리소스의 경우에는 인프라 엔지니어만 사용할 수 있게 제안할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ecf5-133">For production applications, you can control the users that may access those resources, or for the core infrastructure resources you can limit only infrastructure engineers to work with them.</span></span> <span data-ttu-id="7ecf5-134">응용 프로그램 소유자는 작업 환경의 핵심 Azure 인프라가 아닌 리소스 그룹 내의 응용 프로그램 구성 요소에만 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ecf5-134">Your application owners only have access to the application components within their Resource Group and not the core Azure infrastructure of your environment.</span></span> <span data-ttu-id="7ecf5-135">작업 환경을 디자인할 때 리소스에 액세스해야 하는 사용자를 고려하고 그에 맞게 리소스 그룹을 디자인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ecf5-135">As you design your environment, consider the users that require access to the resources and design your Resource Groups accordingly.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="7ecf5-136">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7ecf5-136">Next steps</span></span>
[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-windows-infrastructure-guidelines-next-steps.md)]

