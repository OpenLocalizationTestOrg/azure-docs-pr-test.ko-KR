---
title: "Azure 인프라 명명 지침 - Linux | Microsoft Docs"
description: "Azure 인프라 서비스에서 이름을 지정하기 위한 핵심 디자인 및 구현 지침에 대해 알아봅니다."
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 18ee4fb1-8297-49a1-8d3f-097880be67c7
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1b086f0972c02d569a7219820a3d596960b6014b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-infrastructure-naming-guidelines-for-linux-vms"></a><span data-ttu-id="ebdbc-103">Linux VM에 대한 Azure 인프라 명명 지침</span><span class="sxs-lookup"><span data-stu-id="ebdbc-103">Azure infrastructure naming guidelines for Linux VMs</span></span> 

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

<span data-ttu-id="ebdbc-104">이 문서에서는 작업 환경 전반에 걸쳐 논리적이며 쉽게 식별할 수 있는 리소스 집합을 작성할 수 있도록 다양한 Azure 리소스 전체에 명명 규칙을 적용하는 방식을 중점적으로 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="ebdbc-104">This article focuses on understanding how to approach naming conventions for all your various Azure resources to build a logical and easily identifiable set of resources across your environment.</span></span>

## <a name="implementation-guidelines-for-naming-conventions"></a><span data-ttu-id="ebdbc-105">명명 규칙에 대한 구현 지침</span><span class="sxs-lookup"><span data-stu-id="ebdbc-105">Implementation guidelines for naming conventions</span></span>
<span data-ttu-id="ebdbc-106">의사 결정:</span><span class="sxs-lookup"><span data-stu-id="ebdbc-106">Decisions:</span></span>

* <span data-ttu-id="ebdbc-107">Azure 리소스에 대한 명명 규칙은 무엇인가?</span><span class="sxs-lookup"><span data-stu-id="ebdbc-107">What are your naming conventions for Azure resources?</span></span>

<span data-ttu-id="ebdbc-108">작업:</span><span class="sxs-lookup"><span data-stu-id="ebdbc-108">Tasks:</span></span>

* <span data-ttu-id="ebdbc-109">전체 리소스에서 일관된 방식으로 사용할 수 있게 접사를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="ebdbc-109">Define the affixes to use across your resources to maintain consistency.</span></span>
* <span data-ttu-id="ebdbc-110">저장소 계정 이름을 전역적으로 고유하게 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="ebdbc-110">Define storage account names given the requirement for them to be globally unique.</span></span>
* <span data-ttu-id="ebdbc-111">사용할 명명 규칙을 문서화하고 관련된 모든 당사자에게 제공하여 배포 간에 일관성이 유지되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebdbc-111">Document the naming convention to be used and distribute to all parties involved to ensure consistency across deployments.</span></span>

## <a name="naming-conventions"></a><span data-ttu-id="ebdbc-112">명명 규칙</span><span class="sxs-lookup"><span data-stu-id="ebdbc-112">Naming conventions</span></span>
<span data-ttu-id="ebdbc-113">Azure에서 항목을 만들기 전에 좋은 명명 규칙이 구현되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebdbc-113">You should have a good naming convention in place before creating anything in Azure.</span></span> <span data-ttu-id="ebdbc-114">명명 규칙은 모든 리소스에 예측 가능한 이름이 있어야 하며, 이는 해당 리소스의 관리와 연관된 관리 부담을 줄이는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebdbc-114">A naming convention ensures that all the resources have a predictable name, which helps lower the administrative burden associated with managing those resources.</span></span>

<span data-ttu-id="ebdbc-115">전체 조직 또는 특정 Azure 구독이나 계정에 정의된 명명 규칙의 특정 집합을 따를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebdbc-115">You might choose to follow a specific set of naming conventions defined for your entire organization or for a specific Azure subscription or account.</span></span> <span data-ttu-id="ebdbc-116">조직 내의 개인이 Azure 리소스로 작업할 때 암시적 규칙을 쉽게 설정할 수는 있지만, Azure에서 함께 작업을 하는 팀에서도 사용 가능하도록 이러한 규칙을 확장할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebdbc-116">Although it is easy for individuals within organizations to establish implicit rules when working with Azure resources, you need to be able to scale for teams working together in Azure.</span></span>

<span data-ttu-id="ebdbc-117">사전에 명명 규칙 집합을 합의합니다.</span><span class="sxs-lookup"><span data-stu-id="ebdbc-117">Agree on a set of naming conventions up front.</span></span> <span data-ttu-id="ebdbc-118">규칙 집합에 영향을 미치는 명명 규칙과 관련한 고려 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebdbc-118">There are some considerations regarding naming conventions that cut across that sets of rules.</span></span>

