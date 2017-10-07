---
title: "사용자 지정: Azure AD SSPR | Microsoft Docs"
description: "Azure AD 셀프 서비스 암호 재설정에 대한 사용자 지정 옵션"
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 4762fffef040f9b409355f9ee0e8cc593e3eea0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-azure-ad-functionality-for-self-service-password-reset"></a>셀프 서비스 암호 재설정을 위한 Azure AD 기능 사용자 지정

IT 전문가 toodeploy 셀프 서비스 암호 재설정을 찾고 사용자 지정할 수 hello 경험 toomatch 사용자.

## <a name="customize-hello-contact-your-administrator-link"></a>Hello 연락처 관리자 링크를 사용자 지정

경우에 SSPR 사용 되는 사용자 여전히는 "관리자에 게 문의" 링크 hello 암호 재설정 포털을 사용 합니다.  이 링크를 클릭 하면 hello 사용자의 암호 변경에 대 한 도움말을 요청 하는 관리자에 게 문의 전자 메일로 보냅니다. 이 전자 메일은 다음 순서에 따라 hello에서 받는 사람 toohello를 전송 되었습니다.

1. 경우 hello **암호 관리자** 역할이 할당 될,이 역할이 있는 관리자는 알림을
2. 하는 경우 암호 관리자 할당 되었는지, 다음 hello로 관리자 **사용자 관리자** 역할 알림이 표시 됩니다
3. 경우 모두 hello 앞의 역할 할당, 다음 **전역 관리자** 알림이 표시 됩니다

어떠한 경우에도 최대 100명의 받는 사람에게 알림이 제공됩니다.

hello 다른 관리자 역할 및 tooassign 해당 참조 문서 hello 하는 방법에 대 한 자세한 내용을 toofind [Azure Active Directory에서 관리자 역할 할당](active-directory-assign-admin-roles.md)

### <a name="disable-contact-your-administrator-emails"></a>관리자에게 문의 전자 메일 사용 안 함

조직에서 관리자 암호에 대 한 알림을 다시 설정 요청을 원치 않을 경우 hello 다음 구성을 사용할 수 있습니다.

* 모든 최종 사용자에게 셀프 서비스 암호 재설정 사용 이 옵션은 **암호 재설정 > 속성** 아래에 있습니다.
    * 싶지 않은 사용자가 tooreset 자신의 암호를 하는 경우 범위를 지정 하면 액세스 tooan 빈 그룹 **이 옵션은 좋지 않습니다**합니다.
* 웹 URL 또는 mailto hello 기술 지원팀 링크 tooprovide 사용자 지정: 사용자가 tooget 지원을 사용할 수 있는 주소입니다. 이 옵션은 **암호 재설정 > 사용자 지정 > 사용자 지정 기술 지원 팀 메일 또는 URL** 아래에 있습니다.

## <a name="customize-adfs-sign-in-page-for-sspr"></a>SSPR에 대한 ADFS 로그인 페이지 사용자 지정

Ad FS 관리자는 링크 tootheir 로그인 페이지의 hello 문서 hello 지침을 사용 하 여 추가할 수 있습니다 [로그인 페이지 설명을 추가](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/add-sign-in-page-description)합니다.

ADFS 서버에서 다음에 나오는 hello 명령을 사용 하 여 사용자가 tooenter hello 셀프 서비스 암호 재설정 워크플로 직접 허용 링크 toohello ADFS 로그인 페이지를 추가 합니다.

``` Set-ADFSGlobalWebContent -SigninPageDescriptionText "<p><A href=’https://passwordreset.microsoftonline.com’>Can’t access your account?</A></p>" ```

## <a name="customize-hello-sign-in-and-access-panel-look-and-feel"></a>Hello 로그인 및 액세스 패널 모양 및 느낌을 사용자 지정

Hello 로그인 페이지에 액세스 하는 사용자가 회사 브랜딩을 hello 로그인 페이지 이미지 toofit 함께 나타나는 hello 로고를 사용자 지정할 수 있습니다.

이러한 그래픽 hello 상황 뒤에 나와 있습니다.

* 사용자가 사용자 이름을 입력한 후
* 사용자가 사용자 지정된 URL에 액세스
    * Hello 전달 하 여 "whr" 매개 변수 toohello 암호 재설정 페이지 "https://login.microsoftonline.com/?whr=contoso.com"와 같은
    * Hello "username"을 전달 하 여 매개 변수 toohello 암호 재설정 페이지에 같은 "https://login.microsoftonline.com/?username=admin@contoso.com"

### <a name="graphics-details"></a>그래픽 정보

hello 다음 toochange hello hello 로그인 페이지의 시각적 특성을 사용 하면 설정과 확인할 수 있습니다 **Azure Active Directory**, **회사 브랜딩**, **회사 편집 브랜딩**

