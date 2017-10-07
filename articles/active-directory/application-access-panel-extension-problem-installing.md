---
title: "hello 응용 프로그램 액세스 패널 브라우저 확장을 설치 하는 aaaProblem | Microsoft Docs"
description: "일반적인 오류 toofix hello 액세스 패널 브라우저 확장을 설치할 때 발생 하는 방법"
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
ms.reviewer: japere
ms.openlocfilehash: 5f750d12c5f9b405ec4f81596d5cc5e0a48f9a62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="problem-installing-hello-application-access-panel-browser-extension"></a>Hello 응용 프로그램 액세스 패널 브라우저 확장을 설치 하는 문제

액세스 패널 hello 활성화 있는 사용자가 회사 또는 학교 계정을 Azure Active Directory (Azure AD) tooview 및 시작 클라우드 기반 응용 프로그램에서 해당 관리자에 게 Azure AD는 웹 기반 포털이 부여 해 준에 대 한 액세스입니다. Azure AD 버전을 가진 사용자는 셀프 서비스 그룹 및 hello 액세스 패널을 통해 응용 프로그램 관리 기능 사용할 수도 있습니다. 액세스 패널 hello는 hello Azure 포털에서에서 분리 되 고 사용자가 toohave Azure 구독이 필요 하지 않습니다.

toouse 암호 기반 single 로그온 (SSO)에서 액세스 패널 액세스 패널 확장 hello hello hello 사용자 브라우저에 설치 되어야 합니다. 사용자가 암호 기반 SSO에 구성된 응용 프로그램을 선택할 때 이 확장이 자동으로 다운로드됩니다.

## <a name="meeting-browser-requirements-for-hello-access-panel"></a>액세스 패널 hello에 대 한 브라우저 요구 사항 충족

hello 액세스 패널을 지 원하는 JavaScript 브라우저 필요 하 고 CSS를 활성화 합니다. toouse 암호 기반 single 로그온 (SSO)에서 액세스 패널 액세스 패널 확장 hello hello hello 사용자 브라우저에 설치 되어야 합니다. 사용자가 암호 기반 SSO에 구성된 응용 프로그램을 선택할 때 이 확장이 자동으로 다운로드됩니다.

암호 기반 SSO에 대 한 hello 최종 사용자의 브라우저 될 수 있습니다.

-   Internet Explorer 8, 9, 10, 11 - Windows 7 이상

-   Windows 10 Anniversary Edition 이상 Edge 

-   Chrome - Windows 7 이상 및 Mac OS X 이상

-   Firefox 26.0 이상 - Windows XP SP2 이상 및 Mac OS X 10.6 이상

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a>Tooinstall은 액세스 패널 브라우저 확장을 hello 하는 방법

아래의 hello 단계를 수행 하는 액세스 패널 브라우저 확장 tooinstall hello:

1.  열기 hello [액세스 패널](https://myapps.microsoft.com) hello 지원 되는 브라우저와로 로그인 중 하나에 **사용자** Azure AD에 있습니다.

2.  클릭는 **password SSO 응용 프로그램** hello 액세스 패널에에서 있습니다.

3.  Hello 프롬프트 묻는 tooinstall hello 소프트웨어에서 선택 **지금 설치**합니다.

4.  브라우저에 따라 toohello 방향이 지정 된 다운로드 링크 할 수 있습니다. **추가** hello 확장 tooyour 브라우저.

5.  브라우저를 요청 하면 선택 tooeither **사용** 또는 **허용** hello 확장 합니다.

6.  설치되면 브라우저 세션을 **다시 시작**합니다.

7.  Hello 액세스 패널에 로그인 하 고 참조 하면 **시작** password SSO 응용 프로그램

Hello 직접 링크 아래에서 Edge 및 Chrome에 대 한 hello 확장을 다운로드할 수 있습니다.

-   [Chrome 액세스 패널 확장](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [Edge 액세스 패널 확장](https://www.microsoft.com/store/apps/9pc9sckkzk84) 

## <a name="setting-up-a-group-policy-for-internet-explorer"></a>Internet Explorer에 대한 그룹 정책 설정

할 수 있도록 tooremotely 설치 hello 액세스 패널 확장 Internet Explorer에 대 한 사용자의 컴퓨터에서 그룹 정책을 설정할 수 있습니다.

hello 필수 구성 요소는 다음과 같습니다.

-   설정한 후 [Active Directory 도메인 서비스](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), 사용자의 컴퓨터 tooyour 도메인에 가입한 하 고 있습니다.

-   Hello "설정 편집" 권한이 tooedit hello 그룹 정책 개체 (GPO) 있어야 합니다. 기본적으로 hello 다음 보안 그룹의 멤버는이 권한이 있는: Domain Administrators, 엔터프라이즈 관리자 및 Group Policy Creator Owners 합니다. [자세히 알아봅니다](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).

Hello 자습서에 따라 [tooDeploy 그룹 정책을 사용 하 여 Internet Explorer에 대 한 액세스 패널 확장을 hello 하는 방법을](active-directory-saas-ie-group-policy.md) tooconfigure hello 그룹 정책 하 고 toousers 배포 하는 방법에 대 한 단계별 지침에 대 한 합니다.

## <a name="troubleshoot-hello-access-panel-in-internet-explorer"></a>Internet Explorer에서 액세스 패널 hello 문제 해결

Hello에 따라 [문제 해결 hello Internet Explorer에 대 한 액세스 패널 확장이](active-directory-saas-ie-troubleshooting.md) IE hello 확장 구성에 액세스에 대 한 진단 도구 및 단계별 지침 안내 합니다.

## <a name="if-these-troubleshooting-steps-do-not-resolve-hello-issue"></a>이러한 문제 해결 단계 hello 문제가 해결 되지 않는 경우

사용 가능한 경우 다음 정보는 hello로 지원 티켓을 엽니다.

-   상관 관계 오류 ID

-   UPN(사용자 전자 메일 주소)

-   TenantID

-   브라우저 종류

-   오류가 발생하는 동안 표준 시간대 및 시간/기간

-   Fiddler 추적

## <a name="next-steps"></a>다음 단계
[Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)
