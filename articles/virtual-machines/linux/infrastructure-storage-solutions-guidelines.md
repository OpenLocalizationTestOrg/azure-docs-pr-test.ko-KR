---
title: "Azure에서 Linux Vm에 대 한 aaaStorage 솔루션 | Microsoft Docs"
description: "Hello 핵심 디자인 및 구현 지침 Azure 인프라 서비스에서 저장소 솔루션을 배포 하기 위한 방법을 알아봅니다."
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3c368f07-189b-4520-bbe2-f4080253bbf2
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d270c4786d7b55b18b011aa345063b6816a80876
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-infrastructure-guidelines-for-linux-vms"></a><span data-ttu-id="33b8d-103">Linux VM에 대한 Azure Storage 인프라 지침</span><span class="sxs-lookup"><span data-stu-id="33b8d-103">Azure storage infrastructure guidelines for Linux VMs</span></span>

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

<span data-ttu-id="33b8d-104">이 문서에서는 최적의 VM(가상 컴퓨터) 성능을 위한 저장소 요구 사항 및 디자인 고려 사항을 이해하는 데 주안점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="33b8d-104">This article focuses on understanding storage needs and design considerations for achieving optimum virtual machine (VM) performance.</span></span>

## <a name="implementation-guidelines-for-storage"></a><span data-ttu-id="33b8d-105">저장소에 대한 구현 지침</span><span class="sxs-lookup"><span data-stu-id="33b8d-105">Implementation guidelines for storage</span></span>
<span data-ttu-id="33b8d-106">의사 결정:</span><span class="sxs-lookup"><span data-stu-id="33b8d-106">Decisions:</span></span>

* <span data-ttu-id="33b8d-107">관리 되지 않는 디스크 또는 Azure 관리 되는 디스크 toouse 예정 입니까?</span><span class="sxs-lookup"><span data-stu-id="33b8d-107">Are you going toouse Azure Managed Disks or unmanaged disks?</span></span>
* <span data-ttu-id="33b8d-108">Toouse 표준 또는 프리미엄 저장소 작업에 필요 합니까?</span><span class="sxs-lookup"><span data-stu-id="33b8d-108">Do you need toouse Standard or Premium storage for your workload?</span></span>
* <span data-ttu-id="33b8d-109">필요 디스크 스트라이프 toocreate 디스크 4TB 보다 큰?</span><span class="sxs-lookup"><span data-stu-id="33b8d-109">Do you need disk striping toocreate disks larger than 4TB?</span></span>
* <span data-ttu-id="33b8d-110">디스크 스트라이프 tooachieve 최적의 I/O 성능 작업에 필요 합니까?</span><span class="sxs-lookup"><span data-stu-id="33b8d-110">Do you need disk striping tooachieve optimal I/O performance for your workload?</span></span>
* <span data-ttu-id="33b8d-111">집합의 저장소 계정이 필요 한가요 toohost IT 작업 또는 인프라?</span><span class="sxs-lookup"><span data-stu-id="33b8d-111">What set of storage accounts do you need toohost your IT workload or infrastructure?</span></span>

<span data-ttu-id="33b8d-112">작업:</span><span class="sxs-lookup"><span data-stu-id="33b8d-112">Tasks:</span></span>

* <span data-ttu-id="33b8d-113">배포 하 고 적절 한 수 hello 및 저장소 계정의 유형을 계획 hello 응용 프로그램의 I/O 요구 사항을 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="33b8d-113">Review I/O demands of hello applications you are deploying and plan hello appropriate number and type of storage accounts.</span></span>
* <span data-ttu-id="33b8d-114">명명 규칙을 사용 하 여 저장소 계정의 hello 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="33b8d-114">Create hello set of storage accounts using your naming convention.</span></span> <span data-ttu-id="33b8d-115">Hello Azure CLI 또는 hello 포털을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33b8d-115">You can use hello Azure CLI or hello portal.</span></span>

