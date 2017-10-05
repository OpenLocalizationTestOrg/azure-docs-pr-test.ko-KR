---
title: "Azure Site Recovery를 사용하여 Azure에 VMware 복제를 위한 용량 및 크기 조정 계획 | Microsoft Docs"
description: "Azure Site Recovery를 사용하여 Azure에 VMware VM을 복제하는 경우 용량 및 크기 조정을 계획하려면 이 문서를 사용합니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 0a1cd8eb-a8f7-4228-ab84-9449e0b2887b
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/27/2017
ms.author: rayne
ms.openlocfilehash: f5b334e594e3d002e1862b25c4faba7163efa7d4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="step-3-plan-capacity-and-scaling-for-vmware-to-azure-replication"></a><span data-ttu-id="e7c64-103">3단계: Azure로 VMware를 복제하기 위한 용량 및 크기 조정 계획</span><span class="sxs-lookup"><span data-stu-id="e7c64-103">Step 3: Plan capacity and scaling for VMware to Azure replication</span></span>

<span data-ttu-id="e7c64-104">[Azure Site Recovery](site-recovery-overview.md)를 사용하여 온-프레미스 VMware VM 및 물리적 서버를 Azure에 복제하는 경우 용량 및 크기 조정 계획을 파악하려면 이 문서를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-104">Use this article to figure out planning for capacity and scaling, when replicating on-premises VMware VMs and physical servers to Azure with [Azure Site Recovery](site-recovery-overview.md).</span></span>

<span data-ttu-id="e7c64-105">이 문서의 하단 또는 [Azure Recovery Services 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)에서 의견이나 질문을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="how-do-i-start-capacity-planning"></a><span data-ttu-id="e7c64-106">용량 계획을 시작하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="e7c64-106">How do I start capacity planning?</span></span>

<span data-ttu-id="e7c64-107">이 문서에서 강조 표시된 고려 사항과 더불어 복제 환경에 대한 정보를 수집하고 이 정보를 사용하여 용량을 계획합니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-107">You gather information about your replication environment, and then plan capacity using this information, together with the considerations highlighted in this article.</span></span>


## <a name="gather-information"></a><span data-ttu-id="e7c64-108">정보 수집</span><span class="sxs-lookup"><span data-stu-id="e7c64-108">Gather information</span></span>

