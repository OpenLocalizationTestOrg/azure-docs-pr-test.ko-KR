---
title: "Azure 트래픽 관리자의 성능 저하 상태 문제해결"
description: "성능 저하 상태로 표시할 때 Traffic Manager 문제를 해결하는 방법입니다."
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
ms.assetid: 8af0433d-e61b-4761-adcc-7bc9b8142fc6
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/03/2017
ms.author: kumud
ms.openlocfilehash: b1d00fb84695d2289f37647f55a7c56cf28c8c96
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-degraded-state-on-azure-traffic-manager"></a><span data-ttu-id="4908c-103">Azure 트래픽 관리자의 성능 저하 상태 문제 해결</span><span class="sxs-lookup"><span data-stu-id="4908c-103">Troubleshooting degraded state on Azure Traffic Manager</span></span>

<span data-ttu-id="4908c-104">이 문서에서는 성능 저하 상태를 보여 주는 Azure Traffic Manager 프로필 문제를 해결하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4908c-104">This article describes how to troubleshoot an Azure Traffic Manager profile that is showing a degraded status.</span></span> <span data-ttu-id="4908c-105">이 시나리오의 경우 사용자의 일부 .cloudapp.net 호스티드 서비스를 가리키는 Traffic Manager 프로필을 구성했다는 점을 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="4908c-105">For this scenario, consider that you have configured a Traffic Manager profile pointing to some of your cloudapp.net hosted services.</span></span> <span data-ttu-id="4908c-106">Traffic Manager의 상태가 **성능 저하됨** 상태를 표시하는 경우 하나 이상의 끝점 상태가 **성능 저하됨**일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4908c-106">If the health of your Traffic Manager displays a **Degraded** status, then the status of one or more endpoints may be **Degraded**:</span></span>

![성능 저하 끝점 상태](./media/traffic-manager-troubleshooting-degraded/traffic-manager-degradedifonedegraded.png)

<span data-ttu-id="4908c-108">Traffic Manager의 상태가 **비활성** 상태를 표시하는 경우 두 끝점이 모두 **비활성**일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4908c-108">If the health of your Traffic Manager displays an **Inactive** status, then both end points may be **Disabled**:</span></span>

![비활성 Traffic Manager 상태](./media/traffic-manager-troubleshooting-degraded/traffic-manager-inactive.png)

## <a name="understanding-traffic-manager-probes"></a><span data-ttu-id="4908c-110">Traffic Manager 이해 프로브</span><span class="sxs-lookup"><span data-stu-id="4908c-110">Understanding Traffic Manager probes</span></span>

