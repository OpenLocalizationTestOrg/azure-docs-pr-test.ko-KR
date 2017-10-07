---
title: "aaaHow toodetermine 어떤 single sign-on 메서드 toouse | Microsoft Docs"
description: "Hello single sign on 모드 Azure AD에서 지 원하는 이해 및 방법에 대 한 하나의 toochoose 어떤 응용 프로그램 hello toopick에 관심이 있습니다."
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
ms.openlocfilehash: 64f0bc1dc8281d1ab8222fd50eaceaf710704886
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodetermine-what-single-sign-on-method-toouse"></a>어떻게 toodetermine 어떤 single sign-on toouse 메서드

이 문서가 도움이 toounderstand hello single sign on 모드 Azure AD에서 지 원하는 방법에 대 한 하나의 toochoose 어떤 응용 프로그램 hello toopick 관심 있는에 있습니다.

## <a name="single-sign-on-and-provisioning-modes-supported-by-specific-application-types"></a>특정 응용 프로그램 형식에서 지원되는 Single Sign-On 및 프로비전 모드

hello 표에서 hello 다른 single sign on 및 각 응용 프로그램 종류 위에 hello에서 지 원하는 모드 프로 비전을 설명 합니다. 이 테이블 toohelp를 사용할 수 있습니다 toounderstand 필요한 응용 프로그램을 tooadd toosupport 구체적인 목표입니다.

  ![앱 형식 표](./media/application-tables/table1.png)

## <a name="how-toochoose-a-single-sign-on-mode"></a>어떻게 toochoose single sign on 모드

지원 되는 hello **단일 로그온** Azure AD 응용 프로그램에 대 한 모드는 다음과 같습니다.

-   **Azure AD에서 single sign-on 사용 하지 않도록 설정** – Azure AD에서 single sign-on 사용 하지 않도록 설정 선택 **single sign on 모드** 아직 준비 되지 않음 toointegrate로 Azure ad에서 single sign이 응용이 프로그램은 또는 아웃 테스트 하기만 하는 경우

-   **로그온 연결** – hello 선택 [연결 된 로그온](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **single sign on 모드** 는 기존 single sign-on 솔루션와 이미 연결 된 응용 프로그램이 있는 경우 또는 원하는 경우 에 있는 사용자에 대 한 링크는 간단한 toopublish 자신의 [응용 프로그램 액세스 패널로](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) 또는 [Office 365 응용 프로그램 실행 프로그램](https://login.microsoftonline.com/common/oauth2/authorize?response_mode=form_post&response_type=id_token&scope=openid&nonce=d508a995-f6d6-4b8a-81b8-825c71f1be46.636253878097046923&state=https%3a%2f%2fsupport.office.com%2farticle%2fMeet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a%3fui%3den-US%26rs%3den-US%26ad%3dUS&client_id=4b233688-031c-404b-9a80-a4f3f2351f90&redirect_uri=https%3a%2f%2fsupport.office.com%2fauth%2fsignin&login_hint=asteen%40microsoft.com&prompt=none)

-   **암호 기반 로그온** – hello 선택 [암호 기반 로그온](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **single sign on 모드** 응용 프로그램 HTML 사용자 이름 및 암호 필드를 렌더링 하 고 toostore입니다 사용자 이름 및 암호 안전 하 게 toobe 재생 나중에 toohello 응용 프로그램

-   **SAML 기반 로그온** – hello 선택 [SAML 기반 로그온](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) 응용 프로그램 hello SAML 또는 OpenID Connect 프로토콜을 지원 하거나 toobe 수 toomap 사용자 모드에서 single sign toospecific 응용 프로그램 역할 기반 saml 사용자 정의 규칙 클레임 *(**참고:** hello 응용 프로그램 프록시 응용 프로그램에 대해 구성 된 경우이 옵션을 사용할 수 없습니다) *

-   **머리글 기반 로그온** –이 옵션을 선택 [헤더 기반 로그온](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access#what-is-pingaccess-for-azure-ad) single sign on 모드 PingAccess 지 원하는 HTTP 헤더를 사용 하 여 응용 프로그램이 있는 경우 기반 인증을 tooperform 단일 기호에 너무 *(**참고:** hello 응용 프로그램 프록시와 PingAccess 응용 프로그램에 대해 구성 된 경우이 옵션은 사용할 수만) *

-   **Windows 통합 인증을** – hello 선택 [Windows 통합 인증](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) single sign-on 모드를 원하는 tooperform 단일 기호에 너무 하는 온-프레미스 WIA 응용 프로그램을 노출 하는 경우*드 (*  *참고:** hello 응용 프로그램 프록시 응용 프로그램에 대해 구성 된 경우이 옵션은 사용할 수만) *

## <a name="single-sign-on-modes-for-custom-developed-applications"></a>사용자 지정 개발된 응용 프로그램에 대한 Single Sign-On 모드

Hello 통해 개발 하는 사용자 지정 수 있는 응용 프로그램 [응용 프로그램 사용자 지정 개발](#_Custom-Developed_Applications) 환경에 추가 single sign on 모드 위에 나열 되지 않은 지원 합니다. 내용은 다음과 같습니다.

-   [OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code) 기반 로그온

-   [OpenID Connect 1.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-openid-connect-code) 기반 로그온

-   [WS-Federation 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html) 기반 로그온

-   [SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) 기반 로그온

읽기 hello [Azure Active Directory 개발자 가이드](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide) toolearn 어떻게는 이러한 사용자 지정 개발 toocreate 응용 프로그램 single sign on 모드에 대 한 자세한 합니다.

## <a name="how-tooset-an-applications-single-sign-on-mode"></a>어떻게 tooset 응용 프로그램의 single sign on 모드

tooset 응용 프로그램의 **단일 로그온** 아래 지침에 따라 hello 모드:

1.  열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**

2.  열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.

3.  에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.

4.  클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.

5.  클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.

   * 여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**

6.  Hello 응용 프로그램 선택 tooconfigure single sign on

7.  Hello 응용 프로그램 로드 되 면 클릭 **Single sign on** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.

## <a name="next-steps"></a>다음 단계
[응용 프로그램 프록시 single sign on tooyour 앱을 제공 합니다.](active-directory-application-proxy-sso-using-kcd.md)

