---
title: "aaaProblem toohello 액세스 패널 웹 사이트에 로그인 | Microsoft Docs"
description: "Toosign toouse에서 시도 하는 동안 발생할 수 있는 지침 tootroubleshoot 문제 hello 액세스 패널"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.reviwer: japere
ms.openlocfilehash: 1037f7c5fbaa9425760ad5739b383c716d5fc3a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="problem-signing-in-toohello-access-panel-website"></a>Toohello 액세스 패널 웹 사이트에 로그인 하는 문제

액세스 패널 hello 활성화 있는 사용자가 회사 또는 학교 계정을 Azure Active Directory (Azure AD) tooview 및 시작 클라우드 기반 응용 프로그램에서 해당 관리자에 게 Azure AD는 웹 기반 포털이 부여 해 준에 대 한 액세스입니다. Azure AD 버전을 가진 사용자는 셀프 서비스 그룹 및 hello 액세스 패널을 통해 응용 프로그램 관리 기능 사용할 수도 있습니다. 액세스 패널 hello는 hello Azure 포털에서에서 분리 되 고 사용자가 toohave Azure 구독이 필요 하지 않습니다.

Azure AD에 회사 또는 학교 계정이 있는 경우 사용자가 액세스 패널 toohello 로그인 수 있습니다.

-   사용자는 Azure AD에서 직접 인증을 받을 수 있습니다.

-   사용자는 AD FS(Active Directory Federation Services)를 사용하여 인증을 받을 수 있습니다.

-   사용자는 Windows Server Active Directory에서 인증을 받을 수 있습니다.

사용자는 Azure 또는 Office 365에 대 한 구독을 보유 하 고 hello Azure 포털 또는 Office 365 응용 프로그램에서 사용, 경우 할 것 수 toouse toosign에 다시 필요 없이 액세스 패널을 원활 하 게 hello 합니다. 인증 되지 않은 사용자의 Azure AD에서 자신의 계정에 대 한 hello 사용자 이름 및 암호를 사용 하 여에서 증명된 toosign 수.입니다. Hello 조직에서 페더레이션을 구성한 경우 만으로는 hello 사용자 이름을 입력 합니다.

## <a name="general-issues-toocheck-first"></a>일반 toocheck를 먼저 문제 

-   Hello 사용자가 로그인 하 여 toohello에 있는지 확인 **올바른 URL**: <https://myapps.microsoft.com>

-   Hello 사용자의 브라우저 hello URL tooits가 추가 되었는지 확인 **신뢰할 수 있는 사이트**

-   Hello 사용자의 계정이 인지 확인 **활성화** 에 로그인 합니다.

-   Hello 사용자의 계정이 인지 확인 **잠겨 있지 않으면입니다.**

-   있는지 hello 사용자 확인 **암호를 만료 하거나 잊어버린 되지 않습니다.**

-   **Multi-Factor Authentication**에서 사용자 액세스를 차단하지 않는지 확인합니다.

-   **조건부 액세스 정책** 또는 **ID 보호** 정책이 사용자 액세스를 차단하지 않는지 확인합니다.

-   다음 사항을 확인 한 사용자의 **인증 연락처 정보** toodate tooallow Multi-factor Authentication 또는 조건부 액세스 정책 toobe 적용 중일 합니다.

-   확인 되었는지 tooalso try 브라우저의 쿠키를 지우고 toosign에 다시 시도 합니다.

## <a name="meeting-browser-requirements-for-hello-access-panel"></a>액세스 패널 hello에 대 한 브라우저 요구 사항 충족

hello 액세스 패널을 지 원하는 JavaScript 브라우저 필요 하 고 CSS를 활성화 합니다. toouse 암호 기반 single 로그온 (SSO)에서 액세스 패널 액세스 패널 확장 hello hello hello 사용자 브라우저에 설치 되어야 합니다. 사용자가 암호 기반 SSO에 구성된 응용 프로그램을 선택할 때 이 확장이 자동으로 다운로드됩니다.

암호 기반 SSO에 대 한 hello 최종 사용자의 브라우저 될 수 있습니다.

-   Internet Explorer 8, 9, 10, 11 - Windows 7 이상

-   Windows 10 Anniversary Edition 이상 Edge 

-   Chrome - Windows 7 이상 및 Mac OS X 이상

-   Firefox 26.0 이상 - Windows XP SP2 이상 및 Mac OS X 10.6 이상


## <a name="problems-with-hello-users-account"></a>Hello 사용자 계정과 관련 된 문제

액세스 패널 액세스 toohello tooa 문제 hello 사용자 계정으로 인해 차단 될 수 있습니다. 다음 몇 가지 방법으로 사용자 및 해당 계정 설정과 관련된 문제를 해결할 수 있습니다.

