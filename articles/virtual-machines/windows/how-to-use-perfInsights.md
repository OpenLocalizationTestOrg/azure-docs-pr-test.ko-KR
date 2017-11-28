---
title: "Microsoft Azure에서 PerfInsights aaaHow toouse | Microsoft Docs"
description: "학습 방법을 toouse PerfInsights tootroubleshoot Windows VM 성능 문제."
services: virtual-machines-windows'
documentationcenter: 
author: genlin
manager: cshepard
editor: na
tags: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: genli
ms.openlocfilehash: f23ff7708c0c63bd02674b1bdc07753e8a89d9be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-perfinsights"></a><span data-ttu-id="2af03-103">어떻게 toouse PerfInsights</span><span class="sxs-lookup"><span data-stu-id="2af03-103">How toouse PerfInsights</span></span> 

<span data-ttu-id="2af03-104">[PerfInsights](http://aka.ms/perfinsightsdownload) 유용한 진단 정보 수집 하 고, I/O 스트레스 부하를 실행 한 다음 분석 보고서 toohelp 제공 하는 자동화 된 스크립트는 Microsoft Azure에서 Windows VM 성능 문제를 해결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-104">[PerfInsights](http://aka.ms/perfinsightsdownload) is an automated script that collects useful diagnostic information, runs I/O stress loads, and provides an analysis report toohelp troubleshoot Windows VM performance problems in Microsoft Azure.</span></span> 

<span data-ttu-id="2af03-105">VM 성능 문제로 Microsoft 지원 티켓을 열기 전에 이 스크립트를 실행하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-105">We recommend that you run this script before you open a Support ticket with Microsoft for VM performance issues.</span></span>

## <a name="supported-troubleshooting-scenarios"></a><span data-ttu-id="2af03-106">지원되는 문제 해결 시나리오</span><span class="sxs-lookup"><span data-stu-id="2af03-106">Supported troubleshooting scenarios</span></span>

<span data-ttu-id="2af03-107">PerfInsights에서는 고유한 시나리오로 그룹화된 여러 종류의 정보를 수집하고 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-107">PerfInsights can collect and analyze several kinds of information that are grouped into unique scenarios.</span></span>

### <a name="collect-disk-configuration"></a><span data-ttu-id="2af03-108">디스크 구성 수집</span><span class="sxs-lookup"><span data-stu-id="2af03-108">Collect disk configuration</span></span> 

<span data-ttu-id="2af03-109">이 시나리오에서는 hello 디스크 구성 및 hello 다음 항목을 포함 하 여 다른 중요 한 정보를 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-109">This scenario collects hello disk configuration and other important information, including hello following items:</span></span>

-   <span data-ttu-id="2af03-110">이벤트 로그</span><span class="sxs-lookup"><span data-stu-id="2af03-110">Event logs</span></span>

-   <span data-ttu-id="2af03-111">모든 들어오는 연결과 나가는 연결에 대한 네트워크 상태</span><span class="sxs-lookup"><span data-stu-id="2af03-111">Network status for all incoming and outgoing connections</span></span>

-   <span data-ttu-id="2af03-112">네트워크 및 방화벽 구성 설정</span><span class="sxs-lookup"><span data-stu-id="2af03-112">Network and firewall configuration settings</span></span>

-   <span data-ttu-id="2af03-113">Hello 시스템에서 현재 실행 중인 모든 응용 프로그램에 대 한 작업 목록</span><span class="sxs-lookup"><span data-stu-id="2af03-113">Task list for all applications that are currently running on hello system</span></span>

-   <span data-ttu-id="2af03-114">Msinfo32 hello 가상 컴퓨터 (VM)에 의해 생성 되는 정보 파일</span><span class="sxs-lookup"><span data-stu-id="2af03-114">Information file created by msinfo32 for hello virtual machine (VM)</span></span>

-   <span data-ttu-id="2af03-115">Microsoft SQL Server 데이터베이스 구성 설정 (SQL Server를 실행 하는 서버 hello VM 식별) 하는 경우</span><span class="sxs-lookup"><span data-stu-id="2af03-115">Microsoft SQL Server database configuration settings (if hello VM is identified as a server that is running SQL Server)</span></span>

-   <span data-ttu-id="2af03-116">저장소 안정성 카운터</span><span class="sxs-lookup"><span data-stu-id="2af03-116">Storage reliability counters</span></span>

-   <span data-ttu-id="2af03-117">중요한 Windows 핫픽스</span><span class="sxs-lookup"><span data-stu-id="2af03-117">Important Windows hotfixes</span></span>

-   <span data-ttu-id="2af03-118">설치된 필터 드라이버</span><span class="sxs-lookup"><span data-stu-id="2af03-118">Installed filter drivers</span></span>

<span data-ttu-id="2af03-119">Hello 시스템에 영향을 하지 않아야 하는 정보의 수동 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-119">This is a passive collection of information that shouldn't affect hello system.</span></span> 

>[!Note]
><span data-ttu-id="2af03-120">이 시나리오는 각각 hello 다음 시나리오에 자동으로 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-120">This scenario is automatically included in each of hello following scenarios.</span></span>

### <a name="benchmarkstorage-performance-test"></a><span data-ttu-id="2af03-121">벤치마크/저장소 성능 테스트</span><span class="sxs-lookup"><span data-stu-id="2af03-121">Benchmark/Storage Performance Test</span></span>

<span data-ttu-id="2af03-122">이 시나리오 실행 hello [diskspd](https://github.com/Microsoft/diskspd) 모든 드라이브 연결 toohello VM에 대 한 테스트 (IOPS 및 MBPS) 벤치 마크입니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-122">This scenario runs hello [diskspd](https://github.com/Microsoft/diskspd) benchmark test (IOPS and MBPS) for all drives that are attached toohello VM.</span></span> 

> [!Note]
> <span data-ttu-id="2af03-123">이 시나리오는 hello 시스템에 영향을 줄 수와 실제 프로덕션 시스템에서 실행 하지 않는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-123">This scenario can affect hello system and shouldn’t be run on a live production system.</span></span> <span data-ttu-id="2af03-124">필요한 경우이 시나리오에서에서 실행 전용된 유지 관리 창 tooavoid 문제.</span><span class="sxs-lookup"><span data-stu-id="2af03-124">If necessary, run this scenario in a dedicated maintenance window tooavoid any problems.</span></span> <span data-ttu-id="2af03-125">추적 또는 벤치 마크 테스트 인해 발생 하는 워크플로가 증가할 VM의 hello 성능을 저하 될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-125">An increased workload that is caused by a trace or benchmark test could adversely affect hello performance of your VM.</span></span>
>

### <a name="general-vm-slow-analysis"></a><span data-ttu-id="2af03-126">일반 VM 저속 분석</span><span class="sxs-lookup"><span data-stu-id="2af03-126">General VM Slow analysis</span></span> 

<span data-ttu-id="2af03-127">이 시나리오를 실행 한 [성능 카운터](https://msdn.microsoft.com/library/windows/desktop/aa373083(v=vs.85).aspx) hello Generalcounters.txt 파일에 지정 하는 hello 카운터를 사용 하 여 추적 합니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-127">This scenario runs a [performance counter](https://msdn.microsoft.com/library/windows/desktop/aa373083(v=vs.85).aspx) trace by using hello counters that are specified in hello Generalcounters.txt file.</span></span> <span data-ttu-id="2af03-128">Hello VM으로 식별 되 면 SQL Server를 실행 하는 서버, 성능 카운터 추적 hello Sqlcounters.txt 파일에 있는 hello 카운터를 사용 하 여 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-128">If hello VM is identified as a server that is running SQL Server, it runs a performance counter trace by using hello counters that are found in hello Sqlcounters.txt file.</span></span> <span data-ttu-id="2af03-129">또한 성능 진단 데이터도 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-129">It also includes Performance Diagnostics data.</span></span>

### <a name="vm-slow-analysis-and-benchmark"></a><span data-ttu-id="2af03-130">VM 저속 분석 및 벤치마크</span><span class="sxs-lookup"><span data-stu-id="2af03-130">VM Slow analysis and benchmark</span></span>

<span data-ttu-id="2af03-131">이 시나리오에서는 [성능 카운터](https://msdn.microsoft.com/library/windows/desktop/aa373083(v=vs.85).aspx) 추적을 실행한 다음 [diskspd](https://github.com/Microsoft/diskspd) 벤치마크 테스트를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-131">This scenario runs a [performance counter](https://msdn.microsoft.com/library/windows/desktop/aa373083(v=vs.85).aspx) trace that is followed by a [diskspd](https://github.com/Microsoft/diskspd) benchmark test.</span></span> 

> [!Note]
> <span data-ttu-id="2af03-132">이 시나리오는 hello 시스템에 영향을 줄 수와 실제 프로덕션 시스템에서 실행 하지 않는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-132">This scenario can affect hello system and shouldn’t be run on a live production system.</span></span> <span data-ttu-id="2af03-133">필요한 경우이 시나리오에서에서 실행 전용된 유지 관리 창 tooavoid 문제.</span><span class="sxs-lookup"><span data-stu-id="2af03-133">If necessary, run this scenario in a dedicated maintenance window tooavoid any problems.</span></span> <span data-ttu-id="2af03-134">추적 또는 벤치 마크 테스트 인해 발생 하는 워크플로가 증가할 VM의 hello 성능을 저하 될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-134">An increased workload that is caused by a trace or benchmark test could adversely affect hello performance of your VM.</span></span>
>

### <a name="azure-files-analysis"></a><span data-ttu-id="2af03-135">Azure Files 분석</span><span class="sxs-lookup"><span data-stu-id="2af03-135">Azure Files analysis</span></span> 

<span data-ttu-id="2af03-136">이 시나리오에서는 네트워크 추적과 함께 특별한 성능 카운터 캡처를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-136">This scenario runs a special performance counter capture together with a network trace.</span></span> <span data-ttu-id="2af03-137">캡처 모든 hello "SMB 클라이언트 공유" 카운터를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-137">The capture includes all hello "SMB Client Shares" counters.</span></span> <span data-ttu-id="2af03-138">hello 다음은 몇 가지 주요 SMB 클라이언트 공유 성능 카운터 hello 캡처의 일부인입니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-138">hello following are some key SMB client share performance counters that are part of hello capture:</span></span>

| <span data-ttu-id="2af03-139">**형식**</span><span class="sxs-lookup"><span data-stu-id="2af03-139">**Type**</span></span>     | <span data-ttu-id="2af03-140">**SMB 클라이언트 공유 카운터**</span><span class="sxs-lookup"><span data-stu-id="2af03-140">**SMB client shares counter**</span></span> |
|--------------|-------------------------------|
| <span data-ttu-id="2af03-141">IOPS</span><span class="sxs-lookup"><span data-stu-id="2af03-141">IOPS</span></span>         | <span data-ttu-id="2af03-142">데이터 요청 수/초</span><span class="sxs-lookup"><span data-stu-id="2af03-142">Data Requests/sec</span></span>             |
|              | <span data-ttu-id="2af03-143">읽기 요청 수/초</span><span class="sxs-lookup"><span data-stu-id="2af03-143">Read Requests/sec</span></span>             |
|              | <span data-ttu-id="2af03-144">쓰기 요청 수/초</span><span class="sxs-lookup"><span data-stu-id="2af03-144">Write Requests/sec</span></span>            |
| <span data-ttu-id="2af03-145">대기 시간</span><span class="sxs-lookup"><span data-stu-id="2af03-145">Latency</span></span>      | <span data-ttu-id="2af03-146">Avg. 초/데이터 요청</span><span class="sxs-lookup"><span data-stu-id="2af03-146">Avg. sec/Data Request</span></span>         |
|              | <span data-ttu-id="2af03-147">평균 초/읽기</span><span class="sxs-lookup"><span data-stu-id="2af03-147">Avg. sec/Read</span></span>                 |
|              | <span data-ttu-id="2af03-148">평균 sec/Write</span><span class="sxs-lookup"><span data-stu-id="2af03-148">Avg. sec/Write</span></span>                |
| <span data-ttu-id="2af03-149">IO 크기</span><span class="sxs-lookup"><span data-stu-id="2af03-149">IO Size</span></span>      | <span data-ttu-id="2af03-150">평균 바이트 수/데이터 요청</span><span class="sxs-lookup"><span data-stu-id="2af03-150">Avg. Bytes/Data Request</span></span>       |
|              | <span data-ttu-id="2af03-151">평균 바이트 수/읽기</span><span class="sxs-lookup"><span data-stu-id="2af03-151">Avg. Bytes/Read</span></span>               |
|              | <span data-ttu-id="2af03-152">평균 바이트 수/쓰기</span><span class="sxs-lookup"><span data-stu-id="2af03-152">Avg. Bytes/Write</span></span>              |
| <span data-ttu-id="2af03-153">처리량</span><span class="sxs-lookup"><span data-stu-id="2af03-153">Throughput</span></span>   | <span data-ttu-id="2af03-154">데이터 바이트 수/쓰기</span><span class="sxs-lookup"><span data-stu-id="2af03-154">Data Bytes/sec</span></span>                |
|              | <span data-ttu-id="2af03-155">읽기 바이트 수/초</span><span class="sxs-lookup"><span data-stu-id="2af03-155">Read Bytes/sec</span></span>                |
|              | <span data-ttu-id="2af03-156">쓰기 바이트 수/초</span><span class="sxs-lookup"><span data-stu-id="2af03-156">Write Bytes/sec</span></span>               |
| <span data-ttu-id="2af03-157">큐 길이</span><span class="sxs-lookup"><span data-stu-id="2af03-157">Queue Length</span></span> | <span data-ttu-id="2af03-158">평균 읽기 큐 길이</span><span class="sxs-lookup"><span data-stu-id="2af03-158">Avg. Read Queue Length</span></span>        |
|              | <span data-ttu-id="2af03-159">평균 쓰기 큐 길이</span><span class="sxs-lookup"><span data-stu-id="2af03-159">Avg. Write Queue Length</span></span>       |
|              | <span data-ttu-id="2af03-160">평균 데이터 큐 길이</span><span class="sxs-lookup"><span data-stu-id="2af03-160">Avg. Data Queue Length</span></span>        |

### <a name="custom-configuration"></a><span data-ttu-id="2af03-161">사용자 지정 구성</span><span class="sxs-lookup"><span data-stu-id="2af03-161">Custom configuration</span></span> 

<span data-ttu-id="2af03-162">사용자 지정 구성을 실행하면 서로 다른 추적을 선택한 개수에 따라 모든 추적(성능 진단, 성능 카운터, xperf, 네트워크, storport)이 병렬로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-162">When you run a custom configuration, you are running all traces (performance diagnostics, performance counter, xperf, network, storport) in parallel, depending how many different traces are selected.</span></span> <span data-ttu-id="2af03-163">추적 완료 되 면 hello 도구 선택 되어 있으면 hello diskspd 벤치 마크를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-163">After tracing is completed, hello tool runs hello diskspd benchmark, if it is selected.</span></span> 

> [!Note]
> <span data-ttu-id="2af03-164">이 시나리오는 hello 시스템에 영향을 줄 수와 실제 프로덕션 시스템에서 실행 하지 않는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-164">This scenario can affect hello system and shouldn’t be run on a live production system.</span></span> <span data-ttu-id="2af03-165">필요한 경우이 시나리오에서에서 실행 전용된 유지 관리 창 tooavoid 문제.</span><span class="sxs-lookup"><span data-stu-id="2af03-165">If necessary, run this scenario in a dedicated maintenance window tooavoid any problems.</span></span> <span data-ttu-id="2af03-166">추적 또는 벤치 마크 테스트 인해 발생 하는 워크플로가 증가할 VM의 hello 성능을 저하 될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-166">An increased workload that is caused by a trace or benchmark test could adversely affect hello performance of your VM.</span></span>
>

## <a name="what-kind-of-information-is-collected-by-hello-script"></a><span data-ttu-id="2af03-167">Hello 스크립트에 의해 어떤 종류의 정보를 수집 하나요?</span><span class="sxs-lookup"><span data-stu-id="2af03-167">What kind of information is collected by hello script?</span></span>

<span data-ttu-id="2af03-168">Windows VM, 디스크 또는 저장소에 대 한 내용은 풀 구성, 성능 카운터, 로그 및 다양 한 추적에서 사용 하는 hello 성능 시나리오에 따라 수집 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-168">Information about Windows VM, disks or storage pools configuration, performance counters, logs and various traces are collected depending on hello performance scenario used:</span></span>

|<span data-ttu-id="2af03-169">수집되는 데이터</span><span class="sxs-lookup"><span data-stu-id="2af03-169">Data collected</span></span>                              |  |  | <span data-ttu-id="2af03-170">성능 시나리오</span><span class="sxs-lookup"><span data-stu-id="2af03-170">Performance Scenarios</span></span> |  |  | |
|----------------------------------|----------------------------|------------------------------------|--------------------------|--------------------------------|----------------------|----------------------|
|                              | <span data-ttu-id="2af03-171">디스크 구성 수집</span><span class="sxs-lookup"><span data-stu-id="2af03-171">Collect disk Configuration</span></span> | <span data-ttu-id="2af03-172">벤치마크/저장소 성능 테스트</span><span class="sxs-lookup"><span data-stu-id="2af03-172">Benchmark/Storage Performance test</span></span> | <span data-ttu-id="2af03-173">일반 VM 저속 분석</span><span class="sxs-lookup"><span data-stu-id="2af03-173">General VM Slow analysis</span></span> | <span data-ttu-id="2af03-174">VM 저속 분석 및 벤치마크</span><span class="sxs-lookup"><span data-stu-id="2af03-174">VM Slow analysis and benchmark</span></span> | <span data-ttu-id="2af03-175">Azure Files 분석</span><span class="sxs-lookup"><span data-stu-id="2af03-175">Azure Files analysis</span></span> | <span data-ttu-id="2af03-176">사용자 지정 구성</span><span class="sxs-lookup"><span data-stu-id="2af03-176">Custom configuration</span></span> |
| <span data-ttu-id="2af03-177">이벤트 로그의 정보</span><span class="sxs-lookup"><span data-stu-id="2af03-177">Information from Event logs</span></span>      | <span data-ttu-id="2af03-178">예</span><span class="sxs-lookup"><span data-stu-id="2af03-178">Yes</span></span>                        | <span data-ttu-id="2af03-179">예</span><span class="sxs-lookup"><span data-stu-id="2af03-179">Yes</span></span>                                | <span data-ttu-id="2af03-180">예</span><span class="sxs-lookup"><span data-stu-id="2af03-180">Yes</span></span>                      | <span data-ttu-id="2af03-181">예</span><span class="sxs-lookup"><span data-stu-id="2af03-181">Yes</span></span>                            | <span data-ttu-id="2af03-182">예</span><span class="sxs-lookup"><span data-stu-id="2af03-182">Yes</span></span>                  | <span data-ttu-id="2af03-183">예</span><span class="sxs-lookup"><span data-stu-id="2af03-183">Yes</span></span>                  |
| <span data-ttu-id="2af03-184">시스템 정보</span><span class="sxs-lookup"><span data-stu-id="2af03-184">System information</span></span>               | <span data-ttu-id="2af03-185">예</span><span class="sxs-lookup"><span data-stu-id="2af03-185">Yes</span></span>                        | <span data-ttu-id="2af03-186">예</span><span class="sxs-lookup"><span data-stu-id="2af03-186">Yes</span></span>                                | <span data-ttu-id="2af03-187">예</span><span class="sxs-lookup"><span data-stu-id="2af03-187">Yes</span></span>                      | <span data-ttu-id="2af03-188">예</span><span class="sxs-lookup"><span data-stu-id="2af03-188">Yes</span></span>                            | <span data-ttu-id="2af03-189">예</span><span class="sxs-lookup"><span data-stu-id="2af03-189">Yes</span></span>                  | <span data-ttu-id="2af03-190">예</span><span class="sxs-lookup"><span data-stu-id="2af03-190">Yes</span></span>                  |
| <span data-ttu-id="2af03-191">볼륨 매핑</span><span class="sxs-lookup"><span data-stu-id="2af03-191">Volume Map</span></span>                       | <span data-ttu-id="2af03-192">예</span><span class="sxs-lookup"><span data-stu-id="2af03-192">Yes</span></span>                        | <span data-ttu-id="2af03-193">예</span><span class="sxs-lookup"><span data-stu-id="2af03-193">Yes</span></span>                                | <span data-ttu-id="2af03-194">예</span><span class="sxs-lookup"><span data-stu-id="2af03-194">Yes</span></span>                      | <span data-ttu-id="2af03-195">예</span><span class="sxs-lookup"><span data-stu-id="2af03-195">Yes</span></span>                            | <span data-ttu-id="2af03-196">예</span><span class="sxs-lookup"><span data-stu-id="2af03-196">Yes</span></span>                  | <span data-ttu-id="2af03-197">예</span><span class="sxs-lookup"><span data-stu-id="2af03-197">Yes</span></span>                  |
| <span data-ttu-id="2af03-198">디스크 매핑</span><span class="sxs-lookup"><span data-stu-id="2af03-198">Disk Map</span></span>                         | <span data-ttu-id="2af03-199">예</span><span class="sxs-lookup"><span data-stu-id="2af03-199">Yes</span></span>                        | <span data-ttu-id="2af03-200">예</span><span class="sxs-lookup"><span data-stu-id="2af03-200">Yes</span></span>                                | <span data-ttu-id="2af03-201">예</span><span class="sxs-lookup"><span data-stu-id="2af03-201">Yes</span></span>                      | <span data-ttu-id="2af03-202">예</span><span class="sxs-lookup"><span data-stu-id="2af03-202">Yes</span></span>                            | <span data-ttu-id="2af03-203">예</span><span class="sxs-lookup"><span data-stu-id="2af03-203">Yes</span></span>                  | <span data-ttu-id="2af03-204">예</span><span class="sxs-lookup"><span data-stu-id="2af03-204">Yes</span></span>                  |
| <span data-ttu-id="2af03-205">실행 중인 작업</span><span class="sxs-lookup"><span data-stu-id="2af03-205">Running Tasks</span></span>                    | <span data-ttu-id="2af03-206">예</span><span class="sxs-lookup"><span data-stu-id="2af03-206">Yes</span></span>                        | <span data-ttu-id="2af03-207">예</span><span class="sxs-lookup"><span data-stu-id="2af03-207">Yes</span></span>                                | <span data-ttu-id="2af03-208">예</span><span class="sxs-lookup"><span data-stu-id="2af03-208">Yes</span></span>                      | <span data-ttu-id="2af03-209">예</span><span class="sxs-lookup"><span data-stu-id="2af03-209">Yes</span></span>                            | <span data-ttu-id="2af03-210">예</span><span class="sxs-lookup"><span data-stu-id="2af03-210">Yes</span></span>                  | <span data-ttu-id="2af03-211">예</span><span class="sxs-lookup"><span data-stu-id="2af03-211">Yes</span></span>                  |
| <span data-ttu-id="2af03-212">저장소 안정성 카운터</span><span class="sxs-lookup"><span data-stu-id="2af03-212">Storage Reliability Counters</span></span>     | <span data-ttu-id="2af03-213">예</span><span class="sxs-lookup"><span data-stu-id="2af03-213">Yes</span></span>                        | <span data-ttu-id="2af03-214">예</span><span class="sxs-lookup"><span data-stu-id="2af03-214">Yes</span></span>                                | <span data-ttu-id="2af03-215">예</span><span class="sxs-lookup"><span data-stu-id="2af03-215">Yes</span></span>                      | <span data-ttu-id="2af03-216">예</span><span class="sxs-lookup"><span data-stu-id="2af03-216">Yes</span></span>                            | <span data-ttu-id="2af03-217">예</span><span class="sxs-lookup"><span data-stu-id="2af03-217">Yes</span></span>                  | <span data-ttu-id="2af03-218">예</span><span class="sxs-lookup"><span data-stu-id="2af03-218">Yes</span></span>                  |
| <span data-ttu-id="2af03-219">저장소 정보</span><span class="sxs-lookup"><span data-stu-id="2af03-219">Storage information</span></span>              | <span data-ttu-id="2af03-220">예</span><span class="sxs-lookup"><span data-stu-id="2af03-220">Yes</span></span>                        | <span data-ttu-id="2af03-221">예</span><span class="sxs-lookup"><span data-stu-id="2af03-221">Yes</span></span>                                | <span data-ttu-id="2af03-222">예</span><span class="sxs-lookup"><span data-stu-id="2af03-222">Yes</span></span>                      | <span data-ttu-id="2af03-223">예</span><span class="sxs-lookup"><span data-stu-id="2af03-223">Yes</span></span>                            | <span data-ttu-id="2af03-224">예</span><span class="sxs-lookup"><span data-stu-id="2af03-224">Yes</span></span>                  | <span data-ttu-id="2af03-225">예</span><span class="sxs-lookup"><span data-stu-id="2af03-225">Yes</span></span>                  |
| <span data-ttu-id="2af03-226">Fsutil 출력</span><span class="sxs-lookup"><span data-stu-id="2af03-226">Fsutil output</span></span>                    | <span data-ttu-id="2af03-227">예</span><span class="sxs-lookup"><span data-stu-id="2af03-227">Yes</span></span>                        | <span data-ttu-id="2af03-228">예</span><span class="sxs-lookup"><span data-stu-id="2af03-228">Yes</span></span>                                | <span data-ttu-id="2af03-229">예</span><span class="sxs-lookup"><span data-stu-id="2af03-229">Yes</span></span>                      | <span data-ttu-id="2af03-230">예</span><span class="sxs-lookup"><span data-stu-id="2af03-230">Yes</span></span>                            | <span data-ttu-id="2af03-231">예</span><span class="sxs-lookup"><span data-stu-id="2af03-231">Yes</span></span>                  | <span data-ttu-id="2af03-232">예</span><span class="sxs-lookup"><span data-stu-id="2af03-232">Yes</span></span>                  |
| <span data-ttu-id="2af03-233">필터 드라이버 정보</span><span class="sxs-lookup"><span data-stu-id="2af03-233">Filter Driver info</span></span>               | <span data-ttu-id="2af03-234">예</span><span class="sxs-lookup"><span data-stu-id="2af03-234">Yes</span></span>                        | <span data-ttu-id="2af03-235">예</span><span class="sxs-lookup"><span data-stu-id="2af03-235">Yes</span></span>                                | <span data-ttu-id="2af03-236">예</span><span class="sxs-lookup"><span data-stu-id="2af03-236">Yes</span></span>                      | <span data-ttu-id="2af03-237">예</span><span class="sxs-lookup"><span data-stu-id="2af03-237">Yes</span></span>                            | <span data-ttu-id="2af03-238">예</span><span class="sxs-lookup"><span data-stu-id="2af03-238">Yes</span></span>                  | <span data-ttu-id="2af03-239">예</span><span class="sxs-lookup"><span data-stu-id="2af03-239">Yes</span></span>                  |
| <span data-ttu-id="2af03-240">Netstat 출력</span><span class="sxs-lookup"><span data-stu-id="2af03-240">Netstat output</span></span>                   | <span data-ttu-id="2af03-241">예</span><span class="sxs-lookup"><span data-stu-id="2af03-241">Yes</span></span>                        | <span data-ttu-id="2af03-242">예</span><span class="sxs-lookup"><span data-stu-id="2af03-242">Yes</span></span>                                | <span data-ttu-id="2af03-243">예</span><span class="sxs-lookup"><span data-stu-id="2af03-243">Yes</span></span>                      | <span data-ttu-id="2af03-244">예</span><span class="sxs-lookup"><span data-stu-id="2af03-244">Yes</span></span>                            | <span data-ttu-id="2af03-245">예</span><span class="sxs-lookup"><span data-stu-id="2af03-245">Yes</span></span>                  | <span data-ttu-id="2af03-246">예</span><span class="sxs-lookup"><span data-stu-id="2af03-246">Yes</span></span>                  |
| <span data-ttu-id="2af03-247">네트워크 구성</span><span class="sxs-lookup"><span data-stu-id="2af03-247">Network configuration</span></span>            | <span data-ttu-id="2af03-248">예</span><span class="sxs-lookup"><span data-stu-id="2af03-248">Yes</span></span>                        | <span data-ttu-id="2af03-249">예</span><span class="sxs-lookup"><span data-stu-id="2af03-249">Yes</span></span>                                | <span data-ttu-id="2af03-250">예</span><span class="sxs-lookup"><span data-stu-id="2af03-250">Yes</span></span>                      | <span data-ttu-id="2af03-251">예</span><span class="sxs-lookup"><span data-stu-id="2af03-251">Yes</span></span>                            | <span data-ttu-id="2af03-252">예</span><span class="sxs-lookup"><span data-stu-id="2af03-252">Yes</span></span>                  | <span data-ttu-id="2af03-253">예</span><span class="sxs-lookup"><span data-stu-id="2af03-253">Yes</span></span>                  |
| <span data-ttu-id="2af03-254">방화벽 구성</span><span class="sxs-lookup"><span data-stu-id="2af03-254">Firewall configuration</span></span>           | <span data-ttu-id="2af03-255">예</span><span class="sxs-lookup"><span data-stu-id="2af03-255">Yes</span></span>                        | <span data-ttu-id="2af03-256">예</span><span class="sxs-lookup"><span data-stu-id="2af03-256">Yes</span></span>                                | <span data-ttu-id="2af03-257">예</span><span class="sxs-lookup"><span data-stu-id="2af03-257">Yes</span></span>                      | <span data-ttu-id="2af03-258">예</span><span class="sxs-lookup"><span data-stu-id="2af03-258">Yes</span></span>                            | <span data-ttu-id="2af03-259">예</span><span class="sxs-lookup"><span data-stu-id="2af03-259">Yes</span></span>                  | <span data-ttu-id="2af03-260">예</span><span class="sxs-lookup"><span data-stu-id="2af03-260">Yes</span></span>                  |
| <span data-ttu-id="2af03-261">SQL Server 구성</span><span class="sxs-lookup"><span data-stu-id="2af03-261">SQL Server configuration</span></span>         | <span data-ttu-id="2af03-262">예</span><span class="sxs-lookup"><span data-stu-id="2af03-262">Yes</span></span>                        | <span data-ttu-id="2af03-263">예</span><span class="sxs-lookup"><span data-stu-id="2af03-263">Yes</span></span>                                | <span data-ttu-id="2af03-264">예</span><span class="sxs-lookup"><span data-stu-id="2af03-264">Yes</span></span>                      | <span data-ttu-id="2af03-265">예</span><span class="sxs-lookup"><span data-stu-id="2af03-265">Yes</span></span>                            | <span data-ttu-id="2af03-266">예</span><span class="sxs-lookup"><span data-stu-id="2af03-266">Yes</span></span>                  | <span data-ttu-id="2af03-267">예</span><span class="sxs-lookup"><span data-stu-id="2af03-267">Yes</span></span>                  |
| <span data-ttu-id="2af03-268">성능 진단 추적 *</span><span class="sxs-lookup"><span data-stu-id="2af03-268">Performance Diagnostics Traces *</span></span> |                            |                                    | <span data-ttu-id="2af03-269">예</span><span class="sxs-lookup"><span data-stu-id="2af03-269">Yes</span></span>                      |                                |                      | <span data-ttu-id="2af03-270">예</span><span class="sxs-lookup"><span data-stu-id="2af03-270">Yes</span></span>                  |
| <span data-ttu-id="2af03-271">성능 카운터 추적 **</span><span class="sxs-lookup"><span data-stu-id="2af03-271">Performance counter Trace **</span></span>     |                            |                                    |                          |                                |                      | <span data-ttu-id="2af03-272">예</span><span class="sxs-lookup"><span data-stu-id="2af03-272">Yes</span></span>                  |
| <span data-ttu-id="2af03-273">SMB 카운터 추적 **</span><span class="sxs-lookup"><span data-stu-id="2af03-273">SMB counter Trace **</span></span>             |                            |                                    |                          |                                | <span data-ttu-id="2af03-274">예</span><span class="sxs-lookup"><span data-stu-id="2af03-274">Yes</span></span>                  |                      |
| <span data-ttu-id="2af03-275">SQL Server 카운터 추적 **</span><span class="sxs-lookup"><span data-stu-id="2af03-275">SQL Server counter Trace **</span></span>      |                            |                                    |                          |                                |                      | <span data-ttu-id="2af03-276">예</span><span class="sxs-lookup"><span data-stu-id="2af03-276">Yes</span></span>                  |
| <span data-ttu-id="2af03-277">XPerf 추적</span><span class="sxs-lookup"><span data-stu-id="2af03-277">XPerf Trace</span></span>                      |                            |                                    |                          |                                |                      | <span data-ttu-id="2af03-278">예</span><span class="sxs-lookup"><span data-stu-id="2af03-278">Yes</span></span>                  |
| <span data-ttu-id="2af03-279">StorPort 추적</span><span class="sxs-lookup"><span data-stu-id="2af03-279">StorPort Trace</span></span>                   |                            |                                    |                          |                                |                      | <span data-ttu-id="2af03-280">예</span><span class="sxs-lookup"><span data-stu-id="2af03-280">Yes</span></span>                  |
| <span data-ttu-id="2af03-281">네트워크 추적</span><span class="sxs-lookup"><span data-stu-id="2af03-281">Network Trace</span></span>                    |                            |                                    |                          |                                | <span data-ttu-id="2af03-282">예</span><span class="sxs-lookup"><span data-stu-id="2af03-282">Yes</span></span>                  | <span data-ttu-id="2af03-283">예</span><span class="sxs-lookup"><span data-stu-id="2af03-283">Yes</span></span>                  |
| <span data-ttu-id="2af03-284">Diskspd 벤치마크 추적 ***</span><span class="sxs-lookup"><span data-stu-id="2af03-284">Diskspd Benchmark trace ***</span></span>      |                            | <span data-ttu-id="2af03-285">예</span><span class="sxs-lookup"><span data-stu-id="2af03-285">Yes</span></span>                                |                          | <span data-ttu-id="2af03-286">예</span><span class="sxs-lookup"><span data-stu-id="2af03-286">Yes</span></span>                            |                      |                      |
|       |                            |                         |                                                   |                      |                      |

### <a name="performance-diagnostics-trace-"></a><span data-ttu-id="2af03-287">성능 진단 추적 (*)</span><span class="sxs-lookup"><span data-stu-id="2af03-287">Performance Diagnostics trace (*)</span></span>

<span data-ttu-id="2af03-288">규칙 기반 엔진 hello 배경 toocollect 데이터에서 실행 하 고 지속적인 성능 문제를 진단 합니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-288">Runs a rule-based engine in hello background toocollect data and diagnose ongoing performance issues.</span></span> <span data-ttu-id="2af03-289">hello 규칙은 현재 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-289">hello following rules are currently supported:</span></span>

- <span data-ttu-id="2af03-290">HighCpuUsage 규칙: 높은 CPU 사용 기간을 검색 하 고 해당 기간 동안 hello CPU 사용 하는 소비자를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-290">HighCpuUsage rule: Detects high CPU usage periods and shows hello top CPU usage consumers during those periods.</span></span>
- <span data-ttu-id="2af03-291">HighDiskUsage 규칙: 실제 디스크에서 디스크 사용 기간을 검색 하 고 해당 기간 동안 hello 상위 디스크 사용 소비자를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-291">HighDiskUsage rule: Detects high disk usage periods on physical disks and shows hello top disk usage consumers during those periods.</span></span>
- <span data-ttu-id="2af03-292">HighResolutionDiskMetric 규칙: 각 실제 디스크에 대한 50밀리초당 IOPS, 처리량 및 IO 대기 시간 메트릭을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-292">HighResolutionDiskMetric rule: Shows IOPS, throughput and IO latency metrics per 50 milliseconds for each physical disk.</span></span> <span data-ttu-id="2af03-293">Tooquickly 기간을 제한 하는 디스크를 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-293">It helps tooquickly identify disk throttling periods.</span></span>
- <span data-ttu-id="2af03-294">HighMemoryUsage 규칙: 높은 메모리 사용 기간을 검색 하 고 해당 기간 동안 hello 상위 메모리 사용 소비자를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-294">HighMemoryUsage rule: Detects high memory usage periods, and shows hello top memory usage consumers during those periods.</span></span>

> [!NOTE] 
> <span data-ttu-id="2af03-295">현재.NET Framework 3.5 hello를 포함 하는 Windows 버전 또는 이후 버전은 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-295">Currently, Windows versions that include hello .NET Framework 3.5 or later versions are supported.</span></span>

### <a name="performance-counter-trace-"></a><span data-ttu-id="2af03-296">성능 카운터 추적 (**)</span><span class="sxs-lookup"><span data-stu-id="2af03-296">Performance Counter trace (**)</span></span>

<span data-ttu-id="2af03-297">Hello 다음 성능 카운터를 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-297">Collects hello following Performance Counters:</span></span>

- <span data-ttu-id="2af03-298">\Process, \Processor, \Memory, \Thread, \PhysicalDisk, \LogicalDisk</span><span class="sxs-lookup"><span data-stu-id="2af03-298">\Process, \Processor, \Memory, \Thread, \PhysicalDisk, \LogicalDisk</span></span>
- <span data-ttu-id="2af03-299">\Cache\Dirty Pages, \Cache\Lazy Write Flushes/sec, \Server\Pool Nonpaged, Failures, \Server\Pool Paged Failures</span><span class="sxs-lookup"><span data-stu-id="2af03-299">\Cache\Dirty Pages, \Cache\Lazy Write Flushes/sec, \Server\Pool Nonpaged, Failures, \Server\Pool Paged Failures</span></span>
- <span data-ttu-id="2af03-300">\Network Interface, \IPv4\Datagrams, \IPv6\Datagrams, \TCPv4\Segments, \TCPv6\Segments, \Network Adapter, \WFPv4\Packets, \WFPv6\Packets, \UDPv4\Datagrams, \UDPv6\Datagrams, \TCPv4\Connection, \TCPv6\Connection, \Network QoS Policy\Packets, \Per Processor Network Interface Card Activity, \Microsoft Winsock BSP 중에서 선택한 카운터</span><span class="sxs-lookup"><span data-stu-id="2af03-300">Selected counters under \Network Interface, \IPv4\Datagrams, \IPv6\Datagrams, \TCPv4\Segments, \TCPv6\Segments,  \Network Adapter, \WFPv4\Packets, \WFPv6\Packets, \UDPv4\Datagrams, \UDPv6\Datagrams, \TCPv4\Connection, \TCPv6\Connection, \Network QoS Policy\Packets, \Per Processor Network Interface Card Activity, \Microsoft Winsock BSP</span></span>

#### <a name="for-sql-server-instances"></a><span data-ttu-id="2af03-301">SQL Server 인스턴스의 경우</span><span class="sxs-lookup"><span data-stu-id="2af03-301">For SQL Server instances</span></span>
- <span data-ttu-id="2af03-302">\SQL Server:Buffer Manager, \SQLServer:Resource Pool Stats, \SQLServer:SQL Statistics\\</span><span class="sxs-lookup"><span data-stu-id="2af03-302">\SQL Server:Buffer Manager, \SQLServer:Resource Pool Stats, \SQLServer:SQL Statistics\\</span></span>
- <span data-ttu-id="2af03-303">\SQLServer:Locks, \SQLServer:General, Statistics</span><span class="sxs-lookup"><span data-stu-id="2af03-303">\SQLServer:Locks, \SQLServer:General, Statistics</span></span>
- <span data-ttu-id="2af03-304">\SQLServer:Access Methods</span><span class="sxs-lookup"><span data-stu-id="2af03-304">\SQLServer:Access Methods</span></span>

#### <a name="for-azure-files"></a><span data-ttu-id="2af03-305">Azure Files의 경우</span><span class="sxs-lookup"><span data-stu-id="2af03-305">For Azure Files</span></span>
<span data-ttu-id="2af03-306">\SMB Client Shares</span><span class="sxs-lookup"><span data-stu-id="2af03-306">\SMB Client Shares</span></span>

### <a name="diskspd-benchmark-trace-"></a><span data-ttu-id="2af03-307">Diskspd 벤치마크 추적 (***)</span><span class="sxs-lookup"><span data-stu-id="2af03-307">Diskspd Benchmark trace (***)</span></span>
<span data-ttu-id="2af03-308">Diskspd IO 워크로드 테스트[OS 디스크(쓰기) 및 풀 드라이브(읽기/쓰기)]</span><span class="sxs-lookup"><span data-stu-id="2af03-308">Diskspd IO workload tests [OS Disk (write) and pool drives (read/write)]</span></span>

## <a name="run-hello-perfinsights-on-your-vm"></a><span data-ttu-id="2af03-309">Hello PerfInsights VM에서 실행</span><span class="sxs-lookup"><span data-stu-id="2af03-309">Run hello PerfInsights on your VM</span></span>

### <a name="what-do-i-have-tooknow-before-i-run-hello-script"></a><span data-ttu-id="2af03-310">어떤 용량은 tooknow hello 스크립트를 실행 하기 전에</span><span class="sxs-lookup"><span data-stu-id="2af03-310">What do I have tooknow before I run hello script?</span></span> 

<span data-ttu-id="2af03-311">**스크립트 요구 사항**</span><span class="sxs-lookup"><span data-stu-id="2af03-311">**Script requirements**</span></span>

1.  <span data-ttu-id="2af03-312">이 스크립트는 hello hello 성능 문제가 있는 VM에서 실행 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-312">This script must be run on hello VM that has hello performance issue.</span></span> 

2.  <span data-ttu-id="2af03-313">다음 예: 지원 되는 hello: Windows Server 2008 R2, 2012, 2012 R2, 2016; Windows 8.1 및 Windows 10입니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-313">hello following OSes are supported: Windows Server 2008 R2, 2012, 2012 R2, 2016; Windows 8.1 and Windows 10.</span></span>

<span data-ttu-id="2af03-314">**가능한 문제 프로덕션 Vm에서 hello 스크립트를 실행 하는 경우:**</span><span class="sxs-lookup"><span data-stu-id="2af03-314">**Possible issues when you run hello script on production VMs:**</span></span>

1.  <span data-ttu-id="2af03-315">XPerf 또는 DiskSpd를 사용 하 여 구성 된 hello "벤치 마크" 또는 "Custom" 시나리오와 함께 사용 하는 경우 hello 스크립트 hello VM의 hello 성능이 저하 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-315">hello script might adversely affect hello performance of hello VM when it is used together with hello "Benchmark" or "Custom" scenario that is configured by using XPerf or DiskSpd.</span></span> <span data-ttu-id="2af03-316">프로덕션 환경에서 hello 스크립트를 실행할 때 주의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-316">Be careful when you run hello script in a production environment.</span></span>

2.  <span data-ttu-id="2af03-317">DiskSpd를 사용 하 여 구성 된 hello "벤치 마크" 또는 "Custom" 시나리오와 함께 hello 스크립트를 사용 하면 테스트 hello 디스크에서 I/O 작업이 hello 방해가 다른 백그라운드 작업이 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-317">When you use hello script together with hello "Benchmark" or "Custom" scenario that is configured by using DiskSpd, make sure that no other background activity interferes with hello I/O workload on hello tested disks.</span></span>

3.  <span data-ttu-id="2af03-318">기본적으로 hello 스크립트 hello 임시 저장소 드라이브 toocollect 데이터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-318">By default, hello script uses hello temporary storage drive toocollect data.</span></span> <span data-ttu-id="2af03-319">더 긴 시간 동안 사용 하도록 설정 하는 유지 되며, 추적 하는 경우 수집 되는 데이터 양을 hello 관련성 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-319">If tracing stays enabled for a longer time, hello amount of data that is collected might be relevant.</span></span> <span data-ttu-id="2af03-320">이렇게 하면 hello 가용성 따라서이 드라이브에 의존 하는 모든 응용 프로그램에 영향을 주는 hello 임시 디스크 공간을 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-320">This can reduce hello availability of space on hello temporary disk, therefore affecting any application that relies on this drive.</span></span>

### <a name="how-do-i-run-perfinsights"></a><span data-ttu-id="2af03-321">PerfInsights를 실행하는 방법</span><span class="sxs-lookup"><span data-stu-id="2af03-321">How do I run PerfInsights?</span></span> 

<span data-ttu-id="2af03-322">toorun 스크립트 hello, 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-322">toorun hello script, follow these steps:</span></span>

1. <span data-ttu-id="2af03-323">[PerfInsights.zip](http://aka.ms/perfinsightsdownload)을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-323">Download [PerfInsights.zip](http://aka.ms/perfinsightsdownload).</span></span>

2. <span data-ttu-id="2af03-324">Hello PerfInsights.zip 파일 차단을 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-324">Unblock hello PerfInsights.zip file.</span></span> <span data-ttu-id="2af03-325">이 마우스 오른쪽 단추로 클릭 hello PerfInsights.zip 파일 선택 toodo **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-325">toodo this, right-click hello PerfInsights.zip file, select **Properties**.</span></span> <span data-ttu-id="2af03-326">Hello에 **일반** 탭에서 **차단 해제** 선택한 후 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-326">In hello **General** tab, select **Unblock** and then select **OK**.</span></span> <span data-ttu-id="2af03-327">Hello 스크립트 추가적인 보안 메시지 표시 없이 실행 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-327">This will make sure that hello script runs without any additional security prompts.</span></span>  

    ![Hello zip 파일의 잠금을 해제합니다](media/how-to-use-perfInsights/unlock-file.png)

3.  <span data-ttu-id="2af03-329">임시 드라이브 (기본적으로 보통 hello D 드라이브)에 압축 hello PerfInsights.zip 파일을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-329">Expand hello compressed PerfInsights.zip file into your temporary drive (by default, usually hello D drive).</span></span> <span data-ttu-id="2af03-330">hello 압축 된 파일을 포함 해야 hello 다음 파일 및 폴더:</span><span class="sxs-lookup"><span data-stu-id="2af03-330">hello compressed file should contain hello following files and folders:</span></span>

    ![hello zip 폴더의 파일](media/how-to-use-perfInsights/file-folder.png)

4.  <span data-ttu-id="2af03-332">관리자 권한으로 Windows PowerShell을 열고 hello PerfInsights.ps1 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-332">Open Windows PowerShell as an administrator, and then run hello PerfInsights.ps1 script.</span></span>

    ```
    cd <hello path of PerfInsights folder >
    Powershell.exe -ExecutionPolicy UnRestricted -NoProfile -File .\\PerfInsights.ps1
    ```

    <span data-ttu-id="2af03-333">"Y" tooenter를 할 수 있습니다는 tooif toochange hello 실행 정책을 원하는 tooconfirm 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-333">You might have tooenter "y" tooif you are asked tooconfirm that you want toochange hello execution policy.</span></span>

    <span data-ttu-id="2af03-334">Hello 부인 대화 상자에서 Microsoft 기술 지원 서비스와 함께 hello 옵션 tooshare 진단 정보를 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-334">In hello Disclaimer dialog box, you are given hello option tooshare diagnostic information with Microsoft Support.</span></span> <span data-ttu-id="2af03-335">또한 toohello 사용권 계약 toocontinue를 동의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-335">You must also consent toohello license agreement toocontinue.</span></span> <span data-ttu-id="2af03-336">선택한 다음 **스크립트 실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-336">Make your selections, and then click **Run Script**.</span></span>

    ![고지 사항 상자](media/how-to-use-perfInsights/disclaimer.png)

5.  <span data-ttu-id="2af03-338">사용 가능한 경우, (이 통계에 대 한은) hello 스크립트를 실행할 때 hello 사례 번호를 제출 합니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-338">Submit hello case number, if it is available, when you run hello script (This is for our statistics).</span></span> <span data-ttu-id="2af03-339">그런 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-339">Then, click **OK**.</span></span>
    
    ![지원 ID 입력](media/how-to-use-perfInsights/enter-support-number.png)

6.  <span data-ttu-id="2af03-341">임시 저장소 드라이브를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-341">Select your temporary storage drive.</span></span> <span data-ttu-id="2af03-342">hello 스크립트는 hello 드라이브의 드라이브 문자 hello 자동 감지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-342">hello Script can auto-detect hello drive letter of hello drive.</span></span> <span data-ttu-id="2af03-343">이 단계에서 문제가 발생 하는 경우 수도 있습니다 tooselect hello 드라이브 라는 메시지가 표시 (hello 기본 드라이브는 D).</span><span class="sxs-lookup"><span data-stu-id="2af03-343">If any problems occur in this stage, you might be prompted tooselect hello drive (hello default drive is D).</span></span> <span data-ttu-id="2af03-344">Hello 로그에 생성 된 로그는 여기에 저장 하는\_컬렉션 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-344">Generated logs are stored here in hello log\_collection folder.</span></span> <span data-ttu-id="2af03-345">을 입력 하거나 hello 드라이브 문자를 적용 한 후 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-345">After you enter or accept hello drive letter, click **OK**.</span></span>

    ![드라이브 입력](media/how-to-use-perfInsights/enter-drive.png)

7.  <span data-ttu-id="2af03-347">Hello 제공 목록에서에서 문제 해결 시나리오를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-347">Select a troubleshooting scenario from hello provided list.</span></span>

       ![지원 시나리오 선택](media/how-to-use-perfInsights/select-scenarios.png)

8.  <span data-ttu-id="2af03-349">UI 없이 PerfInsights를 실행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-349">You can also run PerfInsights without UI.</span></span>

    <span data-ttu-id="2af03-350">hello 다음 실행 hello UI 프롬프트 없이 시나리오 문제 해결 "일반 VM 저속 분석" 명령을 선택 하거나 30 초 동안 데이터를 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-350">hello following command runs hello "General VM Slow analysis" troubleshooting scenario without a UI prompt or capture data for 30 seconds.</span></span> <span data-ttu-id="2af03-351">묻는 tooconsent toohello 동일한 부인과 4 단계에서 설명 하는 EULA 합니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-351">It prompts you tooconsent toohello same disclaimer and EULA that  are mentioned in step 4.</span></span>

        powershell.exe -ExecutionPolicy UnRestricted -NoProfile -Command ".\\PerfInsights.ps1 -NoGui -Scenario vmslow -TracingDuration 30"

    <span data-ttu-id="2af03-352">자동 모드에서 PerfInsights toorun 하려는 경우 사용 된 **-AcceptDisclaimerAndShareDiagnostics** 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-352">If you want PerfInsights toorun in silent mode, use the **-AcceptDisclaimerAndShareDiagnostics** parameter.</span></span> <span data-ttu-id="2af03-353">예를 들어 다음 명령을 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-353">For example, use hello following command:</span></span>

        powershell.exe -ExecutionPolicy UnRestricted -NoProfile -Command ".\\PerfInsights.ps1 -NoGui -Scenario vmslow -TracingDuration 30 -AcceptDisclaimerAndShareDiagnostics"

### <a name="how-do-i-troubleshoot-issues-while-running-hello-script"></a><span data-ttu-id="2af03-354">Hello 스크립트를 실행 하는 동안 문제를 해결 하려면 어떻게 합니까?</span><span class="sxs-lookup"><span data-stu-id="2af03-354">How do I troubleshoot issues while running hello script?</span></span>

<span data-ttu-id="2af03-355">와 함께 hello 스크립트를 실행 하 여 일관성이 없는 상태를 정리할 수 hello 스크립트 비정상적으로 종료 되 면 hello-정리 스위치 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-355">If hello script terminates abnormally, you can clean up an inconsistent state by running hello script together with hello -Cleanup switch, as follows:</span></span>

    powershell.exe -ExecutionPolicy UnRestricted -NoProfile -Command ".\\PerfInsights.ps1 -Cleanup"

<span data-ttu-id="2af03-356">Hello hello 임시 드라이브의 자동 검색 하는 동안 문제가 발생을 것일 경우 tooselect hello 드라이브 라는 메시지가 표시 (hello 기본 드라이브는 D).</span><span class="sxs-lookup"><span data-stu-id="2af03-356">If any problems occur during hello automatic detection of hello temporary drive, you might be prompted tooselect hello drive (hello default drive is D).</span></span>

![드라이브 입력](media/how-to-use-perfInsights/enter-drive.png)

<span data-ttu-id="2af03-358">hello 스크립트 hello 유틸리티 도구를 제거 하 고 임시 폴더를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-358">hello script uninstalls hello utility tools and removes temporary folders.</span></span>

### <a name="troubleshooting-other-script-issues"></a><span data-ttu-id="2af03-359">기타 스크립트 문제 해결</span><span class="sxs-lookup"><span data-stu-id="2af03-359">Troubleshooting other script issues</span></span> 

<span data-ttu-id="2af03-360">Hello 스크립트를 실행할 때 문제가 발생 하는 경우 Ctrl + C toointerrupt hello 스크립트 실행 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-360">If any problems occur when you run hello script, press Ctrl+C toointerrupt hello script execution.</span></span> <span data-ttu-id="2af03-361">tooremove 임시 개체는 hello "비정상적인 종료 후 정리" 섹션을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-361">tooremove temporary objects, see hello "Clean up after abnormal termination" section.</span></span>

<span data-ttu-id="2af03-362">Tooexperience 스크립트 실패를 몇 차례 시도 후에 계속 진행 하면 좋습니다 "디버그 모드" hello 스크립트를 실행 하는 hello를 사용 하 여 "-디버그" 시작할 때 매개 변수 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-362">If you continue tooexperience script failure even after several attempts, we recommend that you run hello script in "debug mode" by using hello "-Debug" parameter option on startup.</span></span>

<span data-ttu-id="2af03-363">Toohello Microsoft 지원 에이전트 역할을 담당 하기 지원을 받는 보낼 hello 오류 발생, hello PowerShell 콘솔의 복사 hello 전체 출력 한 후 toohelp hello 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-363">After hello failure occurs, copy hello full output of hello PowerShell console, and send it toohello Microsoft Support agent who is assisting you toohelp troubleshoot hello problem.</span></span>

### <a name="how-do-i-run-hello-script-in-custom-configuration-mode"></a><span data-ttu-id="2af03-364">사용자 지정 구성 모드로 hello 스크립트를 실행 하려면 어떻게 합니까?</span><span class="sxs-lookup"><span data-stu-id="2af03-364">How do I run hello script in custom configuration mode?</span></span>

<span data-ttu-id="2af03-365">Hello를 선택 하 여 **사용자 지정** 구성 (사용 하 여 Shift toomulti 선택) 동시에 여러 추적을 활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-365">By selecting hello **Custom** configuration, you can enable several traces in parallel (use Shift toomulti-select):</span></span>

![시나리오 선택](media/how-to-use-perfInsights/select-scenario.png)

<span data-ttu-id="2af03-367">Hello 성능 진단, 성능 카운터를 추적, XPerf 추적, 네트워크 추적 또는 Storport 추적 시나리오를 선택 하면 hello 대화 상자에서 hello 지침에 따라 한 hello 추적을 시작한 후에 tooreproduce hello 성능 저하 문제를 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="2af03-367">When you select hello Performance Diagnostics, Performance Counter Trace, XPerf Trace, Network Trace, or Storport Trace scenarios, follow hello instructions in hello dialog boxes, and try tooreproduce hello slow performance issue after you start hello traces.</span></span>

<span data-ttu-id="2af03-368">대화 상자를 수행 하는 hello 추적을 시작 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-368">hello following dialog box lets you start a trace:</span></span>

![추적 시작](media/how-to-use-perfInsights/start-trace-message.png)

<span data-ttu-id="2af03-370">toostop hello 추적을 두 번째 대화 상자 내에서 tooconfirm hello 명령을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-370">toostop hello traces, you have tooconfirm hello command in a second dialog box.</span></span>

<span data-ttu-id="2af03-371">![추적 중지](media/how-to-use-perfInsights/stop-trace-message.png)
![추적 중지](media/how-to-use-perfInsights/ok-trace-message.png)</span><span class="sxs-lookup"><span data-stu-id="2af03-371">![stop-trace](media/how-to-use-perfInsights/stop-trace-message.png)
![stop-trace](media/how-to-use-perfInsights/ok-trace-message.png)</span></span>

<span data-ttu-id="2af03-372">추적 때 hello 또는 작업이 완료 되, d:에 새 파일이 생성 됩니다\\로그\_컬렉션 (또는 hello 임시 드라이브) 라는 **CollectedData\_yyyy-월-일\_hh\_mm \_ss.zip 합니다.**</span><span class="sxs-lookup"><span data-stu-id="2af03-372">When hello traces or operations are completed, a new file is generated in D:\\log\_collection (or hello temporary drive) that is named **CollectedData\_yyyy-MM-dd\_hh\_mm\_ss.zip.**</span></span> <span data-ttu-id="2af03-373">이 파일 toohello 지원 에이전트 분석을 위해 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-373">You can send this file toohello Support agent for analysis.</span></span>

## <a name="review-hello-diagnostics-report-created-by-perfinsights"></a><span data-ttu-id="2af03-374">PerfInsights에서 만든 hello 진단 보고서를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-374">Review hello diagnostics report created by PerfInsights</span></span>

<span data-ttu-id="2af03-375">Hello 내 **CollectedData\_yyyy-월-일\_hh\_mm\_ss.zip 파일** PerfInsights 생성 하는의 hello 결과 자세히 설명 하는 HTML 보고서를 찾을 수 있습니다 PerfInsights 합니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-375">Within hello **CollectedData\_yyyy-MM-dd\_hh\_mm\_ss.zip file,** that is generated by PerfInsights, you can find an HTML report that details hello findings of PerfInsights.</span></span> <span data-ttu-id="2af03-376">tooreview 보고서 hello를 hello 확장 **CollectedData\_yyyy-월-일\_hh\_mm\_ss.zip** 파일을 열고 hello **PerfInsights Report.html**파일입니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-376">tooreview hello report, expand hello **CollectedData\_yyyy-MM-dd\_hh\_mm\_ss.zip** file, and then open hello **PerfInsights Report.html** file.</span></span>

<span data-ttu-id="2af03-377">선택 hello **결과** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-377">Select hello **Findings** tab.</span></span>

![찾기 탭](media/how-to-use-perfInsights/findingtab.png)

<span data-ttu-id="2af03-379">**참고 사항**</span><span class="sxs-lookup"><span data-stu-id="2af03-379">**Notes**</span></span>

-   <span data-ttu-id="2af03-380">빨간색 메시지는 성능 문제를 일으킬 수 있는 알려진 구성 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-380">Messages in red are known configuration issues that may cause performance issues.</span></span>

-   <span data-ttu-id="2af03-381">노란색 메시지는 반드시 성능 문제를 일으키지는 않지만 최적이 아닌 구성을 나타내는 경고입니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-381">Messages in yellow are warnings that represent non-optimal configurations that do not necessarily cause performance issues.</span></span>

-   <span data-ttu-id="2af03-382">파란색 메시지는 유익한 정보만 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-382">Messages in blue are informative statements only.</span></span>

<span data-ttu-id="2af03-383">검토 hello 빨간색 tooget의 모든 오류 메시지에 대 한 HTTP 링크 hello 한 결과 및 어떻게 영향을 미치는지 hello 성능이 나 성능 액세스에 최적화 된 구성에 대 한 모범 사례에 대 한 정보를 더 자세한 합니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-383">Review hello HTTP links for all error messages in red tooget more detailed information about hello findings and how they can affect hello performance or best practices for performance-optimized configurations.</span></span>

### <a name="disk-configuration-tab"></a><span data-ttu-id="2af03-384">디스크 구성 탭</span><span class="sxs-lookup"><span data-stu-id="2af03-384">Disk Configuration Tab</span></span>

<span data-ttu-id="2af03-385">hello **개요** 섹션 hello 저장소 구성, Diskpart 및 저장소 공간에서 정보를 포함 하 여 다른 보기를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-385">hello **Overview** section displays different views of hello storage configuration, including information from Diskpart and Storage Spaces</span></span>

<span data-ttu-id="2af03-386">hello **DiskMap** 및 **VolumeMap** 설명 어떻게 논리는 이중 관점에 볼륨 및 실제 디스크는 기타 관련된 tooeach 합니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-386">hello **DiskMap** and **VolumeMap** sections describe on a dual perspective how logical volumes and physical disks are related tooeach other.</span></span>

<span data-ttu-id="2af03-387">실제 디스크 관점 (DiskMap) hello hello 테이블 hello 디스크에서 실행 되는 모든 논리 볼륨을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-387">In hello PhysicalDisk perspective (DiskMap), hello table shows all logical volumes that are running on hello disk.</span></span> <span data-ttu-id="2af03-388">다음 예제는 hello, PhysicalDrive2 여러 파티션을 (J 및 H)에서 만든 논리 볼륨 2를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-388">In hello following example, PhysicalDrive2 runs 2 Logical Volumes created on multiple partitions (J and H):</span></span>

![데이터 탭](media/how-to-use-perfInsights/disktab.png)

<span data-ttu-id="2af03-390">Hello 볼륨 관점에서에서 (*VolumeMap*), hello 테이블의 각 논리 볼륨에서 모든 hello 실제 디스크를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-390">In hello Volume perspective (*VolumeMap*), hello tables show all hello physical disks under each logical volume.</span></span> <span data-ttu-id="2af03-391">RAID/동적 디스크의 경우 여러 실제 디스크에서 논리 볼륨을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-391">Notice that for RAID/Dynamic disks, you might run a logical volume upon multiple physical disks.</span></span> <span data-ttu-id="2af03-392">다음 예제는 hello에 *c:\\탑재* 로 구성 하는 "탑재 지점"은 *SpannedDisk* PhysicalDisks에 \#2 및 \#3:</span><span class="sxs-lookup"><span data-stu-id="2af03-392">In hello following sample *C:\\mount* is a mountpoint configured as *SpannedDisk* on PhysicalDisks \#2 and \#3:</span></span>

![볼륨 탭](media/how-to-use-perfInsights/volumetab.png)

### <a name="sql-server-tab"></a><span data-ttu-id="2af03-394">SQL Server 탭</span><span class="sxs-lookup"><span data-stu-id="2af03-394">SQL Server tab</span></span>

<span data-ttu-id="2af03-395">명명 된 hello 보고서의 탭이 추가로 표시는 hello 대상 VM에서 SQL Server 인스턴스를 호스팅하는 경우 **SQL Server**:</span><span class="sxs-lookup"><span data-stu-id="2af03-395">If hello target VM hosts any SQL Server instances, you will see an additional tab in hello report that is named **SQL Server**:</span></span>

![sql 탭](media/how-to-use-perfInsights/sqltab.png)

<span data-ttu-id="2af03-397">이 섹션의 hello VM에서 호스팅되는 hello SQL Server 인스턴스 각각에 대해 "개요" 및 추가 하위 탭을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-397">This section contains an "Overview" and additional sub tabs for each of hello SQL Server instances hosted on hello VM.</span></span>

<span data-ttu-id="2af03-398">hello "개요" 섹션에는 모든 hello 실제 디스크 (시스템 및 데이터 디스크) 실행 되 고 있는 다양 한 데이터 파일 및 트랜잭션 로그 파일을 포함 하는 요약 하는 것이 도움이 테이블 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-398">hello "Overview" section contains a helpful table that summarizes all hello physical disks (system and data disks) that are running and that contain a mixture of data files and transaction log files.</span></span>

<span data-ttu-id="2af03-399">다음 예에서는, hello에 *PhysicalDrive0* hello 모두 때문에 표시 됩니다 (실행 hello C 드라이브) *modeldev* 및 *modellog* hello C 드라이브에 있는 파일 및 서로 다른 형식의 (예: 데이터 파일 및 트랜잭션 로그를 각각):</span><span class="sxs-lookup"><span data-stu-id="2af03-399">In hello following example, *PhysicalDrive0* (running hello C drive) is displayed because both hello *modeldev* and *modellog* files are located on hello C drive, and they are of different types (such as Data File and Transaction Log, respectively):</span></span>

![로그 정보](media/how-to-use-perfInsights/loginfo.png)

<span data-ttu-id="2af03-401">hello SQL Server 인스턴스 관련 탭 hello 선택한 인스턴스에 대 한 기본 정보를 표시 하는 일반 섹션 및 설정, 구성 및 사용자 옵션을 비롯 한 고급 정보에 대 한 추가 섹션이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-401">hello SQL Server instance-specific tabs contain a general section that displays basic information about hello selected instance and additional sections for advanced information, including Settings, Configurations, and User Options.</span></span>

## <a name="references-toohello-external-tools-used"></a><span data-ttu-id="2af03-402">사용 되는 toohello 외부 도구 참조</span><span class="sxs-lookup"><span data-stu-id="2af03-402">References toohello external tools used</span></span>

### <a name="diskspd"></a><span data-ttu-id="2af03-403">Diskspd</span><span class="sxs-lookup"><span data-stu-id="2af03-403">Diskspd</span></span>

<span data-ttu-id="2af03-404">DISKSPD는 저장소 로드 생성기 및 성능 테스트 도구 hello Windows 및 Windows Server 및 클라우드 서버 인프라 엔지니어링 팀에서.</span><span class="sxs-lookup"><span data-stu-id="2af03-404">DISKSPD is a storage load generator and performance test tool from hello Windows and Windows Server and Cloud Server Infrastructure engineering teams.</span></span> <span data-ttu-id="2af03-405">자세한 내용은 [Diskspd](https://github.com/Microsoft/diskspd)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2af03-405">For more information, see [Diskspd](https://github.com/Microsoft/diskspd).</span></span>

### <a name="xperf"></a><span data-ttu-id="2af03-406">XPerf</span><span class="sxs-lookup"><span data-stu-id="2af03-406">XPerf</span></span>

<span data-ttu-id="2af03-407">Xperf는 hello Windows 성능 도구 키트에서에서 명령줄 도구 toocapture 추적입니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-407">Xperf is a command-line tool toocapture traces from hello Windows Performance Tools Kit.</span></span>

<span data-ttu-id="2af03-408">자세한 내용은 [Windows 성능 도구 키트 - Xperf(영문)](https://blogs.msdn.microsoft.com/ntdebugging/2008/04/03/windows-performance-toolkit-xperf/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2af03-408">For more information, see [Windows Performance Toolkit – Xperf](https://blogs.msdn.microsoft.com/ntdebugging/2008/04/03/windows-performance-toolkit-xperf/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2af03-409">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2af03-409">Next Steps</span></span>

### <a name="upload-diagnostics-logs-and-reports-toomicrosoft-support-for-further-review"></a><span data-ttu-id="2af03-410">업로드 진단 기록 및 검토 지원 tooMicrosoft 보고</span><span class="sxs-lookup"><span data-stu-id="2af03-410">Upload diagnostics logs and reports tooMicrosoft Support for further review</span></span>

<span data-ttu-id="2af03-411">Microsoft 지원 담당자 hello로 작업할 때 PerfInsights tooassist hello 문제 해결 과정에서 생성 되는 요청 된 tootransmit hello 출력 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-411">When you work with hello Microsoft Support staff, you may be requested tootransmit hello output that is generated by PerfInsights tooassist hello troubleshooting process.</span></span>

<span data-ttu-id="2af03-412">hello 지원 에이전트 DTM 작업 영역을 만들고 [DTM 포털 (https://filetransfer.support.microsoft.com/EFTClient/Account/Login.htm)와 고유한 사용자 ID와 암호 링크 toohello 포함 된 전자 메일 메시지를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-412">hello Support agent will create a DTM workspace for you, and you will receive an email message that includes a link toohello [DTM portal (https://filetransfer.support.microsoft.com/EFTClient/Account/Login.htm) and a unique user ID and password.</span></span>

<span data-ttu-id="2af03-413">이 메시지는 **CTS 자동 진단 서비스**(ctsadiag@microsoft.com)에서 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-413">This message will be sent from **CTS Automated Diagnostics Services** (ctsadiag@microsoft.com).</span></span>

![Hello 메시지의 샘플](media/how-to-use-perfInsights/supportemail.png)

<span data-ttu-id="2af03-415">추가 보안을 위해 됩니다 필요 toochange에서 암호를 먼저 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-415">For additional security, you will be required toochange your password on first use.</span></span>

<span data-ttu-id="2af03-416">대화 상자 tooupload hello 있습니다. tooDTM에 로그인 한 후 **CollectedData\_yyyy-월-일\_hh\_mm\_ss.zip** PerfInsights 여 수집 된 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="2af03-416">After you log in tooDTM, you will find a dialog box tooupload hello **CollectedData\_yyyy-MM-dd\_hh\_mm\_ss.zip** file that was collected by PerfInsights.</span></span>
