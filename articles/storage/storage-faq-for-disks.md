---
title: "Azure IaaS VM 디스크에 대한 질문과 대답(FAQ) | Microsoft Docs"
description: "Azure IaaS VM 디스크 및 프리미엄 디스크(관리 및 관리되지 않는 디스크)에 대한 질문과 대답"
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: e2a20625-6224-4187-8401-abadc8f1de91
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: robinsh
ms.openlocfilehash: 9e5eed35334f1b95441b8181c8e90645be78b389
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="frequently-asked-questions-about-azure-iaas-vm-disks-and-managed-and-unmanaged-premium-disks"></a><span data-ttu-id="f203f-103">Azure IaaS VM 디스크와 관리 및 관리되지 않는 프리미엄 디스크에 대한 질문과 대답</span><span class="sxs-lookup"><span data-stu-id="f203f-103">Frequently asked questions about Azure IaaS VM disks and managed and unmanaged premium disks</span></span>

<span data-ttu-id="f203f-104">이 문서에서는 Azure Managed Disks 및 Azure Premium Storage에 대해 몇몇 자주 묻는 질문과 대답을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f203f-104">This article answers some frequently asked questions about Azure Managed Disks and Azure Premium Storage.</span></span>

## <a name="managed-disks"></a><span data-ttu-id="f203f-105">Managed Disks</span><span class="sxs-lookup"><span data-stu-id="f203f-105">Managed Disks</span></span>

<span data-ttu-id="f203f-106">**Azure Managed Disks란?**</span><span class="sxs-lookup"><span data-stu-id="f203f-106">**What is Azure Managed Disks?**</span></span>

