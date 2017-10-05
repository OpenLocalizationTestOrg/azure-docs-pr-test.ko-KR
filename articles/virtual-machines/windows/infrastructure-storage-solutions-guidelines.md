---
title: "Windows VM에 대한 Azure Storage 솔루션 | Microsoft Docs"
description: "Azure 인프라 서비스에서 저장소 솔루션을 배포하기 위한 핵심 디자인 및 구현 지침에 대해 알아봅니다."
documentationcenter: 
services: virtual-machines-windows
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4ceb7d32-7a0d-4004-b701-c2bbcaff6b0b
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ba0d66c5af771ebcb3ca8e6742e15a5506d8fd61
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-storage-infrastructure-guidelines-for-windows-vms"></a><span data-ttu-id="00eba-103">Windows VM에 대한 Azure Storage 인프라 지침</span><span class="sxs-lookup"><span data-stu-id="00eba-103">Azure storage infrastructure guidelines for Windows VMs</span></span>

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

<span data-ttu-id="00eba-104">이 문서에서는 최적의 VM(가상 컴퓨터) 성능을 위한 저장소 요구 사항 및 디자인 고려 사항을 이해하는 데 주안점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="00eba-104">This article focuses on understanding storage needs and design considerations for achieving optimum virtual machine (VM) performance.</span></span>

## <a name="implementation-guidelines-for-storage"></a><span data-ttu-id="00eba-105">저장소에 대한 구현 지침</span><span class="sxs-lookup"><span data-stu-id="00eba-105">Implementation guidelines for storage</span></span>
<span data-ttu-id="00eba-106">의사 결정:</span><span class="sxs-lookup"><span data-stu-id="00eba-106">Decisions:</span></span>

* <span data-ttu-id="00eba-107">Azure Managed Disks를 사용할 것인가? 아니면 관리되지 않는 디스크를 사용할 것인가?</span><span class="sxs-lookup"><span data-stu-id="00eba-107">Are you going to use Azure Managed Disks or unmanaged disks?</span></span>
* <span data-ttu-id="00eba-108">작업을 위해 표준 저장소를 사용해야 하나? 아니면 프리미엄 저장소를 사용해야 하나?</span><span class="sxs-lookup"><span data-stu-id="00eba-108">Do you need to use Standard or Premium storage for your workload?</span></span>
* <span data-ttu-id="00eba-109">4TB보다 큰 디스크를 만들기 위해 디스크 스트라이프가 필요한가?</span><span class="sxs-lookup"><span data-stu-id="00eba-109">Do you need disk striping to create disks larger than 4TB?</span></span>
* <span data-ttu-id="00eba-110">작업에 대한 최적의 I/O 성능을 얻기 위해 디스크 스트라이프가 필요한가?</span><span class="sxs-lookup"><span data-stu-id="00eba-110">Do you need disk striping to achieve optimal I/O performance for your workload?</span></span>
* <span data-ttu-id="00eba-111">IT 작업 또는 인프라를 호스트하는 데 필요한 저장소 계정 집합은 무엇인가?</span><span class="sxs-lookup"><span data-stu-id="00eba-111">What set of storage accounts do you need to host your IT workload or infrastructure?</span></span>

<span data-ttu-id="00eba-112">작업:</span><span class="sxs-lookup"><span data-stu-id="00eba-112">Tasks:</span></span>

* <span data-ttu-id="00eba-113">배포하는 응용 프로그램의 I/O 요구를 검토하고 저장소 계정의 적절한 수와 유형을 계획합니다.</span><span class="sxs-lookup"><span data-stu-id="00eba-113">Review I/O demands of the applications you are deploying and plan the appropriate number and type of storage accounts.</span></span>
* <span data-ttu-id="00eba-114">명명 규칙을 사용하여 저장소 계정 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="00eba-114">Create the set of storage accounts using your naming convention.</span></span> <span data-ttu-id="00eba-115">Azure PowerShell 또는 포털을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00eba-115">You can use Azure PowerShell or the portal.</span></span>

## <a name="storage"></a><span data-ttu-id="00eba-116">저장소</span><span class="sxs-lookup"><span data-stu-id="00eba-116">Storage</span></span>
<span data-ttu-id="00eba-117">Azure 저장소는 VM(가상 컴퓨터) 및 응용 프로그램의 배포 및 관리 작업의 핵심 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="00eba-117">Azure Storage is a key part of deploying and managing virtual machines (VMs) and applications.</span></span> <span data-ttu-id="00eba-118">Azure 저장소는 파일 데이터, 구조화되지 않은 데이터 및 메시지를 저장하기 위한 서비스를 제공하며, VM을 지원하는 인프라의 일부이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="00eba-118">Azure Storage provides services for storing file data, unstructured data, and messages, and it is also part of the infrastructure supporting VMs.</span></span>

