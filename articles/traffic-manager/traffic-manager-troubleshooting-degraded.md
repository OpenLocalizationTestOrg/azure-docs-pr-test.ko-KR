---
title: "Azure 트래픽 관리자 성능 저하 aaaTroubleshooting 상태"
description: "방법으로 표시 되 면 tootroubleshoot 트래픽 관리자 프로필을 성능 저하 상태입니다."
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
ms.openlocfilehash: fd95697781472b52e98d856e66beb7b89dfeaf23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-degraded-state-on-azure-traffic-manager"></a><span data-ttu-id="213a7-103">Azure 트래픽 관리자의 성능 저하 상태 문제 해결</span><span class="sxs-lookup"><span data-stu-id="213a7-103">Troubleshooting degraded state on Azure Traffic Manager</span></span>

<span data-ttu-id="213a7-104">이 문서에서는 어떻게 tootroubleshoot Azure 트래픽 관리자 프로필은 표시 된 성능 저하 상태를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="213a7-104">This article describes how tootroubleshoot an Azure Traffic Manager profile that is showing a degraded status.</span></span> <span data-ttu-id="213a7-105">이 시나리오에서는 가리키는 toosome cloudapp.net 호스팅된 서비스의 트래픽 관리자 프로필을 구성 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="213a7-105">For this scenario, consider that you have configured a Traffic Manager profile pointing toosome of your cloudapp.net hosted services.</span></span> <span data-ttu-id="213a7-106">트래픽 관리자의 hello 상태를 표시 하는 경우는 **Degraded** 상태, 다음 하나 이상의 끝점의 hello 상태 수 **Degraded**:</span><span class="sxs-lookup"><span data-stu-id="213a7-106">If hello health of your Traffic Manager displays a **Degraded** status, then hello status of one or more endpoints may be **Degraded**:</span></span>

![성능 저하 끝점 상태](./media/traffic-manager-troubleshooting-degraded/traffic-manager-degradedifonedegraded.png)

<span data-ttu-id="213a7-108">Hello 트래픽 관리자의 상태를 표시 하는 경우는 **비활성** 상태, 다음 두 끝점 수 **비활성화**:</span><span class="sxs-lookup"><span data-stu-id="213a7-108">If hello health of your Traffic Manager displays an **Inactive** status, then both end points may be **Disabled**:</span></span>

![비활성 Traffic Manager 상태](./media/traffic-manager-troubleshooting-degraded/traffic-manager-inactive.png)

## <a name="understanding-traffic-manager-probes"></a><span data-ttu-id="213a7-110">Traffic Manager 이해 프로브</span><span class="sxs-lookup"><span data-stu-id="213a7-110">Understanding Traffic Manager probes</span></span>

