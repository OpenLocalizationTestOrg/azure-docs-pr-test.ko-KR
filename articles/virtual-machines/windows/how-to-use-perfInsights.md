---
title: "Microsoft Azure에서 PerfInsights를 사용하는 방법 | Microsoft Docs"
description: "PerfInsights를 사용하여 Windows VM 성능 문제를 해결하는 방법을 설명합니다."
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
ms.openlocfilehash: f22bd42302b96118dba0d4e5e387c6798a0b8777
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-perfinsights"></a><span data-ttu-id="9518d-103">PerfInsights를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="9518d-103">How to use PerfInsights</span></span> 

<span data-ttu-id="9518d-104">[PerfInsights](http://aka.ms/perfinsightsdownload)는 유용한 진단 정보를 수집하고, I/O 스트레스 부하를 실행하며, Microsoft Azure에서 Windows VM 성능 문제를 해결하는 데 도움이 되는 분석 보고서를 제공하는 자동화된 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-104">[PerfInsights](http://aka.ms/perfinsightsdownload) is an automated script that collects useful diagnostic information, runs I/O stress loads, and provides an analysis report to help troubleshoot Windows VM performance problems in Microsoft Azure.</span></span> 

<span data-ttu-id="9518d-105">VM 성능 문제로 Microsoft 지원 티켓을 열기 전에 이 스크립트를 실행하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-105">We recommend that you run this script before you open a Support ticket with Microsoft for VM performance issues.</span></span>

## <a name="supported-troubleshooting-scenarios"></a><span data-ttu-id="9518d-106">지원되는 문제 해결 시나리오</span><span class="sxs-lookup"><span data-stu-id="9518d-106">Supported troubleshooting scenarios</span></span>

<span data-ttu-id="9518d-107">PerfInsights에서는 고유한 시나리오로 그룹화된 여러 종류의 정보를 수집하고 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-107">PerfInsights can collect and analyze several kinds of information that are grouped into unique scenarios.</span></span>

### <a name="collect-disk-configuration"></a><span data-ttu-id="9518d-108">디스크 구성 수집</span><span class="sxs-lookup"><span data-stu-id="9518d-108">Collect disk configuration</span></span> 

<span data-ttu-id="9518d-109">이 시나리오에서는 다음 항목을 포함하여 디스크 구성 및 기타 중요한 정보를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-109">This scenario collects the disk configuration and other important information, including the following items:</span></span>

-   <span data-ttu-id="9518d-110">이벤트 로그</span><span class="sxs-lookup"><span data-stu-id="9518d-110">Event logs</span></span>

-   <span data-ttu-id="9518d-111">모든 들어오는 연결과 나가는 연결에 대한 네트워크 상태</span><span class="sxs-lookup"><span data-stu-id="9518d-111">Network status for all incoming and outgoing connections</span></span>

-   <span data-ttu-id="9518d-112">네트워크 및 방화벽 구성 설정</span><span class="sxs-lookup"><span data-stu-id="9518d-112">Network and firewall configuration settings</span></span>

-   <span data-ttu-id="9518d-113">현재 시스템에서 실행 중인 모든 응용 프로그램의 작업 목록</span><span class="sxs-lookup"><span data-stu-id="9518d-113">Task list for all applications that are currently running on the system</span></span>

-   <span data-ttu-id="9518d-114">msinfo32에서 VM(가상 컴퓨터)에 대해 만든 정보 파일</span><span class="sxs-lookup"><span data-stu-id="9518d-114">Information file created by msinfo32 for the virtual machine (VM)</span></span>

-   <span data-ttu-id="9518d-115">Microsoft SQL Server 데이터베이스 구성 설정(VM이 SQL Server를 실행하는 서버로 식별된 경우)</span><span class="sxs-lookup"><span data-stu-id="9518d-115">Microsoft SQL Server database configuration settings (if the VM is identified as a server that is running SQL Server)</span></span>

-   <span data-ttu-id="9518d-116">저장소 안정성 카운터</span><span class="sxs-lookup"><span data-stu-id="9518d-116">Storage reliability counters</span></span>

-   <span data-ttu-id="9518d-117">중요한 Windows 핫픽스</span><span class="sxs-lookup"><span data-stu-id="9518d-117">Important Windows hotfixes</span></span>

-   <span data-ttu-id="9518d-118">설치된 필터 드라이버</span><span class="sxs-lookup"><span data-stu-id="9518d-118">Installed filter drivers</span></span>

<span data-ttu-id="9518d-119">이 모음은 시스템에 영향을 주지 않아야 하는 수동적인 정보 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-119">This is a passive collection of information that shouldn't affect the system.</span></span> 

>[!Note]
><span data-ttu-id="9518d-120">이 시나리오는 다음과 같은 각각의 시나리오에 자동으로 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-120">This scenario is automatically included in each of the following scenarios.</span></span>

### <a name="benchmarkstorage-performance-test"></a><span data-ttu-id="9518d-121">벤치마크/저장소 성능 테스트</span><span class="sxs-lookup"><span data-stu-id="9518d-121">Benchmark/Storage Performance Test</span></span>

<span data-ttu-id="9518d-122">이 시나리오에서는 VM에 연결된 모든 드라이브에 대해 [diskspd](https://github.com/Microsoft/diskspd) 벤치마크 테스트(IOPS 및 MBPS)를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-122">This scenario runs the [diskspd](https://github.com/Microsoft/diskspd) benchmark test (IOPS and MBPS) for all drives that are attached to the VM.</span></span> 

> [!Note]
> <span data-ttu-id="9518d-123">이 시나리오는 시스템에 영향을 줄 수 있으므로 라이브 프로덕션 시스템에서 실행하면 안됩니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-123">This scenario can affect the system and shouldn’t be run on a live production system.</span></span> <span data-ttu-id="9518d-124">필요한 경우 문제가 발생하지 않도록 전용 유지 관리 창에서 이 시나리오를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-124">If necessary, run this scenario in a dedicated maintenance window to avoid any problems.</span></span> <span data-ttu-id="9518d-125">추적 또는 벤치마크 테스트로 인해 워크로드가 증가하면 VM 성능이 저하될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-125">An increased workload that is caused by a trace or benchmark test could adversely affect the performance of your VM.</span></span>
>

### <a name="general-vm-slow-analysis"></a><span data-ttu-id="9518d-126">일반 VM 저속 분석</span><span class="sxs-lookup"><span data-stu-id="9518d-126">General VM Slow analysis</span></span> 

<span data-ttu-id="9518d-127">이 시나리오에서는 Generalcounters.txt 파일에 지정된 카운터를 사용하여 [성능 카운터](https://msdn.microsoft.com/library/windows/desktop/aa373083(v=vs.85).aspx) 추적을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-127">This scenario runs a [performance counter](https://msdn.microsoft.com/library/windows/desktop/aa373083(v=vs.85).aspx) trace by using the counters that are specified in the Generalcounters.txt file.</span></span> <span data-ttu-id="9518d-128">VM이 SQL Server를 실행하는 서버로 식별되면 Sqlcounters.txt 파일에 있는 카운터를 사용하여 성능 카운터 추적을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-128">If the VM is identified as a server that is running SQL Server, it runs a performance counter trace by using the counters that are found in the Sqlcounters.txt file.</span></span> <span data-ttu-id="9518d-129">또한 성능 진단 데이터도 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-129">It also includes Performance Diagnostics data.</span></span>

### <a name="vm-slow-analysis-and-benchmark"></a><span data-ttu-id="9518d-130">VM 저속 분석 및 벤치마크</span><span class="sxs-lookup"><span data-stu-id="9518d-130">VM Slow analysis and benchmark</span></span>

<span data-ttu-id="9518d-131">이 시나리오에서는 [성능 카운터](https://msdn.microsoft.com/library/windows/desktop/aa373083(v=vs.85).aspx) 추적을 실행한 다음 [diskspd](https://github.com/Microsoft/diskspd) 벤치마크 테스트를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-131">This scenario runs a [performance counter](https://msdn.microsoft.com/library/windows/desktop/aa373083(v=vs.85).aspx) trace that is followed by a [diskspd](https://github.com/Microsoft/diskspd) benchmark test.</span></span> 

> [!Note]
> <span data-ttu-id="9518d-132">이 시나리오는 시스템에 영향을 줄 수 있으므로 라이브 프로덕션 시스템에서 실행하면 안됩니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-132">This scenario can affect the system and shouldn’t be run on a live production system.</span></span> <span data-ttu-id="9518d-133">필요한 경우 문제가 발생하지 않도록 전용 유지 관리 창에서 이 시나리오를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-133">If necessary, run this scenario in a dedicated maintenance window to avoid any problems.</span></span> <span data-ttu-id="9518d-134">추적 또는 벤치마크 테스트로 인해 워크로드가 증가하면 VM 성능이 저하될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-134">An increased workload that is caused by a trace or benchmark test could adversely affect the performance of your VM.</span></span>
>

### <a name="azure-files-analysis"></a><span data-ttu-id="9518d-135">Azure Files 분석</span><span class="sxs-lookup"><span data-stu-id="9518d-135">Azure Files analysis</span></span> 

<span data-ttu-id="9518d-136">이 시나리오에서는 네트워크 추적과 함께 특별한 성능 카운터 캡처를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-136">This scenario runs a special performance counter capture together with a network trace.</span></span> <span data-ttu-id="9518d-137">캡처에는 모든 "SMB 클라이언트 공유" 카운터가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-137">The capture includes all the "SMB Client Shares" counters.</span></span> <span data-ttu-id="9518d-138">다음은 캡처에 포함되는 몇 가지 주요 SMB 클라이언트 공유 성능 카운터입니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-138">The following are some key SMB client share performance counters that are part of the capture:</span></span>

| <span data-ttu-id="9518d-139">**형식**</span><span class="sxs-lookup"><span data-stu-id="9518d-139">**Type**</span></span>     | <span data-ttu-id="9518d-140">**SMB 클라이언트 공유 카운터**</span><span class="sxs-lookup"><span data-stu-id="9518d-140">**SMB client shares counter**</span></span> |
|--------------|-------------------------------|
| <span data-ttu-id="9518d-141">IOPS</span><span class="sxs-lookup"><span data-stu-id="9518d-141">IOPS</span></span>         | <span data-ttu-id="9518d-142">데이터 요청 수/초</span><span class="sxs-lookup"><span data-stu-id="9518d-142">Data Requests/sec</span></span>             |
|              | <span data-ttu-id="9518d-143">읽기 요청 수/초</span><span class="sxs-lookup"><span data-stu-id="9518d-143">Read Requests/sec</span></span>             |
|              | <span data-ttu-id="9518d-144">쓰기 요청 수/초</span><span class="sxs-lookup"><span data-stu-id="9518d-144">Write Requests/sec</span></span>            |
| <span data-ttu-id="9518d-145">대기 시간</span><span class="sxs-lookup"><span data-stu-id="9518d-145">Latency</span></span>      | <span data-ttu-id="9518d-146">Avg. 초/데이터 요청</span><span class="sxs-lookup"><span data-stu-id="9518d-146">Avg. sec/Data Request</span></span>         |
|              | <span data-ttu-id="9518d-147">평균 초/읽기</span><span class="sxs-lookup"><span data-stu-id="9518d-147">Avg. sec/Read</span></span>                 |
|              | <span data-ttu-id="9518d-148">평균 sec/Write</span><span class="sxs-lookup"><span data-stu-id="9518d-148">Avg. sec/Write</span></span>                |
| <span data-ttu-id="9518d-149">IO 크기</span><span class="sxs-lookup"><span data-stu-id="9518d-149">IO Size</span></span>      | <span data-ttu-id="9518d-150">평균 바이트 수/데이터 요청</span><span class="sxs-lookup"><span data-stu-id="9518d-150">Avg. Bytes/Data Request</span></span>       |
|              | <span data-ttu-id="9518d-151">평균 바이트 수/읽기</span><span class="sxs-lookup"><span data-stu-id="9518d-151">Avg. Bytes/Read</span></span>               |
|              | <span data-ttu-id="9518d-152">평균 바이트 수/쓰기</span><span class="sxs-lookup"><span data-stu-id="9518d-152">Avg. Bytes/Write</span></span>              |
| <span data-ttu-id="9518d-153">처리량</span><span class="sxs-lookup"><span data-stu-id="9518d-153">Throughput</span></span>   | <span data-ttu-id="9518d-154">데이터 바이트 수/쓰기</span><span class="sxs-lookup"><span data-stu-id="9518d-154">Data Bytes/sec</span></span>                |
|              | <span data-ttu-id="9518d-155">읽기 바이트 수/초</span><span class="sxs-lookup"><span data-stu-id="9518d-155">Read Bytes/sec</span></span>                |
|              | <span data-ttu-id="9518d-156">쓰기 바이트 수/초</span><span class="sxs-lookup"><span data-stu-id="9518d-156">Write Bytes/sec</span></span>               |
| <span data-ttu-id="9518d-157">큐 길이</span><span class="sxs-lookup"><span data-stu-id="9518d-157">Queue Length</span></span> | <span data-ttu-id="9518d-158">평균 읽기 큐 길이</span><span class="sxs-lookup"><span data-stu-id="9518d-158">Avg. Read Queue Length</span></span>        |
|              | <span data-ttu-id="9518d-159">평균 쓰기 큐 길이</span><span class="sxs-lookup"><span data-stu-id="9518d-159">Avg. Write Queue Length</span></span>       |
|              | <span data-ttu-id="9518d-160">평균 데이터 큐 길이</span><span class="sxs-lookup"><span data-stu-id="9518d-160">Avg. Data Queue Length</span></span>        |

### <a name="custom-configuration"></a><span data-ttu-id="9518d-161">사용자 지정 구성</span><span class="sxs-lookup"><span data-stu-id="9518d-161">Custom configuration</span></span> 

<span data-ttu-id="9518d-162">사용자 지정 구성을 실행하면 서로 다른 추적을 선택한 개수에 따라 모든 추적(성능 진단, 성능 카운터, xperf, 네트워크, storport)이 병렬로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-162">When you run a custom configuration, you are running all traces (performance diagnostics, performance counter, xperf, network, storport) in parallel, depending how many different traces are selected.</span></span> <span data-ttu-id="9518d-163">추적이 완료되면 도구에서 diskspd 벤치마크(선택한 경우)를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-163">After tracing is completed, the tool runs the diskspd benchmark, if it is selected.</span></span> 

> [!Note]
> <span data-ttu-id="9518d-164">이 시나리오는 시스템에 영향을 줄 수 있으므로 라이브 프로덕션 시스템에서 실행하면 안됩니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-164">This scenario can affect the system and shouldn’t be run on a live production system.</span></span> <span data-ttu-id="9518d-165">필요한 경우 문제가 발생하지 않도록 전용 유지 관리 창에서 이 시나리오를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-165">If necessary, run this scenario in a dedicated maintenance window to avoid any problems.</span></span> <span data-ttu-id="9518d-166">추적 또는 벤치마크 테스트로 인해 워크로드가 증가하면 VM 성능이 저하될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-166">An increased workload that is caused by a trace or benchmark test could adversely affect the performance of your VM.</span></span>
>

## <a name="what-kind-of-information-is-collected-by-the-script"></a><span data-ttu-id="9518d-167">스크립트에서 수집하는 정보 유형</span><span class="sxs-lookup"><span data-stu-id="9518d-167">What kind of information is collected by the script?</span></span>

<span data-ttu-id="9518d-168">사용된 성능 시나리오에 따라 Windows VM, 디스크 또는 저장소 풀 구성, 성능 카운터, 로그 및 다양한 추적과 관련된 정보가 수집됩니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-168">Information about Windows VM, disks or storage pools configuration, performance counters, logs and various traces are collected depending on the performance scenario used:</span></span>

|<span data-ttu-id="9518d-169">수집되는 데이터</span><span class="sxs-lookup"><span data-stu-id="9518d-169">Data collected</span></span>                              |  |  | <span data-ttu-id="9518d-170">성능 시나리오</span><span class="sxs-lookup"><span data-stu-id="9518d-170">Performance Scenarios</span></span> |  |  | |
|----------------------------------|----------------------------|------------------------------------|--------------------------|--------------------------------|----------------------|----------------------|
|                              | <span data-ttu-id="9518d-171">디스크 구성 수집</span><span class="sxs-lookup"><span data-stu-id="9518d-171">Collect disk Configuration</span></span> | <span data-ttu-id="9518d-172">벤치마크/저장소 성능 테스트</span><span class="sxs-lookup"><span data-stu-id="9518d-172">Benchmark/Storage Performance test</span></span> | <span data-ttu-id="9518d-173">일반 VM 저속 분석</span><span class="sxs-lookup"><span data-stu-id="9518d-173">General VM Slow analysis</span></span> | <span data-ttu-id="9518d-174">VM 저속 분석 및 벤치마크</span><span class="sxs-lookup"><span data-stu-id="9518d-174">VM Slow analysis and benchmark</span></span> | <span data-ttu-id="9518d-175">Azure Files 분석</span><span class="sxs-lookup"><span data-stu-id="9518d-175">Azure Files analysis</span></span> | <span data-ttu-id="9518d-176">사용자 지정 구성</span><span class="sxs-lookup"><span data-stu-id="9518d-176">Custom configuration</span></span> |
| <span data-ttu-id="9518d-177">이벤트 로그의 정보</span><span class="sxs-lookup"><span data-stu-id="9518d-177">Information from Event logs</span></span>      | <span data-ttu-id="9518d-178">예</span><span class="sxs-lookup"><span data-stu-id="9518d-178">Yes</span></span>                        | <span data-ttu-id="9518d-179">예</span><span class="sxs-lookup"><span data-stu-id="9518d-179">Yes</span></span>                                | <span data-ttu-id="9518d-180">예</span><span class="sxs-lookup"><span data-stu-id="9518d-180">Yes</span></span>                      | <span data-ttu-id="9518d-181">예</span><span class="sxs-lookup"><span data-stu-id="9518d-181">Yes</span></span>                            | <span data-ttu-id="9518d-182">예</span><span class="sxs-lookup"><span data-stu-id="9518d-182">Yes</span></span>                  | <span data-ttu-id="9518d-183">예</span><span class="sxs-lookup"><span data-stu-id="9518d-183">Yes</span></span>                  |
| <span data-ttu-id="9518d-184">시스템 정보</span><span class="sxs-lookup"><span data-stu-id="9518d-184">System information</span></span>               | <span data-ttu-id="9518d-185">예</span><span class="sxs-lookup"><span data-stu-id="9518d-185">Yes</span></span>                        | <span data-ttu-id="9518d-186">예</span><span class="sxs-lookup"><span data-stu-id="9518d-186">Yes</span></span>                                | <span data-ttu-id="9518d-187">예</span><span class="sxs-lookup"><span data-stu-id="9518d-187">Yes</span></span>                      | <span data-ttu-id="9518d-188">예</span><span class="sxs-lookup"><span data-stu-id="9518d-188">Yes</span></span>                            | <span data-ttu-id="9518d-189">예</span><span class="sxs-lookup"><span data-stu-id="9518d-189">Yes</span></span>                  | <span data-ttu-id="9518d-190">예</span><span class="sxs-lookup"><span data-stu-id="9518d-190">Yes</span></span>                  |
| <span data-ttu-id="9518d-191">볼륨 매핑</span><span class="sxs-lookup"><span data-stu-id="9518d-191">Volume Map</span></span>                       | <span data-ttu-id="9518d-192">예</span><span class="sxs-lookup"><span data-stu-id="9518d-192">Yes</span></span>                        | <span data-ttu-id="9518d-193">예</span><span class="sxs-lookup"><span data-stu-id="9518d-193">Yes</span></span>                                | <span data-ttu-id="9518d-194">예</span><span class="sxs-lookup"><span data-stu-id="9518d-194">Yes</span></span>                      | <span data-ttu-id="9518d-195">예</span><span class="sxs-lookup"><span data-stu-id="9518d-195">Yes</span></span>                            | <span data-ttu-id="9518d-196">예</span><span class="sxs-lookup"><span data-stu-id="9518d-196">Yes</span></span>                  | <span data-ttu-id="9518d-197">예</span><span class="sxs-lookup"><span data-stu-id="9518d-197">Yes</span></span>                  |
| <span data-ttu-id="9518d-198">디스크 매핑</span><span class="sxs-lookup"><span data-stu-id="9518d-198">Disk Map</span></span>                         | <span data-ttu-id="9518d-199">예</span><span class="sxs-lookup"><span data-stu-id="9518d-199">Yes</span></span>                        | <span data-ttu-id="9518d-200">예</span><span class="sxs-lookup"><span data-stu-id="9518d-200">Yes</span></span>                                | <span data-ttu-id="9518d-201">예</span><span class="sxs-lookup"><span data-stu-id="9518d-201">Yes</span></span>                      | <span data-ttu-id="9518d-202">예</span><span class="sxs-lookup"><span data-stu-id="9518d-202">Yes</span></span>                            | <span data-ttu-id="9518d-203">예</span><span class="sxs-lookup"><span data-stu-id="9518d-203">Yes</span></span>                  | <span data-ttu-id="9518d-204">예</span><span class="sxs-lookup"><span data-stu-id="9518d-204">Yes</span></span>                  |
| <span data-ttu-id="9518d-205">실행 중인 작업</span><span class="sxs-lookup"><span data-stu-id="9518d-205">Running Tasks</span></span>                    | <span data-ttu-id="9518d-206">예</span><span class="sxs-lookup"><span data-stu-id="9518d-206">Yes</span></span>                        | <span data-ttu-id="9518d-207">예</span><span class="sxs-lookup"><span data-stu-id="9518d-207">Yes</span></span>                                | <span data-ttu-id="9518d-208">예</span><span class="sxs-lookup"><span data-stu-id="9518d-208">Yes</span></span>                      | <span data-ttu-id="9518d-209">예</span><span class="sxs-lookup"><span data-stu-id="9518d-209">Yes</span></span>                            | <span data-ttu-id="9518d-210">예</span><span class="sxs-lookup"><span data-stu-id="9518d-210">Yes</span></span>                  | <span data-ttu-id="9518d-211">예</span><span class="sxs-lookup"><span data-stu-id="9518d-211">Yes</span></span>                  |
| <span data-ttu-id="9518d-212">저장소 안정성 카운터</span><span class="sxs-lookup"><span data-stu-id="9518d-212">Storage Reliability Counters</span></span>     | <span data-ttu-id="9518d-213">예</span><span class="sxs-lookup"><span data-stu-id="9518d-213">Yes</span></span>                        | <span data-ttu-id="9518d-214">예</span><span class="sxs-lookup"><span data-stu-id="9518d-214">Yes</span></span>                                | <span data-ttu-id="9518d-215">예</span><span class="sxs-lookup"><span data-stu-id="9518d-215">Yes</span></span>                      | <span data-ttu-id="9518d-216">예</span><span class="sxs-lookup"><span data-stu-id="9518d-216">Yes</span></span>                            | <span data-ttu-id="9518d-217">예</span><span class="sxs-lookup"><span data-stu-id="9518d-217">Yes</span></span>                  | <span data-ttu-id="9518d-218">예</span><span class="sxs-lookup"><span data-stu-id="9518d-218">Yes</span></span>                  |
| <span data-ttu-id="9518d-219">저장소 정보</span><span class="sxs-lookup"><span data-stu-id="9518d-219">Storage information</span></span>              | <span data-ttu-id="9518d-220">예</span><span class="sxs-lookup"><span data-stu-id="9518d-220">Yes</span></span>                        | <span data-ttu-id="9518d-221">예</span><span class="sxs-lookup"><span data-stu-id="9518d-221">Yes</span></span>                                | <span data-ttu-id="9518d-222">예</span><span class="sxs-lookup"><span data-stu-id="9518d-222">Yes</span></span>                      | <span data-ttu-id="9518d-223">예</span><span class="sxs-lookup"><span data-stu-id="9518d-223">Yes</span></span>                            | <span data-ttu-id="9518d-224">예</span><span class="sxs-lookup"><span data-stu-id="9518d-224">Yes</span></span>                  | <span data-ttu-id="9518d-225">예</span><span class="sxs-lookup"><span data-stu-id="9518d-225">Yes</span></span>                  |
| <span data-ttu-id="9518d-226">Fsutil 출력</span><span class="sxs-lookup"><span data-stu-id="9518d-226">Fsutil output</span></span>                    | <span data-ttu-id="9518d-227">예</span><span class="sxs-lookup"><span data-stu-id="9518d-227">Yes</span></span>                        | <span data-ttu-id="9518d-228">예</span><span class="sxs-lookup"><span data-stu-id="9518d-228">Yes</span></span>                                | <span data-ttu-id="9518d-229">예</span><span class="sxs-lookup"><span data-stu-id="9518d-229">Yes</span></span>                      | <span data-ttu-id="9518d-230">예</span><span class="sxs-lookup"><span data-stu-id="9518d-230">Yes</span></span>                            | <span data-ttu-id="9518d-231">예</span><span class="sxs-lookup"><span data-stu-id="9518d-231">Yes</span></span>                  | <span data-ttu-id="9518d-232">예</span><span class="sxs-lookup"><span data-stu-id="9518d-232">Yes</span></span>                  |
| <span data-ttu-id="9518d-233">필터 드라이버 정보</span><span class="sxs-lookup"><span data-stu-id="9518d-233">Filter Driver info</span></span>               | <span data-ttu-id="9518d-234">예</span><span class="sxs-lookup"><span data-stu-id="9518d-234">Yes</span></span>                        | <span data-ttu-id="9518d-235">예</span><span class="sxs-lookup"><span data-stu-id="9518d-235">Yes</span></span>                                | <span data-ttu-id="9518d-236">예</span><span class="sxs-lookup"><span data-stu-id="9518d-236">Yes</span></span>                      | <span data-ttu-id="9518d-237">예</span><span class="sxs-lookup"><span data-stu-id="9518d-237">Yes</span></span>                            | <span data-ttu-id="9518d-238">예</span><span class="sxs-lookup"><span data-stu-id="9518d-238">Yes</span></span>                  | <span data-ttu-id="9518d-239">예</span><span class="sxs-lookup"><span data-stu-id="9518d-239">Yes</span></span>                  |
| <span data-ttu-id="9518d-240">Netstat 출력</span><span class="sxs-lookup"><span data-stu-id="9518d-240">Netstat output</span></span>                   | <span data-ttu-id="9518d-241">예</span><span class="sxs-lookup"><span data-stu-id="9518d-241">Yes</span></span>                        | <span data-ttu-id="9518d-242">예</span><span class="sxs-lookup"><span data-stu-id="9518d-242">Yes</span></span>                                | <span data-ttu-id="9518d-243">예</span><span class="sxs-lookup"><span data-stu-id="9518d-243">Yes</span></span>                      | <span data-ttu-id="9518d-244">예</span><span class="sxs-lookup"><span data-stu-id="9518d-244">Yes</span></span>                            | <span data-ttu-id="9518d-245">예</span><span class="sxs-lookup"><span data-stu-id="9518d-245">Yes</span></span>                  | <span data-ttu-id="9518d-246">예</span><span class="sxs-lookup"><span data-stu-id="9518d-246">Yes</span></span>                  |
| <span data-ttu-id="9518d-247">네트워크 구성</span><span class="sxs-lookup"><span data-stu-id="9518d-247">Network configuration</span></span>            | <span data-ttu-id="9518d-248">예</span><span class="sxs-lookup"><span data-stu-id="9518d-248">Yes</span></span>                        | <span data-ttu-id="9518d-249">예</span><span class="sxs-lookup"><span data-stu-id="9518d-249">Yes</span></span>                                | <span data-ttu-id="9518d-250">예</span><span class="sxs-lookup"><span data-stu-id="9518d-250">Yes</span></span>                      | <span data-ttu-id="9518d-251">예</span><span class="sxs-lookup"><span data-stu-id="9518d-251">Yes</span></span>                            | <span data-ttu-id="9518d-252">예</span><span class="sxs-lookup"><span data-stu-id="9518d-252">Yes</span></span>                  | <span data-ttu-id="9518d-253">예</span><span class="sxs-lookup"><span data-stu-id="9518d-253">Yes</span></span>                  |
| <span data-ttu-id="9518d-254">방화벽 구성</span><span class="sxs-lookup"><span data-stu-id="9518d-254">Firewall configuration</span></span>           | <span data-ttu-id="9518d-255">예</span><span class="sxs-lookup"><span data-stu-id="9518d-255">Yes</span></span>                        | <span data-ttu-id="9518d-256">예</span><span class="sxs-lookup"><span data-stu-id="9518d-256">Yes</span></span>                                | <span data-ttu-id="9518d-257">예</span><span class="sxs-lookup"><span data-stu-id="9518d-257">Yes</span></span>                      | <span data-ttu-id="9518d-258">예</span><span class="sxs-lookup"><span data-stu-id="9518d-258">Yes</span></span>                            | <span data-ttu-id="9518d-259">예</span><span class="sxs-lookup"><span data-stu-id="9518d-259">Yes</span></span>                  | <span data-ttu-id="9518d-260">예</span><span class="sxs-lookup"><span data-stu-id="9518d-260">Yes</span></span>                  |
| <span data-ttu-id="9518d-261">SQL Server 구성</span><span class="sxs-lookup"><span data-stu-id="9518d-261">SQL Server configuration</span></span>         | <span data-ttu-id="9518d-262">예</span><span class="sxs-lookup"><span data-stu-id="9518d-262">Yes</span></span>                        | <span data-ttu-id="9518d-263">예</span><span class="sxs-lookup"><span data-stu-id="9518d-263">Yes</span></span>                                | <span data-ttu-id="9518d-264">예</span><span class="sxs-lookup"><span data-stu-id="9518d-264">Yes</span></span>                      | <span data-ttu-id="9518d-265">예</span><span class="sxs-lookup"><span data-stu-id="9518d-265">Yes</span></span>                            | <span data-ttu-id="9518d-266">예</span><span class="sxs-lookup"><span data-stu-id="9518d-266">Yes</span></span>                  | <span data-ttu-id="9518d-267">예</span><span class="sxs-lookup"><span data-stu-id="9518d-267">Yes</span></span>                  |
| <span data-ttu-id="9518d-268">성능 진단 추적 *</span><span class="sxs-lookup"><span data-stu-id="9518d-268">Performance Diagnostics Traces *</span></span> |                            |                                    | <span data-ttu-id="9518d-269">예</span><span class="sxs-lookup"><span data-stu-id="9518d-269">Yes</span></span>                      |                                |                      | <span data-ttu-id="9518d-270">예</span><span class="sxs-lookup"><span data-stu-id="9518d-270">Yes</span></span>                  |
| <span data-ttu-id="9518d-271">성능 카운터 추적 **</span><span class="sxs-lookup"><span data-stu-id="9518d-271">Performance counter Trace **</span></span>     |                            |                                    |                          |                                |                      | <span data-ttu-id="9518d-272">예</span><span class="sxs-lookup"><span data-stu-id="9518d-272">Yes</span></span>                  |
| <span data-ttu-id="9518d-273">SMB 카운터 추적 **</span><span class="sxs-lookup"><span data-stu-id="9518d-273">SMB counter Trace **</span></span>             |                            |                                    |                          |                                | <span data-ttu-id="9518d-274">예</span><span class="sxs-lookup"><span data-stu-id="9518d-274">Yes</span></span>                  |                      |
| <span data-ttu-id="9518d-275">SQL Server 카운터 추적 **</span><span class="sxs-lookup"><span data-stu-id="9518d-275">SQL Server counter Trace **</span></span>      |                            |                                    |                          |                                |                      | <span data-ttu-id="9518d-276">예</span><span class="sxs-lookup"><span data-stu-id="9518d-276">Yes</span></span>                  |
| <span data-ttu-id="9518d-277">XPerf 추적</span><span class="sxs-lookup"><span data-stu-id="9518d-277">XPerf Trace</span></span>                      |                            |                                    |                          |                                |                      | <span data-ttu-id="9518d-278">예</span><span class="sxs-lookup"><span data-stu-id="9518d-278">Yes</span></span>                  |
| <span data-ttu-id="9518d-279">StorPort 추적</span><span class="sxs-lookup"><span data-stu-id="9518d-279">StorPort Trace</span></span>                   |                            |                                    |                          |                                |                      | <span data-ttu-id="9518d-280">예</span><span class="sxs-lookup"><span data-stu-id="9518d-280">Yes</span></span>                  |
| <span data-ttu-id="9518d-281">네트워크 추적</span><span class="sxs-lookup"><span data-stu-id="9518d-281">Network Trace</span></span>                    |                            |                                    |                          |                                | <span data-ttu-id="9518d-282">예</span><span class="sxs-lookup"><span data-stu-id="9518d-282">Yes</span></span>                  | <span data-ttu-id="9518d-283">예</span><span class="sxs-lookup"><span data-stu-id="9518d-283">Yes</span></span>                  |
| <span data-ttu-id="9518d-284">Diskspd 벤치마크 추적 ***</span><span class="sxs-lookup"><span data-stu-id="9518d-284">Diskspd Benchmark trace ***</span></span>      |                            | <span data-ttu-id="9518d-285">예</span><span class="sxs-lookup"><span data-stu-id="9518d-285">Yes</span></span>                                |                          | <span data-ttu-id="9518d-286">예</span><span class="sxs-lookup"><span data-stu-id="9518d-286">Yes</span></span>                            |                      |                      |
|       |                            |                         |                                                   |                      |                      |

### <a name="performance-diagnostics-trace-"></a><span data-ttu-id="9518d-287">성능 진단 추적 (*)</span><span class="sxs-lookup"><span data-stu-id="9518d-287">Performance Diagnostics trace (*)</span></span>

<span data-ttu-id="9518d-288">백그라운드에서 규칙 기반 엔진을 실행하여 데이터를 수집하고 지속적인 성능 문제를 진단합니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-288">Runs a rule-based engine in the background to collect data and diagnose ongoing performance issues.</span></span> <span data-ttu-id="9518d-289">현재 지원되는 규칙은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-289">The following rules are currently supported:</span></span>

- <span data-ttu-id="9518d-290">HighCpuUsage 규칙: 높은 CPU 사용량 기간을 검색하고 해당 기간 동안의 최고 CPU 사용량 소비자를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-290">HighCpuUsage rule: Detects high CPU usage periods and shows the top CPU usage consumers during those periods.</span></span>
- <span data-ttu-id="9518d-291">HighDiskUsage 규칙: 실제 디스크에 대한 높은 디스크 사용량 기간을 검색하고 해당 기간 동안의 최고 디스크 사용량 소비자를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-291">HighDiskUsage rule: Detects high disk usage periods on physical disks and shows the top disk usage consumers during those periods.</span></span>
- <span data-ttu-id="9518d-292">HighResolutionDiskMetric 규칙: 각 실제 디스크에 대한 50밀리초당 IOPS, 처리량 및 IO 대기 시간 메트릭을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-292">HighResolutionDiskMetric rule: Shows IOPS, throughput and IO latency metrics per 50 milliseconds for each physical disk.</span></span> <span data-ttu-id="9518d-293">디스크 제한 기간을 빠르게 식별하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-293">It helps to quickly identify disk throttling periods.</span></span>
- <span data-ttu-id="9518d-294">HighMemoryUsage 규칙: 높은 메모리 사용 기간을 검색하고 해당 기간 동안의 최고 메모리 사용량 소비자를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-294">HighMemoryUsage rule: Detects high memory usage periods, and shows the top memory usage consumers during those periods.</span></span>

> [!NOTE] 
> <span data-ttu-id="9518d-295">현재 .NET Framework 3.5 이상 버전이 포함된 Windows 버전이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-295">Currently, Windows versions that include the .NET Framework 3.5 or later versions are supported.</span></span>

### <a name="performance-counter-trace-"></a><span data-ttu-id="9518d-296">성능 카운터 추적 (**)</span><span class="sxs-lookup"><span data-stu-id="9518d-296">Performance Counter trace (**)</span></span>

<span data-ttu-id="9518d-297">다음 성능 카운터를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-297">Collects the following Performance Counters:</span></span>

- <span data-ttu-id="9518d-298">\Process, \Processor, \Memory, \Thread, \PhysicalDisk, \LogicalDisk</span><span class="sxs-lookup"><span data-stu-id="9518d-298">\Process, \Processor, \Memory, \Thread, \PhysicalDisk, \LogicalDisk</span></span>
- <span data-ttu-id="9518d-299">\Cache\Dirty Pages, \Cache\Lazy Write Flushes/sec, \Server\Pool Nonpaged, Failures, \Server\Pool Paged Failures</span><span class="sxs-lookup"><span data-stu-id="9518d-299">\Cache\Dirty Pages, \Cache\Lazy Write Flushes/sec, \Server\Pool Nonpaged, Failures, \Server\Pool Paged Failures</span></span>
- <span data-ttu-id="9518d-300">\Network Interface, \IPv4\Datagrams, \IPv6\Datagrams, \TCPv4\Segments, \TCPv6\Segments, \Network Adapter, \WFPv4\Packets, \WFPv6\Packets, \UDPv4\Datagrams, \UDPv6\Datagrams, \TCPv4\Connection, \TCPv6\Connection, \Network QoS Policy\Packets, \Per Processor Network Interface Card Activity, \Microsoft Winsock BSP 중에서 선택한 카운터</span><span class="sxs-lookup"><span data-stu-id="9518d-300">Selected counters under \Network Interface, \IPv4\Datagrams, \IPv6\Datagrams, \TCPv4\Segments, \TCPv6\Segments,  \Network Adapter, \WFPv4\Packets, \WFPv6\Packets, \UDPv4\Datagrams, \UDPv6\Datagrams, \TCPv4\Connection, \TCPv6\Connection, \Network QoS Policy\Packets, \Per Processor Network Interface Card Activity, \Microsoft Winsock BSP</span></span>

#### <a name="for-sql-server-instances"></a><span data-ttu-id="9518d-301">SQL Server 인스턴스의 경우</span><span class="sxs-lookup"><span data-stu-id="9518d-301">For SQL Server instances</span></span>
- <span data-ttu-id="9518d-302">\SQL Server:Buffer Manager, \SQLServer:Resource Pool Stats, \SQLServer:SQL Statistics\\</span><span class="sxs-lookup"><span data-stu-id="9518d-302">\SQL Server:Buffer Manager, \SQLServer:Resource Pool Stats, \SQLServer:SQL Statistics\\</span></span>
- <span data-ttu-id="9518d-303">\SQLServer:Locks, \SQLServer:General, Statistics</span><span class="sxs-lookup"><span data-stu-id="9518d-303">\SQLServer:Locks, \SQLServer:General, Statistics</span></span>
- <span data-ttu-id="9518d-304">\SQLServer:Access Methods</span><span class="sxs-lookup"><span data-stu-id="9518d-304">\SQLServer:Access Methods</span></span>

#### <a name="for-azure-files"></a><span data-ttu-id="9518d-305">Azure Files의 경우</span><span class="sxs-lookup"><span data-stu-id="9518d-305">For Azure Files</span></span>
<span data-ttu-id="9518d-306">\SMB Client Shares</span><span class="sxs-lookup"><span data-stu-id="9518d-306">\SMB Client Shares</span></span>

### <a name="diskspd-benchmark-trace-"></a><span data-ttu-id="9518d-307">Diskspd 벤치마크 추적 (***)</span><span class="sxs-lookup"><span data-stu-id="9518d-307">Diskspd Benchmark trace (***)</span></span>
<span data-ttu-id="9518d-308">Diskspd IO 워크로드 테스트[OS 디스크(쓰기) 및 풀 드라이브(읽기/쓰기)]</span><span class="sxs-lookup"><span data-stu-id="9518d-308">Diskspd IO workload tests [OS Disk (write) and pool drives (read/write)]</span></span>

## <a name="run-the-perfinsights-on-your-vm"></a><span data-ttu-id="9518d-309">VM에서 PerfInsights 실행</span><span class="sxs-lookup"><span data-stu-id="9518d-309">Run the PerfInsights on your VM</span></span>

### <a name="what-do-i-have-to-know-before-i-run-the-script"></a><span data-ttu-id="9518d-310">스크립트를 실행하기 전에 알고 있어야 하는 사항</span><span class="sxs-lookup"><span data-stu-id="9518d-310">What do I have to know before I run the script?</span></span> 

<span data-ttu-id="9518d-311">**스크립트 요구 사항**</span><span class="sxs-lookup"><span data-stu-id="9518d-311">**Script requirements**</span></span>

1.  <span data-ttu-id="9518d-312">이 스크립트는 성능 문제가 있는 VM에서 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-312">This script must be run on the VM that has the performance issue.</span></span> 

2.  <span data-ttu-id="9518d-313">지원되는 OS: Windows Server 2008 R2, 2012, 2012 R2, 2016; Windows 8.1 및 Windows 10</span><span class="sxs-lookup"><span data-stu-id="9518d-313">The following OSes are supported: Windows Server 2008 R2, 2012, 2012 R2, 2016; Windows 8.1 and Windows 10.</span></span>

<span data-ttu-id="9518d-314">**프로덕션 VM에서 스크립트 실행 시 발생할 수 있는 문제**</span><span class="sxs-lookup"><span data-stu-id="9518d-314">**Possible issues when you run the script on production VMs:**</span></span>

1.  <span data-ttu-id="9518d-315">XPerf 또는 DiskSpd로 구성된 "벤치마크" 또는 "사용자 지정" 시나리오와 함께 스크립트를 사용하는 경우 VM의 성능이 저하될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-315">The script might adversely affect the performance of the VM when it is used together with the "Benchmark" or "Custom" scenario that is configured by using XPerf or DiskSpd.</span></span> <span data-ttu-id="9518d-316">따라서 프로덕션 환경에서 스크립트를 실행할 때는 주의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-316">Be careful when you run the script in a production environment.</span></span>

2.  <span data-ttu-id="9518d-317">DiskSpd로 구성된 "벤치마크" 또는 "사용자 지정" 시나리오와 함께 스크립트를 사용하는 경우 다른 백그라운드 활동이 테스트된 디스크의 I/O 워크로드를 방해하지 않는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-317">When you use the script together with the "Benchmark" or "Custom" scenario that is configured by using DiskSpd, make sure that no other background activity interferes with the I/O workload on the tested disks.</span></span>

3.  <span data-ttu-id="9518d-318">기본적으로 스크립트는 임시 저장소 드라이브를 사용하여 데이터를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-318">By default, the script uses the temporary storage drive to collect data.</span></span> <span data-ttu-id="9518d-319">추적을 더 오랫동안 사용하도록 유지하면 수집되는 데이터의 양이 적절할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-319">If tracing stays enabled for a longer time, the amount of data that is collected might be relevant.</span></span> <span data-ttu-id="9518d-320">이렇게 하면 임시 디스크의 공간 가용성을 낮출 수 있으므로 이 드라이브를 사용하는 모든 응용 프로그램에 영향을 미칩니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-320">This can reduce the availability of space on the temporary disk, therefore affecting any application that relies on this drive.</span></span>

### <a name="how-do-i-run-perfinsights"></a><span data-ttu-id="9518d-321">PerfInsights를 실행하는 방법</span><span class="sxs-lookup"><span data-stu-id="9518d-321">How do I run PerfInsights?</span></span> 

<span data-ttu-id="9518d-322">스크립트를 실행하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-322">To run the script, follow these steps:</span></span>

1. <span data-ttu-id="9518d-323">[PerfInsights.zip](http://aka.ms/perfinsightsdownload)을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-323">Download [PerfInsights.zip](http://aka.ms/perfinsightsdownload).</span></span>

2. <span data-ttu-id="9518d-324">PerfInsights.zip 파일의 차단을 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-324">Unblock the PerfInsights.zip file.</span></span> <span data-ttu-id="9518d-325">이렇게 하려면 PerfInsights.zip 파일을 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-325">To do this, right-click the PerfInsights.zip file, select **Properties**.</span></span> <span data-ttu-id="9518d-326">**일반** 탭에서 **차단 해제**를 선택한 다음 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-326">In the **General** tab, select **Unblock** and then select **OK**.</span></span> <span data-ttu-id="9518d-327">이렇게 하면 추가 보안을 요구하는 메시지가 표시되지 않고 스크립트가 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-327">This will make sure that the script runs without any additional security prompts.</span></span>  

    ![zip 파일 잠금 해제](media/how-to-use-perfInsights/unlock-file.png)

3.  <span data-ttu-id="9518d-329">압축된 PerfInsights.zip 파일을 임시 드라이브(기본적으로 D 드라이브)로 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-329">Expand the compressed PerfInsights.zip file into your temporary drive (by default, usually the D drive).</span></span> <span data-ttu-id="9518d-330">압축된 파일에는 다음 파일과 폴더가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-330">The compressed file should contain the following files and folders:</span></span>

    ![zip 폴더에 포함된 파일](media/how-to-use-perfInsights/file-folder.png)

4.  <span data-ttu-id="9518d-332">Windows PowerShell을 관리자로 연 다음 PerfInsights.ps1 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-332">Open Windows PowerShell as an administrator, and then run the PerfInsights.ps1 script.</span></span>

    ```
    cd <the path of PerfInsights folder >
    Powershell.exe -ExecutionPolicy UnRestricted -NoProfile -File .\\PerfInsights.ps1
    ```

    <span data-ttu-id="9518d-333">실행 정책을 변경할지 묻는 메시지가 표시되면 "y"를 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-333">You might have to enter "y" to if you are asked to confirm that you want to change the execution policy.</span></span>

    <span data-ttu-id="9518d-334">[고지 사항] 대화 상자에서는 Microsoft 지원 서비스와 진단 정보를 공유하는 옵션이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-334">In the Disclaimer dialog box, you are given the option to share diagnostic information with Microsoft Support.</span></span> <span data-ttu-id="9518d-335">계속하려면 사용권 계약에도 동의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-335">You must also consent to the license agreement to continue.</span></span> <span data-ttu-id="9518d-336">선택한 다음 **스크립트 실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-336">Make your selections, and then click **Run Script**.</span></span>

    ![고지 사항 상자](media/how-to-use-perfInsights/disclaimer.png)

5.  <span data-ttu-id="9518d-338">스크립트를 실행할 때 사례 번호(통계 용도)를 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-338">Submit the case number, if it is available, when you run the script (This is for our statistics).</span></span> <span data-ttu-id="9518d-339">그런 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-339">Then, click **OK**.</span></span>
    
    ![지원 ID 입력](media/how-to-use-perfInsights/enter-support-number.png)

6.  <span data-ttu-id="9518d-341">임시 저장소 드라이브를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-341">Select your temporary storage drive.</span></span> <span data-ttu-id="9518d-342">스크립트는 드라이브의 드라이브 문자를 자동으로 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-342">The Script can auto-detect the drive letter of the drive.</span></span> <span data-ttu-id="9518d-343">이 단계에서 문제가 발생하면 드라이브를 선택하라는 메시지가 표시될 수 있습니다(기본 드라이브: D).</span><span class="sxs-lookup"><span data-stu-id="9518d-343">If any problems occur in this stage, you might be prompted to select the drive (the default drive is D).</span></span> <span data-ttu-id="9518d-344">생성된 로그는 log\_collection 폴더에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-344">Generated logs are stored here in the log\_collection folder.</span></span> <span data-ttu-id="9518d-345">드라이브 문자를 입력하거나 그대로 둔 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-345">After you enter or accept the drive letter, click **OK**.</span></span>

    ![드라이브 입력](media/how-to-use-perfInsights/enter-drive.png)

7.  <span data-ttu-id="9518d-347">제공된 목록에서 문제 해결 시나리오를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-347">Select a troubleshooting scenario from the provided list.</span></span>

       ![지원 시나리오 선택](media/how-to-use-perfInsights/select-scenarios.png)

8.  <span data-ttu-id="9518d-349">UI 없이 PerfInsights를 실행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-349">You can also run PerfInsights without UI.</span></span>

    <span data-ttu-id="9518d-350">다음 명령에서는 UI 프롬프트 없이 30초 동안 "일반 VM 저속 분석" 문제 해결 시나리오를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-350">The following command runs the "General VM Slow analysis" troubleshooting scenario without a UI prompt or capture data for 30 seconds.</span></span> <span data-ttu-id="9518d-351">4단계에서 언급한 동일한 고지 사항 및 EULA에 동의하도록 요구하는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-351">It prompts you to consent to the same disclaimer and EULA that  are mentioned in step 4.</span></span>

        powershell.exe -ExecutionPolicy UnRestricted -NoProfile -Command ".\\PerfInsights.ps1 -NoGui -Scenario vmslow -TracingDuration 30"

    <span data-ttu-id="9518d-352">PerfInsights를 자동 모드로 실행하려면 **-AcceptDisclaimerAndShareDiagnostics** 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-352">If you want PerfInsights to run in silent mode, use the **-AcceptDisclaimerAndShareDiagnostics** parameter.</span></span> <span data-ttu-id="9518d-353">예를 들어 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-353">For example, use the following command:</span></span>

        powershell.exe -ExecutionPolicy UnRestricted -NoProfile -Command ".\\PerfInsights.ps1 -NoGui -Scenario vmslow -TracingDuration 30 -AcceptDisclaimerAndShareDiagnostics"

### <a name="how-do-i-troubleshoot-issues-while-running-the-script"></a><span data-ttu-id="9518d-354">스크립트를 실행하는 동안 문제를 해결하는 방법</span><span class="sxs-lookup"><span data-stu-id="9518d-354">How do I troubleshoot issues while running the script?</span></span>

<span data-ttu-id="9518d-355">스크립트가 비정상적으로 종료되면 다음과 같이 -Cleanup 스위치와 함께 스크립트를 실행하여 일관성이 없는 상태를 정리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-355">If the script terminates abnormally, you can clean up an inconsistent state by running the script together with the -Cleanup switch, as follows:</span></span>

    powershell.exe -ExecutionPolicy UnRestricted -NoProfile -Command ".\\PerfInsights.ps1 -Cleanup"

<span data-ttu-id="9518d-356">임시 드라이브를 자동 검색하는 중에 문제가 발생하면 드라이브를 선택하라는 메시지가 표시될 수 있습니다(기본 드라이브: D).</span><span class="sxs-lookup"><span data-stu-id="9518d-356">If any problems occur during the automatic detection of the temporary drive, you might be prompted to select the drive (the default drive is D).</span></span>

![드라이브 입력](media/how-to-use-perfInsights/enter-drive.png)

<span data-ttu-id="9518d-358">스크립트에서 유틸리티 도구를 제거하고 임시 폴더를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-358">The script uninstalls the utility tools and removes temporary folders.</span></span>

### <a name="troubleshooting-other-script-issues"></a><span data-ttu-id="9518d-359">기타 스크립트 문제 해결</span><span class="sxs-lookup"><span data-stu-id="9518d-359">Troubleshooting other script issues</span></span> 

<span data-ttu-id="9518d-360">스크립트를 실행할 때 문제가 발생하면 Ctrl+C를 눌러 스크립트 실행을 중단합니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-360">If any problems occur when you run the script, press Ctrl+C to interrupt the script execution.</span></span> <span data-ttu-id="9518d-361">임시 개체를 제거하려면 "비정상 종료 후 정리" 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9518d-361">To remove temporary objects, see the "Clean up after abnormal termination" section.</span></span>

<span data-ttu-id="9518d-362">여러 번 시도한 후에도 스크립트 오류가 계속 발생하면 시작할 때 "-Debug" 매개 변수 옵션을 사용하여 "디버그 모드"에서 스크립트를 실행하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-362">If you continue to experience script failure even after several attempts, we recommend that you run the script in "debug mode" by using the "-Debug" parameter option on startup.</span></span>

<span data-ttu-id="9518d-363">오류가 발생한 후에는 PowerShell 콘솔의 전체 출력을 복사하여 문제를 해결하기 위해 도움을 주는 Microsoft 지원 담당자에게 보내주세요.</span><span class="sxs-lookup"><span data-stu-id="9518d-363">After the failure occurs, copy the full output of the PowerShell console, and send it to the Microsoft Support agent who is assisting you to help troubleshoot the problem.</span></span>

### <a name="how-do-i-run-the-script-in-custom-configuration-mode"></a><span data-ttu-id="9518d-364">스크립트를 사용자 지정 구성 모드로 실행하는 방법</span><span class="sxs-lookup"><span data-stu-id="9518d-364">How do I run the script in custom configuration mode?</span></span>

<span data-ttu-id="9518d-365">**사용자 지정** 구성을 선택하면 여러 추적을 동시에 사용할 수 있습니다(Shift 키로 다중 선택).</span><span class="sxs-lookup"><span data-stu-id="9518d-365">By selecting the **Custom** configuration, you can enable several traces in parallel (use Shift to multi-select):</span></span>

![시나리오 선택](media/how-to-use-perfInsights/select-scenario.png)

<span data-ttu-id="9518d-367">성능 진단, 성능 카운터 추적, XPerf 추적, 네트워크 추적 또는 Storport 추적 시나리오를 선택하는 경우 대화 상자의 지침을 따르고, 추적을 시작한 후에 성능 저하 문제를 재현합니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-367">When you select the Performance Diagnostics, Performance Counter Trace, XPerf Trace, Network Trace, or Storport Trace scenarios, follow the instructions in the dialog boxes, and try to reproduce the slow performance issue after you start the traces.</span></span>

<span data-ttu-id="9518d-368">다음 대화 상자에서 추적을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-368">The following dialog box lets you start a trace:</span></span>

![추적 시작](media/how-to-use-perfInsights/start-trace-message.png)

<span data-ttu-id="9518d-370">추적을 중지하려면 두 번째 대화 상자에서 명령을 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-370">To stop the traces, you have to confirm the command in a second dialog box.</span></span>

<span data-ttu-id="9518d-371">![추적 중지](media/how-to-use-perfInsights/stop-trace-message.png)
![추적 중지](media/how-to-use-perfInsights/ok-trace-message.png)</span><span class="sxs-lookup"><span data-stu-id="9518d-371">![stop-trace](media/how-to-use-perfInsights/stop-trace-message.png)
![stop-trace](media/how-to-use-perfInsights/ok-trace-message.png)</span></span>

<span data-ttu-id="9518d-372">추적 또는 작업이 완료되면 D:\\log\_collection(또는 임시 드라이브)에 **CollectedData\_yyyy-MM-dd\_hh\_mm\_ss.zip**이라는 새 파일이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-372">When the traces or operations are completed, a new file is generated in D:\\log\_collection (or the temporary drive) that is named **CollectedData\_yyyy-MM-dd\_hh\_mm\_ss.zip.**</span></span> <span data-ttu-id="9518d-373">이 파일은 분석을 위해 지원 담당자에게 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-373">You can send this file to the Support agent for analysis.</span></span>

## <a name="review-the-diagnostics-report-created-by-perfinsights"></a><span data-ttu-id="9518d-374">PerfInsights에서 만든 진단 보고서 검토</span><span class="sxs-lookup"><span data-stu-id="9518d-374">Review the diagnostics report created by PerfInsights</span></span>

<span data-ttu-id="9518d-375">PerfInsights에서 생성된 **CollectedData\_yyyy-MM-dd\_hh\_mm\_ss.zip 파일** 내에서 PerfInsights의 결과를 자세히 설명하는 HTML 보고서를 찾을 수 있습니다. .</span><span class="sxs-lookup"><span data-stu-id="9518d-375">Within the **CollectedData\_yyyy-MM-dd\_hh\_mm\_ss.zip file,** that is generated by PerfInsights, you can find an HTML report that details the findings of PerfInsights.</span></span> <span data-ttu-id="9518d-376">보고서를 검토하려면 **CollectedData\_yyyy-MM-dd\_hh\_mm\_ss.zip** 파일을 펼친 다음 **PerfInsights Report.html** 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-376">To review the report, expand the **CollectedData\_yyyy-MM-dd\_hh\_mm\_ss.zip** file, and then open the **PerfInsights Report.html** file.</span></span>

<span data-ttu-id="9518d-377">**검색 결과** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-377">Select the **Findings** tab.</span></span>

![찾기 탭](media/how-to-use-perfInsights/findingtab.png)

<span data-ttu-id="9518d-379">**참고 사항**</span><span class="sxs-lookup"><span data-stu-id="9518d-379">**Notes**</span></span>

-   <span data-ttu-id="9518d-380">빨간색 메시지는 성능 문제를 일으킬 수 있는 알려진 구성 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-380">Messages in red are known configuration issues that may cause performance issues.</span></span>

-   <span data-ttu-id="9518d-381">노란색 메시지는 반드시 성능 문제를 일으키지는 않지만 최적이 아닌 구성을 나타내는 경고입니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-381">Messages in yellow are warnings that represent non-optimal configurations that do not necessarily cause performance issues.</span></span>

-   <span data-ttu-id="9518d-382">파란색 메시지는 유익한 정보만 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-382">Messages in blue are informative statements only.</span></span>

<span data-ttu-id="9518d-383">결과에 대한 자세한 정보와 성능 최적화 구성에 대한 성능 또는 모범 사례에 미칠 수 있는 영향에 대한 자세한 정보를 얻으려면 모든 오류 메시지의 빨간색 HTTP 링크를 검토하세요.</span><span class="sxs-lookup"><span data-stu-id="9518d-383">Review the HTTP links for all error messages in red to get more detailed information about the findings and how they can affect the performance or best practices for performance-optimized configurations.</span></span>

### <a name="disk-configuration-tab"></a><span data-ttu-id="9518d-384">디스크 구성 탭</span><span class="sxs-lookup"><span data-stu-id="9518d-384">Disk Configuration Tab</span></span>

<span data-ttu-id="9518d-385">**개요** 섹션에는 Diskpart 및 저장소 공간의 정보를 포함하여 저장소 구성에 대한 다양한 보기가 표시됩니다</span><span class="sxs-lookup"><span data-stu-id="9518d-385">The **Overview** section displays different views of the storage configuration, including information from Diskpart and Storage Spaces</span></span>

<span data-ttu-id="9518d-386">**DiskMap** 및 **VolumeMap** 섹션에서는 논리 볼륨과 실제 디스크가 서로 관련된 방식을 이중 관점에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-386">The **DiskMap** and **VolumeMap** sections describe on a dual perspective how logical volumes and physical disks are related to each other.</span></span>

<span data-ttu-id="9518d-387">PhysicalDisk 관점(DiskMap)에서 테이블은 디스크에서 실행 중인 모든 논리 볼륨을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-387">In the PhysicalDisk perspective (DiskMap), the table shows all logical volumes that are running on the disk.</span></span> <span data-ttu-id="9518d-388">다음 예에서 PhysicalDrive2는 여러 파티션(J 및 H)에서 만든 2개의 논리 볼륨을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-388">In the following example, PhysicalDrive2 runs 2 Logical Volumes created on multiple partitions (J and H):</span></span>

![데이터 탭](media/how-to-use-perfInsights/disktab.png)

<span data-ttu-id="9518d-390">볼륨 관점(*VolumeMap*)에서 테이블은 각 논리 볼륨 아래의 모든 실제 디스크를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-390">In the Volume perspective (*VolumeMap*), the tables show all the physical disks under each logical volume.</span></span> <span data-ttu-id="9518d-391">RAID/동적 디스크의 경우 여러 실제 디스크에서 논리 볼륨을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-391">Notice that for RAID/Dynamic disks, you might run a logical volume upon multiple physical disks.</span></span> <span data-ttu-id="9518d-392">다음 샘플에서 *C:\\mount*는 PhysicalDisks \#2 및 \#3에 *SpannedDisk*로 구성된 탑재 지점입니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-392">In the following sample *C:\\mount* is a mountpoint configured as *SpannedDisk* on PhysicalDisks \#2 and \#3:</span></span>

![볼륨 탭](media/how-to-use-perfInsights/volumetab.png)

### <a name="sql-server-tab"></a><span data-ttu-id="9518d-394">SQL Server 탭</span><span class="sxs-lookup"><span data-stu-id="9518d-394">SQL Server tab</span></span>

<span data-ttu-id="9518d-395">대상 VM에서 SQL Server 인스턴스를 호스팅하는 경우 **SQL Server**라는 보고서에 추가 탭이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-395">If the target VM hosts any SQL Server instances, you will see an additional tab in the report that is named **SQL Server**:</span></span>

![sql 탭](media/how-to-use-perfInsights/sqltab.png)

<span data-ttu-id="9518d-397">이 섹션에는 VM에 호스팅된 SQL Server 인스턴스 각각에 대한 "개요" 및 추가 하위 탭이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-397">This section contains an "Overview" and additional sub tabs for each of the SQL Server instances hosted on the VM.</span></span>

<span data-ttu-id="9518d-398">"개요" 섹션에는 실행 중인 모든 실제 디스크(시스템 및 데이터 디스크)를 요약하고 데이터 파일과 트랜잭션 로그 파일이 혼합되어 있는 유용한 테이블이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-398">The "Overview" section contains a helpful table that summarizes all the physical disks (system and data disks) that are running and that contain a mixture of data files and transaction log files.</span></span>

<span data-ttu-id="9518d-399">다음 예에서는 *modeldev* 및 *modellog* 파일이 모두 C 드라이브에 있으므로 *PhysicalDrive0*(C 드라이브 실행 중)이 표시되며, 이 파일들은 서로 다른 형식의 파일입니다(예: 데이터 파일 및 트랜잭션 로그).</span><span class="sxs-lookup"><span data-stu-id="9518d-399">In the following example, *PhysicalDrive0* (running the C drive) is displayed because both the *modeldev* and *modellog* files are located on the C drive, and they are of different types (such as Data File and Transaction Log, respectively):</span></span>

![로그 정보](media/how-to-use-perfInsights/loginfo.png)

<span data-ttu-id="9518d-401">SQL Server 인스턴스별 탭에는 선택한 인스턴스에 대한 기본 정보와 [설정], [구성] 및 [사용자 옵션]을 포함하여 고급 정보를 위한 추가 섹션이 표시되는 일반 섹션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-401">The SQL Server instance-specific tabs contain a general section that displays basic information about the selected instance and additional sections for advanced information, including Settings, Configurations, and User Options.</span></span>

## <a name="references-to-the-external-tools-used"></a><span data-ttu-id="9518d-402">사용되는 외부 도구에 대한 참조</span><span class="sxs-lookup"><span data-stu-id="9518d-402">References to the external tools used</span></span>

### <a name="diskspd"></a><span data-ttu-id="9518d-403">Diskspd</span><span class="sxs-lookup"><span data-stu-id="9518d-403">Diskspd</span></span>

<span data-ttu-id="9518d-404">Diskspd는 Windows, Windows Server 및 클라우드 서버 인프라 엔지니어링 팀의 저장소 로드 생성기 및 성능 테스트 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-404">DISKSPD is a storage load generator and performance test tool from the Windows and Windows Server and Cloud Server Infrastructure engineering teams.</span></span> <span data-ttu-id="9518d-405">자세한 내용은 [Diskspd](https://github.com/Microsoft/diskspd)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9518d-405">For more information, see [Diskspd](https://github.com/Microsoft/diskspd).</span></span>

### <a name="xperf"></a><span data-ttu-id="9518d-406">XPerf</span><span class="sxs-lookup"><span data-stu-id="9518d-406">XPerf</span></span>

<span data-ttu-id="9518d-407">Xperf는 Windows 성능 도구 키트에서 추적을 캡처하는 명령줄 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-407">Xperf is a command-line tool to capture traces from the Windows Performance Tools Kit.</span></span>

<span data-ttu-id="9518d-408">자세한 내용은 [Windows 성능 도구 키트 - Xperf(영문)](https://blogs.msdn.microsoft.com/ntdebugging/2008/04/03/windows-performance-toolkit-xperf/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9518d-408">For more information, see [Windows Performance Toolkit – Xperf](https://blogs.msdn.microsoft.com/ntdebugging/2008/04/03/windows-performance-toolkit-xperf/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9518d-409">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9518d-409">Next Steps</span></span>

### <a name="upload-diagnostics-logs-and-reports-to-microsoft-support-for-further-review"></a><span data-ttu-id="9518d-410">추가 검토를 위해 Microsoft 지원 서비스에 진단 로그 및 보고서 업로드</span><span class="sxs-lookup"><span data-stu-id="9518d-410">Upload diagnostics logs and reports to Microsoft Support for further review</span></span>

<span data-ttu-id="9518d-411">Microsoft 지원 담당자와 협력할 때 문제 해결 프로세스를 지원하기 위해 PerfInsights에서 생성된 출력을 전송하도록 요청받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-411">When you work with the Microsoft Support staff, you may be requested to transmit the output that is generated by PerfInsights to assist the troubleshooting process.</span></span>

<span data-ttu-id="9518d-412">지원 담당자는 DTM 작업 영역을 만들고 [DTM 포털](https://filetransfer.support.microsoft.com/EFTClient/Account/Login.htm)과 고유한 사용자 ID 및 암호에 대한 링크가 포함된 전자 메일 메시지를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-412">The Support agent will create a DTM workspace for you, and you will receive an email message that includes a link to the [DTM portal (https://filetransfer.support.microsoft.com/EFTClient/Account/Login.htm) and a unique user ID and password.</span></span>

<span data-ttu-id="9518d-413">이 메시지는 **CTS 자동 진단 서비스**(ctsadiag@microsoft.com)에서 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-413">This message will be sent from **CTS Automated Diagnostics Services** (ctsadiag@microsoft.com).</span></span>

![메시지 샘플](media/how-to-use-perfInsights/supportemail.png)

<span data-ttu-id="9518d-415">보안을 강화하기 위해 처음 사용할 때 암호를 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-415">For additional security, you will be required to change your password on first use.</span></span>

<span data-ttu-id="9518d-416">DTM에 로그인하면 PerfInsights에서 수집한 **CollectedData\_yyyy-MM-dd\_hh\_mm\_ss.zip** 파일을 업로드하는 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9518d-416">After you log in to DTM, you will find a dialog box to upload the **CollectedData\_yyyy-MM-dd\_hh\_mm\_ss.zip** file that was collected by PerfInsights.</span></span>
