---
title: "aaaProblems tooa Microsoft 응용 프로그램에에서 서명 | Microsoft Docs"
description: "Toofirst 파티 Microsoft Azure AD (예: Office 365)를 사용 하 여 응용 프로그램에 로그인 할 때 직면 하는 일반적인 문제 해결"
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
ms.openlocfilehash: 35849ca8dbaa909d17b6d0da572f5c11041a8559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
## <a name="problems-signing-in-tooa-microsoft-application"></a>Tooa Microsoft 응용 프로그램에에서 로그인 하는 문제

타사 SaaS 응용 프로그램 또는 Single Sign-On을 위해 Azure AD와 통합하는 다른 응용 프로그램과는 약간 다른 방법으로 Microsoft 응용 프로그램(예: Office 365 Exchange, SharePoint, Yammer 등)을 할당하고 관리합니다.

사용자 액세스 tooa Microsoft 게시 된 응용 프로그램을 얻을 수 있는 세 가지 주요 방법이 있습니다.

-   Hello Office 365 또는 다른 유료 도구 모음에서 응용 프로그램에 대 한 사용자 액세스를 통해 부여 됩니다 **라이선스 할당** 하거나 직접 tootheir 사용자 계정 또는 그룹 기반의 라이선스 할당 기능을 사용 하 여 그룹을 통해.

-   Microsoft 소프트웨어 또는 세 번째 파티 게시 자유롭게 누구나 toouse 응용 프로그램에 대 한 사용자가 부여할 수 있습니다를 통한 액세스 **사용자 동의**합니다. This0 있음을 나타내는 Azure AD의 직장 또는 학교 계정으로 toohello 응용 프로그램에 로그인 계정에 데이터 집합이 액세스 제한 toosome toohave 허용 합니다.

-   Microsoft 소프트웨어 또는 3rd 파티 게시 자유롭게 누구나 toouse 응용 프로그램에 대 한 사용자 수 또한 권한을 부여 통해 **관리자의 동의가**합니다. 즉, 전역 관리자 계정 가진 toohello 응용 프로그램에 로그인 하 고 액세스 tooeveryone hello 조직에서 부여 있도록 hello 조직의 모든 사용자가 hello 응용 프로그램을 사용할 수 있습니다는 관리자가 결정 합니다.