## <a name="affixes"></a><span data-ttu-id="ebdbc-119">접사</span><span class="sxs-lookup"><span data-stu-id="ebdbc-119">Affixes</span></span>
<span data-ttu-id="ebdbc-120">명명 규칙을 정의하려는 경우에는 접사의 위치를 결정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebdbc-120">As you look to define a naming convention, one decision is whether the affix is at:</span></span>

* <span data-ttu-id="ebdbc-121">이름(접두사)의 시작 부분</span><span class="sxs-lookup"><span data-stu-id="ebdbc-121">The beginning of the name (prefix)</span></span>
* <span data-ttu-id="ebdbc-122">이름(접미사)의 끝 부분</span><span class="sxs-lookup"><span data-stu-id="ebdbc-122">The end of the name (suffix)</span></span>

<span data-ttu-id="ebdbc-123">예를 들어 `rg` 접사를 사용할 경우 리소스 그룹에 대해 다음 두 가지 이름을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebdbc-123">For instance, here are two possible names for a Resource Group using the `rg` affix:</span></span>

* <span data-ttu-id="ebdbc-124">Rg-WebApp(접두사)</span><span class="sxs-lookup"><span data-stu-id="ebdbc-124">Rg-WebApp (prefix)</span></span>
* <span data-ttu-id="ebdbc-125">WebApp-Rg(접미사)</span><span class="sxs-lookup"><span data-stu-id="ebdbc-125">WebApp-Rg (suffix)</span></span>

<span data-ttu-id="ebdbc-126">접사는 특정 리소스를 설명하는 다양한 측면을 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebdbc-126">Affixes can refer to different aspects that describe the particular resources.</span></span> <span data-ttu-id="ebdbc-127">다음 표에서 일반적으로 사용하는 일부 예를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="ebdbc-127">The following table shows some examples typically used.</span></span>

| <span data-ttu-id="ebdbc-128">측면</span><span class="sxs-lookup"><span data-stu-id="ebdbc-128">Aspect</span></span> | <span data-ttu-id="ebdbc-129">예</span><span class="sxs-lookup"><span data-stu-id="ebdbc-129">Examples</span></span> | <span data-ttu-id="ebdbc-130">참고 사항</span><span class="sxs-lookup"><span data-stu-id="ebdbc-130">Notes</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="ebdbc-131">Environment</span><span class="sxs-lookup"><span data-stu-id="ebdbc-131">Environment</span></span> |<span data-ttu-id="ebdbc-132">dev, stg, prod</span><span class="sxs-lookup"><span data-stu-id="ebdbc-132">dev, stg, prod</span></span> |<span data-ttu-id="ebdbc-133">각 환경의 목적 및 이름에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="ebdbc-133">Depending on the purpose and name of each environment.</span></span> |
| <span data-ttu-id="ebdbc-134">위치</span><span class="sxs-lookup"><span data-stu-id="ebdbc-134">Location</span></span> |<span data-ttu-id="ebdbc-135">usw(West US), use(East US 2)</span><span class="sxs-lookup"><span data-stu-id="ebdbc-135">usw (West US), use (East US 2)</span></span> |<span data-ttu-id="ebdbc-136">데이터 센터의 지역 또는 조직의 지역에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="ebdbc-136">Depending on the region of the datacenter or the region of the organization.</span></span> |
| <span data-ttu-id="ebdbc-137">Azure 구성 요소, 서비스 또는 제품</span><span class="sxs-lookup"><span data-stu-id="ebdbc-137">Azure component, service, or product</span></span> |<span data-ttu-id="ebdbc-138">리소스 그룹은 RG, 가상 네트워크는 VNet</span><span class="sxs-lookup"><span data-stu-id="ebdbc-138">Rg for resource group, VNet for virtual network</span></span> |<span data-ttu-id="ebdbc-139">리소스가 지원을 제공하는 제품에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="ebdbc-139">Depending on the product for which the resource provides support.</span></span> |
| <span data-ttu-id="ebdbc-140">역할</span><span class="sxs-lookup"><span data-stu-id="ebdbc-140">Role</span></span> |<span data-ttu-id="ebdbc-141">db, 앱, 웹</span><span class="sxs-lookup"><span data-stu-id="ebdbc-141">db, app, web</span></span> |<span data-ttu-id="ebdbc-142">가상 컴퓨터의 역할에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="ebdbc-142">Depending on the role of the virtual machine.</span></span> |
| <span data-ttu-id="ebdbc-143">인스턴스</span><span class="sxs-lookup"><span data-stu-id="ebdbc-143">Instance</span></span> |<span data-ttu-id="ebdbc-144">01, 02, 03 등</span><span class="sxs-lookup"><span data-stu-id="ebdbc-144">01, 02, 03, etc.</span></span> |<span data-ttu-id="ebdbc-145">둘 이상의 인스턴스가 있는 리소스의 경우.</span><span class="sxs-lookup"><span data-stu-id="ebdbc-145">For resources that have more than one instance.</span></span> <span data-ttu-id="ebdbc-146">예를들어, 클라우드 서비스의 분산된 웹 서버를 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="ebdbc-146">For example, load balanced web servers in a cloud service.</span></span> |

