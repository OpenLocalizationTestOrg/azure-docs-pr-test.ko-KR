---
title: "Application Insights에 사용된 IP 주소 | Microsoft Docs"
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
ms.openlocfilehash: 3bb076c63223fc1567c6b7b25c1a513bbc81ed58
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="ip-addresses-used-by-application-insights"></a><span data-ttu-id="1f1ed-103">Application Insights에 사용된 IP 주소</span><span class="sxs-lookup"><span data-stu-id="1f1ed-103">IP addresses used by Application Insights</span></span>
<span data-ttu-id="1f1ed-104">[Azure Application Insights](app-insights-overview.md) 서비스는 많은 IP 주소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1f1ed-104">The [Azure Application Insights](app-insights-overview.md) service uses a number of IP addresses.</span></span> <span data-ttu-id="1f1ed-105">모니터링하는 앱이 방화벽 뒤에서 호스팅되는 경우 이러한 주소를 알아야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f1ed-105">You might need to know these addresses if the app that you are monitoring is hosted behind a firewall.</span></span>

> [!NOTE]
> <span data-ttu-id="1f1ed-106">이러한 주소는 정적이지만 경우에 따라 변경해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f1ed-106">Although these addresses are static, it's possible that we will need to change them from time to time.</span></span>
> 
> 

## <a name="outgoing-ports"></a><span data-ttu-id="1f1ed-107">발신 포트</span><span class="sxs-lookup"><span data-stu-id="1f1ed-107">Outgoing ports</span></span>
<span data-ttu-id="1f1ed-108">Application Insights SDK 및/또는 상태 모니터가 데이터를 포털에 보낼 수 있도록 서버 방화벽에서 일부 나가는 포트를 열어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f1ed-108">You need to open some outgoing ports in your server's firewall to allow the Application Insights SDK and/or Status Monitor to send data to the portal:</span></span>

| <span data-ttu-id="1f1ed-109">목적</span><span class="sxs-lookup"><span data-stu-id="1f1ed-109">Purpose</span></span> | <span data-ttu-id="1f1ed-110">URL</span><span class="sxs-lookup"><span data-stu-id="1f1ed-110">URL</span></span> | <span data-ttu-id="1f1ed-111">IP</span><span class="sxs-lookup"><span data-stu-id="1f1ed-111">IP</span></span> | <span data-ttu-id="1f1ed-112">포트</span><span class="sxs-lookup"><span data-stu-id="1f1ed-112">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1f1ed-113">원격 분석</span><span class="sxs-lookup"><span data-stu-id="1f1ed-113">Telemetry</span></span> |<span data-ttu-id="1f1ed-114">dc.services.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="1f1ed-114">dc.services.visualstudio.com</span></span><br/><span data-ttu-id="1f1ed-115">dc.applicationinsights.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="1f1ed-115">dc.applicationinsights.microsoft.com</span></span> |<span data-ttu-id="1f1ed-116">40.114.241.141</span><span class="sxs-lookup"><span data-stu-id="1f1ed-116">40.114.241.141</span></span><br/><span data-ttu-id="1f1ed-117">104.45.136.42</span><span class="sxs-lookup"><span data-stu-id="1f1ed-117">104.45.136.42</span></span><br/><span data-ttu-id="1f1ed-118">40.84.189.107</span><span class="sxs-lookup"><span data-stu-id="1f1ed-118">40.84.189.107</span></span><br/><span data-ttu-id="1f1ed-119">168.63.242.221</span><span class="sxs-lookup"><span data-stu-id="1f1ed-119">168.63.242.221</span></span><br/><span data-ttu-id="1f1ed-120">52.167.221.184</span><span class="sxs-lookup"><span data-stu-id="1f1ed-120">52.167.221.184</span></span><br/><span data-ttu-id="1f1ed-121">52.169.64.244</span><span class="sxs-lookup"><span data-stu-id="1f1ed-121">52.169.64.244</span></span> |<span data-ttu-id="1f1ed-122">443</span><span class="sxs-lookup"><span data-stu-id="1f1ed-122">443</span></span> |
| <span data-ttu-id="1f1ed-123">라이브 메트릭 스트림</span><span class="sxs-lookup"><span data-stu-id="1f1ed-123">Live Metrics Stream</span></span> |<span data-ttu-id="1f1ed-124">rt.services.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="1f1ed-124">rt.services.visualstudio.com</span></span><br/><span data-ttu-id="1f1ed-125">rt.applicationinsights.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="1f1ed-125">rt.applicationinsights.microsoft.com</span></span> |<span data-ttu-id="1f1ed-126">23.96.28.38</span><span class="sxs-lookup"><span data-stu-id="1f1ed-126">23.96.28.38</span></span><br/><span data-ttu-id="1f1ed-127">13.92.40.198</span><span class="sxs-lookup"><span data-stu-id="1f1ed-127">13.92.40.198</span></span> |<span data-ttu-id="1f1ed-128">443</span><span class="sxs-lookup"><span data-stu-id="1f1ed-128">443</span></span> |
| <span data-ttu-id="1f1ed-129">내부 원격 분석</span><span class="sxs-lookup"><span data-stu-id="1f1ed-129">Internal Telemetry</span></span> |<span data-ttu-id="1f1ed-130">breeze.aimon.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="1f1ed-130">breeze.aimon.applicationinsights.io</span></span> |<span data-ttu-id="1f1ed-131">52.161.11.71</span><span class="sxs-lookup"><span data-stu-id="1f1ed-131">52.161.11.71</span></span> |<span data-ttu-id="1f1ed-132">443</span><span class="sxs-lookup"><span data-stu-id="1f1ed-132">443</span></span> |

