---
title: "Azure에서 데이터베이스 aaaDesign 및 Oracle 구현 | Microsoft Docs"
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
ms.openlocfilehash: 8fa1207458695df1c7330ec626888b1b6b8d8939
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="design-and-implement-an-oracle-database-in-azure"></a><span data-ttu-id="2d939-103">Azure에서 Oracle 데이터베이스 설계 및 구현</span><span class="sxs-lookup"><span data-stu-id="2d939-103">Design and implement an Oracle database in Azure</span></span>

## <a name="assumptions"></a><span data-ttu-id="2d939-104">가정</span><span class="sxs-lookup"><span data-stu-id="2d939-104">Assumptions</span></span>

- <span data-ttu-id="2d939-105">Oracle 데이터베이스에서 온-프레미스 tooAzure toomigrate를 계획 중인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-105">You're planning toomigrate an Oracle database from on-premises tooAzure.</span></span>
- <span data-ttu-id="2d939-106">Hello에 대 한 이해가 다양 한 메트릭을 보고서에 있는 Oracle AWR 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-106">You have an understanding of hello various metrics in Oracle AWR reports.</span></span>
- <span data-ttu-id="2d939-107">응용 프로그램 성능 및 플랫폼 사용률에 대해 기본적으로 이해하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-107">You have a baseline understanding of application performance and platform utilization.</span></span>

## <a name="goals"></a><span data-ttu-id="2d939-108">목표</span><span class="sxs-lookup"><span data-stu-id="2d939-108">Goals</span></span>

- <span data-ttu-id="2d939-109">이해 어떻게 toooptimize Azure에서 Oracle 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-109">Understand how toooptimize your Oracle deployment in Azure.</span></span>
- <span data-ttu-id="2d939-110">Azure 환경에서 Oracle 데이터베이스에 대한 성능 튜닝 옵션을 탐색합니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-110">Explore performance tuning options for an Oracle database in an Azure environment.</span></span>

## <a name="hello-differences-between-an-on-premises-and-azure-implementation"></a><span data-ttu-id="2d939-111">온-프레미스 간의 차이점을 hello 및 Azure 구현</span><span class="sxs-lookup"><span data-stu-id="2d939-111">hello differences between an on-premises and Azure implementation</span></span> 

<span data-ttu-id="2d939-112">다음은 몇 가지 중요 한 마이그레이션하는 경우 고려에서 사항 tookeep 온-프레미스 응용 프로그램 tooAzure입니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-112">Following are some important things tookeep in mind when you're migrating on-premises applications tooAzure.</span></span> 

<span data-ttu-id="2d939-113">중요한 차이점 중 하나는 Azure 구현에서 VM, 디스크 및 가상 네트워크와 같은 리소스가 다른 클라이언트와 공유된다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-113">One important difference is that in an Azure implementation, resources such as VMs, disks, and virtual networks are shared among other clients.</span></span> <span data-ttu-id="2d939-114">또한 리소스 hello 요구 사항에 따라 제한 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-114">In addition, resources can be throttled based on hello requirements.</span></span> <span data-ttu-id="2d939-115">보다 MTBF ()를 실패를 방지, Azure는 더 hello 실패 (MTTR) 정상 작동 하는 데 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-115">Instead of focusing on avoiding failing (MTBF), Azure is more focused on surviving hello failure (MTTR).</span></span>

<span data-ttu-id="2d939-116">hello 다음 표에 온-프레미스 구현 및 Oracle 데이터베이스의 Azure 구현 hello 차이점 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-116">hello following table lists some of hello differences between an on-premises implementation and an Azure implementation of an Oracle database.</span></span>

