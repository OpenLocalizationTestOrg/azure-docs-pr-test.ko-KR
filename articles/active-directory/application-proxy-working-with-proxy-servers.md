---
title: "aaaWork 기존 온-프레미스 프록시 서버와 Azure AD | Microsoft Docs"
description: "어떻게 toowork을 기존 온-프레미스 프록시 서버에 설명 합니다."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: kgremban
ms.openlocfilehash: 7f8cec4f676f99bead5211bcbcf23056bd7f211f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="work-with-existing-on-premises-proxy-servers"></a>기존 온-프레미스 프록시 서버 작업

이 문서에서는 설명 어떻게 아웃 바운드 프록시 서버와 Azure Active Directory (Azure AD) 응용 프로그램 프록시 커넥터 toowork tooconfigure 합니다. 네트워크 환경에 기존 프록시가 있는 고객을 위한 것입니다.

이러한 주요 배포 시나리오를 살펴보는 것으로 시작합니다.
* 커넥터 toobypass 온-프레미스 아웃 바운드 프록시를 구성 합니다.
* 커넥터 toouse 아웃 바운드 프록시 tooaccess Azure AD 응용 프로그램 프록시를 구성 합니다.

커넥터 작동 방법에 대한 자세한 내용은 [Azure AD 응용 프로그램 프록시 커넥터 이해](application-proxy-understand-connectors.md)를 참조하세요.

## <a name="configure-hello-outbound-proxy"></a>Hello 아웃 바운드 프록시 구성

아웃 바운드 프록시 사용자 환경에 있으면 적절 한 사용 권한 tooconfigure hello에 대 한 아웃 바운드 프록시 계정을 사용 합니다. Hello 설치 관리자에서 실행 되므로 hello hello 설치를 수행 하는 hello 사용자의 상황에 맞는, Microsoft Edge 또는 다른 인터넷 브라우저를 사용 하 여 hello 구성을 확인할 수 있습니다.

Microsoft Edge의 tooconfigure hello 프록시 설정:

1. 너무 이동**설정** > **고급 설정 보기** > **프록시 설정 열기** > **수동 프록시 설치** .
2. 설정 **프록시 서버를 사용 하 여** 너무**에**선택, hello **(인트라넷) 로컬 주소에 프록시 서버 hello를 사용 하지 않는** 확인란을 선택한 다음 변경 hello 주소와 포트 tooreflect 로컬 프록시 서버입니다.
3. Hello 필요한 프록시 설정을 입력 합니다.

   ![프록시 설정에 대한 대화 상자](./media/application-proxy-working-with-proxy-servers/proxy-bypass-local-addresses.png)

## <a name="bypass-outbound-proxies"></a>아웃바운드 프록시 바이패스

커넥터에는 아웃바운드 요청을 하는 기본 OS 구성 요소가 있습니다. 이러한 구성 요소는 자동 toolocate hello 네트워크에서 프록시 서버를 시도합니다. Hello 환경에서 사용 하는 경우 웹 프록시 자동 검색 (WPAD) 사용 합니다.

hello OS 구성 요소는 wpad.domainsuffix에 대 한 DNS 조회를 수행 하 여 toolocate 프록시 서버를 시도 합니다. 이 DNS에 확인 되 면 HTTP은 다음 요청이 toohello IP wpad.dat에 대 한 주소입니다. 이 요청에는 사용자 환경에서 프록시 구성 스크립트 hello 됩니다. hello 커넥터가 스크립트 tooselect 아웃 바운드 프록시 서버를 사용합니다. 그러나 커넥터 트래픽은 수 여전히 통과 하지, hello 프록시에 필요한 추가 구성 설정으로 인해 합니다.

사용 하 여 온-프레미스 프록시 tooensure 직접 연결 toohello Azure hello 커넥터 toobypass를 구성할 수 있습니다 서비스입니다. (네트워크 정책에 대 한 허용) 하는 경우이 접근 방법이 권장 적은 하나의 구성 toomaintain 있다고 의미 하기 때문에, 합니다.

hello C:\Program Files\Microsoft AAD 응용 프로그램 프록시 Connector\ApplicationProxyConnectorService.exe.config 파일을 편집 하 고 hello를 추가 하는 hello 커넥터에 대 한 아웃 바운드 프록시 사용 toodisable *system.net* 이 코드 예제에 표시 된 섹션 :

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.net>
    <defaultProxy enabled="false"></defaultProxy>
  </system.net>
  <runtime>
    <gcServer enabled="true"/>
  </runtime>
  <appSettings>
    <add key="TraceFilename" value="AadAppProxyConnector.log" />
  </appSettings>
