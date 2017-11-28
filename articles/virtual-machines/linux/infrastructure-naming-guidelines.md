---
title: "명명 지침-Linux aaaAzure 인프라 | Microsoft Docs"
description: "Hello 주요 디자인 및 구현에 대 한 지침 Azure 인프라 서비스에서 이름에 대해 알아봅니다."
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
ms.openlocfilehash: 333146e7b2071e43527a5d7dc2ec02ebfb316eb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-infrastructure-naming-guidelines-for-linux-vms"></a><span data-ttu-id="3f725-103">Linux VM에 대한 Azure 인프라 명명 지침</span><span class="sxs-lookup"><span data-stu-id="3f725-103">Azure infrastructure naming guidelines for Linux VMs</span></span> 

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

<span data-ttu-id="3f725-104">이 문서는 tooapproach 명명 규칙에 다양 한 모든 Azure 리소스 toobuild 논리 and 쉽게 식별할 수에 대 한 리소스의 환경 전체에서 설정 하는 방법을 이해에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="3f725-104">This article focuses on understanding how tooapproach naming conventions for all your various Azure resources toobuild a logical and easily identifiable set of resources across your environment.</span></span>

## <a name="implementation-guidelines-for-naming-conventions"></a><span data-ttu-id="3f725-105">명명 규칙에 대한 구현 지침</span><span class="sxs-lookup"><span data-stu-id="3f725-105">Implementation guidelines for naming conventions</span></span>
<span data-ttu-id="3f725-106">의사 결정:</span><span class="sxs-lookup"><span data-stu-id="3f725-106">Decisions:</span></span>

* <span data-ttu-id="3f725-107">Azure 리소스에 대한 명명 규칙은 무엇인가?</span><span class="sxs-lookup"><span data-stu-id="3f725-107">What are your naming conventions for Azure resources?</span></span>

<span data-ttu-id="3f725-108">작업:</span><span class="sxs-lookup"><span data-stu-id="3f725-108">Tasks:</span></span>

* <span data-ttu-id="3f725-109">리소스 toomaintain 일관성 hello affixes toouse를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f725-109">Define hello affixes toouse across your resources toomaintain consistency.</span></span>
* <span data-ttu-id="3f725-110">저장소 계정 이름을 hello 요구 사항에 대 한 전역 고유 toobe를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f725-110">Define storage account names given hello requirement for them toobe globally unique.</span></span>
* <span data-ttu-id="3f725-111">사용 되는 배포 간에 tooall 당사자와 관련 된 tooensure 일관성을 분산 하는 명명 규칙 toobe 문서 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f725-111">Document hello naming convention toobe used and distribute tooall parties involved tooensure consistency across deployments.</span></span>

## <a name="naming-conventions"></a><span data-ttu-id="3f725-112">명명 규칙</span><span class="sxs-lookup"><span data-stu-id="3f725-112">Naming conventions</span></span>
<span data-ttu-id="3f725-113">Azure에서 항목을 만들기 전에 좋은 명명 규칙이 구현되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f725-113">You should have a good naming convention in place before creating anything in Azure.</span></span> <span data-ttu-id="3f725-114">명명 규칙 모든 hello 리소스 hello 관리 비용이 절감 이러한 리소스 관리와 관련 된는 데 도움이 되는 예측 가능한 이름이 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f725-114">A naming convention ensures that all hello resources have a predictable name, which helps lower hello administrative burden associated with managing those resources.</span></span>

<span data-ttu-id="3f725-115">전체 조직에 대해 또는 특정 Azure 구독 또는 계정에 대해 정의 된 명명 규칙의 특정 집합 toofollow를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f725-115">You might choose toofollow a specific set of naming conventions defined for your entire organization or for a specific Azure subscription or account.</span></span> <span data-ttu-id="3f725-116">수도 있지만 조직 tooestablish 암시적 규칙 내에서 개별 사용자를 쉽게 Azure 리소스를 사용 하는 경우, Azure에서 함께 작업 하는 팀 toobe 수 tooscale가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f725-116">Although it is easy for individuals within organizations tooestablish implicit rules when working with Azure resources, you need toobe able tooscale for teams working together in Azure.</span></span>

<span data-ttu-id="3f725-117">사전에 명명 규칙 집합을 합의합니다.</span><span class="sxs-lookup"><span data-stu-id="3f725-117">Agree on a set of naming conventions up front.</span></span> <span data-ttu-id="3f725-118">규칙 집합에 영향을 미치는 명명 규칙과 관련한 고려 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f725-118">There are some considerations regarding naming conventions that cut across that sets of rules.</span></span>

