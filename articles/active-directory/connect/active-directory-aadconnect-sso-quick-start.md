---
title: "Azure AD Connect: Seamless Single Sign-On - 빠른 시작 | Microsoft Docs"
description: "이 문서에서는 Azure Active Directory 원활한 Single Sign-on을 tooget 시작 하는 방법을 설명 합니다."
services: active-directory
keywords: "Azure AD Connect의 정의, Active Directory 설치, Azure AD에 대한 필수 구성 요소, SSO, Single Sign-on"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: billmath
ms.openlocfilehash: 97d40ed41b3bfad9ff7e11ddbdb8de594ee85de1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-seamless-single-sign-on-quick-start"></a>Azure Active Directory Seamless Single Sign-On: 빠른 시작

## <a name="how-toodeploy-seamless-sso"></a>어떻게 toodeploy 원활한 SSO

Azure Active Directory 원활한 Single Sign-on (Azure AD 원활한 SSO) 자동으로 사용자가 자신의 회사 데스크톱 연결 된 tooyour 회사 네트워크에서 서로에 서명 합니다. 에 사용자가 쉽게 액세스할 tooyour 클라우드 기반 응용 프로그램 추가 온-프레미스 구성 요소 필요 없이 합니다.

>[!IMPORTANT]
>hello 원활한 SSO 기능은 현재 미리 보기 중입니다.

toofollow 해야 원활한 SSO toodeploy 다음이 단계:

## <a name="step-1-check-prerequisites"></a>1단계: 필수 조건 확인

필수 구성 요소를 다음 해당 hello 적절 한지 확인 합니다.