</configuration>
```
tooensure hello 커넥터 업데이트 프로그램 서비스 hello 프록시를 바이패스 하는 C:\Program Files\Microsoft AAD 응용 프로그램 프록시 커넥터 업데이트 프로그램에 있는 유사한 변경 toohello ApplicationProxyConnectorUpdaterService.exe.config 파일을 확인 합니다.

Hello 원본 파일의 있는지 toomake 복사본 수 있게 toorevert toohello 기본.config 파일이 필요 합니다.

## <a name="use-hello-outbound-proxy-server"></a>Hello 아웃 바운드 프록시 서버 사용

일부 환경 예외 없이 아웃 바운드 프록시를 통해 모든 아웃 바운드 트래픽을 toogo가 필요합니다. 결과적으로, hello 프록시 바이패스 하 고 사용할 수 없습니다.

Hello 다음 다이어그램에에서 나와 있는 것 처럼 hello 커넥터 트래픽 toogo hello 아웃 바운드 프록시를 통해 구성할 수 있습니다.

 ![아웃 바운드 프록시 tooAzure AD 통해 트래픽을 toogo 커넥터 구성 응용 프로그램 프록시](./media/application-proxy-working-with-proxy-servers/configure-proxy-settings.png)

따라서 아웃 바운드 트래픽을 having,이 없는 필요 tooconfigure 인바운드 방화벽을 통해 액세스 합니다.

### <a name="step-1-configure-hello-connector-and-related-services-toogo-through-hello-outbound-proxy"></a>1 단계: hello 커넥터를 구성 및 관련 서비스 toogo hello 아웃 바운드 프록시를 통해

Hello 커넥터 hello 아웃 바운드 프록시 서버 및 시도 toouse이 자동으로 검색 WPAD hello 환경에서 사용 되 고 적절 하 게 구성 하는 경우 앞에서 설명, 것입니다. 그러나 hello 커넥터 toogo 아웃 바운드 프록시를 통해 명시적으로 구성할 수 있습니다.

따라서 hello C:\Program Files\Microsoft AAD 응용 프로그램 프록시 Connector\ApplicationProxyConnectorService.exe.config 파일을 편집 및 hello 추가 toodo *system.net* 이 코드 예제에 표시 된 섹션입니다. 변경 *proxyserver:8080* tooreflect 로컬 프록시 서버 이름 또는 IP 주소 및 hello 포트에서 수신 대기 합니다.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.net>  
    <defaultProxy>   
      <proxy proxyaddress="http://proxyserver:8080" bypassonlocal="True" usesystemdefault="True"/>   
    </defaultProxy>  
  </system.net>
  <runtime>
    <gcServer enabled="true"/>
  </runtime>
  <appSettings>
    <add key="TraceFilename" value="AadAppProxyConnector.log" />
  </appSettings>
</configuration>
```

다음으로 C:\Program Files\Microsoft AAD 응용 프로그램 프록시 커넥터 Updater\ApplicationProxyConnectorUpdaterService.exe.config 있는 비슷한 변경 toohello 파일 하 여 hello 커넥터 업데이트 프로그램 서비스 toouse hello 프록시를 구성 합니다.

### <a name="step-2-configure-hello-proxy-tooallow-traffic-from-hello-connector-and-related-services-tooflow-through"></a>2 단계: 구성 hello 커넥터를 통해 관련된 서비스 tooflow hello 프록시 tooallow 트래픽

4 개의 측면 tooconsider hello 아웃 바운드 프록시에 있습니다.
* 프록시 아웃바운드 규칙
* 프록시 인증
* 프록시 포트
* SSL 조사

#### <a name="proxy-outbound-rules"></a>프록시 아웃바운드 규칙
커넥터 서비스 액세스에 대 한 끝점을 다음 액세스 toohello 허용:

* *.msappproxy.net
* *.servicebus.windows.net

초기 등록에 대 한 끝점을 다음 액세스 toohello 허용:

* login.windows.net
* login.microsoftonline.com

FQDN으로 연결 허용 대신 toospecify IP 범위를 할 수 없는 경우이 옵션을 사용 합니다.

