---
title: "Application Insights에서 사용 되는 aaaIP 주소 | Microsoft Docs"
description: "Application Insights에 필요한 서버 방화벽 예외"
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 44d989f8-bae9-40ff-bfd5-8343d3e59358
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 8/11/2017
ms.author: bwren
ms.openlocfilehash: 2c101b8da2ba9594fbff607f4f7551cda80c3c25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="ip-addresses-used-by-application-insights"></a><span data-ttu-id="88a66-103">Application Insights에 사용된 IP 주소</span><span class="sxs-lookup"><span data-stu-id="88a66-103">IP addresses used by Application Insights</span></span>
<span data-ttu-id="88a66-104">hello [Azure Application Insights](app-insights-overview.md) 서비스의 IP 주소 수를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="88a66-104">hello [Azure Application Insights](app-insights-overview.md) service uses a number of IP addresses.</span></span> <span data-ttu-id="88a66-105">모니터링 중인 hello 앱 방화벽 뒤에 있는 호스트 되는 경우 이러한 주소 tooknow 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88a66-105">You might need tooknow these addresses if hello app that you are monitoring is hosted behind a firewall.</span></span>

> [!NOTE]
> <span data-ttu-id="88a66-106">하지만 이러한 주소는 정적가 toochange 필요 합니다 시간 tootime에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="88a66-106">Although these addresses are static, it's possible that we will need toochange them from time tootime.</span></span>
> 
> 

## <a name="outgoing-ports"></a><span data-ttu-id="88a66-107">발신 포트</span><span class="sxs-lookup"><span data-stu-id="88a66-107">Outgoing ports</span></span>
<span data-ttu-id="88a66-108">일부 서버의 방화벽 tooallow hello Application Insights SDK에서에서 송신 포트 및/또는 상태 모니터 toosend 데이터 toohello 포털 tooopen 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="88a66-108">You need tooopen some outgoing ports in your server's firewall tooallow hello Application Insights SDK and/or Status Monitor toosend data toohello portal:</span></span>

| <span data-ttu-id="88a66-109">목적</span><span class="sxs-lookup"><span data-stu-id="88a66-109">Purpose</span></span> | <span data-ttu-id="88a66-110">URL</span><span class="sxs-lookup"><span data-stu-id="88a66-110">URL</span></span> | <span data-ttu-id="88a66-111">IP</span><span class="sxs-lookup"><span data-stu-id="88a66-111">IP</span></span> | <span data-ttu-id="88a66-112">포트</span><span class="sxs-lookup"><span data-stu-id="88a66-112">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="88a66-113">원격 분석</span><span class="sxs-lookup"><span data-stu-id="88a66-113">Telemetry</span></span> |<span data-ttu-id="88a66-114">dc.services.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="88a66-114">dc.services.visualstudio.com</span></span><br/><span data-ttu-id="88a66-115">dc.applicationinsights.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="88a66-115">dc.applicationinsights.microsoft.com</span></span> |<span data-ttu-id="88a66-116">40.114.241.141</span><span class="sxs-lookup"><span data-stu-id="88a66-116">40.114.241.141</span></span><br/><span data-ttu-id="88a66-117">104.45.136.42</span><span class="sxs-lookup"><span data-stu-id="88a66-117">104.45.136.42</span></span><br/><span data-ttu-id="88a66-118">40.84.189.107</span><span class="sxs-lookup"><span data-stu-id="88a66-118">40.84.189.107</span></span><br/><span data-ttu-id="88a66-119">168.63.242.221</span><span class="sxs-lookup"><span data-stu-id="88a66-119">168.63.242.221</span></span><br/><span data-ttu-id="88a66-120">52.167.221.184</span><span class="sxs-lookup"><span data-stu-id="88a66-120">52.167.221.184</span></span><br/><span data-ttu-id="88a66-121">52.169.64.244</span><span class="sxs-lookup"><span data-stu-id="88a66-121">52.169.64.244</span></span> |<span data-ttu-id="88a66-122">443</span><span class="sxs-lookup"><span data-stu-id="88a66-122">443</span></span> |
| <span data-ttu-id="88a66-123">라이브 메트릭 스트림</span><span class="sxs-lookup"><span data-stu-id="88a66-123">Live Metrics Stream</span></span> |<span data-ttu-id="88a66-124">rt.services.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="88a66-124">rt.services.visualstudio.com</span></span><br/><span data-ttu-id="88a66-125">rt.applicationinsights.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="88a66-125">rt.applicationinsights.microsoft.com</span></span> |<span data-ttu-id="88a66-126">23.96.28.38</span><span class="sxs-lookup"><span data-stu-id="88a66-126">23.96.28.38</span></span><br/><span data-ttu-id="88a66-127">13.92.40.198</span><span class="sxs-lookup"><span data-stu-id="88a66-127">13.92.40.198</span></span> |<span data-ttu-id="88a66-128">443</span><span class="sxs-lookup"><span data-stu-id="88a66-128">443</span></span> |
| <span data-ttu-id="88a66-129">내부 원격 분석</span><span class="sxs-lookup"><span data-stu-id="88a66-129">Internal Telemetry</span></span> |<span data-ttu-id="88a66-130">breeze.aimon.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="88a66-130">breeze.aimon.applicationinsights.io</span></span> |<span data-ttu-id="88a66-131">52.161.11.71</span><span class="sxs-lookup"><span data-stu-id="88a66-131">52.161.11.71</span></span> |<span data-ttu-id="88a66-132">443</span><span class="sxs-lookup"><span data-stu-id="88a66-132">443</span></span> |

