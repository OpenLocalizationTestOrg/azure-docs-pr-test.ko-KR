---
title: "hello Azure Active Directory에서에서 엔터프라이즈 응용 프로그램에 대 한 관리 로그온 aaaSingle | Microsoft Docs"
description: "Toomanage single sign-on 엔터프라이즈 응용 프로그램을 사용 하 여 Azure Active Directory hello 하는 방법에 대해 알아봅니다"
services: active-directory
documentationcenter: 
author: asmalser
manager: femila
editor: 
ms.assetid: bcc954d3-ddbe-4ec2-96cc-3df996cbc899
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/26/2017
ms.author: asmalser
ms.openlocfilehash: b0a8e622ab10517b7b69f786406b6e9b9f2e7eaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-single-sign-on-for-enterprise-apps"></a>엔터프라이즈 앱에 대한 Single Sign-On 관리
> [!div class="op_single_selector"]
> * [Azure 포털](active-directory-enterprise-apps-manage-sso.md)
> * [Azure 클래식 포털](active-directory-sso-integrate-saas-apps.md)
> 

이 문서에서는 설명 방법을 toouse hello [Azure 포털](https://portal.azure.com) toomanage single sign on 설정 엔터프라이즈 응용 프로그램에 대 한 합니다. 엔터프라이즈 앱은 조직 내에서 배포 및 사용되는 앱입니다. 이 문서에는 hello에서 추가 된 tooapps 특히 적용 됩니다. [Azure Active Directory 응용 프로그램 갤러리](active-directory-appssoaccess-whatis.md#get-started-with-the-azure-ad-application-gallery)합니다. 

## <a name="finding-your-apps-in-hello-portal"></a>Hello 포털에서 앱 찾기
Single sign on 설정 되어 있는 모든 엔터프라이즈 응용 프로그램 확인 및 hello Azure 포털에서에서 관리할 수 있습니다. hello 응용 프로그램에 hello 있습니다 **더 서비스** &gt; **엔터프라이즈 응용 프로그램** hello 포털의 섹션입니다. 

![엔터프라이즈 응용 프로그램 블레이드][1]

선택 **모든 응용 프로그램** tooview 구성 된 모든 앱의 목록입니다. 응용 프로그램을 선택 하면 해당 앱에 대 한 보고서를 볼 수 있습니다 하 고 다양 한 설정 관리할 수 있는 해당 앱에 대 한 hello 리소스 블레이드를 로드 합니다.

toomanage single sign on 설정, 선택 **Single sign on**합니다.

![응용 프로그램 리소스 블레이드][2]

## <a name="single-sign-on-modes"></a>Single Sign-On 모드
hello **Single sign on** 블레이드로 시작 하는 **모드** 메뉴 hello single sign on 모드 toobe 구성 되어 있습니다. hello 사용할 수 있는 옵션은 다음과 같습니다.

* **SAML 기반 로그온** -이 옵션은 hello SAML 2.0 프로토콜을 사용 하 여 Azure Active Directory와 전체 페더레이션 single sign on hello 응용 프로그램이 지 원하는 경우 사용할 수 있습니다.
* **암호 기반 로그온** - 이 옵션은 Azure AD가 이 응용 프로그램에 대해 입력하는 암호 양식을 지원하는 경우 사용할 수 있습니다.
* **기호에 있는 연결 된** -이전에 "기존 single sign on",이 옵션을 사용 하면 관리자가 tooplace 링크 toothis 응용 프로그램에서 해당 사용자의 Azure AD 액세스 패널 또는 Office 365 응용 프로그램 실행 프로그램입니다.

이러한 모드에 대한 자세한 내용은 [Azure Active Directory에서 Single Sign-On이 작동하는 방식](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work)을 참조하세요.

## <a name="saml-based-sign-on"></a>SAML 기반 로그온
hello **SAML 기반 로그온** 옵션 4 개 섹션에서 나누어져 있는 블레이드를 표시 합니다.

### <a name="domains-and-urls"></a>도메인 및 URL
이 hello 응용 프로그램 도메인 및 Url에 대 한 모든 세부 정보 tooyour Azure AD 디렉터리를 추가 됩니다. 모든 입력 toomake single sign on 작업 앱 hello 화면에 직접 표시 hello를 선택 하 여 모든 선택적 입력을 볼 수 있지만 필요한 **고급 URL 설정 표시** 확인란을 선택 합니다. 지원 되는 입력 hello 전체 목록에는 다음이 포함 됩니다.

* **로그온 URL** hello 사용자가 응용 프로그램에서 toosign toothis 위치 – 합니다. Hello 응용 프로그램은 단일 공급자가 시작한 로그온 하는 구성 된 tooperform 서비스 hello 서비스 공급자가 필요한 hello는 사용자가 toothis URL, 다음 리디렉션 tooAzure AD tooauthenticate 및 로그인에 사용자를 hello 합니다. 이 필드는 채워집니다 경우 Azure AD는이 URL toolaunch hello 응용 프로그램에서 Office 365 및 Azure AD 액세스 패널 hello를 사용 합니다. 이 필드를 생략 하면 다음 Azure AD id 공급자를 대신 수행 하는 경우-시작 된 로그온 hello 앱 시작 시 hello Azure AD 또는 Office 365, Azure AD 액세스 패널 hello에서에서 single sign on URL입니다.
* **식별자** -구성 되는 단일 로그온에 대 한이 URI hello 응용 프로그램을 고유 하 게 식별 해야 합니다. 이 값은 Azure AD는 hello SAML 토큰의 대상 그룹 매개 변수를 hello로 백 tooapplication를 보냅니다 및 hello 응용 프로그램은 예상된 toovalidate hello 값 것입니다. 이 값은 또한 hello 응용 프로그램에서 제공 하는 SAML 메타 데이터에 엔터티 ID hello로 나타납니다.
* **회신 URL** -hello 회신 URL은 hello 응용 프로그램이 tooreceive hello SAML 토큰을 예상 하는 위치입니다. 또한 참조 tooas hello 서비스 ACS (Assertion Consumer) URL입니다. 이러한 입력 된 다음 tooproceed toohello 다음 화면을 클릭 합니다. 이 화면 어떤 요구 toobe에 구성 된 응용 프로그램 쪽 tooenable hello 것 tooaccept Azure AD에서 SAML 토큰에 대 한 정보를 제공 합니다.
* **릴레이 상태** -hello 릴레이 상태가 인증이 완료 된 후 사용자 hello tooredirect는 여기서 hello 응용 프로그램에 지시 하는 데 도움이 되는 선택적 매개 변수입니다. 하지만 일반적으로 hello 값이 올바른 URL이 hello 응용 프로그램에서 일부 응용 프로그램에서이 필드를 다르게 사용 (hello 응용 프로그램의 단일 로그인에 대 한 자세한 내용은 설명서 참조). hello 기능 tooset hello 릴레이 상태가 고유 toohello 새 Azure 포털을가 하는 새로운 기능입니다.

### <a name="user-attributes"></a>사용자 특성
여기서 관리자를 볼 수와 편집 hello 특성을 Azure AD에서 발행 toohello 응용 프로그램 사용자가 각 hello SAML 토큰에 전송 된 로그인입니다.

지원 되는 편집 가능한 특성은 hello hello **사용자 식별자** 특성입니다. 이 특성의 값 hello는 hello 응용 프로그램 내에서 각 사용자를 고유 하 게 식별 하는 Azure AD의 hello 필드입니다. 예를 들어 hello 앱에서 "전자 메일 주소" hello hello 사용자 이름 및 고유 식별자로 사용 하 여 배포 된 경우 다음 hello 값은 설정 됩니다 toohello "user.mail" 필드에 Azure AD.

### <a name="saml-signing-certificate"></a>SAML 서명 인증서
이 섹션에는 Azure AD toosign hello SAML 발급 된 토큰을 인증 하는 각 타임 hello 사용자 toohello 응용 프로그램에서는 hello 인증서의 hello 세부 표시 합니다. Hello 현재 인증서 toobe 검사 hello 만료 날짜를 포함 하 여의 hello 속성 수 있습니다.

### <a name="application-configuration"></a>응용 프로그램 구성
hello 최종 섹션에서는 hello 설명서 및/또는 컨트롤 필요한 tooconfigure hello 응용 프로그램 자체 toouse Azure Active Directory를 id 공급자로 합니다.

hello **응용 프로그램 구성** 플라이 아웃 메뉴 hello 응용 프로그램을 구성 하기 위한 새 간결 하 고 포함 된 지침을 제공 합니다. 다른 새 기능 고유 toohello 새 Azure 포털입니다.

> [!NOTE]
> 포함 된 설명서의 전체 예제는 hello Salesforce.com 응용 프로그램을 참조 하십시오. 추가 앱에 대한 설명서는 계속 추가됩니다.
> 
> 

![포함된 문서][3]

## <a name="password-based-sign-on"></a>암호 기반 로그온
암호 기반 SSO 모드 및 선택 hello 응용 프로그램에 대 한 지원 되는 경우을 선택 하면 hello **저장** 즉시 toodo 구성 암호 기반 SSO 합니다. 암호 기반 SSO를 배포하는 방법은 [Azure Active Directory에서 Single Sign-On이 작동하는 방식](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work)을 참조하세요.

![암호 기반 로그온][4]

## <a name="linked-sign-on"></a>연결된 로그온
Hello 응용 프로그램에 대 한 지원 되는 경우 연결 된 hello SSO 모드를 선택 하면 있습니다 tooenter hello URL을 hello Azure AD 액세스 패널 또는 Office 365 tooredirect toowhen을 클릭 하 여이 응용 프로그램입니다. 연결된 SSO(이전의 "기존 SSO")에 대한 자세한 내용은 [Azure Active Directory에서 Single Sign-On이 작동하는 방식](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work)을 참조하세요.

![연결된 로그온][5]

##<a name="feedback"></a>사용자 의견

Azure AD 환경 개선 hello를 사용 하 여 원하는 하시기 바랍니다. 들어오는 hello 피드백을 유지 하세요! Hello에 피드백 및 개선 위한 아이디어 게시 **관리자 포털** 섹션 우리의 [피드백 포럼](https://feedback.azure.com/forums/169401-azure-active-directory/category/162510-admin-portal)합니다.  에서는 매일 멋진 새로운 기능을 작성 하는 방법에 대 한 기대 하는 및 사용 하 여 지침 tooshape 다음에 빌드 정의 합니다.

[1]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-blade.PNG
[2]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-sso-blade.PNG
[3]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-blade-embedded-docs.PNG
[4]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-blade-password-sso.PNG
[5]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-blade-linked-sso.PNG