<span data-ttu-id="00eba-119">[Azure Managed Disks](../../storage/storage-managed-disks-overview.md)는 배후에서 저장소를 처리해 줍니다.</span><span class="sxs-lookup"><span data-stu-id="00eba-119">[Azure Managed Disks](../../storage/storage-managed-disks-overview.md) handles storage for you behind the scenes.</span></span> <span data-ttu-id="00eba-120">관리되지 않는 디스크를 사용하는 경우 Azure VM의 디스크(VHD 파일)를 갖기 위해 저장소 계정을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00eba-120">With unmanaged disks, you create storage accounts to hold the disks (VHD files) for your Azure VMs.</span></span> <span data-ttu-id="00eba-121">확장하는 경우에는 디스크를 포함하는 저장소의 IOPS 제한을 초과하지 않도록 저장소 계정을 추가로 만들었는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00eba-121">When scaling up, you must make sure you created additional storage accounts so you don’t exceed the IOPS limit for storage with any of your disks.</span></span> <span data-ttu-id="00eba-122">Managed Disks로 저장소를 처리하면 저장소 계정 한도(예: 20,000 IOPS/계정)로 인해 더 이상 제한을 받지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="00eba-122">With Managed Disks handling storage, you are no longer limited by the storage account limits (such as 20,000 IOPS / account).</span></span> <span data-ttu-id="00eba-123">사용자 지정 이미지(VHD 파일)를 여러 저장소 계정에 복사할 필요도 없습니다.</span><span class="sxs-lookup"><span data-stu-id="00eba-123">You also no longer have to copy your custom images (VHD files) to multiple storage accounts.</span></span> <span data-ttu-id="00eba-124">중앙 위치(Azure 지역당 하나의 저장소 계정)에서 저장소 계정을 관리할 수 있고 이를 통해 구독에 수백 개의 VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00eba-124">You can manage them in a central location – one storage account per Azure region – and use them to create hundreds of VMs in a subscription.</span></span> <span data-ttu-id="00eba-125">새 배포에 Managed Disks를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="00eba-125">We recommend you use Managed Disks for new deployments.</span></span>

<span data-ttu-id="00eba-126">VM 지원을 위해 다음 두 가지 저장소 계정 유형을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00eba-126">There are two types of storage accounts available for supporting VMs:</span></span>

* <span data-ttu-id="00eba-127">Standard 저장소 계정은 Blob 저장소(Azure VM 디스크를 저장하는 데 사용), 테이블 저장소, 큐 저장소 및 파일 저장소에 대한 액세스 권한을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="00eba-127">Standard storage accounts give you access to blob storage (used for storing Azure VM disks), table storage, queue storage, and file storage.</span></span>
* <span data-ttu-id="00eba-128">[Premium 저장소](../../storage/storage-premium-storage.md) 계정은 AlwaysOn 클러스터의 SQL Server와 같이 I/O 집약적 워크로드에 대해 대기 시간이 낮은 고성능 디스크 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="00eba-128">[Premium storage](../../storage/storage-premium-storage.md) accounts deliver high-performance, low-latency disk support for I/O intensive workloads, such as SQL Servers in an AlwaysOn cluster.</span></span> <span data-ttu-id="00eba-129">Premium 저장소는 현재 Azure VM 디스크만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="00eba-129">Premium storage currently supports Azure VM disks only.</span></span>

<span data-ttu-id="00eba-130">Azure는 운영 체제 디스크, 임시 디스크를 및 0개 이상의 선택적 데이터 디스크로 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="00eba-130">Azure creates VMs with an operating system disk, a temporary disk, and zero or more optional data disks.</span></span> <span data-ttu-id="00eba-131">운영 체제 디스크 및 데이터 디스크는 Azure 페이지 Blob이지만 임시 디스크는 컴퓨터가 있는 노드에 로컬로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="00eba-131">The operating system disk and data disks are Azure page blobs, whereas the temporary disk is stored locally on the node where the machine lives.</span></span> <span data-ttu-id="00eba-132">VM은 유지 관리 이벤트 동안 호스트 간에 마이그레이션될 수 있으므로 응용 프로그램을 디자인할 때는 비영구 데이터에 대해 이러한 임시 디스크만 사용하도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00eba-132">Take care when designing applications to only use this temporary disk for non-persistent data as the VM may be migrated between hosts during a maintenance event.</span></span> <span data-ttu-id="00eba-133">임시 디스크에 저장된 모든 데이터는 손실됩니다.</span><span class="sxs-lookup"><span data-stu-id="00eba-133">Any data stored on the temporary disk would be lost.</span></span>