## <a name="status-monitor"></a><span data-ttu-id="88a66-133">상태 모니터</span><span class="sxs-lookup"><span data-stu-id="88a66-133">Status Monitor</span></span>
<span data-ttu-id="88a66-134">상태 모니터 구성 - 변경하는 경우에만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="88a66-134">Status Monitor Configuration - needed only when making changes.</span></span>

| <span data-ttu-id="88a66-135">목적</span><span class="sxs-lookup"><span data-stu-id="88a66-135">Purpose</span></span> | <span data-ttu-id="88a66-136">URL</span><span class="sxs-lookup"><span data-stu-id="88a66-136">URL</span></span> | <span data-ttu-id="88a66-137">IP</span><span class="sxs-lookup"><span data-stu-id="88a66-137">IP</span></span> | <span data-ttu-id="88a66-138">포트</span><span class="sxs-lookup"><span data-stu-id="88a66-138">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="88a66-139">구성</span><span class="sxs-lookup"><span data-stu-id="88a66-139">Configuration</span></span> |`management.core.windows.net` | |`443` |
| <span data-ttu-id="88a66-140">구성</span><span class="sxs-lookup"><span data-stu-id="88a66-140">Configuration</span></span> |`management.azure.com` | |`443` |
| <span data-ttu-id="88a66-141">구성</span><span class="sxs-lookup"><span data-stu-id="88a66-141">Configuration</span></span> |`login.windows.net` | |`443` |
| <span data-ttu-id="88a66-142">구성</span><span class="sxs-lookup"><span data-stu-id="88a66-142">Configuration</span></span> |`login.microsoftonline.com` | |`443` |
| <span data-ttu-id="88a66-143">구성</span><span class="sxs-lookup"><span data-stu-id="88a66-143">Configuration</span></span> |`secure.aadcdn.microsoftonline-p.com` | |`443` |
| <span data-ttu-id="88a66-144">구성</span><span class="sxs-lookup"><span data-stu-id="88a66-144">Configuration</span></span> |`auth.gfx.ms` | |`443` |
| <span data-ttu-id="88a66-145">구성</span><span class="sxs-lookup"><span data-stu-id="88a66-145">Configuration</span></span> |`login.live.com` | |`443` |
| <span data-ttu-id="88a66-146">설치</span><span class="sxs-lookup"><span data-stu-id="88a66-146">Installation</span></span> |`packages.nuget.org` | |`443` |