## <a name="status-monitor"></a><span data-ttu-id="1f1ed-133">상태 모니터</span><span class="sxs-lookup"><span data-stu-id="1f1ed-133">Status Monitor</span></span>
<span data-ttu-id="1f1ed-134">상태 모니터 구성 - 변경하는 경우에만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1f1ed-134">Status Monitor Configuration - needed only when making changes.</span></span>

| <span data-ttu-id="1f1ed-135">목적</span><span class="sxs-lookup"><span data-stu-id="1f1ed-135">Purpose</span></span> | <span data-ttu-id="1f1ed-136">URL</span><span class="sxs-lookup"><span data-stu-id="1f1ed-136">URL</span></span> | <span data-ttu-id="1f1ed-137">IP</span><span class="sxs-lookup"><span data-stu-id="1f1ed-137">IP</span></span> | <span data-ttu-id="1f1ed-138">포트</span><span class="sxs-lookup"><span data-stu-id="1f1ed-138">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1f1ed-139">구성</span><span class="sxs-lookup"><span data-stu-id="1f1ed-139">Configuration</span></span> |`management.core.windows.net` | |`443` |
| <span data-ttu-id="1f1ed-140">구성</span><span class="sxs-lookup"><span data-stu-id="1f1ed-140">Configuration</span></span> |`management.azure.com` | |`443` |
| <span data-ttu-id="1f1ed-141">구성</span><span class="sxs-lookup"><span data-stu-id="1f1ed-141">Configuration</span></span> |`login.windows.net` | |`443` |
| <span data-ttu-id="1f1ed-142">구성</span><span class="sxs-lookup"><span data-stu-id="1f1ed-142">Configuration</span></span> |`login.microsoftonline.com` | |`443` |
| <span data-ttu-id="1f1ed-143">구성</span><span class="sxs-lookup"><span data-stu-id="1f1ed-143">Configuration</span></span> |`secure.aadcdn.microsoftonline-p.com` | |`443` |
| <span data-ttu-id="1f1ed-144">구성</span><span class="sxs-lookup"><span data-stu-id="1f1ed-144">Configuration</span></span> |`auth.gfx.ms` | |`443` |
| <span data-ttu-id="1f1ed-145">구성</span><span class="sxs-lookup"><span data-stu-id="1f1ed-145">Configuration</span></span> |`login.live.com` | |`443` |
| <span data-ttu-id="1f1ed-146">설치</span><span class="sxs-lookup"><span data-stu-id="1f1ed-146">Installation</span></span> |`packages.nuget.org` | |`443` |