* <span data-ttu-id="213a7-111">트래픽 관리자는 끝점 toobe hello 프로브 경로에서 hello 프로브는 HTTP 200 응답을 수신 하는 경우에 온라인 백업으로 간주 합니다.</span><span class="sxs-lookup"><span data-stu-id="213a7-111">Traffic Manager considers an endpoint toobe ONLINE only when hello probe receives an HTTP 200 response back from hello probe path.</span></span> <span data-ttu-id="213a7-112">다른 200 이외의 응답은 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="213a7-112">Any other non-200 response is a failure.</span></span>
* <span data-ttu-id="213a7-113">Hello 리디렉션 URL 반환 200 하는 경우에 30 x 리디렉션 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="213a7-113">A 30x redirect fails, even if hello redirected URL returns a 200.</span></span>
* <span data-ttu-id="213a7-114">HTTP 검색의 경우 인증서 오류는 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="213a7-114">For HTTPs probes, certificate errors are ignored.</span></span>
* <span data-ttu-id="213a7-115">hello 프로브 경로의 hello 실제 콘텐츠는 200이 반환 되는 중요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="213a7-115">hello actual content of hello probe path doesn't matter, as long as a 200 is returned.</span></span> <span data-ttu-id="213a7-116">검색 URL toosome 정적 콘텐츠 like "/ favicon.ico"은 일반적인 기술입니다.</span><span class="sxs-lookup"><span data-stu-id="213a7-116">Probing a URL toosome static content like "/favicon.ico" is a common technique.</span></span> <span data-ttu-id="213a7-117">정상 hello 응용 프로그램은 경우에 hello ASP 페이지와 같은 동적 콘텐츠 200을 항상 반환 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="213a7-117">Dynamic content, like hello ASP pages, may not always return 200, even when hello application is healthy.</span></span>
* <span data-ttu-id="213a7-118">가장 좋은 방법은 tooset hello 프로브 사이트 hello 충분 한 논리 toodetermine 있는 경로 toosomething 위나 아래로 이동 됩니다.</span><span class="sxs-lookup"><span data-stu-id="213a7-118">A best practice is tooset hello Probe path toosomething that has enough logic toodetermine that hello site is up or down.</span></span> <span data-ttu-id="213a7-119">Hello에 앞의 예제를 설정 하 여 hello 경로 too"/favicon.ico", 대해서만 응답은 해당 w3wp.exe를 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="213a7-119">In hello previous example, by setting hello path too"/favicon.ico", you are only testing that w3wp.exe is responding.</span></span> <span data-ttu-id="213a7-120">이 검색에서는 웹 응용 프로그램 상태가 정상인지 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="213a7-120">This probe may not indicate that your web application is healthy.</span></span> <span data-ttu-id="213a7-121">편이 더 나은지 것 tooset 경로 tooa 것 같은 "/ Probe.aspx" hello 사이트의 논리 toodetermine hello 상태 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="213a7-121">A better option would be tooset a path tooa something such as "/Probe.aspx" that has logic toodetermine hello health of hello site.</span></span> <span data-ttu-id="213a7-122">예를 들어 성능 카운터 tooCPU 사용률 또는 실패 한 요청 hello 수 측정값을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="213a7-122">For example, you could use performance counters tooCPU utilization or measure hello number of failed requests.</span></span> <span data-ttu-id="213a7-123">또는 세션 상태 toomake hello 웹 응용 프로그램 작동 하 고 있는지 또는 tooaccess 데이터베이스 리소스를 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="213a7-123">Or you could attempt tooaccess database resources or session state toomake sure that hello web application is working.</span></span>
* <span data-ttu-id="213a7-124">프로필의 모든 끝점 저하 된 경우에 트래픽 관리자가 정상으로 모든 끝점을 처리 하는 다음 및 경로 트래픽 tooall 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="213a7-124">If all endpoints in a profile are degraded, then Traffic Manager treats all endpoints as healthy and routes traffic tooall endpoints.</span></span> <span data-ttu-id="213a7-125">이 동작은 검색 메커니즘 hello 문제가 사용자의 서비스는 전체 중지 되지는지 않습니다을 보장 합니다.</span><span class="sxs-lookup"><span data-stu-id="213a7-125">This behavior ensures that problems with hello probing mechanism do not result in a complete outage of your service.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="213a7-126">문제 해결</span><span class="sxs-lookup"><span data-stu-id="213a7-126">Troubleshooting</span></span>

<span data-ttu-id="213a7-127">프로브 실패 tootroubleshoot hello 프로브 URL에서 반환 hello HTTP 상태 코드를 보여 주는 도구가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="213a7-127">tootroubleshoot a probe failure, you need a tool that shows hello HTTP status code return from hello probe URL.</span></span> <span data-ttu-id="213a7-128">원시 HTTP 응답을 hello 보여 주는 많은 도구를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="213a7-128">There are many tools available that show you hello raw HTTP response.</span></span>