## <a name="hockeyapp"></a><span data-ttu-id="88a66-147">HockeyApp</span><span class="sxs-lookup"><span data-stu-id="88a66-147">HockeyApp</span></span>
| <span data-ttu-id="88a66-148">목적</span><span class="sxs-lookup"><span data-stu-id="88a66-148">Purpose</span></span> | <span data-ttu-id="88a66-149">URL</span><span class="sxs-lookup"><span data-stu-id="88a66-149">URL</span></span> | <span data-ttu-id="88a66-150">IP</span><span class="sxs-lookup"><span data-stu-id="88a66-150">IP</span></span> | <span data-ttu-id="88a66-151">포트</span><span class="sxs-lookup"><span data-stu-id="88a66-151">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="88a66-152">충돌 데이터</span><span class="sxs-lookup"><span data-stu-id="88a66-152">Crash data</span></span> |<span data-ttu-id="88a66-153">gate.hockeyapp.net</span><span class="sxs-lookup"><span data-stu-id="88a66-153">gate.hockeyapp.net</span></span> |<span data-ttu-id="88a66-154">104.45.136.42</span><span class="sxs-lookup"><span data-stu-id="88a66-154">104.45.136.42</span></span> |<span data-ttu-id="88a66-155">80, 443</span><span class="sxs-lookup"><span data-stu-id="88a66-155">80, 443</span></span> |

## <a name="availability-tests"></a><span data-ttu-id="88a66-156">가용성 테스트</span><span class="sxs-lookup"><span data-stu-id="88a66-156">Availability tests</span></span>
<span data-ttu-id="88a66-157">주소를 hello 목록이 [가용성 웹 테스트](app-insights-monitor-web-app-availability.md) 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="88a66-157">This is hello list of addresses from which [availability web tests](app-insights-monitor-web-app-availability.md) are run.</span></span> <span data-ttu-id="88a66-158">Toorun 웹 테스트 응용 프로그램에서 원하는 경우 웹 서버에 있으면 제한 된 tooserving 특정 클라이언트 가용성 테스트 서버에서 들어오는 트래픽을 toopermit 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="88a66-158">If you want toorun web tests on your app, but your web server is restricted tooserving specific clients, then you will have toopermit incoming traffic from our availability test servers.</span></span>

<span data-ttu-id="88a66-159">이 주소에서 들어오는 트래픽에 대한 포트 80(http) 및 443(https)을 엽니다(IP 주소가 위치별로 그룹화됨).</span><span class="sxs-lookup"><span data-stu-id="88a66-159">Open ports 80 (http) and 443 (https) for incoming traffic from these addresses (IP addresses are grouped by location):</span></span>

```
AU : Sydney
13.70.83.252
13.75.150.96
13.75.153.9
13.75.158.185
BR : Sao Paulo
191.232.32.122
191.232.172.45
191.232.176.218
191.232.191.225
CH : Zurich
94.245.66.43
94.245.66.44
94.245.66.45
94.245.66.48
FR : Paris
94.245.72.44
94.245.72.45
94.245.72.46
94.245.72.49
94.245.72.52
94.245.72.53
HK : Hong Kong
13.75.121.122
23.99.115.153
23.99.123.38
23.102.232.186
52.175.38.49
52.175.39.103
IE : Dublin
13.74.184.101
13.74.185.160
40.69.200.198
52.164.224.46
52.169.12.203
52.169.14.11
52.169.237.149
52.178.183.105
JP : Kawaguchi
52.243.33.33
52.243.33.141
52.243.35.253
52.243.41.117
NL : Amsterdam
52.174.166.113
52.174.178.96
52.174.31.140
52.174.35.14
52.178.104.23
52.178.109.190
52.178.111.139
52.233.166.221
RU : Moscow
94.245.82.32
94.245.82.33
94.245.82.37
94.245.82.38
SE : Stockholm
94.245.78.40
94.245.78.41
94.245.78.42
94.245.78.45
SG : Singapore
52.187.29.7
52.187.179.17
52.187.76.248
52.187.43.24
52.163.57.91
52.187.30.120
US : CA-San Jose
104.45.228.236
104.45.237.251
13.64.152.110
13.64.156.54
13.64.232.251
13.64.236.105
13.91.94.59
40.118.131.182
40.83.189.192
40.83.215.122
US : FL-Miami
65.54.78.49
65.54.78.50
65.54.78.51
65.54.78.54
65.54.78.57
65.54.78.58
65.54.78.59
65.54.78.60
US : IL-Chicago
23.96.247.139
23.96.249.113
52.162.124.242
52.162.126.139
52.162.241.147
52.162.246.222
52.162.247.136
52.237.153.231
52.237.154.216
52.237.156.14
52.237.157.218
52.237.157.37
US : TX-San Antonio
104.210.145.106
13.84.176.24
13.84.49.16
13.85.11.137
13.85.26.248
13.85.69.145
52.171.136.162
52.171.141.253
52.171.57.172
52.171.58.140
US : VA-Ashburn
13.82.218.95
13.90.96.71
13.90.98.52
13.92.137.70
40.85.187.235
40.87.61.61
52.168.8.247
52.170.38.79
52.170.80.61
52.179.9.26

```  

