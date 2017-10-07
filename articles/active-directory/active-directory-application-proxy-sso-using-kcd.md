---
title: "aaaSingle 로그온 응용 프로그램 프록시 | Microsoft Docs"
description: "Azure AD 응용 프로그램 프록시를 사용 하 여 sign-on tooprovide single 하는 방법에 대해 설명 합니다."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: ded0d9c9-45f6-47d7-bd0f-3f7fd99ab621
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: H1Hack27Feb2017, it-pro
ms.openlocfilehash: 0047e834cd42e057a75ebc0c5dcf860734464a05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="kerberos-constrained-delegation-for-single-sign-on-tooyour-apps-with-application-proxy"></a>Kerberos 제한 위임 single sign on tooyour 앱에 대 한 응용 프로그램 프록시

Windows 통합 인증으로 보안되는 응용 프로그램 프록시를 통해 게시된 온-프레미스 응용 프로그램에 대한 Single Sign-On을 제공할 수 있습니다. 이러한 응용 프로그램은 액세스를 위해 Kerberos 티켓이 필요합니다. 응용 프로그램 프록시는 제한 된 위임 KCD (Kerberos) toosupport 이러한 응용 프로그램을 사용합니다. 

Active Directory tooimpersonate 사용자에서 응용 프로그램 프록시 커넥터 권한을 지정 하 여 통합 IWA (Windows 인증)를 사용 하 여 single sign on tooyour 응용 프로그램을 사용할 수 있습니다. hello 커넥터가 권한을 toosend 사용 하며 사용자 대신 토큰을 수신 합니다.

## <a name="how-single-sign-on-with-kcd-works"></a>KCD를 사용하는 Single Sign-On 작동 방식
이 다이어그램에서는 사용자가 IWA를 사용 하는 온-프레미스 응용 프로그램 tooaccess hello 흐름을 설명 합니다.

![Microsoft AAD 인증 흐름 다이어그램](./media/active-directory-application-proxy-sso-using-kcd/AuthDiagram.png)

1. hello 사용자 hello URL tooaccess hello 온-프레미스 응용 프로그램을 통해 응용 프로그램 프록시를 입력합니다.
2. 응용 프로그램 프록시는 hello 요청 tooAzure AD 인증 서비스 toopreauthenticate를 리디렉션합니다. 이 시점에서 Azure AD는 다단계 인증 등, 모든 적용 가능한 인증 및 권한 부여 정책을 적용합니다. Hello 사용자가 확인 되 면 Azure AD 토큰을 만들고 toohello 사용자 보냅니다.
3. hello 사용자 hello 토큰 tooApplication 프록시를 전달합니다.
4. 응용 프로그램 프록시 hello 토큰의 유효성을 검사 및 검색, 이름 UPN (사용자 계정) hello 다음 고 보냅니다 hello 요청, UPN hello 이중 인증 된 보안 채널을 통해 이름 SPN (서비스 사용자) toohello 커넥터 hello 합니다.
5. hello 온-프레미스와 KCD Kerberos 제한 위임 () 협상을 수행 하는 hello 커넥터 광고를 hello 사용자 tooget Kerberos 토큰 toohello 응용 프로그램을 가장 합니다.
6. Active Directory hello 응용 프로그램 toohello 커넥터에 대 한 hello Kerberos 토큰을 보냅니다.
7. hello 커넥터 hello 원래 요청 toohello 응용 프로그램 서버를 AD에서 받은 hello Kerberos 토큰을 사용 하 여 보냅니다.
8. hello 응용 프로그램 hello 응답 toohello toohello 응용 프로그램 프록시 서비스 및 마지막으로 toohello 사용자 그런 다음 반환 되는 커넥터를 보냅니다.

## <a name="prerequisites"></a>필수 조건
Single sign-on에서 IWA 응용 프로그램에 대 한 시작 하기 전에 준비가 되었는지 확인 환경 hello로 다음 설정 및 구성:

* SharePoint 웹 앱 같은 앱 toouse 설정 되어 Windows 통합 인증입니다. 자세한 내용은 [Kerberos 인증 지원 사용](https://technet.microsoft.com/library/dd759186.aspx) 또는 SharePoint의 경우 [SharePoint 2013에서 Kerberos 인증 계획](https://technet.microsoft.com/library/ee806870.aspx)(영문)을 참조하세요.
* 모든 앱에는 [서비스 주체 이름](https://social.technet.microsoft.com/wiki/contents/articles/717.service-principal-names-spns-setspn-syntax-setspn-exe.aspx)이 있습니다.
* hello의 일부와 도메인에 가입 hello 서버 실행 중인 hello 커넥터 및 hello 응용 프로그램을 실행 하는 hello 서버는 동일한 도메인 또는 트러스트를 준 도메인입니다. 도메인 가입에 대 한 자세한 내용은 참조 하십시오. [컴퓨터 tooa 도메인 가입](https://technet.microsoft.com/library/dd807102.aspx)합니다.
* hello 커넥터를 실행 하는 hello 서버는 사용자에 대 한 액세스 tooread hello TokenGroupsGlobalAndUniversal 특성이 있습니다. 이 기본 설정은 수 영향을 받았는지 보안 hello 환경을 강화 합니다.

### <a name="configure-active-directory"></a>Active Directory 구성
hello Active Directory 구성은 다릅니다, 그리고 여부 같은 도메인 hello 응용 프로그램 프록시 커넥터 및 hello 응용 프로그램 서버에서 지 여부에 따라 합니다.

#### <a name="connector-and-application-server-in-hello-same-domain"></a>커넥터 및 응용 프로그램 서버 hello에 동일한 도메인
1. Active Directory에서 이동 너무**도구** > **사용자 및 컴퓨터**합니다.
2. Hello 커넥터를 실행 하는 hello 서버를 선택 합니다.
3. 마우스 오른쪽 단추를 클릭하고 **속성** > **위임**을 선택합니다.
4. 선택 **toospecified 서비스에만 위임에 대 한이 컴퓨터 트러스트**합니다. 
5. 아래 **서비스 toowhich이이 계정 위임 된 자격 증명을 제공할 수** hello hello 응용 프로그램 서버의 SPN id에 대 한 hello 값을 추가 합니다. 이렇게 하면 hello 응용 프로그램 프록시 커넥터 tooimpersonate 사용자 ad에서 hello 목록에 정의 된 hello 응용 프로그램에 대 한 합니다.

   ![커넥터 SVR 속성 창 스크린샷](./media/active-directory-application-proxy-sso-using-kcd/Properties.jpg)

#### <a name="connector-and-application-server-in-different-domains"></a>다른 도메인 내의 커넥터와 응용 프로그램 서버
1. 도메인에 걸쳐 KCD로 작업하기 위한 필수 구성 요소 목록은 [도메인 간의 Kerberos 제한 위임](https://technet.microsoft.com/library/hh831477.aspx)을 참조하세요.
2. 사용 하 여 hello `principalsallowedtodelegateto` hello 커넥터 서버 tooenable hello 응용 프로그램 프록시 toodelegate hello 커넥터 서버에 대 한 속성. hello 응용 프로그램 서버는 `sharepointserviceaccount` hello 서버 위임 되며 `connectormachineaccount`합니다. Windows 2012 R2의 경우 예로 이 코드를 사용합니다.

        $connector= Get-ADComputer -Identity connectormachineaccount -server dc.connectordomain.com

        Set-ADComputer -Identity sharepointserviceaccount -PrincipalsAllowedToDelegateToAccount $connector

        Get-ADComputer sharepointserviceaccount -Properties PrincipalsAllowedToDelegateToAccount

Sharepointserviceaccount은 hello SPS 컴퓨터 계정 또는 응용 프로그램 풀이 실행 되는 hello SPS 서비스 계정이 될 수 있습니다.

## <a name="configure-single-sign-on"></a>Single Sign-On 구성 
1. 에 설명 된 toohello 지침에 따라 응용 프로그램을 게시 [응용 프로그램 프록시는 응용 프로그램 게시](application-proxy-publish-azure-portal.md)합니다. 있는지 tooselect 확인 **Azure Active Directory** hello로 **사전 인증 방법**합니다.
2. 응용 프로그램이 엔터프라이즈 응용 프로그램의 hello 목록에 표시 되 고 나면 선택 하 고 클릭 **Single sign on**합니다.
3. 너무 hello single sign on 모드 설정**Windows 통합 인증**합니다.  
4. Hello 입력 **내부 응용 프로그램 SPN** hello 응용 프로그램 서버. 이 예제에서는 게시 된 응용 프로그램에 대 한 SPN hello는 http/www.contoso.com입니다. 이 SPN 요구 toobe 서비스 toowhich hello 커넥터의 hello 목록에는 위임 된 자격 증명을 제공할 수 있습니다. 
5. Hello 선택 **로그인 Id 위임** 사용자를 대신 하 여 커넥터 toouse hello에 대 한 합니다. 자세한 내용은 [다른 온-프레미스 및 클라우드 ID로 작업](#Working-with-different-on-premises-and-cloud-identities) 참조

   ![고급 응용 프로그램 구성](./media/active-directory-application-proxy-sso-using-kcd/cwap_auth2.png)  


## <a name="sso-for-non-windows-apps"></a>비 Windows 앱에 대한 SSO
Azure AD 응용 프로그램 프록시에 Kerberos 위임 흐름 hello hello 클라우드에서 hello 사용자를 인증 하는 Azure AD를 시작 합니다. 온-프레미스 hello 요청이 수신 되 면 Azure AD 응용 프로그램 프록시 커넥터와의 상호 작용 하 여 hello 사용자 대신 Kerberos 티켓을 발행 hello 로컬 Active Directory hello 합니다. 이 프로세스는 참조 된 tooas 위임 KCD (Kerberos 제한). Hello에서 다음 단계에서는 요청이 전송 되 toohello 백 엔드 응용 프로그램이 Kerberos 티켓을 사용 합니다. 어떻게 toosend 요청 등을 정의 하는 여러 프로토콜 있습니다. 현재 비 Windows Server는 대부분 Azure AD 응용 프로그램 프록시에 지원되는 Negotiate/SPNego를 참조합니다.

Kerberos에 대 한 자세한 내용은 참조 [모든 원하는 tooknow에 대 한 제한 된 위임 KCD (Kerberos)](https://blogs.technet.microsoft.com/applicationproxyblog/2015/09/21/all-you-want-to-know-about-kerberos-constrained-delegation-kcd)합니다.

비 Windows 앱은 일반적으로 도메인 이메일 주소 대신 사용자 이름 또는 SAM 계정 이름을 사용합니다. 상황 tooyour 응용 프로그램을 적용 해야 tooconfigure 위임 hello 로그인 identity 필드 tooconnect 클라우드 identities tooyour 응용 프로그램 id. 

## <a name="working-with-different-on-premises-and-cloud-identities"></a>다른 온-프레미스 및 클라우드 ID로 작업
사용자가 정확 하 게 있다고 가정 하는 응용 프로그램 프록시 hello hello 클라우드 및 온-프레미스에서 동일한 id입니다. 경우 않은 hello 경우 사용할 수 있습니다 수 여전히 KCD single sign on에 대 한 합니다. 구성 된 **로그인 id를 위임** single sign on을 수행할 때 어떤 id를 사용 해야 하는 각 응용 프로그램 toospecify에 대 한 합니다.  

다른 온-프레미스와 hello 클라우드 tooon 온-프레미스 응용 프로그램에서 SSO identities toohave hello 사용자 tooenter 서로 다른 사용자 이름 및 암호를 요구 하지 않고 클라우드 많은 조직에서는이 기능을 사용 합니다. 이 작업은 다음의 조직을 포함합니다.

* 내부적으로 여러 도메인이 있는 (joe@us.contoso.com, joe@eu.contoso.com) 및 hello 클라우드에서 단일 도메인 (joe@contoso.com).
* 라우팅할 수 없는 도메인 이름이 내부적으로 (joe@contoso.usa)와 hello 클라우드에서 법적 비밀 번호입니다.
* 내부적으로 도메인 이름을 사용하지 마십시오(joe).
* 서로 다른 별칭 온-프레미스를 사용 하 여 hello 클라우드에서 하 고 있습니다. 예제: joe-johns@contoso.com 및 joej@contoso.com  

응용 프로그램 프록시는 identity toouse tooobtain hello Kerberos 티켓을 선택할 수 있습니다. 이 설정은 응용 프로그램별입니다. 이러한 옵션 중 일부는 전자 메일 주소 형식을 받아들이지 않는 시스템에 적합한 반면 다른 것들은 대체 로그인을 위해 설계되었습니다.

![위임된 로그인 ID 매개 변수 스크린샷](./media/active-directory-application-proxy-sso-using-kcd/app_proxy_sso_diff_id_upn.png)

위임 된 로그인 id를 사용 하는 경우 hello 수 고유할 모든 hello 도메인 또는 조직에서 포리스트 간에 합니다. 다른 두 가지 커넥터 그룹을 사용하여 이러한 응용 프로그램을 두 번 게시함으로써 이 문제를 방지할 수 있습니다. 각 응용 프로그램의 다른 사용자 그룹에 있으므로 해당 커넥터 tooa 다른 도메인에 조인할 수 있습니다.

### <a name="configure-sso-for-different-identities"></a>다른 ID에 대한 SSO 구성
1. Hello 주 id는 hello 전자 메일 주소 (메일) Azure AD Connect 설정을 구성 합니다. 이 작업은 수행 hello 부분의 hello를 변경 하 여 프로세스를 사용자 지정할 **사용자 계정 이름** 필드 hello 동기화 설정에 있습니다. 이러한 설정은 또한 사용자 tooOffice365, 및 Windows10 장치 및 해당 id 저장소로 Azure AD를 사용 하는 다른 응용 프로그램에 로그인 하는 방법을 결정 합니다.  
   ![사용자 식별 스크린샷 - 사용자 계정 이름 드롭다운](./media/active-directory-application-proxy-sso-using-kcd/app_proxy_sso_diff_id_connect_settings.png)  
2. Hello 응용 프로그램에 대 한 hello 응용 프로그램 구성 설정에서 원하는 toomodify, 선택 hello **로그인 Id 위임** toobe 사용:

   * 사용자 계정 이름(예: joe@contoso.com)
   * 대체 사용자 계정 이름(예: joed@contoso.local)
   * 사용자 계정 이름의 사용자 이름 일부(예: joe)
   * 대체 사용자 계정 이름의 사용자 이름 일부(예: joed)
   * 온-프레미스 SAM 계정 이름 (hello 도메인 컨트롤러 구성에 따라 다름)

### <a name="troubleshooting-sso-for-different-identities"></a>다른 ID에 대한 SSO 문제 해결
에 설명 된 대로 hello 커넥터 컴퓨터 이벤트 로그에 표시 hello SSO 프로세스에에서 오류가 있으면 [문제 해결](application-proxy-back-end-kerberos-constrained-delegation-how-to.md)합니다.
그러나 경우에 따라 hello 요청은 성공적으로 보낸 toohello 백 엔드 응용 프로그램 다른 다양 한 HTTP 응답에이 응용 프로그램에 응답 하는 동안. 이러한 경우 문제 해결 이벤트 번호 24029 hello 응용 프로그램 프록시 세션 이벤트 로그에 hello 커넥터 컴퓨터에서 검사 하 여 시작 해야 합니다. hello 사용자 id 위임에 대해 사용 된 hello 이벤트 세부 정보 내 hello "user" 필드에 나타납니다. 세션 로그에 tooturn 선택 **분석 및 디버그 로그 표시** hello 이벤트 뷰어 보기 메뉴에 있습니다.

## <a name="next-steps"></a>다음 단계

* [어떻게 tooconfigure 응용 프로그램 프록시 응용 프로그램 toouse Kerberos 제한 위임](application-proxy-back-end-kerberos-constrained-delegation-how-to.md)
* [응용 프로그램 프록시에서 발생한 문제 해결](active-directory-application-proxy-troubleshoot.md)


Hello 최신 뉴스 및 업데이트에 대 한 체크 아웃 hello [응용 프로그램 프록시 블로그](http://blogs.technet.com/b/applicationproxyblog/)