## <a name="storage"></a><span data-ttu-id="33b8d-116">저장소</span><span class="sxs-lookup"><span data-stu-id="33b8d-116">Storage</span></span>
<span data-ttu-id="33b8d-117">Azure 저장소는 VM(가상 컴퓨터) 및 응용 프로그램의 배포 및 관리 작업의 핵심 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="33b8d-117">Azure Storage is a key part of deploying and managing virtual machines (VMs) and applications.</span></span> <span data-ttu-id="33b8d-118">Azure 저장소 파일 데이터, 구조화 되지 않은 데이터 및 메시지를 저장 하기 위한 서비스를 제공 하 고 Vm을 지 원하는 hello 인프라의 일부 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="33b8d-118">Azure Storage provides services for storing file data, unstructured data, and messages, and it is also part of hello infrastructure supporting VMs.</span></span>

<span data-ttu-id="33b8d-119">[Azure 관리 되는 디스크](../../storage/storage-managed-disks-overview.md) hello 백그라운드 있습니다에 대 한 저장소를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="33b8d-119">[Azure Managed Disks](../../storage/storage-managed-disks-overview.md) handles storage for you behind hello scenes.</span></span> <span data-ttu-id="33b8d-120">관리 되지 않는 디스크와 저장소 계정을 만듭니다 toohold hello 디스크 (VHD 파일) Azure Vm에 대 한.</span><span class="sxs-lookup"><span data-stu-id="33b8d-120">With unmanaged disks, you create storage accounts toohold hello disks (VHD files) for your Azure VMs.</span></span> <span data-ttu-id="33b8d-121">확장 하는 경우 디스크를 사용 하 여 저장소에 대 한 hello IOPS 제한을 초과 하지 않도록 추가 저장소 계정을 만들어지므로 있는지 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="33b8d-121">When scaling up, you must make sure you created additional storage accounts so you don’t exceed hello IOPS limit for storage with any of your disks.</span></span> <span data-ttu-id="33b8d-122">관리 되는 디스크 저장소를 처리를 사용 하면 더 이상 영향을 받습니다 hello 저장소 계정 제한 하 여 (20, 000 IOPS 등 / 계정).</span><span class="sxs-lookup"><span data-stu-id="33b8d-122">With Managed Disks handling storage, you are no longer limited by hello storage account limits (such as 20,000 IOPS / account).</span></span> <span data-ttu-id="33b8d-123">또한 없을 toocopy 사용자 지정 이미지 (VHD 파일) toomultiple 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="33b8d-123">You also no longer have toocopy your custom images (VHD files) toomultiple storage accounts.</span></span> <span data-ttu-id="33b8d-124">– Azure 지역 마다 하나의 저장소 계정-중앙 위치에서 관리할 수 있으며 구독에 있는 Vm의 toocreate 수백 사용.</span><span class="sxs-lookup"><span data-stu-id="33b8d-124">You can manage them in a central location – one storage account per Azure region – and use them toocreate hundreds of VMs in a subscription.</span></span> <span data-ttu-id="33b8d-125">새 배포에 Managed Disks를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="33b8d-125">We recommend you use Managed Disks for new deployments.</span></span>

<span data-ttu-id="33b8d-126">VM 지원을 위해 다음 두 가지 저장소 계정 유형을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33b8d-126">There are two types of storage accounts available for supporting VMs:</span></span>

* <span data-ttu-id="33b8d-127">표준 저장소 계정 제공 되는 tooblob 저장소 (Azure VM 디스크를 저장 하는 데 사용), 테이블 저장소, 큐 저장소 및 파일 저장소.</span><span class="sxs-lookup"><span data-stu-id="33b8d-127">Standard storage accounts give you access tooblob storage (used for storing Azure VM disks), table storage, queue storage, and file storage.</span></span>
* <span data-ttu-id="33b8d-128">[Premium 저장소](../../storage/storage-premium-storage.md) 계정은 MongoDB Sharded 클러스터와 같이 I/O 집약적 워크로드에 대해 대기 시간이 낮은 고성능 디스크 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="33b8d-128">[Premium storage](../../storage/storage-premium-storage.md) accounts deliver high-performance, low-latency disk support for I/O intensive workloads, such as MongoDB Sharded cluster.</span></span> <span data-ttu-id="33b8d-129">Premium 저장소는 현재 Azure VM 디스크만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="33b8d-129">Premium storage currently supports Azure VM disks only.</span></span>