## <a name="data-access-api"></a><span data-ttu-id="88a66-160">데이터 액세스 API</span><span class="sxs-lookup"><span data-stu-id="88a66-160">Data access API</span></span>
| <span data-ttu-id="88a66-161">목적</span><span class="sxs-lookup"><span data-stu-id="88a66-161">Purpose</span></span> | <span data-ttu-id="88a66-162">URI</span><span class="sxs-lookup"><span data-stu-id="88a66-162">URI</span></span> | <span data-ttu-id="88a66-163">IP</span><span class="sxs-lookup"><span data-stu-id="88a66-163">IP</span></span> | <span data-ttu-id="88a66-164">포트</span><span class="sxs-lookup"><span data-stu-id="88a66-164">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="88a66-165">API</span><span class="sxs-lookup"><span data-stu-id="88a66-165">API</span></span> |<span data-ttu-id="88a66-166">api.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="88a66-166">api.applicationinsights.io</span></span><br/><span data-ttu-id="88a66-167">api1.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="88a66-167">api1.applicationinsights.io</span></span><br/><span data-ttu-id="88a66-168">api2.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="88a66-168">api2.applicationinsights.io</span></span><br/><span data-ttu-id="88a66-169">api3.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="88a66-169">api3.applicationinsights.io</span></span><br/><span data-ttu-id="88a66-170">api4.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="88a66-170">api4.applicationinsights.io</span></span><br/><span data-ttu-id="88a66-171">api5.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="88a66-171">api5.applicationinsights.io</span></span> |<span data-ttu-id="88a66-172">13.82.26.252</span><span class="sxs-lookup"><span data-stu-id="88a66-172">13.82.26.252</span></span><br/><span data-ttu-id="88a66-173">40.76.213.73</span><span class="sxs-lookup"><span data-stu-id="88a66-173">40.76.213.73</span></span> |<span data-ttu-id="88a66-174">80,443</span><span class="sxs-lookup"><span data-stu-id="88a66-174">80,443</span></span> |
| <span data-ttu-id="88a66-175">API 문서</span><span class="sxs-lookup"><span data-stu-id="88a66-175">API docs</span></span> |<span data-ttu-id="88a66-176">dev.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="88a66-176">dev.applicationinsights.io</span></span><br/><span data-ttu-id="88a66-177">dev.applicationinsights.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="88a66-177">dev.applicationinsights.microsoft.com</span></span><br/><span data-ttu-id="88a66-178">dev.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="88a66-178">dev.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="88a66-179">www.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="88a66-179">www.applicationinsights.io</span></span><br/><span data-ttu-id="88a66-180">www.applicationinsights.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="88a66-180">www.applicationinsights.microsoft.com</span></span><br/><span data-ttu-id="88a66-181">www.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="88a66-181">www.aisvc.visualstudio.com</span></span> |<span data-ttu-id="88a66-182">13.82.24.149</span><span class="sxs-lookup"><span data-stu-id="88a66-182">13.82.24.149</span></span><br/><span data-ttu-id="88a66-183">40.114.82.10</span><span class="sxs-lookup"><span data-stu-id="88a66-183">40.114.82.10</span></span> |<span data-ttu-id="88a66-184">80,443</span><span class="sxs-lookup"><span data-stu-id="88a66-184">80,443</span></span> |
| <span data-ttu-id="88a66-185">내부 API</span><span class="sxs-lookup"><span data-stu-id="88a66-185">Internal API</span></span> |<span data-ttu-id="88a66-186">aigs.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="88a66-186">aigs.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="88a66-187">aigs1.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="88a66-187">aigs1.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="88a66-188">aigs2.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="88a66-188">aigs2.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="88a66-189">aigs3.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="88a66-189">aigs3.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="88a66-190">aigs4.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="88a66-190">aigs4.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="88a66-191">aigs5.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="88a66-191">aigs5.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="88a66-192">aigs6.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="88a66-192">aigs6.aisvc.visualstudio.com</span></span> |<span data-ttu-id="88a66-193">동적</span><span class="sxs-lookup"><span data-stu-id="88a66-193">dynamic</span></span>|<span data-ttu-id="88a66-194">443</span><span class="sxs-lookup"><span data-stu-id="88a66-194">443</span></span> |