tootroubleshoot hello로 시작 문제를 [응용 프로그램 액세스 tooconsider로 일반적인 문제 영역](#general-problem-areas-with-application-access-to-consider) hello 읽습니다 [연습: Microsoft 응용 프로그램 액세스 단계 tootroubleshoot](#walkthrough-steps-to-troubleshoot-microsoft-application-access) hello 세부 정보로 tooget 합니다.

## <a name="general-problem-areas-with-application-access-tooconsider"></a>응용 프로그램 액세스 tooconsider로 일반적인 문제 영역

다음 목록은 hello toostart, 하지만 권장할 신속 하 게 진행 하는 hello 연습 tooget 읽기의 방법이 있는 경우 드릴 수 있는 일반적인 문제 영역: [연습: Microsoft 응용 프로그램 액세스단계tootroubleshoot](#walkthrough-steps-to-troubleshoot-microsoft-application-access).

-   [Hello 사용자 계정과 관련 된 문제](#problems-with-the-users-account)

-   [그룹과 관련된 문제](#problems-with-groups)

-   [조건부 액세스 정책과 관련된 문제](#problems-with-conditional-access-policies)

-   [응용 프로그램 동의와 관련된 문제](#problems-with-application-consent)

## <a name="steps-tootroubleshoot-microsoft-application-access"></a>단계 tootroubleshoot Microsoft 응용 프로그램 액세스

아래 몇 가지 일반적인 문제 동료 들을 때 실행가 사용자에 게 tooa Microsoft 응용 프로그램에 로그인 할 수 없습니다.

-   일반 toocheck를 먼저 문제

  * Hello 사용자가 로그인 하 여 toohello에 있는지 확인 **올바른 URL** 및 로컬 응용 프로그램 URL이 아니기 때문입니다.

  * Hello 사용자의 계정이 인지 확인 **잠겨 있지 않으면입니다.**

  * 있는지 hello 확인 **사용자의 계정이 존재** Azure Active Directory에 있습니다. [Azure Active Directory에 사용자의 계정이 존재하는지 확인](#problems-with-the-users-account)

  * Hello 사용자의 계정이 인지 확인 **활성화** 에 로그인 합니다. [사용자의 계정 상태 확인](#problems-with-the-users-account)

  * 있는지 hello 사용자 확인 **암호를 만료 하거나 잊어버린 되지 않습니다.** [사용자의 암호 재설정](#reset-a-users-password) 또는 [셀프 서비스 암호 재설정 사용](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started)

   * **Multi-Factor Authentication**에서 사용자 액세스를 차단하지 않는지 확인합니다. [사용자의 Multi-Factor Authentication 상태 확인](#check-a-users-multi-factor-authentication-status) 또는 [사용자의 인증 연락처 정보 확인](#check-a-users-authentication-contact-info)

   * **조건부 액세스 정책** 또는 **ID 보호** 정책이 사용자 액세스를 차단하지 않는지 확인합니다. [특정 조건부 액세스 정책 확인](#problems-with-conditional-access-policies) 또는 [특정 응용 프로그램의 조건부 액세스 정책 확인](#check-a-specific-applications-conditional-access-policy) 또는 [특정 조건부 액세스 정책 사용 안 함](#disable-a-specific-conditional-access-policy)

   * 다음 사항을 확인 한 사용자의 **인증 연락처 정보** toodate tooallow Multi-factor Authentication 또는 조건부 액세스 정책 toobe 적용 중일 합니다. [사용자의 Multi-Factor Authentication 상태 확인](#check-a-users-multi-factor-authentication-status) 또는 [사용자의 인증 연락처 정보 확인](#check-a-users-authentication-contact-info)

-   에 대 한 **Microsoft** **라이선스를 필요로 하는 응용 프로그램** (예: office 365), 다음은 몇 가지 특정 문제 toocheck 위의 일반적인 문제 hello 아닌 경우:

   * Hello 사용자 확인 되었거나는 **라이선스가 할당 합니다.** [사용자의 할당된 라이선스 확인](#check-a-users-assigned-licenses) 또는 [그룹의 할당된 라이선스 확인](#check-a-groups-assigned-licenses)

   * Hello 라이선스가 **tooa 할당** **정적 그룹**, 해당 hello 확인 **사용자가 멤버인** 해당 그룹의 합니다. [사용자의 그룹 구성원 자격 확인](#check-a-users-group-memberships)

   * Hello 라이선스가 **tooa 할당** **동적 그룹**, 해당 hello 확인 **동적 그룹 규칙을 올바르게 설정**합니다. [동적 그룹의 구성원 자격 조건 확인](#check-a-dynamic-groups-membership-criteria)

   * Hello 라이선스가 **tooa 할당** **동적 그룹**, 해당 hello 동적 그룹에 있는지 확인 **처리가 완료** 구성원 자격 및 해당 hello **사용자가을 멤버** (다소 시간이 걸릴 수 있습니다). [사용자의 그룹 구성원 자격 확인](#check-a-users-group-memberships)

   *  Hello 라이선스가 할당 되었는지 확인 하면 hello 라이선스가 있는지 확인 **만료 되지**합니다.

   *  Hello 라이선스가 있는지 확인 **hello 응용 프로그램에 대 한** 에 액세스 합니다.

-   에 대 한 **Microsoft** **라이선스를 필요로 하지 않는 응용 프로그램**, 일부 다른 작업 toocheck 다음과 같습니다.

   * Hello 응용 프로그램을 요청 하는 경우 **사용자 수준 권한** 해당 hello 사용자가 toohello 응용 프로그램에 로그인 하 고가 수행 되었는지 확인 (예를 들어 "이이 사용자의이 사서함")에 액세스 한 **사용자 동의 작업**  toolet hello 응용 프로그램의 데이터에 액세스 합니다.

   * Hello 응용 프로그램을 요청 하는 경우 **관리자 수준 사용 권한이** 전역 관리자가 수행 했는지 있는지 확인 (예를 들어 "모든 사용자의 사서함")에 액세스 한 **에서 관리자 권한으로 승인 작업 모든 사용자를 대신 하 여** hello 조직에 있습니다.

## <a name="problems-with-hello-users-account"></a>Hello 사용자 계정과 관련 된 문제

기한 tooa 문제 toohello 응용 프로그램에 할당 된 사용자와 응용 프로그램 액세스를 차단할 수 있습니다. 다음 몇 가지 방법으로 사용자 및 해당 계정 설정과 관련된 문제를 해결할 수 있습니다.

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

  * **참고**: 사용자가 있는 경우에 **Enforced** 상태 이면 너무 설정할 수 있습니다**비활성화 된** 일시적으로 toolet 다시 자신의 계정에 있습니다. 인 다시 변경할 수 있습니다 다음 상태로 너무**Enabled** toorequire 다시 해당 toore 레지스터 그들의 연락처 정보 중 다음 번에 로그인 합니다. Hello의 hello 단계를 수행 수 또는 [사용자의 인증 연락처 정보를 확인](#check-a-users-authentication-contact-info) tooverify 하거나 하에이 데이터를 설정 합니다.

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

## <a name="problems-with-groups"></a>그룹과 관련된 문제

Tooa 문제 toohello 응용 프로그램에 할당 된 그룹으로 인해 응용 프로그램 액세스를 차단할 수 있습니다. 다음 몇 가지 방법으로 그룹 및 구성원 자격과 관련된 문제를 해결할 수 있습니다.

-   [그룹의 구성원 자격 확인](#check-a-groups-membership)

-   [동적 그룹의 구성원 자격 조건 확인](#check-a-dynamic-groups-membership-criteria)

-   [그룹의 할당된 라이선스 확인](#check-a-groups-assigned-licenses)

-   [그룹의 라이선스 다시 처리](#reprocess-a-groups-licenses)

-   [그룹에 라이선스 할당](#assign-a-group-a-license)

### <a name="check-a-groups-membership"></a>그룹의 구성원 자격 확인

toocheck 그룹의 구성원, 다음 단계에 따라 hello:

1.  열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**

2.  열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.

3.  에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.

4.  클릭 **사용자 및 그룹** hello 탐색 메뉴에 있습니다.

5.  **모든 그룹**을 클릭합니다.

6.  **검색** 에 관심이 있는 hello 그룹에 대 한 및 **hello 행 클릭** tooselect 합니다.

7.  클릭 **멤버** 사용자 tooreview hello 목록 toothis 그룹을 할당 합니다.

### <a name="check-a-dynamic-groups-membership-criteria"></a>동적 그룹의 구성원 자격 조건 확인 

toocheck 아래의 hello 단계를 수행 하는 동적 그룹 멤버 자격 기준:

1.  열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**

2.  열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.

3.  에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.

4.  클릭 **사용자 및 그룹** hello 탐색 메뉴에 있습니다.

5.  **모든 그룹**을 클릭합니다.

6.  **검색** 에 관심이 있는 hello 그룹에 대 한 및 **hello 행 클릭** tooselect 합니다.

7.  **동적 구성원 자격 규칙**을 클릭합니다.

8.  검토 hello **간단한** 또는 **고급** 이 그룹에 대해 정의 된 규칙 및 해당 toobe이이 그룹의 구성원 hello 사용자를 이러한 조건을 충족 하는지 확인 합니다.

### <a name="check-a-groups-assigned-licenses"></a>그룹의 할당된 라이선스 확인

toocheck 그룹의 할당 된 라이선스를 아래 hello 단계 수행:

1.  열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**

2.  열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.

3.  에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.

4.  클릭 **사용자 및 그룹** hello 탐색 메뉴에 있습니다.

5.  **모든 그룹**을 클릭합니다.

6.  **검색** 에 관심이 있는 hello 그룹에 대 한 및 **hello 행 클릭** tooselect 합니다.

7.  클릭 **라이선스** toosee 현재 hello 라이선스 그룹에 할당 합니다.

### <a name="reprocess-a-groups-licenses"></a>그룹의 라이선스 다시 처리

tooreprocess 그룹의 할당 된 라이선스를 아래 hello 단계 수행:

1.  열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**

2.  열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.

3.  에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.

4.  클릭 **사용자 및 그룹** hello 탐색 메뉴에 있습니다.

5.  **모든 그룹**을 클릭합니다.

6.  **검색** 에 관심이 있는 hello 그룹에 대 한 및 **hello 행 클릭** tooselect 합니다.

7.  클릭 **라이선스** toosee 현재 hello 라이선스 그룹에 할당 합니다.

8.  hello 클릭 **다시 처리** 라이선스가 할당 toothis 그룹의 구성원 hello 단추 tooensure 최신 상태로 유지 됩니다. Hello 그룹의 hello 크기와 복잡성에 따라 시간이 오래 걸릴 수 있습니다.

   >[!NOTE]
   >toodo이 더 빨리 고려 임시로 라이선스 toohello 사용자를 직접 지정 합니다. [사용자에게 라이선스를 할당합니다](#problems-with-application-consent).
   >
   >

### <a name="assign-a-group-a-license"></a>그룹에 라이선스 할당

아래의 hello 단계를 수행 하는 라이선스 tooa 그룹을 tooassign:

1.  열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**

2.  열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.

3.  에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.

4.  클릭 **사용자 및 그룹** hello 탐색 메뉴에 있습니다.

5.  **모든 그룹**을 클릭합니다.

6.  **검색** 에 관심이 있는 hello 그룹에 대 한 및 **hello 행 클릭** tooselect 합니다.

7.  클릭 **라이선스** toosee 현재 hello 라이선스 그룹에 할당 합니다.

8.  Hello 클릭 **할당** 단추입니다.

9.  선택 **하나 이상의 제품** hello 사용 가능한 제품 목록에서 합니다.

10. **선택적** hello 클릭 **할당 옵션** 항목 toogranularly 제품을 할당 합니다. 완료되면 **확인**을 클릭합니다.

11. Hello 클릭 **할당** tooassign 이러한 라이선스 toothis 그룹 단추입니다. Hello 그룹의 hello 크기와 복잡성에 따라 시간이 오래 걸릴 수 있습니다.

   >[!NOTE]
   >toodo이 더 빨리 고려 임시로 라이선스 toohello 사용자를 직접 지정 합니다. [사용자에게 라이선스를 할당합니다](#problems-with-application-consent).
   > 
   >

## <a name="problems-with-conditional-access-policies"></a>조건부 액세스 정책과 관련된 문제

### <a name="check-a-specific-conditional-access-policy"></a>특정 조건부 액세스 정책 확인

toocheck 또는 단일 조건부 액세스 정책의 유효성을 검사 합니다.

1.  열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**

2.  열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.

3.  에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.

4.  클릭 **엔터프라이즈 응용 프로그램** hello 탐색 메뉴에 있습니다.

5.  hello 클릭 **조건부 액세스** 탐색 항목입니다.

6.  검사 하려는 hello 정책을 클릭 합니다.

7.  특정 조건, 할당 또는 사용자 액세스를 차단할 수 있는 기타 설정이 없는지 검토합니다.

   >[!NOTE]
   >이 정책 tooensure 것 적용 되지 않는 기호 안함 toodo이, 집합 hello tootemporarily 비활성화를 지정할 수 있습니다 **정책 사용** 너무 설정/해제**아니요** hello를 클릭 하 고 **저장** 단추 .
   >
   >

### <a name="check-a-specific-applications-conditional-access-policy"></a>특정 응용 프로그램의 조건부 액세스 정책 확인

toocheck 단일 응용 프로그램의 현재 구성 된 조건부 액세스 정책을 유효성을 검사 합니다.

1.  열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**

2.  열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.

3.  에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.

4.  클릭 **엔터프라이즈 응용 프로그램** hello 탐색 메뉴에 있습니다.

5.  **모든 응용 프로그램**을 클릭합니다.

6.  검색은 toosign tooby 응용 프로그램에서 시도 관심 있는 또는 사용자를 환영 hello 응용 프로그램에 대 한 표시 이름 또는 응용 프로그램 id입니다.

     >[!NOTE]
     >Hello 응용 프로그램에 대 한 원하는 보이지 않으면 클릭 hello **필터** 단추 및 hello 목록의 hello 범위가 너무 확장 되는**모든 응용 프로그램**합니다. Toosee 더 많은 열을 클릭 hello **열** 응용 프로그램에 대 한 추가 세부 정보 tooadd 단추입니다.
     >
     >

7.  hello 클릭 **조건부 액세스** 탐색 항목입니다.

8.  검사 하려는 hello 정책을 클릭 합니다.

9.  특정 조건, 할당 또는 사용자 액세스를 차단할 수 있는 기타 설정이 없는지 검토합니다.

     >[!NOTE]
     >이 정책 tooensure 것 적용 되지 않는 기호 안함 toodo이, 집합 hello tootemporarily 비활성화를 지정할 수 있습니다 **정책 사용** 너무 설정/해제**아니요** hello를 클릭 하 고 **저장** 단추 .
     >
     >

### <a name="disable-a-specific-conditional-access-policy"></a>특정 조건부 액세스 정책 사용 안 함

toocheck 또는 단일 조건부 액세스 정책의 유효성을 검사 합니다.

1.  열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**

2.  열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.

3.  에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.

4.  클릭 **엔터프라이즈 응용 프로그램** hello 탐색 메뉴에 있습니다.

5.  hello 클릭 **조건부 액세스** 탐색 항목입니다.

6.  검사 하려는 hello 정책을 클릭 합니다.

7.  Hello 설정 하 여 hello 정책을 사용 하지 않도록 **정책 사용** 너무 설정/해제**아니요** hello를 클릭 하 고 **저장** 단추입니다.

## <a name="problems-with-application-consent"></a>응용 프로그램 동의와 관련된 문제

Hello 적절 한 사용 권한을 승인 작업이 발생 하지 않았기 때문에 응용 프로그램 액세스를 차단할 수 있습니다. 응용 프로그램 동의 문제를 해결할 수 있는 몇 가지 방법은 다음과 같습니다.

-   [사용자 수준 동의 작업 수행](#perform-a-user-level-consent-operation)

-   [응용 프로그램에 대해 관리자 수준 동의 작업 수행](#perform-administrator-level-consent-operation-for-any-application)

-   [단일 테넌트 응용 프로그램에 대해 관리자 수준 동의 작업 수행](#perform-administrator-level-consent-for-a-single-tenant-application)

-   [다중 테넌트 응용 프로그램에 대해 관리자 수준 동의 작업 수행](#perform-administrator-level-consent-for-a-multi-tenant-application)

### <a name="perform-a-user-level-consent-operation"></a>사용자 수준 동의 작업 수행

-   모든 열린 ID 연결 사용이 가능한 응용 프로그램에 사용 권한을 요청 하는, toohello 응용 프로그램의 로그인 화면 탐색 hello 로그인 한 사용자에 대 한 사용자의 동의 수준 toohello 응용 프로그램을 수행 합니다.

-   원할 경우 toodo이 프로그래밍 방식으로 참조 [개별 사용자의 동의 요청](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#requesting-individual-user-consent)합니다.

### <a name="perform-administrator-level-consent-operation-for-any-application"></a>응용 프로그램에 대해 관리자 수준 동의 작업 수행

-   에 대 한 **hello V1 응용 프로그램 모델을 사용 하 여 개발 된 응용 프로그램에만**를 추가 하 여이 관리자 수준 동의 toooccur 강제로 수 "**? = 프롬프트 admin\_동의**" toohello 끝날은 응용 프로그램의 로그인 URL입니다.

-   에 대 한 **hello V2 응용 프로그램 모델을 사용 하 여 개발 하는 모든 응용 프로그램**, hello hello 지침에 따라이 관리자 권한으로 동의 toooccur를 적용할 수 있습니다 **디렉터리에서 hello 권한 요청 관리자** 섹션 [hello 관리자 동의 끝점을 사용 하 여](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint)합니다.

### <a name="perform-administrator-level-consent-for-a-single-tenant-application"></a>단일 테넌트 응용 프로그램에 대해 관리자 수준 동의 작업 수행

-   에 대 한 **단일 테 넌 트 응용 프로그램** (예: 개발 중인 하거나 조직에서 소유), 사용 권한을 요청 하는 수행할 수 있습니다는 **관리자 수준의 동의** 대신 모든 작업 전역 관리자로 로그인 하 고 hello 클릭 하 여 사용자 **권한을 부여** hello hello 위쪽에 단추 **응용 프로그램 레지스트리-&gt; 모든 응용 프로그램-&gt; -응용 프로그램을 선택 합니다. &gt; 필요한 권한** 블레이드입니다.

-   에 대 한 **hello V1 또는 V2 응용 프로그램 모델을 사용 하 여 개발 하는 모든 응용 프로그램**, hello hello 지침에 따라이 관리자 권한으로 동의 toooccur를 적용할 수 있습니다 **hello 사용 권한 요청을 디렉터리 관리자** 섹션 [hello 관리자 동의 끝점을 사용 하 여](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint)합니다.

### <a name="perform-administrator-level-consent-for-a-multi-tenant-application"></a>다중 테넌트 응용 프로그램에 대해 관리자 수준 동의 작업 수행

-   권한을 요청하는 **다중 테넌트 응용 프로그램**의 경우(예: 타사 또는 Microsoft에서 개발하는 응용 프로그램) **관리 수준 동의** 작업을 수행할 수 있습니다. 전역 관리자로 로그인 하 고 hello 클릭할 **권한을 부여** hello에 따라 단추 **엔터프라이즈 응용 프로그램-&gt; 모든 응용 프로그램-&gt; 앱-선택&gt; 사용 권한** 블레이드 (사용 가능한 빨리).

-   Hello hello 지침에 따라는 관리자 권한으로 동의 toooccur이도 강제 적용할 수 **hello 권한을 디렉터리 관리자의 요청** 섹션 [hello 관리자 동의 끝점를사용하여](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).

## <a name="next-steps"></a>다음 단계
[Hello 관리자 동의 끝점을 사용 하 여](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint)