## <a name="hockeyapp"></a><span data-ttu-id="1f1ed-147">HockeyApp</span><span class="sxs-lookup"><span data-stu-id="1f1ed-147">HockeyApp</span></span>
| <span data-ttu-id="1f1ed-148">목적</span><span class="sxs-lookup"><span data-stu-id="1f1ed-148">Purpose</span></span> | <span data-ttu-id="1f1ed-149">URL</span><span class="sxs-lookup"><span data-stu-id="1f1ed-149">URL</span></span> | <span data-ttu-id="1f1ed-150">IP</span><span class="sxs-lookup"><span data-stu-id="1f1ed-150">IP</span></span> | <span data-ttu-id="1f1ed-151">포트</span><span class="sxs-lookup"><span data-stu-id="1f1ed-151">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1f1ed-152">충돌 데이터</span><span class="sxs-lookup"><span data-stu-id="1f1ed-152">Crash data</span></span> |<span data-ttu-id="1f1ed-153">gate.hockeyapp.net</span><span class="sxs-lookup"><span data-stu-id="1f1ed-153">gate.hockeyapp.net</span></span> |<span data-ttu-id="1f1ed-154">104.45.136.42</span><span class="sxs-lookup"><span data-stu-id="1f1ed-154">104.45.136.42</span></span> |<span data-ttu-id="1f1ed-155">80, 443</span><span class="sxs-lookup"><span data-stu-id="1f1ed-155">80, 443</span></span> |

## <a name="availability-tests"></a><span data-ttu-id="1f1ed-156">가용성 테스트</span><span class="sxs-lookup"><span data-stu-id="1f1ed-156">Availability tests</span></span>
<span data-ttu-id="1f1ed-157">[가용성 웹 테스트](app-insights-monitor-web-app-availability.md) 가 실행되는 주소 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="1f1ed-157">This is the list of addresses from which [availability web tests](app-insights-monitor-web-app-availability.md) are run.</span></span> <span data-ttu-id="1f1ed-158">앱에서 웹 테스트를 실행하려고 하지만 웹 서버가 특정 클라이언트 서비스를 제공하도록 제한된 경우 가용성 테스트 서버에서 들어오는 트래픽을 허용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f1ed-158">If you want to run web tests on your app, but your web server is restricted to serving specific clients, then you will have to permit incoming traffic from our availability test servers.</span></span>

<span data-ttu-id="1f1ed-159">이 주소에서 들어오는 트래픽에 대한 포트 80(http) 및 443(https)을 엽니다(IP 주소가 위치별로 그룹화됨).</span><span class="sxs-lookup"><span data-stu-id="1f1ed-159">Open ports 80 (http) and 443 (https) for incoming traffic from these addresses (IP addresses are grouped by location):</span></span>

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