<span data-ttu-id="ebdbc-147">명명 규칙을 설정할 때 각 리소스 유형에 사용할 접사 및 어느 위치(접두사 및 접미사)에 사용할지 분명하게 언급해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebdbc-147">When establishing your naming conventions, make sure that they clearly state which affixes to use for each type of resource, and in which position (prefix vs suffix).</span></span>

## <a name="dates"></a><span data-ttu-id="ebdbc-148">날짜</span><span class="sxs-lookup"><span data-stu-id="ebdbc-148">Dates</span></span>
<span data-ttu-id="ebdbc-149">리소스 이름에서 만든 날짜를 확인하는 것이 중요한 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="ebdbc-149">It is often important to determine the date of creation from the name of a resource.</span></span> <span data-ttu-id="ebdbc-150">YYYYMMDD 날짜 형식을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ebdbc-150">We recommend the YYYYMMDD date format.</span></span> <span data-ttu-id="ebdbc-151">이 형식을 사용하는 경우 전체 날짜가 기록될 뿐 아니라, 이름에서 날짜만 다른 두 리소스가 사전순/시간순으로 정렬됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebdbc-151">This format ensures that not only is the full date is recorded, but also that two resources whose names differ only on the date are sorted alphabetically and chronologically.</span></span>

## <a name="naming-resources"></a><span data-ttu-id="ebdbc-152">리소스 명명</span><span class="sxs-lookup"><span data-stu-id="ebdbc-152">Naming resources</span></span>
<span data-ttu-id="ebdbc-153">명명 규칙에서 각 리소스 형식을 정의합니다. 이 명명 규칙은 작성되는 각 리소스에 이름을 할당하는 방법을 정의하는 규칙을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebdbc-153">Define each type of resource in the naming convention, which should have rules that define how to assign names to each resource that is created.</span></span> <span data-ttu-id="ebdbc-154">이러한 규칙은 모든 유형의 리소스에 적용해야 합니다. 예를들어 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ebdbc-154">These rules should apply to all types of resources, for example:</span></span>

* <span data-ttu-id="ebdbc-155">구독</span><span class="sxs-lookup"><span data-stu-id="ebdbc-155">Subscriptions</span></span>
* <span data-ttu-id="ebdbc-156">계정</span><span class="sxs-lookup"><span data-stu-id="ebdbc-156">Accounts</span></span>
* <span data-ttu-id="ebdbc-157">저장소 계정</span><span class="sxs-lookup"><span data-stu-id="ebdbc-157">Storage accounts</span></span>
* <span data-ttu-id="ebdbc-158">가상 네트워크</span><span class="sxs-lookup"><span data-stu-id="ebdbc-158">Virtual networks</span></span>
* <span data-ttu-id="ebdbc-159">서브넷</span><span class="sxs-lookup"><span data-stu-id="ebdbc-159">Subnets</span></span>
* <span data-ttu-id="ebdbc-160">가용성 집합</span><span class="sxs-lookup"><span data-stu-id="ebdbc-160">Availability sets</span></span>
* <span data-ttu-id="ebdbc-161">리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="ebdbc-161">Resource groups</span></span>
* <span data-ttu-id="ebdbc-162">가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="ebdbc-162">Virtual machines</span></span>
* <span data-ttu-id="ebdbc-163">끝점</span><span class="sxs-lookup"><span data-stu-id="ebdbc-163">Endpoints</span></span>
* <span data-ttu-id="ebdbc-164">네트워크 보안 그룹</span><span class="sxs-lookup"><span data-stu-id="ebdbc-164">Network security groups</span></span>
* <span data-ttu-id="ebdbc-165">역할</span><span class="sxs-lookup"><span data-stu-id="ebdbc-165">Roles</span></span>

