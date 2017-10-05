---
title: "Azure 리소스 관리자 개요 | Microsoft Docs"
description: "Azure에서 리소스 배포, 관리 및 Access Control용 Azure 리소스 관리자 사용 방법을 설명합니다."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 76df7de1-1d3b-436e-9b44-e1b3766b3961
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: tomfitz
ms.openlocfilehash: f539931e0704f904f4b942f185f086a790caf4da
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-resource-manager-overview"></a><span data-ttu-id="1ff9b-103">Azure Resource Manager 개요</span><span class="sxs-lookup"><span data-stu-id="1ff9b-103">Azure Resource Manager overview</span></span>
<span data-ttu-id="1ff9b-104">응용 프로그램에 대한 인프라는 일반적으로 가상 컴퓨터, 저장소 계정 및 가상 네트워크 또는 웹앱, 데이터베이스, 데이터베이스 서버 및 타사 서비스 등의 많은 구성 요소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-104">The infrastructure for your application is typically made up of many components – maybe a virtual machine, storage account, and virtual network, or a web app, database, database server, and 3rd party services.</span></span> <span data-ttu-id="1ff9b-105">이러한 구성 요소를 별도 엔터티로 표시하지 않으면, 대신 관련된 단일 엔터티의 상호 종속적으로 부분으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-105">You do not see these components as separate entities, instead you see them as related and interdependent parts of a single entity.</span></span> <span data-ttu-id="1ff9b-106">그룹으로 배포, 관리 및 모니터링하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-106">You want to deploy, manage, and monitor them as a group.</span></span> <span data-ttu-id="1ff9b-107">Azure 리소스 관리자를 사용하면 솔루션에서 리소스를 그룹으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-107">Azure Resource Manager enables you to work with the resources in your solution as a group.</span></span> <span data-ttu-id="1ff9b-108">조정된 단일 작업에서 솔루션에 대한 모든 리소스를 배포, 업데이트 또는 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-108">You can deploy, update, or delete all the resources for your solution in a single, coordinated operation.</span></span> <span data-ttu-id="1ff9b-109">배포용 템플릿을 사용하고 이 템플릿을 테스트, 스테이징 및 프로덕션과 같은 여러 환경에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-109">You use a template for deployment and that template can work for different environments such as testing, staging, and production.</span></span> <span data-ttu-id="1ff9b-110">리소스 관리자는 보안, 감사 및 태그 기능을 제공하여 배포 후에 리소스를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-110">Resource Manager provides security, auditing, and tagging features to help you manage your resources after deployment.</span></span> 

## <a name="terminology"></a><span data-ttu-id="1ff9b-111">용어</span><span class="sxs-lookup"><span data-stu-id="1ff9b-111">Terminology</span></span>
<span data-ttu-id="1ff9b-112">Azure Resource Manager가 처음이라면 익숙하지 않은 용어가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-112">If you are new to Azure Resource Manager, there are some terms you might not be familiar with.</span></span>