## <a name="data-access-api"></a><span data-ttu-id="1f1ed-160">데이터 액세스 API</span><span class="sxs-lookup"><span data-stu-id="1f1ed-160">Data access API</span></span>
| <span data-ttu-id="1f1ed-161">목적</span><span class="sxs-lookup"><span data-stu-id="1f1ed-161">Purpose</span></span> | <span data-ttu-id="1f1ed-162">URI</span><span class="sxs-lookup"><span data-stu-id="1f1ed-162">URI</span></span> | <span data-ttu-id="1f1ed-163">IP</span><span class="sxs-lookup"><span data-stu-id="1f1ed-163">IP</span></span> | <span data-ttu-id="1f1ed-164">포트</span><span class="sxs-lookup"><span data-stu-id="1f1ed-164">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1f1ed-165">API</span><span class="sxs-lookup"><span data-stu-id="1f1ed-165">API</span></span> |<span data-ttu-id="1f1ed-166">api.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="1f1ed-166">api.applicationinsights.io</span></span><br/><span data-ttu-id="1f1ed-167">api1.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="1f1ed-167">api1.applicationinsights.io</span></span><br/><span data-ttu-id="1f1ed-168">api2.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="1f1ed-168">api2.applicationinsights.io</span></span><br/><span data-ttu-id="1f1ed-169">api3.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="1f1ed-169">api3.applicationinsights.io</span></span><br/><span data-ttu-id="1f1ed-170">api4.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="1f1ed-170">api4.applicationinsights.io</span></span><br/><span data-ttu-id="1f1ed-171">api5.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="1f1ed-171">api5.applicationinsights.io</span></span> |<span data-ttu-id="1f1ed-172">13.82.26.252</span><span class="sxs-lookup"><span data-stu-id="1f1ed-172">13.82.26.252</span></span><br/><span data-ttu-id="1f1ed-173">40.76.213.73</span><span class="sxs-lookup"><span data-stu-id="1f1ed-173">40.76.213.73</span></span> |<span data-ttu-id="1f1ed-174">80,443</span><span class="sxs-lookup"><span data-stu-id="1f1ed-174">80,443</span></span> |
| <span data-ttu-id="1f1ed-175">API 문서</span><span class="sxs-lookup"><span data-stu-id="1f1ed-175">API docs</span></span> |<span data-ttu-id="1f1ed-176">dev.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="1f1ed-176">dev.applicationinsights.io</span></span><br/><span data-ttu-id="1f1ed-177">dev.applicationinsights.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="1f1ed-177">dev.applicationinsights.microsoft.com</span></span><br/><span data-ttu-id="1f1ed-178">dev.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="1f1ed-178">dev.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="1f1ed-179">www.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="1f1ed-179">www.applicationinsights.io</span></span><br/><span data-ttu-id="1f1ed-180">www.applicationinsights.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="1f1ed-180">www.applicationinsights.microsoft.com</span></span><br/><span data-ttu-id="1f1ed-181">www.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="1f1ed-181">www.aisvc.visualstudio.com</span></span> |<span data-ttu-id="1f1ed-182">13.82.24.149</span><span class="sxs-lookup"><span data-stu-id="1f1ed-182">13.82.24.149</span></span><br/><span data-ttu-id="1f1ed-183">40.114.82.10</span><span class="sxs-lookup"><span data-stu-id="1f1ed-183">40.114.82.10</span></span> |<span data-ttu-id="1f1ed-184">80,443</span><span class="sxs-lookup"><span data-stu-id="1f1ed-184">80,443</span></span> |
| <span data-ttu-id="1f1ed-185">내부 API</span><span class="sxs-lookup"><span data-stu-id="1f1ed-185">Internal API</span></span> |<span data-ttu-id="1f1ed-186">aigs.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="1f1ed-186">aigs.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="1f1ed-187">aigs1.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="1f1ed-187">aigs1.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="1f1ed-188">aigs2.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="1f1ed-188">aigs2.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="1f1ed-189">aigs3.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="1f1ed-189">aigs3.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="1f1ed-190">aigs4.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="1f1ed-190">aigs4.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="1f1ed-191">aigs5.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="1f1ed-191">aigs5.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="1f1ed-192">aigs6.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="1f1ed-192">aigs6.aisvc.visualstudio.com</span></span> |<span data-ttu-id="1f1ed-193">동적</span><span class="sxs-lookup"><span data-stu-id="1f1ed-193">dynamic</span></span>|<span data-ttu-id="1f1ed-194">443</span><span class="sxs-lookup"><span data-stu-id="1f1ed-194">443</span></span> |

## <a name="application-insights-analytics"></a><span data-ttu-id="1f1ed-195">Application Insights Analytics</span><span class="sxs-lookup"><span data-stu-id="1f1ed-195">Application Insights Analytics</span></span>