## <a name="affixes"></a><span data-ttu-id="3f725-119">접사</span><span class="sxs-lookup"><span data-stu-id="3f725-119">Affixes</span></span>
<span data-ttu-id="3f725-120">Toodefine 명명 규칙을 볼 때 결정 인지 여부 hello를 붙일에서:</span><span class="sxs-lookup"><span data-stu-id="3f725-120">As you look toodefine a naming convention, one decision is whether hello affix is at:</span></span>

* <span data-ttu-id="3f725-121">hello 이름 시작 부분 hello (접두사)</span><span class="sxs-lookup"><span data-stu-id="3f725-121">hello beginning of hello name (prefix)</span></span>
* <span data-ttu-id="3f725-122">hello 이름 끝에 hello (접미사)</span><span class="sxs-lookup"><span data-stu-id="3f725-122">hello end of hello name (suffix)</span></span>

<span data-ttu-id="3f725-123">Hello를 사용 하 여 리소스 그룹에 대 한 두 가지 가능한 이름 예를 들어, 다음은 `rg` 붙입니다.</span><span class="sxs-lookup"><span data-stu-id="3f725-123">For instance, here are two possible names for a Resource Group using hello `rg` affix:</span></span>

* <span data-ttu-id="3f725-124">Rg-WebApp(접두사)</span><span class="sxs-lookup"><span data-stu-id="3f725-124">Rg-WebApp (prefix)</span></span>
* <span data-ttu-id="3f725-125">WebApp-Rg(접미사)</span><span class="sxs-lookup"><span data-stu-id="3f725-125">WebApp-Rg (suffix)</span></span>

<span data-ttu-id="3f725-126">Affixes는 hello 특정 리소스를 설명 하는 toodifferent 측면을 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f725-126">Affixes can refer toodifferent aspects that describe hello particular resources.</span></span> <span data-ttu-id="3f725-127">hello 다음 표에서 일반적으로 사용 되는 몇 가지 예입니다.</span><span class="sxs-lookup"><span data-stu-id="3f725-127">hello following table shows some examples typically used.</span></span>

| <span data-ttu-id="3f725-128">측면</span><span class="sxs-lookup"><span data-stu-id="3f725-128">Aspect</span></span> | <span data-ttu-id="3f725-129">예</span><span class="sxs-lookup"><span data-stu-id="3f725-129">Examples</span></span> | <span data-ttu-id="3f725-130">참고 사항</span><span class="sxs-lookup"><span data-stu-id="3f725-130">Notes</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="3f725-131">Environment</span><span class="sxs-lookup"><span data-stu-id="3f725-131">Environment</span></span> |<span data-ttu-id="3f725-132">dev, stg, prod</span><span class="sxs-lookup"><span data-stu-id="3f725-132">dev, stg, prod</span></span> |<span data-ttu-id="3f725-133">에 따라 hello 용도 각 환경의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3f725-133">Depending on hello purpose and name of each environment.</span></span> |
| <span data-ttu-id="3f725-134">위치</span><span class="sxs-lookup"><span data-stu-id="3f725-134">Location</span></span> |<span data-ttu-id="3f725-135">usw(West US), use(East US 2)</span><span class="sxs-lookup"><span data-stu-id="3f725-135">usw (West US), use (East US 2)</span></span> |<span data-ttu-id="3f725-136">Hello 데이터 센터의 hello 지역 또는 hello 조직의 hello 지역에 따라.</span><span class="sxs-lookup"><span data-stu-id="3f725-136">Depending on hello region of hello datacenter or hello region of hello organization.</span></span> |
| <span data-ttu-id="3f725-137">Azure 구성 요소, 서비스 또는 제품</span><span class="sxs-lookup"><span data-stu-id="3f725-137">Azure component, service, or product</span></span> |<span data-ttu-id="3f725-138">리소스 그룹은 RG, 가상 네트워크는 VNet</span><span class="sxs-lookup"><span data-stu-id="3f725-138">Rg for resource group, VNet for virtual network</span></span> |<span data-ttu-id="3f725-139">hello에 대 한 리소스를 제공 하는 hello 제품에 따라 다음을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f725-139">Depending on hello product for which hello resource provides support.</span></span> |
| <span data-ttu-id="3f725-140">역할</span><span class="sxs-lookup"><span data-stu-id="3f725-140">Role</span></span> |<span data-ttu-id="3f725-141">db, 앱, 웹</span><span class="sxs-lookup"><span data-stu-id="3f725-141">db, app, web</span></span> |<span data-ttu-id="3f725-142">Hello 가상 컴퓨터의 hello 역할에 따라.</span><span class="sxs-lookup"><span data-stu-id="3f725-142">Depending on hello role of hello virtual machine.</span></span> |
| <span data-ttu-id="3f725-143">인스턴스</span><span class="sxs-lookup"><span data-stu-id="3f725-143">Instance</span></span> |<span data-ttu-id="3f725-144">01, 02, 03 등</span><span class="sxs-lookup"><span data-stu-id="3f725-144">01, 02, 03, etc.</span></span> |<span data-ttu-id="3f725-145">둘 이상의 인스턴스가 있는 리소스의 경우.</span><span class="sxs-lookup"><span data-stu-id="3f725-145">For resources that have more than one instance.</span></span> <span data-ttu-id="3f725-146">예를들어, 클라우드 서비스의 분산된 웹 서버를 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="3f725-146">For example, load balanced web servers in a cloud service.</span></span> |