<span data-ttu-id="f203f-107">Managed Disks는 저장소 계정 관리를 처리하여 Azure IaaS VM을 위한 디스크 관리를 간소화하는 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="f203f-107">Managed Disks is a feature that simplifies disk management for Azure IaaS VMs by handling storage account management for you.</span></span> <span data-ttu-id="f203f-108">자세한 내용은 [Managed Disks 개요](storage-managed-disks-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f203f-108">For more information, see the [Managed Disks overview](storage-managed-disks-overview.md).</span></span>

<span data-ttu-id="f203f-109">**80GB인 기존 VHD에서 표준 Managed Disk를 만들 경우 비용은 얼마나 드나요?**</span><span class="sxs-lookup"><span data-stu-id="f203f-109">**If I create a standard managed disk from an existing VHD that's 80 GB, how much will that cost me?**</span></span>

<span data-ttu-id="f203f-110">80GB VHD로 만든 표준 관리 디스크는 다음과 같은 사용 가능 표준 디스크 크기인 S10 디스크로 취급됩니다.</span><span class="sxs-lookup"><span data-stu-id="f203f-110">A standard managed disk created from an 80-GB VHD is treated as the next available standard disk size, which is an S10 disk.</span></span> <span data-ttu-id="f203f-111">S10 디스크 가격 책정에 따라 요금이 부과됩니다.</span><span class="sxs-lookup"><span data-stu-id="f203f-111">You're charged according to the S10 disk pricing.</span></span> <span data-ttu-id="f203f-112">자세한 내용은 [가격 책정 페이지](https://azure.microsoft.com/pricing/details/storage)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f203f-112">For more information, see the [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="f203f-113">**표준 관리 디스크에 대한 트랜잭션 비용이 있나요?**</span><span class="sxs-lookup"><span data-stu-id="f203f-113">**Are there any transaction costs for standard managed disks?**</span></span>

<span data-ttu-id="f203f-114">예.</span><span class="sxs-lookup"><span data-stu-id="f203f-114">Yes.</span></span> <span data-ttu-id="f203f-115">각 트랜잭션에 대해 요금이 부과됩니다.</span><span class="sxs-lookup"><span data-stu-id="f203f-115">You're charged for each transaction.</span></span> <span data-ttu-id="f203f-116">자세한 내용은 [가격 책정 페이지](https://azure.microsoft.com/pricing/details/storage)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f203f-116">For more information, see the [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="f203f-117">**표준 관리 디스크에 대한 요금은 디스크에 있는 데이터의 실제 크기에 대해 부과되나요? 아니면 디스크의 프로비전된 용량에 대해 부과되나요?**</span><span class="sxs-lookup"><span data-stu-id="f203f-117">**For a standard managed disk, will I be charged for the actual size of the data on the disk or for the provisioned capacity of the disk?**</span></span>

<span data-ttu-id="f203f-118">디스크의 프로비전된 용량에 따라 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="f203f-118">You're charged based on the provisioned capacity of the disk.</span></span> <span data-ttu-id="f203f-119">자세한 내용은 [가격 책정 페이지](https://azure.microsoft.com/pricing/details/storage)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f203f-119">For more information, see the [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="f203f-120">**프리미엄 Managed Disks의 가격은 관리되지 않는 디스크와 어떻게 다르게 책정되나요?**</span><span class="sxs-lookup"><span data-stu-id="f203f-120">**How is pricing of premium managed disks different from unmanaged disks?**</span></span>

<span data-ttu-id="f203f-121">프리미엄 관리 디스크의 가격은 관리되지 않는 프리미엄 디스크와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f203f-121">The pricing of premium managed disks is the same as unmanaged premium disks.</span></span>

<span data-ttu-id="f203f-122">**내 Managed Disks의 저장소 계정 유형(표준 또는 프리미엄)을 내가 변경할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="f203f-122">**Can I change the storage account type (Standard or Premium) of my managed disks?**</span></span>

<span data-ttu-id="f203f-123">예.</span><span class="sxs-lookup"><span data-stu-id="f203f-123">Yes.</span></span> <span data-ttu-id="f203f-124">Azure Portal, PowerShell 또는 Azure CLI를 사용하여 Managed Disks의 저장소 계정 형식을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f203f-124">You can change the storage account type of your managed disks by using the Azure portal, PowerShell, or the Azure CLI.</span></span>

<span data-ttu-id="f203f-125">**개인 저장소 계정에 Managed Disk를 복사하거나 내보낼 수 있는 방법이 있나요?**</span><span class="sxs-lookup"><span data-stu-id="f203f-125">**Is there a way that I can copy or export a managed disk to a private storage account?**</span></span>

<span data-ttu-id="f203f-126">예.</span><span class="sxs-lookup"><span data-stu-id="f203f-126">Yes.</span></span> <span data-ttu-id="f203f-127">Azure Portal, PowerShell 또는 Azure CLI를 사용하여 Managed Disks를 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f203f-127">You can export your managed disks by using the Azure portal, PowerShell, or the Azure CLI.</span></span>

<span data-ttu-id="f203f-128">**Azure Storage 계정에서 VHD 파일을 사용하여 다른 구독에 Managed Disk를 만들 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="f203f-128">**Can I use a VHD file in an Azure storage account to create a managed disk with a different subscription?**</span></span>

<span data-ttu-id="f203f-129">아니요.</span><span class="sxs-lookup"><span data-stu-id="f203f-129">No.</span></span>

<span data-ttu-id="f203f-130">**Azure Storage 계정에서 VHD 파일을 사용하여 다른 지역에 관리 디스크를 만들 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="f203f-130">**Can I use a VHD file in an Azure storage account to create a managed disk in a different region?**</span></span>

<span data-ttu-id="f203f-131">아니요.</span><span class="sxs-lookup"><span data-stu-id="f203f-131">No.</span></span>

<span data-ttu-id="f203f-132">**고객이 Managed Disks를 사용하는 경우 규모 제한이 있나요?**</span><span class="sxs-lookup"><span data-stu-id="f203f-132">**Are there any scale limitations for customers that use managed disks?**</span></span>

<span data-ttu-id="f203f-133">Managed Disks는 저장소 계정과 관련된 한도를 없앱니다.</span><span class="sxs-lookup"><span data-stu-id="f203f-133">Managed Disks eliminates the limits associated with storage accounts.</span></span> <span data-ttu-id="f203f-134">그러나 구독당 Managed Disks의 수는 기본적으로 2,000개로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="f203f-134">However, the number of managed disks per subscription is limited to 2,000 by default.</span></span> <span data-ttu-id="f203f-135">이 수를 늘리려면 지원에 문의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f203f-135">You can call support to increase this number.</span></span>

<span data-ttu-id="f203f-136">**관리 디스크의 증분 스냅숏을 가져올 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="f203f-136">**Can I take an incremental snapshot of a managed disk?**</span></span>

<span data-ttu-id="f203f-137">아니요.</span><span class="sxs-lookup"><span data-stu-id="f203f-137">No.</span></span> <span data-ttu-id="f203f-138">현재 스냅숏 기능은 Managed Disk의 전체 복사본을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f203f-138">The current snapshot capability makes a full copy of a managed disk.</span></span> <span data-ttu-id="f203f-139">그러나 나중에는 증분 스냅숏을 지원하도록 할 계획입니다.</span><span class="sxs-lookup"><span data-stu-id="f203f-139">However, we are planning to support incremental snapshots in the future.</span></span>

<span data-ttu-id="f203f-140">**관리 및 관리되지 않는 디스크를 조합하여 가용성 집합의 VM을 구성할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="f203f-140">**Can VMs in an availability set consist of a combination of managed and unmanaged disks?**</span></span>

<span data-ttu-id="f203f-141">아니요.</span><span class="sxs-lookup"><span data-stu-id="f203f-141">No.</span></span> <span data-ttu-id="f203f-142">가용성 집합에 있는 VM은 모두 Managed Disks를 사용하거나 모두 관리되지 않는 디스크를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f203f-142">The VMs in an availability set must use either all managed disks or all unmanaged disks.</span></span> <span data-ttu-id="f203f-143">가용성 집합을 만들 때 사용할 디스크 유형을 사용자가 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f203f-143">When you create an availability set, you can choose which type of disks you want to use.</span></span>

<span data-ttu-id="f203f-144">**Managed Disks가 Azure Portal에서 기본 옵션인가요?**</span><span class="sxs-lookup"><span data-stu-id="f203f-144">**Is Managed Disks the default option in the Azure portal?**</span></span>

<span data-ttu-id="f203f-145">현재는 아니지만 나중에는 기본 옵션으로 사용될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="f203f-145">Not currently, but it will become the default in the future.</span></span>

<span data-ttu-id="f203f-146">**내가 빈 관리 디스크를 만들 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="f203f-146">**Can I create an empty managed disk?**</span></span>

<span data-ttu-id="f203f-147">예.</span><span class="sxs-lookup"><span data-stu-id="f203f-147">Yes.</span></span> <span data-ttu-id="f203f-148">사용자가 빈 디스크를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f203f-148">You can create an empty disk.</span></span> <span data-ttu-id="f203f-149">Managed Disk는 VM에 독립적으로 즉, VM에 연결하지 않고 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f203f-149">A managed disk can be created independently of a VM, for example, without attaching it to a VM.</span></span>

<span data-ttu-id="f203f-150">**Managed Disks를 사용하는 가용성 집합에 지원되는 장애 도메인 수는 몇 개인가요?**</span><span class="sxs-lookup"><span data-stu-id="f203f-150">**What is the supported fault domain count for an availability set that uses Managed Disks?**</span></span>

<span data-ttu-id="f203f-151">Managed Disks를 사용하는 가용성 집합이 위치한 지역에 따라 지원되는 장애 도메인 수는 2개 또는 3개입니다.</span><span class="sxs-lookup"><span data-stu-id="f203f-151">Depending on the region where the availability set that uses Managed Disks is located, the supported fault domain count is 2 or 3.</span></span>

<span data-ttu-id="f203f-152">**진단을 위한 표준 저장소 계정은 어떤 방식으로 설정되나요?**</span><span class="sxs-lookup"><span data-stu-id="f203f-152">**How is the standard storage account for diagnostics set up?**</span></span>

<span data-ttu-id="f203f-153">VM 진단을 위한 개인 저장소 계정을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f203f-153">You set up a private storage account for VM diagnostics.</span></span> <span data-ttu-id="f203f-154">향후에는 진단 역시 Managed Disks로 전환할 계획입니다.</span><span class="sxs-lookup"><span data-stu-id="f203f-154">In the future, we plan to switch diagnostics to Managed Disks as well.</span></span>

<span data-ttu-id="f203f-155">**어떤 종류의 역할 기반 액세스 제어 지원을 Managed Disks에 사용할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="f203f-155">**What kind of Role-Based Access Control support is available for Managed Disks?**</span></span>

<span data-ttu-id="f203f-156">Managed Disks에서는 세 가지 주요 기본 역할을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="f203f-156">Managed Disks supports three key default roles:</span></span>

* <span data-ttu-id="f203f-157">소유자: 액세스를 포함한 모든 것을 관리할 수 있음</span><span class="sxs-lookup"><span data-stu-id="f203f-157">Owner: Can manage everything, including access</span></span>
* <span data-ttu-id="f203f-158">참여자: 액세스를 제외한 모든 것을 관리할 수 있음</span><span class="sxs-lookup"><span data-stu-id="f203f-158">Contributor: Can manage everything except access</span></span>
* <span data-ttu-id="f203f-159">읽기 권한자: 모든 항목을 볼 수 있지만 변경할 수 없음</span><span class="sxs-lookup"><span data-stu-id="f203f-159">Reader: Can view everything, but can't make changes</span></span>

<span data-ttu-id="f203f-160">**개인 저장소 계정에 Managed Disk를 복사하거나 내보낼 수 있는 방법이 있나요?**</span><span class="sxs-lookup"><span data-stu-id="f203f-160">**Is there a way that I can copy or export a managed disk to a private storage account?**</span></span>

<span data-ttu-id="f203f-161">관리 디스크에 대한 읽기 전용 공유 액세스 서명 URI를 가져온 후 이를 사용하여 개인 저장소 계정 또는 온-프레미스 저장소에 콘텐츠를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f203f-161">You can get a read-only shared access signature URI for the managed disk and use it to copy the contents to a private storage account or on-premises storage.</span></span>

<span data-ttu-id="f203f-162">**내 관리 디스크의 복사본을 만들 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="f203f-162">**Can I create a copy of my managed disk?**</span></span>

<span data-ttu-id="f203f-163">사용자는 관리 디스크의 스냅숏을 만든 후 이 스냅숏을 사용하여 다른 관리 디스크를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f203f-163">Customers can take a snapshot of their managed disks and then use the snapshot to create another managed disk.</span></span>

<span data-ttu-id="f203f-164">**관리되지 않는 디스크도 계속 지원되나요?**</span><span class="sxs-lookup"><span data-stu-id="f203f-164">**Are unmanaged disks still supported?**</span></span>

<span data-ttu-id="f203f-165">예.</span><span class="sxs-lookup"><span data-stu-id="f203f-165">Yes.</span></span> <span data-ttu-id="f203f-166">관리되지 않는 디스크 및 Managed Disks가 모두 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="f203f-166">We support unmanaged and managed disks.</span></span> <span data-ttu-id="f203f-167">새 워크로드에 대해 Managed Disks를 사용하고 현재 워크로드를 Managed Disks로 마이그레이션하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f203f-167">We recommend that you use managed disks for new workloads and migrate your current workloads to managed disks.</span></span>


<span data-ttu-id="f203f-168">**128GB 디스크를 만든 후 130GB로 크기를 증가시키려는 경우 다음 디스크 크기(512GB)에 대한 요금이 부과되나요?**</span><span class="sxs-lookup"><span data-stu-id="f203f-168">**If I create a 128-GB disk and then increase the size to 130 GB, will I be charged for the next disk size (512 GB)?**</span></span>

<span data-ttu-id="f203f-169">예.</span><span class="sxs-lookup"><span data-stu-id="f203f-169">Yes.</span></span>

<span data-ttu-id="f203f-170">**로컬 중복 저장소, 지역 중복 저장소 및 영역 중복 저장소 Managed Disks를 만들 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="f203f-170">**Can I create locally redundant storage, geo-redundant storage, and zone-redundant storage managed disks?**</span></span>

<span data-ttu-id="f203f-171">Azure Managed Disks에서는 현재 로컬 중복 저장소 Managed Disks만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="f203f-171">Azure Managed Disks currently supports only locally redundant storage managed disks.</span></span>

<span data-ttu-id="f203f-172">**Managed Disks를 축소하거나 크기를 줄일 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="f203f-172">**Can I shrink or downsize my managed disks?**</span></span>

<span data-ttu-id="f203f-173">아니요.</span><span class="sxs-lookup"><span data-stu-id="f203f-173">No.</span></span> <span data-ttu-id="f203f-174">이 기능은 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f203f-174">This feature is not supported currently.</span></span> 

<span data-ttu-id="f203f-175">**VM을 프로비전하는 데 특수화된(시스템 준비 도구를 사용하여 생성되거나 일반화된) 운영 체제 디스크를 사용하는 경우 컴퓨터 이름 속성을 변경할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="f203f-175">**Can I change the computer name property when a specialized (not created by using the System Preparation tool or generalized) operating system disk is used to provision a VM?**</span></span>

<span data-ttu-id="f203f-176">아니요.</span><span class="sxs-lookup"><span data-stu-id="f203f-176">No.</span></span> <span data-ttu-id="f203f-177">컴퓨터 이름 속성은 업데이트할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f203f-177">You can't update the computer name property.</span></span> <span data-ttu-id="f203f-178">새 VM은 운영 체제 디스크를 만들 때 사용한 부모 VM에서 이 속성을 상속합니다.</span><span class="sxs-lookup"><span data-stu-id="f203f-178">The new VM inherits it from the parent VM, which was used to create the operating system disk.</span></span> 

<span data-ttu-id="f203f-179">**Managed Disks를 사용하여 VM을 만드는 Azure Resource Manager 템플릿 예제를 어디에 배치할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="f203f-179">**Where can I find sample Azure Resource Manager templates to create VMs with managed disks?**</span></span>
* [<span data-ttu-id="f203f-180">Managed Disks를 사용하는 템플릿 목록</span><span class="sxs-lookup"><span data-stu-id="f203f-180">List of templates using Managed Disks</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)
* <span data-ttu-id="f203f-181">https://github.com/chagarw/MDPP</span><span class="sxs-lookup"><span data-stu-id="f203f-181">https://github.com/chagarw/MDPP</span></span>

## <a name="managed-disks-and-storage-service-encryption"></a><span data-ttu-id="f203f-182">Managed Disks 및 Storage 서비스 암호화</span><span class="sxs-lookup"><span data-stu-id="f203f-182">Managed Disks and Storage Service Encryption</span></span> 

<span data-ttu-id="f203f-183">**Managed Disk를 만들 경우 Azure Storage 서비스 암호화를 기본적으로 사용하나요?**</span><span class="sxs-lookup"><span data-stu-id="f203f-183">**Is Azure Storage Service Encryption enabled by default when I create a managed disk?**</span></span>

<span data-ttu-id="f203f-184">예.</span><span class="sxs-lookup"><span data-stu-id="f203f-184">Yes.</span></span>

<span data-ttu-id="f203f-185">**암호화 키는 누가 관리하나요?**</span><span class="sxs-lookup"><span data-stu-id="f203f-185">**Who manages the encryption keys?**</span></span>

<span data-ttu-id="f203f-186">Microsoft에서 암호화 키를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="f203f-186">Microsoft manages the encryption keys.</span></span>

<span data-ttu-id="f203f-187">**내 Managed Disks에 Storage 서비스 암호화를 비활성화할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="f203f-187">**Can I disable Storage Service Encryption for my managed disks?**</span></span>

<span data-ttu-id="f203f-188">아니요.</span><span class="sxs-lookup"><span data-stu-id="f203f-188">No.</span></span>

<span data-ttu-id="f203f-189">**Storage 서비스 암호화는 특정 지역에서만 사용할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="f203f-189">**Is Storage Service Encryption only available in specific regions?**</span></span>

<span data-ttu-id="f203f-190">아니요.</span><span class="sxs-lookup"><span data-stu-id="f203f-190">No.</span></span> <span data-ttu-id="f203f-191">Managed Disks를 사용할 수 있는 모든 지역에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f203f-191">It's available in all the regions where Managed Disks is available.</span></span> <span data-ttu-id="f203f-192">모든 공용 지역 및 독일에서 Managed Disks를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f203f-192">Managed Disks is available in all public regions and Germany.</span></span>

<span data-ttu-id="f203f-193">**내 Managed Disk가 암호화되었는지 어떻게 확인할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="f203f-193">**How can I find out if my managed disk is encrypted?**</span></span>

<span data-ttu-id="f203f-194">Azure Portal, Azure CLI 및 PowerShell에서 Managed Disk를 만든 시간을 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f203f-194">You can find out the time when a managed disk was created from the Azure portal, the Azure CLI, and PowerShell.</span></span> <span data-ttu-id="f203f-195">2017년 6월 9일 이후인 경우 디스크는 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="f203f-195">If the time is after June 9, 2017, then your disk is encrypted.</span></span> 

<span data-ttu-id="f203f-196">**2017년 6월 10일 이전에 만들어진 내 기존 디스크를 어떻게 암호화할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="f203f-196">**How can I encrypt my existing disks that were created before June 10, 2017?**</span></span>

<span data-ttu-id="f203f-197">2017년 6월 10일을 기준으로 기존 Managed Disks에 작성된 새 데이터는 자동으로 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="f203f-197">As of June 10, 2017, new data written to existing managed disks is automatically encrypted.</span></span> <span data-ttu-id="f203f-198">기존 데이터를 암호화할 예정이며 암호화는 백그라운드에서 비동기적으로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="f203f-198">We are also planning to encrypt existing data, and the encryption will happen asynchronously in the background.</span></span> <span data-ttu-id="f203f-199">이제 기존 데이터를 암호화해야 하는 경우 디스크의 복사본을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f203f-199">If you must encrypt existing data now, create a copy of your disk.</span></span> <span data-ttu-id="f203f-200">새 디스크가 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="f203f-200">New disks will be encrypted.</span></span>

* [<span data-ttu-id="f203f-201">Azure CLI를 사용하여 Managed Disks 복사</span><span class="sxs-lookup"><span data-stu-id="f203f-201">Copy managed disks by using the Azure CLI</span></span>](https://docs.microsoft.com/en-us/azure/storage/scripts/storage-linux-cli-sample-copy-managed-disks-to-same-or-different-subscription?toc=%2fcli%2fmodule%2ftoc.json)
* [<span data-ttu-id="f203f-202">PowerShell을 사용하여 Managed Disks 복사</span><span class="sxs-lookup"><span data-stu-id="f203f-202">Copy managed disks by using PowerShell</span></span>](https://docs.microsoft.com/en-us/azure/storage/scripts/storage-windows-powershell-sample-copy-managed-disks-to-same-or-different-subscription?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="f203f-203">**관리되는 스냅숏 및 이미지가 암호화되나요?**</span><span class="sxs-lookup"><span data-stu-id="f203f-203">**Are managed snapshots and images encrypted?**</span></span>

<span data-ttu-id="f203f-204">예.</span><span class="sxs-lookup"><span data-stu-id="f203f-204">Yes.</span></span> <span data-ttu-id="f203f-205">2017년 6월 9일 이후에 만든 모든 관리되는 스냅숏 및 이미지는 자동으로 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="f203f-205">All managed snapshots and images created after June 9, 2017, are automatically encrypted.</span></span> 

<span data-ttu-id="f203f-206">**Managed Disks에 이전에 암호화된 저장소 계정에 있는 관리되지 않는 디스크가 있는 VM을 변환할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="f203f-206">**Can I convert VMs with unmanaged disks that are located on storage accounts that are or were previously encrypted to managed disks?**</span></span>

<span data-ttu-id="f203f-207">예</span><span class="sxs-lookup"><span data-stu-id="f203f-207">Yes</span></span>

<span data-ttu-id="f203f-208">**Managed Disk 또는 스냅숏에서 내보낸 VHD도 암호화되나요?**</span><span class="sxs-lookup"><span data-stu-id="f203f-208">**Will an exported VHD from a managed disk or a snapshot also be encrypted?**</span></span>

<span data-ttu-id="f203f-209">아니요.</span><span class="sxs-lookup"><span data-stu-id="f203f-209">No.</span></span> <span data-ttu-id="f203f-210">하지만 암호화된 Managed Disk 또는 스냅숏의 암호화된 저장소 계정에 VHD를 내보낼 경우 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="f203f-210">But if you export a VHD to an encrypted storage account from an encrypted managed disk or snapshot, then it's encrypted.</span></span> 

## <a name="premium-disks-managed-and-unmanaged"></a><span data-ttu-id="f203f-211">프리미엄 디스크: 관리 및 관리되지 않는 디스크</span><span class="sxs-lookup"><span data-stu-id="f203f-211">Premium disks: Managed and unmanaged</span></span>

<span data-ttu-id="f203f-212">**VM에서 DSv2와 같이 Premium Storage를 지원하는 크기를 사용하는 경우 프리미엄 및 표준 데이터 디스크를 모두 연결할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="f203f-212">**If a VM uses a size series that supports Premium Storage, such as a DSv2, can I attach both premium and standard data disks?**</span></span> 

<span data-ttu-id="f203f-213">예.</span><span class="sxs-lookup"><span data-stu-id="f203f-213">Yes.</span></span>

<span data-ttu-id="f203f-214">**프리미엄 및 표준 데이터 디스크를 모두 D, Dv2, G 또는 F 시리즈와 같이 Premium Storage를 지원하지 않는 크기에 연결할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="f203f-214">**Can I attach both premium and standard data disks to a size series that doesn't support Premium Storage, such as D, Dv2, G, or F series?**</span></span>

<span data-ttu-id="f203f-215">아니요.</span><span class="sxs-lookup"><span data-stu-id="f203f-215">No.</span></span> <span data-ttu-id="f203f-216">Premium Storage를 지원하는 크기를 사용하지 않는 VM에는 표준 데이터 디스크만 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f203f-216">You can attach only standard data disks to VMs that don't use a size series that supports Premium Storage.</span></span>

<span data-ttu-id="f203f-217">**80GB인 기존 VHD로 프리미엄 데이터 디스크를 만들 경우 비용은 얼마가 드나요?**</span><span class="sxs-lookup"><span data-stu-id="f203f-217">**If I create a premium data disk from an existing VHD that was 80 GB, how much will that cost?**</span></span>

<span data-ttu-id="f203f-218">80GB VHD에서 만든 프리미엄 데이터 디스크는 그 다음 프리미엄 디스크 크기인 P10으로 취급됩니다.</span><span class="sxs-lookup"><span data-stu-id="f203f-218">A premium data disk created from an 80-GB VHD is treated as the next-available premium disk size, which is a P10 disk.</span></span> <span data-ttu-id="f203f-219">P10 디스크 가격 책정에 따라 요금이 부과됩니다.</span><span class="sxs-lookup"><span data-stu-id="f203f-219">You're charged according to the P10 disk pricing.</span></span>

<span data-ttu-id="f203f-220">**Premium Storage를 사용하면 트랜잭션 비용이 있나요?**</span><span class="sxs-lookup"><span data-stu-id="f203f-220">**Are there transaction costs to use Premium Storage?**</span></span>

<span data-ttu-id="f203f-221">특정 한도의 IOPS 및 처리량이 프로비전되는 디스크 크기마다 고정 비용이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f203f-221">There is a fixed cost for each disk size, which comes provisioned with specific limits on IOPS and throughput.</span></span> <span data-ttu-id="f203f-222">기타 비용은 아웃바운드 대역폭 및 스냅숏 용량입니다(해당하는 경우).</span><span class="sxs-lookup"><span data-stu-id="f203f-222">The other costs are outbound bandwidth and snapshot capacity, if applicable.</span></span> <span data-ttu-id="f203f-223">자세한 내용은 [가격 책정 페이지](https://azure.microsoft.com/pricing/details/storage)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f203f-223">For more information, see the [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="f203f-224">**디스크 캐시에서 가져올 수 있는 IOPS 및 처리량 한도는 얼마나 되나요?**</span><span class="sxs-lookup"><span data-stu-id="f203f-224">**What are the limits for IOPS and throughput that I can get from the disk cache?**</span></span>

<span data-ttu-id="f203f-225">DS 시리즈의 캐시 및 로컬 SSD에 대한 결합 제한은 코어당 4,000 IOPS 및 코어당 초당 33MB입니다.</span><span class="sxs-lookup"><span data-stu-id="f203f-225">The combined limits for cache and local SSD for a DS series are 4,000 IOPS per core and 33 MB per second per core.</span></span> <span data-ttu-id="f203f-226">GS 시리즈는 코어당 5,000 IOPS 및 코어당 초당 50MB를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f203f-226">The GS series offers 5,000 IOPS per core and 50 MB per second per core.</span></span>

<span data-ttu-id="f203f-227">**Managed Disks VM에 로컬 SSD가 지원되나요?**</span><span class="sxs-lookup"><span data-stu-id="f203f-227">**Is the local SSD supported for a Managed Disks VM?**</span></span>

<span data-ttu-id="f203f-228">로컬 SSD는 Managed Disks VM에 포함되어 있는 임시 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="f203f-228">The local SSD is temporary storage that is included with a Managed Disks VM.</span></span> <span data-ttu-id="f203f-229">이 임시 저장소에 대한 추가 비용은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f203f-229">There is no extra cost for this temporary storage.</span></span> <span data-ttu-id="f203f-230">이 로컬 SSD가 Azure Blob Storage에 보존되지 않기 때문에 응용 프로그램 데이터를 저장하는 데 사용하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f203f-230">We recommend that you do not use this local SSD to store your application data because it isn't persisted in Azure Blob storage.</span></span>

<span data-ttu-id="f203f-231">**프리미엄 디스크에서 TRIM의 사용에 대한 영향이 있나요?**</span><span class="sxs-lookup"><span data-stu-id="f203f-231">**Are there any repercussions for the use of TRIM on premium disks?**</span></span>

<span data-ttu-id="f203f-232">프리미엄 또는 표준 디스크의 Azure 디스크에서 TRIM을 사용해도 문제는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f203f-232">There is no downside to the use of TRIM on Azure disks on either premium or standard disks.</span></span>

## <a name="new-disk-sizes-managed-and-unmanaged"></a><span data-ttu-id="f203f-233">새 디스크 크기: 관리 및 관리되지 않는 디스크</span><span class="sxs-lookup"><span data-stu-id="f203f-233">New disk sizes: Managed and unmanaged</span></span>

<span data-ttu-id="f203f-234">**운영 체제 및 데이터 디스크에 지원되는 가장 큰 디스크 크기는 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="f203f-234">**What is the largest disk size supported for operating system and data disks?**</span></span>

<span data-ttu-id="f203f-235">Azure에서 운영 체제 디스크에 지원하는 파티션 형식은 MBR(마스터 부트 레코드)입니다.</span><span class="sxs-lookup"><span data-stu-id="f203f-235">The partition type that Azure supports for an operating system disk is the master boot record (MBR).</span></span> <span data-ttu-id="f203f-236">MBR 형식은 최대 2TB의 디스크를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="f203f-236">The MBR format supports a disk size up to 2 TB.</span></span> <span data-ttu-id="f203f-237">Azure에서 운영 체제 디스크에 지원하는 최대 크기는 2TB입니다.</span><span class="sxs-lookup"><span data-stu-id="f203f-237">The largest size that Azure supports for an operating system disk is 2 TB.</span></span> <span data-ttu-id="f203f-238">Azure는 데이터 디스크에 최대 4TB를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="f203f-238">Azure supports up to 4 TB for data disks.</span></span> 

<span data-ttu-id="f203f-239">**지원되는 가장 큰 페이지 Blob 크기는 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="f203f-239">**What is the largest page blob size that's supported?**</span></span>

<span data-ttu-id="f203f-240">Azure에서 지원하는 페이지 Blob 크기는 최대 8TB(8,191GB)입니다.</span><span class="sxs-lookup"><span data-stu-id="f203f-240">The largest page blob size that Azure supports is 8 TB (8,191 GB).</span></span> <span data-ttu-id="f203f-241">데이터 또는 운영 체제 디스크로 VM에 연결된 4TB(4,095GB)를 초과하는 페이지 blob는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f203f-241">We don't support page blobs larger than 4 TB (4,095 GB) attached to a VM as data or operating system disks.</span></span>

<span data-ttu-id="f203f-242">**새 버전의 Azure 도구를 사용하여 1TB를 초과하는 디스크를 생성, 연결, 크기 조정 및 업로드해야 하나요?**</span><span class="sxs-lookup"><span data-stu-id="f203f-242">**Do I need to use a new version of Azure tools to create, attach, resize, and upload disks larger than 1 TB?**</span></span>

<span data-ttu-id="f203f-243">1TB를 초과하는 디스크를 생성, 연결 또는 크기 조정하기 위해 기존 Azure 도구를 업그레이드할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f203f-243">You don't need to upgrade your existing Azure tools to create, attach, or resize disks larger than 1 TB.</span></span> <span data-ttu-id="f203f-244">페이지 Blob 또는 관리되지 않는 디스크와 같이 온-프레미스에서 Azure에 직접 VHD 파일을 업로드하려면 최신 도구 집합을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f203f-244">To upload your VHD file from on-premises directly to Azure as a page blob or unmanaged disk, you need to use the latest tool sets:</span></span>

|<span data-ttu-id="f203f-245">Azure 도구</span><span class="sxs-lookup"><span data-stu-id="f203f-245">Azure tools</span></span>      | <span data-ttu-id="f203f-246">지원되는 버전</span><span class="sxs-lookup"><span data-stu-id="f203f-246">Supported versions</span></span>                                |
|-----------------|---------------------------------------------------|
|<span data-ttu-id="f203f-247">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="f203f-247">Azure PowerShell</span></span> | <span data-ttu-id="f203f-248">버전 번호 4.1.0: 2017년 6월 릴리스 이상</span><span class="sxs-lookup"><span data-stu-id="f203f-248">Version number 4.1.0: June 2017 release or later</span></span>|
|<span data-ttu-id="f203f-249">Azure CLI v1</span><span class="sxs-lookup"><span data-stu-id="f203f-249">Azure CLI v1</span></span>     | <span data-ttu-id="f203f-250">버전 번호 0.10.13: 2017년 5월 릴리스 이상</span><span class="sxs-lookup"><span data-stu-id="f203f-250">Version number 0.10.13: May 2017 release or later</span></span>|
|<span data-ttu-id="f203f-251">AzCopy</span><span class="sxs-lookup"><span data-stu-id="f203f-251">AzCopy</span></span>           | <span data-ttu-id="f203f-252">버전 번호 6.1.0: 2017년 6월 릴리스 이상</span><span class="sxs-lookup"><span data-stu-id="f203f-252">Version number 6.1.0: June 2017 release or later</span></span>|

<span data-ttu-id="f203f-253">Azure CLI v2 및 Azure Storage Explorer에 대한 지원이 곧 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="f203f-253">The support for Azure CLI v2 and Azure Storage Explorer is coming soon.</span></span> 

<span data-ttu-id="f203f-254">**P4 및 P6 디스크 크기가 관리되지 않는 디스크 또는 페이지 Blob에 지원되나요?**</span><span class="sxs-lookup"><span data-stu-id="f203f-254">**Are P4 and P6 disk sizes supported for unmanaged disks or page blobs?**</span></span>

<span data-ttu-id="f203f-255">아니요.</span><span class="sxs-lookup"><span data-stu-id="f203f-255">No.</span></span> <span data-ttu-id="f203f-256">P4(32GB) 및 P6(64GB) 디스크 크기는 Managed Disks에만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="f203f-256">P4 (32 GB) and P6 (64 GB) disk sizes are supported only for managed disks.</span></span> <span data-ttu-id="f203f-257">관리되지 않는 디스크 및 페이지 Blob에도 곧 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="f203f-257">Support for unmanaged disks and page blobs is coming soon.</span></span>

<span data-ttu-id="f203f-258">**작은 디스크를 사용하기 전에 64GB 미만인 기존 프리미엄 Managed Disks를 만든 경우(2017년 6월 15일경) 어떻게 청구되나요?**</span><span class="sxs-lookup"><span data-stu-id="f203f-258">**If my existing premium managed disk less than 64 GB was created before the small disk was enabled (around June 15, 2017), how is it billed?**</span></span>

<span data-ttu-id="f203f-259">64GB 미만의 기존 프리미엄 디스크는 P10 가격 책정 계층에 따라 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="f203f-259">Existing small premium disks less than 64 GB continue to be billed according to the P10 pricing tier.</span></span> 

<span data-ttu-id="f203f-260">**P4 또는 P6 P10에서 64GB 미만인 작은 프리미엄 디스크의 디스크 계층을 전환하려면 어떻게 해야 하나요?**</span><span class="sxs-lookup"><span data-stu-id="f203f-260">**How can I switch the disk tier of small premium disks less than 64 GB from P10 to P4 or P6?**</span></span>

<span data-ttu-id="f203f-261">작은 디스크의 스냅숏을 찍고 디스크를 만들어서 프로비전된 크기에 따라 P4 또는 P6으로 가격 책정 계층을 자동으로 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f203f-261">You can take a snapshot of your small disks and then create a disk to automatically switch the pricing tier to P4 or P6 based on the provisioned size.</span></span> 


## <a name="what-if-my-question-isnt-answered-here"></a><span data-ttu-id="f203f-262">여기서 내 질문에 대답하지 않으면 어떻게 하나요?</span><span class="sxs-lookup"><span data-stu-id="f203f-262">What if my question isn't answered here?</span></span>

<span data-ttu-id="f203f-263">질문하려는 내용이 아래 목록에 나와 있지 않으면 알려 주세요. 대답을 확인하는 방법을 알려 드리겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f203f-263">If your question isn't listed here, let us know and we'll help you find an answer.</span></span> <span data-ttu-id="f203f-264">설명에 있는 이 문서의 끝에 질문을 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f203f-264">You can post a question at the end of this article in the comments.</span></span> <span data-ttu-id="f203f-265">Azure Storage 팀 및 다른 커뮤니티 구성원과 이 문서에 대한 의견을 교환하려면 MSDN [Azure Storage 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f203f-265">To engage with the Azure Storage team and other community members about this article, use the MSDN [Azure Storage forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata).</span></span>

<span data-ttu-id="f203f-266">기능을 요청하려면 요청 내용과 아이디어를 [Azure Storage 피드백 포럼](https://feedback.azure.com/forums/217298-storage)으로 제출해 주세요.</span><span class="sxs-lookup"><span data-stu-id="f203f-266">To request features, submit your requests and ideas to the [Azure Storage feedback forum](https://feedback.azure.com/forums/217298-storage).</span></span>