<span data-ttu-id="00eba-134">계획되지 않은 유지 관리 또는 하드웨어 오류로부터 데이터를 보호하기 위해 기본 Azure Storage 환경에서는 내구성 및 고가용성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="00eba-134">Durability and high availability is provided by the underlying Azure Storage environment to ensure that your data remains protected against unplanned maintenance or hardware failures.</span></span> <span data-ttu-id="00eba-135">Azure Storage 환경을 디자인하는 경우에 VM 저장소를 복제 하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00eba-135">As you design your Azure Storage environment, you can choose to replicate VM storage:</span></span>

* <span data-ttu-id="00eba-136">지정된 Azure 데이터 센터 내에서 로컬로</span><span class="sxs-lookup"><span data-stu-id="00eba-136">locally within a given Azure datacenter</span></span>
* <span data-ttu-id="00eba-137">지정된 지역 내에서 Azure 데이터 센터에서</span><span class="sxs-lookup"><span data-stu-id="00eba-137">across Azure datacenters within a given region</span></span>
* <span data-ttu-id="00eba-138">서로 다른 지역의 Azure 데이터 센터에서</span><span class="sxs-lookup"><span data-stu-id="00eba-138">across Azure datacenters across different regions</span></span>

<span data-ttu-id="00eba-139">[고가용성을 위한 복제 옵션에 대해 좀 더 자세히](../../storage/storage-introduction.md#replication-for-durability-and-high-availability)읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="00eba-139">You can read [more about the replication options for high availability](../../storage/storage-introduction.md#replication-for-durability-and-high-availability).</span></span>

<span data-ttu-id="00eba-140">운영 체제 디스크 및 데이터 디스크의 최대 크기는 4TB입니다.</span><span class="sxs-lookup"><span data-stu-id="00eba-140">Operating system disks and data disks have a maximum size of 4TB.</span></span> <span data-ttu-id="00eba-141">Windows Server 2012 이상의 저장 공간을 사용하면 데이터 디스크를 함께 풀링하여 4TB보다 큰 논리 볼륨을 VM에 제공함으로써 이러한 제한을 극복할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00eba-141">You can use Storage Spaces in Windows Server 2012 or later to surpass this limit by pooling together data disks to present logical volumes larger than 4TB to your VM.</span></span>

<span data-ttu-id="00eba-142">Azure Storage 배포를 디자인할 때는 확장성이 어느 정도 제한될 수 있습니다. 자세한 내용은 [Microsoft Azure 구독 및 서비스 제한, 할당량 및 제약 조건](../../azure-subscription-service-limits.md#storage-limits)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="00eba-142">There are some scalability limits when designing your Azure Storage deployments - for more information, see [Microsoft Azure subscription and service limits, quotas, and constraints](../../azure-subscription-service-limits.md#storage-limits).</span></span> <span data-ttu-id="00eba-143">[Azure Storage 확장성 및 성능 목표](../../storage/storage-scalability-targets.md)도 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="00eba-143">Also see [Azure storage scalability and performance targets](../../storage/storage-scalability-targets.md).</span></span>

<span data-ttu-id="00eba-144">응용 프로그램 저장소의 경우 문서, 이미지, 백업, 구성 데이터, 로그 등의 구조화되지 않은 개체 데이터를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00eba-144">For application storage, you can store unstructured object data such as documents, images, backups, configuration data, logs, etc.</span></span> <span data-ttu-id="00eba-145">Blob Storage를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="00eba-145">using blob storage.</span></span> <span data-ttu-id="00eba-146">응용 프로그램이 VM에 연결된 가상 디스크에 쓰는 대신, Azure Blob 저장소에 직접 쓸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00eba-146">Rather than your application writing to a virtual disk attached to the VM, the application can write directly to Azure blob storage.</span></span> <span data-ttu-id="00eba-147">Blob Storage는 가용성 요구와 비용 제약에 따라 [핫 및 콜드 저장소 계층](../../storage/storage-blob-storage-tiers.md) 옵션도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="00eba-147">Blob storage also provides the option of [hot and cool storage tiers](../../storage/storage-blob-storage-tiers.md) depending on your availability needs and cost constraints.</span></span>

## <a name="striped-disks"></a><span data-ttu-id="00eba-148">스트라이프 디스크</span><span class="sxs-lookup"><span data-stu-id="00eba-148">Striped disks</span></span>
<span data-ttu-id="00eba-149">데이터 디스크의 스트라이프는 대부분의 경우에 4TB보다 큰 디스크를 만들 수 있을 뿐만 아니라 단일 볼륨에 대한 저장소를 지원하기 위해 여러 blob을 허용하여 성능을 강화합니다.</span><span class="sxs-lookup"><span data-stu-id="00eba-149">Besides allowing you to create disks larger than 4TB, in many instances, using striping for data disks enhances performance by allowing multiple blobs to back the storage for a single volume.</span></span> <span data-ttu-id="00eba-150">스트라이프에서는 단일 논리적 디스크에서 데이터를 읽고 쓰는 데 필요한 I/O가 병렬로 진행됩니다.</span><span class="sxs-lookup"><span data-stu-id="00eba-150">With striping, the I/O required to write and read data from a single logical disk proceeds in parallel.</span></span>

<span data-ttu-id="00eba-151">Azure는 VM 크기에 따라 사용 가능한 데이터 디스크 수 및 대역폭의 양에 제한을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="00eba-151">Azure imposes limits on the number of data disks and amount of bandwidth available, depending on the VM size.</span></span> <span data-ttu-id="00eba-152">자세한 내용은 [가상 컴퓨터의 크기](sizes.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="00eba-152">For details, see [Sizes for virtual machines](sizes.md).</span></span>

<span data-ttu-id="00eba-153">Azure 데이터 디스크에 디스크 스트라이프를 사용하고 있는 경우 다음 지침을 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="00eba-153">If you are using disk striping for Azure data disks, consider the following guidelines:</span></span>

* <span data-ttu-id="00eba-154">VM 크기에 허용된 최대 데이터 디스크를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="00eba-154">Attach the maximum data disks allowed for the VM size.</span></span>
* <span data-ttu-id="00eba-155">저장소 공간을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="00eba-155">Use Storage Spaces.</span></span>
* <span data-ttu-id="00eba-156">Azure 데이터 디스크 캐싱 옵션을 사용하지 않습니다(캐싱 정책 = 없음).</span><span class="sxs-lookup"><span data-stu-id="00eba-156">Avoid using Azure data disk caching options (caching policy = None).</span></span>

<span data-ttu-id="00eba-157">자세한 내용은 [저장소 공간 - 성능을 높이기 위한 설계](http://social.technet.microsoft.com/wiki/contents/articles/15200.storage-spaces-designing-for-performance.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="00eba-157">For more information, see [Storage spaces - designing for performance](http://social.technet.microsoft.com/wiki/contents/articles/15200.storage-spaces-designing-for-performance.aspx).</span></span>

## <a name="multiple-storage-accounts"></a><span data-ttu-id="00eba-158">여러 저장소 계정</span><span class="sxs-lookup"><span data-stu-id="00eba-158">Multiple storage accounts</span></span>
<span data-ttu-id="00eba-159">별도의 저장소 계정을 만들지 않으므로 이 섹션은 [Azure Managed Disks](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)에 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="00eba-159">This section does not apply to [Azure Managed Disks](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), as you do not create separate storage accounts.</span></span> 

<span data-ttu-id="00eba-160">관리되지 않는 디스크에 대한 Azure Storage 환경을 디자인할 때 배포하는 VM 수가 증가할 경우 여러 저장소 계정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00eba-160">When designing your Azure Storage environment for unmanaged disks, you can use multiple storage accounts as the number of VMs you deploy increases.</span></span> <span data-ttu-id="00eba-161">이 방법을 사용하면 기본 Azure Storage 인프라 전반에 I/O가 분산되므로 VM 및 응용 프로그램에 대해 최적의 성능을 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00eba-161">This approach helps distribute out the I/O across the underlying Azure Storage infrastructure to maintain optimum performance for your VMs and applications.</span></span> <span data-ttu-id="00eba-162">배포하는 응용 프로그램을 디자인할 때는 각 VM의 I/O 요구 사항을 고려하고 Azure Storage 계정에 이러한 I/O를 분산해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00eba-162">As you design the applications that you are deploying, consider the I/O requirements each VM has and balance out those VMs across Azure Storage accounts.</span></span> <span data-ttu-id="00eba-163">I/O 요구가 높은 모든 VM을 하나 또는 두 개의 저장소 계정으로만 그룹화하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="00eba-163">Try to avoid grouping all the high I/O demanding VMs in to just one or two storage accounts.</span></span>

<span data-ttu-id="00eba-164">다른 Azure Storage 옵션의 I/O 기능 및 일부 권장 최대값에 대한 자세한 내용은 [Azure 저장소 확장성 및 성능 목표](../../storage/storage-scalability-targets.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="00eba-164">For more information about the I/O capabilities of the different Azure Storage options and some recommend maximums, see [Azure storage scalability and performance targets](../../storage/storage-scalability-targets.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="00eba-165">다음 단계</span><span class="sxs-lookup"><span data-stu-id="00eba-165">Next steps</span></span>
[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-windows-infrastructure-guidelines-next-steps.md)]

