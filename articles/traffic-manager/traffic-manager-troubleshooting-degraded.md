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
# <a name="troubleshooting-degraded-state-on-azure-traffic-manager"></a>Azure 트래픽 관리자의 성능 저하 상태 문제 해결

이 문서에서는 어떻게 tootroubleshoot Azure 트래픽 관리자 프로필은 표시 된 성능 저하 상태를 설명 합니다. 이 시나리오에서는 가리키는 toosome cloudapp.net 호스팅된 서비스의 트래픽 관리자 프로필을 구성 하는 것이 좋습니다. 트래픽 관리자의 hello 상태를 표시 하는 경우는 **Degraded** 상태, 다음 하나 이상의 끝점의 hello 상태 수 **Degraded**:

![성능 저하 끝점 상태](./media/traffic-manager-troubleshooting-degraded/traffic-manager-degradedifonedegraded.png)

Hello 트래픽 관리자의 상태를 표시 하는 경우는 **비활성** 상태, 다음 두 끝점 수 **비활성화**:

![비활성 Traffic Manager 상태](./media/traffic-manager-troubleshooting-degraded/traffic-manager-inactive.png)

## <a name="understanding-traffic-manager-probes"></a>Traffic Manager 이해 프로브

* 트래픽 관리자는 끝점 toobe hello 프로브 경로에서 hello 프로브는 HTTP 200 응답을 수신 하는 경우에 온라인 백업으로 간주 합니다. 다른 200 이외의 응답은 오류입니다.
* Hello 리디렉션 URL 반환 200 하는 경우에 30 x 리디렉션 실패 합니다.
* HTTP 검색의 경우 인증서 오류는 무시됩니다.
* hello 프로브 경로의 hello 실제 콘텐츠는 200이 반환 되는 중요 하지 않습니다. 검색 URL toosome 정적 콘텐츠 like "/ favicon.ico"은 일반적인 기술입니다. 정상 hello 응용 프로그램은 경우에 hello ASP 페이지와 같은 동적 콘텐츠 200을 항상 반환 하지 않을 수 있습니다.
* 가장 좋은 방법은 tooset hello 프로브 사이트 hello 충분 한 논리 toodetermine 있는 경로 toosomething 위나 아래로 이동 됩니다. Hello에 앞의 예제를 설정 하 여 hello 경로 too"/favicon.ico", 대해서만 응답은 해당 w3wp.exe를 테스트 합니다. 이 검색에서는 웹 응용 프로그램 상태가 정상인지 나타낼 수 있습니다. 편이 더 나은지 것 tooset 경로 tooa 것 같은 "/ Probe.aspx" hello 사이트의 논리 toodetermine hello 상태 포함 합니다. 예를 들어 성능 카운터 tooCPU 사용률 또는 실패 한 요청 hello 수 측정값을 사용할 수 있습니다. 또는 세션 상태 toomake hello 웹 응용 프로그램 작동 하 고 있는지 또는 tooaccess 데이터베이스 리소스를 시도할 수 있습니다.
* 프로필의 모든 끝점 저하 된 경우에 트래픽 관리자가 정상으로 모든 끝점을 처리 하는 다음 및 경로 트래픽 tooall 끝점입니다. 이 동작은 검색 메커니즘 hello 문제가 사용자의 서비스는 전체 중지 되지는지 않습니다을 보장 합니다.

## <a name="troubleshooting"></a>문제 해결

프로브 실패 tootroubleshoot hello 프로브 URL에서 반환 hello HTTP 상태 코드를 보여 주는 도구가 필요 합니다. 원시 HTTP 응답을 hello 보여 주는 많은 도구를 사용할 수 있습니다.

* [Fiddler](http://www.telerik.com/fiddler)
* [curl](https://curl.haxx.se/)
* [wget](http://gnuwin32.sourceforge.net/packages/wget.htm)

또한 Internet Explorer tooview hello HTTP 응답에 hello F12 디버깅 도구의 hello 네트워크 탭을 사용할 수 있습니다.

이 예에서는 toosee hello 응답 우리의 프로브 URL에서 원하는: http://watestsdp2008r2.cloudapp.net:80/프로브 합니다. 다음 PowerShell 예에서는 hello hello 문제를 보여 줍니다.

```powershell
Invoke-WebRequest 'http://watestsdp2008r2.cloudapp.net/Probe' -MaximumRedirection 0 -ErrorAction SilentlyContinue | Select-Object StatusCode,StatusDescription
```

예제 출력:

    StatusCode StatusDescription
    ---------- -----------------
           301 Moved Permanently

리디렉션 응답을 수신했습니다. 앞서 설명한 대로 200 이외의 StatusCode는 실패로 간주됩니다. 변경 내용을 트래픽 관리자 끝점 상태 tooOffline hello 합니다. tooresolve hello 문제를 적절 한 StatusCode hello 하는 검사 hello 웹 사이트 구성 tooensure hello 프로브 경로에서 반환할 수 있습니다. Hello 트래픽 관리자 프로브 toopoint tooa 경로 200을 반환 하는 다시 구성 합니다.

프로그램 프로브 hello HTTPS 프로토콜을 사용 하는 경우 toodisable 인증서를 테스트 하는 동안 tooavoid SSL/TLS 오류 검사를 할 수 있습니다. hello 다음 PowerShell 문을 사용 하지 않으려면 hello 현재 PowerShell 세션에 대 한 인증서 유효성 검사

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

## <a name="next-steps"></a>다음 단계

[트래픽 관리자 트래픽 라우팅 방법 정보](traffic-manager-routing-methods.md)

[트래픽 관리자란?](traffic-manager-overview.md)

[클라우드 서비스](http://go.microsoft.com/fwlink/?LinkId=314074)

[Azure Web Apps](https://azure.microsoft.com/documentation/services/app-service/web/)

[트래픽 관리자 작업(REST API 참조)](http://go.microsoft.com/fwlink/?LinkId=313584)

[Azure Traffic Manager cmdlet][1]

[1]: https://msdn.microsoft.com/library/mt125941(v=azure.200).aspx
