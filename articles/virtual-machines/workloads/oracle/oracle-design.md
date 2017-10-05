---
title: "Azure에서 Oracle 데이터베이스 설계 및 구현 | Microsoft Docs"
description: "Azure 환경에서 Oracle 데이터베이스를 설계하고 구현합니다."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: v-shiuma
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 6/22/2017
ms.author: rclaus
ms.openlocfilehash: 1af7e1d40a0eb129875dd6a30ac899f2025bee13
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="design-and-implement-an-oracle-database-in-azure"></a><span data-ttu-id="e9208-103">Azure에서 Oracle 데이터베이스 설계 및 구현</span><span class="sxs-lookup"><span data-stu-id="e9208-103">Design and implement an Oracle database in Azure</span></span>

## <a name="assumptions"></a><span data-ttu-id="e9208-104">가정</span><span class="sxs-lookup"><span data-stu-id="e9208-104">Assumptions</span></span>

- <span data-ttu-id="e9208-105">온-프레미스에서 Azure로 Oracle 데이터베이스 마이그레이션할 계획입니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-105">You're planning to migrate an Oracle database from on-premises to Azure.</span></span>
- <span data-ttu-id="e9208-106">Oracle AWR 보고서의 다양한 메트릭에 대해 이해하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-106">You have an understanding of the various metrics in Oracle AWR reports.</span></span>
- <span data-ttu-id="e9208-107">응용 프로그램 성능 및 플랫폼 사용률에 대해 기본적으로 이해하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-107">You have a baseline understanding of application performance and platform utilization.</span></span>

## <a name="goals"></a><span data-ttu-id="e9208-108">목표</span><span class="sxs-lookup"><span data-stu-id="e9208-108">Goals</span></span>

- <span data-ttu-id="e9208-109">Azure에서 Oracle 배포를 최적화하는 방법을 이해합니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-109">Understand how to optimize your Oracle deployment in Azure.</span></span>
- <span data-ttu-id="e9208-110">Azure 환경에서 Oracle 데이터베이스에 대한 성능 튜닝 옵션을 탐색합니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-110">Explore performance tuning options for an Oracle database in an Azure environment.</span></span>

## <a name="the-differences-between-an-on-premises-and-azure-implementation"></a><span data-ttu-id="e9208-111">온-프레미스와 Azure 구현 간의 차이점</span><span class="sxs-lookup"><span data-stu-id="e9208-111">The differences between an on-premises and Azure implementation</span></span> 

<span data-ttu-id="e9208-112">다음은 온-프레미스 응용 프로그램을 Azure로 마이그레이션할 때 유의해야 할 몇 가지 중요 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-112">Following are some important things to keep in mind when you're migrating on-premises applications to Azure.</span></span> 

<span data-ttu-id="e9208-113">중요한 차이점 중 하나는 Azure 구현에서 VM, 디스크 및 가상 네트워크와 같은 리소스가 다른 클라이언트와 공유된다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-113">One important difference is that in an Azure implementation, resources such as VMs, disks, and virtual networks are shared among other clients.</span></span> <span data-ttu-id="e9208-114">또한 리소스는 요구 사항에 따라 제한될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-114">In addition, resources can be throttled based on the requirements.</span></span> <span data-ttu-id="e9208-115">Azure에서는 실패 방지(MTBF)에 집중하는 대신 실패 극복(MTTR)에 더 많이 집중합니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-115">Instead of focusing on avoiding failing (MTBF), Azure is more focused on surviving the failure (MTTR).</span></span>

<span data-ttu-id="e9208-116">다음 표에는 Oracle 데이터베이스의 온-프레미스 구현과 Azure 구현 간의 차이점이 나열되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-116">The following table lists some of the differences between an on-premises implementation and an Azure implementation of an Oracle database.</span></span>

