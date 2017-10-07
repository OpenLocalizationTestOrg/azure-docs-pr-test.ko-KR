---
title: "응용 프로그램을 응용 프로그램을 추가할 때 toouse 입력 aaaHow toochoose | Microsoft Docs"
description: "지원 되는 hello 유형의 Azure AD와 통합할 수 있습니다 하는 응용 프로그램 이해 및 관련된 구성 옵션"
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
ms.openlocfilehash: 46e3672e7f5048b0fa54171f0fc169362c9d5ac6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toochoose-which-application-type-toouse-when-adding-an-application"></a>어떻게 응용 프로그램을 응용 프로그램을 추가할 때 toouse 입력 toochoose

이 문서가 도움이 되었나요 toounderstand hello 라는 네 가지 종류의 응용 프로그램을 Azure AD와 통합할 수 있습니다.

* 각 형식에 의해 지원되는 항목
* 해당 응용 프로그램을 선택할 수도 있는 이유
* 어떻게 tooconfigure 해당 응용 프로그램의 핵심 속성 같은 사용자가 방법을 **프로 비전**, 기능 또는 **단일 로그온** 기술 toouse 합니다.

## <a name="supported-application-types-in-azure-ad"></a>Azure AD에서 지원되는 응용 프로그램 형식

Azure AD에서는 4 개의 주 응용 프로그램 유형을 사용 하 여 추가할 수 있는 hello **추가** 기능을 확인할 **엔터프라이즈 응용 프로그램**합니다. 내용은 다음과 같습니다.

-   **Azure AD 갤러리 응용 프로그램** – Single Sign-On에 대해 Azure AD와 사전 통합된 응용 프로그램입니다.

-   **응용 프로그램 프록시 응용 프로그램** – tooprovide 보안 single sign-on tooexternally 원하는 온-프레미스 환경에서 실행 중인 응용 프로그램입니다.

-   **사용자 지정 응용 프로그램 개발** – 조직에서 toodevelop 하지 않고자 한다면 응용 프로그램에 Azure AD 응용 프로그램 개발 플랫폼 hello 하지만 아직 존재 하지 않을 수 있습니다.

-   **비 갤러리 응용 프로그램** – 사용자의 응용 프로그램을 가져옵니다! 원하는 모든 웹 링크 또는 사용자 이름 및 암호 필드를 렌더링 하는 응용 프로그램에는 SAML 또는 OpenID Connect 프로토콜을 지원 또는 Azure ad에서 single sign-on toointegrate 복원할 SCIM를 지원 합니다.

## <a name="features-and-capabilities-supported-by-all-hello-above-application-types"></a>기능 및 응용 프로그램 종류 위의 모든 hello에서 지 원하는 기능

hello 다음과 같은 기능이 지원 됩니다 hello 위의 4 응용 프로그램 종류의 Azure AD에서.