## <a name="application-insights-analytics"></a><span data-ttu-id="88a66-195">Application Insights Analytics</span><span class="sxs-lookup"><span data-stu-id="88a66-195">Application Insights Analytics</span></span>

| <span data-ttu-id="88a66-196">목적</span><span class="sxs-lookup"><span data-stu-id="88a66-196">Purpose</span></span> | <span data-ttu-id="88a66-197">URI</span><span class="sxs-lookup"><span data-stu-id="88a66-197">URI</span></span> | <span data-ttu-id="88a66-198">IP</span><span class="sxs-lookup"><span data-stu-id="88a66-198">IP</span></span> | <span data-ttu-id="88a66-199">포트</span><span class="sxs-lookup"><span data-stu-id="88a66-199">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="88a66-200">분석 포털</span><span class="sxs-lookup"><span data-stu-id="88a66-200">Analytics Portal</span></span> | <span data-ttu-id="88a66-201">analytics.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="88a66-201">analytics.applicationinsights.io</span></span> | <span data-ttu-id="88a66-202">동적</span><span class="sxs-lookup"><span data-stu-id="88a66-202">dynamic</span></span> | <span data-ttu-id="88a66-203">80,443</span><span class="sxs-lookup"><span data-stu-id="88a66-203">80,443</span></span> |
| <span data-ttu-id="88a66-204">CDN</span><span class="sxs-lookup"><span data-stu-id="88a66-204">CDN</span></span> | <span data-ttu-id="88a66-205">applicationanalytics.azureedge.net</span><span class="sxs-lookup"><span data-stu-id="88a66-205">applicationanalytics.azureedge.net</span></span> | <span data-ttu-id="88a66-206">동적</span><span class="sxs-lookup"><span data-stu-id="88a66-206">dynamic</span></span> | <span data-ttu-id="88a66-207">80,443</span><span class="sxs-lookup"><span data-stu-id="88a66-207">80,443</span></span> |
| <span data-ttu-id="88a66-208">미디어 CDN</span><span class="sxs-lookup"><span data-stu-id="88a66-208">Media CDN</span></span> | <span data-ttu-id="88a66-209">applicationanalyticsmedia.azureedge.net</span><span class="sxs-lookup"><span data-stu-id="88a66-209">applicationanalyticsmedia.azureedge.net</span></span> | <span data-ttu-id="88a66-210">동적</span><span class="sxs-lookup"><span data-stu-id="88a66-210">dynamic</span></span> | <span data-ttu-id="88a66-211">80,443</span><span class="sxs-lookup"><span data-stu-id="88a66-211">80,443</span></span> |

<span data-ttu-id="88a66-212">참고: *.applicationinsights.io 도메인은 Application Insights 팀이 소유합니다.</span><span class="sxs-lookup"><span data-stu-id="88a66-212">Note: *.applicationinsights.io domain is owned by Application Insights team.</span></span>

## <a name="application-insights-azure-portal-extension"></a><span data-ttu-id="88a66-213">Application Insights Azure Portal 확장</span><span class="sxs-lookup"><span data-stu-id="88a66-213">Application Insights Azure Portal Extension</span></span>

