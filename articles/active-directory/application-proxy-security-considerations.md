---
title: "Azure AD 응용 프로그램 프록시에 대 한 고려 사항 aaaSecurity | Microsoft Docs"
description: "Azure AD 응용 프로그램 프록시를 사용하는 경우 보안 고려 사항 설명"
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
ms.date: 08/03/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: ebd14b9d1fc8f4629c5916e5a910595727d935d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="security-considerations-for-accessing-apps-remotely-with-azure-ad-application-proxy"></a>Azure AD 응용 프로그램 프록시를 사용하여 앱에 원격으로 액세스하는 경우 보안 고려 사항

이 문서에서는 Azure Active Directory 응용 프로그램 프록시 서비스에서 응용 프로그램을 원격으로 게시 및 액세스하기 위한 안전한 서비스를 제공하는 방법에 대해 설명합니다.

다음 다이어그램에 표시 방법을 Azure AD는 hello를 사용 하면 보안 된 원격 액세스 tooyour 온-프레미스 응용 프로그램입니다.

 ![Azure AD 응용 프로그램 프록시를 통한 보안 원격 액세스의 다이어그램](./media/application-proxy-security-considerations/secure-remote-access.png)

## <a name="security-benefits"></a>보안 이점

Azure AD 응용 프로그램 프록시는 hello 다음 보안 이점을 제공 합니다.

### <a name="authenticated-access"></a>인증된 액세스 

Toouse Azure Active Directory 사전 인증을 선택 하면 인증 된 연결만 네트워크에 액세스할 수 있습니다.

Azure AD 응용 프로그램 프록시는 hello 모든 인증의 Azure AD 보안 토큰 서비스 (STS)를 사용합니다.  사전 인증을은 본질적으로 차단 익명 공격 상당수 인증 된 id만 hello 백 엔드 응용 프로그램에 액세스할 수 있으므로 합니다.

사전 인증 방법으로 통과를 선택하면 이러한 이점을 활용할 수 없습니다. 

### <a name="conditional-access"></a>조건부 액세스

Tooyour 네트워크 설정 된 연결 하기 전에 다양 한 정책 제어를 적용 합니다.

와 [조건부 액세스](active-directory-conditional-access-azuread-connected-apps.md)를 정의할 수 있습니다 트래픽 종류에 대 한 제한이 tooaccess 백 엔드 응용 프로그램을 허용 합니다. 위치, 인증 강도 및 사용자 위험 프로필에 따라 로그인을 제한하는 정책을 사항을 만들 수 있습니다.

또한 보안 tooyour 사용자 인증의 다른 레이어를 추가 조건부 액세스 tooconfigure Multi-factor Authentication 정책을 사용할 수 있습니다. 

### <a name="traffic-termination"></a>트래픽 종료

모든 트래픽이 hello 클라우드에서 종료 됩니다.

Azure AD 응용 프로그램 프록시는 역방향 프록시 이기 때문에 모든 트래픽 tooback 간 응용 프로그램은 hello 서비스에서 끝납니다. hello 세션 가져올 다시 설정할 수 있는 hello 백 엔드 서버에만 백 엔드 서버에 없는 즉 toodirect HTTP 트래픽을 노출 합니다. 이 구성은 대상이 지정된 공격으로부터 더 잘 보호받을 수 있음을 의미합니다.

### <a name="all-access-is-outbound"></a>모든 액세스가 아웃바운드임 

Tooopen 인바운드 연결 toohello 회사 네트워크가 필요 하지 않습니다.

응용 프로그램 프록시 커넥터는만 있다는 것을 의미 하지 않아도 tooopen 방화벽 포트 들어오는 연결에 대 한 아웃 바운드 연결 toohello Azure AD 응용 프로그램 프록시 서비스를 사용 합니다. 기존 프록시 필요한 경계 네트워크 (라고도 *DMZ*, *완충 영역*, 또는 *스크린 된 서브넷*) toounauthenticated 액세스 허용 hello 네트워크 가장자리에 연결 합니다. 이 시나리오는 웹 응용 프로그램에서 추가 투자가 많은 제품 tooanalyze 트래픽이 방화벽 및 추가 보호 기능은 toohello 환경을 제공 필요 합니다. 응용 프로그램 프록시를 사용하는 경우에는 모든 연결은 아웃바운드이고 보안 채널을 통해 발생하기 때문에 경계 네트워크가 필요하지 않습니다.