<span data-ttu-id="3f725-147">명명 규칙을 설정할 때 확인 있는 명확 하 게 상태는 리소스의 위치 (접두사 및 접미사) 각 유형에 toouse affixes 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f725-147">When establishing your naming conventions, make sure that they clearly state which affixes toouse for each type of resource, and in which position (prefix vs suffix).</span></span>

## <a name="dates"></a><span data-ttu-id="3f725-148">날짜</span><span class="sxs-lookup"><span data-stu-id="3f725-148">Dates</span></span>
<span data-ttu-id="3f725-149">리소스의 생성 hello 이름에서 중요 한 toodetermine hello 날짜 방식은 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f725-149">It is often important toodetermine hello date of creation from hello name of a resource.</span></span> <span data-ttu-id="3f725-150">Hello YYYYMMDD 날짜 형식을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3f725-150">We recommend hello YYYYMMDD date format.</span></span> <span data-ttu-id="3f725-151">이 형식을 사용 하면 뿐만 아니라 hello 전체 날짜, 기록 하지만 이름이 hello 날짜만 다른 두 자원을 사전순으로 및 시간순으로 정렬 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f725-151">This format ensures that not only is hello full date is recorded, but also that two resources whose names differ only on hello date are sorted alphabetically and chronologically.</span></span>

## <a name="naming-resources"></a><span data-ttu-id="3f725-152">리소스 명명</span><span class="sxs-lookup"><span data-stu-id="3f725-152">Naming resources</span></span>
<span data-ttu-id="3f725-153">각 유형의 리소스 hello 명명 규칙에 정의 방법을 tooassign tooeach 리소스의 이름을 정의 하는 규칙 있어야 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="3f725-153">Define each type of resource in hello naming convention, which should have rules that define how tooassign names tooeach resource that is created.</span></span> <span data-ttu-id="3f725-154">이러한 규칙에는 예를 들어 tooall 유형의 리소스를 적용 해야:</span><span class="sxs-lookup"><span data-stu-id="3f725-154">These rules should apply tooall types of resources, for example:</span></span>

* <span data-ttu-id="3f725-155">구독</span><span class="sxs-lookup"><span data-stu-id="3f725-155">Subscriptions</span></span>
* <span data-ttu-id="3f725-156">계정</span><span class="sxs-lookup"><span data-stu-id="3f725-156">Accounts</span></span>
* <span data-ttu-id="3f725-157">저장소 계정</span><span class="sxs-lookup"><span data-stu-id="3f725-157">Storage accounts</span></span>
* <span data-ttu-id="3f725-158">가상 네트워크</span><span class="sxs-lookup"><span data-stu-id="3f725-158">Virtual networks</span></span>
* <span data-ttu-id="3f725-159">서브넷</span><span class="sxs-lookup"><span data-stu-id="3f725-159">Subnets</span></span>
* <span data-ttu-id="3f725-160">가용성 집합</span><span class="sxs-lookup"><span data-stu-id="3f725-160">Availability sets</span></span>
* <span data-ttu-id="3f725-161">리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="3f725-161">Resource groups</span></span>
* <span data-ttu-id="3f725-162">가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="3f725-162">Virtual machines</span></span>
* <span data-ttu-id="3f725-163">끝점</span><span class="sxs-lookup"><span data-stu-id="3f725-163">Endpoints</span></span>
* <span data-ttu-id="3f725-164">네트워크 보안 그룹</span><span class="sxs-lookup"><span data-stu-id="3f725-164">Network security groups</span></span>
* <span data-ttu-id="3f725-165">역할</span><span class="sxs-lookup"><span data-stu-id="3f725-165">Roles</span></span>