| <span data-ttu-id="1f1ed-196">목적</span><span class="sxs-lookup"><span data-stu-id="1f1ed-196">Purpose</span></span> | <span data-ttu-id="1f1ed-197">URI</span><span class="sxs-lookup"><span data-stu-id="1f1ed-197">URI</span></span> | <span data-ttu-id="1f1ed-198">IP</span><span class="sxs-lookup"><span data-stu-id="1f1ed-198">IP</span></span> | <span data-ttu-id="1f1ed-199">포트</span><span class="sxs-lookup"><span data-stu-id="1f1ed-199">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1f1ed-200">분석 포털</span><span class="sxs-lookup"><span data-stu-id="1f1ed-200">Analytics Portal</span></span> | <span data-ttu-id="1f1ed-201">analytics.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="1f1ed-201">analytics.applicationinsights.io</span></span> | <span data-ttu-id="1f1ed-202">동적</span><span class="sxs-lookup"><span data-stu-id="1f1ed-202">dynamic</span></span> | <span data-ttu-id="1f1ed-203">80,443</span><span class="sxs-lookup"><span data-stu-id="1f1ed-203">80,443</span></span> |
| <span data-ttu-id="1f1ed-204">CDN</span><span class="sxs-lookup"><span data-stu-id="1f1ed-204">CDN</span></span> | <span data-ttu-id="1f1ed-205">applicationanalytics.azureedge.net</span><span class="sxs-lookup"><span data-stu-id="1f1ed-205">applicationanalytics.azureedge.net</span></span> | <span data-ttu-id="1f1ed-206">동적</span><span class="sxs-lookup"><span data-stu-id="1f1ed-206">dynamic</span></span> | <span data-ttu-id="1f1ed-207">80,443</span><span class="sxs-lookup"><span data-stu-id="1f1ed-207">80,443</span></span> |
| <span data-ttu-id="1f1ed-208">미디어 CDN</span><span class="sxs-lookup"><span data-stu-id="1f1ed-208">Media CDN</span></span> | <span data-ttu-id="1f1ed-209">applicationanalyticsmedia.azureedge.net</span><span class="sxs-lookup"><span data-stu-id="1f1ed-209">applicationanalyticsmedia.azureedge.net</span></span> | <span data-ttu-id="1f1ed-210">동적</span><span class="sxs-lookup"><span data-stu-id="1f1ed-210">dynamic</span></span> | <span data-ttu-id="1f1ed-211">80,443</span><span class="sxs-lookup"><span data-stu-id="1f1ed-211">80,443</span></span> |

<span data-ttu-id="1f1ed-212">참고: *.applicationinsights.io 도메인은 Application Insights 팀이 소유합니다.</span><span class="sxs-lookup"><span data-stu-id="1f1ed-212">Note: *.applicationinsights.io domain is owned by Application Insights team.</span></span>

## <a name="application-insights-azure-portal-extension"></a><span data-ttu-id="1f1ed-213">Application Insights Azure Portal 확장</span><span class="sxs-lookup"><span data-stu-id="1f1ed-213">Application Insights Azure Portal Extension</span></span>

| <span data-ttu-id="1f1ed-214">목적</span><span class="sxs-lookup"><span data-stu-id="1f1ed-214">Purpose</span></span> | <span data-ttu-id="1f1ed-215">URI</span><span class="sxs-lookup"><span data-stu-id="1f1ed-215">URI</span></span> | <span data-ttu-id="1f1ed-216">IP</span><span class="sxs-lookup"><span data-stu-id="1f1ed-216">IP</span></span> | <span data-ttu-id="1f1ed-217">포트</span><span class="sxs-lookup"><span data-stu-id="1f1ed-217">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1f1ed-218">Application Insights 확장</span><span class="sxs-lookup"><span data-stu-id="1f1ed-218">Application Insights Extension</span></span> | <span data-ttu-id="1f1ed-219">stamp2.app.insightsportal.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="1f1ed-219">stamp2.app.insightsportal.visualstudio.com</span></span> | <span data-ttu-id="1f1ed-220">동적</span><span class="sxs-lookup"><span data-stu-id="1f1ed-220">dynamic</span></span> | <span data-ttu-id="1f1ed-221">80,443</span><span class="sxs-lookup"><span data-stu-id="1f1ed-221">80,443</span></span> |
| <span data-ttu-id="1f1ed-222">Application Insights 확장 CDN</span><span class="sxs-lookup"><span data-stu-id="1f1ed-222">Application Insights Extension CDN</span></span> | <span data-ttu-id="1f1ed-223">insightsportal-prod2-cdn.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="1f1ed-223">insightsportal-prod2-cdn.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="1f1ed-224">insightsportal-prod2-asiae-cdn.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="1f1ed-224">insightsportal-prod2-asiae-cdn.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="1f1ed-225">insightsportal-cdn-aimon.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="1f1ed-225">insightsportal-cdn-aimon.applicationinsights.io</span></span> | <span data-ttu-id="1f1ed-226">동적</span><span class="sxs-lookup"><span data-stu-id="1f1ed-226">dynamic</span></span> | <span data-ttu-id="1f1ed-227">80,443</span><span class="sxs-lookup"><span data-stu-id="1f1ed-227">80,443</span></span> |