커넥터에 대한 자세한 내용은 [Azure AD 응용 프로그램 프록시 커넥터 이해](application-proxy-understand-connectors.md)를 참조하세요.

### <a name="cloud-scale-analytics-and-machine-learning"></a>클라우드 규모 분석 및 기계 학습 

최첨단 보안 보호를 가져옵니다.

Azure Active Directory의 일부 이기 때문에 응용 프로그램 프록시를 활용해 [Azure AD Identity Protection](active-directory-identityprotection.md), 컴퓨터 학습 기반 인텔리전스 및 Microsoft 보안 대응 센터 hello 및 Digital Crimes Unit에서 데이터와 함께 합니다. 따라서 손상된 계정을 사전에 식별하고 위험도 높은 로그인으로부터 실시간 보호를 제공합니다. 감염된 장치에서 익명의 네트워크를 통한 액세스, 일반적이고 가능성이 적은 위치 등 다양한 요소를 고려합니다.

SIEM(보안 정보 및 이벤트 관리) 시스템과 통합을 위해 이러한 많은 보고서 및 이벤트가 API를 통해 제공됩니다.

### <a name="remote-access-as-a-service"></a>서비스로서의 원격 액세스

유지 관리 하 고 온-프레미스 서버를 패치 하는 방법에 대 한 tooworry가 필요는 없습니다.

패치가 적용되지 않은 소프트웨어는 여전히 다수의 공격 대상입니다. Azure AD 응용 프로그램 프록시 Microsoft 소유 하는 인터넷 범위의 서비스 이므로 hello 최신 보안 패치 및 업그레이드를 항상에 다시 가져옵니다.

Azure AD 응용 프로그램 프록시에 의해 게시 된 응용 프로그램의 tooimprove hello 보안, 인덱싱 및 응용 프로그램 보관에서 웹 크롤러 로봇 차단 합니다. 웹 크롤러 로봇이 게시된 앱에 대한 로봇 설정을 검색하려 할 때마다 응용 프로그램 프록시는 `User-agent: * Disallow: /`를 포함하는 robots.txt 파일로 응답합니다.

## <a name="under-hello-hood"></a>Hello 내부적

Azure AD 응용 프로그램 프록시는 두 부분으로 구성됩니다.

* 클라우드 기반 서비스 hello:이 서비스를 Azure에서 실행에 대 한 hello 외부 클라이언트/사용자 연결은 설정 됩니다.
* [hello 온-프레미스 커넥터](application-proxy-understand-connectors.md): hello 커넥터는 온-프레미스 구성 요소, hello Azure AD 응용 프로그램 프록시 서비스에서 요청을 수신 하 고 연결 toohello 내부 응용 프로그램을 처리 합니다. 

Hello 커넥터와 hello 응용 프로그램 프록시 서비스 간의 흐름 설정 되는 경우:

* hello 커넥터 처음 설정 됩니다.
* hello 커넥터 hello 응용 프로그램 프록시 서비스에서에서 구성 정보를 끌어옵니다.
* 사용자는 게시된 응용 프로그램에 액세스합니다.

>[!NOTE]
>모든 통신은 SSL을 통해 발생 하 고 항상 hello 커넥터 toohello 응용 프로그램 프록시 서비스에서 시작 합니다. hello 서비스는 아웃 바운드만 제공 합니다.

hello 커넥터는 클라이언트 인증서 tooauthenticate toohello 거의 모든 호출에 대 한 응용 프로그램 프록시 서비스를 사용합니다. hello만 예외 toothis 프로세스는 hello 초기 설치 단계 hello 클라이언트 인증서 설정 됩니다.

### <a name="installing-hello-connector"></a>Hello 커넥터 설치

Hello 커넥터를 처음 설치할 때 다음 흐름 이벤트 hello 수행.