* Tooall 대상 hello 커넥터에 대 한 아웃 바운드 액세스를 허용 합니다.
* 너무 hello 커넥터에 대 한 아웃 바운드 액세스를 허용[Azure 데이터 센터 IP 범위](https://www.microsoft.com/en-gb/download/details.aspx?id=41653)합니다. Azure 데이터 센터 IP 범위 목록이 hello를 사용 하 여 hello 챌린지는 매주 업데이트 됩니다. 해야 tooput 내의 프로세스에 위치 tooensure 액세스 규칙에 따라 업데이트 됩니다.

#### <a name="proxy-authentication"></a>프록시 인증

프록시 인증은 현재 지원되지 않습니다. 현재 권장 하는 것은 tooallow hello 커넥터 익명 액세스 toohello 인터넷 대상입니다.

#### <a name="proxy-ports"></a>프록시 포트

hello 커넥터 hello CONNECT 메서드를 사용 하 여 SSL 기반 아웃 바운드 연결을 만듭니다. 기본적으로이 메서드는 hello 아웃 바운드 프록시를 통해 터널을 설정합니다. Hello 프록시 서버 tooallow 443 및 80 tooports 터널링을 구성 합니다.

>[!NOTE]
>Service Bus가 HTTPS를 초과하면 포트 443을 사용합니다. 그러나 기본적으로 서비스 버스 직접 TCP 연결을 시도 되 고 다시 tooHTTPS 직접 연결에 실패 하는 경우에 됩니다.

tooensure hello 아웃 바운드 프록시 서버를 통해 트래픽이도 전송 되는 서비스 버스 hello, 해당 hello 커넥터 toohello 직접 연결할 수 없는 확인 하는 포트 9350, 9352, 및 5671 용 Azure 서비스입니다.

#### <a name="ssl-inspection"></a>SSL 조사
Hello 커넥터 트래픽에 대 한 문제를 일으키기 때문에 hello 커넥터 트래픽에 대 한 SSL 검사를 사용 하지 마십시오.

## <a name="troubleshoot-connector-proxy-problems-and-service-connectivity-issues"></a>커넥터 프록시 및 서비스 연결 문제 해결
이제 hello 프록시를 통과 하는 모든 트래픽이 표시 됩니다. 문제가 있는 경우 다음 문제 해결 정보는 hello 데 도움이 됩니다.

가장 좋은 방법은 tooidentify hello 및 커넥터 연결 문제 해결을 hello 커넥터 서비스를 시작 하는 동안 hello 커넥터 서비스에서 네트워크 캡처 tootake 문제의 합니다. 이는 어려운 작업일 수 있으므로 네트워크 추적을 캡처 및 필터링하는 빠른 팁을 살펴 보겠습니다.

선택한 도구를 모니터링 하는 hello를 사용할 수 있습니다. Hello이이 문서에서는 Microsoft Network Monitor 3.4 사용 했습니다. [Microsoft에서 다운로드](https://www.microsoft.com/download/details.aspx?id=4865)할 수 있습니다.

hello 예제 및 hello 다음 섹션에서에서 사용 하는 필터는 특정 tooNetwork 모니터, 하지만 hello 원칙 적용된 tooany 분석 도구가 될 수 있습니다.

### <a name="take-a-capture-by-using-network-monitor"></a>네트워크 모니터를 사용하여 캡처

toostart 캡처:

1. 네트워크 모니터를 열고 **새 캡처**를 클릭합니다.
2. Hello 클릭 **시작** 단추입니다.

   ![네트워크 모니터 창](./media/application-proxy-working-with-proxy-servers/network-capture.png)

캡처를 완료 한 후 클릭 hello **중지** 단추 tooend 것입니다.

### <a name="take-a-capture-of-connector-traffic"></a>커넥터 트래픽 캡처

초기 문제 해결을 위해 수행할 단계를 수행 하는 hello:

1. Services.msc를에서 hello Azure AD 응용 프로그램 프록시 커넥터 서비스를 중지 합니다.
2. Hello 네트워크 캡처를 시작 합니다.
3. Hello Azure AD 응용 프로그램 프록시 커넥터 서비스를 시작 합니다.
4. Hello 네트워크 캡처를 중지 합니다.

   ![services.msc의 Azure AD 응용 프로그램 프록시 커넥터 서비스](./media/application-proxy-working-with-proxy-servers/services-local.png)

### <a name="look-at-hello-requests-from-hello-connector-toohello-proxy-server"></a>Hello 커넥터 toohello 프록시 서버에서 hello 요청 확인

이제 네트워크 캡처를가지고 하 준비 toofilter 것입니다. hello 추적 hello 키 toolooking toofilter hello 캡처 방법을 파악 합니다.

필터가 두 개는 다음과 같습니다 (여기서: hello 모드 해제 프록시 서비스 포트는 8080)입니다.

**(http.Request 또는 http.Response) 및 tcp.port==8080**

Hello에이 필터를 입력 하면 **표시 필터** 창과 선택 **적용**, 캡처된 hello 트래픽 hello 필터에 따라 필터링 합니다.

hello 이전 필터 표시 hello HTTP 요청 및 응답 방금 hello 모드 해제 프록시 포트에서 합니다. 여기서 hello 커넥터는 구성 된 프록시 서버 toouse 커넥터 시작을 위한 hello 필터 다음과 같이 표시 됩니다.

 ![필터링된 HTTP 요청 및 응답의 예제 목록](./media/application-proxy-working-with-proxy-servers/http-requests.png)

이제 구체적으로 원하는 hello hello 프록시 서버와의 통신을 보여 주는 연결 요청에 대 한 합니다. 성공하면 HTTP OK(200) 응답을 받게 됩니다.

407 또는 502, 같은 다른 응답 코드에 표시 되 면 hello 프록시 인증을 요구 되었거나 다른 이유로 hello 트래픽을 허용 하지 않도록 됩니다. 이 시점에는 프록시 서버 지원 팀이 관여합니다.

### <a name="identify-failed-tcp-connection-attempts"></a>실패한 TCP 연결 시도 식별

hello에 관심이 있을 수 있습니다 하는 다른 일반적인 시나리오는 hello 커넥터 시도 tooconnect를 직접 하지만 실패 하는 경우입니다.

다음은 tooeasily이이 문제를 식별에 도움이 되는 다른 네트워크 모니터 필터가입니다.

**property.TCPSynRetransmit**

SYN 패킷을 hello 첫 번째 패킷이 전송 tooestablish TCP 연결입니다. 이 패킷 응답은 반환 하지 않습니다, hello SYN 다시 시도 합니다. 모든 재전송 된 SYNs hello 필터 toosee 앞에 사용할 수 있습니다. 그런 다음 이러한 SYNs tooany 커넥터 관련 트래픽와 일치 하는지 확인할 수 있습니다.

hello 다음 예제는 실패 한 연결을 시도 하는 9352 tooService 버스 포트.

 ![실패한 연결 시도의 예제 응답](./media/application-proxy-working-with-proxy-servers/failed-connection-attempt.png)

앞에 응답 하는 hello 같은 결과 볼 경우 hello 커넥터 hello Azure 서비스 버스 서비스를 사용 하 여 직접 toocommunicate를 하려고 합니다. Hello 커넥터 toomake 직접 연결 toohello Azure 예상 되는 경우 서비스를이 응답은 뚜렷한 네트워크 또는 방화벽 문제가 있는 것입니다.

>[!NOTE]
>프록시 서버 구성된 toouse 인 경우이 응답 서비스 버스가 HTTPS를 통해 연결 tooattempting 전환 하기 전에 직접 TCP 연결을 시도 하 의미할 수도 있습니다.
>

네트워크 추적 분석은 만능 도구는 아닙니다. 하지만 네트워크의 진행 상황에 대 한 중요 한 도구 tooget 요약 정보를 수 있습니다.

커넥터 연결 문제가 있는 toostruggle를 계속 진행 하면 지원 팀으로 티켓을 만드세요. hello 팀 추가 문제 해결을 지원할 수 있습니다.

응용 프로그램 프록시 커넥터와 관련된 오류를 해결하는 방법에 대한 자세한 내용은 [응용 프로그램 프록시 문제 해결](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-troubleshoot)을 참조하세요.

## <a name="next-steps"></a>다음 단계

[Azure AD 응용 프로그램 프록시 커넥터 이해](application-proxy-understand-connectors.md)<br>
[Toosilently hello Azure AD 응용 프로그램 프록시 커넥터를 설치 하는 방법](active-directory-application-proxy-silent-installation.md)