<span data-ttu-id="33b8d-130">Azure는 운영 체제 디스크, 임시 디스크를 및 0개 이상의 선택적 데이터 디스크로 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="33b8d-130">Azure creates VMs with an operating system disk, a temporary disk, and zero or more optional data disks.</span></span> <span data-ttu-id="33b8d-131">hello 운영 체제 디스크 및 데이터 디스크는 hello 컴퓨터 거주 hello 노드에서 hello 임시 디스크를 로컬로 저장 하는 반면 Azure 페이지 blob입니다.</span><span class="sxs-lookup"><span data-stu-id="33b8d-131">hello operating system disk and data disks are Azure page blobs, whereas hello temporary disk is stored locally on hello node where hello machine lives.</span></span> <span data-ttu-id="33b8d-132">Tooonly 비 영구적인 데이터에 대 한 VM을 유지 관리 이벤트 중 호스트 간에 마이그레이션할 수 있습니다 hello로이 임시 디스크를 사용 하는 응용 프로그램을 디자인할 때 주의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="33b8d-132">Take care when designing applications tooonly use this temporary disk for non-persistent data as hello VM may be migrated between hosts during a maintenance event.</span></span> <span data-ttu-id="33b8d-133">Hello 임시 디스크에 저장 된 모든 데이터가 손실 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33b8d-133">Any data stored on hello temporary disk would be lost.</span></span>

<span data-ttu-id="33b8d-134">내 구성과 고가용성 제공한 hello 기본 Azure 저장소 환경 tooensure 데이터가 유지 계획 되지 않은 유지 관리 또는 하드웨어 오류 로부터 보호 됩니다.</span><span class="sxs-lookup"><span data-stu-id="33b8d-134">Durability and high availability is provided by hello underlying Azure Storage environment tooensure that your data remains protected against unplanned maintenance or hardware failures.</span></span> <span data-ttu-id="33b8d-135">Azure 저장소 환경을 디자인할 때 tooreplicate VM 저장소를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33b8d-135">As you design your Azure Storage environment, you can choose tooreplicate VM storage:</span></span>

* <span data-ttu-id="33b8d-136">지정된 Azure 데이터 센터 내에서 로컬로</span><span class="sxs-lookup"><span data-stu-id="33b8d-136">locally within a given Azure datacenter</span></span>
* <span data-ttu-id="33b8d-137">지정된 지역 내에서 Azure 데이터 센터에서</span><span class="sxs-lookup"><span data-stu-id="33b8d-137">across Azure datacenters within a given region</span></span>
* <span data-ttu-id="33b8d-138">서로 다른 지역의 Azure 데이터 센터에서.</span><span class="sxs-lookup"><span data-stu-id="33b8d-138">across Azure datacenters across different regions.</span></span>