<span data-ttu-id="3f725-166">설명이 포함 된 이름을 사용 하도록, 이름 hello tooensure 참조 충분 한 정보 toodetermine toowhich 리소스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f725-166">tooensure that hello name provides enough information toodetermine toowhich resource it refers, you should use descriptive names.</span></span>

## <a name="computer-names"></a><span data-ttu-id="3f725-167">컴퓨터 이름</span><span class="sxs-lookup"><span data-stu-id="3f725-167">Computer names</span></span>
<span data-ttu-id="3f725-168">가상 컴퓨터 (VM)를 만들 때 Azure는 VM의 이름을 too64 문자를 hello 리소스 이름에 사용 되는 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f725-168">When you create a virtual machine (VM), Azure requires a VM name of up too64 characters that is used for hello resource name.</span></span> <span data-ttu-id="3f725-169">Azure 사용 하 여 hello hello VM에에서 설치 된 hello 운영 체제에 대 한 동일한 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3f725-169">Azure uses hello same name for hello operating system installed in hello VM.</span></span> <span data-ttu-id="3f725-170">그러나 이러한 이름은 수 하지 항상 될 hello 동일한 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f725-170">However, these names might not always be hello same.</span></span>

<span data-ttu-id="3f725-171">VM를 운영 체제에 이미 있는.vhd 이미지 파일에서 만든 경우에 VM의 운영 체제 컴퓨터 이름으로 hello에서 Azure의 hello VM 이름을 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f725-171">If a VM is created from a .vhd image file that already contains an operating system, hello VM name in Azure can differ from hello VM's operating system computer name.</span></span> <span data-ttu-id="3f725-172">이 경우 난이도 tooVM 관리 하므로 권장 하지는 않습니다, 수준을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f725-172">This situation can add a degree of difficulty tooVM management, which we therefore do not recommend.</span></span> <span data-ttu-id="3f725-173">Hello Azure VM 리소스 hello 이름과 같은 해당 VM의 운영 체제 toohello 할당 하는 hello 컴퓨터 이름으로 이름을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f725-173">Assign hello Azure VM resource hello same name as hello computer name that you assign toohello operating system of that VM.</span></span>

<span data-ttu-id="3f725-174">Hello Azure VM 이름이 hello 기본 운영 체제 컴퓨터 이름으로 같은 hello 되는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3f725-174">We recommend that hello Azure VM name is hello same as hello underlying operating system computer name.</span></span>

## <a name="storage-account-names"></a><span data-ttu-id="3f725-175">저장소 계정 이름</span><span class="sxs-lookup"><span data-stu-id="3f725-175">Storage account names</span></span>
<span data-ttu-id="3f725-176">이 섹션이 너무 적용 되지 않습니다[Azure 관리 되는 디스크](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)별도 저장소 계정을 만들지 않으면 처럼 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f725-176">This section does not apply too[Azure Managed Disks](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), as you do not create a separate storage account.</span></span> <span data-ttu-id="3f725-177">관리되지 않는 디스크의 경우 저장소 계정 이름에 적용되는 특별한 규칙이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f725-177">For unmanaged disks, storage accounts have special rules governing their names.</span></span> <span data-ttu-id="3f725-178">소문자와 숫자만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f725-178">You can only use lowercase letters and numbers.</span></span> <span data-ttu-id="3f725-179">자세한 내용은 [저장소 계정 만들기](../../storage/storage-create-storage-account.md#create-a-storage-account) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3f725-179">For more information, see [Create a storage account](../../storage/storage-create-storage-account.md#create-a-storage-account).</span></span> <span data-ttu-id="3f725-180">또한, core.windows.net으로 hello 저장소 계정 이름에는 전역적으로 유효 하 고 고유한 DNS 이름 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f725-180">Additionally, hello storage account name, with core.windows.net, should be a globally valid, unique DNS name.</span></span> <span data-ttu-id="3f725-181">예를 들어 hello 저장소 계정 mystorageaccount을 라고 hello 다음 결과 DNS 이름은 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f725-181">For instance, if hello storage account is called mystorageaccount, hello following resulting DNS names should be unique:</span></span>

* <span data-ttu-id="3f725-182">mystorageaccount.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="3f725-182">mystorageaccount.blob.core.windows.net</span></span>
* <span data-ttu-id="3f725-183">mystorageaccount.table.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="3f725-183">mystorageaccount.table.core.windows.net</span></span>
* <span data-ttu-id="3f725-184">mystorageaccount.queue.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="3f725-184">mystorageaccount.queue.core.windows.net</span></span>

## <a name="next-steps"></a><span data-ttu-id="3f725-185">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3f725-185">Next steps</span></span>
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

