---
title: "Azure 진단에서 성능 카운터 aaaUse | Microsoft Docs"
description: "Azure 클라우드 서비스 또는 가상 컴퓨터 toofind 병목 상태에서 성능 카운터를 사용 하 여 및 성능 튜닝 합니다."
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: tysonn
ms.assetid: fc4c61e9-d49d-4ed9-a32c-b91cdf851909
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/29/2016
ms.author: robb
ms.openlocfilehash: f3250816c01fc6e164a6aae48da5035845e6d2b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-use-performance-counters-in-an-azure-application"></a><span data-ttu-id="95b5c-103">Azure 응용 프로그램에서 성능 카운터 만들기 및 사용</span><span class="sxs-lookup"><span data-stu-id="95b5c-103">Create and use performance counters in an Azure application</span></span>
<span data-ttu-id="95b5c-104">이 문서에서는의 hello 이점 및 Azure 응용 프로그램에 tooput 성능 카운터 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-104">This article describes hello benefits of and how tooput performance counters into your Azure application.</span></span> <span data-ttu-id="95b5c-105">Toocollect 데이터를 사용 하 고, 병목 상태를 찾을 하 고, 시스템 및 응용 프로그램 성능을 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-105">You can use them toocollect data, find bottlenecks, and tune system and application performance.</span></span>

<span data-ttu-id="95b5c-106">Windows Server, IIS 및 ASP.NET에 대해 성능 카운터를 수집할 수도 있습니다 및 Azure 웹 역할, 작업자 역할 및 가상 컴퓨터의 toodetermine hello 상태를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-106">Performance counters available for Windows Server, IIS, and ASP.NET can also be collected and used toodetermine hello health of your Azure web roles, worker roles, and Virtual Machines.</span></span> <span data-ttu-id="95b5c-107">사용자 지정 성능 카운터를 만들고 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-107">You can also create and use custom performance counters.</span></span>  

<span data-ttu-id="95b5c-108">성능 카운터 데이터를 다음과 같이 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-108">You can examine performance counter data</span></span>

1. <span data-ttu-id="95b5c-109">원격 데스크톱을 사용 하 여 액세스 하는 hello 성능 모니터 도구와 함께 hello 응용 프로그램 호스트에서 직접</span><span class="sxs-lookup"><span data-stu-id="95b5c-109">Directly on hello application host with hello Performance Monitor tool accessed using Remote Desktop</span></span>
2. <span data-ttu-id="95b5c-110">Azure 관리 팩 hello를 사용 하 여 System Center Operations manager</span><span class="sxs-lookup"><span data-stu-id="95b5c-110">With System Center Operations Manager using hello Azure Management Pack</span></span>
3. <span data-ttu-id="95b5c-111">Hello에 액세스 하는 다른 모니터링 도구와 함께 진단 데이터가 tooAzure 저장소를 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-111">With other monitoring tools that access hello diagnostic data transferred tooAzure storage.</span></span> <span data-ttu-id="95b5c-112">자세한 내용은 [Azure 저장소에서 진단 데이터 저장 및 보기](https://msdn.microsoft.com/library/azure/hh411534.aspx) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="95b5c-112">See [Store and View Diagnostic Data in Azure Storage](https://msdn.microsoft.com/library/azure/hh411534.aspx) for more information.</span></span>  

