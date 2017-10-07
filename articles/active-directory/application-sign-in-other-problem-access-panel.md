---
title: "aaaProblems hello 액세스 패널에서 tooan 응용 프로그램에 서명 | Microsoft Docs"
description: "응용 프로그램에 액세스 하는 tootroubleshoot 문제 myapps.microsoft.com에서 Microsoft Azure AD 액세스 패널 hello 하는 방법"
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
ms.openlocfilehash: 346c4da06416bb9b330bdd5b1201253af19ba58b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooan-application-from-hello-access-panel"></a>Hello 액세스 패널에서 tooan 응용 프로그램에 로그인 하는 문제

hello 액세스 패널은 작업으로는 사용할 수 있는 웹 기반 포털 또는 학교 계정을 Azure Active Directory (Azure AD) tooview 및 시작 클라우드 기반 응용 프로그램에서 해당 hello Azure AD 관리자가 부여 해 준에 대 한 액세스. 

이러한 응용 프로그램 hello Azure AD 포털에서 hello 사용자를 대신 하 여 구성 됩니다. hello 응용 프로그램을 올바르게 구성 되어야 합니다. 및 할당 된 toohello 사용자 또는 그룹 hello 사용자가 hello 액세스 패널에에서 toosee hello 응용 프로그램의 구성원입니다.

사용자 표시 될 수는 앱의 hello 유형 hello 다음 범주에에서 속합니다.

-   Office 365 응용 프로그램

-   페더레이션 기반 SSO로 구성된 Microsoft 및 타사 응용 프로그램

-   암호 기반 SSO 응용 프로그램

-   기존 SSO 솔루션을 사용한 응용 프로그램

## <a name="general-issues-toocheck-first"></a>일반 toocheck를 먼저 문제

-   사용 하 여 있는지 확인 한 **브라우저** hello hello 액세스 패널에 대 한 최소 요구 사항을 충족 하 합니다.

-   Hello 사용자의 브라우저 hello 응용 프로그램 tooits의 hello URL이 추가 되었는지 확인 **신뢰할 수 있는 사이트**합니다.

-   Toocheck hello 응용 프로그램 인지 확인 **구성** 올바르게 합니다.

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

## <a name="how-tooconfigure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a>Single sign on Azure AD 갤러리 응용 프로그램에 대 한 tooconfigure 페더레이션 하는 방법

Enterprise Single Sign-on 기능을 사용 하도록 설정 하는 hello Azure AD 갤러리에 있는 모든 응용 프로그램에는 단계별 자습서를 사용할 수 있습니다. Hello에 액세스할 수 있습니다 [방법에 대 한 자습서 목록 toointegrate SaaS 앱 Azure Active Directory와](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) 세부 단계별 지침에 대 한 합니다.

tooconfigure hello Azure AD 갤러리에서 응용 프로그램 해야합니다.

