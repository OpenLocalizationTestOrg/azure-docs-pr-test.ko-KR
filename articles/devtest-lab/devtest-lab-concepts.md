---
title: "DevTest Labs 개념 | Microsoft 문서"
description: "DevTest Lab의 기본 개념과 Azure 가상 컴퓨터를 쉽게 만들고 관리하고 모니터링할 수 있는 방법 알아보기"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 105919e8-3617-4ce3-a29f-a289fa608fb2
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/25/2016
ms.author: tarcher
ms.openlocfilehash: 1caea59e71126e934e2e52a1ad7f533ffa7d4b03
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="devtest-labs-concepts"></a><span data-ttu-id="c58d1-103">DevTest Lab 개념</span><span class="sxs-lookup"><span data-stu-id="c58d1-103">DevTest Labs concepts</span></span>
## <a name="overview"></a><span data-ttu-id="c58d1-104">개요</span><span class="sxs-lookup"><span data-stu-id="c58d1-104">Overview</span></span>
<span data-ttu-id="c58d1-105">다음은 DevTest Lab 개념 및 정의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="c58d1-105">The following list contains key DevTest Labs concepts and definitions:</span></span>

## <a name="labs"></a><span data-ttu-id="c58d1-106">랩</span><span class="sxs-lookup"><span data-stu-id="c58d1-106">Labs</span></span>
<span data-ttu-id="c58d1-107">랩은 VM(Virtual Machines)과 같은 리소스 그룹을 포함하는 인프라로서, 이를 통해 한도 및 할당량을 지정하여 해당 리소스를 더 잘 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c58d1-107">A lab is the infrastructure that encompasses a group of resources, such as Virtual Machines (VMs), that lets you better manage those resources by specifying limits and quotas.</span></span>

