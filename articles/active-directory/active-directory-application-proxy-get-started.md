---
title: "aaaHow tooprovide 보안 된 원격 액세스 tooon 온-프레미스 응용 프로그램"
description: "어떻게 toouse Azure AD 응용 프로그램 프록시 tooprovide 보안 된 원격 액세스 tooyour 온-프레미스 응용 프로그램에 설명 합니다."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d5450da1-9e06-4d08-8146-011c84922ab5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 289e970ed0596fcd06ccf6b2ad92203366fbb494
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooprovide-secure-remote-access-tooon-premises-applications"></a>어떻게 tooprovide 보안 원격 액세스 tooon 온-프레미스 응용 프로그램

직원 오늘 toobe 생산성에 원하는 어디에서 든 모든 장치에서 하 고 언제 든 지 합니다. 태블릿, 전화 또는 랩톱 든 상관 없이 자신의 장치로 toowork를 원하는 것입니다. 및 기대 toobe 수 tooaccess 해당 응용 프로그램을 온-프레미스 hello 클라우드에서 SaaS 앱 및 회사 앱을 모두 합니다. Tooon 온-프레미스 응용 프로그램 액세스를 제공 하는 가상 사설망 (Vpn) 또는 완충 (Dmz) 일반적으로 관련 됩니다. 뿐만 아니라 이러한 솔루션 복잡 하 고 하드 toomake는 안전 하지만 비용이 많이 드는 tooset를 하 고 관리 합니다.

더 나은 방법이 있습니다!

Hello 모바일 중심에서 최신 인력, 클라우드 우선 세계에 최신 원격 액세스 솔루션이 필요합니다. Azure AD 응용 프로그램 프록시는 Azure Active Directory의 기능이며 원격 액세스 서비스를 제공합니다. 즉, 것은 쉽게 toodeploy, 사용 및 관리 합니다.

[!INCLUDE [identity](../../includes/azure-ad-licenses.md)]

## <a name="what-is-azure-active-directory-application-proxy"></a>Azure Active Directory 응용 프로그램 프록시란?
Azure AD 응용 프로그램 프록시는 온-프레미스에 호스트된 웹 응용 프로그램에 대한 SSO(Single Sign-On) 및 보안된 원격 액세스를 제공합니다. 일부 앱 toopublish 원하는 SharePoint 사이트, Outlook Web Access 또는 다른 LOB 웹 응용 프로그램 해야 포함 됩니다. 이러한 온-프레미스 웹 응용 프로그램이 Azure AD와 통합 되어 동일한 id hello 하 고 o 365에서 사용 되는 플랫폼을 제어 합니다. 최종 사용자가 O365 및 기타 SaaS 앱에 액세스할 동일한 방식으로 Azure AD와 통합 하 여 온-프레미스 응용 프로그램 hello를 액세스할 수 있습니다. Toochange hello 네트워크 인프라가 필요 하지 않거나 사용자에 대 한 VPN tooprovide이이 솔루션이 필요 합니다.

## <a name="why-is-application-proxy-a-better-solution"></a>응용 프로그램 프록시가 더 나은 솔루션인 이유
Azure AD 응용 프로그램 프록시는 원격 액세스를 간단 하 고 안전 하며 비용 효율적인 솔루션 tooall 온-프레미스 응용 프로그램을 제공합니다.

Azure AD 응용 프로그램 프록시는:

* **간단**
   * Toochange 필요 하지 않거나 응용 프로그램 프록시 응용 프로그램 toowork를 업데이트 합니다. 
   * 사용자는 일관된 인증 환경을 제공 받습니다. Hello 클라우드 및 앱 온-프레미스 MyApps 포털 tooget single sign on hello tooboth SaaS 앱을 사용할 수 있습니다. 
* **보안**
   * Azure AD 응용 프로그램 프록시를 사용 하 여 앱을 게시할 때는 Azure의 hello 풍부한 권한 부여 컨트롤 및 보안 분석 활용을 걸릴 수 있습니다. 조건부 액세스 및 2단계 인증과 같은 클라우드 규모 보안 및 Azure 보안 기능을 제공 받습니다.
   * 없는 tooopen 모든 인바운드 연결 방화벽 toogive를 통해 사용자가 원격 액세스 합니다. 
* **비용 효율성**
   * 응용 프로그램 프록시 hello 클라우드에서 작동 하는 시간과 비용을 저장할 수 있도록 합니다. 일반적으로 온-프레미스 솔루션을 tooset 요구 하 게 되 고 Dmz에 지 서버 또는 기타 복잡 한 인프라 유지 관리 합니다.  

## <a name="what-kind-of-applications-work-with-application-proxy"></a>어떤 종류의 응용 프로그램이 응용 프로그램 프록시에서 작동합니까?
Azure AD 응용 프로그램 프록시를 사용하면 다양한 유형의 내부 응용 프로그램에 액세스할 수 있습니다.

* 인증을 위해 [Windows 통합 인증](active-directory-application-proxy-sso-using-kcd.md)을 사용하는 웹 응용 프로그램  
* 폼 기반 또는 [헤더 기반](application-proxy-ping-access.md) 액세스를 사용하는 웹 응용 프로그램  
* 웹 tooexpose toorich 응용 프로그램을 서로 다른 장치에서 지정 하는 Api  
* [원격 데스크톱 게이트웨이](application-proxy-publish-remote-desktop.md) 뒤에서 호스트되는 응용 프로그램  
* Active Directory 인증 라이브러리 (ADAL) hello와 통합 하는 리치 클라이언트 응용 프로그램

## <a name="how-does-application-proxy-work"></a>응용 프로그램 프록시는 어떻게 작동합니까?
Tooconfigure toomake 응용 프로그램 프록시 작업 해야 하는 두 구성 요소가 있습니다: 커넥터 및 외부 끝점입니다. 