## <a name="application-insights-sdks"></a><span data-ttu-id="1f1ed-228">Application Insights SDK</span><span class="sxs-lookup"><span data-stu-id="1f1ed-228">Application Insights SDKs</span></span>

| <span data-ttu-id="1f1ed-229">목적</span><span class="sxs-lookup"><span data-stu-id="1f1ed-229">Purpose</span></span> | <span data-ttu-id="1f1ed-230">URI</span><span class="sxs-lookup"><span data-stu-id="1f1ed-230">URI</span></span> | <span data-ttu-id="1f1ed-231">IP</span><span class="sxs-lookup"><span data-stu-id="1f1ed-231">IP</span></span> | <span data-ttu-id="1f1ed-232">포트</span><span class="sxs-lookup"><span data-stu-id="1f1ed-232">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1f1ed-233">Application Insights JS SDK CDN</span><span class="sxs-lookup"><span data-stu-id="1f1ed-233">Application Insights JS SDK CDN</span></span> | <span data-ttu-id="1f1ed-234">az416426.vo.msecnd.net</span><span class="sxs-lookup"><span data-stu-id="1f1ed-234">az416426.vo.msecnd.net</span></span> | <span data-ttu-id="1f1ed-235">동적</span><span class="sxs-lookup"><span data-stu-id="1f1ed-235">dynamic</span></span> | <span data-ttu-id="1f1ed-236">80,443</span><span class="sxs-lookup"><span data-stu-id="1f1ed-236">80,443</span></span> |
| <span data-ttu-id="1f1ed-237">Application Insights Java SDK</span><span class="sxs-lookup"><span data-stu-id="1f1ed-237">Application Insights Java SDK</span></span> | <span data-ttu-id="1f1ed-238">aijavasdk.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="1f1ed-238">aijavasdk.blob.core.windows.net</span></span> | <span data-ttu-id="1f1ed-239">동적</span><span class="sxs-lookup"><span data-stu-id="1f1ed-239">dynamic</span></span> | <span data-ttu-id="1f1ed-240">80,443</span><span class="sxs-lookup"><span data-stu-id="1f1ed-240">80,443</span></span> |

## <a name="profiler"></a><span data-ttu-id="1f1ed-241">프로파일러</span><span class="sxs-lookup"><span data-stu-id="1f1ed-241">Profiler</span></span>