* <span data-ttu-id="4908c-111">Traffic Manager는 프로브가 프로브 경로에서 다시 HTTP 200 응답을 수신하는 경우에만 끝점을 온라인 상태로 변경할 것을 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="4908c-111">Traffic Manager considers an endpoint to be ONLINE only when the probe receives an HTTP 200 response back from the probe path.</span></span> <span data-ttu-id="4908c-112">다른 200 이외의 응답은 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="4908c-112">Any other non-200 response is a failure.</span></span>
* <span data-ttu-id="4908c-113">리디렉션된 URL이 200을 반환하더라도 30x 리디렉션은 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="4908c-113">A 30x redirect fails, even if the redirected URL returns a 200.</span></span>
* <span data-ttu-id="4908c-114">HTTP 검색의 경우 인증서 오류는 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4908c-114">For HTTPs probes, certificate errors are ignored.</span></span>
* <span data-ttu-id="4908c-115">200가 반환되면 검색 경로의 실제 콘텐츠는 문제가 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4908c-115">The actual content of the probe path doesn't matter, as long as a 200 is returned.</span></span> <span data-ttu-id="4908c-116">"/favicon.ico"와 같은 정적 콘텐츠에 대한 URL을 검색하는 작업은 일반적인 기술입니다.</span><span class="sxs-lookup"><span data-stu-id="4908c-116">Probing a URL to some static content like "/favicon.ico" is a common technique.</span></span> <span data-ttu-id="4908c-117">응용 프로그램이 정상적인 경우더라도 ASP 페이지와 같은 동적 콘텐츠는 항상 200을 반환하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4908c-117">Dynamic content, like the ASP pages, may not always return 200, even when the application is healthy.</span></span>
* <span data-ttu-id="4908c-118">모범 사례는 사이트 가동 또는 중지를 결정하기 위한 충분한 논리가 있는 경로로 검색 경로를 설정하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4908c-118">A best practice is to set the Probe path to something that has enough logic to determine that the site is up or down.</span></span> <span data-ttu-id="4908c-119">이전 예제에서는 "/favicon.ico"로 경로를 설정하여 w3wp.exe가 응답하는지 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="4908c-119">In the previous example, by setting the path to "/favicon.ico", you are only testing that w3wp.exe is responding.</span></span> <span data-ttu-id="4908c-120">이 검색에서는 웹 응용 프로그램 상태가 정상인지 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4908c-120">This probe may not indicate that your web application is healthy.</span></span> <span data-ttu-id="4908c-121">사이트의 상태를 확인하는 논리를 포함하는 "/Probe.aspx"와 같이 경로를 설정하는 것이 더 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="4908c-121">A better option would be to set a path to a something such as "/Probe.aspx" that has logic to determine the health of the site.</span></span> <span data-ttu-id="4908c-122">예를 들어, CPU 사용률에 성능 카운터를 사용하거나 실패한 요청 수를 측정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4908c-122">For example, you could use performance counters to CPU utilization or measure the number of failed requests.</span></span> <span data-ttu-id="4908c-123">또는 데이터베이스 리소스 또는 세션 상태에 액세스하여 웹 응용 프로그램이 작동하는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4908c-123">Or you could attempt to access database resources or session state to make sure that the web application is working.</span></span>
* <span data-ttu-id="4908c-124">프로필의 모든 끝점의 성능이 저하된 경우 Traffic Manager는 모든 끝점을 정상으로 처리하고 트래픽을 모든 끝점으로 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="4908c-124">If all endpoints in a profile are degraded, then Traffic Manager treats all endpoints as healthy and routes traffic to all endpoints.</span></span> <span data-ttu-id="4908c-125">이 동작을 통해 검색 메커니즘과 관련된 문제가 서비스의 전체 가동 중단을 일으키지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="4908c-125">This behavior ensures that problems with the probing mechanism do not result in a complete outage of your service.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="4908c-126">문제 해결</span><span class="sxs-lookup"><span data-stu-id="4908c-126">Troubleshooting</span></span>

<span data-ttu-id="4908c-127">검색 실패 문제를 해결하려면 프로브 URL에서 HTTP 상태 코드 반환을 보여 주는 도구가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4908c-127">To troubleshoot a probe failure, you need a tool that shows the HTTP status code return from the probe URL.</span></span> <span data-ttu-id="4908c-128">원시 HTTP 응답을 보여 주는 사용 가능한 도구가 많이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4908c-128">There are many tools available that show you the raw HTTP response.</span></span>

