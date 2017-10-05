---
title: "Azure 진단에서 성능 카운터 사용 | Microsoft Docs"
description: "Azure 클라우드 서비스 또는 가상 컴퓨터에서 성능 카운터를 사용하여 병목을 찾고 성능을 조정합니다."
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
ms.openlocfilehash: 2cf765cb034725199127c547a9b8b997a4a6089c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-use-performance-counters-in-an-azure-application"></a><span data-ttu-id="31e43-103">Azure 응용 프로그램에서 성능 카운터 만들기 및 사용</span><span class="sxs-lookup"><span data-stu-id="31e43-103">Create and use performance counters in an Azure application</span></span>
<span data-ttu-id="31e43-104">이 문서에서는 성능 카운터의 이점 및 Azure 응용 프로그램에 성능 카운터를 배치하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-104">This article describes the benefits of and how to put performance counters into your Azure application.</span></span> <span data-ttu-id="31e43-105">데이터를 수집하고 병목을 찾고 시스템 및 응용 프로그램 성능 튜닝에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-105">You can use them to collect data, find bottlenecks, and tune system and application performance.</span></span>

<span data-ttu-id="31e43-106">Windows Server, IIS 및 ASP.NET에서 사용할 수 있는 성능 카운터를 수집하여 Azure 웹 역할, 작업자 역할 및 가상 컴퓨터의 상태를 확인하는 데 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-106">Performance counters available for Windows Server, IIS, and ASP.NET can also be collected and used to determine the health of your Azure web roles, worker roles, and Virtual Machines.</span></span> <span data-ttu-id="31e43-107">사용자 지정 성능 카운터를 만들고 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-107">You can also create and use custom performance counters.</span></span>  

<span data-ttu-id="31e43-108">성능 카운터 데이터를 다음과 같이 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-108">You can examine performance counter data</span></span>

