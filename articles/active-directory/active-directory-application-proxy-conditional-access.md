---
title: "aaaConditional 액세스 tooon 온-프레미스 앱-Azure AD | Microsoft Docs"
description: "응용 프로그램에 대 한 조건부 액세스를 tooset 게시할 방법을 사용 하 여 원격으로 액세스할 toobe에서는 Azure AD 응용 프로그램 프록시입니다."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 2e97722b-eb4e-4078-b607-9fed210d8a0f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro; oldportal
ms.openlocfilehash: 7bed25dd4ba17941e77d8c4b2b9ba4edcf0cf597
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-conditional-access-in-azure-ad-application-proxy"></a>Azure AD 응용 프로그램 프록시에서 조건부 액세스 작업

>[!NOTE]
>이 문서는 사용 중지 되 고 Azure 클래식 포털 toohello 적용 됩니다. Hello를 사용 하는 것이 좋습니다 [Azure 포털](https://portal.azure.com)합니다. Hello Azure 포털에서에서 앱은 응용 프로그램 프록시 다른 SaaS 응용 프로그램 같은 조건부 액세스 기능을 hello 합니다. 조건부 액세스에 대해 자세히 toolearn 참조 [Azure Active Directory의 조건부 액세스 시작](active-directory-conditional-access-azure-portal-get-started.md)합니다.

액세스를 구성할 수 규칙 toogrant 조건부 액세스 tooapplications 응용 프로그램 프록시를 사용 하 여 게시 합니다. 다음을 수행할 수 있습니다.

* 응용 프로그램 당 Multi-Factor Authentication 요구
* 사용자가 직장이 아닌 경우 Multi-Factor Authentication 요구
* 사용자가 직장 되지 않은 hello 응용 프로그램에 액세스 하지 못하도록 차단

이러한 규칙은 적용된 tooall 사용자, 그룹 또는 toospecific 사용자 및 그룹 될 수 있습니다. 기본적으로 hello 규칙이 toohello 응용 프로그램 액세스 권한이 있는 tooall 사용자가 적용 합니다. 그러나 hello 규칙은 지정 된 보안 그룹의 구성원 인 toousers 제한 될 수도 있습니다.  

사용자가 OAuth 2.0, OpenID Connect, SAML 또는 WS-Federation을 사용하는 페더레이션된 응용 프로그램에 액세스할 때 액세스 규칙이 평가됩니다. 또한 새로 고침 토큰이 사용 되는 액세스 토큰을 tooacquire 경우 OAuth 2.0 및 OpenID Connect 액세스 규칙이 평가 됩니다.

## <a name="conditional-access-prerequisites"></a>조건부 액세스 필수 조건
* 구독 tooAzure Active Directory Premium
* 페더레이션 또는 관리되는 Azure Active Directory 테넌트
* 페더레이션된 테넌트가 MFA(Multi-Factor Authentication) 요구  
    ![액세스 규칙 구성 - 다단계 인증 필요](./media/active-directory-application-proxy-conditional-access/application-proxy-conditional-access.png)

## <a name="configure-per-application-multi-factor-authentication"></a>응용 프로그램당 Multi-Factor Authentication 구성
1. Azure 클래식 포털 hello에 관리자 권한으로 로그인 합니다.
2. 디렉터리 tooActive 이동한 다음 응용 프로그램 프록시 tooenable 원하는 hello 디렉터리를 선택 합니다.
3. 클릭 **응용 프로그램** 및 toohello 아래로 스크롤하여 **액세스 규칙** 섹션. hello 액세스 규칙 섹션 페더레이션된 인증을 사용 하는 응용 프로그램 응용 프로그램 프록시를 사용 하 여 게시에 나타납니다.
4. 선택 하 여 hello 규칙 설정 **액세스 규칙을 사용 하도록 설정** 너무**에**합니다.
5. Hello 사용자 및 그룹 toowhom hello 적용 되는 규칙을 지정 합니다. 사용 하 여 hello **그룹 추가** 단추 tooselect toowhich hello 액세스 규칙이 적용 되는 그룹을 하나 이상 있습니다. 이 대화 상자에 사용 되는 tooremove 선택 그룹 될 수도 있습니다.  지정 된 hello tooone 속해 있는 사용자에 대해서만 hello 액세스 규칙을 적용 hello 규칙은 선택한 tooapply toogroups 때 보안 그룹입니다.  

   * tooexplicitly hello 규칙에서 보안 그룹 제외 확인 **제외 하 고** 하나 이상의 그룹을 지정 합니다. Hello 제외 하 고 목록에서에서 그룹의 구성원 인 사용자 필요한 tooperform 다단계 인증 되지 않습니다.  
   * Hello 사용자별 다단계 인증 기능을 사용 하 여 사용자가 구성 된 경우이 설정은 우선 hello 응용 프로그램 다단계 인증 규칙 합니다. 사용자가 사용자별으로 multi-factor authentication에 대해 구성 된은 hello 응용 프로그램의 다단계 인증 규칙에서 제외 된 경우에 필요한 tooperform 다단계 인증입니다. [Multi-Factor Authentication 및 사용자별 설정](../multi-factor-authentication/multi-factor-authentication.md)에 대해 자세히 알아보세요.
6. 원하는 tooset hello 액세스 규칙을 선택 합니다.

   * **Multi-factor authentication 필요**: toowhom 액세스 규칙이 적용 되는 사용자는 필요한 toocomplete 다단계 인증 전에 hello 응용 프로그램에 액세스 toowhich hello 규칙이 적용 됩니다.
   * **Multi-factor authentication이 아닐 때 작업 요구**: 신뢰할 수 있는 IP 주소에서 tooaccess hello 응용 프로그램을 시도 하는 사용자는 필요한 tooperform 다단계 인증 되지 것입니다. hello 신뢰 hello 다단계 인증 설정 페이지에서 IP 주소 범위를 구성할 수 있습니다.
   * **이 아닐 때 작업 액세스를 차단**: tooaccess hello 응용 프로그램에서 회사 네트워크 외부를 시도 하는 사용자 수 tooaccess hello 응용 프로그램을 되지 것입니다.

## <a name="configuring-mfa-for-federation-services"></a>페더레이션 서비스에 대한 MFA 구성
페더레이션된 테 넌 트에 대 한 multi-factor authentication (MFA) 수행할 수 있습니다 hello 또는 Azure Active Directory에서 온-프레미스 AD FS 서버입니다. 기본적으로 MFA는 Azure Active Directory에서 호스팅되는 모든 페이지에 발생합니다. tooconfigure MFA 온-프레미스에서 Windows PowerShell을 사용 하 여 hello – SupportsMFA 속성 tooset hello Azure AD 모듈을 실행 합니다.

hello 다음 예제에서는 어떻게 tooenable 온-프레미스 MFA hello를 사용 하 여 [Set-msoldomainfederationsettings cmdlet](https://msdn.microsoft.com/library/azure/dn194088.aspx) hello contoso.com 테 넌 트에:`Set-MsolDomainFederationSettings -DomainName contoso.com -SupportsMFA $true `

또한 toosetting이이 플래그를 hello 페더레이션된 테 넌 트 AD FS 인스턴스 해야 tooperform 다단계 인증을 구성 합니다. 에 대 한 hello 지침 [Microsoft Azure multi-factor authentication이 온-프레미스 배포](../multi-factor-authentication/multi-factor-authentication-get-started-server.md)합니다.

## <a name="see-also"></a>참고 항목
* [클레임 인식 응용 프로그램으로 작업](active-directory-application-proxy-claims-aware-apps.md)
* [응용 프로그램 프록시를 사용하여 응용 프로그램 게시](active-directory-application-proxy-publish.md)
* [Single Sign-On 사용](active-directory-application-proxy-sso-using-kcd.md)
* [고유한 도메인 이름을 사용하여 응용 프로그램 게시](active-directory-application-proxy-custom-domains.md)

Hello 최신 뉴스 및 업데이트에 대 한 체크 아웃 hello [응용 프로그램 프록시 블로그](http://blogs.technet.com/b/applicationproxyblog/)