<span data-ttu-id="ebdbc-166">이름이 참조하는 리소스를 확인하기에 충분한 정보를 제공할 수 있도록 설명이 포함된 이름을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebdbc-166">To ensure that the name provides enough information to determine to which resource it refers, you should use descriptive names.</span></span>

## <a name="computer-names"></a><span data-ttu-id="ebdbc-167">컴퓨터 이름</span><span class="sxs-lookup"><span data-stu-id="ebdbc-167">Computer names</span></span>
<span data-ttu-id="ebdbc-168">Azure에서 VM(가상 컴퓨터)을 만들 때는 리소스 이름에 사용되는 VM 이름(최대 64자)을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebdbc-168">When you create a virtual machine (VM), Azure requires a VM name of up to 64 characters that is used for the resource name.</span></span> <span data-ttu-id="ebdbc-169">Azure는 VM에 설치된 운영 체제에 동일한 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ebdbc-169">Azure uses the same name for the operating system installed in the VM.</span></span> <span data-ttu-id="ebdbc-170">하지만 이 이름이 항상 같지는 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebdbc-170">However, these names might not always be the same.</span></span>

<span data-ttu-id="ebdbc-171">운영 체제를 이미 포함하는 .vhd 이미지 파일에서 VM을 만드는 경우, Azure의 VM 이름이 VM의 운영 체제 컴퓨터 이름과 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebdbc-171">If a VM is created from a .vhd image file that already contains an operating system, the VM name in Azure can differ from the VM's operating system computer name.</span></span> <span data-ttu-id="ebdbc-172">이 경우 VM 관리가 더욱 어려워질 수 있으므로 권장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ebdbc-172">This situation can add a degree of difficulty to VM management, which we therefore do not recommend.</span></span> <span data-ttu-id="ebdbc-173">Azure VM 리소스 이름을 해당 VM의 운영 체제에 할당하는 컴퓨터 이름과 동일한 이름으로 지정하세요.</span><span class="sxs-lookup"><span data-stu-id="ebdbc-173">Assign the Azure VM resource the same name as the computer name that you assign to the operating system of that VM.</span></span>

<span data-ttu-id="ebdbc-174">Azure VM 이름은 기본 운영 체제 컴퓨터 이름과 동일하게 지정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ebdbc-174">We recommend that the Azure VM name is the same as the underlying operating system computer name.</span></span>

## <a name="storage-account-names"></a><span data-ttu-id="ebdbc-175">저장소 계정 이름</span><span class="sxs-lookup"><span data-stu-id="ebdbc-175">Storage account names</span></span>
<span data-ttu-id="ebdbc-176">별도의 저장소 계정을 만들지 않으므로 이 섹션은 [Azure Managed Disks](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)에 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ebdbc-176">This section does not apply to [Azure Managed Disks](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), as you do not create a separate storage account.</span></span> <span data-ttu-id="ebdbc-177">관리되지 않는 디스크의 경우 저장소 계정 이름에 적용되는 특별한 규칙이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebdbc-177">For unmanaged disks, storage accounts have special rules governing their names.</span></span> <span data-ttu-id="ebdbc-178">소문자와 숫자만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebdbc-178">You can only use lowercase letters and numbers.</span></span> <span data-ttu-id="ebdbc-179">자세한 내용은 [저장소 계정 만들기](../../storage/storage-create-storage-account.md#create-a-storage-account) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ebdbc-179">For more information, see [Create a storage account](../../storage/storage-create-storage-account.md#create-a-storage-account).</span></span> <span data-ttu-id="ebdbc-180">또한 core.windows.net이 포함된 저장소 계정 이름은 전역적으로 유효하고 고유한 DNS 이름이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebdbc-180">Additionally, the storage account name, with core.windows.net, should be a globally valid, unique DNS name.</span></span> <span data-ttu-id="ebdbc-181">예를 들어 저장소 계정이 mystorageaccount인 경우 결과로 생성된 다음 DNS 이름이 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebdbc-181">For instance, if the storage account is called mystorageaccount, the following resulting DNS names should be unique:</span></span>

* <span data-ttu-id="ebdbc-182">mystorageaccount.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="ebdbc-182">mystorageaccount.blob.core.windows.net</span></span>
* <span data-ttu-id="ebdbc-183">mystorageaccount.table.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="ebdbc-183">mystorageaccount.table.core.windows.net</span></span>
* <span data-ttu-id="ebdbc-184">mystorageaccount.queue.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="ebdbc-184">mystorageaccount.queue.core.windows.net</span></span>

## <a name="next-steps"></a><span data-ttu-id="ebdbc-185">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ebdbc-185">Next steps</span></span>
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

