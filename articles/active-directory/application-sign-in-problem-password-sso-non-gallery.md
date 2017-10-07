---
title: "암호에 대해 구성 된 Azure AD 갤러리 응용 프로그램이 tooan 로그인 aaaProblems 단일 로그온 | Microsoft Docs"
description: "지침 tootroubleshoot 발급 tooAzure에 관련된 toosigning 암호 single sign on에 대해 구성 된 AD 갤러리 응용 프로그램을 제공 하는 문제 영역에 설명"
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
ms.openlocfilehash: f53ef4176db37dc6b1da2d61027155a6ba8f331e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooan-azure-ad-gallery-application-configured-for-password-single-sign-on"></a>Tooan 암호 single sign on에 대해 구성 된 Azure AD 갤러리 응용 프로그램에에서 로그인 하는 문제

액세스 패널 hello 활성화 있는 사용자가 회사 또는 학교 계정을 Azure Active Directory (Azure AD) tooview 및 시작 클라우드 기반 응용 프로그램에서 해당 관리자에 게 Azure AD는 웹 기반 포털이 부여 해 준에 대 한 액세스입니다. Azure AD 버전을 가진 사용자는 셀프 서비스 그룹 및 hello 액세스 패널을 통해 응용 프로그램 관리 기능 사용할 수도 있습니다. 액세스 패널 hello는 hello Azure 포털에서에서 분리 되 고 사용자가 toohave Azure 구독이 필요 하지 않습니다.

toouse 암호 기반 single 로그온 (SSO)에서 액세스 패널 액세스 패널 확장 hello hello hello 사용자 브라우저에 설치 되어야 합니다. 사용자가 암호 기반 SSO에 구성된 응용 프로그램을 선택할 때 이 확장이 자동으로 다운로드됩니다.

## <a name="meeting-browser-requirements-for-hello-access-panel"></a>액세스 패널 hello에 대 한 브라우저 요구 사항 충족

hello 액세스 패널을 지 원하는 JavaScript 브라우저 필요 하 고 CSS를 활성화 합니다. toouse 암호 기반 single 로그온 (SSO)에서 액세스 패널 액세스 패널 확장 hello hello hello 사용자 브라우저에 설치 되어야 합니다. 사용자가 암호 기반 SSO에 구성된 응용 프로그램을 선택할 때 이 확장이 자동으로 다운로드됩니다.

암호 기반 SSO에 대 한 hello 최종 사용자의 브라우저 될 수 있습니다.

-   Internet Explorer 8, 9, 10, 11 - Windows 7 이상

-   Chrome - Windows 7 이상 및 Mac OS X 이상

-   Firefox 26.0 이상 - Windows XP SP2 이상 및 Mac OS X 10.6 이상

>[!NOTE]
>hello 암호 기반 SSO 확장 브라우저 확장 될 지에 대해 지원 되는 경우 Windows 10에서에 지에 대해 사용할 수 있게 합니다.
>
>

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a>Tooinstall은 액세스 패널 브라우저 확장을 hello 하는 방법

아래의 hello 단계를 수행 하는 액세스 패널 브라우저 확장 tooinstall hello:

1.  열기 hello [액세스 패널](https://myapps.microsoft.com) hello 지원 되는 브라우저와로 로그인 중 하나에 **사용자** Azure AD에 있습니다.

2.  클릭는 **password SSO 응용 프로그램** hello 액세스 패널에에서 있습니다.

3.  Hello 프롬프트 묻는 tooinstall hello 소프트웨어에서 선택 **지금 설치**합니다.

4.  브라우저에 따라 toohello 방향이 지정 된 다운로드 링크 할 수 있습니다. **추가** hello 확장 tooyour 브라우저.

5.  브라우저를 요청 하면 선택 tooeither **사용** 또는 **허용** hello 확장 합니다.

6.  설치되면 브라우저 세션을 **다시 시작**합니다.

7.  Hello 액세스 패널에 로그인 하 고 참조 하면 **시작** password SSO 응용 프로그램

Hello 직접 링크 아래에서 Chrome 및 Firefox에 대 한 hello 확장을 다운로드할 수 있습니다.

-   [Chrome 액세스 패널 확장](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [Firefox 액세스 패널 확장](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="setting-up-a-group-policy-for-internet-explorer"></a>Internet Explorer에 대한 그룹 정책 설정

할 수 있도록 tooremotely 설치 hello 액세스 패널 확장 Internet Explorer에 대 한 사용자의 컴퓨터에서 그룹 정책을 설정할 수 있습니다.

hello 필수 구성 요소는 다음과 같습니다.

-   설정한 후 [Active Directory 도메인 서비스](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), 사용자의 컴퓨터 tooyour 도메인에 가입한 하 고 있습니다.

-   Hello "설정 편집" 권한이 tooedit hello 그룹 정책 개체 (GPO) 있어야 합니다. 기본적으로 hello 다음 보안 그룹의 멤버는이 권한이 있는: Domain Administrators, 엔터프라이즈 관리자 및 Group Policy Creator Owners 합니다. [자세히 알아봅니다](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).

Hello 자습서에 따라 [tooDeploy 그룹 정책을 사용 하 여 Internet Explorer에 대 한 액세스 패널 확장을 hello 하는 방법을](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-group-policy) tooconfigure hello 그룹 정책 하 고 toousers 배포 하는 방법에 대 한 단계별 지침에 대 한 합니다.

## <a name="troubleshoot-hello-access-panel-in-internet-explorer"></a>Internet Explorer에서 액세스 패널 hello 문제 해결

Hello에 따라 [문제 해결 hello Internet Explorer에 대 한 액세스 패널 확장이](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-Troubleshoot) IE hello 확장 구성에 액세스에 대 한 진단 도구 및 단계별 지침 안내 합니다.

## <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a>Tooconfigure 암호 로그온 갤러리가 아닌 응용 프로그램에 대 한 단일 하는 방법

tooconfigure hello Azure AD 갤러리에서 응용 프로그램 해야합니다.

-   [비갤러리 응용 프로그램 추가](#add-a-non-gallery-application)

-   [암호 single sign on에 대 한 hello 응용 프로그램 구성](#configure-the-application-for-password-single-sign-on)

-   [사용자가 toohello 응용 프로그램 할당](#assign-users-to-the-application)

### <a name="add-a-non-gallery-application"></a>비갤러리 응용 프로그램 추가

아래의 hello 단계를 수행 하는 tooadd hello Azure AD 갤러리에서에서 응용 프로그램:

1.  열기 hello [Azure 포털](https://portal.azure.com) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**

2.  열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.

3.  에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.

4.  클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.

5.  hello 클릭 **추가** hello hello 오른쪽 위 모서리에 있는 단추 **엔터프라이즈 응용 프로그램** 블레이드

6.  **비갤러리 응용 프로그램**을 클릭합니다.

7.  Hello에 응용 프로그램의 hello 이름을 입력 **이름** 텍스트 상자에 붙여넣습니다. **추가**를 선택합니다.

짧은 시간 후 수 toosee hello 응용 프로그램의 구성 블레이드에서 수 있습니다.

### <a name="configure-hello-application-for-password-single-sign-on"></a>암호 single sign on에 대 한 hello 응용 프로그램 구성

tooconfigure single sign on 응용 프로그램에 대 한 아래의 hello 단계를 수행 합니다.

1.  열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**

2.  열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.

3.  에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.

4.  클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.

5.  클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.

   * 여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**

6.  Hello 응용 프로그램 선택 tooconfigure single sign on

7.  Hello 응용 프로그램 로드 되 면 클릭 hello **Single sign on** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.

8.  선택 hello 모드 **암호 기반 로그온 합니다.**

9.  Hello 입력 **로그온 URL**합니다. 사용자가을 자신의 사용자 이름 및 암호 toosign 입력할 수 있는 hello URL입니다. Hello 로그인 필드 hello URL에 표시 되는지 확인 합니다.

10. Toohello 응용 프로그램 사용자를 할당 합니다.

11. Hello 사용자의 hello 행을 선택 하 고를 클릭 하 여 hello 사용자 대신 자격 증명도 제공할 수 또한 **업데이트 자격 증명** hello 사용자를 대신해 서 hello 사용자 이름 및 암호를 입력 합니다. 그렇지 않은 경우 사용자 수 증명된 tooenter hello 자격 증명 자체 종료 합니다.

### <a name="assign-users-toohello-application"></a>사용자가 toohello 응용 프로그램 할당

tooassign 아래의 hello 단계를 직접 수행 하는 하나 이상의 사용자가 tooan 응용 프로그램:

1.  열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**

2.  열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.

3.  에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.

4.  클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.

5.  클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.

   * 여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**

6.  원하는 사용자 toofrom hello 목록 tooassign hello 응용 프로그램을 선택 합니다.

7.  Hello 응용 프로그램 로드 되 면 클릭 **사용자 및 그룹** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.

8.  Hello 클릭 **추가** hello 위로 단추 **사용자 및 그룹** 목록 tooopen hello **할당 추가** 블레이드입니다.

9.  hello 클릭 **사용자 및 그룹** hello에서 선택기 **할당 추가** 블레이드입니다.

10. Hello 입력 **전체 이름** 또는 **전자 메일 주소** hello에 할당 하려는 hello 사용자의 **이름 또는 전자 메일 주소로 검색을 통해** 검색 상자입니다.

11. Hello 위로 마우스를 가져가고 **사용자** hello 목록 tooreveal에는 **확인란**합니다. Hello 확인란 다음 toohello 사용자의 프로필 사진 또는 로고 tooadd 사용자 toohello 클릭 **선택한** 목록입니다.

12. **선택 사항:** 너무 원하는 경우**둘 이상의 사용자를 추가**, 다른 유형 **전체 이름** 또는 **전자 메일 주소** hello에 **이름으로 검색 전자 메일 주소 또는** 상자에서 검색 하 고이 사용자 toohello hello 확인란 tooadd 클릭 **선택한** 목록입니다.

13. 사용자 선택을 완료 했으면 클릭 hello **선택** 단추 tooadd 해당 사용자 및 그룹 toobe toohello 목록이 toohello 응용 프로그램을 할당 합니다.

14. **선택 사항:** hello 클릭 **역할 선택** hello에 선택 기가 **할당 추가** 블레이드 tooselect 역할 tooassign toohello 사용자가 선택한 합니다.

15. Hello 클릭 **할당** 단추 tooassign hello 응용 프로그램 toohello 사용자를 선택 합니다.

짧은 기간 hello 사용자가 선택한 수 수 toolaunch에서 이러한 응용 프로그램 액세스 패널 hello 합니다.

## <a name="if-these-troubleshooting-steps-do-not-hello-resolve-hello-issue"></a>이러한 문제 해결 단계 hello 하지 않는 경우 hello 문제 해결

사용 가능한 경우 다음 정보는 hello로 지원 티켓을 엽니다.

-   상관 관계 오류 ID

-   UPN(사용자 전자 메일 주소)

-   TenantID

-   브라우저 종류

-   오류가 발생하는 동안 표준 시간대 및 시간/기간

-   Fiddler 추적

## <a name="next-steps"></a>다음 단계
[응용 프로그램 프록시 single sign on tooyour 앱을 제공 합니다.](active-directory-application-proxy-sso-using-kcd.md)