* [<span data-ttu-id="213a7-129">Fiddler</span><span class="sxs-lookup"><span data-stu-id="213a7-129">Fiddler</span></span>](http://www.telerik.com/fiddler)
* [<span data-ttu-id="213a7-130">curl</span><span class="sxs-lookup"><span data-stu-id="213a7-130">curl</span></span>](https://curl.haxx.se/)
* [<span data-ttu-id="213a7-131">wget</span><span class="sxs-lookup"><span data-stu-id="213a7-131">wget</span></span>](http://gnuwin32.sourceforge.net/packages/wget.htm)

<span data-ttu-id="213a7-132">또한 Internet Explorer tooview hello HTTP 응답에 hello F12 디버깅 도구의 hello 네트워크 탭을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="213a7-132">Also, you can use hello Network tab of hello F12 Debugging Tools in Internet Explorer tooview hello HTTP responses.</span></span>

<span data-ttu-id="213a7-133">이 예에서는 toosee hello 응답 우리의 프로브 URL에서 원하는: http://watestsdp2008r2.cloudapp.net:80/프로브 합니다.</span><span class="sxs-lookup"><span data-stu-id="213a7-133">For this example we want toosee hello response from our probe URL: http://watestsdp2008r2.cloudapp.net:80/Probe.</span></span> <span data-ttu-id="213a7-134">다음 PowerShell 예에서는 hello hello 문제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="213a7-134">hello following PowerShell example illustrates hello problem.</span></span>

```powershell
Invoke-WebRequest 'http://watestsdp2008r2.cloudapp.net/Probe' -MaximumRedirection 0 -ErrorAction SilentlyContinue | Select-Object StatusCode,StatusDescription
```

<span data-ttu-id="213a7-135">예제 출력:</span><span class="sxs-lookup"><span data-stu-id="213a7-135">Example output:</span></span>

    StatusCode StatusDescription
    ---------- -----------------
           301 Moved Permanently

<span data-ttu-id="213a7-136">리디렉션 응답을 수신했습니다.</span><span class="sxs-lookup"><span data-stu-id="213a7-136">Notice that we received a redirect response.</span></span> <span data-ttu-id="213a7-137">앞서 설명한 대로 200 이외의 StatusCode는 실패로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="213a7-137">As stated previously, any StatusCode other than 200 is considered a failure.</span></span> <span data-ttu-id="213a7-138">변경 내용을 트래픽 관리자 끝점 상태 tooOffline hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="213a7-138">Traffic Manager changes hello endpoint status tooOffline.</span></span> <span data-ttu-id="213a7-139">tooresolve hello 문제를 적절 한 StatusCode hello 하는 검사 hello 웹 사이트 구성 tooensure hello 프로브 경로에서 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="213a7-139">tooresolve hello problem, check hello website configuration tooensure that hello proper StatusCode can be returned from hello probe path.</span></span> <span data-ttu-id="213a7-140">Hello 트래픽 관리자 프로브 toopoint tooa 경로 200을 반환 하는 다시 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="213a7-140">Reconfigure hello Traffic Manager probe toopoint tooa path that returns a 200.</span></span>

<span data-ttu-id="213a7-141">프로그램 프로브 hello HTTPS 프로토콜을 사용 하는 경우 toodisable 인증서를 테스트 하는 동안 tooavoid SSL/TLS 오류 검사를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="213a7-141">If your probe is using hello HTTPS protocol, you may need toodisable certificate checking tooavoid SSL/TLS errors during your test.</span></span> <span data-ttu-id="213a7-142">hello 다음 PowerShell 문을 사용 하지 않으려면 hello 현재 PowerShell 세션에 대 한 인증서 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="213a7-142">hello following PowerShell statements disable certificate validation for hello current PowerShell session:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="213a7-143">다음 단계</span><span class="sxs-lookup"><span data-stu-id="213a7-143">Next Steps</span></span>

[<span data-ttu-id="213a7-144">트래픽 관리자 트래픽 라우팅 방법 정보</span><span class="sxs-lookup"><span data-stu-id="213a7-144">About Traffic Manager traffic routing methods</span></span>](traffic-manager-routing-methods.md)

[<span data-ttu-id="213a7-145">트래픽 관리자란?</span><span class="sxs-lookup"><span data-stu-id="213a7-145">What is Traffic Manager</span></span>](traffic-manager-overview.md)

[<span data-ttu-id="213a7-146">클라우드 서비스</span><span class="sxs-lookup"><span data-stu-id="213a7-146">Cloud Services</span></span>](http://go.microsoft.com/fwlink/?LinkId=314074)

[<span data-ttu-id="213a7-147">Azure Web Apps</span><span class="sxs-lookup"><span data-stu-id="213a7-147">Azure Web Apps</span></span>](https://azure.microsoft.com/documentation/services/app-service/web/)

[<span data-ttu-id="213a7-148">트래픽 관리자 작업(REST API 참조)</span><span class="sxs-lookup"><span data-stu-id="213a7-148">Operations on Traffic Manager (REST API Reference)</span></span>](http://go.microsoft.com/fwlink/?LinkId=313584)

<span data-ttu-id="213a7-149">[Azure Traffic Manager cmdlet][1]</span><span class="sxs-lookup"><span data-stu-id="213a7-149">[Azure Traffic Manager Cmdlets][1]</span></span>

[1]: https://msdn.microsoft.com/library/mt125941(v=azure.200).aspx