-   [Hello Azure AD 갤러리에서 응용 프로그램 추가](#add-an-application)

-   [Azure ad (로그온 URL, 식별자, 회신 URL) hello 응용 프로그램의 메타 데이터 값을 구성 합니다.](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [사용자의 Id를 선택 하 고 사용자 특성 전송 toobe toohello 응용 프로그램 추가](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [Azure AD 메타데이터 및 인증서 검색](#download-the-azure-ad-metadata-or-certificate)

-   [Hello 응용 프로그램 (로그온 URL, 발급자, 로그 아웃 URL 및 인증서)에 Azure AD 메타 데이터 값을 구성 합니다.](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [사용자가 toohello 응용 프로그램 할당](#assign-users-to-the-application)

### <a name="add-an-application-from-hello-azure-ad-gallery"></a>Hello Azure AD 갤러리에서 응용 프로그램 추가

아래의 hello 단계를 수행 하는 tooadd hello Azure AD 갤러리에서에서 응용 프로그램:

1.  열기 hello [Azure 포털](https://portal.azure.com) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**

2.  열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.

3.  에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.

4.  클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.

5.  hello 클릭 **추가** hello hello 오른쪽 위 모서리에 있는 단추 **엔터프라이즈 응용 프로그램** 블레이드

6.  Hello에 **이름을 입력** hello에서 텍스트 상자에 붙여넣습니다 **hello 갤러리에서 추가** 섹션, hello 응용 프로그램의 형식 hello 이름입니다.

7.  Single sign on tooconfigure 원하는 hello 응용 프로그램을 선택 합니다.

8.  Hello 응용 프로그램을 추가 하기 전에 hello에서 이름을 변경할 수 **이름** 텍스트 상자에 붙여넣습니다.

9.  클릭 **추가** tooadd hello 응용 프로그램 단추입니다.

짧은 시간 후 수 toosee hello 응용 프로그램의 구성 블레이드에서 수 있습니다.

### <a name="configure-single-sign-on-for-an-application-from-hello-azure-ad-gallery"></a>Single sign on hello Azure AD 갤러리에서 응용 프로그램에 대 한 구성

tooconfigure single sign on 응용 프로그램에 대 한 아래의 hello 단계를 수행 합니다.

1.  <span id="_Hlk477187909" class="anchor"><span id="_Hlk477001983" class="anchor"></span></span>열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**

2.  열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.

3.  에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.

4.  클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.

5.  클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.

  * 여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**

6.  Tooconfigure single sign on 원하는 hello 응용 프로그램을 선택 합니다.

7.  Hello 응용 프로그램 로드 되 면 클릭 hello **Single sign on** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.

8.  선택 **SAML 기반 로그온** hello에서 **모드** 드롭다운입니다.

9.  필요한 hello 값을 입력 **도메인 및 Url입니다.** Hello 응용 프로그램 공급 업체에서 이러한 값을 구해야 합니다.

   1. SP에서 시작한 SSO와 tooconfigure hello 응용 프로그램 hello 로그인 URL에 필요한 값입니다. 일부 응용 프로그램에 대 한 hello 식별자도 필요한 값입니다.

   2. IdP에서 시작한 SSO, hello 필수 값입니다. 회신 URL로 tooconfigure hello 응용 프로그램입니다. 일부 응용 프로그램에 대 한 hello 식별자도 필요한 값입니다.

10. **선택 사항:** 클릭 **고급 URL 설정 표시** toosee hello 선택적 값입니다.

11. Hello에 **사용자 특성**, 선택 hello에 있는 사용자에 대 한 고유 식별자를 hello **사용자 식별자** 드롭다운입니다.

12. **선택 사항:** 클릭 **보기 및 다른 모든 사용자 특성 편집** tooedit hello 사용자가 로그인 할 때 hello SAML 토큰에서 보낸 toobe toohello 응용 프로그램 특성입니다.

   tooadd 특성:

   1. **특성 추가**를 클릭합니다. Hello 입력 **이름** 및 hello 선택 hello **값** hello 드롭다운에서 합니다.

   2. **저장**을 클릭합니다. Hello 테이블에 새 특성을 hello 표시 됩니다.

13. 클릭 **구성 &lt;응용 프로그램 이름&gt;**  방법은 tooaccess 설명서 tooconfigure single sign on hello 응용 프로그램에 있습니다. 또한 hello 메타 데이터 Url 및 hello 응용 프로그램과 함께 필요한 인증서 toosetup SSO에 있습니다.

14. 클릭 **저장** toosave hello 구성 합니다.

15. Toohello 응용 프로그램 사용자를 할당 합니다.

### <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a>사용자의 Id를 선택 하 고 사용자 특성 전송 toobe toohello 응용 프로그램 추가

tooselect hello 사용자 식별자 또는 사용자 특성 추가, 아래의 hello 단계를 수행:

1.  열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**

2.  열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.

3.  에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.

4.  클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.

5.  클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.

  * Hello를 사용 하 여 원하는 여기 tooshow hello 응용 프로그램을 표시 되지 않으면 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**

6.  Single sign on 구성한 hello 응용 프로그램을 선택 합니다.

7.  Hello 응용 프로그램 로드 되 면 클릭 hello **Single sign on** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.

8.  Hello에서 **사용자 특성** 섹션에서 사용자 hello에 대 한 고유 식별자를 hello **사용자 식별자** 드롭다운입니다. hello 선택된 된 옵션 두어야 hello 응용 프로그램 tooauthenticate hello 사용자에서 toomatch hello 예상 값.

    >[!NOTE]
    >Hello NameID 특성 (사용자 식별자)에 대 한 azure AD 선택 hello 형식 선택한 hello 값에 따라 또는 hello SAML AuthRequest hello에 hello 응용 프로그램에서 요청한 형식입니다. 자세한 내용은 방문 hello 문서 [Single Sign On SAML 프로토콜](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) hello에서 NameIDPolicy 섹션.
    >
    >

9.  tooadd 사용자 특성을 클릭 하 여 **보기 및 다른 모든 사용자 특성을 편집** tooedit hello 사용자가 로그인 할 때 hello SAML 토큰에서 보낸 toobe toohello 응용 프로그램 특성입니다.

   tooadd 특성:

   1. **특성 추가**를 클릭합니다. Hello 입력 **이름** 및 hello 선택 hello **값** hello 드롭다운에서 합니다.

   2. **저장**을 클릭합니다. Hello 테이블에 새 특성을 hello 표시 됩니다.

### <a name="download-hello-azure-ad-metadata-or-certificate"></a>Hello Azure AD 메타 데이터 또는 인증서를 다운로드 합니다.

toodownload hello에 대 한 응용 프로그램 메타 데이터 또는 Azure AD에서 인증서를 다음 hello 단계를 따라 합니다.

1.  열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**

2.  열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.

3.  에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.

4.  클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.

5.  클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.

  * 여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**

6.  Single sign on 구성한 hello 응용 프로그램을 선택 합니다.

7.  Hello 응용 프로그램 로드 되 면 클릭 hello **Single sign on** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.

8.  너무 이동**SAML 서명 인증서** 섹션에서 다음 클릭 **다운로드** 열 값입니다. 어떤 hello 응용 프로그램에 single sign-on 구성 필요한 경우에 따라 메타 데이터 XML hello 또는 인증서를 환영 hello 옵션 toodownload를 볼 수 있습니다.

    Azure AD URL tooget hello 메타 데이터를 제공 하지 않습니다. hello 메타 데이터를 XML 파일로 검색할 수 있습니다.

## <a name="how-tooconfigure-federated-single-sign-on-for-a-non-gallery-application"></a>Single sign on 갤러리가 아닌 응용 프로그램에 대 한 tooconfigure 페더레이션 하는 방법

toohave Azure AD premium이 필요 tooconfigure 갤러리가 아닌 응용 프로그램 및 hello 응용 프로그램이 SAML 2.0을 지원 합니다. Azure AD 버전에 대한 자세한 내용은 [Azure AD 가격 책정](https://azure.microsoft.com/pricing/details/active-directory/)에서 확인할 수 있습니다.

-   [Azure ad (로그온 URL, 식별자, 회신 URL) hello 응용 프로그램의 메타 데이터 값을 구성 합니다.](#configuring-single-sign-on)

-   [사용자의 Id를 선택 하 고 사용자 특성 전송 toobe toohello 응용 프로그램 추가](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [Azure AD 메타데이터 및 인증서 검색](#download-the-azure-ad-metadata-or-certificate)

-   [Hello 응용 프로그램 (로그온 URL, 발급자, 로그 아웃 URL 및 인증서)에 Azure AD 메타 데이터 값을 구성 합니다.](#configuring-single-sign-on)

### <a name="configure-hello-applications-metadata-values-in-azure-ad-sign-on-url-identifier-reply-url"></a>Azure ad (로그온 URL, 식별자, 회신 URL) hello 응용 프로그램의 메타 데이터 값을 구성 합니다.

tooconfigure single sign on hello Azure AD 갤러리에 없는 응용 프로그램에 대 한 아래의 hello 단계를 수행 합니다.

1.  열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**

2.  열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.

3.  에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.

4.  클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.

5.  hello 클릭 **추가** hello hello 오른쪽 위 모서리에 있는 단추 **엔터프라이즈 응용 프로그램** 블레이드

6.  클릭 **비 갤러리 응용 프로그램** hello에 **위해 자신의 앱 추가** 섹션

7.  Hello에 hello 응용 프로그램의 hello 이름을 입력 **이름** 텍스트 상자에 붙여넣습니다.

8.  클릭 **추가** tooadd hello 응용 프로그램 단추입니다.

9.  Hello 응용 프로그램 로드 되 면 클릭 hello **Single sign on** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.

10. 선택 **SAML 기반 로그온** hello에 **모드** 드롭다운

11. 필요한 hello 값을 입력 **도메인 및 Url입니다.** Hello 응용 프로그램 공급 업체에서 이러한 값을 구해야 합니다.

  1. IdP에서 시작한 SSO와 tooconfigure hello 응용 프로그램 회신 URL hello 및 hello 식별자를 입력 합니다.

  2. **선택 사항:** SP에서 시작한 SSO와 tooconfigure hello 응용 프로그램 hello 로그인 URL에 필요한 값입니다.

12. Hello에 **사용자 특성**, 선택 hello에 있는 사용자에 대 한 고유 식별자를 hello **사용자 식별자** 드롭다운입니다.

13. **선택 사항:** 클릭 **보기 및 다른 모든 사용자 특성 편집** tooedit hello 사용자가 로그인 할 때 hello SAML 토큰에서 보낸 toobe toohello 응용 프로그램 특성입니다.

   tooadd 특성:

   1. **특성 추가**를 클릭합니다. Hello 입력 **이름** 및 hello 선택 hello **값** hello 드롭다운에서 합니다.

   2. **저장**을 클릭합니다. Hello 테이블에 새 특성을 hello 표시 됩니다.

14. 클릭 **구성 &lt;응용 프로그램 이름&gt;**  방법은 tooaccess 설명서 tooconfigure single sign on hello 응용 프로그램에 있습니다. 또한 Azure AD Url 및 hello 응용 프로그램에 필요한 인증서에 있습니다.

### <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a>사용자의 Id를 선택 하 고 사용자 특성 전송 toobe toohello 응용 프로그램 추가

tooselect hello 사용자 식별자 또는 사용자 특성 추가, 아래의 hello 단계를 수행:

1.  열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**

2.  열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.

3.  에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.

4.  클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.

5.  클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.

  * 여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**

6.  Single sign on 구성한 hello 응용 프로그램을 선택 합니다.

7.  Hello 응용 프로그램 로드 되 면 클릭 hello **Single sign on** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.

8.  Hello에서 **사용자 특성** 섹션에서 사용자 hello에 대 한 고유 식별자를 hello **사용자 식별자** 드롭다운입니다. hello 선택된 된 옵션 두어야 hello 응용 프로그램 tooauthenticate hello 사용자에서 toomatch hello 예상 값.

   >[!NOTE]
   >Hello NameID 특성 (사용자 식별자)에 대 한 azure AD 선택 hello 형식 선택한 hello 값에 따라 또는 hello SAML AuthRequest hello에 hello 응용 프로그램에서 요청한 형식입니다. 자세한 내용은 방문 hello 문서 [Single Sign On SAML 프로토콜](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) hello에서 NameIDPolicy 섹션.
   >
   >

9.  tooadd 사용자 특성을 클릭 하 여 **보기 및 다른 모든 사용자 특성을 편집** tooedit hello 사용자가 로그인 할 때 hello SAML 토큰에서 보낸 toobe toohello 응용 프로그램 특성입니다.

   tooadd 특성:

   1. **특성 추가**를 클릭합니다. Hello 입력 **이름** 및 hello 선택 hello **값** hello 드롭다운에서 합니다.

   2. **저장**을 클릭합니다. Hello 테이블에 새 특성을 hello 표시 됩니다.

### <a name="download-hello-azure-ad-metadata-or-certificate"></a>Hello Azure AD 메타 데이터 또는 인증서를 다운로드 합니다.

toodownload hello에 대 한 응용 프로그램 메타 데이터 또는 Azure AD에서 인증서를 다음 hello 단계를 따라 합니다.

1.  열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**

2.  열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.

3.  에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.

4.  클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.

5.  클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.

   * 여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**

6.  Single sign on 구성한 hello 응용 프로그램을 선택 합니다.

7.  Hello 응용 프로그램 로드 되 면 클릭 hello **Single sign on** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.

8.  너무 이동**SAML 서명 인증서** 섹션에서 다음 클릭 **다운로드** 열 값입니다. 어떤 hello 응용 프로그램에 single sign-on 구성 필요한 경우에 따라 메타 데이터 XML hello 또는 인증서를 환영 hello 옵션 toodownload를 볼 수 있습니다.

    Azure AD URL tooget hello 메타 데이터를 제공 하지 않습니다. hello 메타 데이터를 XML 파일로 검색할 수 있습니다.

## <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a>Azure AD 갤러리 응용 프로그램에 대 한 sign-on tooconfigure 암호 single 방법

tooconfigure hello Azure AD 갤러리에서 응용 프로그램 해야합니다.

-   [Hello Azure AD 갤러리에서 응용 프로그램 추가](#add-an-application)

-   [암호 single sign on에 대 한 hello 응용 프로그램 구성](#configure-the-application)

### <a name="add-an-application-from-hello-azure-ad-gallery"></a>Hello Azure AD 갤러리에서 응용 프로그램 추가

아래의 hello 단계를 수행 하는 tooadd hello Azure AD 갤러리에서에서 응용 프로그램:

1.  열기 hello [Azure 포털](https://portal.azure.com) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**

2.  열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.

3.  에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.

4.  클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.

5.  hello 클릭 **추가** hello hello 오른쪽 위 모서리에 있는 단추 **엔터프라이즈 응용 프로그램** 블레이드

6.  Hello에 **이름을 입력** hello에서 textbox **hello 갤러리에서 추가** 섹션, hello 응용 프로그램의 형식 hello 이름

7.  Hello 응용 프로그램 선택 tooconfigure single sign on

8.  Hello 응용 프로그램을 추가 하기 전에 hello에서 이름을 변경할 수 **이름** 텍스트 상자에 붙여넣습니다.

9.  클릭 **추가** tooadd hello 응용 프로그램 단추입니다.

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

9.  Toohello 응용 프로그램 사용자를 할당 합니다.

10. Hello 사용자의 hello 행을 선택 하 고를 클릭 하 여 hello 사용자 대신 자격 증명도 제공할 수 또한 **업데이트 자격 증명** hello 사용자를 대신해 서 hello 사용자 이름 및 암호를 입력 합니다. 그렇지 않은 경우 사용자 수 증명된 tooenter hello 자격 증명 자체 종료 합니다.

## <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a>Tooconfigure 암호 로그온 갤러리가 아닌 응용 프로그램에 대 한 단일 하는 방법

tooconfigure hello Azure AD 갤러리에서 응용 프로그램 해야합니다.

-   [비갤러리 응용 프로그램 추가](#add-a-non-gallery-application)

-   [암호 single sign on에 대 한 hello 응용 프로그램 구성](#configure-the-application-for-password-single-sign-on)

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

6.  Tooconfigure single sign on 원하는 hello 응용 프로그램을 선택 합니다.

7.  Hello 응용 프로그램 로드 되 면 클릭 hello **Single sign on** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.

8.  선택 hello 모드 **암호 기반 로그온 합니다.**

9.  Hello 입력 **로그온 URL**합니다. 사용자가을 자신의 사용자 이름 및 암호 toosign 입력할 수 있는 hello URL입니다. Hello 로그인 필드 hello URL에 표시 되는지 확인 합니다.

10. Toohello 응용 프로그램 사용자를 할당 합니다.

11. Hello 사용자의 hello 행을 선택 하 고를 클릭 하 여 hello 사용자 대신 자격 증명도 제공할 수 또한 **업데이트 자격 증명** hello 사용자를 대신해 서 hello 사용자 이름 및 암호를 입력 합니다. 그렇지 않은 경우 사용자 수 증명된 tooenter hello 자격 증명 자체 종료 합니다.

## <a name="how-tooassign-a-user-tooan-application-directly"></a>어떻게 tooassign 사용자 tooan 응용 프로그램을 직접

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