1. <span data-ttu-id="e7c64-109">VMware를 복제하기 위해 [Deployment Planner 도구](https://aka.ms/asr-deployment-planner)를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-109">Download the [Deployment Planner tool](https://aka.ms/asr-deployment-planner) for VMware replication.</span></span>
2. <span data-ttu-id="e7c64-110">[이 문서를 읽고](site-recovery-deployment-planner.md) 도구를 실행하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-110">[Read this article](site-recovery-deployment-planner.md) to understand how to run the tool.</span></span>
3. <span data-ttu-id="e7c64-111">이 도구를 사용하여 호환되거나 호환되지 않는 VM, VM당 디스크 및 디스크당 데이터 변동에 대한 정보를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-111">Using the tool you gather information about compatible and incompatible VMs, disks per VM, and data churn per disk.</span></span> <span data-ttu-id="e7c64-112">도구는 네트워크 대역폭 요구 사항과 성공적인 복제 및 테스트 장애 조치(failover)에 필요한 Azure 인프라에 대해서도 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-112">The tool also covers network bandwidth requirements, and the Azure infrastructure needed for successful replication and test failover.</span></span>

## <a name="replication-considerations"></a><span data-ttu-id="e7c64-113">복제 시 고려 사항</span><span class="sxs-lookup"><span data-stu-id="e7c64-113">Replication considerations</span></span>

<span data-ttu-id="e7c64-114">배포를 시작하기 전에 다음과 같은 고려 사항을 기억하세요.</span><span class="sxs-lookup"><span data-stu-id="e7c64-114">Note these considerations before you start deployment:</span></span>

<span data-ttu-id="e7c64-115">**구성 요소**</span><span class="sxs-lookup"><span data-stu-id="e7c64-115">**Component**</span></span> | <span data-ttu-id="e7c64-116">**세부 정보**</span><span class="sxs-lookup"><span data-stu-id="e7c64-116">**Details**</span></span> |
--- | --- | ---
<span data-ttu-id="e7c64-117">**복제**</span><span class="sxs-lookup"><span data-stu-id="e7c64-117">**Replication**</span></span> | <span data-ttu-id="e7c64-118">**일일 최대 변경률:** 보호된 컴퓨터는 하나의 프로세스 서버만 사용할 수 있으며 단일 프로세스 서버는 최대 2TB의 일일 최대 변경률을 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-118">**Maximum daily change rate:** A protected machine can only use one process server, and a single process server can handle a daily change rate up to 2 TB.</span></span> <span data-ttu-id="e7c64-119">따라서 2TB는 보호되는 컴퓨터에 대해 지원되는 최대 일일 데이터 변경률입니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-119">Thus 2 TB is the maximum daily data change rate that’s supported for a protected machine.</span></span><br/><br/> <span data-ttu-id="e7c64-120">**최대 처리량:** 복제된 컴퓨터는 Azure에서 하나의 저장소 계정에 속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-120">**Maximum throughput:** A replicated machine can belong to one storage account in Azure.</span></span> <span data-ttu-id="e7c64-121">표준 저장소 계정은 초당 최대 20,000개의 요청을 처리할 수 있으며 원본 컴퓨터의 IOPS(초당 입력/출력 작업 수)를 20,000으로 유지하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-121">A standard storage account can handle a maximum of 20,000 requests per second, and we recommend that you keep the number of input/output operations per second (IOPS) across a source machine to 20,000.</span></span> <span data-ttu-id="e7c64-122">예를 들어 원본 컴퓨터의 디스크가 5개이고 각 디스크가 원본 컴퓨터에서 120 IOPS(8K 크기)를 생성할 경우 Azure 내에서 디스크당 IOPS 한도인 500을 초과하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-122">For example, if you have a source machine with 5 disks, and each disk generates 120 IOPS (8K size) on the source machine, then it will be within the Azure per disk IOPS limit of 500.</span></span> <span data-ttu-id="e7c64-123">(필요한 저장소 계정 수는 총 원본 컴퓨터 IOPS 수를 20,000으로 나눈 값입니다.)</span><span class="sxs-lookup"><span data-stu-id="e7c64-123">(The number of storage accounts required is equal to the total source machine IOPS, divided by 20,000.)</span></span>

## <a name="configuration-server-capacity"></a><span data-ttu-id="e7c64-124">구성 서버 용량</span><span class="sxs-lookup"><span data-stu-id="e7c64-124">Configuration server capacity</span></span>

<span data-ttu-id="e7c64-125">구성 서버는 보호된 컴퓨터에서 실행되는 모든 워크로드에 대한 일일 변경률 용량을 처리할 수 있어야 하며 데이터를 Azure storage로 지속적으로 복제할 만큼 충분한 대역폭을 보유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-125">The configuration server should be able to handle the daily change rate capacity across all workloads running on protected machines, and needs sufficient bandwidth to continuously replicate data to Azure Storage.</span></span>

<span data-ttu-id="e7c64-126">가장 좋은 방법은 보호하려는 컴퓨터와 동일한 네트워크 및 LAN 세그먼트에 구성 서버를 배치하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-126">As a best practice, locate the configuration server on the same network and LAN segment as the machines you want to protect.</span></span> <span data-ttu-id="e7c64-127">다른 네트워크에 배치할 수도 있지만 보호하려는 컴퓨터에서 구성 서버의 L3 네트워크를 볼 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-127">It can be located on a different network, but machines you want to protect should have layer 3 network visibility to it.</span></span>

## <a name="sizing-recommendations"></a><span data-ttu-id="e7c64-128">크기 조정 권장 사항</span><span class="sxs-lookup"><span data-stu-id="e7c64-128">Sizing recommendations</span></span>

<span data-ttu-id="e7c64-129">표에 CPU를 기반으로 하는 크기 조정 권장 사항이 요약되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-129">The table summarizes sizing recommendations based on CPU.</span></span>

<span data-ttu-id="e7c64-130">**CPU**</span><span class="sxs-lookup"><span data-stu-id="e7c64-130">**CPU**</span></span> | <span data-ttu-id="e7c64-131">**메모리**</span><span class="sxs-lookup"><span data-stu-id="e7c64-131">**Memory**</span></span> | <span data-ttu-id="e7c64-132">**캐시 디스크 크기**</span><span class="sxs-lookup"><span data-stu-id="e7c64-132">**Cache disk size**</span></span> | <span data-ttu-id="e7c64-133">**데이터 변경률**</span><span class="sxs-lookup"><span data-stu-id="e7c64-133">**Data change rate**</span></span> | <span data-ttu-id="e7c64-134">**보호된 컴퓨터**</span><span class="sxs-lookup"><span data-stu-id="e7c64-134">**Protected machines**</span></span>
--- | --- | --- | --- | ---
<span data-ttu-id="e7c64-135">8개 vCPU(2개 소켓 * 4코어 @ 2.5GHz)</span><span class="sxs-lookup"><span data-stu-id="e7c64-135">8 vCPUs (2 sockets * 4 cores @ 2.5 gigahertz [GHz])</span></span> | <span data-ttu-id="e7c64-136">16GB</span><span class="sxs-lookup"><span data-stu-id="e7c64-136">16 GB</span></span> | <span data-ttu-id="e7c64-137">300GB</span><span class="sxs-lookup"><span data-stu-id="e7c64-137">300 GB</span></span> | <span data-ttu-id="e7c64-138">500GB 이하</span><span class="sxs-lookup"><span data-stu-id="e7c64-138">500 GB or less</span></span> | <span data-ttu-id="e7c64-139">100대 미만의 컴퓨터를 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-139">Replicate less than 100 machines.</span></span>
<span data-ttu-id="e7c64-140">12개 vCPU(2개 소켓 * 6코어 @ 2.5GHz)</span><span class="sxs-lookup"><span data-stu-id="e7c64-140">12 vCPUs (2 sockets * 6 cores @ 2.5 GHz)</span></span> | <span data-ttu-id="e7c64-141">18GB</span><span class="sxs-lookup"><span data-stu-id="e7c64-141">18 GB</span></span> | <span data-ttu-id="e7c64-142">600GB</span><span class="sxs-lookup"><span data-stu-id="e7c64-142">600 GB</span></span> | <span data-ttu-id="e7c64-143">500GB ~ 1TB</span><span class="sxs-lookup"><span data-stu-id="e7c64-143">500 GB to 1 TB</span></span> | <span data-ttu-id="e7c64-144">100-150대 컴퓨터를 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-144">Replicate between 100-150 machines.</span></span>
<span data-ttu-id="e7c64-145">16개 vCPU(2개 소켓 * 8코어 @ 2.5GHz)</span><span class="sxs-lookup"><span data-stu-id="e7c64-145">16 vCPUs (2 sockets * 8 cores @ 2.5 GHz)</span></span> | <span data-ttu-id="e7c64-146">32GB</span><span class="sxs-lookup"><span data-stu-id="e7c64-146">32 GB</span></span> | <span data-ttu-id="e7c64-147">1TB</span><span class="sxs-lookup"><span data-stu-id="e7c64-147">1 TB</span></span> | <span data-ttu-id="e7c64-148">1TB ~ 2TB</span><span class="sxs-lookup"><span data-stu-id="e7c64-148">1 TB to 2 TB</span></span> | <span data-ttu-id="e7c64-149">150-200대 컴퓨터를 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-149">Replicate between 150-200 machines.</span></span>
<span data-ttu-id="e7c64-150">다른 프로세스 서버 배포</span><span class="sxs-lookup"><span data-stu-id="e7c64-150">Deploy another process server</span></span> | | | <span data-ttu-id="e7c64-151">> 2TB</span><span class="sxs-lookup"><span data-stu-id="e7c64-151">> 2 TB</span></span> | <span data-ttu-id="e7c64-152">200대 이상의 컴퓨터를 복제하는 경우 또는 일일 데이터 변경률이 2TB를 초과하는 경우 추가 프로세스 서버를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-152">Deploy additional process servers if you're replicating more than 200 machines, or if the daily data change rate exceeds 2 TB.</span></span>

<span data-ttu-id="e7c64-153">여기서,</span><span class="sxs-lookup"><span data-stu-id="e7c64-153">Where:</span></span>

* <span data-ttu-id="e7c64-154">각 원본 컴퓨터는 각각 100GB의 디스크 3개로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-154">Each source machine is configured with 3 disks of 100 GB each.</span></span>
* <span data-ttu-id="e7c64-155">캐시 디스크 측정을 위해 벤치마킹 저장소로 RAID 10을 이용한 10K RPM의 8개 SAS 드라이브를 사용했습니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-155">We used benchmarking storage of 8 SAS drives of 10 K RPM, with RAID 10, for cache disk measurements.</span></span>

## <a name="process-server-capacity"></a><span data-ttu-id="e7c64-156">프로세스 서버 용량</span><span class="sxs-lookup"><span data-stu-id="e7c64-156">Process server capacity</span></span>


<span data-ttu-id="e7c64-157">프로세스 서버는 보호된 컴퓨터에서 데이터를 수신하고 캐싱, 압축 및 암호화를 사용하여 최적화합니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-157">The process server receives replication data from protected machines, and optimizes it with caching, compression, and encryption.</span></span> <span data-ttu-id="e7c64-158">그런 다음 Azure에 데이터를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-158">Then it sends the data to Azure.</span></span>

- <span data-ttu-id="e7c64-159">프로세스 서버 컴퓨터에는 이러한 작업을 수행할 충분한 리소스가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-159">The process server machine should have sufficient resources to perform these tasks.</span></span>
- <span data-ttu-id="e7c64-160">첫 번째 프로세스 서버는 기본적으로 구성 서버에 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-160">The first process server is installed by default on the configuration server.</span></span> <span data-ttu-id="e7c64-161">사용자 환경의 크기를 조정하는 추가 프로세스 서버를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-161">You can deploy additional process servers to scale your environment.</span></span>
- <span data-ttu-id="e7c64-162">프로세스 서버는 디스크 기반 캐시를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-162">The process server uses a disk-based cache.</span></span> <span data-ttu-id="e7c64-163">네트워크 병목 현상 또는 중단이 발생하는 경우 저장된 데이터 변경을 처리할 수 있도록 600GB 이상의 별도의 캐시 디스크를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="e7c64-163">Use a separate cache disk of 600 GB or more to handle data changes stored in the event of a network bottleneck or outage.</span></span>
- <span data-ttu-id="e7c64-164">200대보다 많은 컴퓨터를 보호해야 하거나 일일 변경률이 2TB를 초과하는 경우 복제 로드를 처리할 프로세스 서버를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-164">If you need to protect more than 200 machines, or the daily change rate is greater than 2 TB, you can add process servers to handle the replication load.</span></span> <span data-ttu-id="e7c64-165">다음과 같이 규모를 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-165">To scale out, you can:</span></span>
    - <span data-ttu-id="e7c64-166">구성 서버의 수를 늘립니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-166">Increase the number of configuration servers.</span></span> <span data-ttu-id="e7c64-167">예를 들어 구성 서버를 두 대 사용할 경우 최대 400대의 컴퓨터를 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-167">For example, you can protect up to 400 machines with two configuration servers.</span></span>
    - <span data-ttu-id="e7c64-168">프로세스 서버를 추가하고 추가한 프로세스 서버를 사용하여 구성 서버 대신(또는 추가로) 트래픽을 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-168">Add more process servers, and use these to handle traffic instead of (or in addition to) the configuration server.</span></span>


### <a name="example-process-server-scaling"></a><span data-ttu-id="e7c64-169">예제 프로세스 서버 크기 조정</span><span class="sxs-lookup"><span data-stu-id="e7c64-169">Example process server scaling</span></span>

<span data-ttu-id="e7c64-170">다음 테이블에서는 다음과 같은 시나리오를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-170">The following table describes a scenario in which:</span></span>

* <span data-ttu-id="e7c64-171">구성 서버를 프로세스 서버로 사용할 계획이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-171">You're not planning to use the configuration server as a process server.</span></span>
* <span data-ttu-id="e7c64-172">추가 프로세스 서버를 설정했습니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-172">You've set up an additional process server.</span></span>
* <span data-ttu-id="e7c64-173">추가 프로세스 서버를 사용하도록 보호된 가상 컴퓨터를 구성했습니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-173">You've configured protected virtual machines to use the additional process server.</span></span>
* <span data-ttu-id="e7c64-174">보호된 원본 컴퓨터는 각각 100GB의 디스크 3개로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-174">Each protected source machine is configured with three disks of 100 GB each.</span></span>

<span data-ttu-id="e7c64-175">**구성 서버**</span><span class="sxs-lookup"><span data-stu-id="e7c64-175">**Configuration server**</span></span> | <span data-ttu-id="e7c64-176">**추가 프로세스 서버**</span><span class="sxs-lookup"><span data-stu-id="e7c64-176">**Additional process server**</span></span> | <span data-ttu-id="e7c64-177">**캐시 디스크 크기**</span><span class="sxs-lookup"><span data-stu-id="e7c64-177">**Cache disk size**</span></span> | <span data-ttu-id="e7c64-178">**데이터 변경률**</span><span class="sxs-lookup"><span data-stu-id="e7c64-178">**Data change rate**</span></span> | <span data-ttu-id="e7c64-179">**보호된 컴퓨터**</span><span class="sxs-lookup"><span data-stu-id="e7c64-179">**Protected machines**</span></span>
--- | --- | --- | --- | ---
<span data-ttu-id="e7c64-180">8개 vCPU(2개 소켓 * 4코어 @ 2.5GHz), 16GB 메모리</span><span class="sxs-lookup"><span data-stu-id="e7c64-180">8 vCPUs (2 sockets * 4 cores @ 2.5 GHz), 16 GB memory</span></span> | <span data-ttu-id="e7c64-181">4개 vCPU(2개 소켓 * 2코어 @ 2.5GHz), 8GB 메모리</span><span class="sxs-lookup"><span data-stu-id="e7c64-181">4 vCPUs (2 sockets * 2 cores @ 2.5 GHz), 8 GB memory</span></span> | <span data-ttu-id="e7c64-182">300GB</span><span class="sxs-lookup"><span data-stu-id="e7c64-182">300 GB</span></span> | <span data-ttu-id="e7c64-183">250GB 이하</span><span class="sxs-lookup"><span data-stu-id="e7c64-183">250 GB or less</span></span> | <span data-ttu-id="e7c64-184">85개 이하의 컴퓨터를 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-184">Replicate 85 or fewer machines.</span></span>
<span data-ttu-id="e7c64-185">8개 vCPU(2개 소켓 * 4코어 @ 2.5GHz), 16GB 메모리</span><span class="sxs-lookup"><span data-stu-id="e7c64-185">8 vCPUs (2 sockets * 4 cores @ 2.5 GHz), 16 GB memory</span></span> | <span data-ttu-id="e7c64-186">8개 vCPU(2개 소켓 * 4코어 @ 2.5GHz), 12GB 메모리</span><span class="sxs-lookup"><span data-stu-id="e7c64-186">8 vCPUs (2 sockets * 4 cores @ 2.5 GHz), 12 GB memory</span></span> | <span data-ttu-id="e7c64-187">600GB</span><span class="sxs-lookup"><span data-stu-id="e7c64-187">600 GB</span></span> | <span data-ttu-id="e7c64-188">250GB ~ 1TB</span><span class="sxs-lookup"><span data-stu-id="e7c64-188">250 GB to 1 TB</span></span> | <span data-ttu-id="e7c64-189">85-150대 컴퓨터를 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-189">Replicate between 85-150 machines.</span></span>
<span data-ttu-id="e7c64-190">12개 vCPU(2개 소켓 * 6코어 @ 2.5GHz), 18GB 메모리</span><span class="sxs-lookup"><span data-stu-id="e7c64-190">12 vCPUs (2 sockets * 6 cores @ 2.5 GHz), 18 GB memory</span></span> | <span data-ttu-id="e7c64-191">12개 vCPU(2개 소켓 * 6코어 @ 2.5GHz), 24GB 메모리</span><span class="sxs-lookup"><span data-stu-id="e7c64-191">12 vCPUs (2 sockets * 6 cores @ 2.5 GHz) 24 GB memory</span></span> | <span data-ttu-id="e7c64-192">1TB</span><span class="sxs-lookup"><span data-stu-id="e7c64-192">1 TB</span></span> | <span data-ttu-id="e7c64-193">1TB ~ 2TB</span><span class="sxs-lookup"><span data-stu-id="e7c64-193">1 TB to 2 TB</span></span> | <span data-ttu-id="e7c64-194">150-225대 컴퓨터를 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-194">Replicate between 150-225 machines.</span></span>

<span data-ttu-id="e7c64-195">서버 크기를 조정하는 방법은 모델을 강화할지, 규모를 확장할지에 대한 선호도에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-195">The way in which you scale your servers depends on your preference for a scale-up or scale-out model.</span></span>  <span data-ttu-id="e7c64-196">몇 가지 고급 구성 및 프로세스 서버를 배포하여 강화하거나 적은 리소스로 더 많은 서버를 배포하여 규모를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-196">You scale up by deploying a few high-end configuration and process servers, or scale out by deploying more servers with fewer resources.</span></span> <span data-ttu-id="e7c64-197">예를 들어 220대 컴퓨터를 보호해야 하는 경우 다음 중 하나를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-197">For example, if you need to protect 220 machines, you could do either of the following:</span></span>

* <span data-ttu-id="e7c64-198">vCPU 12개, 메모리 18GB인 구성 서버와 vCPU 12개, 메모리 24GB인 추가 프로세스 서버를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-198">Set up the configuration server with 12 vCPU, 18 GB of memory, and an additional process server with 12 vCPU, 24 GB of memory.</span></span> <span data-ttu-id="e7c64-199">추가 프로세스 서버만 사용하도록 보호된 컴퓨터를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-199">Configure protected machines to use the additional process server only.</span></span>
* <span data-ttu-id="e7c64-200">구성 서버 두 개(2 x 8 vCPU, 16GB RAM)와 추가 프로세스 서버 두 개(135 + 85 [220]개 컴퓨터를 처리할 1 x 8 vCPU 및 4 vCPU x 1)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-200">Set up two configuration servers (2 x 8 vCPU, 16 GB RAM) and two additional process servers (1 x 8 vCPU and 4 vCPU x 1 to handle 135 + 85 [220] machines).</span></span> <span data-ttu-id="e7c64-201">추가 프로세스 서버만 사용하도록 보호된 컴퓨터를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-201">Configure protected machines to use the additional process servers only.</span></span>

## <a name="deploy-additional-process-servers"></a><span data-ttu-id="e7c64-202">추가 프로세스 서버 배포</span><span class="sxs-lookup"><span data-stu-id="e7c64-202">Deploy additional process servers</span></span>

<span data-ttu-id="e7c64-203">이 지침에 따라 추가 프로세스 서버를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-203">Follow these instructions to set up an additional process server.</span></span> <span data-ttu-id="e7c64-204">서버를 설정한 후 이를 사용하도록 원본 컴퓨터를 마이그레이션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-204">After setting up the server, you migrate source machines to use it.</span></span>

1. <span data-ttu-id="e7c64-205">**Site Recovery 서버**에서 구성 서버 > **+프로세스 서버**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-205">In **Site Recovery servers**, click the configuration server > **+Process Server**.</span></span>
2. <span data-ttu-id="e7c64-206">**서버 형식**에서 **프로세스 서버(온-프레미스)**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-206">In **Server type**, click **Process server (on-premises)**.</span></span>

    ![프로세스 서버](./media/vmware-walkthrough-capacity/migrate-ps2.png)
3. <span data-ttu-id="e7c64-208">Site Recovery 통합 설치 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-208">Download the Site Recovery Unified Setup file.</span></span>
4. <span data-ttu-id="e7c64-209">설치 프로그램을 실행하여 프로세스 서버를 설치하고 자격 증명 모음에 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-209">Run setup to install the process server, and register it in the vault.</span></span>
5. <span data-ttu-id="e7c64-210">**시작하기 전에**에서 **배포 규모 확장을 위해 추가 프로세스 서버 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-210">In **Before you begin**, select **Add additional process servers to scale out deployment**.</span></span>
6. <span data-ttu-id="e7c64-211">**구성 서버 세부 정보**에서 구성 서버의 IP 주소 및 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-211">In **Configuration Server Details**, specify the IP address of the configuration server, and the passphrase.</span></span> <span data-ttu-id="e7c64-212">암호가 없는 경우 구성 서버에서 **[SiteRecoveryInstallationFolder]\home\sysystems\bin\genpassphrase.exe –n**을 실행하여 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-212">If you don't have the passphrase, get it by running **[SiteRecoveryInstallationFolder]\home\sysystems\bin\genpassphrase.exe –n** on the configuration server.</span></span>

    ![구성 서버](./media/vmware-walkthrough-capacity/add-ps2.png)
7. <span data-ttu-id="e7c64-214">구성 서버를 설정할 때 수행한 것과 동일한 방식으로 나머지 설치를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-214">Complete the rest of setup in the same way you did when you set up the configuration server.</span></span>

### <a name="migrate-machines-to-use-the-process-server"></a><span data-ttu-id="e7c64-215">프로세스 서버를 사용하도록 컴퓨터 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="e7c64-215">Migrate machines to use the process server</span></span>

1. <span data-ttu-id="e7c64-216">**설정** > **Site Recovery 서버**에서 구성 서버 > **프로세스 서버**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-216">In **Settings** > **Site Recovery servers**, click the configuration server > **Process servers**.</span></span>
2. <span data-ttu-id="e7c64-217">현재 사용 중인 프로세스 서버를 마우스 오른쪽 버튼으로 클릭하고 > **전환**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-217">Right-click the process server currently in use > **Switch**.</span></span>

    ![프로세스 서버 전환](./media/vmware-walkthrough-capacity/migrate-ps3.png)
3. <span data-ttu-id="e7c64-219">**대상 프로세스 서버 선택**에서 사용할 프로세스 서버를 선택한 다음 서버가 처리할 VM을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-219">In **Select target process server**, select the process server you want to use, and select the VMs that the server will handle.</span></span>
4. <span data-ttu-id="e7c64-220">정보 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-220">Click the information icon.</span></span> <span data-ttu-id="e7c64-221">부하를 결정할 수 있도록 선택된 각 VM을 새 프로세스 서버로 복제하는 데 필요한 평균 공간이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-221">To help you make load decisions, the average space that's needed to replicate each selected VM to the new process server is displayed.</span></span>
5. <span data-ttu-id="e7c64-222">새 프로세스 서버로 복제를 시작하려면 확인 표시를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-222">Click the check mark to start replication to the new process server.</span></span>

## <a name="control-network-bandwidth"></a><span data-ttu-id="e7c64-223">네트워크 대역폭 제어</span><span class="sxs-lookup"><span data-stu-id="e7c64-223">Control network bandwidth</span></span>

<span data-ttu-id="e7c64-224">[Deployment Planner 도구](site-recovery-deployment-planner.md)를 실행하여 복제(초기 복제 및 델타)에 필요한 대역폭을 계산한 후 두 가지 옵션을 사용하여 복제에 사용된 대역폭 양을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-224">After you run [the Deployment Planner tool](site-recovery-deployment-planner.md) to calculate the bandwidth you need for replication (the initial replication and then delta), you can control the amount of bandwidth used for replication using a couple of options:</span></span>

* <span data-ttu-id="e7c64-225">**대역폭 제한**: Azure에 복제하는 VMware 트래픽이 특정 프로세스 서버를 통과합니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-225">**Throttle bandwidth**: VMware traffic that replicates to Azure goes through a specific process server.</span></span> <span data-ttu-id="e7c64-226">프로세스 서버로 실행되는 컴퓨터에서 대역폭을 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-226">You can throttle bandwidth on the machines running as process servers.</span></span>
* <span data-ttu-id="e7c64-227">**대역폭 영향**: 몇 가지 레지스트리 키를 사용하면 복제에 사용되는 대역폭에 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-227">**Influence bandwidth**: You can influence the bandwidth used for replication by using a couple of registry keys:</span></span>
  * <span data-ttu-id="e7c64-228">**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\UploadThreadsPerVM** 레지스트리 값은 디스크의 데이터 전송(초기 또는 델타 복제)에 사용되는 스레드 수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-228">The **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\UploadThreadsPerVM** registry value specifies the number of threads that are used for data transfer (initial or delta replication) of a disk.</span></span> <span data-ttu-id="e7c64-229">값이 높을수록 복제에 사용되는 네트워크 대역폭이 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-229">A higher value increases the network bandwidth used for replication.</span></span>
  * <span data-ttu-id="e7c64-230">**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\DownloadThreadsPerVM**은 장애 복구(failback) 동안 데이터 전송에 사용되는 스레드 수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-230">The **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\DownloadThreadsPerVM** specifies the number of threads used for data transfer during failback.</span></span>

### <a name="throttle-bandwidth"></a><span data-ttu-id="e7c64-231">대역폭 제한</span><span class="sxs-lookup"><span data-stu-id="e7c64-231">Throttle bandwidth</span></span>

1. <span data-ttu-id="e7c64-232">프로세스 서버 역할을 하는 컴퓨터에서 Azure Backup MMC 스냅인을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-232">Open the Azure Backup MMC snap-in on the machine acting as the process server.</span></span> <span data-ttu-id="e7c64-233">기본적으로 바탕 화면 또는 C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin 폴더에 Backup의 바로 가기가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-233">By default, a shortcut for Backup is available on the desktop, or in the following folder: C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.</span></span>
2. <span data-ttu-id="e7c64-234">스냅인에서 **속성 변경**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-234">In the snap-in, click **Change Properties**.</span></span>
3. <span data-ttu-id="e7c64-235">**제한** 탭에서 **백업 작업에 인터넷 대역폭 사용 제한 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-235">On the **Throttling** tab, select **Enable internet bandwidth usage throttling for backup operations**.</span></span>
4. <span data-ttu-id="e7c64-236">작업 시간 및 비 작업 시간의 제한을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-236">Set the limits for work and non-work hours.</span></span> <span data-ttu-id="e7c64-237">유효 범위는 초당 512Kbps~102Mbp입니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-237">Valid ranges are from 512 Kbps to 102 Mbps per second.</span></span>

    ![제한](./media/vmware-walkthrough-capacity/throttle2.png)

<span data-ttu-id="e7c64-239">[Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) cmdlet를 사용하여 제한을 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-239">You can also use the [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) cmdlet to set throttling.</span></span> <span data-ttu-id="e7c64-240">다음은 샘플입니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-240">Here's a sample:</span></span>

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

<span data-ttu-id="e7c64-241">**Set-OBMachineSetting -NoThrottle** 은 제한이 필요 없다는 뜻입니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-241">**Set-OBMachineSetting -NoThrottle** indicates that no throttling is required.</span></span>

### <a name="influence-network-bandwidth-for-a-vm"></a><span data-ttu-id="e7c64-242">VM의 네트워크 대역폭에 영향</span><span class="sxs-lookup"><span data-stu-id="e7c64-242">Influence network bandwidth for a VM</span></span>

1. <span data-ttu-id="e7c64-243">VM의 레지스트리에서 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-243">In registry of the VM, go to **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**.</span></span>
   * <span data-ttu-id="e7c64-244">복제 디스크의 대역폭 트래픽에 영향을 주려면 **UploadThreadsPerVM** 값을 수정하거나 키가 없는 경우 키를 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-244">To influence the bandwidth traffic on a replicating disk, modify the value of **UploadThreadsPerVM**, or create the key if it doesn't exist.</span></span>
   * <span data-ttu-id="e7c64-245">Azure에서 장애 복구(failback) 트래픽에 대한 대역폭에 영향을 주려면 **DownloadThreadsPerVM** 값을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-245">To influence the bandwidth for failback traffic from Azure, modify the value of **DownloadThreadsPerVM**.</span></span>
2. <span data-ttu-id="e7c64-246">기본값은 4입니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-246">The default value is 4.</span></span> <span data-ttu-id="e7c64-247">과도하게 프로비전된 네트워크에서는 이러한 레지스트리 키를 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-247">In an overprovisioned network, these registry keys should be modified.</span></span> <span data-ttu-id="e7c64-248">최대값은 32입니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-248">The maximum is 32.</span></span> <span data-ttu-id="e7c64-249">트래픽을 모니터링하여 값을 최적화합니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-249">Monitor traffic to optimize the value.</span></span>




## <a name="next-steps"></a><span data-ttu-id="e7c64-250">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e7c64-250">Next steps</span></span>

<span data-ttu-id="e7c64-251">[4단계: 네트워킹 계획](vmware-walkthrough-network.md)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e7c64-251">Go to [Step 4: Plan networking](vmware-walkthrough-network.md).</span></span>