> 
> |  | <span data-ttu-id="e9208-117">**온-프레미스 구현**</span><span class="sxs-lookup"><span data-stu-id="e9208-117">**On-premises implementation**</span></span> | <span data-ttu-id="e9208-118">**Azure 구현**</span><span class="sxs-lookup"><span data-stu-id="e9208-118">**Azure implementation**</span></span> |
> | --- | --- | --- |
> | <span data-ttu-id="e9208-119">**네트워킹**</span><span class="sxs-lookup"><span data-stu-id="e9208-119">**Networking**</span></span> |<span data-ttu-id="e9208-120">LAN/WAN</span><span class="sxs-lookup"><span data-stu-id="e9208-120">LAN/WAN</span></span>  |<span data-ttu-id="e9208-121">SDN(소프트웨어 방식 네트워킹)</span><span class="sxs-lookup"><span data-stu-id="e9208-121">SDN (software-defined networking)</span></span>|
> | <span data-ttu-id="e9208-122">**보안 그룹**</span><span class="sxs-lookup"><span data-stu-id="e9208-122">**Security group**</span></span> |<span data-ttu-id="e9208-123">IP/포트 제한 도구</span><span class="sxs-lookup"><span data-stu-id="e9208-123">IP/port restriction tools</span></span> |[<span data-ttu-id="e9208-124">NSG(네트워크 보안 그룹)</span><span class="sxs-lookup"><span data-stu-id="e9208-124">Network Security Group (NSG)</span></span>](https://azure.microsoft.com/blog/network-security-groups) |
> | <span data-ttu-id="e9208-125">**복원력**</span><span class="sxs-lookup"><span data-stu-id="e9208-125">**Resilience**</span></span> |<span data-ttu-id="e9208-126">MTBF(평균 고장 간격)</span><span class="sxs-lookup"><span data-stu-id="e9208-126">MTBF (mean time between failures)</span></span> |<span data-ttu-id="e9208-127">MTTR(평균 복구 시간)</span><span class="sxs-lookup"><span data-stu-id="e9208-127">MTTR (mean time to recovery)</span></span>|
> | <span data-ttu-id="e9208-128">**계획된 유지 보수**</span><span class="sxs-lookup"><span data-stu-id="e9208-128">**Planned maintenance**</span></span> |<span data-ttu-id="e9208-129">패치/업그레이드</span><span class="sxs-lookup"><span data-stu-id="e9208-129">Patching/upgrades</span></span>|<span data-ttu-id="e9208-130">[가용성 집합](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines)(Azure에서 관리되는 패치/업그레이드)</span><span class="sxs-lookup"><span data-stu-id="e9208-130">[Availability sets](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines) (patching/upgrades managed by Azure)</span></span> |
> | <span data-ttu-id="e9208-131">**리소스**</span><span class="sxs-lookup"><span data-stu-id="e9208-131">**Resource**</span></span> |<span data-ttu-id="e9208-132">전용</span><span class="sxs-lookup"><span data-stu-id="e9208-132">Dedicated</span></span>  |<span data-ttu-id="e9208-133">다른 클라이언트와 공유</span><span class="sxs-lookup"><span data-stu-id="e9208-133">Shared with other clients</span></span>|
> | <span data-ttu-id="e9208-134">**지역**</span><span class="sxs-lookup"><span data-stu-id="e9208-134">**Regions**</span></span> |<span data-ttu-id="e9208-135">데이터 센터</span><span class="sxs-lookup"><span data-stu-id="e9208-135">Datacenters</span></span> |[<span data-ttu-id="e9208-136">지역 쌍</span><span class="sxs-lookup"><span data-stu-id="e9208-136">Region pairs</span></span>](https://docs.microsoft.com/azure/virtual-machines/windows/regions-and-availability)|
> | <span data-ttu-id="e9208-137">**저장소**</span><span class="sxs-lookup"><span data-stu-id="e9208-137">**Storage**</span></span> |<span data-ttu-id="e9208-138">SAN/실제 디스크</span><span class="sxs-lookup"><span data-stu-id="e9208-138">SAN/physical disks</span></span> |[<span data-ttu-id="e9208-139">Azure 관리 저장소</span><span class="sxs-lookup"><span data-stu-id="e9208-139">Azure-managed storage</span></span>](https://azure.microsoft.com/pricing/details/managed-disks/?v=17.23h)|
> | <span data-ttu-id="e9208-140">**규모**</span><span class="sxs-lookup"><span data-stu-id="e9208-140">**Scale**</span></span> |<span data-ttu-id="e9208-141">수직적 확장</span><span class="sxs-lookup"><span data-stu-id="e9208-141">Vertical scale</span></span> |<span data-ttu-id="e9208-142">수평적 확장</span><span class="sxs-lookup"><span data-stu-id="e9208-142">Horizontal scale</span></span>|


### <a name="requirements"></a><span data-ttu-id="e9208-143">요구 사항</span><span class="sxs-lookup"><span data-stu-id="e9208-143">Requirements</span></span>

- <span data-ttu-id="e9208-144">데이터베이스 크기 및 증가 속도를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-144">Determine the database size and growth rate.</span></span>
- <span data-ttu-id="e9208-145">Oracle AWR 보고서 또는 다른 네트워크 모니터링 도구에 따라 예측할 수 있는 IOPS 요구 사항을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-145">Determine the IOPS requirements, which you can estimate based on Oracle AWR reports or other network monitoring tools.</span></span>

## <a name="configuration-options"></a><span data-ttu-id="e9208-146">구성 옵션</span><span class="sxs-lookup"><span data-stu-id="e9208-146">Configuration options</span></span>

<span data-ttu-id="e9208-147">Azure 환경에서 성능을 향상시키기 위해 조정할 수 있는 잠재적인 네 가지 영역이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-147">There are four potential areas that you can tune to improve performance in an Azure environment:</span></span>

- <span data-ttu-id="e9208-148">가상 컴퓨터 크기</span><span class="sxs-lookup"><span data-stu-id="e9208-148">Virtual machine size</span></span>
- <span data-ttu-id="e9208-149">네트워크 처리량</span><span class="sxs-lookup"><span data-stu-id="e9208-149">Network throughput</span></span>
- <span data-ttu-id="e9208-150">디스크 형식 및 구성</span><span class="sxs-lookup"><span data-stu-id="e9208-150">Disk types and configurations</span></span>
- <span data-ttu-id="e9208-151">디스크 캐시 설정</span><span class="sxs-lookup"><span data-stu-id="e9208-151">Disk cache settings</span></span>

### <a name="generate-an-awr-report"></a><span data-ttu-id="e9208-152">AWR 보고서 생성</span><span class="sxs-lookup"><span data-stu-id="e9208-152">Generate an AWR report</span></span>

<span data-ttu-id="e9208-153">기존 Oracle 데이터베이스가 있고 Azure로 마이그레이션하도록 계획하는 경우 몇 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-153">If you have an existing an Oracle database and are planning to migrate to Azure, you have several options.</span></span> <span data-ttu-id="e9208-154">Oracle AWR 보고서를 실행하여 메트릭(IOPS, Mbps, GiBs 등)을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-154">You can run the Oracle AWR report to get the metrics (IOPS, Mbps, GiBs, and so on).</span></span> <span data-ttu-id="e9208-155">그런 다음 수집한 메트릭을 기반으로 하여 VM을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-155">Then choose the VM based on the metrics that you collected.</span></span> <span data-ttu-id="e9208-156">또는 인프라 팀에 문의하여 유사한 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-156">Or you can contact your infrastructure team to get similar information.</span></span>

<span data-ttu-id="e9208-157">일반 및 최대 워크로드 모두에서 AWR 보고서를 실행하여 비교하는 것이 좋을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-157">You might consider running your AWR report during both regular and peak workloads, so you can compare.</span></span> <span data-ttu-id="e9208-158">이러한 보고서에 따라 평균 워크로드 또는 최대 워크로드를 기준으로 VM 크기를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-158">Based on these reports, you can size the VMs based on either the average workload or the maximum workload.</span></span>

<span data-ttu-id="e9208-159">다음은 AWR 보고서를 생성하는 방법의 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-159">Following is an example of how to generate an AWR report:</span></span>

```bash
$ sqlplus / as sysdba
SQL> EXEC DBMS_WORKLOAD_REPOSITORY.CREATE_SNAPSHOT;
SQL> @?/rdbms/admin/awrrpt.sql
```

### <a name="key-metrics"></a><span data-ttu-id="e9208-160">주요 메트릭</span><span class="sxs-lookup"><span data-stu-id="e9208-160">Key metrics</span></span>

<span data-ttu-id="e9208-161">다음은 AWR 보고서에서 얻을 수 있는 메트릭입니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-161">Following are the metrics that you can obtain from the AWR report:</span></span>

- <span data-ttu-id="e9208-162">총 코어 수</span><span class="sxs-lookup"><span data-stu-id="e9208-162">Total number of cores</span></span>
- <span data-ttu-id="e9208-163">CPU 클럭 속도</span><span class="sxs-lookup"><span data-stu-id="e9208-163">CPU clock speed</span></span>
- <span data-ttu-id="e9208-164">전체 메모리(GB)</span><span class="sxs-lookup"><span data-stu-id="e9208-164">Total memory in GB</span></span>
- <span data-ttu-id="e9208-165">CPU 사용률</span><span class="sxs-lookup"><span data-stu-id="e9208-165">CPU utilization</span></span>
- <span data-ttu-id="e9208-166">최대 데이터 전송 속도</span><span class="sxs-lookup"><span data-stu-id="e9208-166">Peak data transfer rate</span></span>
- <span data-ttu-id="e9208-167">I/O 변경률(읽기/쓰기)</span><span class="sxs-lookup"><span data-stu-id="e9208-167">Rate of I/O changes (read/write)</span></span>
- <span data-ttu-id="e9208-168">다시 실행 로그 속도(MBPs)</span><span class="sxs-lookup"><span data-stu-id="e9208-168">Redo log rate (MBPs)</span></span>
- <span data-ttu-id="e9208-169">네트워크 처리량</span><span class="sxs-lookup"><span data-stu-id="e9208-169">Network throughput</span></span>
- <span data-ttu-id="e9208-170">네트워크 대기 시간 비율(낮음/높음)</span><span class="sxs-lookup"><span data-stu-id="e9208-170">Network latency rate (low/high)</span></span>
- <span data-ttu-id="e9208-171">데이터베이스 크기(GB)</span><span class="sxs-lookup"><span data-stu-id="e9208-171">Database size in GB</span></span>
- <span data-ttu-id="e9208-172">클라이언트 간 SQL*Net을 통해 수신된 바이트 수</span><span class="sxs-lookup"><span data-stu-id="e9208-172">Bytes received via SQL*Net from/to client</span></span>

### <a name="virtual-machine-size"></a><span data-ttu-id="e9208-173">가상 컴퓨터 크기</span><span class="sxs-lookup"><span data-stu-id="e9208-173">Virtual machine size</span></span>

#### <a name="1-estimate-vm-size-based-on-cpu-memory-and-io-usage-from-the-awr-report"></a><span data-ttu-id="e9208-174">1. AWR 보고서의 CPU, 메모리 및 I/O 사용량에 따라 VM 크기 예측</span><span class="sxs-lookup"><span data-stu-id="e9208-174">1. Estimate VM size based on CPU, memory, and I/O usage from the AWR report</span></span>

<span data-ttu-id="e9208-175">시스템 병목 현상이 발생하는 위치를 나타내는 상위 5개 시간 지정 전경 이벤트를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-175">One thing you might look at is the top five timed foreground events that indicate where the system bottlenecks are.</span></span>

<span data-ttu-id="e9208-176">예를 들어 다음 다이어그램에서는 로그 파일 동기화가 맨 위에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-176">For example, in the following diagram, the log file sync is at the top.</span></span> <span data-ttu-id="e9208-177">LGWR에서 로그 버퍼를 다시 실행 로그 파일에 쓰기 전에 필요한 대기 수를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-177">It indicates the number of waits that are required before the LGWR writes the log buffer to the redo log file.</span></span> <span data-ttu-id="e9208-178">이러한 결과는 더 효율적으로 수행되는 저장소 또는 디스크가 필요함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-178">These results indicate that better performing storage or disks are required.</span></span> <span data-ttu-id="e9208-179">또한 다이어그램에서는 CPU(코어) 수와 메모리 양도 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-179">In addition, the diagram also shows the number of CPU (cores) and the amount of memory.</span></span>

![AWR 보고서 페이지의 스크린샷](./media/oracle-design/cpu_memory_info.png)

<span data-ttu-id="e9208-181">다음 다이어그램에서는 읽기 및 쓰기의 총 I/O 수를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-181">The following diagram shows the total I/O of read and write.</span></span> <span data-ttu-id="e9208-182">보고서 시간 동안 59GB의 읽기 및 247.3GB의 쓰기가 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-182">There were 59 GB read and 247.3 GB written during the time of the report.</span></span>

![AWR 보고서 페이지의 스크린샷](./media/oracle-design/io_info.png)

#### <a name="2-choose-a-vm"></a><span data-ttu-id="e9208-184">2. VM 선택</span><span class="sxs-lookup"><span data-stu-id="e9208-184">2. Choose a VM</span></span>

<span data-ttu-id="e9208-185">다음 단계에서는 AWR 보고서에서 수집한 정보에 따라 요구 사항을 충족하는 비슷한 크기의 VM을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-185">Based on the information that you collected from the AWR report, the next step is to choose a VM of a similar size that meets your requirements.</span></span> <span data-ttu-id="e9208-186">[메모리 최적화](https://docs.microsoft.com/azure/virtual-machinFine tune es/virtual-machines-windows-sizes-memory) 문서에서 사용 가능한 VM 목록을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-186">You can find a list of available VMs in the article [Memory optimized](https://docs.microsoft.com/azure/virtual-machinFine tune es/virtual-machines-windows-sizes-memory).</span></span>

#### <a name="3-fine-tune-the-vm-sizing-with-a-similar-vm-series-based-on-the-acu"></a><span data-ttu-id="e9208-187">3. ACU에 따라 비슷한 VM 시리즈로 VM 크기 미세 조정</span><span class="sxs-lookup"><span data-stu-id="e9208-187">3. Fine-tune the VM sizing with a similar VM series based on the ACU</span></span>

<span data-ttu-id="e9208-188">VM을 선택한 후에는 해당 VM에 대한 ACU에 주의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-188">After you've chosen the VM, pay attention to the ACU for the VM.</span></span> <span data-ttu-id="e9208-189">요구 사항에 더 적합한 ACU 값에 따라 다른 VM을 선택할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-189">You might choose a different VM based on the ACU value that better suits your requirements.</span></span> <span data-ttu-id="e9208-190">자세한 내용은 [ACU(Azure Compute 단위)](https://docs.microsoft.com/azure/virtual-machines/windows/acu)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e9208-190">For more information, see [Azure compute unit](https://docs.microsoft.com/azure/virtual-machines/windows/acu).</span></span>

![ACU 단위 페이지의 스크린샷](./media/oracle-design/acu_units.png)

### <a name="network-throughput"></a><span data-ttu-id="e9208-192">네트워크 처리량</span><span class="sxs-lookup"><span data-stu-id="e9208-192">Network throughput</span></span>

<span data-ttu-id="e9208-193">다음 다이어그램에서는 처리량과 IOPS 간의 관계를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-193">The following diagram shows the relation between throughput and IOPS:</span></span>

![처리량 스크린샷](./media/oracle-design/throughput.png)

<span data-ttu-id="e9208-195">총 네트워크 처리량은 다음 정보를 기반으로 하여 예측합니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-195">The total network throughput is estimated based on the following information:</span></span>
- <span data-ttu-id="e9208-196">SQL*Net 트래픽</span><span class="sxs-lookup"><span data-stu-id="e9208-196">SQL*Net traffic</span></span>
- <span data-ttu-id="e9208-197">MBps x 서버 수(Oracle Data Guard와 같은 아웃바운드 스트림)</span><span class="sxs-lookup"><span data-stu-id="e9208-197">MBps x number of servers (outbound stream such as Oracle Data Guard)</span></span>
- <span data-ttu-id="e9208-198">응용 프로그램 복제와 같은 다른 요소</span><span class="sxs-lookup"><span data-stu-id="e9208-198">Other factors, such as application replication</span></span>

![SQL*Net 처리량의 스크린샷](./media/oracle-design/sqlnet_info.png)

<span data-ttu-id="e9208-200">네트워크 대역폭 요구 사항에 따라 다양한 게이트웨이 유형을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-200">Based on your network bandwidth requirements, there are various gateway types for you to choose from.</span></span> <span data-ttu-id="e9208-201">여기에는 기본, VpnGw 및 Azure ExpressRoute가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-201">These include basic, VpnGw, and Azure ExpressRoute.</span></span> <span data-ttu-id="e9208-202">자세한 내용은 [VPN Gateway 가격 페이지](https://azure.microsoft.com/en-us/pricing/details/vpn-gateway/?v=17.23h)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e9208-202">For more information, see the [VPN gateway pricing page](https://azure.microsoft.com/en-us/pricing/details/vpn-gateway/?v=17.23h).</span></span>

<span data-ttu-id="e9208-203">**권장 사항**</span><span class="sxs-lookup"><span data-stu-id="e9208-203">**Recommendations**</span></span>

- <span data-ttu-id="e9208-204">네트워크 대기 시간은 온-프레미스 배포에 비해 더 높습니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-204">Network latency is higher compared to an on-premises deployment.</span></span> <span data-ttu-id="e9208-205">네트워크 왕복 수를 줄이면 성능이 크게 향상될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-205">Reducing network round trips can greatly improve performance.</span></span>
- <span data-ttu-id="e9208-206">왕복을 줄이려면 동일한 가상 컴퓨터에서 트랜잭션이 많은 응용 프로그램 또는 "채팅 가능한(chatty)" 앱을 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-206">To reduce round-trips, consolidate applications that have high transactions or “chatty” apps on the same virtual machine.</span></span>

### <a name="disk-types-and-configurations"></a><span data-ttu-id="e9208-207">디스크 형식 및 구성</span><span class="sxs-lookup"><span data-stu-id="e9208-207">Disk types and configurations</span></span>

- <span data-ttu-id="e9208-208">*기본 OS 디스크*: 이러한 디스크 유형은 영구 데이터 및 캐싱을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-208">*Default OS disks*: These disk types offer persistent data and caching.</span></span> <span data-ttu-id="e9208-209">시작 시 OS 액세스에 최적화되며, 트랜잭션 또는 데이터 웨어하우스(분석) 워크로드용으로는 설계되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-209">They are optimized for OS access at startup, and aren't designed for either transactional or data warehouse (analytical) workloads.</span></span>

- <span data-ttu-id="e9208-210">*비관리 디스크*: 이러한 디스크 유형을 사용하면 VM 디스크에 해당하는 VHD(가상 하드 디스크) 파일을 저장하는 저장소 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-210">*Unmanaged disks*: With these disk types, you manage the storage accounts that store the virtual hard disk (VHD) files that correspond to your VM disks.</span></span> <span data-ttu-id="e9208-211">VHD 파일은 Azure Storage 계정에 페이지 Blob으로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-211">VHD files are stored as page blobs in Azure storage accounts.</span></span>

- <span data-ttu-id="e9208-212">*관리 디스크*: Azure에서 VM 디스크에 사용하는 저장소 계정을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-212">*Managed disks*: Azure manages the storage accounts that you use for your VM disks.</span></span> <span data-ttu-id="e9208-213">필요한 디스크 유형(프리미엄 또는 표준)과 디스크 크기를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-213">You specify the disk type (premium or standard) and the size of the disk that you need.</span></span> <span data-ttu-id="e9208-214">Azure에서 사용자에게 맞는 디스크를 만들고 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-214">Azure creates and manages the disk for you.</span></span>

- <span data-ttu-id="e9208-215">*프리미엄 저장소 디스크*: 이러한 디스크 유형은 프로덕션 워크로드에 가장 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-215">*Premium storage disks*: These disk types are best suited for production workloads.</span></span> <span data-ttu-id="e9208-216">프리미엄 저장소는 특정 크기 시리즈 VM(예: DS, DSv2, GS 및 F 시리즈 VM)에 연결할 수 있는 VM 디스크를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-216">Premium storage supports VM disks that can be attached to specific size-series VMs, such as DS, DSv2, GS, and F series VMs.</span></span> <span data-ttu-id="e9208-217">다양한 크기로 제공되며 32GB에서 4,096GB까지 다양한 디스크를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-217">The premium disk comes with different sizes, and you can choose between disks ranging from 32 GB to 4,096 GB.</span></span> <span data-ttu-id="e9208-218">디스크 크기마다 자체 성능 사양이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-218">Each disk size has its own performance specifications.</span></span> <span data-ttu-id="e9208-219">응용 프로그램 요구 사항에 따라 하나 이상의 디스크를 VM에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-219">Depending on your application requirements, you can attach one or more disks to your VM.</span></span>

<span data-ttu-id="e9208-220">포털에서 새 관리 디스크를 만드는 경우 사용하려는 디스크 유형에 대한 **계정 유형**을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-220">When you create a new managed disk from the portal, you can choose the **Account type** for the type of disk you want to use.</span></span> <span data-ttu-id="e9208-221">사용 가능한 모든 디스크가 드롭다운 메뉴에 표시되는 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-221">Keep in mind that not all available disks are shown in the drop-down menu.</span></span> <span data-ttu-id="e9208-222">특정 VM 크기를 선택하면 해당 VM 크기를 기반으로 하여 사용할 수 있는 프리미엄 저장소 SKU만 메뉴에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-222">After you choose a particular VM size, the menu shows only the available premium storage SKUs that are based on that VM size.</span></span>

![관리되는 디스크 페이지의 스크린샷](./media/oracle-design/premium_disk01.png)

<span data-ttu-id="e9208-224">자세한 내용은 [VM의 고성능 Premium Storage 및 관리 디스크](https://docs.microsoft.com/azure/storage/storage-premium-storage)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e9208-224">For more information, see [High-performance Premium Storage and managed disks for VMs](https://docs.microsoft.com/azure/storage/storage-premium-storage).</span></span>

<span data-ttu-id="e9208-225">VM에서 저장소를 구성한 후 데이터베이스를 만들기 전에 디스크를 로드하여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-225">After you configure your storage on a VM, you might want to load test the disks before creating a database.</span></span> <span data-ttu-id="e9208-226">대기 시간 및 처리량 모두와 관련된 I/O 속도를 알고 있으면 VM에서 대기 시간 목표로 예상되는 처리량을 지원할 수 있는지 확인하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-226">Knowing the I/O rate in terms of both latency and throughput can help you determine if the VMs support the expected throughput with latency targets.</span></span>

<span data-ttu-id="e9208-227">Oracle Orion, Sysbench 및 Fio와 같이 응용 프로그램 부하 테스트를 위한 여러 가지 도구가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-227">There are a number of tools for application load testing, such as Oracle Orion, Sysbench, and Fio.</span></span>

<span data-ttu-id="e9208-228">Oracle 데이터베이스를 배포한 후에 부하 테스트를 다시 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-228">Run the load test again after you've deployed an Oracle database.</span></span> <span data-ttu-id="e9208-229">일반 및 최대 워크로드를 시작합니다. 그러면 결과에서 사용자 환경의 초기 계획을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-229">Start your regular and peak workloads, and the results show you the baseline of your environment.</span></span>

<span data-ttu-id="e9208-230">저장소 크기 대신 IOPS 속도에 따라 저장소 크기를 조정하는 것이 더 중요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-230">It might be more important to size the storage based on the IOPS rate rather than the storage size.</span></span> <span data-ttu-id="e9208-231">예를 들어 필요한 IOPS가 5,000이지만 200GB만 필요한 경우 200GB 이상의 저장소가 있어도 P30 클래스 프리미엄 디스크를 받을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-231">For example, if the required IOPS is 5,000, but you only need 200 GB, you might still get the P30 class premium disk even though it comes with more than 200 GB of storage.</span></span>

<span data-ttu-id="e9208-232">IOPS 속도는 AWR 보고서에서 얻을 수 있으며,</span><span class="sxs-lookup"><span data-stu-id="e9208-232">The IOPS rate can be obtained from the AWR report.</span></span> <span data-ttu-id="e9208-233">다시 실행 로그, 물리적 읽기 및 쓰기 속도로 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-233">It's determined by the redo log, physical reads, and writes rate.</span></span>

![AWR 보고서 페이지의 스크린샷](./media/oracle-design/awr_report.png)

<span data-ttu-id="e9208-235">예를 들어 다시 실행 크기는 초당 12,200,000바이트이며, 11.63MBps와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-235">For example, the redo size is 12,200,000 bytes per second, which is equal to 11.63 MBPs.</span></span>
<span data-ttu-id="e9208-236">IOPS는 12,200,000 / 2,358 = 5,174입니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-236">The IOPS is 12,200,000 / 2,358 = 5,174.</span></span>

<span data-ttu-id="e9208-237">I/O 요구 사항에 대해 명확히 알고 있으면 이러한 요구 사항에 가장 적합한 드라이브 조합을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-237">After you have a clear picture of the I/O requirements, you can choose a combination of drives that are best suited to meet those requirements.</span></span>

<span data-ttu-id="e9208-238">**권장 사항**</span><span class="sxs-lookup"><span data-stu-id="e9208-238">**Recommendations**</span></span>

- <span data-ttu-id="e9208-239">데이터 테이블스페이스의 경우 관리되는 저장소 또는 Oracle ASM을 사용하여 I/O 워크로드를 여러 디스크에 분산합니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-239">For data tablespace, spread the I/O workload across a number of disks by using managed storage or Oracle ASM.</span></span>
- <span data-ttu-id="e9208-240">읽기 및 쓰기 집약적 작업에 대한 I/O 블록 크기가 늘어남에 따라 데이터 디스크를 더 많이 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-240">As the I/O block size increases for read-intensive and write-intensive operations, add more data disks.</span></span>
- <span data-ttu-id="e9208-241">대규모 순차적 프로세스에 대한 블록 크기를 늘립니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-241">Increase the block size for large sequential processes.</span></span>
- <span data-ttu-id="e9208-242">데이터 압축을 사용하여 I/O를 줄입니다(데이터 및 인덱스 모두에 해당).</span><span class="sxs-lookup"><span data-stu-id="e9208-242">Use data compression to reduce I/O (for both data and indexes).</span></span>
- <span data-ttu-id="e9208-243">개별 데이터 디스크에서 다시 실행 로그, 시스템, 임시 디스크를 분리하고 TS를 실행 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-243">Separate redo logs, system, and temps, and undo TS on separate data disks.</span></span>
- <span data-ttu-id="e9208-244">기본 OS 디스크(/dev/sda)에 응용 프로그램 파일을 배치하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-244">Don't put any application files on default OS disks (/dev/sda).</span></span> <span data-ttu-id="e9208-245">이러한 디스크는 빠른 VM 부팅 시간에 맞게 최적화되지 않으며, 응용 프로그램에 좋은 성능을 제공하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-245">These disks aren't optimized for fast VM boot times, and they might not provide good performance for your application.</span></span>

### <a name="disk-cache-settings"></a><span data-ttu-id="e9208-246">디스크 캐시 설정</span><span class="sxs-lookup"><span data-stu-id="e9208-246">Disk cache settings</span></span>

<span data-ttu-id="e9208-247">호스트 캐싱에는 세 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-247">There are three options for host caching:</span></span>

- <span data-ttu-id="e9208-248">*읽기 전용*: 모든 요청이 이후 읽기를 위해 캐시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-248">*Read-only*: All requests are cached for future reads.</span></span> <span data-ttu-id="e9208-249">모든 쓰기는 Azure Blob 저장소에 직접 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-249">All writes are persisted directly to Azure Blob storage.</span></span>

- <span data-ttu-id="e9208-250">*읽기-쓰기*: "미리 읽기" 알고리즘입니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-250">*Read-write*: This is a “read-ahead” algorithm.</span></span> <span data-ttu-id="e9208-251">읽기 및 쓰기가 향후 읽기에 대해 캐시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-251">The reads and writes are cached for future reads.</span></span> <span data-ttu-id="e9208-252">연속 쓰기(write-through) 이외의 쓰기 작업은 먼저 로컬 캐시에 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-252">Non-write-through writes are persisted to the local cache first.</span></span> <span data-ttu-id="e9208-253">SQL Server의 경우 연속 쓰기를 사용하므로 쓰기가 Azure Storage에 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-253">For SQL Server, writes are persisted to Azure Storage because it uses write-through.</span></span> <span data-ttu-id="e9208-254">또한 가벼운 워크로드에 대해 가장 낮은 디스크 대기 시간을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-254">It also provides the lowest disk latency for light workloads.</span></span>

- <span data-ttu-id="e9208-255">*없음*(사용 안 함): 이 옵션을 사용하면 캐시를 무시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-255">*None* (disabled): By using this option, you can bypass the cache.</span></span> <span data-ttu-id="e9208-256">모든 데이터가 디스크에 전송되며 Azure Storage에 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-256">All the data is transferred to disk and persisted to Azure Storage.</span></span> <span data-ttu-id="e9208-257">이 메서드를 사용하면 I/O 집약적 워크로드에 대해 가장 높은 I/O 속도를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-257">This method gives you the highest I/O rate for I/O intensive workloads.</span></span> <span data-ttu-id="e9208-258">"트랜잭션 비용"도 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-258">You also need to take “transaction cost” into consideration.</span></span>

<span data-ttu-id="e9208-259">**권장 사항**</span><span class="sxs-lookup"><span data-stu-id="e9208-259">**Recommendations**</span></span>

<span data-ttu-id="e9208-260">처리량을 최대화하려면 호스트 캐싱에 대해 **없음**으로 시작하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-260">To maximize the throughput, we recommend that you  start with **None** for host caching.</span></span> <span data-ttu-id="e9208-261">Premium Storage의 경우 **읽기 전용** 또는 **없음** 옵션을 사용하여 파일 시스템을 탑재할 때 "barrier"를 사용하지 않도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-261">For Premium Storage, keep in mind that you must disable the "barriers" when you mount the file system with the **ReadOnly** or **None** options.</span></span> <span data-ttu-id="e9208-262">/etc/fstab 파일을 UUID로 디스크에 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-262">Update the /etc/fstab file with the UUID to the disks.</span></span>

<span data-ttu-id="e9208-263">자세한 내용은 [Linux VM용 Premium Storage](https://docs.microsoft.com/azure/storage/storage-premium-storage#premium-storage-for-linux-vms)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e9208-263">For more information, see [Premium Storage for Linux VMs](https://docs.microsoft.com/azure/storage/storage-premium-storage#premium-storage-for-linux-vms).</span></span>

![관리되는 디스크 페이지의 스크린샷](./media/oracle-design/premium_disk02.png)

- <span data-ttu-id="e9208-265">OS 디스크의 경우 기본 **읽기/쓰기** 캐싱을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-265">For OS disks, use default **Read/Write** caching.</span></span>
- <span data-ttu-id="e9208-266">시스템, 임시 및 실행 취소 디스크의 경우 캐싱에 **없음**을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-266">For SYSTEM, TEMP, and UNDO use **None** for caching.</span></span>
- <span data-ttu-id="e9208-267">데이터 디스크의 경우 캐싱에 **없음**을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-267">For DATA, use **None** for caching.</span></span> <span data-ttu-id="e9208-268">그러나 데이터베이스가 읽기 전용이거나 읽기 집약적인 경우 **읽기 전용** 캐싱을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-268">But if your database is read-only or read-intensive, use **Read-only** caching.</span></span>

<span data-ttu-id="e9208-269">데이터 디스크 설정을 저장한 후에 OS 수준에서 드라이브를 분리한 다음 변경한 후에 다시 탑재하지 않는 한 호스트 캐시 설정은 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-269">After your data disk setting is saved, you can't change the host cache setting unless you unmount the drive at the OS level and then remount it after you've made the change.</span></span>


## <a name="security"></a><span data-ttu-id="e9208-270">보안</span><span class="sxs-lookup"><span data-stu-id="e9208-270">Security</span></span>

<span data-ttu-id="e9208-271">Azure 환경을 설정하고 구성한 후의 다음 단계는 네트워크를 보호하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-271">After you have set up and configured your Azure environment, the next step is to secure your network.</span></span> <span data-ttu-id="e9208-272">몇 가지 권장 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-272">Here are some recommendations:</span></span>

- <span data-ttu-id="e9208-273">*NSG 정책*: NSG는 서브넷 또는 NIC에서 정의될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-273">*NSG policy*: NSG can be defined by a subnet or NIC.</span></span> <span data-ttu-id="e9208-274">응용 프로그램 방화벽과 같이 작업에 대한 보안 및 강제 라우팅 모두를 위해 서브넷 수준에서 액세스를 제어하는 것이 더 간단합니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-274">It's simpler to control access at the subnet level both for security and force routing for things like application firewalls.</span></span>

- <span data-ttu-id="e9208-275">*Jumpbox*: 더 안전한 액세스를 위해 관리자는 응용 프로그램 서비스 또는 데이터베이스에 직접 연결하면 안됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-275">*Jumpbox*: For more secure access, administrators should not directly connect to the application service or database.</span></span> <span data-ttu-id="e9208-276">Jumpbox는 관리자 컴퓨터와 Azure 리소스 간 미디어로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-276">A jumpbox is used as a media between the administrator machine and Azure resources.</span></span>
<span data-ttu-id="e9208-277">![Jumpbox 토폴로지 페이지의 스크린샷](./media/oracle-design/jumpbox.png)</span><span class="sxs-lookup"><span data-stu-id="e9208-277">![Screenshot of the Jumpbox topology page](./media/oracle-design/jumpbox.png)</span></span>

    <span data-ttu-id="e9208-278">관리자 컴퓨터는 Jumpbox에 대해 IP가 제한된 액세스만 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-278">The administrator machine should offer IP-restricted access to the jumpbox only.</span></span> <span data-ttu-id="e9208-279">Jumpbox에는 응용 프로그램과 데이터베이스에 대한 액세스 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-279">The jumpbox should have access to the application and database.</span></span>

- <span data-ttu-id="e9208-280">*사설망*(서브넷): NSG 정책에 따라 더 나은 제어를 설정할 수 있도록 응용 프로그램 서비스와 데이터베이스를 별도의 서브넷에 두는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e9208-280">*Private network* (subnets): We recommend that you have the application service and database on separate subnets, so better control can be set by NSG policy.</span></span>


## <a name="additional-reading"></a><span data-ttu-id="e9208-281">추가 참조 자료</span><span class="sxs-lookup"><span data-stu-id="e9208-281">Additional reading</span></span>

- [<span data-ttu-id="e9208-282">Oracle ASM 구성</span><span class="sxs-lookup"><span data-stu-id="e9208-282">Configure Oracle ASM</span></span>](configure-oracle-asm.md)
- [<span data-ttu-id="e9208-283">Oracle Data Guard 구성</span><span class="sxs-lookup"><span data-stu-id="e9208-283">Configure Oracle Data Guard</span></span>](configure-oracle-dataguard.md)
- [<span data-ttu-id="e9208-284">Oracle Golden Gate 구성</span><span class="sxs-lookup"><span data-stu-id="e9208-284">Configure Oracle Golden Gate</span></span>](configure-oracle-golden-gate.md)
- [<span data-ttu-id="e9208-285">Oracle 백업 및 복구</span><span class="sxs-lookup"><span data-stu-id="e9208-285">Oracle backup and recovery</span></span>](oracle-backup-recovery.md)

## <a name="next-steps"></a><span data-ttu-id="e9208-286">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e9208-286">Next steps</span></span>

- [<span data-ttu-id="e9208-287">자습서: 고가용성 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="e9208-287">Tutorial: Create highly available VMs</span></span>](../../linux/create-cli-complete.md)
- [<span data-ttu-id="e9208-288">VM 배포 Azure CLI 샘플 탐색</span><span class="sxs-lookup"><span data-stu-id="e9208-288">Explore VM deployment Azure CLI samples</span></span>](../../linux/cli-samples.md)