-   **빠른 시작** – [간단한 배포 단계](https://docs.microsoft.com/azure/active-directory/active-directory-integrating-applications-getting-started)를 수행하여 신속하게 응용 프로그램 시작

-   **일반 속성 관리** -가져오기는 [직접 딥 링크](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users) tooan 응용 프로그램 [hello 브랜딩 사용자 지정](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-change-app-logo-user-azure-portal) 응용 프로그램의 또는 [hello응용프로그램을사용하지않도록설정](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) 모든 사용자에 대 한 합니다.

-   **사용자 및 그룹 관리** – [할당](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) 또는 [제거](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) tooan 응용 프로그램을 사용자 및 그룹 및 필요에 따라이 사용자 및 그룹에 대 한 액세스 권한이 할당 hello 특정 응용 프로그램 역할

-   **셀프 서비스 응용 프로그램 액세스** – 사용자가 toorequest 활성화 [셀프 서비스 응용 프로그램 액세스](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) tooan 응용 프로그램에서 해당 응용 프로그램 액세스 패널 응용 프로그램을 직접 추가 하 여 하나 또는 [ 셀프 서비스 활성화 된 그룹에 가입](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management), 선택적으로 hello 따라 비즈니스 승인이 필요한 방식으로

-   **로그인 로그가** – 참조 [로그인 tooan 응용 프로그램을 hello 모든](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins), 또는 모든 응용 프로그램

-   **감사 로그** – 참조 [수정 tooan 응용 프로그램에 대 한 감사 로그 세부](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs), 또는 tooall 응용 프로그램

-   **조건부 및 위험 기반 액세스** 강력한 설정 – [조건 기반 액세스 규칙](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access) toosign tooa 특정 응용 프로그램에서 사용자가 때 적용 되는

-   **권한 보기** – hello의 [OAuth2 권한](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent) 응용 프로그램은 액세스 tooin 디렉터리 한 곳에서

## <a name="single-sign-on-and-provisioning-modes-supported-by-specific-application-types"></a>특정 응용 프로그램 형식에서 지원되는 Single Sign-On 및 프로비전 모드

hello 표에서 hello 다른 single sign on 및 각 응용 프로그램 종류 위에 hello에서 지 원하는 모드 프로 비전을 설명 합니다. 이 테이블 toohelp를 사용할 수 있습니다 toounderstand 필요한 응용 프로그램을 tooadd toosupport 구체적인 목표입니다.

  ![앱 형식 테이블](./media/application-tables/table1.png)

## <a name="how-toochoose-a-single-sign-on-mode"></a>어떻게 toochoose single sign on 모드

지원 되는 hello **단일 로그온** Azure AD 응용 프로그램에 대 한 모드는 다음과 같습니다.

-   **Azure AD에서 single sign-on 사용 하지 않도록 설정** – Azure AD에서 single sign-on 사용 하지 않도록 설정 선택 **single sign on 모드** 아직 준비 되지 않음 toointegrate로 Azure ad에서 single sign이 응용이 프로그램은 또는 아웃 테스트 하기만 하는 경우

-   **로그온 연결** – hello 선택 [연결 된 로그온](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **single sign on 모드** 는 기존 single sign-on 솔루션와 이미 연결 된 응용 프로그램이 있는 경우 또는 원하는 경우 에 있는 사용자에 대 한 링크는 간단한 toopublish 자신의 [응용 프로그램 액세스 패널로](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) 또는 [Office 365 응용 프로그램 실행 프로그램](https://login.microsoftonline.com/common/oauth2/authorize?response_mode=form_post&response_type=id_token&scope=openid&nonce=d508a995-f6d6-4b8a-81b8-825c71f1be46.636253878097046923&state=https%3a%2f%2fsupport.office.com%2farticle%2fMeet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a%3fui%3den-US%26rs%3den-US%26ad%3dUS&client_id=4b233688-031c-404b-9a80-a4f3f2351f90&redirect_uri=https%3a%2f%2fsupport.office.com%2fauth%2fsignin&login_hint=asteen%40microsoft.com&prompt=none)

-   **암호 기반 로그온** – hello 선택 [암호 기반 로그온](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **single sign on 모드** 응용 프로그램 HTML 사용자 이름 및 암호 필드를 렌더링 하 고 toostore입니다 사용자 이름 및 암호 안전 하 게 toobe 재생 나중에 toohello 응용 프로그램

-   **SAML 기반 로그온** – hello 선택 [SAML 기반 로그온](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) 응용 프로그램 hello SAML 또는 OpenID Connect 프로토콜을 지원 하거나 toobe 수 toomap 사용자 모드에서 single sign toospecific 응용 프로그램 역할 기반 saml 사용자 정의 규칙 클레임 *

   >[!NOTE]
   >Hello 응용 프로그램 프록시 응용 프로그램에 대해 구성 된 경우에이 옵션은 사용할 수 없습니다.
   >
   >

-   **머리글 기반 로그온** –이 옵션을 선택 [헤더 기반 로그온](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access#what-is-pingaccess-for-azure-ad) single sign on 모드 PingAccess 지 원하는 HTTP 헤더를 사용 하 여 응용 프로그램이 있는 경우 기반 인증을 tooperform 단일 기호에 너무

   >[!NOTE]
   >이 옵션은 응용 프로그램 프록시와 PingAccess hello 응용 프로그램에 대해 구성 된 경우에 사용할 수 있습니다.
   >
   >

-   **Windows 통합 인증을** – hello 선택 [Windows 통합 인증](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) single sign-on 모드를 원하는 tooperform 단일 기호에 너무 하는 온-프레미스 WIA 응용 프로그램을 노출 하는 경우

   >[!NOTE]
   >이 옵션은 hello 응용 프로그램 프록시 응용 프로그램에 대해 구성 된 경우에 사용할 수 있습니다.
   >
   >

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

6.  Tooconfigure single sign on 원하는 hello 응용 프로그램을 선택 합니다.

7.  Hello 응용 프로그램 로드 되 면 클릭 **Single sign on** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.

## <a name="how-toochoose-a-provisioning-mode"></a>어떻게 toochoose 프로비저닝 모드

-   **수동 프로 비전** – hello 선택 [수동](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#provisioning-modes) 기존 계정이 있는 또는 외부 Azure AD에서이 응용 프로그램에 대 한 toomanage 계정을 지정할 경우 프로 비전 모드입니다.

-   **자동 프로 비전** – hello 선택 [자동](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#configuring-automatic-user-account-provisioning) **프로비저닝 모드** 사용자 계정을 toothis tooenable 자동 API 기반 프로 비전 및/또는의 프로 비전 해제 하려는 경우 응용 프로그램 

   >[!NOTE]
   >이 옵션은 hello 내에서 응용 프로그램에 대해서만 사용할 수 있는 **갖춘** hello 범주의 [Azure AD 응용 프로그램 갤러리](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-whats-new-azure-portal#the-new-and-improved-application-gallery)합니다.
   >
   >

-   **자동 프로 비전 SCIM 기반** – 사용 하 여 [SCIM 기반 자동 프로 비전](https://docs.microsoft.com/azure/active-directory/active-directory-scim-provisioning) 응용 프로그램 변경 내용 toousers 및 변경 내용에 대해 자동으로 내보내는 그룹 검색에 대 한 hello SCIM 프로토콜을 지 원하는 경우 Azure AD와 통합 tooany 응용 프로그램 

   >[!NOTE]
   >이 옵션은 특정 프로비전 모드로 나열되어 있지 않지만 Azure AD와 통합된 모든 응용 프로그램에 기본적으로 활성화됩니다.
   >
   >

## <a name="how-tooset-an-applications-provisioning-mode"></a>어떻게 tooset 응용 프로그램의 프로 비전 모드

tooset 응용 프로그램의 **프로 비전** 아래 지침에 따라 hello 모드:

tooset 응용 프로그램의 **단일 로그온** 아래 지침에 따라 hello 모드:

1.  열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**

2.  열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.

3.  에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.

4.  클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.

5.  클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.

  * 여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**

6.  Tooconfigure 프로 비전 하려는 hello 응용 프로그램을 선택 합니다.

7.  Hello 응용 프로그램 로드 되 면 클릭 **프로 비전** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.

## <a name="next-steps"></a>다음 단계
[Azure Active Directory로 응용 프로그램 관리](active-directory-enable-sso-scenario.md)