1. hello 커넥터 등록 toohello 서비스는 hello 커넥터의 hello 설치 과정의 일환으로 발생합니다. 사용자가 자신의 Azure AD 관리자 자격 증명된 tooenter 됩니다. 이 인증에서 가져온 토큰 toohello Azure AD 응용 프로그램 프록시 서비스를 제공 됩니다.
2. hello 응용 프로그램 프록시 서비스는 hello 토큰을 평가합니다. Hello 사용자가 토큰 hello hello 테 넌 트 내에서 회사 관리자에 대해 실행 되었습니다 되도록 조정 합니다. Hello 사용자가 관리자가 아닌 hello 프로세스가 종료 됩니다.
3. hello 커넥터는 클라이언트 인증서 요청을 생성 하 고 hello 토큰, toohello 응용 프로그램 프록시 서비스와 함께 전달 합니다. 그러면 hello 서비스는 hello 토큰을 확인 하 고 hello 클라이언트 인증서 요청에 서명 합니다.
4. hello 커넥터 응용 프로그램 프록시 서비스 hello로 나중에 통신에 대 한 hello 클라이언트 인증서를 사용합니다.
5. hello 커넥터에서 해당 클라이언트 인증서를 사용 하 여 hello 서비스 hello 시스템 구성 데이터의 초기는 끌어오기를 수행 하 고 준비 tootake 요청 되었습니다.

### <a name="updating-hello-configuration-settings"></a>Hello 구성 설정을 업데이트

Hello 구성 설정을 업데이트 하는 응용 프로그램 프록시 서비스 hello, 때마다 hello 흐름 이벤트 뒤 수행.

1. 해당 클라이언트 인증서를 사용 하 여 hello 응용 프로그램 프록시 서비스 내에서 toohello 구성 끝점을 연결 하는 hello 연결선입니다.
2. Hello 응용 프로그램 프록시 서비스 구성 데이터 toohello 커넥터 반환 hello 클라이언트 인증서를 확인 한 후 (예를 들어 커넥터 hello hello 커넥터 그룹의 일부 여야) 합니다.
3. Hello 현재 인증서 180 일 이상 이전 이면 hello 커넥터가 효과적으로 180 일 마다 hello 클라이언트 인증서를 업데이트 하는 새 인증서 요청을 생성 합니다.

### <a name="accessing-published-applications"></a>게시된 응용 프로그램 액세스

사용자가 게시 된 응용 프로그램에 액세스 하는 경우 hello 다음과 같은 이벤트가 수행 hello 응용 프로그램 프록시 서비스와 응용 프로그램 프록시 커넥터 hello 사이.

