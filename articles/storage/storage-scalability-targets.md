---
title: "Azure Storage 확장성 및 성능 목표 | Microsoft Docs"
description: "표준 및 프리미엄 저장소 계정에 대한 용량, 요청 속도 및 인바운드 및 아웃 바운드 대역폭을 포함한 Azure 저장소의 확장성 및 성능 목표를 알아보세요. Azure 저장소 서비스 각각의 파티션에 대한 성능 목표를 이해해 보세요."
services: storage
documentationcenter: na
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: be721bd3-159f-40a1-88c1-96418537fe75
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 07/12/2017
ms.author: robinsh
ms.openlocfilehash: ed90e5d63e4c93f9c5054b02d2b4457b44caf6eb
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-storage-scalability-and-performance-targets"></a><span data-ttu-id="1215e-104">Azure 저장소 확장성 및 성능 목표</span><span class="sxs-lookup"><span data-stu-id="1215e-104">Azure Storage Scalability and Performance Targets</span></span>
## <a name="overview"></a><span data-ttu-id="1215e-105">개요</span><span class="sxs-lookup"><span data-stu-id="1215e-105">Overview</span></span>
<span data-ttu-id="1215e-106">이 항목에서는 Microsoft Azure 저장소에 대한 확장성 및 성능을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="1215e-106">This topic describes the scalability and performance topics for Microsoft Azure Storage.</span></span> <span data-ttu-id="1215e-107">기타 Azure 제한 사항에 대한 요약은 [Azure 구독 및 서비스 제한, 할당량 및 제약 조건](../azure-subscription-service-limits.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1215e-107">For a summary of other Azure limits, see [Azure Subscription and Service Limits, Quotas, and Constraints](../azure-subscription-service-limits.md).</span></span>

> [!NOTE]
> <span data-ttu-id="1215e-108">모든 저장소 계정은 새로운 플랫 네트워크 토폴로지에서 실행되고 작성된 시기에 관계 없이 아래에 설명된 확장성 및 성능 목표를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="1215e-108">All storage accounts run on the new flat network topology and support the scalability and performance targets outlined below, regardless of when they were created.</span></span> <span data-ttu-id="1215e-109">Azure 저장소 플랫 네트워크 아키텍처 및 확장성에 대한 자세한 내용은 [Microsoft Azure 저장소: 일관성과 가용성이 뛰어난 클라우드 저장소 서비스](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1215e-109">For more information on the Azure Storage flat network architecture and on scalability, see [Microsoft Azure Storage: A Highly Available Cloud Storage Service with Strong Consistency](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx).</span></span>
> 
> [!IMPORTANT]
> <span data-ttu-id="1215e-110">여기에 나열된 확장성 및 성능 목표는 최첨단 목표이지만 달성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1215e-110">The scalability and performance targets listed here are high-end targets, but are achievable.</span></span> <span data-ttu-id="1215e-111">모든 경우, 계정 사용량에 따라 달성된 요청 속도 및 대역폭은 저장된 개채의 크기 및 응용 프로그램이 수행한 작업 형태에 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="1215e-111">In all cases, the request rate and bandwidth achieved by your storage account depends upon the size of objects stored, the access patterns utilized, and the type of workload your application performs.</span></span> <span data-ttu-id="1215e-112">해당 성능이 요구 사항을 충족시키는지 여부를 확인 하려면 서비스를 반드시 테스트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1215e-112">Be sure to test your service to determine whether its performance meets your requirements.</span></span> <span data-ttu-id="1215e-113">가능하면 트래픽 속도가 갑자기 증가하지 않고 파티션 간의 트래픽이 적절하게 분산되도록 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="1215e-113">If possible, avoid sudden spikes in the rate of traffic and ensure that traffic is well-distributed across partitions.</span></span>
> 
> <span data-ttu-id="1215e-114">응용 프로그램이 파티션의 작업 처리 가능한 제한에 도달하면 Azure 저장소는 오류 코드 503 (서버 작업 중) 또는 오류 코드 500 (작업 시간 초과) 응답을 반송하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="1215e-114">When your application reaches the limit of what a partition can handle for your workload, Azure Storage will begin to return error code 503 (Server Busy) or error code 500 (Operation Timeout) responses.</span></span> <span data-ttu-id="1215e-115">이런 경우 응용 프로그램은 재시도를 위한 지수 백오프 정책을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1215e-115">When this occurs, the application should use an exponential backoff policy for retries.</span></span> <span data-ttu-id="1215e-116">지수 백오프는 파티션에 대한 부하를 감소시키고 해당 파티션에 트래픽의 급증을 완화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1215e-116">The exponential backoff allows the load on the partition to decrease, and to ease out spikes in traffic to that partition.</span></span>
> 
> 

<span data-ttu-id="1215e-117">응용 프로그램의 요구가 단일 저장소 계정의 확장성 목표를 초과하는 경우 여러 저장소 계정을 사용하도록 응용 프로그램을 빌드하고 데이터를 이러한 저장소 계정에 분할합니다.</span><span class="sxs-lookup"><span data-stu-id="1215e-117">If the needs of your application exceed the scalability targets of a single storage account, you can build your application to use multiple storage accounts, and partition your data objects across those storage accounts.</span></span> <span data-ttu-id="1215e-118">볼륨 가격에 대한 자세한 내용은 [Azure 저장소 가격 책정](https://azure.microsoft.com/pricing/details/storage/) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1215e-118">See [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/storage/) for information on volume pricing.</span></span>

## <a name="scalability-targets-for-blobs-queues-tables-and-files"></a><span data-ttu-id="1215e-119">Blob, 큐, 테이블 및 파일에 대한 확장성 목표</span><span class="sxs-lookup"><span data-stu-id="1215e-119">Scalability targets for blobs, queues, tables, and files</span></span>
[!INCLUDE [azure-storage-limits](../../includes/azure-storage-limits.md)]

<!-- conceptual info about disk limits -- applies to unmanaged and managed -->
## <a name="scalability-targets-for-virtual-machine-disks"></a><span data-ttu-id="1215e-120">가상 컴퓨터 디스크에 대한 확장성 목표</span><span class="sxs-lookup"><span data-stu-id="1215e-120">Scalability targets for virtual machine disks</span></span>
[!INCLUDE [azure-storage-limits-vm-disks](../../includes/azure-storage-limits-vm-disks.md)]

<span data-ttu-id="1215e-121">자세한 내용은 [Windows VM 크기](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 또는 [Linux VM 크기](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1215e-121">See [Windows VM sizes](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) or [Linux VM sizes](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for additional details.</span></span>

## <a name="managed-virtual-machine-disks"></a><span data-ttu-id="1215e-122">관리되는 가상 컴퓨터 디스크</span><span class="sxs-lookup"><span data-stu-id="1215e-122">Managed virtual machine disks</span></span>

[!INCLUDE [azure-storage-limits-vm-disks-managed](../../includes/azure-storage-limits-vm-disks-managed.md)]

## <a name="unmanaged-virtual-machine-disks"></a><span data-ttu-id="1215e-123">관리되지 않는 가상 컴퓨터 디스크</span><span class="sxs-lookup"><span data-stu-id="1215e-123">Unmanaged virtual machine disks</span></span>
[!INCLUDE [azure-storage-limits-vm-disks-standard](../../includes/azure-storage-limits-vm-disks-standard.md)]

[!INCLUDE [azure-storage-limits-vm-disks-premium](../../includes/azure-storage-limits-vm-disks-premium.md)]

## <a name="scalability-targets-for-azure-resource-manager"></a><span data-ttu-id="1215e-124">Azure 리소스 관리자에 대한 확장성 목표</span><span class="sxs-lookup"><span data-stu-id="1215e-124">Scalability targets for Azure resource manager</span></span>
[!INCLUDE [azure-storage-limits-azure-resource-manager](../../includes/azure-storage-limits-azure-resource-manager.md)]

## <a name="partitions-in-azure-storage"></a><span data-ttu-id="1215e-125">Azure 저장소의 파티션</span><span class="sxs-lookup"><span data-stu-id="1215e-125">Partitions in Azure Storage</span></span>
<span data-ttu-id="1215e-126">Azure 저장소(blob, 메시지, 엔터티 및 파일)에 저장 된 데이터를 보유한 모든 개체는 파티션에 속하며 파티션 키로 식별됩니다.</span><span class="sxs-lookup"><span data-stu-id="1215e-126">Every object that holds data that is stored in Azure Storage (blobs, messages, entities, and files) belongs to a partition, and is identified by a partition key.</span></span> <span data-ttu-id="1215e-127">파티션은 Azure 저장소 부하가 어떻게 서버의 blob, 메시지, 엔터티 및 파일을 해당 개체의 트래픽 요구를 충족하도록 분산할지 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="1215e-127">The partition determines how Azure Storage load balances blobs, messages, entities, and files across servers to meet the traffic needs of those objects.</span></span> <span data-ttu-id="1215e-128">파티션 키는 고유하며 blob, 메시지 또는 엔터티를 찾는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1215e-128">The partition key is unique and is used to locate a blob, message, or entity.</span></span>

<span data-ttu-id="1215e-129">위의 테이블에 표시된 [표준 저장소 계정의 확장성 목표](#standard-storage-accounts) 는 각 서비스에 대한 단일 파티션의 성능 목표를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="1215e-129">The table shown above in [Scalability Targets for Standard Storage Accounts](#standard-storage-accounts) lists the performance targets for a single partition for each service.</span></span>

<span data-ttu-id="1215e-130">파티션은 각 저장소 서비스의 부하 분산 및 확장성에 다음과 같은 방식으로 영향을 줍니다:</span><span class="sxs-lookup"><span data-stu-id="1215e-130">Partitions affect load balancing and scalability for each of the storage services in the following ways:</span></span>

* <span data-ttu-id="1215e-131">**Blob**: blob의 파티션 키는 계정 이름 + 컨테이너 이름 + blob 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="1215e-131">**Blobs**: The partition key for a blob is account name + container name + blob name.</span></span> <span data-ttu-id="1215e-132">이는 blob의 로드에 필요한 경우 각 blob에 자체 파티션을 둘 수 있음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="1215e-132">This means that each blob can have its own partition if load on the blob demands it.</span></span> <span data-ttu-id="1215e-133">액세스를 확장하기 위해 blob을 여러 서버에 분산시킬 수 있지만 단일 blob은 단일 서버에 의해서만 처리될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1215e-133">Blobs can be distributed across many servers in order to scale out access to them, but a single blob can only be served by a single server.</span></span> <span data-ttu-id="1215e-134">Blob 컨테이너에서 blob를 논리적으로 그룹화하는 반면 해당 그룹화에는 파티션이 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1215e-134">While blobs can be logically grouped in blob containers, there are no partitioning implications from this grouping.</span></span>
* <span data-ttu-id="1215e-135">**파일**: 파일에 대한 파티션 키는 계정 이름 + 파일 공유 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="1215e-135">**Files**: The partition key for a file is account name + file share name.</span></span> <span data-ttu-id="1215e-136">즉, 파일 공유의 모든 파일도 단일 파티션에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="1215e-136">This means all files in a file share are also in a single partition.</span></span>
* <span data-ttu-id="1215e-137">**메시지**: 메시지의 파티션 키는 계정 이름 + 큐 이름이므로 큐에 있는 모든 메시지를 단일 파티션으로 그룹화하고 단일 서버를 통해 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1215e-137">**Messages**: The partition key for a message is the account name + queue name, so all messages in a queue are grouped into a single partition and are served by a single server.</span></span> <span data-ttu-id="1215e-138">서로 다른 큐는 부하를 분산하는 다른 서버에 의해 처리될 수 있지만 하나의 저장소 계정은 다수의 큐를 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1215e-138">Different queues may be processed by different servers to balance the load for however many queues a storage account may have.</span></span>
* <span data-ttu-id="1215e-139">**엔터티**: 엔터티의 파티션 키는 계정 이름 + 테이블 이름 + 파티션 키이며, 여기서 파티션 키는 사용자 정의가 필요한 **PartitionKey** 속성의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="1215e-139">**Entities**: The partition key for an entity is account name + table name + partition key, where the partition key is the value of the required user-defined **PartitionKey** property for the entity.</span></span> <span data-ttu-id="1215e-140">동일한 파티션 키 값을 가진 모든 엔터티는 같은 파티션으로 그룹화 되며 같은 파티션 서버에 의해 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="1215e-140">All entities with the same partition key value are grouped into the same partition and are served by the same partition server.</span></span> <span data-ttu-id="1215e-141">이는 응용 프로그램 디자인에서 이해해야 할 중요한 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="1215e-141">This is an important point to understand in designing your application.</span></span> <span data-ttu-id="1215e-142">응용 프로그램은 엔터티를 단일 파티션으로 그룹화하는 데이터 액세스 이점과 여러 파티션에서 엔터티를 분산시키는 경우의 확장성 이점을 조정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1215e-142">Your application should balance the scalability benefits of spreading entities across multiple partitions with the data access advantages of grouping entities in a single partition.</span></span>  

<span data-ttu-id="1215e-143">테이블의 엔터티 그룹을 단일 파티션으로 그룹화하는 경우 가장 큰 장점은 하나의 파티션이 단일 서버에 존재하므로 동일한 파티션의 엔터티에서 원자성 배치 작업을 수행할 수 있다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="1215e-143">A key advantage to grouping a set of entities in a table into a single partition is that it's possible to perform atomic batch operations across entities in the same partition, since a partition exists on a single server.</span></span> <span data-ttu-id="1215e-144">따라서 엔터티 그룹에 대해 배치 작업을 수행하려는 경우 동일한 파티션 키를 가진 엔터티를 그룹화하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1215e-144">Therefore, if you wish to perform batch operations on a group of entities, consider grouping them with the same partition key.</span></span> 

<span data-ttu-id="1215e-145">반면, 동일한 테이블에 있지만 파티션 키가 서로 다른 엔터티는 서로 다른 서버에 부하를 분산시켜 확장성을 높일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1215e-145">On the other hand, entities that are in the same table but have different partition keys can be load balanced across different servers, making it possible to have greater scalability.</span></span>

<span data-ttu-id="1215e-146">테이블 분할 전략 디자인에 대한 자세한 권장 사항은 [여기](https://msdn.microsoft.com/library/azure/hh508997.aspx)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1215e-146">Detailed recommendations for designing partitioning strategy for tables can be found [here](https://msdn.microsoft.com/library/azure/hh508997.aspx).</span></span>

## <a name="see-also"></a><span data-ttu-id="1215e-147">참고 항목</span><span class="sxs-lookup"><span data-stu-id="1215e-147">See Also</span></span>
* [<span data-ttu-id="1215e-148">저장소 가격 정보</span><span class="sxs-lookup"><span data-stu-id="1215e-148">Storage Pricing Details</span></span>](https://azure.microsoft.com/pricing/details/storage/)
* [<span data-ttu-id="1215e-149">Azure 구독 및 서비스 제한, 할당량 및 제약 조건</span><span class="sxs-lookup"><span data-stu-id="1215e-149">Azure Subscription and Service Limits, Quotas, and Constraints</span></span>](../azure-subscription-service-limits.md)
* [<span data-ttu-id="1215e-150">프리미엄 저장소: Azure 가상 컴퓨터 작업을 위한 고성능 저장소</span><span class="sxs-lookup"><span data-stu-id="1215e-150">Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads</span></span>](storage-premium-storage.md)
* [<span data-ttu-id="1215e-151">Azure 저장소에서 복제</span><span class="sxs-lookup"><span data-stu-id="1215e-151">Azure Storage Replication</span></span>](storage-redundancy.md)
* [<span data-ttu-id="1215e-152">Microsoft Azure 저장소 성능 및 확장성 검사 목록</span><span class="sxs-lookup"><span data-stu-id="1215e-152">Microsoft Azure Storage Performance and Scalability Checklist</span></span>](storage-performance-checklist.md)
* [<span data-ttu-id="1215e-153">Microsoft Azure 저장소: 일관성과 가용성이 뛰어난 클라우드 저장소 서비스</span><span class="sxs-lookup"><span data-stu-id="1215e-153">Microsoft Azure Storage: A Highly Available Cloud Storage Service with Strong Consistency</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx)