-   [Azure Active Directory에 사용자의 계정이 존재하는지 확인](#check-if-a-user-account-exists-in-azure-active-directory)

-   [사용자의 계정 상태 확인](#check-a-users-account-status)

-   [사용자의 암호 다시 설정](#reset-a-users-password)

-   [셀프 서비스 암호 재설정 사용](#enable-self-service-password-reset)

-   [사용자의 Multi-Factor Authentication 상태 확인](#check-a-users-multi-factor-authentication-status)

-   [사용자의 인증 연락처 정보 확인](#check-a-users-authentication-contact-info)

-   [사용자의 그룹 구성원 자격 확인](#check-a-users-group-memberships)

-   [사용자의 할당된 라이선스 확인](#check-a-users-assigned-licenses)

-   [사용자에게 라이선스 할당](#assign-a-user-a-license)

### <a name="check-if-a-user-account-exists-in-azure-active-directory"></a>Azure Active Directory에 사용자의 계정이 존재하는지 확인

아래의 hello 단계를 수행 하는 사용자의 계정이 표시 되 면 toocheck:

1.  열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**

2.  열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.

3.  에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.

4.  클릭 **사용자 및 그룹** hello 탐색 메뉴에 있습니다.

5.  **모든 사용자**를 클릭합니다.

6.  **검색** 에 관심이 있는 hello 사용자에 대 한 및 **hello 행 클릭** tooselect 합니다.

7.  Hello 속성의 hello 사용자 개체 toobe 고 없는 데이터가 누락 된 표시 되어 있는지 확인 합니다.

### <a name="check-a-users-account-status"></a>사용자의 계정 상태 확인

toocheck 사용자의 계정 상태, 아래의 hello 단계를 수행 합니다.

1.  열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**

2.  열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.

3.  에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.

4.  클릭 **사용자 및 그룹** hello 탐색 메뉴에 있습니다.

5.  **모든 사용자**를 클릭합니다.

6.  **검색** 에 관심이 있는 hello 사용자에 대 한 및 **hello 행 클릭** tooselect 합니다.

7.  **프로필**을 클릭합니다.

8.  **설정** 되도록 **블록 로그인** 너무 설정 되어**아니요**합니다.

### <a name="reset-a-users-password"></a>사용자의 암호 다시 설정

tooreset 사용자의 암호를 아래 hello 단계 수행:

1.  열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**

2.  열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.

3.  에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.

4.  클릭 **사용자 및 그룹** hello 탐색 메뉴에 있습니다.

5.  **모든 사용자**를 클릭합니다.

6.  **검색** 에 관심이 있는 hello 사용자에 대 한 및 **hello 행 클릭** tooselect 합니다.

7.  hello 클릭 **암호 재설정** hello hello 사용자 블레이드 위쪽에 단추입니다.

8.  hello 클릭 **암호 재설정** hello에서 단추 **암호 재설정** 블레이드를 표시 합니다.

9.  복사 hello **임시 암호** 또는 **새 암호를 입력** hello 사용자에 대 한 합니다.

10. 이 새 암호 toohello 사용자 통신, 필요한 toochange tooAzure Active Directory에에서 로그인 하는 동안 다음 번이이 암호를 수 있습니다.

### <a name="enable-self-service-password-reset"></a>셀프 서비스 암호 재설정 사용

tooenable 셀프 서비스 암호 재설정에 아래의 hello 배포 단계를 수행 하십시오.

-   [Azure Active Directory 암호 tooreset 사용자가 사용 하도록 설정](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-their-azure-ad-passwords)

-   [사용자가 tooreset를 사용 하거나 Active Directory 온-프레미스 암호 변경](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-or-change-their-ad-passwords)

### <a name="check-a-users-multi-factor-authentication-status"></a>사용자의 Multi-Factor Authentication 상태 확인

toocheck 사용자의 다단계 인증 상태, 다음 단계에 따라 hello:

1.  열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**

2.  열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.

3.  에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.

4.  클릭 **사용자 및 그룹** hello 탐색 메뉴에 있습니다.

5.  **모든 사용자**를 클릭합니다.

6.  hello 클릭 **Multi-factor Authentication** hello hello 블레이드 위쪽에 단추입니다.

7.  한 번 hello **Multi-factor Authentication 관리 포털** 부하를 hello에 있는 확인 하십시오 **사용자** 탭 합니다.

8.  검색, 필터링 또는 정렬 하 여 hello 사용자 목록에서 hello 사용자를 찾을 수 있습니다.

9.  사용자의 hello 목록에서 선택 hello 사용자 및 **사용**, **사용 하지 않도록 설정**, 또는 **적용** 원하는 대로 다단계 인증 합니다.

   >[!NOTE]
   >사용자가 있는 경우에 **Enforced** 상태 이면 너무 설정할 수 있습니다**비활성화 된** 일시적으로 toolet 다시 자신의 계정에 있습니다. 인 다시 변경할 수 있습니다 다음 상태로 너무**Enabled** toorequire 다시 해당 toore 레지스터 그들의 연락처 정보 중 다음 번에 로그인 합니다. Hello의 hello 단계를 수행 수 또는 [사용자의 인증 연락처 정보를 확인](#check-a-users-authentication-contact-info) tooverify 하거나 하에이 데이터를 설정 합니다.
   >
   >

### <a name="check-a-users-authentication-contact-info"></a>사용자의 인증 연락처 정보 확인

아래의 hello 단계를 수행 하는 사용자의 인증 연락처 정보 multi-factor authentication, 조건부 액세스, Id 보호 및 암호 재설정에 사용 되는 toocheck:

1.  열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**

2.  열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.

3.  에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.

4.  클릭 **사용자 및 그룹** hello 탐색 메뉴에 있습니다.

5.  **모든 사용자**를 클릭합니다.

6.  **검색** 에 관심이 있는 hello 사용자에 대 한 및 **hello 행 클릭** tooselect 합니다.

7.  **프로필**을 클릭합니다.

8.  너무 아래로 스크롤하여**인증 연락처 정보**합니다.

9.  **검토** 필요에 따라 hello 데이터 hello 사용자 및 업데이트에 등록 합니다.

### <a name="check-a-users-group-memberships"></a>사용자의 그룹 구성원 자격 확인

toocheck 사용자의 그룹 구성원 자격, 아래의 hello 단계를 수행 합니다.

1.  열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**

2.  열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.

3.  에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.

4.  클릭 **사용자 및 그룹** hello 탐색 메뉴에 있습니다.

5.  **모든 사용자**를 클릭합니다.

6.  **검색** 에 관심이 있는 hello 사용자에 대 한 및 **hello 행 클릭** tooselect 합니다.

7.  클릭 **그룹** toosee hello 사용자 그룹의 멤버인 합니다.

### <a name="check-a-users-assigned-licenses"></a>사용자의 할당된 라이선스 확인

toocheck 사용자의 라이선스를 다음 단계에 따라 hello 할당:

1.  열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**

2.  열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.

3.  에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.

4.  클릭 **사용자 및 그룹** hello 탐색 메뉴에 있습니다.

5.  **모든 사용자**를 클릭합니다.

6.  **검색** 에 관심이 있는 hello 사용자에 대 한 및 **hello 행 클릭** tooselect 합니다.

7.  클릭 **라이선스** toosee 현재 어떤 라이선스 hello 사용자에 게 할당 합니다.

### <a name="assign-a-user-a-license"></a>사용자에게 라이선스 할당 

아래의 hello 단계를 수행 하는 라이선스 tooa 사용자 tooassign:

1.  열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**

2.  열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.

3.  에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.

4.  클릭 **사용자 및 그룹** hello 탐색 메뉴에 있습니다.

5.  **모든 사용자**를 클릭합니다.

6.  **검색** 에 관심이 있는 hello 사용자에 대 한 및 **hello 행 클릭** tooselect 합니다.

7.  클릭 **라이선스** toosee 현재 어떤 라이선스 hello 사용자에 게 할당 합니다.

8.  Hello 클릭 **할당** 단추입니다.

9.  선택 **하나 이상의 제품** hello 사용 가능한 제품 목록에서 합니다.

10. **선택적** hello 클릭 **할당 옵션** 항목 toogranularly 제품을 할당 합니다. 완료되면 **확인**을 클릭합니다.

11. Hello 클릭 **할당** tooassign 이러한 라이선스 toothis 사용자 단추입니다.

## <a name="if-these-troubleshooting-steps-do-not-resolve-hello-issue"></a>이러한 문제 해결 단계 hello 문제가 해결 되지 않는 경우

사용 가능한 경우 다음 정보는 hello로 지원 티켓을 엽니다.

-   상관 관계 오류 ID

-   UPN(사용자 전자 메일 주소)

-   테넌트 ID

-   브라우저 종류

-   오류가 발생하는 동안 표준 시간대 및 시간/기간

-   Fiddler 추적

## <a name="next-steps"></a>다음 단계
[응용 프로그램 프록시 single sign on tooyour 앱을 제공 합니다.](active-directory-application-proxy-sso-using-kcd.md)