| <span data-ttu-id="88a66-214">목적</span><span class="sxs-lookup"><span data-stu-id="88a66-214">Purpose</span></span> | <span data-ttu-id="88a66-215">URI</span><span class="sxs-lookup"><span data-stu-id="88a66-215">URI</span></span> | <span data-ttu-id="88a66-216">IP</span><span class="sxs-lookup"><span data-stu-id="88a66-216">IP</span></span> | <span data-ttu-id="88a66-217">포트</span><span class="sxs-lookup"><span data-stu-id="88a66-217">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="88a66-218">Application Insights 확장</span><span class="sxs-lookup"><span data-stu-id="88a66-218">Application Insights Extension</span></span> | <span data-ttu-id="88a66-219">stamp2.app.insightsportal.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="88a66-219">stamp2.app.insightsportal.visualstudio.com</span></span> | <span data-ttu-id="88a66-220">동적</span><span class="sxs-lookup"><span data-stu-id="88a66-220">dynamic</span></span> | <span data-ttu-id="88a66-221">80,443</span><span class="sxs-lookup"><span data-stu-id="88a66-221">80,443</span></span> |
| <span data-ttu-id="88a66-222">Application Insights 확장 CDN</span><span class="sxs-lookup"><span data-stu-id="88a66-222">Application Insights Extension CDN</span></span> | <span data-ttu-id="88a66-223">insightsportal-prod2-cdn.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="88a66-223">insightsportal-prod2-cdn.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="88a66-224">insightsportal-prod2-asiae-cdn.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="88a66-224">insightsportal-prod2-asiae-cdn.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="88a66-225">insightsportal-cdn-aimon.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="88a66-225">insightsportal-cdn-aimon.applicationinsights.io</span></span> | <span data-ttu-id="88a66-226">동적</span><span class="sxs-lookup"><span data-stu-id="88a66-226">dynamic</span></span> | <span data-ttu-id="88a66-227">80,443</span><span class="sxs-lookup"><span data-stu-id="88a66-227">80,443</span></span> |

## <a name="application-insights-sdks"></a><span data-ttu-id="88a66-228">Application Insights SDK</span><span class="sxs-lookup"><span data-stu-id="88a66-228">Application Insights SDKs</span></span>

| <span data-ttu-id="88a66-229">목적</span><span class="sxs-lookup"><span data-stu-id="88a66-229">Purpose</span></span> | <span data-ttu-id="88a66-230">URI</span><span class="sxs-lookup"><span data-stu-id="88a66-230">URI</span></span> | <span data-ttu-id="88a66-231">IP</span><span class="sxs-lookup"><span data-stu-id="88a66-231">IP</span></span> | <span data-ttu-id="88a66-232">포트</span><span class="sxs-lookup"><span data-stu-id="88a66-232">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="88a66-233">Application Insights JS SDK CDN</span><span class="sxs-lookup"><span data-stu-id="88a66-233">Application Insights JS SDK CDN</span></span> | <span data-ttu-id="88a66-234">az416426.vo.msecnd.net</span><span class="sxs-lookup"><span data-stu-id="88a66-234">az416426.vo.msecnd.net</span></span> | <span data-ttu-id="88a66-235">동적</span><span class="sxs-lookup"><span data-stu-id="88a66-235">dynamic</span></span> | <span data-ttu-id="88a66-236">80,443</span><span class="sxs-lookup"><span data-stu-id="88a66-236">80,443</span></span> |
| <span data-ttu-id="88a66-237">Application Insights Java SDK</span><span class="sxs-lookup"><span data-stu-id="88a66-237">Application Insights Java SDK</span></span> | <span data-ttu-id="88a66-238">aijavasdk.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="88a66-238">aijavasdk.blob.core.windows.net</span></span> | <span data-ttu-id="88a66-239">동적</span><span class="sxs-lookup"><span data-stu-id="88a66-239">dynamic</span></span> | <span data-ttu-id="88a66-240">80,443</span><span class="sxs-lookup"><span data-stu-id="88a66-240">80,443</span></span> |

## <a name="profiler"></a><span data-ttu-id="88a66-241">프로파일러</span><span class="sxs-lookup"><span data-stu-id="88a66-241">Profiler</span></span>