1. [hello 서비스 hello 앱에 대 한 hello 사용자를 인증합니다.](#the-service-checks-the-configuration-settings-for-the-app)
2. [hello 서비스는 hello 커넥터 큐에 요청을 전달](#The-service-places-a-request-in-the-connector-queue)
3. [Hello 큐에서 hello 요청을 처리 하는 커넥터](#the-connector-receives-the-request-from-the-queue)
4. [응답을 대기 하는 hello 커넥터](#the-connector-waits-for-a-response)
5. [hello 서비스 스트림 데이터 toohello 사용자](#the-service-streams-data-to-the-user)

이러한 단계를 각각 수행 기능에 대 한 자세한 toolearn 계속 읽습니다.


#### <a name="1-hello-service-authenticates-hello-user-for-hello-app"></a>1. hello 서비스 hello 앱에 대 한 hello 사용자를 인증합니다.

Hello 앱 toouse 통과 사전 인증 방법으로 구성한 경우이 섹션의 hello 단계는 건너뜁니다.

Azure AD와 앱 toopreauthenticate hello를 구성한 경우 사용자가 Azure AD STS tooauthenticate 리디렉션된 toohello 및 hello 다음 단계가 수행:

1. 응용 프로그램 프록시 hello 특정 응용 프로그램에 대 한 조건부 액세스 정책 요구 사항을 확인합니다. 이렇게 하면 해당 hello 사용자 toohello 응용 프로그램에 할당 되었습니다. 2 단계 인증을 필요한 경우 hello 인증 시퀀스 메시지는 두 번째 인증 방법에 대 한 hello 사용자를 표시 합니다.

2. 모든 검사에 통과 했음을, 후 hello Azure AD STS hello 응용 프로그램에 대 한 서명 된 토큰을 발급 하 고 리디렉션을 hello 사용자 백 toohello 응용 프로그램 프록시 서비스 합니다.

3. 응용 프로그램 프록시 hello 토큰 발급 toocorrect hello 응용 프로그램을 확인 합니다. 또한 다른 검사를 수행 하 고 해당 hello 시키는 토큰 Azure AD를 사용 하 여 서명 hello 유효한 창 내에 있는 한다는 것입니다.

4. 응용 프로그램 프록시는 암호화 된 인증 쿠키 tooindicate toohello 응용 프로그램 인증 발생 했음을 설정 합니다. hello 쿠키 포함 Azure AD의 토큰을 hello 및 기타 데이터를 기반으로 하는 만료 타임 스탬프 인증 hello hello 사용자 이름을 기반으로 합니다. hello 쿠키 toohello 응용 프로그램 프록시 서비스를 알고 있는 개인 키로 암호화 됩니다.

5. 응용 프로그램 프록시 리디렉션을 hello 사용자 백 toohello는 원래 URL을 요청 합니다.

Hello 사전 인증 단계의 일부가 실패 하면, hello 사용자의 요청이 거부 되 면 하 고 hello 사용자 hello 문제의 hello 원인을 나타내는 메시지를 표시 됩니다.


#### <a name="2-hello-service-places-a-request-in-hello-connector-queue"></a>2. hello 서비스는 hello 커넥터 큐에 요청을 전달

커넥터는 아웃 바운드 연결 열기 toohello 응용 프로그램 프록시 서비스를 유지합니다. 대 한 요청이 들어오면 hello 서비스 hello 커넥터 toopick hello에 대 한 열린 연결 중 하나에서 hello 요청을 대기 합니다.

hello 요청 헤더와 데이터를 암호화 하는 hello 쿠키 같은 hello 응용 프로그램에서 항목을 포함 하는 hello 요청, 요청을 hello 고 hello hello 사용자를 만드는 요청 id입니다. Hello 암호화 된 쿠키에서 데이터는 hello 요청으로 전송 하지만 hello 인증 쿠키와 하지 않습니다.

#### <a name="3-hello-connector-processes-hello-request-from-hello-queue"></a>3. hello 커넥터 hello 큐에서 hello 요청을 처리합니다. 

Hello 요청에 따라 응용 프로그램 프록시 중 하나를 수행 작업을 수행 하는 hello:

* Hello 요청은 간단한 작업 하는 경우 (예를 들어 RESTful는 있는 그대로 hello 본문 내에서 데이터가 없는 *가져오기* 요청), hello 커넥터 연결 toohello 대상 내부 리소스를 만들고 다음 응답을 대기 합니다.

* Hello 요청에 데이터 hello 본문에 연결 된 경우 (RESTful 예를 들어 *POST* 작업), hello 커넥터 hello 클라이언트 인증서 toohello 응용 프로그램 프록시 인스턴스를 사용 하 여 아웃 바운드 연결을 만듭니다. 이 연결 toorequest hello 데이터 있도록 지정 하 고 연결 toohello 내부 리소스를 엽니다. Hello 요청 hello 커넥터에서 수신한 후 hello 응용 프로그램 프록시 서비스는 hello 사용자의 콘텐츠를 수락을 시작 하 고 데이터 toohello 커넥터를 전달 합니다. hello 커넥터 차례로 hello 데이터 toohello 내부 리소스를 전달합니다.

#### <a name="4-hello-connector-waits-for-a-response"></a>4. hello 커넥터 응답을 대기 합니다.

Hello 요청 및 모든 콘텐츠 toohello의 전송을 다시 후에 최종 완료 되 면 hello 커넥터 응답을 대기 합니다.

응답을 수신한 후 hello 커넥터에서 아웃 바운드 연결 toohello 응용 프로그램 프록시 서비스를 사용 하면, tooreturn hello 헤더 정보 및 스트리밍 hello 반환 데이터를 시작 합니다.

#### <a name="5-hello-service-streams-data-toohello-user"></a>5. hello 서비스 스트림 데이터 toohello 사용자입니다. 

여기에 일부 처리 hello 응용 프로그램의 발생할 수 있습니다. 응용 프로그램에서 응용 프로그램 프록시 tootranslate 헤더 또는 Url을 구성한 경우이 단계 동안 필요에 따라 해당 처리가 이루어집니다.


## <a name="next-steps"></a>다음 단계

[Azure AD 응용 프로그램 프록시를 사용할 때 네트워크 토폴로지 고려 사항](application-proxy-network-topology-considerations.md)

[Azure AD 응용 프로그램 프록시 커넥터 이해](application-proxy-understand-connectors.md)