<span data-ttu-id="33b8d-139">읽을 수 [고가용성에 대 한 hello 복제 옵션에 대 한 자세한](../../storage/storage-introduction.md#replication-for-durability-and-high-availability)합니다.</span><span class="sxs-lookup"><span data-stu-id="33b8d-139">You can read [more about hello replication options for high availability](../../storage/storage-introduction.md#replication-for-durability-and-high-availability).</span></span>

<span data-ttu-id="33b8d-140">운영 체제 디스크 및 데이터 디스크의 최대 크기는 4TB입니다.</span><span class="sxs-lookup"><span data-stu-id="33b8d-140">Operating system disks and data disks have a maximum size of 4TB.</span></span> <span data-ttu-id="33b8d-141">데이터 디스크 toopresent 논리 보다 큰 볼륨 1023GB tooyour VM 함께 풀링 하 여 논리 볼륨 관리자 (LVM) toosurpass이 한이도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33b8d-141">You can use Logical Volume Manager (LVM) toosurpass this limit by pooling together data disks toopresent logical volumes larger than 1023GB tooyour VM.</span></span>

<span data-ttu-id="33b8d-142">Azure Storage 배포를 디자인할 때는 확장성이 어느 정도 제한될 수 있습니다. 자세한 내용은 [Microsoft Azure 구독 및 서비스 제한, 할당량 및 제약 조건](../../azure-subscription-service-limits.md#storage-limits)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="33b8d-142">There are some scalability limits when designing your Azure Storage deployments - for more information, see [Microsoft Azure subscription and service limits, quotas, and constraints](../../azure-subscription-service-limits.md#storage-limits).</span></span> <span data-ttu-id="33b8d-143">[Azure Storage 확장성 및 성능 목표](../../storage/storage-scalability-targets.md)도 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="33b8d-143">Also see [Azure storage scalability and performance targets](../../storage/storage-scalability-targets.md).</span></span>

<span data-ttu-id="33b8d-144">응용 프로그램 저장소의 경우 문서, 이미지, 백업, 구성 데이터, 로그 등의 구조화되지 않은 개체 데이터를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33b8d-144">For application storage, you can store unstructured object data such as documents, images, backups, configuration data, logs, etc.</span></span> <span data-ttu-id="33b8d-145">Blob Storage를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="33b8d-145">using blob storage.</span></span> <span data-ttu-id="33b8d-146">응용 프로그램 tooa 연결 된 가상 디스크 toohello VM을 작성 하는 대신 hello 응용 프로그램을 작성할 수 직접 tooAzure blob 저장소.</span><span class="sxs-lookup"><span data-stu-id="33b8d-146">Rather than your application writing tooa virtual disk attached toohello VM, hello application can write directly tooAzure blob storage.</span></span> <span data-ttu-id="33b8d-147">Blob 저장소의 hello 옵션도 제공 [핫 및 저장소 계층 냉각용](../../storage/storage-blob-storage-tiers.md) 가용성 요구와 비용 제약 조건에 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="33b8d-147">Blob storage also provides hello option of [hot and cool storage tiers](../../storage/storage-blob-storage-tiers.md) depending on your availability needs and cost constraints.</span></span>

## <a name="striped-disks"></a><span data-ttu-id="33b8d-148">스트라이프 디스크</span><span class="sxs-lookup"><span data-stu-id="33b8d-148">Striped disks</span></span>
<span data-ttu-id="33b8d-149">을 사용 있으므로 toocreate 디스크 1,023 GB 보다 큰 대부분의 경우에서 외에도 데이터 디스크에 대 한 스트라이프를 사용 하 여 단일 볼륨에 대 한 tooback hello 저장소 여러 blob를 허용 하 여 성능이 향상 됩니다.</span><span class="sxs-lookup"><span data-stu-id="33b8d-149">Besides allowing you toocreate disks larger than 1023 GB, in many instances, using striping for data disks enhances performance by allowing multiple blobs tooback hello storage for a single volume.</span></span> <span data-ttu-id="33b8d-150">스트라이핑 기능을 hello I/O 필요한 toowrite 및 단일 논리적 디스크에서 읽은 데이터 동시에 진행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="33b8d-150">With striping, hello I/O required toowrite and read data from a single logical disk proceeds in parallel.</span></span>

<span data-ttu-id="33b8d-151">Azure는 데이터 디스크 개수 hello 및 hello VM 크기에 따라 사용할 수 있는 대역폭에 대 한 제한을 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="33b8d-151">Azure imposes limits on hello number of data disks and amount of bandwidth available, depending on hello VM size.</span></span> <span data-ttu-id="33b8d-152">자세한 내용은 [가상 컴퓨터 크기](sizes.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="33b8d-152">For details, see [Sizes for virtual machines](sizes.md)</span></span>

<span data-ttu-id="33b8d-153">Azure 데이터 디스크에 대 한 디스크 스트라이프를 사용 하는 경우 hello 지침을 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="33b8d-153">If you are using disk striping for Azure data disks, consider hello following guidelines:</span></span>

* <span data-ttu-id="33b8d-154">Hello VM 크기에 허용 되는 hello 최대 데이터 디스크를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="33b8d-154">Attach hello maximum data disks allowed for hello VM size.</span></span>
* <span data-ttu-id="33b8d-155">LVM을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="33b8d-155">Use LVM.</span></span>
* <span data-ttu-id="33b8d-156">Azure 데이터 디스크 캐싱 옵션을 사용하지 않습니다(캐싱 정책 = 없음).</span><span class="sxs-lookup"><span data-stu-id="33b8d-156">Avoid using Azure data disk caching options (caching policy = None).</span></span>

<span data-ttu-id="33b8d-157">자세한 내용은 [Linux VM에서 LVM 구성](configure-lvm.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="33b8d-157">For more information, see [Configuring LVM on a Linux VM](configure-lvm.md).</span></span>

## <a name="multiple-storage-accounts"></a><span data-ttu-id="33b8d-158">여러 저장소 계정</span><span class="sxs-lookup"><span data-stu-id="33b8d-158">Multiple storage accounts</span></span>
<span data-ttu-id="33b8d-159">이 섹션이 너무 적용 되지 않습니다[Azure 관리 되는 디스크](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)와 별도 저장소 계정을 만들지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="33b8d-159">This section does not apply too[Azure Managed Disks](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), as you do not create separate storage accounts.</span></span> 

<span data-ttu-id="33b8d-160">관리 되지 않는 디스크에 대 한 Azure 저장소 환경을 디자인할 때 여러 저장소 계정을 사용할 수 있습니다 증가 hello 수가 Vm으로 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="33b8d-160">When designing your Azure Storage environment for unmanaged disks, you can use multiple storage accounts as hello number of VMs you deploy increases.</span></span> <span data-ttu-id="33b8d-161">이 방법은 hello 기본 Azure 저장소 인프라 toomaintain 최적의 성능 Vm 및 응용 프로그램에서 I/O hello 아웃 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33b8d-161">This approach helps distribute out hello I/O across hello underlying Azure Storage infrastructure toomaintain optimum performance for your VMs and applications.</span></span> <span data-ttu-id="33b8d-162">배포 하는 hello 응용 프로그램을 디자인할 때 Azure 저장소 계정에서 각 VM에 hello I/O 요구 사항 및 해당 Vm으로 균형을 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="33b8d-162">As you design hello applications that you are deploying, consider hello I/O requirements each VM has and balance out those VMs across Azure Storage accounts.</span></span> <span data-ttu-id="33b8d-163">Tooavoid Vm 하나 또는 두 개의 toojust 저장소 계정에 요구 되는 모든 hello 높은 I/O를 그룹화 해 보십시오.</span><span class="sxs-lookup"><span data-stu-id="33b8d-163">Try tooavoid grouping all hello high I/O demanding VMs in toojust one or two storage accounts.</span></span>

<span data-ttu-id="33b8d-164">Hello 다양 한 Azure 저장소 옵션의 hello I/O 기능에 대 한 자세한 내용은 및 일부 권장 최대값에 대 한 참조 [Azure 저장소 확장성 및 성능 목표가](../../storage/storage-scalability-targets.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="33b8d-164">For more information about hello I/O capabilities of hello different Azure Storage options and some recommend maximums, see [Azure storage scalability and performance targets](../../storage/storage-scalability-targets.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="33b8d-165">다음 단계</span><span class="sxs-lookup"><span data-stu-id="33b8d-165">Next steps</span></span>
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