1. Azure AD Connect 서버 설정: 로그인 방법으로 [통과 인증](active-directory-aadconnect-pass-through-authentication.md)을 사용하는 경우 더 이상의 작업이 필요하지 않습니다. 로그인 방법으로 [암호 해시 동기화](active-directory-aadconnectsync-implement-password-synchronization.md)를 사용하고 Azure AD Connect와 Azure AD 사이에 방화벽이 있는 경우 다음을 확인합니다.
- Azure AD Connect 버전 1.1.484.0 이상을 사용하고 있습니다.
- Azure AD Connect 서버에서 `*.msappproxy.net` URL 및 443 포트를 통해 통신할 수 있습니다. 이 필수 구성이 요소는 실제 사용자 로그인에 대해 hello 기능을 사용 하도록 설정 하는 경우에 적용할 수 있습니다.
- Azure AD Connect 직접 IP 연결 toohello 정확해 [Azure 데이터 센터 IP 범위](https://www.microsoft.com/download/details.aspx?id=41653)합니다. 다시이 필수 구성이 요소는 hello 기능을 사용 하는 경우에 적용할 수 있습니다.
2. TooAzure AD를 동기화 하는 각 AD 포리스트에 대 한 도메인 관리자 자격 증명 필요 (Azure AD Connect를 사용 하 여) 및 원하는 tooenable 원활한 SSO 조직과 사용자에 대 한 합니다.

## <a name="step-2-enable-hello-feature"></a>2 단계: hello 기능 사용

Azure AD Seamless SSO는 [Azure AD Connect](active-directory-aadconnect.md)를 통해 사용하도록 설정할 수 있습니다.

Azure AD Connect의 새로 설치를 수행 하는 경우 선택 hello [사용자 지정 설치 경로가](active-directory-aadconnect-get-started-custom.md)합니다. 페이지 "사용자 로그인" hello hello "Enable single sign on" 옵션을 선택 합니다.

![Azure AD Connect - 사용자 로그인](./media/active-directory-aadconnect-sso/sso8.png)

Azure AD Connect가 이미 설치되어 있는 경우 Azure AD Connect에서 "사용자 로그인 변경 페이지"를 선택하고 "다음"을 클릭합니다. Hello "Enable single sign on" 옵션을 확인 합니다.

![Azure AD Connect - 사용자 로그인 변경](./media/active-directory-aadconnect-user-signin/changeusersignin.png)

Toohello "Enable single sign on" 페이지에 도달할 때까지 hello 마법사를 계속 합니다. TooAzure AD를 동기화 하는 각 AD 포리스트에 대 한 도메인 관리자 자격 증명을 제공 (Azure AD Connect를 사용 하 여) 및 원하는 tooenable 원활한 SSO 조직과 사용자에 대 한 합니다. 

Hello 마법사를 완료 한 후 테 넌 트에 원활한 SSO는 사용할 수 있습니다.

>[!NOTE]
> hello 도메인 관리자 자격 증명이 Azure AD 또는 Azure AD Connect에 저장 되지 않습니다 않는 사용 되는 tooenable hello 기능.

이러한 지침은 tooverify 원활한 SSO을 올바르게 설정 했는지를 수행 합니다.

1. Toohello 로그인 [Azure Active Directory 관리 센터](https://aad.portal.azure.com) 테 넌 트에 대 한 hello 전역 관리자 자격 증명을 사용 합니다.
2. 선택 **Azure Active Directory** hello 왼쪽 탐색 모음에 있습니다.
3. **Azure AD Connect**를 선택합니다.
4. 해당 hello 확인 **원활한 Single Sign-on** 기능으로 표시 **Enabled**합니다.

![Azure Portal - Azure AD Connect 블레이드](./media/active-directory-aadconnect-sso/sso10.png)

## <a name="step-3-roll-out-hello-feature"></a>3 단계: 롤아웃 hello 기능

tooroll hello 기능 tooyour 사용자가 Active Directory에서 그룹 정책을 통해 tooadd 두 (https://autologon.microsoftazuread-sso.com 및 https://aadg.windows.net.nsatc.net) Azure AD Url toousers' 인트라넷 영역 설정 해야합니다.

>[!NOTE]
> hello (Internet Explorer와 신뢰할 수 있는 사이트 Url의 집합을 공유) 하는 경우 Windows에서 Internet Explorer 및 Google Chrome에 대 한 지침만 작업을 수행 합니다. Mozilla Firefox 및 Google Chrome mac을 tooset 지침에 대 한 hello 다음 섹션을 읽어

### <a name="why-do-you-need-toomodify-users-intranet-zone-settings"></a>Toomodify 사용자 인트라넷 영역 설정을 왜 필요 합니까?

기본적으로 hello 브라우저 URL에서 hello 오른쪽 영역 (인터넷 또는 인트라넷) 자동으로 계산 합니다. 예를 들어 http://contoso/ 인 매핑된 toohello 인트라넷 영역 반면 http://intranet.contoso.com/ 매핑된 toohello 인터넷 영역 (하기 때문에 마침표를 포함 하는 hello URL). 해당 URL toohello 브라우저의 인트라넷 영역 명시적으로 추가 하지 않는 브라우저 hello 두 개의 Azure AD Url--같은 Kerberos 티켓 tooa 클라우드 끝점을 보내지 않습니다.

### <a name="detailed-steps"></a>자세한 단계

1. Hello 그룹 정책 관리 도구를 엽니다.
2. Hello 적용된 toosome 또는 모든 사용자가 그룹 정책을 편집 합니다. 이 예제에서는 사용 하 여 hello **기본 도메인 정책**합니다.
3. 너무 이동**사용자 구성 \ 관리 템플릿 \ Components\Internet 보게 제어 Panel\Security 페이지** 선택 **사이트 할당 목록 tooZone**합니다.
![Single Sign-On](./media/active-directory-aadconnect-sso/sso6.png)  
4. Hello 정책을 사용 하도록 설정 하 고 다음 값 (Azure AD Url Kerberos 티켓 전달 되어)에 hello 및 데이터 입력 (*1* 인트라넷 영역을 나타냅니다) hello 대화 상자에서.

        Value: https://autologon.microsoftazuread-sso.com
        Data: 1
        Value: https://aadg.windows.net.nsatc.net
        Data: 1
>[!NOTE]
> Toodisallow 원활한 SSO 액세스를 사용 하 여 예를 들어, 일부 사용자가 이러한 사용자가 공유 키오스크-에 로그인 하는 경우 설정 값 앞에 너무 hello*4*합니다. 이 작업 hello Azure AD Url toohello 제한 된 사이트 영역에 추가 하 고 원활한 SSO hello 항상 실패 합니다.

5. **확인**을 클릭하고 **확인**을 다시 클릭합니다.

![SSO(Single sign-on)](./media/active-directory-aadconnect-sso/sso7.png)

### <a name="browser-considerations"></a>브라우저 고려 사항

#### <a name="mozilla-firefox"></a>Mozilla Firefox

Mozilla Firefox는 Kerberos 인증을 자동으로 수행하지 않습니다. 각 사용자에 게 toomanually 단계를 수행 하는 hello를 사용 하 여 Azure AD hello Url tootheir Firefox 설정을 추가 합니다.
1. Firefox를 실행 하 고 입력 `about:config` hello 주소 표시줄에 있습니다. 표시되는 모든 알림을 해제합니다.
2. Hello에 대 한 검색 **network.negotiate-auth.trusted-uri** 기본 설정 합니다. 이 기본 설정은 Firefox의 신뢰할 수 있는 Kerberos 인증 사이트를 나열합니다.
3. 마우스 오른쪽 단추로 클릭하고 "수정"을 선택합니다.
4. 입력 "https://autologon.microsoftazuread-sso.com, https://aadg.windows.net.nsatc.net" hello 필드에 있습니다.
5. "확인"을 클릭 하 고 hello 브라우저를 다시 여세요.

#### <a name="safari-on-mac-os"></a>Mac OS의 Safari

Mac OS를 실행 하는 hello 컴퓨터 조인된 tooAD 확인 하십시오. 방법에 지침을 참조 하십시오. toodo 하 [여기](http://training.apple.com/pdf/Best_Practices_for_Integrating_OS_X_with_Active_Directory.pdf)합니다.

#### <a name="google-chrome-on-mac-os"></a>Mac OS의 Google 크롬

Mac OS 및 기타 Windows 이외의 플랫폼에서 Google Chrome에 대 한 참조 너무[이 여기서](https://dev.chromium.org/administrators/policy-list-3#AuthServerWhitelist) toowhitelist 통합된 인증에 대 한 Azure AD Url hello 하는 방법에 대 한 내용은 합니다.

제 3 자 Active Directory 그룹 정책을 사용 하 여 Mac 사용자에 게 Azure AD Url tooFirefox hello 및 Google Chrome 확장 tooroll가이 문서의 범위를 벗어난 경우

#### <a name="known-limitations"></a>알려진 제한 사항

Firefox 및 Edge 브라우저의 개인 검색 모드에서는 Seamless SSO가 작동하지 않습니다. 또한 실행 되지 Internet Explorer hello 브라우저 확장 된 보호 모드에서 실행 중인 경우.

>[!IMPORTANT]
>에서는 최근에 롤백 가장자리 tooinvestigate에 대 한 지원 고객이 신고한 문제.

## <a name="step-4-test-hello-feature"></a>4 단계: hello 기능 테스트

특정 사용자에 대 한 tootest hello 기능을 확인할 _모든_ hello 다음 조건이 적용 됩니다.
  - hello 사용자가 회사 장치 로그온 합니다.
  - hello 장치를 이전에 결합 된 tooyour Active Directory (AD) 도메인 되었습니다.
  - hello 장치에 직접 연결 tooyour DC (도메인 컨트롤러)를 찾거나 hello 회사 유선 또는 무선 네트워크에 VPN 연결과 같이 원격 액세스 연결을 통해 있습니다.
  - 있는 [hello 기능 롤아웃](##step-3-roll-out-the-feature) toothis 사용자 그룹 정책을 사용 하 여 합니다.

tootest hello 시나리오 hello 사용자가 hello 사용자 이름, 하지만 하지 hello 암호를 입력 하는 위치:
- 새 개인 브라우저 세션에서 *https://myapps.microsoft.com/*에 로그인합니다.

tootest hello 시나리오를 hello 권한이 없습니다. tooenter hello 사용자 이름 또는 hello 암호: 
- 새 개인 브라우저 세션에서 *https://myapps.microsoft.com/contoso.onmicrosoft.com*에 로그인합니다. "*contoso*"를 테넌트의 이름으로 바꿉니다.
- 또는 새 개인 브라우저 세션에서 *https://myapps.microsoft.com/contoso.com*에 로그인합니다. "*contoso.com*"을 테넌트에서 확인된 도메인(페더레이션 도메인이 아님)으로 바꿉니다.

## <a name="step-5-roll-over-keys"></a>5단계: 키 롤오버

2 단계에서에서 Azure AD Connect를 사용 하도록 설정한 원활한 SSO 모든 hello AD 포리스트에의 컴퓨터 계정 (Azure AD를 나타냄)를 만듭니다. [여기](active-directory-aadconnect-sso-how-it-works.md)에서 자세히 알아보세요. 보안 향상된을 위해 이러한 컴퓨터 계정의 hello Kerberos 암호 해독 키를 자주 롤오버는 것이 좋습니다.

>[!IMPORTANT]
>이 단계 toodo 필요 하지 않습니다 _즉시_ hello 기능을 활성화 한 경우. 30 일 마다 적어도 hello Kerberos 암호 해독 키 롤오버 됩니다.

## <a name="next-steps"></a>다음 단계

- [**기술 심층 분석**](active-directory-aadconnect-sso-how-it-works.md) - 이 기능의 작동 방식을 이해합니다.
- [**질문과 대답** ](active-directory-aadconnect-sso-faq.md) -toofrequently 질문과 대답을 제공 합니다.
- [**문제를 해결** ](active-directory-aadconnect-troubleshoot-sso.md) -tooresolve 공통 hello 기능으로 발급 하는 방법에 대해 알아봅니다.
- [**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - 새로운 기능 요청을 제출합니다.