## <a name="virtual-machine"></a><span data-ttu-id="c58d1-108">가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="c58d1-108">Virtual machine</span></span>
<span data-ttu-id="c58d1-109">Azure VM은 Azure에서 제공하는 여러 유형의 [확장성 있는 주문형 컴퓨팅 리소스](https://docs.microsoft.com/azure/app-service-web/choose-web-site-cloud-service-vm) 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="c58d1-109">An Azure VM is one of several types of [on-demand, scalable computing resources](https://docs.microsoft.com/azure/app-service-web/choose-web-site-cloud-service-vm) that Azure offers.</span></span> <span data-ttu-id="c58d1-110">Azure VM은 VM을 실행하는 실제 하드웨어를 구입 및 유지 관리할 필요가 없는 가상화의 유연성을 제공합니다. 하지만 VM에서 실행하는 소프트웨어의 구성, 패치 및 설치와 같은 특정 작업을 수행하여 VM을 계속 유지 관리할 필요가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c58d1-110">Azure VMs give you the flexibility of virtualization without having to buy and maintain the physical hardware that runs it, although you still need to maintain the VM by performing certain tasks, such as configuring, patching, and installing the software that runs on it.</span></span>

<span data-ttu-id="c58d1-111">[Azure에서의 Windows 가상 컴퓨터 개요](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-overview)에서는 VM을 만들기 전에 고려해야 하는 요구 사항, 만드는 방법 및 관리하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c58d1-111">[Overview of Windows virtual machines in Azure](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-overview) gives you information about what you should consider before you create a VM, how you create it, and how you manage it.</span></span>

## <a name="claimable-vm"></a><span data-ttu-id="c58d1-112">클레임할 수 있는 VM</span><span class="sxs-lookup"><span data-stu-id="c58d1-112">Claimable VM</span></span>
<span data-ttu-id="c58d1-113">Azure Claimable VM은 권한이 있는 랩 사용자면 누구나 사용할 수 있는 가상 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="c58d1-113">An Azure Claimable VM is a virtual machine that is available for use by any lab user with permissions.</span></span> <span data-ttu-id="c58d1-114">랩 관리자가 특정한 기본 이미지와 아티팩트를 사용하여 VM을 준비하고 공유 풀에 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c58d1-114">A lab admin can prepare VMs with specific base images and artifacts and save them to a shared pool.</span></span> <span data-ttu-id="c58d1-115">그런 다음 랩 사용자가 특정 구성이 포함된 VM이 필요할 때 풀에서 작동하는 VM을 클레임할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c58d1-115">A lab user can then claim a working VM from the pool when they need one with that specific configuration.</span></span>

<span data-ttu-id="c58d1-116">클레임할 수 있는 VM은 초기에 특정 사용자에게 할당되지 않지만 모든 사용자의 목록에 있는 "클레임할 수 있는 가상 컴퓨터"에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c58d1-116">A VM that is claimable is not initially assigned to any particular user, but will show up in every user's list under "Claimable virtual machines".</span></span> <span data-ttu-id="c58d1-117">VM이 사용자에 의해 클레임되면 해당 사용자의 “내 가상 컴퓨터” 영역으로 이동되며 더 이상 다른 사용자가 클레임할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c58d1-117">After a VM is claimed by a user, it is moved up to their "My virtual machines" area and is no longer claimable by any other user.</span></span>

## <a name="environment"></a><span data-ttu-id="c58d1-118">Environment</span><span class="sxs-lookup"><span data-stu-id="c58d1-118">Environment</span></span>
<span data-ttu-id="c58d1-119">DevTest 랩에서 환경은 랩에 있는 Azure 리소스 컬렉션을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c58d1-119">In DevTest Labs, an environment refers to a collection of Azure resources in a lab.</span></span> <span data-ttu-id="c58d1-120">[이 블로그 게시물](https://blogs.msdn.microsoft.com/devtestlab/2016/11/16/connect-2016-news-for-azure-devtest-labs-azure-resource-manager-template-based-environments-vm-auto-shutdown-and-more/)에서는 Azure Resource Manager 템플릿에서 다중 VM 환경을 만드는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c58d1-120">[This blog post](https://blogs.msdn.microsoft.com/devtestlab/2016/11/16/connect-2016-news-for-azure-devtest-labs-azure-resource-manager-template-based-environments-vm-auto-shutdown-and-more/) discusses how to create multi-VM environments from your Azure Resource Manager templates.</span></span>

## <a name="base-images"></a><span data-ttu-id="c58d1-121">기본 이미지</span><span class="sxs-lookup"><span data-stu-id="c58d1-121">Base images</span></span>
<span data-ttu-id="c58d1-122">기본 이미지는 VM을 빠르게 만들기 위해 미리 설치되고 구성된 모든 도구와 설정이 포함된 VM 이미지입니다.</span><span class="sxs-lookup"><span data-stu-id="c58d1-122">Base images are VM images with all the tools and settings preinstalled and configured to quickly create a VM.</span></span> <span data-ttu-id="c58d1-123">기존 기본 항목을 선택하고 테스트 에이전트를 설치하기 위한 아티팩트를 추가하여 VM을 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c58d1-123">You can provision a VM by picking an existing base and adding an artifact to install your test agent.</span></span> <span data-ttu-id="c58d1-124">그런 다음 프로비전된 VM을 기본으로 설정하면 프로비전된 각각의 VM에 대한 테스트 에이전트를 다시 설치하지 않고도 기본을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c58d1-124">You can then save the provisioned VM as a base so that the base can be used without having to reinstall the test agent for each provisioning of the VM.</span></span>

## <a name="artifacts"></a><span data-ttu-id="c58d1-125">아티팩트</span><span class="sxs-lookup"><span data-stu-id="c58d1-125">Artifacts</span></span>
<span data-ttu-id="c58d1-126">VM이 프로비전된 후 응용 프로그램을 배포하고 구성하기 위해 아티팩트가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c58d1-126">Artifacts are used to deploy and configure your application after a VM is provisioned.</span></span> <span data-ttu-id="c58d1-127">아티팩트는 다음과 같을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c58d1-127">Artifacts can be:</span></span>

* <span data-ttu-id="c58d1-128">VM에 설치하려는 도구(예: 에이전트, Fiddler 및 Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="c58d1-128">Tools that you want to install on the VM - such as agents, Fiddler, and Visual Studio.</span></span>
* <span data-ttu-id="c58d1-129">VM에서 실행하려는 작업(예: 리포지토리 복제)</span><span class="sxs-lookup"><span data-stu-id="c58d1-129">Actions that you want to run on the VM - such as cloning a repo.</span></span>
* <span data-ttu-id="c58d1-130">테스트하려는 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="c58d1-130">Applications that you want to test.</span></span>

<span data-ttu-id="c58d1-131">아티팩트는 배포를 수행하고 구성을 적용하기 위한 지침이 포함된 [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) JSON 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="c58d1-131">Artifacts are [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) JSON files that contain instructions to perform deployment and apply configuration.</span></span>

## <a name="artifact-repositories"></a><span data-ttu-id="c58d1-132">아티팩트 리포지토리</span><span class="sxs-lookup"><span data-stu-id="c58d1-132">Artifact repositories</span></span>
<span data-ttu-id="c58d1-133">아티팩트 리포지토리는 아티팩트가 체크 인되는 Git 리포지토리입니다.</span><span class="sxs-lookup"><span data-stu-id="c58d1-133">Artifact repositories are git repositories where artifacts are checked in.</span></span> <span data-ttu-id="c58d1-134">아티팩트 리포지토리를 조직에 있는 여러 개의 랩에 추가하면 다시 사용하거나 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c58d1-134">Artifact repositories can be added to multiple labs in your organization enabling reuse and sharing.</span></span>

## <a name="formulas"></a><span data-ttu-id="c58d1-135">수식</span><span class="sxs-lookup"><span data-stu-id="c58d1-135">Formulas</span></span>
<span data-ttu-id="c58d1-136">기본 이미지와 더불어, 수식은 신속한 VM 프로비전을 위한 메커니즘을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c58d1-136">Formulas, in addition to base images, provide a mechanism for fast VM provisioning.</span></span> <span data-ttu-id="c58d1-137">DevTest Lab에 포함된 수식은 랩 VM을 만드는 데 사용되는 기본 속성 값의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="c58d1-137">A formula in DevTest Labs is a list of default property values used to create a lab VM.</span></span>
<span data-ttu-id="c58d1-138">수식을 사용하면, 매번 같은 속성을 지정할 필요 없이, 동일한 속성(예: 기본 이미지, VM 크기, 가상 네트워크, 아티팩트) 집합을 포함하는 VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c58d1-138">With formulas, VMs with the same set of properties - such as base image, VM size, virtual network, and artifacts - can be created without needing to specify those properties each time.</span></span> <span data-ttu-id="c58d1-139">수식을 통해 VM을 만들 때, 기본값을 그대로 사용하거나 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c58d1-139">When creating a VM from a formula, the default values can be used as-is or modified.</span></span>

## <a name="policies"></a><span data-ttu-id="c58d1-140">정책</span><span class="sxs-lookup"><span data-stu-id="c58d1-140">Policies</span></span>
<span data-ttu-id="c58d1-141">정책은 랩에서의 비용 제어에 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c58d1-141">Policies help in controlling cost in your lab.</span></span> <span data-ttu-id="c58d1-142">예를 들어 정의된 일정에 따라 VM이 자동으로 종료되도록 정책을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c58d1-142">For example, you can create a policy to automatically shut down VMs based on a defined schedule.</span></span>

## <a name="caps"></a><span data-ttu-id="c58d1-143">캡</span><span class="sxs-lookup"><span data-stu-id="c58d1-143">Caps</span></span>
<span data-ttu-id="c58d1-144">캡은 랩에서 낭비를 최소화하는 메커니즘입니다.</span><span class="sxs-lookup"><span data-stu-id="c58d1-144">Caps is a mechanism to minimize waste in your lab.</span></span> <span data-ttu-id="c58d1-145">예를 들어 캡을 설정하여 사용자당 또는 랩에서 만들 수 있는 VM의 수를 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c58d1-145">For example, you can set a cap to restrict the number of VMs that can be created per user, or in a lab.</span></span>

## <a name="security-levels"></a><span data-ttu-id="c58d1-146">보안 수준</span><span class="sxs-lookup"><span data-stu-id="c58d1-146">Security levels</span></span>
<span data-ttu-id="c58d1-147">보안 액세스는 Azure 역할 기반 액세스 제어(RBAC)를 통해 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="c58d1-147">Security access is determined by Azure Role-Based Access Control (RBAC).</span></span> <span data-ttu-id="c58d1-148">액세스의 작동 방식을 이해하기 위해 RBAC에 의해 정의된 대로 사용 권한, 역할 및 범위 사이의 차이점을 이해하는 데 도움을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c58d1-148">To understand how access works, it helps to understand the differences between a permission, a role, and a scope as defined by RBAC.</span></span>

* <span data-ttu-id="c58d1-149">사용 권한 - 특정 작업에 대해 정의된 액세스입니다(예: 모든 가상 컴퓨터에 대한 읽기 액세스).</span><span class="sxs-lookup"><span data-stu-id="c58d1-149">Permission - A permission is a defined access to a specific action (e.g. read-access to all virtual machines).</span></span>
* <span data-ttu-id="c58d1-150">역할 - 그룹화되고 사용자에게 할당될 수 있는 사용 권한의 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="c58d1-150">Role - A role is a set of permissions that can be grouped and assigned to a user.</span></span> <span data-ttu-id="c58d1-151">예를 들어 *구독 소유자* 역할은 구독 내의 모든 리소스에 대한 액세스를 보유합니다.</span><span class="sxs-lookup"><span data-stu-id="c58d1-151">For example, the *subscription owner* role has access to all resources within a subscription.</span></span>
* <span data-ttu-id="c58d1-152">범위 - Azure 리소스의 계층 구조 내 수준입니다(예: 리소스 그룹, 단일 랩 또는 전체 구독).</span><span class="sxs-lookup"><span data-stu-id="c58d1-152">Scope - A scope is a level within the hierarchy of an Azure resource, such as a resource group, a single lab, or the entire subscription.</span></span>

<span data-ttu-id="c58d1-153">DevTest Labs의 범위 내에 사용자 사용 권한을 정의하는 두 가지 유형의 역할(랩 소유자 및 랩 사용자)이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c58d1-153">Within the scope of DevTest Labs, there are two types of roles to define user permissions: lab owner and lab user.</span></span>

* <span data-ttu-id="c58d1-154">랩 소유자 - 랩 소유자는 랩 내의 모든 리소스에 대한 액세스 권한을 보유합니다.</span><span class="sxs-lookup"><span data-stu-id="c58d1-154">Lab Owner - A lab owner has access to any resources within the lab.</span></span> <span data-ttu-id="c58d1-155">따라서 랩 소유자는 정책을 수정하고 VM을 읽고 쓰고, 가상 네트워크를 변경하는 등의 작업을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c58d1-155">Therefore, a lab owner can modify policies, read and write any VMs, change the virtual network, and so on.</span></span>
* <span data-ttu-id="c58d1-156">랩 사용자 - 랩 사용자는 VM, 정책 및 가상 네트워크와 같은 모든 랩 리소스를 볼 수 있지만 정책 또는 다른 사용자가 만든 VM을 수정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c58d1-156">Lab User - A lab user can view all lab resources, such as VMs, policies, and virtual networks, but cannot modify policies or any VMs created by other users.</span></span>

<span data-ttu-id="c58d1-157">DevTest Lab에서 사용자 지정 역할을 만드는 방법을 보려면 [특정 랩 정책에 사용자 권한 부여](devtest-lab-grant-user-permissions-to-specific-lab-policies.md)문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c58d1-157">To see how to create custom roles in DevTest Labs, refer to the article, [Grant user permissions to specific lab policies](devtest-lab-grant-user-permissions-to-specific-lab-policies.md).</span></span>

<span data-ttu-id="c58d1-158">범위는 계층적이므로 사용자가 특정 범위에서 사용 권한을 가진 경우 포함된 모든 하위 수준 범위에서 해당 사용 권한이 자동으로 부여됩니다.</span><span class="sxs-lookup"><span data-stu-id="c58d1-158">Since scopes are hierarchical, when a user has permissions at a certain scope, they are automatically granted those permissions at every lower-level scope encompassed.</span></span> <span data-ttu-id="c58d1-159">예를 들어 사용자가 구독 소유자의 역할에 할당되면 모든 가상 컴퓨터, 모든 가상 네트워크 및 모든 랩을 포함하는 구독의 모든 리소스에 대한 액세스를 가집니다.</span><span class="sxs-lookup"><span data-stu-id="c58d1-159">For instance, if a user is assigned to the role of subscription owner, then they have access to all resources in a subscription, which include all virtual machines, all virtual networks, and all labs.</span></span> <span data-ttu-id="c58d1-160">따라서 구독 소유자는 자동으로 랩 소유자의 역할을 상속합니다.</span><span class="sxs-lookup"><span data-stu-id="c58d1-160">Therefore, a subscription owner automatically inherits the role of lab owner.</span></span> <span data-ttu-id="c58d1-161">그러나 반대의 경우는 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c58d1-161">However, the opposite is not true.</span></span> <span data-ttu-id="c58d1-162">랩 소유자는 구독 수준보다 낮은 범위인 랩에 대한 액세스를 가집니다.</span><span class="sxs-lookup"><span data-stu-id="c58d1-162">A lab owner has access to a lab, which is a lower scope than the subscription level.</span></span> <span data-ttu-id="c58d1-163">따라서 랩 소유자는 랩 외부에 있는 가상 컴퓨터 또는 가상 네트워크 또는 리소스를 볼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c58d1-163">Therefore, a lab owner will not be able to see virtual machines or virtual networks or any resources that are outside of the lab.</span></span>

## <a name="azure-resource-manager-templates"></a><span data-ttu-id="c58d1-164">Azure 리소스 관리자 템플릿</span><span class="sxs-lookup"><span data-stu-id="c58d1-164">Azure Resource Manager templates</span></span>
<span data-ttu-id="c58d1-165">이 문서에 설명된 모든 개념은 Azure Resource Manager 템플릿을 사용하여 구성할 수 있습니다. 이러한 템플릿에서는 Azure 솔루션의 인프라/구성을 정의하고 반복적으로 일관된 상태로 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c58d1-165">All of the concepts discussed in this article can be configured by using Azure Resource Manager templates, which let you define the infrastructure/configuration of your Azure solution and repeatedly deploy it in a consistent state.</span></span>

<span data-ttu-id="c58d1-166">[Azure Resource Manager 템플릿의 구조 및 구문 이해](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authoring-templates#template-format)에서는 Azure Resource Manager 템플릿의 구조 및 템플릿의 여러 섹션에서 사용 가능한 속성을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c58d1-166">[Understand the structure and syntax of Azure Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authoring-templates#template-format) describes the structure of an Azure Resource Manager template and the properties that are available in the different sections of a template.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="c58d1-167">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c58d1-167">Next steps</span></span>
[<span data-ttu-id="c58d1-168">DevTest Lab에서 랩 만들기</span><span class="sxs-lookup"><span data-stu-id="c58d1-168">Create a lab in DevTest Labs</span></span>](devtest-lab-create-lab.md)