> 
> |  | <span data-ttu-id="2d939-117">**온-프레미스 구현**</span><span class="sxs-lookup"><span data-stu-id="2d939-117">**On-premises implementation**</span></span> | <span data-ttu-id="2d939-118">**Azure 구현**</span><span class="sxs-lookup"><span data-stu-id="2d939-118">**Azure implementation**</span></span> |
> | --- | --- | --- |
> | <span data-ttu-id="2d939-119">**네트워킹**</span><span class="sxs-lookup"><span data-stu-id="2d939-119">**Networking**</span></span> |<span data-ttu-id="2d939-120">LAN/WAN</span><span class="sxs-lookup"><span data-stu-id="2d939-120">LAN/WAN</span></span>  |<span data-ttu-id="2d939-121">SDN(소프트웨어 방식 네트워킹)</span><span class="sxs-lookup"><span data-stu-id="2d939-121">SDN (software-defined networking)</span></span>|
> | <span data-ttu-id="2d939-122">**보안 그룹**</span><span class="sxs-lookup"><span data-stu-id="2d939-122">**Security group**</span></span> |<span data-ttu-id="2d939-123">IP/포트 제한 도구</span><span class="sxs-lookup"><span data-stu-id="2d939-123">IP/port restriction tools</span></span> |[<span data-ttu-id="2d939-124">NSG(네트워크 보안 그룹)</span><span class="sxs-lookup"><span data-stu-id="2d939-124">Network Security Group (NSG)</span></span>](https://azure.microsoft.com/blog/network-security-groups) |
> | <span data-ttu-id="2d939-125">**복원력**</span><span class="sxs-lookup"><span data-stu-id="2d939-125">**Resilience**</span></span> |<span data-ttu-id="2d939-126">MTBF(평균 고장 간격)</span><span class="sxs-lookup"><span data-stu-id="2d939-126">MTBF (mean time between failures)</span></span> |<span data-ttu-id="2d939-127">MTTR (그리니치 표준시 toorecovery)</span><span class="sxs-lookup"><span data-stu-id="2d939-127">MTTR (mean time toorecovery)</span></span>|
> | <span data-ttu-id="2d939-128">**계획된 유지 보수**</span><span class="sxs-lookup"><span data-stu-id="2d939-128">**Planned maintenance**</span></span> |<span data-ttu-id="2d939-129">패치/업그레이드</span><span class="sxs-lookup"><span data-stu-id="2d939-129">Patching/upgrades</span></span>|<span data-ttu-id="2d939-130">[가용성 집합](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines)(Azure에서 관리되는 패치/업그레이드)</span><span class="sxs-lookup"><span data-stu-id="2d939-130">[Availability sets](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines) (patching/upgrades managed by Azure)</span></span> |
> | <span data-ttu-id="2d939-131">**리소스**</span><span class="sxs-lookup"><span data-stu-id="2d939-131">**Resource**</span></span> |<span data-ttu-id="2d939-132">전용</span><span class="sxs-lookup"><span data-stu-id="2d939-132">Dedicated</span></span>  |<span data-ttu-id="2d939-133">다른 클라이언트와 공유</span><span class="sxs-lookup"><span data-stu-id="2d939-133">Shared with other clients</span></span>|
> | <span data-ttu-id="2d939-134">**지역**</span><span class="sxs-lookup"><span data-stu-id="2d939-134">**Regions**</span></span> |<span data-ttu-id="2d939-135">데이터 센터</span><span class="sxs-lookup"><span data-stu-id="2d939-135">Datacenters</span></span> |[<span data-ttu-id="2d939-136">지역 쌍</span><span class="sxs-lookup"><span data-stu-id="2d939-136">Region pairs</span></span>](https://docs.microsoft.com/azure/virtual-machines/windows/regions-and-availability)|
> | <span data-ttu-id="2d939-137">**저장소**</span><span class="sxs-lookup"><span data-stu-id="2d939-137">**Storage**</span></span> |<span data-ttu-id="2d939-138">SAN/실제 디스크</span><span class="sxs-lookup"><span data-stu-id="2d939-138">SAN/physical disks</span></span> |[<span data-ttu-id="2d939-139">Azure 관리 저장소</span><span class="sxs-lookup"><span data-stu-id="2d939-139">Azure-managed storage</span></span>](https://azure.microsoft.com/pricing/details/managed-disks/?v=17.23h)|
> | <span data-ttu-id="2d939-140">**규모**</span><span class="sxs-lookup"><span data-stu-id="2d939-140">**Scale**</span></span> |<span data-ttu-id="2d939-141">수직적 확장</span><span class="sxs-lookup"><span data-stu-id="2d939-141">Vertical scale</span></span> |<span data-ttu-id="2d939-142">수평적 확장</span><span class="sxs-lookup"><span data-stu-id="2d939-142">Horizontal scale</span></span>|


### <a name="requirements"></a><span data-ttu-id="2d939-143">요구 사항</span><span class="sxs-lookup"><span data-stu-id="2d939-143">Requirements</span></span>

- <span data-ttu-id="2d939-144">Hello 데이터베이스 크기 및 증가 속도 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-144">Determine hello database size and growth rate.</span></span>
- <span data-ttu-id="2d939-145">Oracle AWR 보고서 또는 다른 네트워크 모니터링 도구에 따라 예측할 수 hello IOPS 요구를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-145">Determine hello IOPS requirements, which you can estimate based on Oracle AWR reports or other network monitoring tools.</span></span>

## <a name="configuration-options"></a><span data-ttu-id="2d939-146">구성 옵션</span><span class="sxs-lookup"><span data-stu-id="2d939-146">Configuration options</span></span>

<span data-ttu-id="2d939-147">네 가지 잠재적인 영역은 Azure 환경에서 tooimprove 성능을 튜닝할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-147">There are four potential areas that you can tune tooimprove performance in an Azure environment:</span></span>

- <span data-ttu-id="2d939-148">가상 컴퓨터 크기</span><span class="sxs-lookup"><span data-stu-id="2d939-148">Virtual machine size</span></span>
- <span data-ttu-id="2d939-149">네트워크 처리량</span><span class="sxs-lookup"><span data-stu-id="2d939-149">Network throughput</span></span>
- <span data-ttu-id="2d939-150">디스크 형식 및 구성</span><span class="sxs-lookup"><span data-stu-id="2d939-150">Disk types and configurations</span></span>
- <span data-ttu-id="2d939-151">디스크 캐시 설정</span><span class="sxs-lookup"><span data-stu-id="2d939-151">Disk cache settings</span></span>

### <a name="generate-an-awr-report"></a><span data-ttu-id="2d939-152">AWR 보고서 생성</span><span class="sxs-lookup"><span data-stu-id="2d939-152">Generate an AWR report</span></span>

<span data-ttu-id="2d939-153">Oracle 데이터베이스를 기존 toomigrate tooAzure 계획 하는 경우 몇 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-153">If you have an existing an Oracle database and are planning toomigrate tooAzure, you have several options.</span></span> <span data-ttu-id="2d939-154">Hello Oracle AWR 보고서 tooget hello 메트릭 (IOPS, Mbps, GiBs, 및 등)를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-154">You can run hello Oracle AWR report tooget hello metrics (IOPS, Mbps, GiBs, and so on).</span></span> <span data-ttu-id="2d939-155">Hello 수집한 hello 메트릭을 기준으로 VM을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-155">Then choose hello VM based on hello metrics that you collected.</span></span> <span data-ttu-id="2d939-156">또는 인프라 팀 tooget 유사한 정보를 문의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-156">Or you can contact your infrastructure team tooget similar information.</span></span>

<span data-ttu-id="2d939-157">일반 및 최대 워크로드 모두에서 AWR 보고서를 실행하여 비교하는 것이 좋을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-157">You might consider running your AWR report during both regular and peak workloads, so you can compare.</span></span> <span data-ttu-id="2d939-158">이러한 보고서에 따라, 크기를 Vm hello 평균 작업 또는 hello 최대 작업 부하에 따라 hello.</span><span class="sxs-lookup"><span data-stu-id="2d939-158">Based on these reports, you can size hello VMs based on either hello average workload or hello maximum workload.</span></span>

<span data-ttu-id="2d939-159">다음은 방법의 예로 toogenerate AWR 보고서:</span><span class="sxs-lookup"><span data-stu-id="2d939-159">Following is an example of how toogenerate an AWR report:</span></span>

```bash
$ sqlplus / as sysdba
SQL> EXEC DBMS_WORKLOAD_REPOSITORY.CREATE_SNAPSHOT;
SQL> @?/rdbms/admin/awrrpt.sql
```

### <a name="key-metrics"></a><span data-ttu-id="2d939-160">주요 메트릭</span><span class="sxs-lookup"><span data-stu-id="2d939-160">Key metrics</span></span>

<span data-ttu-id="2d939-161">다음은 hello AWR 보고서에서에서 얻을 수 있는 hello 메트릭:</span><span class="sxs-lookup"><span data-stu-id="2d939-161">Following are hello metrics that you can obtain from hello AWR report:</span></span>

- <span data-ttu-id="2d939-162">총 코어 수</span><span class="sxs-lookup"><span data-stu-id="2d939-162">Total number of cores</span></span>
- <span data-ttu-id="2d939-163">CPU 클럭 속도</span><span class="sxs-lookup"><span data-stu-id="2d939-163">CPU clock speed</span></span>
- <span data-ttu-id="2d939-164">전체 메모리(GB)</span><span class="sxs-lookup"><span data-stu-id="2d939-164">Total memory in GB</span></span>
- <span data-ttu-id="2d939-165">CPU 사용률</span><span class="sxs-lookup"><span data-stu-id="2d939-165">CPU utilization</span></span>
- <span data-ttu-id="2d939-166">최대 데이터 전송 속도</span><span class="sxs-lookup"><span data-stu-id="2d939-166">Peak data transfer rate</span></span>
- <span data-ttu-id="2d939-167">I/O 변경률(읽기/쓰기)</span><span class="sxs-lookup"><span data-stu-id="2d939-167">Rate of I/O changes (read/write)</span></span>
- <span data-ttu-id="2d939-168">다시 실행 로그 속도(MBPs)</span><span class="sxs-lookup"><span data-stu-id="2d939-168">Redo log rate (MBPs)</span></span>
- <span data-ttu-id="2d939-169">네트워크 처리량</span><span class="sxs-lookup"><span data-stu-id="2d939-169">Network throughput</span></span>
- <span data-ttu-id="2d939-170">네트워크 대기 시간 비율(낮음/높음)</span><span class="sxs-lookup"><span data-stu-id="2d939-170">Network latency rate (low/high)</span></span>
- <span data-ttu-id="2d939-171">데이터베이스 크기(GB)</span><span class="sxs-lookup"><span data-stu-id="2d939-171">Database size in GB</span></span>
- <span data-ttu-id="2d939-172">SQL을 통해 받은 바이트 *에서 Net / tooclient</span><span class="sxs-lookup"><span data-stu-id="2d939-172">Bytes received via SQL*Net from/tooclient</span></span>

### <a name="virtual-machine-size"></a><span data-ttu-id="2d939-173">가상 컴퓨터 크기</span><span class="sxs-lookup"><span data-stu-id="2d939-173">Virtual machine size</span></span>

#### <a name="1-estimate-vm-size-based-on-cpu-memory-and-io-usage-from-hello-awr-report"></a><span data-ttu-id="2d939-174">1. AWR 보고서 hello에서 CPU, 메모리 및 I/O 사용량에 따라 VM 크기 예측</span><span class="sxs-lookup"><span data-stu-id="2d939-174">1. Estimate VM size based on CPU, memory, and I/O usage from hello AWR report</span></span>

<span data-ttu-id="2d939-175">살펴볼 수 있습니다는 hello 상위 5 개 전경 시간이 지정 된 이벤트를 나타내는 hello 시스템 병목 현상이 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-175">One thing you might look at is hello top five timed foreground events that indicate where hello system bottlenecks are.</span></span>

<span data-ttu-id="2d939-176">예를 들어 다음 다이어그램 hello, hello 위쪽에서 hello 로그 파일 동기화가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-176">For example, in hello following diagram, hello log file sync is at hello top.</span></span> <span data-ttu-id="2d939-177">Hello hello는 LGWR hello 로그 버퍼 toohello 다시 실행 로그 파일을 작성 하기 전에 필요 없는 대기 수를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-177">It indicates hello number of waits that are required before hello LGWR writes hello log buffer toohello redo log file.</span></span> <span data-ttu-id="2d939-178">이러한 결과는 더 효율적으로 수행되는 저장소 또는 디스크가 필요함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-178">These results indicate that better performing storage or disks are required.</span></span> <span data-ttu-id="2d939-179">또한 hello 다이어그램은 hello 수가 CPU (코어) 크기 및 메모리 양을 hello 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-179">In addition, hello diagram also shows hello number of CPU (cores) and hello amount of memory.</span></span>

![Hello AWR 보고서 페이지의 스크린샷](./media/oracle-design/cpu_memory_info.png)

<span data-ttu-id="2d939-181">hello 다음 그림에 대 한 읽기 및 쓰기의 총 I/O hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-181">hello following diagram shows hello total I/O of read and write.</span></span> <span data-ttu-id="2d939-182">읽을 59 GB와 247.3 GB hello 보고서의 hello 시간 중에 기록 했습니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-182">There were 59 GB read and 247.3 GB written during hello time of hello report.</span></span>

![Hello AWR 보고서 페이지의 스크린샷](./media/oracle-design/io_info.png)

#### <a name="2-choose-a-vm"></a><span data-ttu-id="2d939-184">2. VM 선택</span><span class="sxs-lookup"><span data-stu-id="2d939-184">2. Choose a VM</span></span>

<span data-ttu-id="2d939-185">Hello AWR 보고서에서에서 수집 하는 hello 정보에 따라 hello 다음 단계는 요구 사항을 충족 하는 비슷한 크기의 VM toochoose입니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-185">Based on hello information that you collected from hello AWR report, hello next step is toochoose a VM of a similar size that meets your requirements.</span></span> <span data-ttu-id="2d939-186">Hello 문서에서 사용 가능한 Vm의 목록을 찾을 수 있습니다 [메모리 액세스에 최적화](https://docs.microsoft.com/azure/virtual-machinFine tune es/virtual-machines-windows-sizes-memory)합니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-186">You can find a list of available VMs in hello article [Memory optimized](https://docs.microsoft.com/azure/virtual-machinFine tune es/virtual-machines-windows-sizes-memory).</span></span>

#### <a name="3-fine-tune-hello-vm-sizing-with-a-similar-vm-series-based-on-hello-acu"></a><span data-ttu-id="2d939-187">3. Hello ACU에 따라 유사한 VM 시리즈와 hello VM 크기를 미세 조정</span><span class="sxs-lookup"><span data-stu-id="2d939-187">3. Fine-tune hello VM sizing with a similar VM series based on hello ACU</span></span>

<span data-ttu-id="2d939-188">Hello VM을 선택한 후에 주의 기울여야 toohello ACU hello VM에 대 한 지불 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-188">After you've chosen hello VM, pay attention toohello ACU for hello VM.</span></span> <span data-ttu-id="2d939-189">Hello 요구 사항에 가장 잘 맞는 ACU 값에 따라 다른 VM을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-189">You might choose a different VM based on hello ACU value that better suits your requirements.</span></span> <span data-ttu-id="2d939-190">자세한 내용은 [ACU(Azure Compute 단위)](https://docs.microsoft.com/azure/virtual-machines/windows/acu)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d939-190">For more information, see [Azure compute unit](https://docs.microsoft.com/azure/virtual-machines/windows/acu).</span></span>

![Hello ACU 단위 페이지의 스크린샷](./media/oracle-design/acu_units.png)

### <a name="network-throughput"></a><span data-ttu-id="2d939-192">네트워크 처리량</span><span class="sxs-lookup"><span data-stu-id="2d939-192">Network throughput</span></span>

<span data-ttu-id="2d939-193">다음 다이어그램 hello 처리량 및 iops 수 간에 hello 관계를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-193">hello following diagram shows hello relation between throughput and IOPS:</span></span>

![처리량 스크린샷](./media/oracle-design/throughput.png)

<span data-ttu-id="2d939-195">hello 총 네트워크 처리량 hello 다음 정보에 따라 예상 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-195">hello total network throughput is estimated based on hello following information:</span></span>
- <span data-ttu-id="2d939-196">SQL*Net 트래픽</span><span class="sxs-lookup"><span data-stu-id="2d939-196">SQL*Net traffic</span></span>
- <span data-ttu-id="2d939-197">MBps x 서버 수(Oracle Data Guard와 같은 아웃바운드 스트림)</span><span class="sxs-lookup"><span data-stu-id="2d939-197">MBps x number of servers (outbound stream such as Oracle Data Guard)</span></span>
- <span data-ttu-id="2d939-198">응용 프로그램 복제와 같은 다른 요소</span><span class="sxs-lookup"><span data-stu-id="2d939-198">Other factors, such as application replication</span></span>

![스크린샷 hello SQL * Net 처리량](./media/oracle-design/sqlnet_info.png)

<span data-ttu-id="2d939-200">네트워크 대역폭 요구 사항에 따라는에서 toochoose에 대 한 다양 한 게이트웨이 유형이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-200">Based on your network bandwidth requirements, there are various gateway types for you toochoose from.</span></span> <span data-ttu-id="2d939-201">여기에는 기본, VpnGw 및 Azure ExpressRoute가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-201">These include basic, VpnGw, and Azure ExpressRoute.</span></span> <span data-ttu-id="2d939-202">자세한 내용은 참조 hello [VPN 게이트웨이 가격 책정 페이지](https://azure.microsoft.com/en-us/pricing/details/vpn-gateway/?v=17.23h)합니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-202">For more information, see hello [VPN gateway pricing page](https://azure.microsoft.com/en-us/pricing/details/vpn-gateway/?v=17.23h).</span></span>

<span data-ttu-id="2d939-203">**권장 사항**</span><span class="sxs-lookup"><span data-stu-id="2d939-203">**Recommendations**</span></span>

- <span data-ttu-id="2d939-204">네트워크 대기 시간이 더 높은 비교 tooan 온-프레미스 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-204">Network latency is higher compared tooan on-premises deployment.</span></span> <span data-ttu-id="2d939-205">네트워크 왕복 수를 줄이면 성능이 크게 향상될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-205">Reducing network round trips can greatly improve performance.</span></span>
- <span data-ttu-id="2d939-206">tooreduce 왕복 통합 또는 응용 프로그램을 높은 트랜잭션 "수 다 스러운" 앱 hello에 동일한 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="2d939-206">tooreduce round-trips, consolidate applications that have high transactions or “chatty” apps on hello same virtual machine.</span></span>

### <a name="disk-types-and-configurations"></a><span data-ttu-id="2d939-207">디스크 형식 및 구성</span><span class="sxs-lookup"><span data-stu-id="2d939-207">Disk types and configurations</span></span>

- <span data-ttu-id="2d939-208">*기본 OS 디스크*: 이러한 디스크 유형은 영구 데이터 및 캐싱을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-208">*Default OS disks*: These disk types offer persistent data and caching.</span></span> <span data-ttu-id="2d939-209">시작 시 OS 액세스에 최적화되며, 트랜잭션 또는 데이터 웨어하우스(분석) 워크로드용으로는 설계되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-209">They are optimized for OS access at startup, and aren't designed for either transactional or data warehouse (analytical) workloads.</span></span>

- <span data-ttu-id="2d939-210">*디스크 관리 되지 않는*: tooyour VM 디스크를 해당 하는 hello 가상 하드 디스크 (VHD) 파일을 저장 하는 hello 저장소 계정의 이러한 디스크 형식으로 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-210">*Unmanaged disks*: With these disk types, you manage hello storage accounts that store hello virtual hard disk (VHD) files that correspond tooyour VM disks.</span></span> <span data-ttu-id="2d939-211">VHD 파일은 Azure Storage 계정에 페이지 Blob으로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-211">VHD files are stored as page blobs in Azure storage accounts.</span></span>

- <span data-ttu-id="2d939-212">*관리 디스크*: Azure가 VM 디스크를 사용 하는 hello 저장소 계정을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-212">*Managed disks*: Azure manages hello storage accounts that you use for your VM disks.</span></span> <span data-ttu-id="2d939-213">Hello 디스크 유형 (프리미엄 또는 표준)와 필요한 hello 디스크의 hello 크기를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-213">You specify hello disk type (premium or standard) and hello size of hello disk that you need.</span></span> <span data-ttu-id="2d939-214">Azure 만들고에서 hello 디스크를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-214">Azure creates and manages hello disk for you.</span></span>

- <span data-ttu-id="2d939-215">*프리미엄 저장소 디스크*: 이러한 디스크 유형은 프로덕션 워크로드에 가장 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-215">*Premium storage disks*: These disk types are best suited for production workloads.</span></span> <span data-ttu-id="2d939-216">프리미엄 저장소에서는 VM 디스크 일 수 있는 연결 toospecific 크기 시리즈 Vm DS, DSv2, GS 및 F 시리즈 Vm 등.</span><span class="sxs-lookup"><span data-stu-id="2d939-216">Premium storage supports VM disks that can be attached toospecific size-series VMs, such as DS, DSv2, GS, and F series VMs.</span></span> <span data-ttu-id="2d939-217">hello 프리미엄 디스크는 크기가 다양 하 고 32GB too4, 096 GB에서에서 범위의 디스크 중에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-217">hello premium disk comes with different sizes, and you can choose between disks ranging from 32 GB too4,096 GB.</span></span> <span data-ttu-id="2d939-218">디스크 크기마다 자체 성능 사양이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-218">Each disk size has its own performance specifications.</span></span> <span data-ttu-id="2d939-219">응용 프로그램 요구 사항에 따라 하나 이상의 디스크 tooyour VM을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-219">Depending on your application requirements, you can attach one or more disks tooyour VM.</span></span>

<span data-ttu-id="2d939-220">Hello hello 포털에서 새 관리 되는 디스크를 만들 때 선택할 수 있습니다 **계정 유형** 원하는 toouse hello 유형의 디스크에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-220">When you create a new managed disk from hello portal, you can choose hello **Account type** for hello type of disk you want toouse.</span></span> <span data-ttu-id="2d939-221">모든 사용 가능한 디스크 hello 드롭 다운 메뉴에 표시 된 염두에서에 둬야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-221">Keep in mind that not all available disks are shown in hello drop-down menu.</span></span> <span data-ttu-id="2d939-222">특정 VM 크기를 선택한 후만 hello 사용할 수 있는 프리미엄 저장소는 v M 크기를 기반으로 하는 Sku hello 메뉴에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-222">After you choose a particular VM size, hello menu shows only hello available premium storage SKUs that are based on that VM size.</span></span>

![Hello 관리 되는 디스크 페이지의 스크린샷](./media/oracle-design/premium_disk01.png)

<span data-ttu-id="2d939-224">자세한 내용은 [VM의 고성능 Premium Storage 및 관리 디스크](https://docs.microsoft.com/azure/storage/storage-premium-storage)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d939-224">For more information, see [High-performance Premium Storage and managed disks for VMs](https://docs.microsoft.com/azure/storage/storage-premium-storage).</span></span>

<span data-ttu-id="2d939-225">VM의 저장소를 구성한 후에 데이터베이스를 만들기 전에 tooload 테스트 hello 디스크를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-225">After you configure your storage on a VM, you might want tooload test hello disks before creating a database.</span></span> <span data-ttu-id="2d939-226">대상 대기 시간으로 처리량을 예상 알면 대기 시간 및 처리량이 모두를 기준으로 hello I/O 속도 수 hello Vm hello를 지원 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-226">Knowing hello I/O rate in terms of both latency and throughput can help you determine if hello VMs support hello expected throughput with latency targets.</span></span>

<span data-ttu-id="2d939-227">Oracle Orion, Sysbench 및 Fio와 같이 응용 프로그램 부하 테스트를 위한 여러 가지 도구가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-227">There are a number of tools for application load testing, such as Oracle Orion, Sysbench, and Fio.</span></span>

<span data-ttu-id="2d939-228">Oracle 데이터베이스를 배포한 후에 hello 부하 테스트를 다시 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-228">Run hello load test again after you've deployed an Oracle database.</span></span> <span data-ttu-id="2d939-229">일반와 최대 작업을 시작 하 고 사용자 환경의 초기 hello 결과 표시 hello 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-229">Start your regular and peak workloads, and hello results show you hello baseline of your environment.</span></span>

<span data-ttu-id="2d939-230">Hello 저장소 크기 보다는 hello IOPS 속도에 따라 더 중요 한 toosize hello 저장 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-230">It might be more important toosize hello storage based on hello IOPS rate rather than hello storage size.</span></span> <span data-ttu-id="2d939-231">예를 들어 hello IOPS는 5, 000 하지만 200GB 하면 필요한 경우 받게 될 수 있습니다 hello P30 클래스 프리미엄 디스크 저장소 200GB 이상의 함께 제공 하는 경우에 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-231">For example, if hello required IOPS is 5,000, but you only need 200 GB, you might still get hello P30 class premium disk even though it comes with more than 200 GB of storage.</span></span>

<span data-ttu-id="2d939-232">hello IOPS 속도 hello AWR 보고서에서에서 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-232">hello IOPS rate can be obtained from hello AWR report.</span></span> <span data-ttu-id="2d939-233">Hello 다시 실행 로그, 물리적 읽기 및 쓰기 속도 의해 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-233">It's determined by hello redo log, physical reads, and writes rate.</span></span>

![Hello AWR 보고서 페이지의 스크린샷](./media/oracle-design/awr_report.png)

<span data-ttu-id="2d939-235">예를 들어 hello redo 크기는 같은 too11.63 MBPs는 초당 12,200,000 바이트입니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-235">For example, hello redo size is 12,200,000 bytes per second, which is equal too11.63 MBPs.</span></span>
<span data-ttu-id="2d939-236">hello IOPS는 12,200,000 / 2,358 = 5,174 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-236">hello IOPS is 12,200,000 / 2,358 = 5,174.</span></span>

<span data-ttu-id="2d939-237">Hello I/O 요구 사항 명확히를 설정한 후 이러한 요구 사항에 가장 적합 한 toomeet 있는 드라이브의 조합을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-237">After you have a clear picture of hello I/O requirements, you can choose a combination of drives that are best suited toomeet those requirements.</span></span>

<span data-ttu-id="2d939-238">**권장 사항**</span><span class="sxs-lookup"><span data-stu-id="2d939-238">**Recommendations**</span></span>

- <span data-ttu-id="2d939-239">데이터 테이블 스페이스에 대 한 분산 hello I/O 작업이 디스크 수가 Oracle ASM 또는 관리 되는 저장소를 사용 하 여 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-239">For data tablespace, spread hello I/O workload across a number of disks by using managed storage or Oracle ASM.</span></span>
- <span data-ttu-id="2d939-240">Hello I/O 블록 크기 증가 읽기 또는 쓰기를 많이 사용 작업에 대 한 데이터 디스크를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-240">As hello I/O block size increases for read-intensive and write-intensive operations, add more data disks.</span></span>
- <span data-ttu-id="2d939-241">대형 순차 프로세스에 대 한 hello 블록 크기를 늘립니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-241">Increase hello block size for large sequential processes.</span></span>
- <span data-ttu-id="2d939-242">데이터 압축 tooreduce I/O를 사용 하 여 (에 대 한 데이터 및 인덱스).</span><span class="sxs-lookup"><span data-stu-id="2d939-242">Use data compression tooreduce I/O (for both data and indexes).</span></span>
- <span data-ttu-id="2d939-243">개별 데이터 디스크에서 다시 실행 로그, 시스템, 임시 디스크를 분리하고 TS를 실행 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-243">Separate redo logs, system, and temps, and undo TS on separate data disks.</span></span>
- <span data-ttu-id="2d939-244">기본 OS 디스크(/dev/sda)에 응용 프로그램 파일을 배치하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-244">Don't put any application files on default OS disks (/dev/sda).</span></span> <span data-ttu-id="2d939-245">이러한 디스크는 빠른 VM 부팅 시간에 맞게 최적화되지 않으며, 응용 프로그램에 좋은 성능을 제공하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-245">These disks aren't optimized for fast VM boot times, and they might not provide good performance for your application.</span></span>

### <a name="disk-cache-settings"></a><span data-ttu-id="2d939-246">디스크 캐시 설정</span><span class="sxs-lookup"><span data-stu-id="2d939-246">Disk cache settings</span></span>

<span data-ttu-id="2d939-247">호스트 캐싱에는 세 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-247">There are three options for host caching:</span></span>

- <span data-ttu-id="2d939-248">*읽기 전용*: 모든 요청이 이후 읽기를 위해 캐시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-248">*Read-only*: All requests are cached for future reads.</span></span> <span data-ttu-id="2d939-249">모든 쓰기 유지 되는 직접 tooAzure Blob 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-249">All writes are persisted directly tooAzure Blob storage.</span></span>

- <span data-ttu-id="2d939-250">*읽기-쓰기*: "미리 읽기" 알고리즘입니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-250">*Read-write*: This is a “read-ahead” algorithm.</span></span> <span data-ttu-id="2d939-251">hello를 읽고 쓰기 이후 읽기에 대해 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-251">hello reads and writes are cached for future reads.</span></span> <span data-ttu-id="2d939-252">비-통한 쓰기 쓰기는 먼저 toohello 로컬 캐시를 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-252">Non-write-through writes are persisted toohello local cache first.</span></span> <span data-ttu-id="2d939-253">SQL Server에 대 한 쓰기 쓰기 사용 하기 때문에 지속형된 tooAzure 저장소는입니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-253">For SQL Server, writes are persisted tooAzure Storage because it uses write-through.</span></span> <span data-ttu-id="2d939-254">또한 밝은 작업에 대 한 hello 가장 낮은 디스크 대기 시간을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-254">It also provides hello lowest disk latency for light workloads.</span></span>

- <span data-ttu-id="2d939-255">*None* (사용 안 함):이 옵션을 사용 하 여 hello 캐시를 무시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-255">*None* (disabled): By using this option, you can bypass hello cache.</span></span> <span data-ttu-id="2d939-256">모든 hello 데이터 전송된 toodisk 되어 tooAzure 저장소를 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-256">All hello data is transferred toodisk and persisted tooAzure Storage.</span></span> <span data-ttu-id="2d939-257">I/O 집약적인 작업을 위해 높은 I/O 속도 hello를 사용 하는 메서드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-257">This method gives you hello highest I/O rate for I/O intensive workloads.</span></span> <span data-ttu-id="2d939-258">또한 해야 tootake "트랜잭션 비용"를 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-258">You also need tootake “transaction cost” into consideration.</span></span>

<span data-ttu-id="2d939-259">**권장 사항**</span><span class="sxs-lookup"><span data-stu-id="2d939-259">**Recommendations**</span></span>

<span data-ttu-id="2d939-260">toomaximize hello 처리량 권장으로 시작 하는 **None** 캐시 호스트에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-260">toomaximize hello throughput, we recommend that you  start with **None** for host caching.</span></span> <span data-ttu-id="2d939-261">프리미엄 저장소에 대 한 염두 hello로 hello 파일 시스템을 탑재 하면 장벽을"hello"를 해제 해야 **ReadOnly** 또는 **None** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-261">For Premium Storage, keep in mind that you must disable hello "barriers" when you mount hello file system with hello **ReadOnly** or **None** options.</span></span> <span data-ttu-id="2d939-262">Hello UUID toohello 디스크와 hello /etc/fstab 파일을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-262">Update hello /etc/fstab file with hello UUID toohello disks.</span></span>

<span data-ttu-id="2d939-263">자세한 내용은 [Linux VM용 Premium Storage](https://docs.microsoft.com/azure/storage/storage-premium-storage#premium-storage-for-linux-vms)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d939-263">For more information, see [Premium Storage for Linux VMs](https://docs.microsoft.com/azure/storage/storage-premium-storage#premium-storage-for-linux-vms).</span></span>

![Hello 관리 되는 디스크 페이지의 스크린샷](./media/oracle-design/premium_disk02.png)

- <span data-ttu-id="2d939-265">OS 디스크의 경우 기본 **읽기/쓰기** 캐싱을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-265">For OS disks, use default **Read/Write** caching.</span></span>
- <span data-ttu-id="2d939-266">시스템, 임시 및 실행 취소 디스크의 경우 캐싱에 **없음**을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-266">For SYSTEM, TEMP, and UNDO use **None** for caching.</span></span>
- <span data-ttu-id="2d939-267">데이터 디스크의 경우 캐싱에 **없음**을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-267">For DATA, use **None** for caching.</span></span> <span data-ttu-id="2d939-268">그러나 데이터베이스가 읽기 전용이거나 읽기 집약적인 경우 **읽기 전용** 캐싱을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-268">But if your database is read-only or read-intensive, use **Read-only** caching.</span></span>

<span data-ttu-id="2d939-269">저장 된 데이터 디스크 설정은 운영 체제 수준 hello에 hello 드라이브를 마운트 해제 하 고 변경 하는 hello를 변경한 후 다시 탑재 하지 않으면 hello 호스트 캐시 설정을 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-269">After your data disk setting is saved, you can't change hello host cache setting unless you unmount hello drive at hello OS level and then remount it after you've made hello change.</span></span>


## <a name="security"></a><span data-ttu-id="2d939-270">보안</span><span class="sxs-lookup"><span data-stu-id="2d939-270">Security</span></span>

<span data-ttu-id="2d939-271">설정 및 Azure 환경을 구성 해야, hello 다음 단계는 toosecure 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-271">After you have set up and configured your Azure environment, hello next step is toosecure your network.</span></span> <span data-ttu-id="2d939-272">몇 가지 권장 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-272">Here are some recommendations:</span></span>

- <span data-ttu-id="2d939-273">*NSG 정책*: NSG는 서브넷 또는 NIC에서 정의될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-273">*NSG policy*: NSG can be defined by a subnet or NIC.</span></span> <span data-ttu-id="2d939-274">것 hello 서브넷 수준 보안 및 응용 프로그램 방화벽 등을 위한 강제로 라우팅에 모두에서 간단한 toocontrol 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-274">It's simpler toocontrol access at hello subnet level both for security and force routing for things like application firewalls.</span></span>

- <span data-ttu-id="2d939-275">*Jumpbox*: 보다 안전한 액세스를 위해 관리자가 연결 하지 않도록 직접 toohello 응용 프로그램 서비스 또는 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-275">*Jumpbox*: For more secure access, administrators should not directly connect toohello application service or database.</span></span> <span data-ttu-id="2d939-276">jumpbox hello 관리자 컴퓨터와 Azure 리소스 간의 미디어로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-276">A jumpbox is used as a media between hello administrator machine and Azure resources.</span></span>
<span data-ttu-id="2d939-277">![Hello Jumpbox 토폴로지 페이지의 스크린샷](./media/oracle-design/jumpbox.png)</span><span class="sxs-lookup"><span data-stu-id="2d939-277">![Screenshot of hello Jumpbox topology page](./media/oracle-design/jumpbox.png)</span></span>

    <span data-ttu-id="2d939-278">hello 관리자 컴퓨터만 toohello jumpbox IP 제한 된 액세스를 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-278">hello administrator machine should offer IP-restricted access toohello jumpbox only.</span></span> <span data-ttu-id="2d939-279">hello jumpbox 액세스 toohello 응용 프로그램 및 데이터베이스가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-279">hello jumpbox should have access toohello application and database.</span></span>

- <span data-ttu-id="2d939-280">*개인 네트워크* (서브넷): hello 응용 프로그램 서비스 및 데이터베이스에 있는지 별도 서브넷을 더 세부적으로 제어할 NSG 정책에 의해 설정 될 수 있도록 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="2d939-280">*Private network* (subnets): We recommend that you have hello application service and database on separate subnets, so better control can be set by NSG policy.</span></span>


## <a name="additional-reading"></a><span data-ttu-id="2d939-281">추가 참조 자료</span><span class="sxs-lookup"><span data-stu-id="2d939-281">Additional reading</span></span>

- [<span data-ttu-id="2d939-282">Oracle ASM 구성</span><span class="sxs-lookup"><span data-stu-id="2d939-282">Configure Oracle ASM</span></span>](configure-oracle-asm.md)
- [<span data-ttu-id="2d939-283">Oracle Data Guard 구성</span><span class="sxs-lookup"><span data-stu-id="2d939-283">Configure Oracle Data Guard</span></span>](configure-oracle-dataguard.md)
- [<span data-ttu-id="2d939-284">Oracle Golden Gate 구성</span><span class="sxs-lookup"><span data-stu-id="2d939-284">Configure Oracle Golden Gate</span></span>](configure-oracle-golden-gate.md)
- [<span data-ttu-id="2d939-285">Oracle 백업 및 복구</span><span class="sxs-lookup"><span data-stu-id="2d939-285">Oracle backup and recovery</span></span>](oracle-backup-recovery.md)

## <a name="next-steps"></a><span data-ttu-id="2d939-286">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2d939-286">Next steps</span></span>

- [<span data-ttu-id="2d939-287">자습서: 고가용성 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="2d939-287">Tutorial: Create highly available VMs</span></span>](../../linux/create-cli-complete.md)
- [<span data-ttu-id="2d939-288">VM 배포 Azure CLI 샘플 탐색</span><span class="sxs-lookup"><span data-stu-id="2d939-288">Explore VM deployment Azure CLI samples</span></span>](../../linux/cli-samples.md)