1. <span data-ttu-id="31e43-109">원격 데스크톱을 사용하여 액세스된 성능 모니터 도구와 응용 프로그램 호스트에서 직접</span><span class="sxs-lookup"><span data-stu-id="31e43-109">Directly on the application host with the Performance Monitor tool accessed using Remote Desktop</span></span>
2. <span data-ttu-id="31e43-110">Azure 관리 팩을 사용하여 System Center Operations Manager를 통해</span><span class="sxs-lookup"><span data-stu-id="31e43-110">With System Center Operations Manager using the Azure Management Pack</span></span>
3. <span data-ttu-id="31e43-111">Azure 저장소로 전송되는 진단 데이터에 액세스하는 다른 모니터링 도구를 통해.</span><span class="sxs-lookup"><span data-stu-id="31e43-111">With other monitoring tools that access the diagnostic data transferred to Azure storage.</span></span> <span data-ttu-id="31e43-112">자세한 내용은 [Azure 저장소에서 진단 데이터 저장 및 보기](https://msdn.microsoft.com/library/azure/hh411534.aspx) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31e43-112">See [Store and View Diagnostic Data in Azure Storage](https://msdn.microsoft.com/library/azure/hh411534.aspx) for more information.</span></span>  

<span data-ttu-id="31e43-113">[Azure Portal](http://portal.azure.com/)에서의 응용 프로그램 성능 모니터링에 대한 내용은 [클라우드 서비스를 모니터링하는 방법](https://www.azure.com/manage/services/cloud-services/how-to-monitor-a-cloud-service/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31e43-113">For more information on monitoring the performance of your application in the [Azure portal](http://portal.azure.com/), see [How to Monitor Cloud Services](https://www.azure.com/manage/services/cloud-services/how-to-monitor-a-cloud-service/).</span></span>

<span data-ttu-id="31e43-114">문제를 해결하고 Azure 응용 프로그램을 최적화하기 위한 로깅 및 추적 전략 만들기와 진단 및 기타 기술 사용에 대한 더 많은 세부 지침은 [Azure 응용 프로그램 개발 문제 해결 모범 사례](https://msdn.microsoft.com/library/azure/hh771389.aspx)(영문)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="31e43-114">For additional in-depth guidance on creating a logging and tracing strategy and using diagnostics and other techniques to troubleshoot problems and optimize Azure applications, see [Troubleshooting Best Practices for Developing Azure Applications](https://msdn.microsoft.com/library/azure/hh771389.aspx).</span></span>

## <a name="enable-performance-counter-monitoring"></a><span data-ttu-id="31e43-115">성능 카운터 모니터링 사용</span><span class="sxs-lookup"><span data-stu-id="31e43-115">Enable performance counter monitoring</span></span>
<span data-ttu-id="31e43-116">성능 카운터는 기본적으로 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-116">Performance counters are not enabled by default.</span></span> <span data-ttu-id="31e43-117">응용 프로그램 또는 시작 작업은 각 역할 인스턴스에 대해 모니터링하려는 특정 성능 카운터를 포함하도록 기본 진단 에이전트 구성을 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-117">Your application or a startup task must modify the default diagnostics agent configuration to include the specific performance counters that you wish to monitor for each role instance.</span></span>

### <a name="performance-counters-available-for-microsoft-azure"></a><span data-ttu-id="31e43-118">Microsoft Azure에 사용할 수 있는 성능 카운터</span><span class="sxs-lookup"><span data-stu-id="31e43-118">Performance counters available for Microsoft Azure</span></span>
<span data-ttu-id="31e43-119">Azure는 Windows Server, IIS 및 ASP.NET 스택에 사용할 수 있는 성능 카운터의 하위 집합을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-119">Azure provides a subset of the performance counters available for Windows Server, IIS and the ASP.NET stack.</span></span> <span data-ttu-id="31e43-120">다음 표에서 Azure 응용 프로그램에 대한 특정 관심의 성능 카운터 중 일부를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-120">The following table lists some of the performance counters of particular interest for Azure applications.</span></span>

| <span data-ttu-id="31e43-121">카운터 범주: 개체(인스턴스)</span><span class="sxs-lookup"><span data-stu-id="31e43-121">Counter Category: Object (Instance)</span></span> | <span data-ttu-id="31e43-122">카운터 이름</span><span class="sxs-lookup"><span data-stu-id="31e43-122">Counter Name</span></span> | <span data-ttu-id="31e43-123">참조</span><span class="sxs-lookup"><span data-stu-id="31e43-123">Reference</span></span> |
| --- | --- | --- |
| <span data-ttu-id="31e43-124">.NET CLR Exceptions(*Global*)</span><span class="sxs-lookup"><span data-stu-id="31e43-124">.NET CLR Exceptions(*Global*)</span></span> |<span data-ttu-id="31e43-125"># Exceps Thrown / sec</span><span class="sxs-lookup"><span data-stu-id="31e43-125"># Exceps Thrown / sec</span></span> |<span data-ttu-id="31e43-126">예외 성능 카운터</span><span class="sxs-lookup"><span data-stu-id="31e43-126">Exception Performance Counters</span></span> |
| <span data-ttu-id="31e43-127">.NET CLR Memory(*Global*)</span><span class="sxs-lookup"><span data-stu-id="31e43-127">.NET CLR Memory(*Global*)</span></span> |<span data-ttu-id="31e43-128">% Time in GC</span><span class="sxs-lookup"><span data-stu-id="31e43-128">% Time in GC</span></span> |<span data-ttu-id="31e43-129">메모리 성능 카운터</span><span class="sxs-lookup"><span data-stu-id="31e43-129">Memory Performance Counters</span></span> |
| <span data-ttu-id="31e43-130">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="31e43-130">ASP.NET</span></span> |<span data-ttu-id="31e43-131">응용 프로그램 다시 시작</span><span class="sxs-lookup"><span data-stu-id="31e43-131">Application Restarts</span></span> |<span data-ttu-id="31e43-132">ASP.NET용 성능 카운터</span><span class="sxs-lookup"><span data-stu-id="31e43-132">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="31e43-133">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="31e43-133">ASP.NET</span></span> |<span data-ttu-id="31e43-134">요청 실행 시간</span><span class="sxs-lookup"><span data-stu-id="31e43-134">Request Execution Time</span></span> |<span data-ttu-id="31e43-135">ASP.NET용 성능 카운터</span><span class="sxs-lookup"><span data-stu-id="31e43-135">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="31e43-136">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="31e43-136">ASP.NET</span></span> |<span data-ttu-id="31e43-137">요청이 끊김</span><span class="sxs-lookup"><span data-stu-id="31e43-137">Requests Disconnected</span></span> |<span data-ttu-id="31e43-138">ASP.NET용 성능 카운터</span><span class="sxs-lookup"><span data-stu-id="31e43-138">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="31e43-139">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="31e43-139">ASP.NET</span></span> |<span data-ttu-id="31e43-140">작업자 프로세스 다시 시작</span><span class="sxs-lookup"><span data-stu-id="31e43-140">Worker Process Restarts</span></span> |<span data-ttu-id="31e43-141">ASP.NET용 성능 카운터</span><span class="sxs-lookup"><span data-stu-id="31e43-141">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="31e43-142">ASP.NET Applications(**Total**)</span><span class="sxs-lookup"><span data-stu-id="31e43-142">ASP.NET Applications(**Total**)</span></span> |<span data-ttu-id="31e43-143">총 요청 수</span><span class="sxs-lookup"><span data-stu-id="31e43-143">Requests Total</span></span> |<span data-ttu-id="31e43-144">ASP.NET용 성능 카운터</span><span class="sxs-lookup"><span data-stu-id="31e43-144">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="31e43-145">ASP.NET Applications(**Total**)</span><span class="sxs-lookup"><span data-stu-id="31e43-145">ASP.NET Applications(**Total**)</span></span> |<span data-ttu-id="31e43-146">Requests/Sec</span><span class="sxs-lookup"><span data-stu-id="31e43-146">Requests/Sec</span></span> |<span data-ttu-id="31e43-147">ASP.NET용 성능 카운터</span><span class="sxs-lookup"><span data-stu-id="31e43-147">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="31e43-148">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="31e43-148">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="31e43-149">요청 실행 시간</span><span class="sxs-lookup"><span data-stu-id="31e43-149">Request Execution Time</span></span> |<span data-ttu-id="31e43-150">ASP.NET용 성능 카운터</span><span class="sxs-lookup"><span data-stu-id="31e43-150">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="31e43-151">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="31e43-151">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="31e43-152">요청 대기 시간</span><span class="sxs-lookup"><span data-stu-id="31e43-152">Request Wait Time</span></span> |<span data-ttu-id="31e43-153">ASP.NET용 성능 카운터</span><span class="sxs-lookup"><span data-stu-id="31e43-153">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="31e43-154">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="31e43-154">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="31e43-155">현재 요청</span><span class="sxs-lookup"><span data-stu-id="31e43-155">Requests Current</span></span> |<span data-ttu-id="31e43-156">ASP.NET용 성능 카운터</span><span class="sxs-lookup"><span data-stu-id="31e43-156">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="31e43-157">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="31e43-157">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="31e43-158">대기 중인 요청</span><span class="sxs-lookup"><span data-stu-id="31e43-158">Requests Queued</span></span> |<span data-ttu-id="31e43-159">ASP.NET용 성능 카운터</span><span class="sxs-lookup"><span data-stu-id="31e43-159">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="31e43-160">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="31e43-160">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="31e43-161">거부된 요청</span><span class="sxs-lookup"><span data-stu-id="31e43-161">Requests Rejected</span></span> |<span data-ttu-id="31e43-162">ASP.NET용 성능 카운터</span><span class="sxs-lookup"><span data-stu-id="31e43-162">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="31e43-163">메모리</span><span class="sxs-lookup"><span data-stu-id="31e43-163">Memory</span></span> |<span data-ttu-id="31e43-164">Available MBytes</span><span class="sxs-lookup"><span data-stu-id="31e43-164">Available MBytes</span></span> |<span data-ttu-id="31e43-165">메모리 성능 카운터</span><span class="sxs-lookup"><span data-stu-id="31e43-165">Memory Performance Counters</span></span> |
| <span data-ttu-id="31e43-166">메모리</span><span class="sxs-lookup"><span data-stu-id="31e43-166">Memory</span></span> |<span data-ttu-id="31e43-167">커밋된 바이트</span><span class="sxs-lookup"><span data-stu-id="31e43-167">Committed Bytes</span></span> |<span data-ttu-id="31e43-168">메모리 성능 카운터</span><span class="sxs-lookup"><span data-stu-id="31e43-168">Memory Performance Counters</span></span> |
| <span data-ttu-id="31e43-169">Processor(_Total)</span><span class="sxs-lookup"><span data-stu-id="31e43-169">Processor(_Total)</span></span> |<span data-ttu-id="31e43-170">% Processor Time</span><span class="sxs-lookup"><span data-stu-id="31e43-170">% Processor Time</span></span> |<span data-ttu-id="31e43-171">ASP.NET용 성능 카운터</span><span class="sxs-lookup"><span data-stu-id="31e43-171">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="31e43-172">TCPv4</span><span class="sxs-lookup"><span data-stu-id="31e43-172">TCPv4</span></span> |<span data-ttu-id="31e43-173">연결 오류</span><span class="sxs-lookup"><span data-stu-id="31e43-173">Connection Failures</span></span> |<span data-ttu-id="31e43-174">TCP Object</span><span class="sxs-lookup"><span data-stu-id="31e43-174">TCP Object</span></span> |
| <span data-ttu-id="31e43-175">TCPv4</span><span class="sxs-lookup"><span data-stu-id="31e43-175">TCPv4</span></span> |<span data-ttu-id="31e43-176">Connections Established</span><span class="sxs-lookup"><span data-stu-id="31e43-176">Connections Established</span></span> |<span data-ttu-id="31e43-177">TCP Object</span><span class="sxs-lookup"><span data-stu-id="31e43-177">TCP Object</span></span> |
| <span data-ttu-id="31e43-178">TCPv4</span><span class="sxs-lookup"><span data-stu-id="31e43-178">TCPv4</span></span> |<span data-ttu-id="31e43-179">Connections Reset</span><span class="sxs-lookup"><span data-stu-id="31e43-179">Connections Reset</span></span> |<span data-ttu-id="31e43-180">TCP Object</span><span class="sxs-lookup"><span data-stu-id="31e43-180">TCP Object</span></span> |
| <span data-ttu-id="31e43-181">TCPv4</span><span class="sxs-lookup"><span data-stu-id="31e43-181">TCPv4</span></span> |<span data-ttu-id="31e43-182">Segments Sent/sec</span><span class="sxs-lookup"><span data-stu-id="31e43-182">Segments Sent/sec</span></span> |<span data-ttu-id="31e43-183">TCP Object</span><span class="sxs-lookup"><span data-stu-id="31e43-183">TCP Object</span></span> |
| <span data-ttu-id="31e43-184">Network Interface(*)</span><span class="sxs-lookup"><span data-stu-id="31e43-184">Network Interface(*)</span></span> |<span data-ttu-id="31e43-185">Bytes Received/sec</span><span class="sxs-lookup"><span data-stu-id="31e43-185">Bytes Received/sec</span></span> |<span data-ttu-id="31e43-186">Network Interface Object</span><span class="sxs-lookup"><span data-stu-id="31e43-186">Network Interface Object</span></span> |
| <span data-ttu-id="31e43-187">Network Interface(*)</span><span class="sxs-lookup"><span data-stu-id="31e43-187">Network Interface(*)</span></span> |<span data-ttu-id="31e43-188">Bytes Sent/sec</span><span class="sxs-lookup"><span data-stu-id="31e43-188">Bytes Sent/sec</span></span> |<span data-ttu-id="31e43-189">Network Interface Object</span><span class="sxs-lookup"><span data-stu-id="31e43-189">Network Interface Object</span></span> |
| <span data-ttu-id="31e43-190">Network Interface(Microsoft Virtual Machine Bus Network Adapter _2)</span><span class="sxs-lookup"><span data-stu-id="31e43-190">Network Interface(Microsoft Virtual Machine Bus Network Adapter _2)</span></span> |<span data-ttu-id="31e43-191">Bytes Received/sec</span><span class="sxs-lookup"><span data-stu-id="31e43-191">Bytes Received/sec</span></span> |<span data-ttu-id="31e43-192">Network Interface Object</span><span class="sxs-lookup"><span data-stu-id="31e43-192">Network Interface Object</span></span> |
| <span data-ttu-id="31e43-193">Network Interface(Microsoft Virtual Machine Bus Network Adapter _2)</span><span class="sxs-lookup"><span data-stu-id="31e43-193">Network Interface(Microsoft Virtual Machine Bus Network Adapter _2)</span></span> |<span data-ttu-id="31e43-194">Bytes Sent/sec</span><span class="sxs-lookup"><span data-stu-id="31e43-194">Bytes Sent/sec</span></span> |<span data-ttu-id="31e43-195">Network Interface Object</span><span class="sxs-lookup"><span data-stu-id="31e43-195">Network Interface Object</span></span> |
| <span data-ttu-id="31e43-196">Network Interface(Microsoft Virtual Machine Bus Network Adapter _2)</span><span class="sxs-lookup"><span data-stu-id="31e43-196">Network Interface(Microsoft Virtual Machine Bus Network Adapter _2)</span></span> |<span data-ttu-id="31e43-197">Bytes Total/sec</span><span class="sxs-lookup"><span data-stu-id="31e43-197">Bytes Total/sec</span></span> |<span data-ttu-id="31e43-198">Network Interface Object</span><span class="sxs-lookup"><span data-stu-id="31e43-198">Network Interface Object</span></span> |

## <a name="create-and-add-custom-performance-counters-to-your-application"></a><span data-ttu-id="31e43-199">응용 프로그램에 사용자 지정 성능 카운터 만들기 및 추가</span><span class="sxs-lookup"><span data-stu-id="31e43-199">Create and add custom performance counters to your application</span></span>
<span data-ttu-id="31e43-200">Azure는 웹 역할 및 작업자 역할에 대한 사용자 지정 성능 카운터 만들기 및 수정에 대해 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-200">Azure has support to create and modify custom performance counters for web roles and worker roles.</span></span> <span data-ttu-id="31e43-201">카운터는 응용 프로그램 관련 동작을 추적하고 모니터링하는 데 사용될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-201">The counters may be used to track and monitor application-specific behavior.</span></span> <span data-ttu-id="31e43-202">승격된 권한으로 시작 작업, 웹 역할 또는 작업자 역할에서 사용자 지정 성능 카운터 범주 및 지정자를 만들고 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-202">You can create and delete custom performance counter categories and specifiers from a startup task, web role, or worker role with elevated permissions.</span></span>

> [!NOTE]
> <span data-ttu-id="31e43-203">사용자 지정 성능 카운터를 변경하는 코드에는 실행할 승격된 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-203">Code that makes changes to custom performance counters must have elevated permissions to run.</span></span> <span data-ttu-id="31e43-204">코드가 웹 역할 또는 작업자 역할에 있는 경우 역할은 올바르게 초기화하기 위해 ServiceDefinition.csdef 파일에 <Runtime executionContext="elevated" /> 태그를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-204">If the code is in a web role or worker role, the role must include the tag <Runtime executionContext="elevated" /> in the ServiceDefinition.csdef file for the role to initialize properly.</span></span>
>
>

<span data-ttu-id="31e43-205">진단 에이전트를 사용하여 Azure 저장소에 사용자 지정 성능 카운터 데이터를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-205">You can send custom performance counter data to Azure storage using the diagnostics agent.</span></span>

<span data-ttu-id="31e43-206">표준 성능 카운터 데이터는 Azure 프로세스에 의해 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-206">The standard performance counter data is generated by the Azure processes.</span></span> <span data-ttu-id="31e43-207">웹 역할 또는 작업자 역할 응용 프로그램에서 사용자 지정 성능 카운터 데이터를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-207">Custom performance counter data must be created by your web role or worker role application.</span></span> <span data-ttu-id="31e43-208">사용자 지정 성능 카운터에 저장할 수 있는 데이터의 형식에 대한 정보는 [성능 카운터 형식](https://msdn.microsoft.com/library/z573042h.aspx) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31e43-208">See [Performance Counter Types](https://msdn.microsoft.com/library/z573042h.aspx) for information on the types of data that can be stored in custom performance counters.</span></span> <span data-ttu-id="31e43-209">웹 역할에서 사용자 지정 성능 카운터 데이터를 만들고 설정하는 예제는 [PerformanceCounters 샘플](http://code.msdn.microsoft.com/azure/) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31e43-209">See [PerformanceCounters Sample](http://code.msdn.microsoft.com/azure/) for an example that creates and sets custom performance counter data in a web role.</span></span>

## <a name="store-and-view-performance-counter-data"></a><span data-ttu-id="31e43-210">성능 카운터 데이터 저장 및 보기</span><span class="sxs-lookup"><span data-stu-id="31e43-210">Store and view performance counter data</span></span>
<span data-ttu-id="31e43-211">Azure는 기타 진단 정보와 함께 성능 카운터 데이터를 캐시합니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-211">Azure caches performance counter data with other diagnostic information.</span></span> <span data-ttu-id="31e43-212">이 데이터는 성능 모니터와 같은 도구를 보기 위해 원격 데스크톱 액세스를 사용하여 역할 인스턴스가 실행되는 동안 원격 모니터링에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-212">This data is available for remote monitoring while the role instance is running using remote desktop access to view tools such as Performance Monitor.</span></span> <span data-ttu-id="31e43-213">역할 인스턴스 외부의 데이터를 유지하려면 진단 에이전트가 Azure 저장소에 데이터를 전송해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-213">To persist the data outside of the role instance, the diagnostics agent must transfer the data to Azure storage.</span></span> <span data-ttu-id="31e43-214">캐시된 성능 카운터 데이터의 크기 제한은 진단 에이전트에서 구성될 수 있거나 모든 진단 데이터에 대한 공유 제한의 일부가 되도록 구성될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-214">The size limit of the cached performance counter data can be configured in the diagnostics agent, or it may be configured to be part of a shared limit for all the diagnostic data.</span></span> <span data-ttu-id="31e43-215">버퍼 크기 설정에 대한 자세한 내용은 [OverallQuotaInMB](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitorconfiguration.overallquotainmb.aspx) 및 [DirectoriesBufferConfiguration](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.directoriesbufferconfiguration.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31e43-215">For more information about setting the buffer size, see [OverallQuotaInMB](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitorconfiguration.overallquotainmb.aspx) and [DirectoriesBufferConfiguration](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.directoriesbufferconfiguration.aspx).</span></span> <span data-ttu-id="31e43-216">저장소 계정에 데이터를 전송하도록 진단 에이전트 설정에 대한 개요는 [Azure 저장소에서 진단 데이터 저장 및 보기](https://msdn.microsoft.com/library/azure/hh411534.aspx) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31e43-216">See [Store and View Diagnostic Data in Azure Storage](https://msdn.microsoft.com/library/azure/hh411534.aspx) for an overview of setting up the diagnostics agent to transfer data to a storage account.</span></span>

<span data-ttu-id="31e43-217">구성된 각 성능 카운터 인스턴스는 지정된 샘플링 속도로 기록되고 샘플링된 데이터는 예약된 전송 요청 또는 주문형 전송 요청으로 저장소 계정에 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-217">Each configured performance counter instance is recorded at a specified sampling rate, and the sampled data is transferred to the storage account either by a scheduled transfer request or an on-demand transfer request.</span></span> <span data-ttu-id="31e43-218">자동 전송은 매 분마다 예약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-218">Automatic transfers may be scheduled as often as once per minute.</span></span> <span data-ttu-id="31e43-219">진단 에이전트에 의해 전송된 성능 카운터 데이터는 저장소 계정의 테이블, WADPerformanceCountersTable에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-219">Performance counter data transferred by the diagnostics agent is stored in a table, WADPerformanceCountersTable, in the storage account.</span></span> <span data-ttu-id="31e43-220">표준 Azure 저장소 API 메서드를 사용하여 이 테이블에 액세스 및 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-220">This table may be accessed and queried with standard Azure storage API methods.</span></span> <span data-ttu-id="31e43-221">WADPerformanceCountersTable 테이블에서 성능 카운터 데이터 쿼리 및 표시의 예제는 [Microsoft Azure PerformanceCounters 샘플](http://code.msdn.microsoft.com/Windows-Azure-PerformanceCo-7d80ebf9) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31e43-221">See [Microsoft Azure PerformanceCounters Sample](http://code.msdn.microsoft.com/Windows-Azure-PerformanceCo-7d80ebf9) for an example of querying and displaying performance counter data from the WADPerformanceCountersTable table.</span></span>

> [!NOTE]
> <span data-ttu-id="31e43-222">진단 에이전트 전송 빈도 및 큐 대기 시간에 따라 저장소 계정의 가장 최근 성능 카운터 데이터는 몇 분 정도 지연될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-222">Depending on the diagnostics agent transfer frequency and queue latency, the most recent performance counter data in the storage account may be several minutes out of date.</span></span>
>
>

## <a name="enable-performance-counters-using-diagnostics-configuration-file"></a><span data-ttu-id="31e43-223">진단 구성 파일을 사용하여 성능 카운터를 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="31e43-223">Enable performance counters using diagnostics configuration file</span></span>
<span data-ttu-id="31e43-224">다음 절차를 사용하여 Azure 응용 프로그램에서 성능 카운터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-224">Use the following procedure to enable performance counters in your Azure application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="31e43-225">필수 조건</span><span class="sxs-lookup"><span data-stu-id="31e43-225">Prerequisites</span></span>
<span data-ttu-id="31e43-226">이 섹션은 진단 모니터를 응용 프로그램으로 가져왔으며 진단 구성 파일을 Visual Studio 솔루션에 추가했다고 가정합니다(SDK 2.4 이하에서 diagnostics.wadcfg 또는 SDK 2.5 이상에서 diagnostics.wadcfgx).</span><span class="sxs-lookup"><span data-stu-id="31e43-226">This section assumes that you have imported the Diagnostics monitor into your application and added the diagnostics configuration file to your Visual Studio solution (diagnostics.wadcfg in SDK 2.4 and below or diagnostics.wadcfgx in SDK 2.5 and above).</span></span> <span data-ttu-id="31e43-227">자세한 내용은 [Azure 클라우드 서비스 및 Virtual Machine에서 진단 사용](cloud-services-dotnet-diagnostics.md))의 1, 2단계를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31e43-227">See steps 1 and 2 in [Enabling Diagnostics in Azure Cloud Services and Virtual Machines](cloud-services-dotnet-diagnostics.md)) for more information.</span></span>

## <a name="step-1-collect-and-store-data-from-performance-counters"></a><span data-ttu-id="31e43-228">1단계: 성능 카운터에서 데이터 수집 및 저장</span><span class="sxs-lookup"><span data-stu-id="31e43-228">Step 1: Collect and store data from performance counters</span></span>
<span data-ttu-id="31e43-229">진단 파일을 Visual Studio 솔루션에 추가하면 Azure 응용 프로그램에서 성능 카운터 데이터의 수집 및 저장을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-229">After you have added the diagnostics file to your Visual Studio solution, you can configure the collection and storage of performance counter data in an Azure application.</span></span> <span data-ttu-id="31e43-230">이렇게 하려면 성능 카운터를 진단 파일에 추가하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-230">This is done by adding performance counters to the diagnostics file.</span></span> <span data-ttu-id="31e43-231">성능 카운터를 포함한 진단 데이터는 인스턴스에서 먼저 수집됩니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-231">Diagnostics data, including performance counters, is first collected on the instance.</span></span> <span data-ttu-id="31e43-232">그런 다음 그 데이터는 Azure 테이블 서비스의 WADPerformanceCountersTable 테이블에 보관되므로 응용 프로그램에서 저장소 계정도 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-232">The data is then persisted to the WADPerformanceCountersTable table in the Azure Table service, so you will also need to specify the storage account in your application.</span></span> <span data-ttu-id="31e43-233">계산 에뮬레이터에서 응용 프로그램을 로컬로 테스트하는 중이면 진단 데이터도 저장소 에뮬레이터에 로컬로 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-233">If you're testing your application locally in the Compute Emulator, you can also store diagnostics data locally in the Storage Emulator.</span></span> <span data-ttu-id="31e43-234">진단 데이터를 저장하기 전에 먼저 [Azure Portal](http://portal.azure.com/)로 이동하여 클래식 저장소 계정을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-234">Before you store diagnostics data, you must first go to the [Azure portal](http://portal.azure.com/) and create a classic storage account.</span></span> <span data-ttu-id="31e43-235">Azure 응용 프로그램과 동일한 지리적 위치에 저장소 계정을 두는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-235">A best practice is to locate your storage account in the same geo-location as your Azure application.</span></span> <span data-ttu-id="31e43-236">Azure 응용 프로그램 및 저장소 계정을 동일한 지리적 위치에 두면 외부 대역폭 비용을 지불하지 않고 지연 시간도 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-236">By keeping the Azure application and storage account are in the same geo-location, you avoid paying external bandwidth costs and reduce latency.</span></span>

### <a name="add-performance-counters-to-the-diagnostics-file"></a><span data-ttu-id="31e43-237">진단 파일에 성능 카운터 추가</span><span class="sxs-lookup"><span data-stu-id="31e43-237">Add performance counters to the diagnostics file</span></span>
<span data-ttu-id="31e43-238">사용할 수 있는 카운터가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-238">There are many counters you can use.</span></span> <span data-ttu-id="31e43-239">다음 예제는 웹 및 작업자 역할 모니터링에 권장되는 일부 성능 카운터를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-239">The following example shows several performance counters that are recommended for web and worker role monitoring.</span></span>

<span data-ttu-id="31e43-240">진단 파일(SDK 2.4 이하에서 diagnostics.wadcfg 또는 SDK 2.5 이상에서 diagnostics.wadcfgx)을 열고 다음을 DiagnosticMonitorConfiguration 요소에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-240">Open the diagnostics file (diagnostics.wadcfg in SDK 2.4 and below or diagnostics.wadcfgx in SDK 2.5 and above) and add the following to the DiagnosticMonitorConfiguration element:</span></span>

```xml
<PerformanceCounters bufferQuotaInMB="0" scheduledTransferPeriod="PT30M">
    <PerformanceCounterConfiguration counterSpecifier="\Memory\Available Bytes" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT30S" />

    <!-- Use the Process(w3wp) category counters in a web role -->

    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\% Processor Time" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\Private Bytes" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\Thread Count" sampleRate="PT30S" />

    <!-- Use the Process(WaWorkerHost) category counters in a worker role.
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

<span data-ttu-id="31e43-241">bufferQuotaInMB 특성은 데이터 수집 형식(Azure 로그, IIS 로그 등)에 사용할 수 있는 파일 시스템 저장소의 최대량을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-241">The bufferQuotaInMB attribute, which specifies the maximum amount of file system storage that is available for the data collection type (Azure logs, IIS logs, etc.).</span></span> <span data-ttu-id="31e43-242">기본값은 0입니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-242">The default is 0.</span></span> <span data-ttu-id="31e43-243">할당량에 도달하면 새 데이터가 추가될 때 가장 오래된 데이터가 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-243">When the quota is reached, the oldest data is deleted as new data is added.</span></span> <span data-ttu-id="31e43-244">모든 bufferQuotaInMB 속성의 합계는 OverallQuotaInMB 특성 값보다 커야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-244">The sum of all the bufferQuotaInMB properties must be greater than the value of the OverallQuotaInMB attribute.</span></span> <span data-ttu-id="31e43-245">진단 데이터를 수집하는 데 필요한 저장소 양을 결정하는 자세한 논의는 [Azure 응용 프로그램 개발 문제 해결 모범 사례](https://msdn.microsoft.com/library/windowsazure/hh771389.aspx)(영문)의 WAD 설정 섹션을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="31e43-245">For a more detailed discussion of determining how much storage will be required for the collection of diagnostics data, see the Setup WAD section of [Troubleshooting Best Practices for Developing Azure Applications](https://msdn.microsoft.com/library/windowsazure/hh771389.aspx).</span></span>

<span data-ttu-id="31e43-246">scheduledTransferPeriod 특성은 데이터의 예약 전송 사이의 간격을 지정합니다(가장 가까운 시간(분)으로 반올림됨).</span><span class="sxs-lookup"><span data-stu-id="31e43-246">The scheduledTransferPeriod attribute, which specifies the interval between scheduled transfers of data, rounded up to the nearest minute.</span></span> <span data-ttu-id="31e43-247">다음 예제에서는 PT30M(30분)으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-247">In the following examples, it is set to PT30M (30 minutes).</span></span> <span data-ttu-id="31e43-248">전송 간격을 1분처럼 작은 값으로 설정하면 프로덕션에서 응용 프로그램의 성능에 악영향을 주지만 테스트할 때 진단 작업을 빠르게 보는 데는 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-248">Setting the transfer period to a small value, such as 1 minute, will adversely impact your application's performance in production but can be useful for seeing diagnostics working quickly when you are testing.</span></span> <span data-ttu-id="31e43-249">예약 전송 간격은 인스턴스에서 진단 데이터를 덮어쓰지 않을 정도로 작고 응용 프로그램의 성능에 영향을 주지 않을 정도로 커야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-249">The scheduled transfer period should be small enough to ensure that diagnostic data is not overwritten on the instance, but large enough that it will not impact the performance of your application.</span></span>

<span data-ttu-id="31e43-250">counterSpecifier 특성은 수집할 성능 카운터를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-250">The counterSpecifier attribute specifies the performance counter to collect.</span></span> <span data-ttu-id="31e43-251">sampleRate 특성은 성능 카운터가 샘플링되어야 하는 속도를 지정합니다(이 경우 30초).</span><span class="sxs-lookup"><span data-stu-id="31e43-251">The sampleRate attribute specifies the rate at which the performance counter should be sampled, in this case 30 seconds.</span></span>

<span data-ttu-id="31e43-252">수집할 성능 카운터를 추가했으면 변경 내용을 진단 파일에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-252">Once you've added the performance counters that you want to collect, save your changes to the diagnostics file.</span></span> <span data-ttu-id="31e43-253">그 다음에 진단 데이터를 보관할 저장소 계정을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-253">Next, you need to specify the storage account that the diagnostics data will be persisted to.</span></span>

### <a name="specify-the-storage-account"></a><span data-ttu-id="31e43-254">저장소 계정 지정</span><span class="sxs-lookup"><span data-stu-id="31e43-254">Specify the storage account</span></span>
<span data-ttu-id="31e43-255">진단 정보를 Azure 저장소 계정에 보관하려면 서비스 구성(ServiceConfiguration.cscfg) 파일에서 연결 문자열을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-255">To persist your diagnostics information to your Azure Storage account, you must specify a connection string in your service configuration (ServiceConfiguration.cscfg) file.</span></span>

<span data-ttu-id="31e43-256">Azure SDK 2.5에서는 저장소 계정이 diagnostics.wadcfgx 파일에서 지정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-256">For Azure SDK 2.5, the Storage Account can be specified in the diagnostics.wadcfgx file.</span></span>

> [!NOTE]
> <span data-ttu-id="31e43-257">이러한 지침은 Azure SDK 2.4 이하에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-257">These instructions only apply to Azure SDK 2.4 and below.</span></span> <span data-ttu-id="31e43-258">Azure SDK 2.5에서는 저장소 계정이 diagnostics.wadcfgx 파일에서 지정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-258">For Azure SDK 2.5, the Storage Account can be specified in the diagnostics.wadcfgx file.</span></span>
>
>

<span data-ttu-id="31e43-259">연결 문자열을 설정하려면</span><span class="sxs-lookup"><span data-stu-id="31e43-259">To set the connection strings:</span></span>

1. <span data-ttu-id="31e43-260">원하는 텍스트 편집기를 사용하여 ServiceConfiguration.Cloud.cscfg 파일을 열고 저장소에 대한 연결 문자열을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-260">Open the ServiceConfiguration.Cloud.cscfg file using your favorite text editor and set the connection string for your storage.</span></span> <span data-ttu-id="31e43-261">*AccountName* 및 *AccountKey* 값은 Azure Portal 저장소 계정 대시보드의 액세스 키 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-261">The *AccountName* and *AccountKey* values are found in the Azure portal in the storage account dashboard, under Access keys.</span></span>

    ```xml
    <ConfigurationSettings>
      <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="DefaultEndpointsProtocol=https;AccountName=<name>;AccountKey=<key>"/>
    </ConfigurationSettings>
    ```
2. <span data-ttu-id="31e43-262">ServiceConfiguration.Cloud.cscfg 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-262">Save the ServiceConfiguration.Cloud.cscfg file.</span></span>
3. <span data-ttu-id="31e43-263">ServiceConfiguration.Local.cscfg 파일을 열고 UseDevelopmentStorage가 true로 설정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-263">Open the ServiceConfiguration.Local.cscfg file and verify that UseDevelopmentStorage is set to true.</span></span>

    ```xml
    <ConfigurationSettings>
      <Settingname="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true"/>
    </ConfigurationSettings>
    ```
   <span data-ttu-id="31e43-264">연결 문자열이 설정되면 응용 프로그램이 배포될 때 응용 프로그램에서 진단 데이터를 저장소 계정에 보관합니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-264">Now that the connection strings are set, your application will persist diagnostics data to your storage account when your application is deployed.</span></span>
4. <span data-ttu-id="31e43-265">프로젝트를 저장하고 빌드한 다음 응용 프로그램을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-265">Save and build your project, then deploy your application.</span></span>

## <a name="step-2-optional-create-custom-performance-counters"></a><span data-ttu-id="31e43-266">2단계: (옵션) 사용자 지정 성능 카운터 만들기</span><span class="sxs-lookup"><span data-stu-id="31e43-266">Step 2: (Optional) Create custom performance counters</span></span>
<span data-ttu-id="31e43-267">미리 정의한 성능 카운터 외에도 웹 또는 작업자 역할을 모니터링하기 위해 사용자 지정 성능 카운터를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-267">In addition to the pre-defined performance counters, you can add your own custom performance counters to monitor web or worker roles.</span></span> <span data-ttu-id="31e43-268">사용자 지정 성능 카운터는 응용 프로그램별 동작을 추적하고 모니터링하는 데 사용할 수 있으며, 관리자 권한으로 시작 작업, 웹 역할 또는 작업자 역할에서 만들거나 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-268">Custom performance counters may be used to track and monitor application-specific behavior and can be created or deleted in a startup task, web role, or worker role with elevated permissions.</span></span>

<span data-ttu-id="31e43-269">Azure 진단 에이전트는 시작 1분 후 .wadcfg 파일에서 성능 카운터 구성을 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-269">The Azure diagnostics agent refreshes the performance counter configuration from the .wadcfg file one minute after starting.</span></span>  <span data-ttu-id="31e43-270">OnStart 메서드에서 사용자 지정 성능 카운터를 만드는 경우 시작 작업은 실행하는 데 1분 이상이 걸리며 Azure 진단 에이전트가 이를 로드하려는 경우 사용자 지정 성능 카운터는 만들어지지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-270">If you create custom performance counters in the OnStart method and your startup tasks take longer than one minute to execute, your custom performance counters will not have been created when the Azure Diagnostics agent tries to load them.</span></span>  <span data-ttu-id="31e43-271">이 시나리오에서는 Azure 진단이 사용자 지정 성능 카운터를 제외한 모든 진단 데이터를 올바르게 캡처하는 것을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-271">In this scenario, you will see that Azure Diagnostics correctly captures all diagnostics data except your custom performance counters.</span></span>  <span data-ttu-id="31e43-272">이 문제를 해결하려면 시작 작업에서 성능 카운터를 만들거나 성능 카운터를 만든 후 시작 작업 중 일부를 OnStart 메서드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-272">To resolve this issue, create the performance counters in a startup task or move some of your startup task work to the OnStart method after creating the performance counters.</span></span>

<span data-ttu-id="31e43-273">다음 단계를 수행하여 "\MyCustomCounterCategory\MyButton1Counter"라는 간단한 사용자 지정 성능 카운터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-273">Perform the following steps to create a simple custom performance counter named "\MyCustomCounterCategory\MyButton1Counter":</span></span>

1. <span data-ttu-id="31e43-274">응용 프로그램의 서비스 정의 파일(CSDEF)을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-274">Open the service definition file (CSDEF) for your application.</span></span>
2. <span data-ttu-id="31e43-275">Runtime 요소를 WebRole 또는 WorkerRole 요소에 추가하여 관리자 권한으로 실행할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-275">Add the Runtime element to the WebRole or WorkerRole element to allow execution with elevated privileges:</span></span>

    ```xml
    <runtime executioncontext="elevated"/>
    ```
3. <span data-ttu-id="31e43-276">파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-276">Save the file.</span></span>
4. <span data-ttu-id="31e43-277">진단 파일(SDK 2.4 이하에서 diagnostics.wadcfg 또는 SDK 2.5 이상에서 diagnostics.wadcfgx)을 열고 다음을 DiagnosticMonitorConfiguration에 추가</span><span class="sxs-lookup"><span data-stu-id="31e43-277">Open the diagnostics file (diagnostics.wadcfg in SDK 2.4 and below or diagnostics.wadcfgx in SDK 2.5 and above) and add the following to the DiagnosticMonitorConfiguration</span></span>

    ```xml
    <PerformanceCounters bufferQuotaInMB="0" scheduledTransferPeriod="PT30M">
      <PerformanceCounterConfiguration counterSpecifier="\MyCustomCounterCategory\MyButton1Counter" sampleRate="PT30S"/>
    </PerformanceCounters>
    ```
5. <span data-ttu-id="31e43-278">파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-278">Save the file.</span></span>
6. <span data-ttu-id="31e43-279">base.OnStart를 호출하기 전에 역할의 OnStart 메서드에 사용자 지정 성능 카운터 범주를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-279">Create the custom performance counter category in the OnStart method of your role, before invoking base.OnStart.</span></span> <span data-ttu-id="31e43-280">다음 C# 예제는 사용자 지정 범주가 없는 경우 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-280">The following C# example creates a custom category, if it does not already exist:</span></span>

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
7. <span data-ttu-id="31e43-281">응용 프로그램 내에서 카운터를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-281">Update the counters within your application.</span></span> <span data-ttu-id="31e43-282">다음 예제는 Button1_Click 이벤트에서 사용자 지정 성능 카운터를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-282">The following example updates a custom performance counter on Button1_Click events:</span></span>

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
8. <span data-ttu-id="31e43-283">파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-283">Save the file.</span></span>  

<span data-ttu-id="31e43-284">Azure 진단 모니터가 사용자 지정 성능 카운터 데이터를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-284">Custom performance counter data will now be collected by the Azure diagnostics monitor.</span></span>

## <a name="step-3-query-performance-counter-data"></a><span data-ttu-id="31e43-285">3단계: 성능 카운터 데이터 쿼리</span><span class="sxs-lookup"><span data-stu-id="31e43-285">Step 3: Query performance counter data</span></span>
<span data-ttu-id="31e43-286">응용 프로그램이 배포되고 진단 모니터가 실행되면 성능 카운터를 수집하여 해당 데이터를 Azure Storage에 보관하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-286">Once your application is deployed and running, the Diagnostics monitor will begin collecting performance counters and persisting that data to Azure storage.</span></span> <span data-ttu-id="31e43-287">Visual Studio의 서버 탐색기, [Azure Storage 탐색기](http://azurestorageexplorer.codeplex.com/) 또는 Cerebrata의 [Azure Diagnostics Manager](http://www.cerebrata.com/Products/AzureDiagnosticsManager/Default.aspx)와 같은 도구를 사용하여 WADPerformanceCountersTable 테이블의 성능 카운터 데이터를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-287">You use tools such as Server Explorer in Visual Studio,  [Azure Storage Explorer](http://azurestorageexplorer.codeplex.com/), or [Azure Diagnostics Manager](http://www.cerebrata.com/Products/AzureDiagnosticsManager/Default.aspx) by Cerebrata to view the performance counters data in the WADPerformanceCountersTable table.</span></span> <span data-ttu-id="31e43-288">또한 [C#](../cosmos-db/table-storage-how-to-use-dotnet.md),  [Java](../cosmos-db/table-storage-how-to-use-java.md),  [Node.js](../cosmos-db/table-storage-how-to-use-nodejs.md), [Python](../cosmos-db/table-storage-how-to-use-python.md), [Ruby](../cosmos-db/table-storage-how-to-use-ruby.md) 또는 [PHP](../cosmos-db/table-storage-how-to-use-php.md)를 사용하여 Table service를 프로그래밍 방식으로 쿼리할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-288">You can also programmatically query the Table service using [C#](../cosmos-db/table-storage-how-to-use-dotnet.md),  [Java](../cosmos-db/table-storage-how-to-use-java.md),  [Node.js](../cosmos-db/table-storage-how-to-use-nodejs.md), [Python](../cosmos-db/table-storage-how-to-use-python.md), [Ruby](../cosmos-db/table-storage-how-to-use-ruby.md), or [PHP](../cosmos-db/table-storage-how-to-use-php.md).</span></span>

<span data-ttu-id="31e43-289">다음 C# 예제는 WADPerformanceCountersTable 테이블에 대한 기본적인 쿼리를 보여 주고 진단 데이터를 CSV 파일에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-289">The following C# example shows a basic query against the WADPerformanceCountersTable table and saves the diagnostics data to a CSV file.</span></span> <span data-ttu-id="31e43-290">성능 카운터를 CSV 파일에 저장하고 나면 Microsoft Excel 또는 다른 도구의 그래픽 기능을 사용하여 데이터를 시각화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-290">Once the performance counters are saved to a CSV file, you can use the graphing capabilities in Microsoft Excel or some other tool to visualize the data.</span></span> <span data-ttu-id="31e43-291">Azure SDK for .NET 2012년 10월 이상 버전에 포함되어 있는 Microsoft.WindowsAzure.Storage.dll에 참조를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-291">Be sure to add a reference to Microsoft.WindowsAzure.Storage.dll, which is included in the Azure SDK for .NET October 2012 and later.</span></span> <span data-ttu-id="31e43-292">어셈블리는 %Program %Program Files%\Microsoft SDKs\Microsoft Azure.NET SDK\version-num\ref\ 디렉터리에 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-292">The assembly is installed to the %Program Files%\Microsoft SDKs\Microsoft Azure.NET SDK\version-num\ref\ directory.</span></span>

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
using Microsoft.WindowsAzure.Storage.Table;
...

// Get the connection string. When using Microsoft Azure Cloud Services, it is recommended
// you store your connection string using the Microsoft Azure service configuration
// system (*.csdef and *.cscfg files). You can you use the CloudConfigurationManager type
// to retrieve your storage connection string.  If you're not using Cloud Services, it's
// recommended that you store the connection string in your web.config or app.config file.
// Use the ConfigurationManager type to retrieve your storage connection string.

string connectionString = Microsoft.WindowsAzure.CloudConfigurationManager.GetSetting("StorageConnectionString");
//string connectionString = System.Configuration.ConfigurationManager.ConnectionStrings["StorageConnectionString"].ConnectionString;

// Get a reference to the storage account using the connection string.  You can also use the development
// storage account (Storage Emulator) for local debugging.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString);
//CloudStorageAccount storageAccount = CloudStorageAccount.DevelopmentStorageAccount;

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable object that represents the "WADPerformanceCountersTable" table.
CloudTable table = tableClient.GetTableReference("WADPerformanceCountersTable");

// Create the table query, filter on a specific CounterName, DeploymentId and RoleInstance.
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

// Execute the table query.
IEnumerable<PerformanceCountersEntity> result = table.ExecuteQuery(query);

// Process the query results and build a CSV file.
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

<span data-ttu-id="31e43-293">엔터티는 **TableEntity**에서 파생된 사용자 지정 클래스를 사용하여 C# 개체에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-293">Entities map to C# objects using a custom class derived from **TableEntity**.</span></span> <span data-ttu-id="31e43-294">다음 코드는 **WADPerformanceCountersTable** 테이블의 성능 카운터를 나타내는 엔터티 클래스를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="31e43-294">The following code defines an entity class that represents a performance counter in the **WADPerformanceCountersTable** table.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="31e43-295">다음 단계</span><span class="sxs-lookup"><span data-stu-id="31e43-295">Next Steps</span></span>
[<span data-ttu-id="31e43-296">Azure 진단에 대한 추가 문서 보기</span><span class="sxs-lookup"><span data-stu-id="31e43-296">View additional articles on Azure Diagnostics</span></span>](../azure-diagnostics.md)