<span data-ttu-id="95b5c-113">Hello에서 응용 프로그램의 hello 성능 모니터링에 대 한 자세한 내용은 [Azure 포털](http://portal.azure.com/), 참조 [tooMonitor 클라우드 서비스 방법](https://www.azure.com/manage/services/cloud-services/how-to-monitor-a-cloud-service/)합니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-113">For more information on monitoring hello performance of your application in hello [Azure portal](http://portal.azure.com/), see [How tooMonitor Cloud Services](https://www.azure.com/manage/services/cloud-services/how-to-monitor-a-cloud-service/).</span></span>

<span data-ttu-id="95b5c-114">로깅 및 추적 전략 하며 진단 및 기타 기술 tootroubleshoot 문제를 사용 하 여 깊이 있는 추가 지침은 Azure 응용 프로그램을 최적화 하 고, 참조 [Azure 개발에 대 한 모범 사례 문제 해결 응용 프로그램](https://msdn.microsoft.com/library/azure/hh771389.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-114">For additional in-depth guidance on creating a logging and tracing strategy and using diagnostics and other techniques tootroubleshoot problems and optimize Azure applications, see [Troubleshooting Best Practices for Developing Azure Applications](https://msdn.microsoft.com/library/azure/hh771389.aspx).</span></span>

## <a name="enable-performance-counter-monitoring"></a><span data-ttu-id="95b5c-115">성능 카운터 모니터링 사용</span><span class="sxs-lookup"><span data-stu-id="95b5c-115">Enable performance counter monitoring</span></span>
<span data-ttu-id="95b5c-116">성능 카운터는 기본적으로 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-116">Performance counters are not enabled by default.</span></span> <span data-ttu-id="95b5c-117">응용 프로그램 또는 시작 작업 hello 기본 진단 원하는 toomonitor 각 역할 인스턴스에 대 한 에이전트 구성 tooinclude hello 특정 성능 카운터를 수정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-117">Your application or a startup task must modify hello default diagnostics agent configuration tooinclude hello specific performance counters that you wish toomonitor for each role instance.</span></span>

### <a name="performance-counters-available-for-microsoft-azure"></a><span data-ttu-id="95b5c-118">Microsoft Azure에 사용할 수 있는 성능 카운터</span><span class="sxs-lookup"><span data-stu-id="95b5c-118">Performance counters available for Microsoft Azure</span></span>
<span data-ttu-id="95b5c-119">Azure는 Windows Server, IIS 및 ASP.NET 스택에서 hello에 대 한 hello 사용할 수 있는 성능 카운터의 하위 집합을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-119">Azure provides a subset of hello performance counters available for Windows Server, IIS and hello ASP.NET stack.</span></span> <span data-ttu-id="95b5c-120">hello 다음 표에서 Azure 응용 프로그램에 대 한 관심 있는 특정의 hello 성능 카운터입니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-120">hello following table lists some of hello performance counters of particular interest for Azure applications.</span></span>

| <span data-ttu-id="95b5c-121">카운터 범주: 개체(인스턴스)</span><span class="sxs-lookup"><span data-stu-id="95b5c-121">Counter Category: Object (Instance)</span></span> | <span data-ttu-id="95b5c-122">카운터 이름</span><span class="sxs-lookup"><span data-stu-id="95b5c-122">Counter Name</span></span> | <span data-ttu-id="95b5c-123">참조</span><span class="sxs-lookup"><span data-stu-id="95b5c-123">Reference</span></span> |
| --- | --- | --- |
| <span data-ttu-id="95b5c-124">.NET CLR Exceptions(*Global*)</span><span class="sxs-lookup"><span data-stu-id="95b5c-124">.NET CLR Exceptions(*Global*)</span></span> |<span data-ttu-id="95b5c-125"># Exceps Thrown / sec</span><span class="sxs-lookup"><span data-stu-id="95b5c-125"># Exceps Thrown / sec</span></span> |<span data-ttu-id="95b5c-126">예외 성능 카운터</span><span class="sxs-lookup"><span data-stu-id="95b5c-126">Exception Performance Counters</span></span> |
| <span data-ttu-id="95b5c-127">.NET CLR Memory(*Global*)</span><span class="sxs-lookup"><span data-stu-id="95b5c-127">.NET CLR Memory(*Global*)</span></span> |<span data-ttu-id="95b5c-128">% Time in GC</span><span class="sxs-lookup"><span data-stu-id="95b5c-128">% Time in GC</span></span> |<span data-ttu-id="95b5c-129">메모리 성능 카운터</span><span class="sxs-lookup"><span data-stu-id="95b5c-129">Memory Performance Counters</span></span> |
| <span data-ttu-id="95b5c-130">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="95b5c-130">ASP.NET</span></span> |<span data-ttu-id="95b5c-131">응용 프로그램 다시 시작</span><span class="sxs-lookup"><span data-stu-id="95b5c-131">Application Restarts</span></span> |<span data-ttu-id="95b5c-132">ASP.NET용 성능 카운터</span><span class="sxs-lookup"><span data-stu-id="95b5c-132">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="95b5c-133">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="95b5c-133">ASP.NET</span></span> |<span data-ttu-id="95b5c-134">요청 실행 시간</span><span class="sxs-lookup"><span data-stu-id="95b5c-134">Request Execution Time</span></span> |<span data-ttu-id="95b5c-135">ASP.NET용 성능 카운터</span><span class="sxs-lookup"><span data-stu-id="95b5c-135">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="95b5c-136">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="95b5c-136">ASP.NET</span></span> |<span data-ttu-id="95b5c-137">요청이 끊김</span><span class="sxs-lookup"><span data-stu-id="95b5c-137">Requests Disconnected</span></span> |<span data-ttu-id="95b5c-138">ASP.NET용 성능 카운터</span><span class="sxs-lookup"><span data-stu-id="95b5c-138">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="95b5c-139">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="95b5c-139">ASP.NET</span></span> |<span data-ttu-id="95b5c-140">작업자 프로세스 다시 시작</span><span class="sxs-lookup"><span data-stu-id="95b5c-140">Worker Process Restarts</span></span> |<span data-ttu-id="95b5c-141">ASP.NET용 성능 카운터</span><span class="sxs-lookup"><span data-stu-id="95b5c-141">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="95b5c-142">ASP.NET Applications(**Total**)</span><span class="sxs-lookup"><span data-stu-id="95b5c-142">ASP.NET Applications(**Total**)</span></span> |<span data-ttu-id="95b5c-143">총 요청 수</span><span class="sxs-lookup"><span data-stu-id="95b5c-143">Requests Total</span></span> |<span data-ttu-id="95b5c-144">ASP.NET용 성능 카운터</span><span class="sxs-lookup"><span data-stu-id="95b5c-144">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="95b5c-145">ASP.NET Applications(**Total**)</span><span class="sxs-lookup"><span data-stu-id="95b5c-145">ASP.NET Applications(**Total**)</span></span> |<span data-ttu-id="95b5c-146">Requests/Sec</span><span class="sxs-lookup"><span data-stu-id="95b5c-146">Requests/Sec</span></span> |<span data-ttu-id="95b5c-147">ASP.NET용 성능 카운터</span><span class="sxs-lookup"><span data-stu-id="95b5c-147">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="95b5c-148">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="95b5c-148">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="95b5c-149">요청 실행 시간</span><span class="sxs-lookup"><span data-stu-id="95b5c-149">Request Execution Time</span></span> |<span data-ttu-id="95b5c-150">ASP.NET용 성능 카운터</span><span class="sxs-lookup"><span data-stu-id="95b5c-150">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="95b5c-151">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="95b5c-151">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="95b5c-152">요청 대기 시간</span><span class="sxs-lookup"><span data-stu-id="95b5c-152">Request Wait Time</span></span> |<span data-ttu-id="95b5c-153">ASP.NET용 성능 카운터</span><span class="sxs-lookup"><span data-stu-id="95b5c-153">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="95b5c-154">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="95b5c-154">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="95b5c-155">현재 요청</span><span class="sxs-lookup"><span data-stu-id="95b5c-155">Requests Current</span></span> |<span data-ttu-id="95b5c-156">ASP.NET용 성능 카운터</span><span class="sxs-lookup"><span data-stu-id="95b5c-156">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="95b5c-157">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="95b5c-157">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="95b5c-158">대기 중인 요청</span><span class="sxs-lookup"><span data-stu-id="95b5c-158">Requests Queued</span></span> |<span data-ttu-id="95b5c-159">ASP.NET용 성능 카운터</span><span class="sxs-lookup"><span data-stu-id="95b5c-159">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="95b5c-160">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="95b5c-160">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="95b5c-161">거부된 요청</span><span class="sxs-lookup"><span data-stu-id="95b5c-161">Requests Rejected</span></span> |<span data-ttu-id="95b5c-162">ASP.NET용 성능 카운터</span><span class="sxs-lookup"><span data-stu-id="95b5c-162">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="95b5c-163">메모리</span><span class="sxs-lookup"><span data-stu-id="95b5c-163">Memory</span></span> |<span data-ttu-id="95b5c-164">Available MBytes</span><span class="sxs-lookup"><span data-stu-id="95b5c-164">Available MBytes</span></span> |<span data-ttu-id="95b5c-165">메모리 성능 카운터</span><span class="sxs-lookup"><span data-stu-id="95b5c-165">Memory Performance Counters</span></span> |
| <span data-ttu-id="95b5c-166">메모리</span><span class="sxs-lookup"><span data-stu-id="95b5c-166">Memory</span></span> |<span data-ttu-id="95b5c-167">커밋된 바이트</span><span class="sxs-lookup"><span data-stu-id="95b5c-167">Committed Bytes</span></span> |<span data-ttu-id="95b5c-168">메모리 성능 카운터</span><span class="sxs-lookup"><span data-stu-id="95b5c-168">Memory Performance Counters</span></span> |
| <span data-ttu-id="95b5c-169">Processor(_Total)</span><span class="sxs-lookup"><span data-stu-id="95b5c-169">Processor(_Total)</span></span> |<span data-ttu-id="95b5c-170">% Processor Time</span><span class="sxs-lookup"><span data-stu-id="95b5c-170">% Processor Time</span></span> |<span data-ttu-id="95b5c-171">ASP.NET용 성능 카운터</span><span class="sxs-lookup"><span data-stu-id="95b5c-171">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="95b5c-172">TCPv4</span><span class="sxs-lookup"><span data-stu-id="95b5c-172">TCPv4</span></span> |<span data-ttu-id="95b5c-173">연결 오류</span><span class="sxs-lookup"><span data-stu-id="95b5c-173">Connection Failures</span></span> |<span data-ttu-id="95b5c-174">TCP Object</span><span class="sxs-lookup"><span data-stu-id="95b5c-174">TCP Object</span></span> |
| <span data-ttu-id="95b5c-175">TCPv4</span><span class="sxs-lookup"><span data-stu-id="95b5c-175">TCPv4</span></span> |<span data-ttu-id="95b5c-176">Connections Established</span><span class="sxs-lookup"><span data-stu-id="95b5c-176">Connections Established</span></span> |<span data-ttu-id="95b5c-177">TCP Object</span><span class="sxs-lookup"><span data-stu-id="95b5c-177">TCP Object</span></span> |
| <span data-ttu-id="95b5c-178">TCPv4</span><span class="sxs-lookup"><span data-stu-id="95b5c-178">TCPv4</span></span> |<span data-ttu-id="95b5c-179">Connections Reset</span><span class="sxs-lookup"><span data-stu-id="95b5c-179">Connections Reset</span></span> |<span data-ttu-id="95b5c-180">TCP Object</span><span class="sxs-lookup"><span data-stu-id="95b5c-180">TCP Object</span></span> |
| <span data-ttu-id="95b5c-181">TCPv4</span><span class="sxs-lookup"><span data-stu-id="95b5c-181">TCPv4</span></span> |<span data-ttu-id="95b5c-182">Segments Sent/sec</span><span class="sxs-lookup"><span data-stu-id="95b5c-182">Segments Sent/sec</span></span> |<span data-ttu-id="95b5c-183">TCP Object</span><span class="sxs-lookup"><span data-stu-id="95b5c-183">TCP Object</span></span> |
| <span data-ttu-id="95b5c-184">Network Interface(*)</span><span class="sxs-lookup"><span data-stu-id="95b5c-184">Network Interface(*)</span></span> |<span data-ttu-id="95b5c-185">Bytes Received/sec</span><span class="sxs-lookup"><span data-stu-id="95b5c-185">Bytes Received/sec</span></span> |<span data-ttu-id="95b5c-186">Network Interface Object</span><span class="sxs-lookup"><span data-stu-id="95b5c-186">Network Interface Object</span></span> |
| <span data-ttu-id="95b5c-187">Network Interface(*)</span><span class="sxs-lookup"><span data-stu-id="95b5c-187">Network Interface(*)</span></span> |<span data-ttu-id="95b5c-188">Bytes Sent/sec</span><span class="sxs-lookup"><span data-stu-id="95b5c-188">Bytes Sent/sec</span></span> |<span data-ttu-id="95b5c-189">Network Interface Object</span><span class="sxs-lookup"><span data-stu-id="95b5c-189">Network Interface Object</span></span> |
| <span data-ttu-id="95b5c-190">Network Interface(Microsoft Virtual Machine Bus Network Adapter _2)</span><span class="sxs-lookup"><span data-stu-id="95b5c-190">Network Interface(Microsoft Virtual Machine Bus Network Adapter _2)</span></span> |<span data-ttu-id="95b5c-191">Bytes Received/sec</span><span class="sxs-lookup"><span data-stu-id="95b5c-191">Bytes Received/sec</span></span> |<span data-ttu-id="95b5c-192">Network Interface Object</span><span class="sxs-lookup"><span data-stu-id="95b5c-192">Network Interface Object</span></span> |
| <span data-ttu-id="95b5c-193">Network Interface(Microsoft Virtual Machine Bus Network Adapter _2)</span><span class="sxs-lookup"><span data-stu-id="95b5c-193">Network Interface(Microsoft Virtual Machine Bus Network Adapter _2)</span></span> |<span data-ttu-id="95b5c-194">Bytes Sent/sec</span><span class="sxs-lookup"><span data-stu-id="95b5c-194">Bytes Sent/sec</span></span> |<span data-ttu-id="95b5c-195">Network Interface Object</span><span class="sxs-lookup"><span data-stu-id="95b5c-195">Network Interface Object</span></span> |
| <span data-ttu-id="95b5c-196">Network Interface(Microsoft Virtual Machine Bus Network Adapter _2)</span><span class="sxs-lookup"><span data-stu-id="95b5c-196">Network Interface(Microsoft Virtual Machine Bus Network Adapter _2)</span></span> |<span data-ttu-id="95b5c-197">Bytes Total/sec</span><span class="sxs-lookup"><span data-stu-id="95b5c-197">Bytes Total/sec</span></span> |<span data-ttu-id="95b5c-198">Network Interface Object</span><span class="sxs-lookup"><span data-stu-id="95b5c-198">Network Interface Object</span></span> |

## <a name="create-and-add-custom-performance-counters-tooyour-application"></a><span data-ttu-id="95b5c-199">만들기 및 사용자 지정 성능 카운터 tooyour 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="95b5c-199">Create and add custom performance counters tooyour application</span></span>
<span data-ttu-id="95b5c-200">Azure 지원 toocreate 개이고 웹 역할과 작업자 역할에 대 한 사용자 지정 성능 카운터를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-200">Azure has support toocreate and modify custom performance counters for web roles and worker roles.</span></span> <span data-ttu-id="95b5c-201">hello 카운터 tootrack 및 모니터 응용 프로그램 관련 동작을 사용 하는 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-201">hello counters may be used tootrack and monitor application-specific behavior.</span></span> <span data-ttu-id="95b5c-202">승격된 권한으로 시작 작업, 웹 역할 또는 작업자 역할에서 사용자 지정 성능 카운터 범주 및 지정자를 만들고 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-202">You can create and delete custom performance counter categories and specifiers from a startup task, web role, or worker role with elevated permissions.</span></span>

> [!NOTE]
> <span data-ttu-id="95b5c-203">Toocustom ÷ ´ ֹ 변경 하는 코드에서 사용 권한을 toorun을 높은 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-203">Code that makes changes toocustom performance counters must have elevated permissions toorun.</span></span> <span data-ttu-id="95b5c-204">Hello 역할 hello 태그를 포함 해야 hello 코드가 웹 역할 또는 작업자 역할에 포함 된 경우 <Runtime executionContext="elevated" /> hello ServiceDefinition.csdef 파일에 역할 tooinitialize hello에 대 한 적절 합니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-204">If hello code is in a web role or worker role, hello role must include hello tag <Runtime executionContext="elevated" /> in hello ServiceDefinition.csdef file for hello role tooinitialize properly.</span></span>
>
>

<span data-ttu-id="95b5c-205">사용자 지정 성능 카운터 데이터 tooAzure 저장소 hello 진단 에이전트를 사용 하 여 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-205">You can send custom performance counter data tooAzure storage using hello diagnostics agent.</span></span>

<span data-ttu-id="95b5c-206">hello 표준 성능 카운터 데이터는 hello Azure 프로세스에 의해 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-206">hello standard performance counter data is generated by hello Azure processes.</span></span> <span data-ttu-id="95b5c-207">웹 역할 또는 작업자 역할 응용 프로그램에서 사용자 지정 성능 카운터 데이터를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-207">Custom performance counter data must be created by your web role or worker role application.</span></span> <span data-ttu-id="95b5c-208">참조 [성능 카운터 형식](https://msdn.microsoft.com/library/z573042h.aspx) hello 유형의 사용자 지정 성능 카운터에 저장할 수 있는 데이터에 대 한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-208">See [Performance Counter Types](https://msdn.microsoft.com/library/z573042h.aspx) for information on hello types of data that can be stored in custom performance counters.</span></span> <span data-ttu-id="95b5c-209">웹 역할에서 사용자 지정 성능 카운터 데이터를 만들고 설정하는 예제는 [PerformanceCounters 샘플](http://code.msdn.microsoft.com/azure/) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="95b5c-209">See [PerformanceCounters Sample](http://code.msdn.microsoft.com/azure/) for an example that creates and sets custom performance counter data in a web role.</span></span>

## <a name="store-and-view-performance-counter-data"></a><span data-ttu-id="95b5c-210">성능 카운터 데이터 저장 및 보기</span><span class="sxs-lookup"><span data-stu-id="95b5c-210">Store and view performance counter data</span></span>
<span data-ttu-id="95b5c-211">Azure는 기타 진단 정보와 함께 성능 카운터 데이터를 캐시합니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-211">Azure caches performance counter data with other diagnostic information.</span></span> <span data-ttu-id="95b5c-212">이 데이터를 성능 모니터와 같은 원격 데스크톱 액세스 tooview 도구를 사용 하 여 hello 역할 인스턴스가 실행 되는 동안 원격 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-212">This data is available for remote monitoring while hello role instance is running using remote desktop access tooview tools such as Performance Monitor.</span></span> <span data-ttu-id="95b5c-213">hello 역할 인스턴스 외부의 toopersist hello 데이터 hello 진단 에이전트 hello 데이터 tooAzure 저장소를 전송 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-213">toopersist hello data outside of hello role instance, hello diagnostics agent must transfer hello data tooAzure storage.</span></span> <span data-ttu-id="95b5c-214">hello 캐시 성능 카운터 데이터의 크기 제한을 hello hello 진단 에이전트에서 구성할 수 있습니다 또는 것이 모든 진단 데이터를 hello에 대 한 공유 제한의 toobe 일부를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-214">hello size limit of hello cached performance counter data can be configured in hello diagnostics agent, or it may be configured toobe part of a shared limit for all hello diagnostic data.</span></span> <span data-ttu-id="95b5c-215">Hello 버퍼 크기를 설정 하는 방법에 대 한 자세한 내용은 참조 [OverallQuotaInMB](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitorconfiguration.overallquotainmb.aspx) 및 [DirectoriesBufferConfiguration](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.directoriesbufferconfiguration.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-215">For more information about setting hello buffer size, see [OverallQuotaInMB](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitorconfiguration.overallquotainmb.aspx) and [DirectoriesBufferConfiguration](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.directoriesbufferconfiguration.aspx).</span></span> <span data-ttu-id="95b5c-216">참조 [스토어 및 Azure 저장소에 진단 데이터 보기](https://msdn.microsoft.com/library/azure/hh411534.aspx) hello 진단 에이전트 tootransfer 데이터 tooa 저장소 계정 설정에 대 한 개요입니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-216">See [Store and View Diagnostic Data in Azure Storage](https://msdn.microsoft.com/library/azure/hh411534.aspx) for an overview of setting up hello diagnostics agent tootransfer data tooa storage account.</span></span>

<span data-ttu-id="95b5c-217">Hello 샘플링 된 데이터를 전송 하 고 각 구성 된 성능 카운터 인스턴스는 특정된 샘플링 비율로 기록 되며 toohello 저장소 계정 예약된 전송 요청 또는 요청 시 전송 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-217">Each configured performance counter instance is recorded at a specified sampling rate, and hello sampled data is transferred toohello storage account either by a scheduled transfer request or an on-demand transfer request.</span></span> <span data-ttu-id="95b5c-218">자동 전송은 매 분마다 예약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-218">Automatic transfers may be scheduled as often as once per minute.</span></span> <span data-ttu-id="95b5c-219">Hello 진단 에이전트에 의해 전송 되는 성능 카운터 데이터는 테이블 WADPerformanceCountersTable, hello 저장소 계정에에서 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-219">Performance counter data transferred by hello diagnostics agent is stored in a table, WADPerformanceCountersTable, in hello storage account.</span></span> <span data-ttu-id="95b5c-220">표준 Azure 저장소 API 메서드를 사용하여 이 테이블에 액세스 및 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-220">This table may be accessed and queried with standard Azure storage API methods.</span></span> <span data-ttu-id="95b5c-221">참조 [Microsoft Azure PerformanceCounters 샘플](http://code.msdn.microsoft.com/Windows-Azure-PerformanceCo-7d80ebf9) 쿼리하고 표시 hello WADPerformanceCountersTable 테이블에서 성능 카운터 데이터의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-221">See [Microsoft Azure PerformanceCounters Sample](http://code.msdn.microsoft.com/Windows-Azure-PerformanceCo-7d80ebf9) for an example of querying and displaying performance counter data from hello WADPerformanceCountersTable table.</span></span>

> [!NOTE]
> <span data-ttu-id="95b5c-222">Hello 진단 에이전트 전송 빈도 및 큐 대기 시간에 따라 hello hello 저장소 계정에서 성능 카운터 데이터를 가장 최근의 수 몇 분 정도입니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-222">Depending on hello diagnostics agent transfer frequency and queue latency, hello most recent performance counter data in hello storage account may be several minutes out of date.</span></span>
>
>

## <a name="enable-performance-counters-using-diagnostics-configuration-file"></a><span data-ttu-id="95b5c-223">진단 구성 파일을 사용하여 성능 카운터를 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="95b5c-223">Enable performance counters using diagnostics configuration file</span></span>
<span data-ttu-id="95b5c-224">Azure 응용 프로그램에서 프로시저 tooenable 성능 카운터를 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-224">Use hello following procedure tooenable performance counters in your Azure application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="95b5c-225">필수 조건</span><span class="sxs-lookup"><span data-stu-id="95b5c-225">Prerequisites</span></span>
<span data-ttu-id="95b5c-226">이 섹션에서는 hello 진단 모니터를 응용 프로그램으로 가져온 고 hello 진단 구성 파일 tooyour Visual Studio 솔루션 (SDK 2.4이 하 버전에 diagnostics.wadcfg 또는 SDK 2.5에서 이상 diagnostics.wadcfgx)를 추가 했다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-226">This section assumes that you have imported hello Diagnostics monitor into your application and added hello diagnostics configuration file tooyour Visual Studio solution (diagnostics.wadcfg in SDK 2.4 and below or diagnostics.wadcfgx in SDK 2.5 and above).</span></span> <span data-ttu-id="95b5c-227">자세한 내용은 [Azure 클라우드 서비스 및 Virtual Machine에서 진단 사용](cloud-services-dotnet-diagnostics.md))의 1, 2단계를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="95b5c-227">See steps 1 and 2 in [Enabling Diagnostics in Azure Cloud Services and Virtual Machines](cloud-services-dotnet-diagnostics.md)) for more information.</span></span>

## <a name="step-1-collect-and-store-data-from-performance-counters"></a><span data-ttu-id="95b5c-228">1단계: 성능 카운터에서 데이터 수집 및 저장</span><span class="sxs-lookup"><span data-stu-id="95b5c-228">Step 1: Collect and store data from performance counters</span></span>
<span data-ttu-id="95b5c-229">Hello 진단 tooyour Visual Studio 솔루션 파일을 추가 하면 Azure 응용 프로그램에서 성능 카운터 데이터의 hello 수집 및 저장을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-229">After you have added hello diagnostics file tooyour Visual Studio solution, you can configure hello collection and storage of performance counter data in an Azure application.</span></span> <span data-ttu-id="95b5c-230">이 성능 카운터 toohello 진단 파일을 추가 하 여 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-230">This is done by adding performance counters toohello diagnostics file.</span></span> <span data-ttu-id="95b5c-231">진단 데이터를 성능 카운터를 포함 하 여 hello 인스턴스에서 먼저 수집 됩니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-231">Diagnostics data, including performance counters, is first collected on hello instance.</span></span> <span data-ttu-id="95b5c-232">hello 데이터 지속형된 toohello WADPerformanceCountersTable 테이블 hello Azure 테이블 서비스에에서 다음을 할 수 있으므로 필요 toospecify hello 응용 프로그램의 저장소 계정.</span><span class="sxs-lookup"><span data-stu-id="95b5c-232">hello data is then persisted toohello WADPerformanceCountersTable table in hello Azure Table service, so you will also need toospecify hello storage account in your application.</span></span> <span data-ttu-id="95b5c-233">Hello 계산 에뮬레이터에서에서 로컬로 응용 프로그램를 테스트 하는 경우 저장할 수도 있습니다 진단 데이터 로컬 저장소 에뮬레이터의 hello에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-233">If you're testing your application locally in hello Compute Emulator, you can also store diagnostics data locally in hello Storage Emulator.</span></span> <span data-ttu-id="95b5c-234">진단 데이터를 저장 하기 전에 먼저 toohello를 이동 해야 [Azure 포털](http://portal.azure.com/) 클래식 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-234">Before you store diagnostics data, you must first go toohello [Azure portal](http://portal.azure.com/) and create a classic storage account.</span></span> <span data-ttu-id="95b5c-235">가장 좋은 방법은 toolocate 저장소 계정에서 Azure 응용 프로그램과 동일한 지리적 위치의 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-235">A best practice is toolocate your storage account in hello same geo-location as your Azure application.</span></span> <span data-ttu-id="95b5c-236">Hello 유지 하 여 Azure 응용 프로그램 및 저장소 계정은에 hello 동일한 지리적 위치의 외부 대역폭 비용을 지불 하지 않고 대기 시간 단축 합니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-236">By keeping hello Azure application and storage account are in hello same geo-location, you avoid paying external bandwidth costs and reduce latency.</span></span>

### <a name="add-performance-counters-toohello-diagnostics-file"></a><span data-ttu-id="95b5c-237">성능 카운터 toohello 진단 파일 추가</span><span class="sxs-lookup"><span data-stu-id="95b5c-237">Add performance counters toohello diagnostics file</span></span>
<span data-ttu-id="95b5c-238">사용할 수 있는 카운터가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-238">There are many counters you can use.</span></span> <span data-ttu-id="95b5c-239">hello 다음 예제에서는 웹 및 작업자 역할 모니터링에 대 한 권장 되는 몇 가지 성능 카운터</span><span class="sxs-lookup"><span data-stu-id="95b5c-239">hello following example shows several performance counters that are recommended for web and worker role monitoring.</span></span>

<span data-ttu-id="95b5c-240">(SDK 2.4와 그 하위 diagnostics.wadcfg 또는 SDK 2.5에서 이상 diagnostics.wadcfgx) hello 진단 파일을 열고 toohello DiagnosticMonitorConfiguration 요소 다음에 오는 hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-240">Open hello diagnostics file (diagnostics.wadcfg in SDK 2.4 and below or diagnostics.wadcfgx in SDK 2.5 and above) and add hello following toohello DiagnosticMonitorConfiguration element:</span></span>

```xml
<PerformanceCounters bufferQuotaInMB="0" scheduledTransferPeriod="PT30M">
    <PerformanceCounterConfiguration counterSpecifier="\Memory\Available Bytes" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT30S" />

    <!-- Use hello Process(w3wp) category counters in a web role -->

    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\% Processor Time" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\Private Bytes" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\Thread Count" sampleRate="PT30S" />

    <!-- Use hello Process(WaWorkerHost) category counters in a worker role.
        <PerformanceCounterConfiguration counterSpecifier="\Process(WaWorkerHost)\% Processor Time" sampleRate="PT30S" />
        <PerformanceCounterConfiguration counterSpecifier="\Process(WaWorkerHost)\Private Bytes" sampleRate="PT30S" />
        <PerformanceCounterConfiguration counterSpecifier="\Process(WaWorkerHost)\Thread Count" sampleRate="PT30S" />
    -->

    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Interop(_Global_)\# of marshalling" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Loading(_Global_)\% Time Loading" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR LocksAndThreads(_Global_)\Contention Rate / sec" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Memory(_Global_)\# Bytes in all Heaps" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Networking(_Global_)\Connections Established" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Remoting(_Global_)\Remote Calls/sec" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Jit(_Global_)\% Time in Jit" sampleRate="PT30S" />
</PerformanceCounters>
```

<span data-ttu-id="95b5c-241">hello bufferQuotaInMB 특성 hello hello 데이터 컬렉션 형식 (Azure 로그, IIS 로그 등)에 사용할 수 있는 파일 시스템 저장소의 최대 크기를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-241">hello bufferQuotaInMB attribute, which specifies hello maximum amount of file system storage that is available for hello data collection type (Azure logs, IIS logs, etc.).</span></span> <span data-ttu-id="95b5c-242">hello 기본값은 0입니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-242">hello default is 0.</span></span> <span data-ttu-id="95b5c-243">Hello 할당량에 도달 하면 새 데이터가 추가 되므로 hello 가장 오래 된 데이터가 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-243">When hello quota is reached, hello oldest data is deleted as new data is added.</span></span> <span data-ttu-id="95b5c-244">모든 hello bufferQuotaInMB 속성의 hello 합계 hello hello OverallQuotaInMB 특성 값 보다 커야 합니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-244">hello sum of all hello bufferQuotaInMB properties must be greater than hello value of hello OverallQuotaInMB attribute.</span></span> <span data-ttu-id="95b5c-245">저장소 크기는 진단 데이터의 hello 컬렉션에 대 한 요구 됩니다 결정 하는 보다 자세한 논의 알려면의 WAD 설정 섹션 hello [문제 해결에 대 한 유용한 Azure 응용 프로그램 개발](https://msdn.microsoft.com/library/windowsazure/hh771389.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-245">For a more detailed discussion of determining how much storage will be required for hello collection of diagnostics data, see hello Setup WAD section of [Troubleshooting Best Practices for Developing Azure Applications](https://msdn.microsoft.com/library/windowsazure/hh771389.aspx).</span></span>

<span data-ttu-id="95b5c-246">hello 예약 된 데이터 전송 간격을 지정 하는, hello scheduledTransferPeriod 특성 toohello 가장 근접 한 분을 반올림 합니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-246">hello scheduledTransferPeriod attribute, which specifies hello interval between scheduled transfers of data, rounded up toohello nearest minute.</span></span> <span data-ttu-id="95b5c-247">다음 예제는 hello, tooPT30M (30 분) 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-247">In hello following examples, it is set tooPT30M (30 minutes).</span></span> <span data-ttu-id="95b5c-248">설정 hello 전송 기간 tooa 같은 작은 값으로 1 분, 프로덕션 환경에서 응용 프로그램의 성능을 저하 이지만 진단 작업 결과 신속 하 게 테스트 하는 경우를 확인 하는 데 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-248">Setting hello transfer period tooa small value, such as 1 minute, will adversely impact your application's performance in production but can be useful for seeing diagnostics working quickly when you are testing.</span></span> <span data-ttu-id="95b5c-249">hello 예약 된 전송 기간은 진단 데이터를 응용 프로그램의 hello 성능 영향을 주지 것입니다 충분히 큰 하지만 hello 인스턴스에서 덮어쓸 수 없습니다 만큼 작지 않아서 tooensure 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-249">hello scheduled transfer period should be small enough tooensure that diagnostic data is not overwritten on hello instance, but large enough that it will not impact hello performance of your application.</span></span>

<span data-ttu-id="95b5c-250">hello counterSpecifier 특성 hello 성능 카운터 toocollect를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-250">hello counterSpecifier attribute specifies hello performance counter toocollect.</span></span> <span data-ttu-id="95b5c-251">hello sampleRate 특성 hello 속도는 hello 성능 카운터를 샘플링할이 경우 30 초를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-251">hello sampleRate attribute specifies hello rate at which hello performance counter should be sampled, in this case 30 seconds.</span></span>

<span data-ttu-id="95b5c-252">원하는 toocollect hello 성능 카운터를 추가 하면 변경 내용이 toohello 진단 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-252">Once you've added hello performance counters that you want toocollect, save your changes toohello diagnostics file.</span></span> <span data-ttu-id="95b5c-253">다음으로 hello 진단 데이터를 저장할 toospecify hello 저장소 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-253">Next, you need toospecify hello storage account that hello diagnostics data will be persisted to.</span></span>

### <a name="specify-hello-storage-account"></a><span data-ttu-id="95b5c-254">Hello 저장소 계정을 지정합니다</span><span class="sxs-lookup"><span data-stu-id="95b5c-254">Specify hello storage account</span></span>
<span data-ttu-id="95b5c-255">진단 정보 tooyour Azure 저장소 계정으로 지정 해야 toopersist 프로그램 서비스 구성 파일 (ServiceConfiguration.cscfg)에 연결 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-255">toopersist your diagnostics information tooyour Azure Storage account, you must specify a connection string in your service configuration (ServiceConfiguration.cscfg) file.</span></span>

<span data-ttu-id="95b5c-256">Azure SDK 2.5에 대 한 저장소 계정 hello hello diagnostics.wadcfgx 파일에 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-256">For Azure SDK 2.5, hello Storage Account can be specified in hello diagnostics.wadcfgx file.</span></span>

> [!NOTE]
> <span data-ttu-id="95b5c-257">이러한 지침은 tooAzure SDK 2.4이 하 버전을 적용 하 고 아래 합니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-257">These instructions only apply tooAzure SDK 2.4 and below.</span></span> <span data-ttu-id="95b5c-258">Azure SDK 2.5에 대 한 저장소 계정 hello hello diagnostics.wadcfgx 파일에 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-258">For Azure SDK 2.5, hello Storage Account can be specified in hello diagnostics.wadcfgx file.</span></span>
>
>

<span data-ttu-id="95b5c-259">tooset hello 연결 문자열:</span><span class="sxs-lookup"><span data-stu-id="95b5c-259">tooset hello connection strings:</span></span>

1. <span data-ttu-id="95b5c-260">저장소에 대 한 선호 하는 텍스트 편집기 및 연결 문자열을 설정 hello 사용 하 여 hello ServiceConfiguration.Cloud.cscfg 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-260">Open hello ServiceConfiguration.Cloud.cscfg file using your favorite text editor and set hello connection string for your storage.</span></span> <span data-ttu-id="95b5c-261">hello *AccountName* 및 *AccountKey* 값은 hello 저장소 계정 대시보드의 액세스 키 아래에서 Azure 포털 hello에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-261">hello *AccountName* and *AccountKey* values are found in hello Azure portal in hello storage account dashboard, under Access keys.</span></span>

    ```xml
    <ConfigurationSettings>
      <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="DefaultEndpointsProtocol=https;AccountName=<name>;AccountKey=<key>"/>
    </ConfigurationSettings>
    ```
2. <span data-ttu-id="95b5c-262">Hello ServiceConfiguration.Cloud.cscfg 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-262">Save hello ServiceConfiguration.Cloud.cscfg file.</span></span>
3. <span data-ttu-id="95b5c-263">Hello ServiceConfiguration.Local.cscfg 파일을 열고 UseDevelopmentStorage tootrue 설정 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-263">Open hello ServiceConfiguration.Local.cscfg file and verify that UseDevelopmentStorage is set tootrue.</span></span>

    ```xml
    <ConfigurationSettings>
      <Settingname="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true"/>
    </ConfigurationSettings>
    ```
   <span data-ttu-id="95b5c-264">연결 문자열 hello를 설정 하에 응용 프로그램 응용 프로그램을 배포할 때 진단 데이터 tooyour 저장소 계정에 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-264">Now that hello connection strings are set, your application will persist diagnostics data tooyour storage account when your application is deployed.</span></span>
4. <span data-ttu-id="95b5c-265">프로젝트를 저장하고 빌드한 다음 응용 프로그램을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-265">Save and build your project, then deploy your application.</span></span>

## <a name="step-2-optional-create-custom-performance-counters"></a><span data-ttu-id="95b5c-266">2단계: (옵션) 사용자 지정 성능 카운터 만들기</span><span class="sxs-lookup"><span data-stu-id="95b5c-266">Step 2: (Optional) Create custom performance counters</span></span>
<span data-ttu-id="95b5c-267">미리 정의 된 성능 카운터를 또한 toohello, 사용자 고유의 사용자 지정 성능 카운터 toomonitor 웹 또는 작업자 역할을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-267">In addition toohello pre-defined performance counters, you can add your own custom performance counters toomonitor web or worker roles.</span></span> <span data-ttu-id="95b5c-268">사용자 지정 성능 카운터 사용된 tootrack 및 모니터 응용 프로그램별 동작 및 수 수 생성 하거나 삭제할 수 시작 작업, 웹 역할 또는 작업자 역할이 승격 된 권한으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-268">Custom performance counters may be used tootrack and monitor application-specific behavior and can be created or deleted in a startup task, web role, or worker role with elevated permissions.</span></span>

<span data-ttu-id="95b5c-269">hello Azure 진단 에이전트가 hello 성능 카운터 구성을 hello.wadcfg 파일에서 시작한 후 1 분을 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-269">hello Azure diagnostics agent refreshes hello performance counter configuration from hello .wadcfg file one minute after starting.</span></span>  <span data-ttu-id="95b5c-270">Hello OnStart 메서드에에서 사용자 지정 성능 카운터를 만들고 시작 작업 tooexecute 1 분 이상 걸릴 경우 사용자 지정 성능 카운터는 만들어지지 않은 hello Azure 진단 에이전트가 tooload 하려고 할 때 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-270">If you create custom performance counters in hello OnStart method and your startup tasks take longer than one minute tooexecute, your custom performance counters will not have been created when hello Azure Diagnostics agent tries tooload them.</span></span>  <span data-ttu-id="95b5c-271">이 시나리오에서는 Azure 진단이 사용자 지정 성능 카운터를 제외한 모든 진단 데이터를 올바르게 캡처하는 것을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-271">In this scenario, you will see that Azure Diagnostics correctly captures all diagnostics data except your custom performance counters.</span></span>  <span data-ttu-id="95b5c-272">tooresolve이이 문제를 hello 성능 카운터 시작 작업에서 만들거나 이동 hello 성능 카운터를 만든 후 toohello OnStart 메서드 시작 작업의 일부 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-272">tooresolve this issue, create hello performance counters in a startup task or move some of your startup task work toohello OnStart method after creating hello performance counters.</span></span>

<span data-ttu-id="95b5c-273">다음 단계는 간단한 사용자 지정 성능 카운터 "\MyCustomCounterCategory\MyButton1Counter" 라는 toocreate hello를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-273">Perform hello following steps toocreate a simple custom performance counter named "\MyCustomCounterCategory\MyButton1Counter":</span></span>

1. <span data-ttu-id="95b5c-274">응용 프로그램에 대 한 hello 서비스 정의 파일 (CSDEF)을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-274">Open hello service definition file (CSDEF) for your application.</span></span>
2. <span data-ttu-id="95b5c-275">Hello 런타임 요소 toohello WebRole 또는 WorkerRole 요소 tooallow 실행 상승 된 권한으로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-275">Add hello Runtime element toohello WebRole or WorkerRole element tooallow execution with elevated privileges:</span></span>

    ```xml
    <runtime executioncontext="elevated"/>
    ```
3. <span data-ttu-id="95b5c-276">Hello 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-276">Save hello file.</span></span>
4. <span data-ttu-id="95b5c-277">(SDK 2.4와 그 하위 diagnostics.wadcfg 또는 SDK 2.5에서 이상 diagnostics.wadcfgx) hello 진단 파일을 열고 다음 toohello DiagnosticMonitorConfiguration hello 추가</span><span class="sxs-lookup"><span data-stu-id="95b5c-277">Open hello diagnostics file (diagnostics.wadcfg in SDK 2.4 and below or diagnostics.wadcfgx in SDK 2.5 and above) and add hello following toohello DiagnosticMonitorConfiguration</span></span>

    ```xml
    <PerformanceCounters bufferQuotaInMB="0" scheduledTransferPeriod="PT30M">
      <PerformanceCounterConfiguration counterSpecifier="\MyCustomCounterCategory\MyButton1Counter" sampleRate="PT30S"/>
    </PerformanceCounters>
    ```
5. <span data-ttu-id="95b5c-278">Hello 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-278">Save hello file.</span></span>
6. <span data-ttu-id="95b5c-279">사용자 역할의 OnStart 메서드에 hello 자료를 호출 하기 전에 hello 사용자 지정 성능 카운터 범주를 만듭니다. OnStart 합니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-279">Create hello custom performance counter category in hello OnStart method of your role, before invoking base.OnStart.</span></span> <span data-ttu-id="95b5c-280">hello 다음 C# 예제에서는 만들고 사용자 지정 범주 아직 없는 경우:</span><span class="sxs-lookup"><span data-stu-id="95b5c-280">hello following C# example creates a custom category, if it does not already exist:</span></span>

    ```csharp
    public override bool OnStart()
    {
      if (!PerformanceCounterCategory.Exists("MyCustomCounterCategory"))
      {
         CounterCreationDataCollection counterCollection = new CounterCreationDataCollection();

         // add a counter tracking user button1 clicks
         CounterCreationData operationTotal1 = new CounterCreationData();
         operationTotal1.CounterName = "MyButton1Counter";
         operationTotal1.CounterHelp = "My Custom Counter for Button1";
         operationTotal1.CounterType = PerformanceCounterType.NumberOfItems32;
         counterCollection.Add(operationTotal1);

         PerformanceCounterCategory.Create(
           "MyCustomCounterCategory",
           "My Custom Counter Category",
           PerformanceCounterCategoryType.SingleInstance, counterCollection);

         Trace.WriteLine("Custom counter category created.");
      }
      else {
        Trace.WriteLine("Custom counter category already exists.");
      }

    return base.OnStart();
    }
    ```
7. <span data-ttu-id="95b5c-281">응용 프로그램 내에서 hello 카운터를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-281">Update hello counters within your application.</span></span> <span data-ttu-id="95b5c-282">다음 예에서는 hello Button1_Click 이벤트에 사용자 지정 성능 카운터를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-282">hello following example updates a custom performance counter on Button1_Click events:</span></span>

    ```csharp
    protected void Button1_Click(object sender, EventArgs e)
    {
      PerformanceCounter button1Counter = new PerformanceCounter(
        "MyCustomCounterCategory",
        "MyButton1Counter",
        string.Empty,
        false);
      button1Counter.Increment();
      this.Button1.Text = "Button 1 count: " +
        button1Counter.RawValue.ToString();
    }
    ```
8. <span data-ttu-id="95b5c-283">Hello 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-283">Save hello file.</span></span>  

<span data-ttu-id="95b5c-284">사용자 지정 성능 카운터 데이터 이제 hello Azure 진단 모니터에 의해 수집 됩니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-284">Custom performance counter data will now be collected by hello Azure diagnostics monitor.</span></span>

## <a name="step-3-query-performance-counter-data"></a><span data-ttu-id="95b5c-285">3단계: 성능 카운터 데이터 쿼리</span><span class="sxs-lookup"><span data-stu-id="95b5c-285">Step 3: Query performance counter data</span></span>
<span data-ttu-id="95b5c-286">응용 프로그램을 배포 하 고 실행 되 고 hello 진단 모니터가 시작 됩니다 되 면 성능 카운터를 수집 하 고 해당 데이터 tooAzure 저장소를 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-286">Once your application is deployed and running, hello Diagnostics monitor will begin collecting performance counters and persisting that data tooAzure storage.</span></span> <span data-ttu-id="95b5c-287">서버 탐색기와 같은 도구를 사용 하 여 Visual Studio에서 [Azure 저장소 탐색기](http://azurestorageexplorer.codeplex.com/), 또는 [Azure 진단 관리자](http://www.cerebrata.com/Products/AzureDiagnosticsManager/Default.aspx) cerebrata tooview hello의에서 성능 카운터 데이터 hello WADPerformanceCountersTable 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-287">You use tools such as Server Explorer in Visual Studio,  [Azure Storage Explorer](http://azurestorageexplorer.codeplex.com/), or [Azure Diagnostics Manager](http://www.cerebrata.com/Products/AzureDiagnosticsManager/Default.aspx) by Cerebrata tooview hello performance counters data in hello WADPerformanceCountersTable table.</span></span> <span data-ttu-id="95b5c-288">또한 프로그래밍 방식으로 사용 하 여 hello 테이블 서비스를 쿼리할 수 있습니다 [C#](../cosmos-db/table-storage-how-to-use-dotnet.md), [Java](../cosmos-db/table-storage-how-to-use-java.md), [Node.js](../cosmos-db/table-storage-how-to-use-nodejs.md), [Python](../cosmos-db/table-storage-how-to-use-python.md), [Ruby](../cosmos-db/table-storage-how-to-use-ruby.md), 또는 [PHP](../cosmos-db/table-storage-how-to-use-php.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-288">You can also programmatically query hello Table service using [C#](../cosmos-db/table-storage-how-to-use-dotnet.md),  [Java](../cosmos-db/table-storage-how-to-use-java.md),  [Node.js](../cosmos-db/table-storage-how-to-use-nodejs.md), [Python](../cosmos-db/table-storage-how-to-use-python.md), [Ruby](../cosmos-db/table-storage-how-to-use-ruby.md), or [PHP](../cosmos-db/table-storage-how-to-use-php.md).</span></span>

<span data-ttu-id="95b5c-289">hello 다음 C# 예제 hello WADPerformanceCountersTable 테이블에 대 한 기본 쿼리를 보여주며, hello 진단 데이터 tooa CSV 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-289">hello following C# example shows a basic query against hello WADPerformanceCountersTable table and saves hello diagnostics data tooa CSV file.</span></span> <span data-ttu-id="95b5c-290">Hello ÷ ´ ֹ tooa CSV 파일에 저장 되 면 hello 그래프 Microsoft Excel 또는 다른 도구 toovisualize hello 데이터가 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-290">Once hello performance counters are saved tooa CSV file, you can use hello graphing capabilities in Microsoft Excel or some other tool toovisualize hello data.</span></span> <span data-ttu-id="95b5c-291">있는지 tooadd 2012 이상.NET 년 10 월에 대 한 hello Azure SDK에에서 포함 된 참조 tooMicrosoft.WindowsAzure.Storage.dll를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-291">Be sure tooadd a reference tooMicrosoft.WindowsAzure.Storage.dll, which is included in hello Azure SDK for .NET October 2012 and later.</span></span> <span data-ttu-id="95b5c-292">hello 어셈블리는 설치 된 toohello % Program Files%\Microsoft SDKs\Microsoft Azure.NET SDK\version 됩니다 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-292">hello assembly is installed toohello %Program Files%\Microsoft SDKs\Microsoft Azure.NET SDK\version-num\ref\ directory.</span></span>

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
using Microsoft.WindowsAzure.Storage.Table;
...

// Get hello connection string. When using Microsoft Azure Cloud Services, it is recommended
// you store your connection string using hello Microsoft Azure service configuration
// system (*.csdef and *.cscfg files). You can you use hello CloudConfigurationManager type
// tooretrieve your storage connection string.  If you're not using Cloud Services, it's
// recommended that you store hello connection string in your web.config or app.config file.
// Use hello ConfigurationManager type tooretrieve your storage connection string.

string connectionString = Microsoft.WindowsAzure.CloudConfigurationManager.GetSetting("StorageConnectionString");
//string connectionString = System.Configuration.ConfigurationManager.ConnectionStrings["StorageConnectionString"].ConnectionString;

// Get a reference toohello storage account using hello connection string.  You can also use hello development
// storage account (Storage Emulator) for local debugging.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString);
//CloudStorageAccount storageAccount = CloudStorageAccount.DevelopmentStorageAccount;

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "WADPerformanceCountersTable" table.
CloudTable table = tableClient.GetTableReference("WADPerformanceCountersTable");

// Create hello table query, filter on a specific CounterName, DeploymentId and RoleInstance.
TableQuery<PerformanceCountersEntity> query = new TableQuery<PerformanceCountersEntity>()
  .Where(
    TableQuery.CombineFilters(
      TableQuery.GenerateFilterCondition("CounterName", QueryComparisons.Equal, @"\Processor(_Total)\% Processor Time"),
      TableOperators.And,
      TableQuery.CombineFilters(
      TableQuery.GenerateFilterCondition("DeploymentId", QueryComparisons.Equal, "ec26b7a1720447e1bcdeefc41c4892a3"),
      TableOperators.And,
      TableQuery.GenerateFilterCondition("RoleInstance", QueryComparisons.Equal, "WebRole1_IN_0")
    )
  )
);

// Execute hello table query.
IEnumerable<PerformanceCountersEntity> result = table.ExecuteQuery(query);

// Process hello query results and build a CSV file.
StringBuilder sb = new StringBuilder("TimeStamp,EventTickCount,DeploymentId,Role,RoleInstance,CounterName,CounterValue\n");

foreach (PerformanceCountersEntity entity in result)
{
  sb.Append(entity.Timestamp + "," + entity.EventTickCount + "," + entity.DeploymentId + ","
    + entity.Role + "," + entity.RoleInstance + "," + entity.CounterName + "," + entity.CounterValue+"\n");
}

StreamWriter sw = File.CreateText(@"C:\temp\PerfCounters.csv");
sw.Write(sb.ToString());
sw.Close();
```

<span data-ttu-id="95b5c-293">엔터티 tooC # 개체에서 파생 된 사용자 지정 클래스를 사용 하 여 매핑할 **TableEntity**합니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-293">Entities map tooC# objects using a custom class derived from **TableEntity**.</span></span> <span data-ttu-id="95b5c-294">hello 다음 코드에서는 정의 hello에서 성능 카운터를 나타내는 엔터티 클래스 **WADPerformanceCountersTable** 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="95b5c-294">hello following code defines an entity class that represents a performance counter in hello **WADPerformanceCountersTable** table.</span></span>

```csharp
public class PerformanceCountersEntity : TableEntity
{
  public long EventTickCount { get; set; }
  public string DeploymentId { get; set; }
  public string Role { get; set; }
  public string RoleInstance { get; set; }
  public string CounterName { get; set; }
  public double CounterValue { get; set; }
}
```

## <a name="next-steps"></a><span data-ttu-id="95b5c-295">다음 단계</span><span class="sxs-lookup"><span data-stu-id="95b5c-295">Next Steps</span></span>
[<span data-ttu-id="95b5c-296">Azure 진단에 대한 추가 문서 보기</span><span class="sxs-lookup"><span data-stu-id="95b5c-296">View additional articles on Azure Diagnostics</span></span>](../azure-diagnostics.md)