* <span data-ttu-id="1ff9b-113">**리소스** - Azure를 통해 사용할 수 있는 관리 가능한 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-113">**resource** - A manageable item that is available through Azure.</span></span> <span data-ttu-id="1ff9b-114">몇 가지 일반적인 리소스는 가상 컴퓨터, 저장소 계정, 웹앱, 데이터베이스 및 가상 네트워크이지만 더 많은 종류가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-114">Some common resources are a virtual machine, storage account, web app, database, and virtual network, but there are many more.</span></span>
* <span data-ttu-id="1ff9b-115">**리소스 그룹** - Azure 솔루션에 관련된 리소스를 보유하는 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-115">**resource group** - A container that holds related resources for an Azure solution.</span></span> <span data-ttu-id="1ff9b-116">리소스 그룹에는 솔루션에 대한 모든 리소스 또는 그룹으로 관리하려는 해당 리소스만 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-116">The resource group can include all the resources for the solution, or only those resources that you want to manage as a group.</span></span> <span data-ttu-id="1ff9b-117">사용자의 조직에 가장 적합한 내용에 따라 리소스 그룹에 리소스를 어떻게 할당할지 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-117">You decide how you want to allocate resources to resource groups based on what makes the most sense for your organization.</span></span> <span data-ttu-id="1ff9b-118">[리소스 그룹](#resource-groups)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-118">See [Resource groups](#resource-groups).</span></span>
* <span data-ttu-id="1ff9b-119">**리소스 공급자** - Resource Manager를 통해 배포하고 관리할 수 있는 리소스를 제공하는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-119">**resource provider** - A service that supplies the resources you can deploy and manage through Resource Manager.</span></span> <span data-ttu-id="1ff9b-120">각 리소스 공급자는 배포된 리소스로 작업하기 위한 작업을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-120">Each resource provider offers operations for working with the resources that are deployed.</span></span> <span data-ttu-id="1ff9b-121">몇 가지 일반 리소스 공급자는 가상 컴퓨터 리소스를 제공하는 Microsoft.Compute, 저장소 계정 리소스를 제공하는 Microsoft.Storage 및 웹앱에 관련된 리소스를 제공하는 Microsoft.Web입니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-121">Some common resource providers are Microsoft.Compute, which supplies the virtual machine resource, Microsoft.Storage, which supplies the storage account resource, and Microsoft.Web, which supplies resources related to web apps.</span></span> <span data-ttu-id="1ff9b-122">[리소스 공급자](#resource-providers)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-122">See [Resource providers](#resource-providers).</span></span>
* <span data-ttu-id="1ff9b-123">**Resource Manager 템플릿** - 리소스 그룹에 배포한 하나 이상의 리소스를 정의하는 JSON(JavaScript Object Notation) 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-123">**Resource Manager template** - A JavaScript Object Notation (JSON) file that defines one or more resources to deploy to a resource group.</span></span> <span data-ttu-id="1ff9b-124">또한 배포된 리소스 간의 종속성을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-124">It also defines the dependencies between the deployed resources.</span></span> <span data-ttu-id="1ff9b-125">템플릿은 리소스를 일관되고 반복적으로 배포하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-125">The template can be used to deploy the resources consistently and repeatedly.</span></span> <span data-ttu-id="1ff9b-126">[템플릿 배포](#template-deployment)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-126">See [Template deployment](#template-deployment).</span></span>
* <span data-ttu-id="1ff9b-127">**선언적 구문** - 항목을 만드는 프로그래밍 명령의 시퀀스를 작성하지 않고도 "만들려는 대상은 다음과 같습니다"라고 선언하는 구문입니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-127">**declarative syntax** - Syntax that lets you state "Here is what I intend to create" without having to write the sequence of programming commands to create it.</span></span> <span data-ttu-id="1ff9b-128">Resource Manager 템플릿은 선언적 구문의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-128">The Resource Manager template is an example of declarative syntax.</span></span> <span data-ttu-id="1ff9b-129">파일에서 Azure에 배포하는 인프라에 대한 속성을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-129">In the file, you define the properties for the infrastructure to deploy to Azure.</span></span> 

## <a name="the-benefits-of-using-resource-manager"></a><span data-ttu-id="1ff9b-130">리소스 관리자를 사용할 경우의 이점</span><span class="sxs-lookup"><span data-stu-id="1ff9b-130">The benefits of using Resource Manager</span></span>
<span data-ttu-id="1ff9b-131">리소스 관리자는 다음과 같은 여러 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-131">Resource Manager provides several benefits:</span></span>

* <span data-ttu-id="1ff9b-132">이 리소스를 개별적으로 처리하는 것이 아니라 솔루션에 대한 모든 리소스를 그룹으로 배포, 관리 및 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-132">You can deploy, manage, and monitor all the resources for your solution as a group, rather than handling these resources individually.</span></span>
* <span data-ttu-id="1ff9b-133">개발 수명 주기 내내 솔루션을 반복적으로 배포하며 안심하고 일관된 상태로 리소스를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-133">You can repeatedly deploy your solution throughout the development lifecycle and have confidence your resources are deployed in a consistent state.</span></span>
* <span data-ttu-id="1ff9b-134">스크립트가 아닌 선언적 템플릿을 통해 인프라를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-134">You can manage your infrastructure through declarative templates rather than scripts.</span></span>
* <span data-ttu-id="1ff9b-135">올바른 순서로 배포되므로 리소스 간의 종속성을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-135">You can define the dependencies between resources so they are deployed in the correct order.</span></span>
* <span data-ttu-id="1ff9b-136">역할 기반 Access Control(RBAC)가 관리 플랫폼으로 통합되기 때문에 리소스 그룹의 모든 서비스에 대해 Access Control를 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-136">You can apply access control to all services in your resource group because Role-Based Access Control (RBAC) is natively integrated into the management platform.</span></span>
* <span data-ttu-id="1ff9b-137">리소스에 태그를 적용하여 구독에서 모든 리소스를 논리적으로 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-137">You can apply tags to resources to logically organize all the resources in your subscription.</span></span>
* <span data-ttu-id="1ff9b-138">같은 태그를 공유하는 리소스 그룹에 대한 비용을 확인하여 조직의 청구를 명확히 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-138">You can clarify your organization's billing by viewing costs for a group of resources sharing the same tag.</span></span>  

<span data-ttu-id="1ff9b-139">리소스 관리자는 솔루션을 배포 및 관리하는 새로운 방식을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-139">Resource Manager provides a new way to deploy and manage your solutions.</span></span> <span data-ttu-id="1ff9b-140">이전의 배포 모델을 사용한 경우 변경 사항을 알아보려면 [리소스 관리자 배포 및 클래식 배포 이해](resource-manager-deployment-model.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-140">If you used the earlier deployment model and want to learn about the changes, see [Understanding Resource Manager deployment and classic deployment](resource-manager-deployment-model.md).</span></span>

## <a name="consistent-management-layer"></a><span data-ttu-id="1ff9b-141">일관적인 관리 계층</span><span class="sxs-lookup"><span data-stu-id="1ff9b-141">Consistent management layer</span></span>
<span data-ttu-id="1ff9b-142">리소스 관리자는 Azure PowerShell, Azure CLI, Azure 포털, REST API 및 개발 도구를 통해 수행하는 작업에 대한 일관적인 관리 계층을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-142">Resource Manager provides a consistent management layer for the tasks you perform through Azure PowerShell, Azure CLI, Azure portal, REST API, and development tools.</span></span> <span data-ttu-id="1ff9b-143">모든 도구는 작업의 공통 집합을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-143">All the tools use a common set of operations.</span></span> <span data-ttu-id="1ff9b-144">가장 적합한 도구를 사용하며 혼동 없이 서로 교환해서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-144">You use the tools that work best for you, and can use them interchangeably without confusion.</span></span> 

<span data-ttu-id="1ff9b-145">다음 그림에서는 모든 도구가 동일한 Azure Resource Manager API와 상호 작용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-145">The following image shows how all the tools interact with the same Azure Resource Manager API.</span></span> <span data-ttu-id="1ff9b-146">API는 요청을 인증하고 권한을 부여하는 리소스 관리자 서비스에 요청을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-146">The API passes requests to the Resource Manager service, which authenticates and authorizes the requests.</span></span> <span data-ttu-id="1ff9b-147">그런 다음 리소스 관리자는 적절한 리소스 공급자에게 요청을 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-147">Resource Manager then routes the requests to the appropriate resource providers.</span></span>

![리소스 관리자 요청 모델](./media/resource-group-overview/consistent-management-layer.png)

## <a name="guidance"></a><span data-ttu-id="1ff9b-149">인도</span><span class="sxs-lookup"><span data-stu-id="1ff9b-149">Guidance</span></span>
<span data-ttu-id="1ff9b-150">다음 제안으로 솔루션으로 작업할 때 Resource Manager를 완벽하게 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-150">The following suggestions help you take full advantage of Resource Manager when working with your solutions.</span></span>

1. <span data-ttu-id="1ff9b-151">명령적 명령을 사용하는 대신 리소스 관리자 템플릿의 선언적 구문을 통해 인프라를 정의하고 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-151">Define and deploy your infrastructure through the declarative syntax in Resource Manager templates, rather than through imperative commands.</span></span>
2. <span data-ttu-id="1ff9b-152">템플릿에서 모든 배포 및 구성 단계를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-152">Define all deployment and configuration steps in the template.</span></span> <span data-ttu-id="1ff9b-153">솔루션을 설정하기 위해 수동 단계가 없어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-153">You should have no manual steps for setting up your solution.</span></span>
3. <span data-ttu-id="1ff9b-154">명령적 명령을 실행하여 앱 또는 컴퓨터를 시작하거나 중지하는 등 리소스를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-154">Run imperative commands to manage your resources, such as to start or stop an app or machine.</span></span>
4. <span data-ttu-id="1ff9b-155">리소스 그룹에서 동일한 수명 주기로 리소스를 정렬합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-155">Arrange resources with the same lifecycle in a resource group.</span></span> <span data-ttu-id="1ff9b-156">리소스의 모든 다른 구성에 태그를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-156">Use tags for all other organizing of resources.</span></span>

<span data-ttu-id="1ff9b-157">템플릿에 대한 권장 사항은 [Azure Resource Manager 템플릿 생성 모범 사례](resource-manager-template-best-practices.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-157">For recommendations about templates, see [Best practices for creating Azure Resource Manager templates](resource-manager-template-best-practices.md).</span></span>

<span data-ttu-id="1ff9b-158">엔터프라이즈에서 리소스 관리자를 사용하여 구독을 효과적으로 관리할 수 있는 방법에 대한 지침은 [Azure 엔터프라이즈 스캐폴드 - 규범적 구독 거버넌스](resource-manager-subscription-governance.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-158">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

## <a name="resource-groups"></a><span data-ttu-id="1ff9b-159">리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="1ff9b-159">Resource groups</span></span>
<span data-ttu-id="1ff9b-160">리소스 그룹을 정의할 때 고려해야 할 몇 가지 중요한 요인이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-160">There are some important factors to consider when defining your resource group:</span></span>

1. <span data-ttu-id="1ff9b-161">그룹에서 모든 리소스는 동일한 수명 주기를 공유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-161">All the resources in your group should share the same lifecycle.</span></span> <span data-ttu-id="1ff9b-162">리소스를 함께 배포, 업데이트, 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-162">You deploy, update, and delete them together.</span></span> <span data-ttu-id="1ff9b-163">데이터베이스 서버와 같은 하나의 리소스에 다양한 배포 주기가 존재하는 경우 다른 리소스 그룹에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-163">If one resource, such as a database server, needs to exist on a different deployment cycle it should be in another resource group.</span></span>
2. <span data-ttu-id="1ff9b-164">각 리소스는 하나의 리소스 그룹에만 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-164">Each resource can only exist in one resource group.</span></span>
3. <span data-ttu-id="1ff9b-165">언제든지 리소스 그룹에 리소스를 추가하거나 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-165">You can add or remove a resource to a resource group at any time.</span></span>
4. <span data-ttu-id="1ff9b-166">특정 리소스 그룹에서 다른 그룹에 리소스를 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-166">You can move a resource from one resource group to another group.</span></span> <span data-ttu-id="1ff9b-167">자세한 내용을 보려면 [새 리소스 그룹 또는 구독으로 리소스 이동](resource-group-move-resources.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-167">For more information, see [Move resources to new resource group or subscription](resource-group-move-resources.md).</span></span>
5. <span data-ttu-id="1ff9b-168">리소스 그룹을 다른 지역에 상주하는 리소스를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-168">A resource group can contain resources that reside in different regions.</span></span>
6. <span data-ttu-id="1ff9b-169">관리 작업에 대한 Access Control 범위를 지정하는 데 리소스 그룹을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-169">A resource group can be used to scope access control for administrative actions.</span></span>
7. <span data-ttu-id="1ff9b-170">리소스는 다른 리소스 그룹의 리소스와 상호 작용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-170">A resource can interact with resources in other resource groups.</span></span> <span data-ttu-id="1ff9b-171">이 상호 작용은 두 개의 리소스가 관련되어 있지만 동일한 수명 주기를 공유하지 않는 경우에 일반적입니다(예: 데이터베이스에 연결된 웹앱).</span><span class="sxs-lookup"><span data-stu-id="1ff9b-171">This interaction is common when the two resources are related but do not share the same lifecycle (for example, web apps connecting to a database).</span></span>

<span data-ttu-id="1ff9b-172">리소스 그룹을 만들 때 해당 리소스 그룹의 위치를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-172">When creating a resource group, you need to provide a location for that resource group.</span></span> <span data-ttu-id="1ff9b-173">리소스 그룹에 위치가 필요한 이유는 무엇인지 궁금할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-173">You may be wondering, "Why does a resource group need a location?</span></span> <span data-ttu-id="1ff9b-174">리소스의 위치가 리소스 그룹과 다른 경우 리소스 그룹 위치가 중요한 이유는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="1ff9b-174">And, if the resources can have different locations than the resource group, why does the resource group location matter at all?"</span></span> <span data-ttu-id="1ff9b-175">리소스 그룹은 리소스에 대한 메타데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-175">The resource group stores metadata about the resources.</span></span> <span data-ttu-id="1ff9b-176">따라서 리소스 그룹의 위치를 지정하면 메타데이터가 저장된 위치를 지정하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-176">Therefore, when you specify a location for the resource group, you are specifying where that metadata is stored.</span></span> <span data-ttu-id="1ff9b-177">규정 준수 때문에 특정 지역에 데이터가 저장되는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-177">For compliance reasons, you may need to ensure that your data is stored in a particular region.</span></span>

## <a name="resource-providers"></a><span data-ttu-id="1ff9b-178">리소스 공급자</span><span class="sxs-lookup"><span data-stu-id="1ff9b-178">Resource providers</span></span>
<span data-ttu-id="1ff9b-179">각 리소스 공급자는 Azure 서비스를 사용하는 일련의 리소스 및 작업을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-179">Each resource provider offers a set of resources and operations for working with an Azure service.</span></span> <span data-ttu-id="1ff9b-180">예를 들어 키와 암호를 저장하려는 경우 **Microsoft.KeyVault** 리소스 공급자로 작업합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-180">For example, if you want to store keys and secrets, you work with the **Microsoft.KeyVault** resource provider.</span></span> <span data-ttu-id="1ff9b-181">이 리소스 공급자는 키 자격 증명 모음을 만드는 데 **자격 증명 모음**이라는 리소스 유형을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-181">This resource provider offers a resource type called **vaults** for creating the key vault.</span></span> 

<span data-ttu-id="1ff9b-182">리소스 종류의 이름은 **{resource-provider}/{resource-type}** 양식입니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-182">The name of a resource type is in the format: **{resource-provider}/{resource-type}**.</span></span> <span data-ttu-id="1ff9b-183">예를 들어 키 자격 증명 모음 형식은 **Microsoft.KeyVault/vaults**입니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-183">For example, the key vault type is **Microsoft.KeyVault/vaults**.</span></span>

<span data-ttu-id="1ff9b-184">리소스 배포를 시작하기 전에 사용 가능한 리소스 공급자를 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-184">Before getting started with deploying your resources, you should gain an understanding of the available resource providers.</span></span> <span data-ttu-id="1ff9b-185">리소스 공급자 및 리소스의 이름을 알고 있으면 Azure에 배포하려는 리소스를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-185">Knowing the names of resource providers and resources helps you define resources you want to deploy to Azure.</span></span> <span data-ttu-id="1ff9b-186">또한 각 리소스 종류에 대한 유효한 위치와 API 버전을 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-186">Also, you need to know the valid locations and API versions for each resource type.</span></span> <span data-ttu-id="1ff9b-187">자세한 내용은 [리소스 공급자 및 형식](resource-manager-supported-services.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-187">For more information, see [Resource providers and types](resource-manager-supported-services.md).</span></span>

## <a name="template-deployment"></a><span data-ttu-id="1ff9b-188">템플릿 배포</span><span class="sxs-lookup"><span data-stu-id="1ff9b-188">Template deployment</span></span>
<span data-ttu-id="1ff9b-189">Resource Manager로 Azure 솔루션의 인프라 및 구성을 정의하는 템플릿을 JSON 형식으로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-189">With Resource Manager, you can create a template (in JSON format) that defines the infrastructure and configuration of your Azure solution.</span></span> <span data-ttu-id="1ff9b-190">템플릿을 사용하여 수명 주기 내내 솔루션을 반복적으로 배포하고 안심하고 일관된 상태로 리소스를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-190">By using a template, you can repeatedly deploy your solution throughout its lifecycle and have confidence your resources are deployed in a consistent state.</span></span> <span data-ttu-id="1ff9b-191">포털에서 솔루션을 만들 때 자동으로 솔루션에 배포 템플릿을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-191">When you create a solution from the portal, the solution automatically includes a deployment template.</span></span> <span data-ttu-id="1ff9b-192">솔루션용 템플릿으로 시작하고 특정 요구 사항에 맞게 사용자 지정할 수 있기 때문에 서식 파일을 처음부터 새로 만들 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-192">You do not have to create your template from scratch because you can start with the template for your solution and customize it to meet your specific needs.</span></span> <span data-ttu-id="1ff9b-193">리소스 그룹의 현재 상태를 내보내거나 특정 배포에 사용된 템플릿을 검토하여 기존 리소스 그룹에 대한 템플릿을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-193">You can retrieve a template for an existing resource group by either exporting the current state of the resource group, or viewing the template used for a particular deployment.</span></span> <span data-ttu-id="1ff9b-194">[내보낸 템플릿](resource-manager-export-template.md)을 살펴보면 템플릿 구문에 대해 알아보는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-194">Viewing the [exported template](resource-manager-export-template.md) is a helpful way to learn about the template syntax.</span></span>

<span data-ttu-id="1ff9b-195">템플릿의 형식 및 템플릿을 생성하는 방법에 대해 알아보려면 [첫 번째 Azure Resource Manager 템플릿 만들기](resource-manager-create-first-template.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-195">To learn about the format of the template and how you construct it, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span> <span data-ttu-id="1ff9b-196">리소스 유형의 JSON 구문을 보려면 [Azure Resource Manager 템플릿에서 리소스 정의](/azure/templates/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-196">To view the JSON syntax for resources types, see [Define resources in Azure Resource Manager templates](/azure/templates/).</span></span>

<span data-ttu-id="1ff9b-197">리소스 관리자는 다른 요청과 같이 템플릿을 처리합니다([일관적인 관리 계층](#consistent-management-layer)에 대한 이미지 참조).</span><span class="sxs-lookup"><span data-stu-id="1ff9b-197">Resource Manager processes the template like any other request (see the image for [Consistent management layer](#consistent-management-layer)).</span></span> <span data-ttu-id="1ff9b-198">템플릿을 구문 분석하고 해당 구문을 적절한 리소스 공급자에 대한 REST API 작업으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-198">It parses the template and converts its syntax into REST API operations for the appropriate resource providers.</span></span> <span data-ttu-id="1ff9b-199">예를 들어 리소스 관리자가 다음 리소스 정의로 템플릿을 받는 경우:</span><span class="sxs-lookup"><span data-stu-id="1ff9b-199">For example, when Resource Manager receives a template with the following resource definition:</span></span>

```json
"resources": [
  {
    "apiVersion": "2016-01-01",
    "type": "Microsoft.Storage/storageAccounts",
    "name": "mystorageaccount",
    "location": "westus",
    "sku": {
      "name": "Standard_LRS"
    },
    "kind": "Storage",
    "properties": {
    }
  }
]
```

<span data-ttu-id="1ff9b-200">Microsoft.Storage 리소스 공급자에게 전송되는 다음 REST API 작업으로 정의를 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-200">It converts the definition to the following REST API operation, which is sent to the Microsoft.Storage resource provider:</span></span>

```HTTP
PUT
https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/mystorageaccount?api-version=2016-01-01
REQUEST BODY
{
  "location": "westus",
  "properties": {
  }
  "sku": {
    "name": "Standard_LRS"
  },   
  "kind": "Storage"
}
```

<span data-ttu-id="1ff9b-201">템플릿 및 리소스 그룹을 정의하는 방법은 사용자 및 솔루션을 관리하려는 방법에 전적으로 달려 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-201">How you define templates and resource groups is entirely up to you and how you want to manage your solution.</span></span> <span data-ttu-id="1ff9b-202">예를 들어 단일 템플릿을 통해 3계층 응용 프로그램을 단일 리소스 그룹에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-202">For example, you can deploy your three tier application through a single template to a single resource group.</span></span>

![3계층 템플릿](./media/resource-group-overview/3-tier-template.png)

<span data-ttu-id="1ff9b-204">그러나 단일 템플릿에서 전체 인프라를 정의할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-204">But, you do not have to define your entire infrastructure in a single template.</span></span> <span data-ttu-id="1ff9b-205">대부분 배포 요구 사항을 대상, 목적에 특정 템플릿 집합으로 나누는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-205">Often, it makes sense to divide your deployment requirements into a set of targeted, purpose-specific templates.</span></span> <span data-ttu-id="1ff9b-206">서로 다른 솔루션에 이러한 템플릿을 쉽게 다시 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-206">You can easily reuse these templates for different solutions.</span></span> <span data-ttu-id="1ff9b-207">특정 솔루션을 배포하려면 모든 필수 템플릿에 연결하는 마스터 템플릿을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-207">To deploy a particular solution, you create a master template that links all the required templates.</span></span> <span data-ttu-id="1ff9b-208">다음 이미지는 세 개의 중첩된 템플릿을 포함하는 부모 템플릿을 통해 3계층 솔루션을 배포하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-208">The following image shows how to deploy a three tier solution through a parent template that includes three nested templates.</span></span>

![중첩된 계층 템플릿](./media/resource-group-overview/nested-tiers-template.png)

<span data-ttu-id="1ff9b-210">계층이 별도 수명 주기를 갖도록 계획하는 경우 3계층을 별도 리소스 그룹에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-210">If you envision your tiers having separate lifecycles, you can deploy your three tiers to separate resource groups.</span></span> <span data-ttu-id="1ff9b-211">리소스는 다른 리소스 그룹의 리소스에 계속해서 연결될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-211">Notice the resources can still be linked to resources in other resource groups.</span></span>

![계층 템플릿](./media/resource-group-overview/tier-templates.png)

<span data-ttu-id="1ff9b-213">템플릿 설계에 대한 더 많은 제안은 [Azure Resource Manager 템플릿 설계의 패턴](best-practices-resource-manager-design-templates.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-213">For more suggestions about designing your templates, see [Patterns for designing Azure Resource Manager templates](best-practices-resource-manager-design-templates.md).</span></span> <span data-ttu-id="1ff9b-214">중첩된 템플릿에 대한 자세한 내용은 [Azure Resource Manager에서 연결된 템플릿 사용](resource-group-linked-templates.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-214">For information about nested templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>

<span data-ttu-id="1ff9b-215">리소스가 올바른 순서로 생성되도록 Azure Resource Manager가 종속성을 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-215">Azure Resource Manager analyzes dependencies to ensure resources are created in the correct order.</span></span> <span data-ttu-id="1ff9b-216">한 리소스가 다른 리소스(예: 디스크에 대한 저장소 계정을 필요로 하는 가상 컴퓨터)의 값에 의존하는 경우 종속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-216">If one resource relies on a value from another resource (such as a virtual machine needing a storage account for disks), you set a dependency.</span></span> <span data-ttu-id="1ff9b-217">자세한 정보는 [Azure 리소스 관리자 템플릿에서 종속성 정의](resource-group-define-dependencies.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-217">For more information, see [Defining dependencies in Azure Resource Manager templates](resource-group-define-dependencies.md).</span></span>

<span data-ttu-id="1ff9b-218">또한 인프라의 업데이트에 대한 템플릿을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-218">You can also use the template for updates to the infrastructure.</span></span> <span data-ttu-id="1ff9b-219">예를 들어 솔루션에 리소스를 추가할 수 있으며 이미 배포된 리소스에 대한 구성 규칙을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-219">For example, you can add a resource to your solution and add configuration rules for the resources that are already deployed.</span></span> <span data-ttu-id="1ff9b-220">템플릿에서 리소스 만들기를 지정하지만 해당 리소스가 이미 존재하는 경우 Azure Resource Manager는 새 자산을 만드는 대신 업데이트를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-220">If the template specifies creating a resource but that resource already exists, Azure Resource Manager performs an update instead of creating a new asset.</span></span> <span data-ttu-id="1ff9b-221">Azure 리소스 관리자는 새 것과 동일한 상태로 기존 자산을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-221">Azure Resource Manager updates the existing asset to the same state as it would be as new.</span></span>  

<span data-ttu-id="1ff9b-222">리소스 관리자는 설치에 포함되지 않은 특정 소프트웨어를 설치하는 등의 추가 작업을 할 때 시나리오에 대한 확장을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-222">Resource Manager provides extensions for scenarios when you need additional operations such as installing particular software that is not included in the setup.</span></span> <span data-ttu-id="1ff9b-223">DSC, Chef 또는 Puppet와 같은 구성 관리 서비스를 이미 사용 중인 경우 확장을 사용하여 해당 서비스로 작업을 계속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-223">If you are already using a configuration management service, like DSC, Chef or Puppet, you can continue working with that service by using extensions.</span></span> <span data-ttu-id="1ff9b-224">가상 컴퓨터 확장에 대한 자세한 내용은 [가상 컴퓨터 확장 및 기능 정보](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-224">For information about virtual machine extensions, see [About virtual machine extensions and features](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="1ff9b-225">마지막으로 템플릿은 앱에 대한 소스 코드의 일부가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-225">Finally, the template becomes part of the source code for your app.</span></span> <span data-ttu-id="1ff9b-226">소스 코드 리포지토리를 확인하고 앱이 발전하면 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-226">You can check it in to your source code repository and update it as your app evolves.</span></span> <span data-ttu-id="1ff9b-227">Visual Studio를 통해 템플릿을 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-227">You can edit the template through Visual Studio.</span></span>

<span data-ttu-id="1ff9b-228">템플릿을 정의하면 Azure에 리소스를 배포할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-228">After defining your template, you are ready to deploy the resources to Azure.</span></span> <span data-ttu-id="1ff9b-229">리소스를 배포하는 명령은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-229">For the commands to deploy the resources, see:</span></span>

* [<span data-ttu-id="1ff9b-230">Resource Manager 템플릿과 Azure PowerShell로 리소스 배포</span><span class="sxs-lookup"><span data-stu-id="1ff9b-230">Deploy resources with Resource Manager templates and Azure PowerShell</span></span>](resource-group-template-deploy.md)
* [<span data-ttu-id="1ff9b-231">Resource Manager 템플릿과 Azure CLI로 리소스 배포</span><span class="sxs-lookup"><span data-stu-id="1ff9b-231">Deploy resources with Resource Manager templates and Azure CLI</span></span>](resource-group-template-deploy-cli.md)
* [<span data-ttu-id="1ff9b-232">Resource Manager 템플릿과 Azure Portal로 리소스 배포</span><span class="sxs-lookup"><span data-stu-id="1ff9b-232">Deploy resources with Resource Manager templates and Azure portal</span></span>](resource-group-template-deploy-portal.md)
* [<span data-ttu-id="1ff9b-233">Resource Manager 템플릿과 Resource Manager REST API로 리소스 배포</span><span class="sxs-lookup"><span data-stu-id="1ff9b-233">Deploy resources with Resource Manager templates and Resource Manager REST API</span></span>](resource-group-template-deploy-rest.md)

## <a name="tags"></a><span data-ttu-id="1ff9b-234">태그들</span><span class="sxs-lookup"><span data-stu-id="1ff9b-234">Tags</span></span>
<span data-ttu-id="1ff9b-235">리소스 관리자는 관리 또는 청구에 대한 요구 사항에 따라 리소스를 분류할 수 있는 태그 지정 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-235">Resource Manager provides a tagging feature that enables you to categorize resources according to your requirements for managing or billing.</span></span> <span data-ttu-id="1ff9b-236">리소스 그룹 및 리소스의 복잡한 컬렉션이 있고 해당 자산을 사용자에게 가장 적합한 방식으로 시각화할 필요가 있을 때 태그를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-236">Use tags when you have a complex collection of resource groups and resources, and need to visualize those assets in the way that makes the most sense to you.</span></span> <span data-ttu-id="1ff9b-237">예를 들어 조직에서 비슷한 역할을 제공하거나 동일한 부서에 속한 리소스를 태그로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-237">For example, you could tag resources that serve a similar role in your organization or belong to the same department.</span></span> <span data-ttu-id="1ff9b-238">조직의 사용자는 태그 없이 나중에 식별하고 관리하기 어려울 수 있는 여러 리소스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-238">Without tags, users in your organization can create multiple resources that may be difficult to later identify and manage.</span></span> <span data-ttu-id="1ff9b-239">예를 들어 특정 프로젝트에 대한 모든 리소스를 삭제하려고 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-239">For example, you may wish to delete all the resources for a particular project.</span></span> <span data-ttu-id="1ff9b-240">해당 리소스가 프로젝트에 대해 태그가 지정되지 않은 경우 수동으로 찾아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-240">If those resources are not tagged for the project, you have to manually find them.</span></span> <span data-ttu-id="1ff9b-241">태그를 지정하는 작업은 구독에서 불필요한 비용을 줄일 수 있는 좋은 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-241">Tagging can be an important way for you to reduce unnecessary costs in your subscription.</span></span> 

<span data-ttu-id="1ff9b-242">리소스는 태그를 공유하는 동일한 리소스 그룹에 있을 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-242">Resources do not need to reside in the same resource group to share a tag.</span></span> <span data-ttu-id="1ff9b-243">조직의 모든 사용자가 실수로 약간 다른 태그 (예: "dept" 대신 "department")를 적용하지 않고 일반 태그를 사용하는지 확인하려면 사용자 고유의 태그 분류를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-243">You can create your own tag taxonomy to ensure that all users in your organization use common tags rather than users inadvertently applying slightly different tags (such as "dept" instead of "department").</span></span>

<span data-ttu-id="1ff9b-244">다음 예제에서는 가상 컴퓨터에 적용된 태그를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-244">The following example shows a tag applied to a virtual machine.</span></span>

```json
"resources": [    
  {
    "type": "Microsoft.Compute/virtualMachines",
    "apiVersion": "2015-06-15",
    "name": "SimpleWindowsVM",
    "location": "[resourceGroup().location]",
    "tags": {
        "costCenter": "Finance"
    },
    ...
  }
]
```

<span data-ttu-id="1ff9b-245">태그 값을 사용하는 모든 리소스를 검색하려면 다음 PowerShell cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-245">To retrieve all the resources with a tag value, use the following PowerShell cmdlet:</span></span>

```powershell
Find-AzureRmResource -TagName costCenter -TagValue Finance
```

<span data-ttu-id="1ff9b-246">또는 다음 Azure CLI 2.0 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-246">Or, the following Azure CLI 2.0 command:</span></span>

```azurecli
az resource list --tag costCenter=Finance
```

<span data-ttu-id="1ff9b-247">Azure Portal을 통해 태그가 지정된 리소스를 볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-247">You can also view tagged resources through the Azure portal.</span></span>

<span data-ttu-id="1ff9b-248">구독에 대한 [사용 현황 보고서](../billing/billing-understand-your-bill.md)는 태그 이름 및 값을 포함하며 이를 통해 태그별 비용을 알아낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-248">The [usage report](../billing/billing-understand-your-bill.md) for your subscription includes tag names and values, which enables you to break out costs by tags.</span></span> <span data-ttu-id="1ff9b-249">태그에 대한 자세한 내용은 [태그를 사용하여 Azure 리소스 구성](resource-group-using-tags.md)을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-249">For more information about tags, see [Using tags to organize your Azure resources](resource-group-using-tags.md).</span></span>

## <a name="access-control"></a><span data-ttu-id="1ff9b-250">Access Control</span><span class="sxs-lookup"><span data-stu-id="1ff9b-250">Access control</span></span>
<span data-ttu-id="1ff9b-251">리소스 관리자를 사용하면 조직에 대한 특정 작업에 액세스하는 사람을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-251">Resource Manager enables you to control who has access to specific actions for your organization.</span></span> <span data-ttu-id="1ff9b-252">고유하게 관리 플랫폼으로 RBAC(역할 기반 Access Control)를 통합하고 해당 Access Control를 리소스 그룹에서 모든 서비스에 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-252">It natively integrates role-based access control (RBAC) into the management platform and applies that access control to all services in your resource group.</span></span> 

<span data-ttu-id="1ff9b-253">역할 기반 Access Control로 작업하는 경우를 이해하기 위한 두 가지 주요 개념이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-253">There are two main concepts to understand when working with role-based access control:</span></span>

* <span data-ttu-id="1ff9b-254">역할 정의 - 사용 권한 집합을 설명하고 여러 할당에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-254">Role definitions - describe a set of permissions and can be used in many assignments.</span></span>
* <span data-ttu-id="1ff9b-255">역할 할당 - 특정 범위(구독, 리소스 그룹 또는 리소스)에 대한 ID(사용자 또는 그룹)로 정의를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-255">Role assignments - associate a definition with an identity (user or group) for a particular scope (subscription, resource group, or resource).</span></span> <span data-ttu-id="1ff9b-256">할당은 더 낮은 범위로 상속됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-256">The assignment is inherited by lower scopes.</span></span>

<span data-ttu-id="1ff9b-257">미리 정의된 플랫폼 및 리소스 특정 역할에 사용자를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-257">You can add users to pre-defined platform and resource-specific roles.</span></span> <span data-ttu-id="1ff9b-258">예를 들어 사용자가 리소스를 변경하지 않고 보도록 허용하는 읽기 권한자를 호출하는 미리 정의된 역할의 장점을 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-258">For example, you can take advantage of the pre-defined role called Reader that permits users to view resources but not change them.</span></span> <span data-ttu-id="1ff9b-259">이 유형의 액세스를 필요로 하는 조직의 사용자를 읽기 권한자 역할에 추가하고 구독, 리소스 그룹 또는 리소스에 역할을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-259">You add users in your organization that need this type of access to the Reader role and apply the role to the subscription, resource group, or resource.</span></span>

<span data-ttu-id="1ff9b-260">Azure는 다음 4개의 플랫폼 역할을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-260">Azure provides the following four platform roles:</span></span>

1. <span data-ttu-id="1ff9b-261">소유자는 액세스를 제외한 모든 것을 관리할 수 있음</span><span class="sxs-lookup"><span data-stu-id="1ff9b-261">Owner - can manage everything, including access</span></span>
2. <span data-ttu-id="1ff9b-262">참여자는 액세스를 제외한 모든 것을 관리할 수 있음</span><span class="sxs-lookup"><span data-stu-id="1ff9b-262">Contributor - can manage everything except access</span></span>
3. <span data-ttu-id="1ff9b-263">읽기 권한자는 모든 항목을 볼 수 있지만 변경할 수 없음</span><span class="sxs-lookup"><span data-stu-id="1ff9b-263">Reader - can view everything, but can't make changes</span></span>
4. <span data-ttu-id="1ff9b-264">사용자 액세스 관리자는 Azure 리소스에 대한 사용자 액세스를 관리할 수 있음</span><span class="sxs-lookup"><span data-stu-id="1ff9b-264">User Access Administrator - can manage user access to Azure resources</span></span>

<span data-ttu-id="1ff9b-265">Azure는 몇 가지 리소스 특정 역할도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-265">Azure also provides several resource-specific roles.</span></span> <span data-ttu-id="1ff9b-266">몇 가지 일반적인 경우는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-266">Some common ones are:</span></span>

1. <span data-ttu-id="1ff9b-267">가상 컴퓨터 참여자는 가상 컴퓨터를 관리할 수 있지만 그에 대한 액세스 권한을 부여할 수 없고 연결된 가상 네트워크 또는 저장소 계정을 관리할 수 없음</span><span class="sxs-lookup"><span data-stu-id="1ff9b-267">Virtual Machine Contributor - can manage virtual machines but not grant access to them, and cannot manage the virtual network or storage account to which they are connected</span></span>
2. <span data-ttu-id="1ff9b-268">네트워크 참여자는 모든 네트워크 리소스를 관리할 수 있지만 그에 대한 액세스 권한을 부여할 수 없음</span><span class="sxs-lookup"><span data-stu-id="1ff9b-268">Network Contributor - can manage all network resources, but not grant access to them</span></span>
3. <span data-ttu-id="1ff9b-269">저장소 계정 참여자는 저장소 계정을 관리할 수 있지만 그에 대한 액세스 권한을 부여할 수 없음</span><span class="sxs-lookup"><span data-stu-id="1ff9b-269">Storage Account Contributor - Can manage storage accounts, but not grant access to them</span></span>
4. <span data-ttu-id="1ff9b-270">SQL Server 참여자는 해당 보안 관련 정책을 제외한 SQL 서버 및 데이터베이스를 관리할 수 있음</span><span class="sxs-lookup"><span data-stu-id="1ff9b-270">SQL Server Contributor - Can manage SQL servers and databases, but not their security-related policies</span></span>
5. <span data-ttu-id="1ff9b-271">웹 사이트 참여자는 웹 사이트를 관리할 수 있으나 여기에 연결된 웹 계획은 관리할 수 없음</span><span class="sxs-lookup"><span data-stu-id="1ff9b-271">Website Contributor - Can manage websites, but not the web plans to which they are connected</span></span>

<span data-ttu-id="1ff9b-272">역할 및 허용되는 작업의 전체 목록은 [RBAC: 기본 제공 역할](../active-directory/role-based-access-built-in-roles.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-272">For the full list of roles and permitted actions, see [RBAC: Built in Roles](../active-directory/role-based-access-built-in-roles.md).</span></span> <span data-ttu-id="1ff9b-273">역할 기반 Access Control에 대한 자세한 내용은 [Azure 역할 기반 Access Control](../active-directory/role-based-access-control-configure.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-273">For more information about role-based access control, see [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).</span></span> 

<span data-ttu-id="1ff9b-274">경우에 따라 리소스에 액세스하는 코드 또는 스크립트를 실행하려고 하지만 사용자의 자격 증명으로 실행하지 않으려 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-274">In some cases, you want to run code or script that accesses resources, but you do not want to run it under a user’s credentials.</span></span> <span data-ttu-id="1ff9b-275">대신, 응용 프로그램에 대한 서비스 주체를 호출하는 ID를 만들고 서비스 주체에 대한 적절한 역할을 할당하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-275">Instead, you want to create an identity called a service principal for the application and assign the appropriate role for the service principal.</span></span> <span data-ttu-id="1ff9b-276">Resource Manager를 사용하면 응용 프로그램에 대한 자격 증명을 만들고 프로그래밍 방식으로 응용 프로그램을 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-276">Resource Manager enables you to create credentials for the application and programmatically authenticate the application.</span></span> <span data-ttu-id="1ff9b-277">서비스 주체를 만드는 방법에 대해 알아보려면 다음 항목 중 하나를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-277">To learn about creating service principals, see one of following topics:</span></span>

* [<span data-ttu-id="1ff9b-278">Azure PowerShell을 사용하여 리소스에 액세스하는 서비스 주체 만들기</span><span class="sxs-lookup"><span data-stu-id="1ff9b-278">Use Azure PowerShell to create a service principal to access resources</span></span>](resource-group-authenticate-service-principal.md)
* [<span data-ttu-id="1ff9b-279">Azure CLI를 사용하여 리소스에 액세스하는 서비스 주체 만들기</span><span class="sxs-lookup"><span data-stu-id="1ff9b-279">Use Azure CLI to create a service principal to access resources</span></span>](resource-group-authenticate-service-principal-cli.md)
* [<span data-ttu-id="1ff9b-280">포털을 사용하여 리소스에 액세스할 수 있는 Azure Active Directory 응용 프로그램 및 서비스 주체 만들기</span><span class="sxs-lookup"><span data-stu-id="1ff9b-280">Use portal to create Azure Active Directory application and service principal that can access resources</span></span>](resource-group-create-service-principal-portal.md)

<span data-ttu-id="1ff9b-281">또한 사용자가 삭제 및 수정하는 것을 방지하기 위해 명시적으로 중요한 리소스를 잠글 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-281">You can also explicitly lock critical resources to prevent users from deleting or modifying them.</span></span> <span data-ttu-id="1ff9b-282">자세한 내용은 [Azure 리소스 관리자를 사용하여 리소스 잠그기](resource-group-lock-resources.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-282">For more information, see [Lock resources with Azure Resource Manager](resource-group-lock-resources.md).</span></span>

## <a name="activity-logs"></a><span data-ttu-id="1ff9b-283">활동 로그</span><span class="sxs-lookup"><span data-stu-id="1ff9b-283">Activity logs</span></span>
<span data-ttu-id="1ff9b-284">Resource Manager는 리소스를 만들거나 수정 또는 삭제하는 모든 작업을 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-284">Resource Manager logs all operations that create, modify, or delete a resource.</span></span> <span data-ttu-id="1ff9b-285">활동 로그를 사용하여 문제를 해결할 때 오류를 찾거나 조직의 사용자가 리소스를 수정한 방법을 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-285">You can use the activity logs to find an error when troubleshooting or to monitor how a user in your organization modified a resource.</span></span> <span data-ttu-id="1ff9b-286">로그를 보려면 리소스 그룹에 대한 **설정** 블레이드에서 **활동 로그**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-286">To see the logs, select **Activity logs** in the **Settings** blade for a resource group.</span></span> <span data-ttu-id="1ff9b-287">작업을 시작한 사용자를 포함하여 여러 다른 값으로 로그를 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-287">You can filter the logs by many different values including which user initiated the operation.</span></span> <span data-ttu-id="1ff9b-288">활동 로그 작업에 대한 내용은 [Azure 리소스 관리를 위한 활동 로그 보기](resource-group-audit.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-288">For information about working with the activity logs, see [View activity logs to manage Azure resources](resource-group-audit.md).</span></span>

## <a name="customized-policies"></a><span data-ttu-id="1ff9b-289">사용자 지정된 정책</span><span class="sxs-lookup"><span data-stu-id="1ff9b-289">Customized policies</span></span>
<span data-ttu-id="1ff9b-290">리소스 관리자를 사용하면 리소스를 관리하기 위해 사용자 지정된 정책을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-290">Resource Manager enables you to create customized policies for managing your resources.</span></span> <span data-ttu-id="1ff9b-291">만든 정책의 유형에는 다양한 시나리오가 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-291">The types of policies you create can include diverse scenarios.</span></span> <span data-ttu-id="1ff9b-292">리소스에 대한 명명 규칙을 적용하거나 배포할 수 있는 리소스의 형식 및 인스턴스를 제한하거나 리소스 종류를 호스트할 수 있는 지역을 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-292">You can enforce a naming convention on resources, limit which types and instances of resources can be deployed, or limit which regions can host a type of resource.</span></span> <span data-ttu-id="1ff9b-293">부서별로 청구를 구성하기 위해 리소스에 대한 태그 값이 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-293">You can require a tag value on resources to organize billing by departments.</span></span> <span data-ttu-id="1ff9b-294">구독에서 비용을 절감하고 일관성을 유지하는 데 도움이 되는 정책을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-294">You create policies to help reduce costs and maintain consistency in your subscription.</span></span> 

<span data-ttu-id="1ff9b-295">JSON을 사용하여 정책을 정의하고 구독 전체 또는 리소스 그룹 내에서 해당 정책을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-295">You define policies with JSON and then apply those policies either across your subscription or within a resource group.</span></span> <span data-ttu-id="1ff9b-296">정책은 리소스 유형에 적용되기 때문에 역할 기반 Access Control와 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-296">Policies are different than role-based access control because they are applied to resource types.</span></span>

<span data-ttu-id="1ff9b-297">다음 예제에서는 모든 리소스에 costCenter 태그가 포함되는지를 지정하여 태그 일관성을 보장하는 정책을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-297">The following example shows a policy that ensures tag consistency by specifying that all resources include a costCenter tag.</span></span>

```json
{
  "if": {
    "not" : {
      "field" : "tags",
      "containsKey" : "costCenter"
    }
  },
  "then" : {
    "effect" : "deny"
  }
}
```

<span data-ttu-id="1ff9b-298">더 다양한 유형의 정책을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-298">There are many more types of policies you can create.</span></span> <span data-ttu-id="1ff9b-299">자세한 내용은 [정책을 사용하여 리소스 및 컨트롤 액세스 관리](resource-manager-policy.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-299">For more information, see [Use Policy to manage resources and control access](resource-manager-policy.md).</span></span>

## <a name="sdks"></a><span data-ttu-id="1ff9b-300">SDK</span><span class="sxs-lookup"><span data-stu-id="1ff9b-300">SDKs</span></span>
<span data-ttu-id="1ff9b-301">Azure SDK는 여러 언어 및 플랫폼에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-301">Azure SDKs are available for multiple languages and platforms.</span></span> <span data-ttu-id="1ff9b-302">이러한 언어 구현은 각각 해당 에코 시스템 패키지 관리자 및 GitHub를 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-302">Each of these language implementations is available through its ecosystem package manager and GitHub.</span></span>

<span data-ttu-id="1ff9b-303">다음은 오픈 소스 SDK 리포지토리입니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-303">Here are our Open Source SDK repositories.</span></span> <span data-ttu-id="1ff9b-304">피드백, 문제 및 끌어오기 요청을 환영합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-304">We welcome feedback, issues, and pull requests.</span></span>

* [<span data-ttu-id="1ff9b-305">Azure SDK for .NET</span><span class="sxs-lookup"><span data-stu-id="1ff9b-305">Azure SDK for .NET</span></span>](https://github.com/Azure/azure-sdk-for-net)
* [<span data-ttu-id="1ff9b-306">Java용 Azure 관리 라이브러리</span><span class="sxs-lookup"><span data-stu-id="1ff9b-306">Azure Management Libraries for Java</span></span>](https://github.com/Azure/azure-sdk-for-java)
* [<span data-ttu-id="1ff9b-307">Node.js용 Azure SDK</span><span class="sxs-lookup"><span data-stu-id="1ff9b-307">Azure SDK for Node.js</span></span>](https://github.com/Azure/azure-sdk-for-node)
* [<span data-ttu-id="1ff9b-308">PHP용 Azure SDK</span><span class="sxs-lookup"><span data-stu-id="1ff9b-308">Azure SDK for PHP</span></span>](https://github.com/Azure/azure-sdk-for-php)
* [<span data-ttu-id="1ff9b-309">Python용 Azure SDK</span><span class="sxs-lookup"><span data-stu-id="1ff9b-309">Azure SDK for Python</span></span>](https://github.com/Azure/azure-sdk-for-python)
* [<span data-ttu-id="1ff9b-310">Ruby용 Azure SDK</span><span class="sxs-lookup"><span data-stu-id="1ff9b-310">Azure SDK for Ruby</span></span>](https://github.com/Azure/azure-sdk-for-ruby)

<span data-ttu-id="1ff9b-311">사용자 리소스에서 이러한 언어를 사용하는 방법에 대한 정보는 다음을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-311">For information about using these languages with your resources, see:</span></span>

* [<span data-ttu-id="1ff9b-312">.NET 개발자용 Azure</span><span class="sxs-lookup"><span data-stu-id="1ff9b-312">Azure for .NET developers</span></span>](/dotnet/azure/?view=azure-dotnet)
* [<span data-ttu-id="1ff9b-313">Java 개발자용 Azure</span><span class="sxs-lookup"><span data-stu-id="1ff9b-313">Azure for Java developers</span></span>](/java/azure/)
* [<span data-ttu-id="1ff9b-314">Node.js 개발자용 Azure</span><span class="sxs-lookup"><span data-stu-id="1ff9b-314">Azure for Node.js developers</span></span>](/nodejs/azure/)
* [<span data-ttu-id="1ff9b-315">Python 개발자용 Azure</span><span class="sxs-lookup"><span data-stu-id="1ff9b-315">Azure for Python developers</span></span>](/python/azure/)

> [!NOTE]
> <span data-ttu-id="1ff9b-316">SDK가 필요한 기능을 제공하지 않는 경우 [Azure REST API](https://docs.microsoft.com/rest/api/resources/)에 직접 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-316">If the SDK doesn't provide the required functionality, you can also call to the [Azure REST API](https://docs.microsoft.com/rest/api/resources/) directly.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="1ff9b-317">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1ff9b-317">Next steps</span></span>
* <span data-ttu-id="1ff9b-318">템플릿으로 작업하는 방법에 대한 간단한 소개는 [기존 리소스에서 Azure Resource Manager 템플릿 내보내기](resource-manager-export-template.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-318">For a simple introduction to working with templates, see [Export an Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>
* <span data-ttu-id="1ff9b-319">템플릿을 만드는 자세한 연습은 [첫 번째 Azure Resource Manager 템플릿 만들기](resource-manager-create-first-template.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-319">For a more thorough walkthrough of creating a template, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>
* <span data-ttu-id="1ff9b-320">템플릿에서 사용할 수 있는 함수를 이해하려면 [템플릿 함수](resource-group-template-functions.md)</span><span class="sxs-lookup"><span data-stu-id="1ff9b-320">To understand the functions you can use in a template, see [Template functions](resource-group-template-functions.md)</span></span>
* <span data-ttu-id="1ff9b-321">Resource Manager로 Visual Studio를 사용하는 방법에 대한 정보는 [Visual Studio를 통해 Azure 리소스 그룹 생성 및 배포](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-321">For information about using Visual Studio with Resource Manager, see [Creating and deploying Azure resource groups through Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span></span>

<span data-ttu-id="1ff9b-322">이 개요에 대한 비디오 데모는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff9b-322">Here's a video demonstration of this overview:</span></span>

>[!VIDEO https://channel9.msdn.com/Blogs/Azure-Documentation-Shorts/Azure-Resource-Manager-Overview/player]


[powershellref]: https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.2.0/azurerm.resources