* [<span data-ttu-id="4908c-129">Fiddler</span><span class="sxs-lookup"><span data-stu-id="4908c-129">Fiddler</span></span>](http://www.telerik.com/fiddler)
* [<span data-ttu-id="4908c-130">curl</span><span class="sxs-lookup"><span data-stu-id="4908c-130">curl</span></span>](https://curl.haxx.se/)
* [<span data-ttu-id="4908c-131">wget</span><span class="sxs-lookup"><span data-stu-id="4908c-131">wget</span></span>](http://gnuwin32.sourceforge.net/packages/wget.htm)

<span data-ttu-id="4908c-132">또한 Internet Explorer에서 F12 디버깅 도구의 네트워크 탭을 사용하여 HTTP 응답을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4908c-132">Also, you can use the Network tab of the F12 Debugging Tools in Internet Explorer to view the HTTP responses.</span></span>

<span data-ttu-id="4908c-133">이 예에서는 검색 URL인 http://watestsdp2008r2.cloudapp.net:80/Probe에서 응답을 확인하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="4908c-133">For this example we want to see the response from our probe URL: http://watestsdp2008r2.cloudapp.net:80/Probe.</span></span> <span data-ttu-id="4908c-134">다음 PowerShell 예는 이러한 문제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4908c-134">The following PowerShell example illustrates the problem.</span></span>

```powershell
Invoke-WebRequest 'http://watestsdp2008r2.cloudapp.net/Probe' -MaximumRedirection 0 -ErrorAction SilentlyContinue | Select-Object StatusCode,StatusDescription
```

<span data-ttu-id="4908c-135">예제 출력:</span><span class="sxs-lookup"><span data-stu-id="4908c-135">Example output:</span></span>

    StatusCode StatusDescription
    ---------- -----------------
           301 Moved Permanently

<span data-ttu-id="4908c-136">리디렉션 응답을 수신했습니다.</span><span class="sxs-lookup"><span data-stu-id="4908c-136">Notice that we received a redirect response.</span></span> <span data-ttu-id="4908c-137">앞서 설명한 대로 200 이외의 StatusCode는 실패로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="4908c-137">As stated previously, any StatusCode other than 200 is considered a failure.</span></span> <span data-ttu-id="4908c-138">Traffic Manager는 끝점 상태를 오프라인으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="4908c-138">Traffic Manager changes the endpoint status to Offline.</span></span> <span data-ttu-id="4908c-139">이 문제를 해결하려면 웹 사이트 구성을 확인하여 적절한 StatusCode가 프로브 경로에서 반환될 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4908c-139">To resolve the problem, check the website configuration to ensure that the proper StatusCode can be returned from the probe path.</span></span> <span data-ttu-id="4908c-140">Traffic Manager 검색이 200을 반환하는 경로를 가리키도록 다시 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="4908c-140">Reconfigure the Traffic Manager probe to point to a path that returns a 200.</span></span>

<span data-ttu-id="4908c-141">검색이 HTTPS 프로토콜을 사용하는 경우 테스트 중 SSL/TLS 오류를 방지하기 위해 확인하는 인증서를 사용하지 않도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4908c-141">If your probe is using the HTTPS protocol, you may need to disable certificate checking to avoid SSL/TLS errors during your test.</span></span> <span data-ttu-id="4908c-142">다음 PowerShell 문은 현재 PowerShell 세션에 대한 인증서 유효성 검사를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4908c-142">The following PowerShell statements disable certificate validation for the current PowerShell session:</span></span>

```powershell
add-type @"
using System.Net;
using System.Security.Cryptography.X509Certificates;
public class TrustAllCertsPolicy : ICertificatePolicy {
    public bool CheckValidationResult(
    ServicePoint srvPoint, X509Certificate certificate,
    WebRequest request, int certificateProblem) {
    return true;
    }
}
"@
[System.Net.ServicePointManager]::CertificatePolicy = New-Object TrustAllCertsPolicy
```

## <a name="next-steps"></a><span data-ttu-id="4908c-143">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4908c-143">Next Steps</span></span>

[<span data-ttu-id="4908c-144">트래픽 관리자 트래픽 라우팅 방법 정보</span><span class="sxs-lookup"><span data-stu-id="4908c-144">About Traffic Manager traffic routing methods</span></span>](traffic-manager-routing-methods.md)

[<span data-ttu-id="4908c-145">트래픽 관리자란?</span><span class="sxs-lookup"><span data-stu-id="4908c-145">What is Traffic Manager</span></span>](traffic-manager-overview.md)

[<span data-ttu-id="4908c-146">클라우드 서비스</span><span class="sxs-lookup"><span data-stu-id="4908c-146">Cloud Services</span></span>](http://go.microsoft.com/fwlink/?LinkId=314074)

[<span data-ttu-id="4908c-147">Azure Web Apps</span><span class="sxs-lookup"><span data-stu-id="4908c-147">Azure Web Apps</span></span>](https://azure.microsoft.com/documentation/services/app-service/web/)

[<span data-ttu-id="4908c-148">트래픽 관리자 작업(REST API 참조)</span><span class="sxs-lookup"><span data-stu-id="4908c-148">Operations on Traffic Manager (REST API Reference)</span></span>](http://go.microsoft.com/fwlink/?LinkId=313584)

<span data-ttu-id="4908c-149">[Azure Traffic Manager cmdlet][1]</span><span class="sxs-lookup"><span data-stu-id="4908c-149">[Azure Traffic Manager Cmdlets][1]</span></span>

[1]: https://msdn.microsoft.com/library/mt125941(v=azure.200).aspx