| <span data-ttu-id="88a66-242">목적</span><span class="sxs-lookup"><span data-stu-id="88a66-242">Purpose</span></span> | <span data-ttu-id="88a66-243">URI</span><span class="sxs-lookup"><span data-stu-id="88a66-243">URI</span></span> | <span data-ttu-id="88a66-244">IP</span><span class="sxs-lookup"><span data-stu-id="88a66-244">IP</span></span> | <span data-ttu-id="88a66-245">포트</span><span class="sxs-lookup"><span data-stu-id="88a66-245">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="88a66-246">에이전트</span><span class="sxs-lookup"><span data-stu-id="88a66-246">Agent</span></span> | <span data-ttu-id="88a66-247">agent.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="88a66-247">agent.azureserviceprofiler.net</span></span><br/><span data-ttu-id="88a66-248">*.agent.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="88a66-248">*.agent.azureserviceprofiler.net</span></span> | <span data-ttu-id="88a66-249">동적</span><span class="sxs-lookup"><span data-stu-id="88a66-249">dynamic</span></span> | <span data-ttu-id="88a66-250">443</span><span class="sxs-lookup"><span data-stu-id="88a66-250">443</span></span>
| <span data-ttu-id="88a66-251">포털</span><span class="sxs-lookup"><span data-stu-id="88a66-251">Portal</span></span> | <span data-ttu-id="88a66-252">gateway.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="88a66-252">gateway.azureserviceprofiler.net</span></span> | <span data-ttu-id="88a66-253">동적</span><span class="sxs-lookup"><span data-stu-id="88a66-253">dynamic</span></span> | <span data-ttu-id="88a66-254">443</span><span class="sxs-lookup"><span data-stu-id="88a66-254">443</span></span>
| <span data-ttu-id="88a66-255">저장소</span><span class="sxs-lookup"><span data-stu-id="88a66-255">Storage</span></span> | <span data-ttu-id="88a66-256">*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="88a66-256">*.core.windows.net</span></span> | <span data-ttu-id="88a66-257">동적</span><span class="sxs-lookup"><span data-stu-id="88a66-257">dynamic</span></span> | <span data-ttu-id="88a66-258">443</span><span class="sxs-lookup"><span data-stu-id="88a66-258">443</span></span>

## <a name="snapshot-debugger"></a><span data-ttu-id="88a66-259">스냅숏 디버거</span><span class="sxs-lookup"><span data-stu-id="88a66-259">Snapshot Debugger</span></span>

| <span data-ttu-id="88a66-260">목적</span><span class="sxs-lookup"><span data-stu-id="88a66-260">Purpose</span></span> | <span data-ttu-id="88a66-261">URI</span><span class="sxs-lookup"><span data-stu-id="88a66-261">URI</span></span> | <span data-ttu-id="88a66-262">IP</span><span class="sxs-lookup"><span data-stu-id="88a66-262">IP</span></span> | <span data-ttu-id="88a66-263">포트</span><span class="sxs-lookup"><span data-stu-id="88a66-263">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="88a66-264">에이전트</span><span class="sxs-lookup"><span data-stu-id="88a66-264">Agent</span></span> | <span data-ttu-id="88a66-265">ppe.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="88a66-265">ppe.azureserviceprofiler.net</span></span><br/><span data-ttu-id="88a66-266">*.ppe.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="88a66-266">*.ppe.azureserviceprofiler.net</span></span> | <span data-ttu-id="88a66-267">동적</span><span class="sxs-lookup"><span data-stu-id="88a66-267">dynamic</span></span> | <span data-ttu-id="88a66-268">443</span><span class="sxs-lookup"><span data-stu-id="88a66-268">443</span></span>
| <span data-ttu-id="88a66-269">포털</span><span class="sxs-lookup"><span data-stu-id="88a66-269">Portal</span></span> | <span data-ttu-id="88a66-270">ppe.gateway.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="88a66-270">ppe.gateway.azureserviceprofiler.net</span></span> | <span data-ttu-id="88a66-271">동적</span><span class="sxs-lookup"><span data-stu-id="88a66-271">dynamic</span></span> | <span data-ttu-id="88a66-272">443</span><span class="sxs-lookup"><span data-stu-id="88a66-272">443</span></span>
| <span data-ttu-id="88a66-273">저장소</span><span class="sxs-lookup"><span data-stu-id="88a66-273">Storage</span></span> | <span data-ttu-id="88a66-274">*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="88a66-274">*.core.windows.net</span></span> | <span data-ttu-id="88a66-275">동적</span><span class="sxs-lookup"><span data-stu-id="88a66-275">dynamic</span></span> | <span data-ttu-id="88a66-276">443</span><span class="sxs-lookup"><span data-stu-id="88a66-276">443</span></span>