| <span data-ttu-id="1f1ed-242">목적</span><span class="sxs-lookup"><span data-stu-id="1f1ed-242">Purpose</span></span> | <span data-ttu-id="1f1ed-243">URI</span><span class="sxs-lookup"><span data-stu-id="1f1ed-243">URI</span></span> | <span data-ttu-id="1f1ed-244">IP</span><span class="sxs-lookup"><span data-stu-id="1f1ed-244">IP</span></span> | <span data-ttu-id="1f1ed-245">포트</span><span class="sxs-lookup"><span data-stu-id="1f1ed-245">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1f1ed-246">에이전트</span><span class="sxs-lookup"><span data-stu-id="1f1ed-246">Agent</span></span> | <span data-ttu-id="1f1ed-247">agent.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="1f1ed-247">agent.azureserviceprofiler.net</span></span><br/><span data-ttu-id="1f1ed-248">*.agent.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="1f1ed-248">*.agent.azureserviceprofiler.net</span></span> | <span data-ttu-id="1f1ed-249">동적</span><span class="sxs-lookup"><span data-stu-id="1f1ed-249">dynamic</span></span> | <span data-ttu-id="1f1ed-250">443</span><span class="sxs-lookup"><span data-stu-id="1f1ed-250">443</span></span>
| <span data-ttu-id="1f1ed-251">포털</span><span class="sxs-lookup"><span data-stu-id="1f1ed-251">Portal</span></span> | <span data-ttu-id="1f1ed-252">gateway.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="1f1ed-252">gateway.azureserviceprofiler.net</span></span> | <span data-ttu-id="1f1ed-253">동적</span><span class="sxs-lookup"><span data-stu-id="1f1ed-253">dynamic</span></span> | <span data-ttu-id="1f1ed-254">443</span><span class="sxs-lookup"><span data-stu-id="1f1ed-254">443</span></span>
| <span data-ttu-id="1f1ed-255">저장소</span><span class="sxs-lookup"><span data-stu-id="1f1ed-255">Storage</span></span> | <span data-ttu-id="1f1ed-256">*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="1f1ed-256">*.core.windows.net</span></span> | <span data-ttu-id="1f1ed-257">동적</span><span class="sxs-lookup"><span data-stu-id="1f1ed-257">dynamic</span></span> | <span data-ttu-id="1f1ed-258">443</span><span class="sxs-lookup"><span data-stu-id="1f1ed-258">443</span></span>

## <a name="snapshot-debugger"></a><span data-ttu-id="1f1ed-259">스냅숏 디버거</span><span class="sxs-lookup"><span data-stu-id="1f1ed-259">Snapshot Debugger</span></span>

| <span data-ttu-id="1f1ed-260">목적</span><span class="sxs-lookup"><span data-stu-id="1f1ed-260">Purpose</span></span> | <span data-ttu-id="1f1ed-261">URI</span><span class="sxs-lookup"><span data-stu-id="1f1ed-261">URI</span></span> | <span data-ttu-id="1f1ed-262">IP</span><span class="sxs-lookup"><span data-stu-id="1f1ed-262">IP</span></span> | <span data-ttu-id="1f1ed-263">포트</span><span class="sxs-lookup"><span data-stu-id="1f1ed-263">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1f1ed-264">에이전트</span><span class="sxs-lookup"><span data-stu-id="1f1ed-264">Agent</span></span> | <span data-ttu-id="1f1ed-265">ppe.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="1f1ed-265">ppe.azureserviceprofiler.net</span></span><br/><span data-ttu-id="1f1ed-266">*.ppe.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="1f1ed-266">*.ppe.azureserviceprofiler.net</span></span> | <span data-ttu-id="1f1ed-267">동적</span><span class="sxs-lookup"><span data-stu-id="1f1ed-267">dynamic</span></span> | <span data-ttu-id="1f1ed-268">443</span><span class="sxs-lookup"><span data-stu-id="1f1ed-268">443</span></span>
| <span data-ttu-id="1f1ed-269">포털</span><span class="sxs-lookup"><span data-stu-id="1f1ed-269">Portal</span></span> | <span data-ttu-id="1f1ed-270">ppe.gateway.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="1f1ed-270">ppe.gateway.azureserviceprofiler.net</span></span> | <span data-ttu-id="1f1ed-271">동적</span><span class="sxs-lookup"><span data-stu-id="1f1ed-271">dynamic</span></span> | <span data-ttu-id="1f1ed-272">443</span><span class="sxs-lookup"><span data-stu-id="1f1ed-272">443</span></span>
| <span data-ttu-id="1f1ed-273">저장소</span><span class="sxs-lookup"><span data-stu-id="1f1ed-273">Storage</span></span> | <span data-ttu-id="1f1ed-274">*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="1f1ed-274">*.core.windows.net</span></span> | <span data-ttu-id="1f1ed-275">동적</span><span class="sxs-lookup"><span data-stu-id="1f1ed-275">dynamic</span></span> | <span data-ttu-id="1f1ed-276">443</span><span class="sxs-lookup"><span data-stu-id="1f1ed-276">443</span></span>