hello 커넥터는 Windows Server 네트워크 내부에 상주 하는 간단한 에이전트입니다. hello 커넥터 hello hello 클라우드 tooyour 응용 프로그램이 온-프레미스에서 응용 프로그램 프록시 서비스 로부터 hello 트래픽 흐름을 지원합니다. 아웃 바운드 연결에만 사용 하지 않는 tooopen 인바운드 포트가 했거나 hello DMZ에 저장 되므로 합니다. hello 커넥터는 상태 비저장 및 필요에 따라 hello 클라우드에서 정보를 가져오도록 합니다. 커넥터에 대한 정보 및 부하 분산 및 인증하는 방법은 [Azure AD 응용 프로그램 프록시 커넥터 이해](application-proxy-understand-connectors.md)를 참조하세요. 

외부 끝점 hello는 사용자가 네트워크 외부에서 응용 프로그램을 전송 하는 방법입니다. 하거나 직접 tooan을 결정 하는 외부 URL을 확인 하거나 hello MyApps 포털을 통해 hello 응용 프로그램에 액세스할 수 있습니다. 사용자가 이러한 끝점 tooone에 이동 하면 Azure AD에서 인증 하며 다음 hello 커넥터 toohello 온-프레미스 응용 프로그램을 통해 라우팅됩니다.

 ![Azure Ad 응용 프로그램 프록시 다이어그램](./media/active-directory-application-proxy-get-started/azureappproxxy.png)

1. hello 사용자 hello 응용 프로그램 프록시 서비스를 통해 hello 응용 프로그램에 액세스 했으며 toohello 방향이 지정 된 Azure AD 로그인 페이지 tooauthenticate 합니다.
2. 성공적으로 로그인 한 후 토큰 생성 되 고 toohello 클라이언트 장치에 전송 합니다.
3. 클라이언트 hello 토큰 toohello hello 사용자 계정 이름 (UPN)을 검색 하는 응용 프로그램 프록시 서비스 hello 및 hello 토큰에서 보안 주체 이름 (SPN) 안내해 hello 요청 toohello 응용 프로그램 프록시 커넥터를 보냅니다.
4. Single sign on를 구성한 경우 hello 커넥터 hello 사용자를 대신 하는 데 필요한 모든 추가 인증을 수행 합니다.
5. hello 커넥터 hello 요청 toohello 온-프레미스 응용 프로그램을 보냅니다.  
6. hello 응답이 서비스와 커넥터 toohello 사용자 응용 프로그램 프록시를 통해 보내집니다.

### <a name="single-sign-on"></a>SSO(Single sign-on)
Azure AD 응용 프로그램 프록시 IWA Windows 통합 인증 (), 또는 클레임 인식 응용 프로그램을 사용 하는 single sign on (SSO) tooapplications를 제공 합니다. 응용 프로그램에서 IWA를 사용 하는 경우 응용 프로그램 프록시는 Kerberos 제한 위임 tooprovide SSO를 사용 하 여 hello 사용자를 가장 합니다. Azure Active Directory에서 신뢰 하는 클레임 인식 응용 프로그램이 있으면 SSO hello 사용자가 이미 Azure AD에서 인증 하기 때문에 작동 합니다.

Kerberos에 대 한 자세한 내용은 참조 [모든 원하는 tooknow에 대 한 제한 된 위임 KCD (Kerberos)](https://blogs.technet.microsoft.com/applicationproxyblog/2015/09/21/all-you-want-to-know-about-kerberos-constrained-delegation-kcd)합니다.

### <a name="managing-apps"></a>앱 관리
응용 프로그램 프록시을 게시 한 앱, hello Azure 포털에서에서 다른 엔터프라이즈 앱 처럼 관리할 수 있습니다. 조건부 액세스 및 2 단계 확인과 같은 Azure Active Directory 보안 기능을 사용 하 여 사용자 권한을 제어 하 고 hello 앱에 대 한 브랜딩 사용자 지정 수 있습니다. 

## <a name="get-started"></a>시작

응용 프로그램 프록시를 구성하기 전에 지원되는 [Azure Active Directory 버전](https://azure.microsoft.com/pricing/details/active-directory/) 및 전역 관리자 권한이 있는 Azure AD 디렉터리가 있는지 확인합니다.

두 단계에서 응용 프로그램 프록시 시작:

1. [응용 프로그램 프록시를 사용 하도록 설정 하 고 hello 커넥터 구성](active-directory-application-proxy-enable.md)합니다.    
2. [응용 프로그램을 게시](active-directory-application-proxy-publish.md) -사용 하 여 hello 쉽고 빠르게 마법사 tooget 온-프레미스 앱을 게시 하 고 액세스할 수 있는 원격으로 합니다.

## <a name="whats-next"></a>다음 작업
첫 번째 앱을 게시하면 응용 프로그램 프록시를 사용하여 수행할 수 있는 작업은 많습니다.

* [Single Sign-On 사용](active-directory-application-proxy-sso-using-kcd.md)
* [고유한 도메인 이름을 사용하여 응용 프로그램 게시](active-directory-application-proxy-custom-domains.md)
* [Azure AD 응용 프로그램 프록시 커넥터에 대해 알아보기](application-proxy-understand-connectors.md)
* [기존 온-프레미스 프록시 서버 작업](application-proxy-working-with-proxy-servers.md) 
* [사용자 지정 홈페이지 설정](application-proxy-office365-app-launcher.md)

Hello 최신 뉴스 및 업데이트에 대 한 체크 아웃 hello [응용 프로그램 프록시 블로그](http://blogs.technet.com/b/applicationproxyblog/)