* 로그인 페이지 이미지는 500KB 이하의 1420x1200픽셀인 JPG 또는 PNG 파일이어야 합니다. Toobe 약 200KB 최상의 결과 권장 합니다.
* 로그인 페이지 배경색 대기 시간이 긴 연결에서 사용 되 고 hello RGB 16 진수 형식 이어야 합니다.
* 배너 이미지는 10KB 이하의 60x280픽셀인 JPG 또는 PNG 파일이어야 합니다.
* 정사각형 로고(일반 및 어두운 테마)는 10KB 이하의 240x240(크기 조정 가능)픽셀인 JPG 또는 PNG 파일입니다.

### <a name="sign-in-text-options"></a>로그인 텍스트 옵션

다음 설정을 hello를 사용 하면 tooadd 텍스트 toohello 로그인 페이지 관련 tooyour 조직 있습니다. 이러한 설정은 **Azure Active Directory**, **회사 브랜딩**, **회사 브랜딩 편집**에서 찾을 수 있습니다.

* **사용자 이름 힌트** 대체 hello의 예제 텍스트 someone@example.com 내부 및 외부 사용자를 지 원하는 경우 사용자에 게 보다 적합 한 형태로와 toobe 왼쪽된 기본에 권장
* **로그인 페이지 텍스트**는 최대 256자입니다. 이 텍스트 온라인 및 hello Windows 10에서 Azure AD 조인 환경에 사용자가 로그인 아무 곳 이나 표시 됩니다. 사용 약관, 지침 및 사용자에 대한 팁에서 이 텍스트를 사용합니다. **누구든지 로그인 페이지를 볼 수 있으므로 여기에서 중요 정보를 제공하지 않도록 합니다.**

### <a name="keep-me-signed-in-disabled"></a>로그인 사용 안 함

hello 옵션 "로그인 유지 사용 안 함" 브라우저 창을 닫았다가 때 로그인 하는 사용자가 tooremain을 수 있습니다. 이 옵션은 세션 수명에 영향을 주지 않습니다. 이 설정은 **Azure Active Directory > 회사 브랜딩 > 회사 브랜딩 편집** 아래에 있습니다.

SharePoint Online 및 Office 2010의 일부 기능 사용자가 수 toocheck이이 상자에는 종속성이 있는 합니다. 이 옵션을 숨기면 사용자에게 추가 및 예기치 않은 로그인 프롬프트가 표시될 수 있습니다.

### <a name="directory-name"></a>디렉터리 이름

아래에 hello 이름 특성을 변경할 수 있습니다 **Azure Active Directory > 속성** tooshow 친숙 한 조직 이름 hello 포털에서 확인 했 고 자동으로 통신 합니다. 이 옵션은 다음에 나오는 hello 형태로 자동화 된 전자 메일의 hello 형태로 가장 눈에 띄는

* "CONTOSO 데모를 대신하는 Microsoft" 전자 메일의 친숙한 이름
* "CONTOSO 데모 계정 전자 메일 확인 코드" 전자 메일의 제목 줄

## <a name="next-steps"></a>다음 단계

링크를 따라 hello Azure AD를 사용 하 여 다시 설정 하는 암호에 대 한 추가 정보를 제공 합니다.

* [**빠른 시작**](active-directory-passwords-getting-started.md) - Azure AD 셀프 서비스 암호 관리를 사용하여 운영 시작 
* [**라이선스**](active-directory-passwords-licensing.md) - Azure AD 라이선스 구성
* [**데이터** ](active-directory-passwords-data.md) -hello 필요한 데이터를 이해 하 고 암호 관리에 대 한 사용 방법
* [**롤아웃** ](active-directory-passwords-best-practices.md) -계획 및 배포 ´ ֿ ´ hello 지침을 사용 하 여 SSPR tooyour 사용자
* [**정책**](active-directory-passwords-policy.md) - Azure AD 암호 정책을 이해하고 설정
* [**비밀번호 쓰기 저장**](active-directory-passwords-writeback.md) - 비밀번호 쓰기 저장이 온-프레미스 디렉터리와 함께 작동 하는 원리
* [**보고**](active-directory-passwords-reporting.md) - 사용자가 SSPR 기능에 액세스하는 조건, 시간 및 위치 탐색
* [**기술 심층 분석** ](active-directory-passwords-how-it-works.md) -이동 hello 커튼 toounderstand 뒤 작동 방법
* [**질문과 대답**](active-directory-passwords-faq.md) - 어떤 방식으로? 그 이유는 무엇을? 어디서? 누가? 언제? -Tooask 항상 필요한 tooquestions 답변
* [**문제를 해결** ](active-directory-passwords-troubleshoot.md) -SSPR으로 보면 tooresolve 공통을 발급 하는 방법에 대해 알아봅니다

