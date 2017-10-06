---
title: "FAQ(질문과 대답) - Azure AD B2C | Microsoft Docs"
description: "Azure Active Directory B2C에 대해 자주 묻는 질문과 대답입니다."
services: active-directory-b2c
documentationcenter: 
author: saeeda
manager: krassk
editor: bryanla
ms.assetid: ed33c2ca-76d0-442a-abb1-8b7b7bb92d6a
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/16/2017
ms.author: saeeda
ms.openlocfilehash: f7857299bc3cb9d5fbe58e047818ec56741e0740
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-frequently-asked-questions-faq"></a>Azure AD B2C: FAQ(질문과 대답) 
이 페이지 hello (Azure AD) Azure Active Directory B2C에 대 한 질문과 대답을 제공 합니다. 업데이트를 계속 확인합니다.

### <a name="can-i-use-azure-ad-b2c-features-in-my-existing-employee-based-azure-ad-tenant"></a>기존의 직원 기반 Azure AD 테넌트에서 Azure AD B2C 기능을 사용할 수 있나요?
Azure AD 및 Azure AD B2C는 별도 제품 공존할 수 없으며 hello에 동일한 테 넌 트입니다.  Azure AD 테넌트는 조직을 나타냅니다.  Azure AD B2C 테 넌 트와 신뢰 당사자 응용 프로그램에 사용 되는 identities toobe의 컬렉션을 나타냅니다.  (공개 미리 보기)에서 사용자 지정 정책을 사용 하 여 Azure AD B2C 조직에서 직원의 AD tooAzure 수 있도록 인증을 페더레이션 할 수 있습니다.

### <a name="can-i-use-azure-ad-b2c-tooprovide-social-login-facebook-and-google-into-office-365"></a>Office 365에 Azure AD B2C tooprovide 소셜 로그인 (Facebook 및 Google +)를 사용할 수 있습니까?
Azure AD B2C Microsoft Office 365에 대 한 사용된 tooauthenticate 사용자 일 수 없습니다.  Azure AD는 직원 액세스 tooSaaS 앱 관리를 위한 Microsoft의 솔루션 있으며 라이선스 및 조건부 액세스와 같은 이러한 목적으로 디자인 하는 기능입니다.  Azure AD B2C는 웹 및 모바일 응용 프로그램을 빌드하기 위한 ID 및 액세스 관리 플랫폼을 제공합니다.  Azure AD B2C 구성된 toofederate tooan Azure AD 테 넌 트 이면 hello Azure AD 테 넌 트 Azure AD B2C에 의존 하는 직원 액세스 tooapplications를 관리 합니다.

### <a name="what-are-local-accounts-in-azure-ad-b2c-how-are-they-different-from-work-or-school-accounts-in-azure-ad"></a>Azure AD B2C에서 로컬 계정은 무엇인가요? Azure AD의 회사 또는 학교 계정과 어떻게 다른가요?
Azure AD 테 넌 트에 toohello 테 넌 트에 속한 사용자에 게 로그인 hello 폼의 전자 메일 주소와 `<xyz>@<tenant domain>`합니다.  hello `<tenant domain>` 도메인 hello에 테 넌 트 또는 초기 hello 확인할 hello 중 하나는 `<...>.onmicrosoft.com` 도메인입니다. 이 계정 유형은 회사 또는 학교 계정입니다.

Azure AD B2C 테 넌 트의 대부분의 응용 프로그램 원하는 hello 사용자 toosign에서 모든 임의의 전자 메일 주소 (예를 들어 joe@comcast.net, bob@gmail.com, sarah@contoso.com, 또는 jim@live.com). 이 계정 유형은 로컬 계정입니다.  또한 임의의 사용자 이름이 로컬 계정으로 지원됩니다(예: joe, bob, sarah 또는 jim). Azure AD B2C hello Azure 포털에서에서 구성 하 여 이러한 두 로컬 계정 유형 중 하나를 선택할 수 있습니다.

### <a name="which-social-identity-providers-do-you-support-now-which-ones-do-you-plan-toosupport-in-hello-future"></a>지금 어떤 소셜 ID 공급자를 지원하나요? 않은 있습니다 toosupport hello 향후에 계획?
현재 Facebook, Google+, LinkedIn, Amazon, Twitter(미리 보기), WeChat(미리 보기), Weibo(미리 보기) 및 QQ(미리 보기)가 지원됩니다. 고객의 요구에 따라 다른 인기 있는 소셜 ID 공급자에 대한 지원을 추가합니다.

Azure AD B2C에서는 [사용자 지정 정책](https://docs.microsoft.com/en-us/azure/active-directory-b2c/active-directory-b2c-overview-custom)에 대한 지원도 추가했습니다.  이러한 [사용자 지정 정책을](https://docs.microsoft.com/en-us/azure/active-directory-b2c/active-directory-b2c-overview-custom) 개발자 toocreate 지원 하는 모든 id 공급자와는 자체 정책이 허용 [OpenID Connect](http://openid.net/specs/openid-connect-core-1_0.html) 또는 SAML 합니다. 

[사용자 지정 정책 시작 팩](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack)을 확인하여 사용자 지정 정책을 시작하세요.

### <a name="can-i-configure-scopes-toogather-more-information-about-consumers-from-various-social-identity-providers"></a>구성 범위 toogather 다양 한 소셜 id 공급자에서 소비자에 대 한 자세한 내용은?
아니요, 하지만 이 기능은 우리의 로드맵입니다. 소셜 id 공급자는 지원 되는 집합에 사용 하는 hello 기본 범위는:

* Facebook: 전자 메일
* Google+: 전자 메일
* Microsoft 계정: openid 메일 프로필
* Amazon: 프로필
* LinkedIn: r_emailaddress, r_basicprofile

### <a name="does-my-application-have-toobe-run-on-azure-for-it-work-with-azure-ad-b2c"></a>내 응용 프로그램과 Azure AD B2C 사용에 대 한 Azure에서 실행 toobe 있습니까?
아니요, 모든 위치 (hello 클라우드 또는 온-프레미스)에서 응용 프로그램을 호스트할 수 있습니다. Azure AD B2C와 toointeract 필요한 모든은 기능 toosend hello 및 공개적으로 액세스할 수 있는 끝점에 HTTP 요청을 수신 합니다.

### <a name="i-have-multiple-azure-ad-b2c-tenants-how-can-i-manage-them-on-hello-azure-portal"></a>여러 개의 Azure AD B2C 테넌트가 있습니다. 관리 방법으로 hello Azure 포털에서?
전환 해야 ' Azure AD B2C' hello Azure 포털의 hello 왼쪽 메뉴에서를 열기 전에 원하는 toomanage hello 디렉터리에 있습니다.  Hello 오른쪽 상단의 hello Azure 포털에서 사용자의 id를 클릭 하 여 디렉터리를 전환 하 고 hello 드롭다운에 있는 디렉터리는 표시를 선택 합니다.  이미지와 함께 단계별 마법사, 참조 [tooAzure AD B2C 설정 이동](active-directory-b2c-app-registration.md#navigate-to-b2c-settings)합니다.

### <a name="how-do-i-customize-verification-emails-hello-content-and-hello-from-field-sent-by-azure-ad-b2c"></a>확인 전자 메일을 지정 하는 방법 (콘텐츠 hello 및 hello "에서:" 필드)가 Azure AD B2C 보낸?
Hello를 사용할 수 있습니다 [회사 브랜딩 기능](../active-directory/active-directory-add-company-branding.md) 확인 전자 메일의 toocustomize hello 내용입니다. 특히,이 두 요소 hello 전자 메일의을 사용자 지정할 수 있습니다.

* **배너 로고**: 오른쪽 아래 hello에 표시 합니다.
* **배경색**: hello 위쪽에 표시 합니다.

    ![사용자 지정된 확인 전자 메일의 스크린샷](./media/active-directory-b2c-faqs/company-branded-verification-email.png)

hello 전자 메일 서명 hello B2C 테 넌 트를 처음 만들 때 사용자가 제공한 hello B2C 테 넌 트의 이름이 포함 됩니다. 이러한 지침을 사용 하는 hello 이름을 변경할 수 있습니다.

1. Toohello 로그인 [Azure 클래식 포털](https://manage.windowsazure.com/) 구독 관리자 hello으로 합니다.
1. Tooyour B2C 테 넌 트를 이동 합니다.
1. Hello 클릭 **구성** 탭 합니다.
1. 변경 hello **이름** hello 아래 **디렉터리 속성** 섹션.
1. 클릭 **저장** hello hello 페이지 맨 아래에 있습니다.

현재이 방법은 toochange hello "에서:" 필드에 hello 전자 메일입니다. 에 대해 투표 [feedback.azure.com](https://feedback.azure.com/forums/169401-azure-active-directory/suggestions/15334335-fully-customizable-verification-emails) hello hello 확인 전자 메일 본문의 사용자 지정에 관심이 있습니다.

### <a name="how-can-i-migrate-my-existing-user-names-passwords-and-profiles-from-my-database-tooazure-ad-b2c"></a>내 데이터베이스 tooAzure AD B2C에서에서 내 기존 사용자 이름, 암호 및 프로필 마이그레이션할 수는 방법
Hello Azure AD Graph API toowrite 마이그레이션 도구를 사용할 수 있습니다. Hello 참조 [Graph API 샘플](active-directory-b2c-devquickstarts-graph-dotnet.md) 대 한 자세한 내용은 합니다.

### <a name="what-password-policy-is-used-for-local-accounts-in-azure-ad-b2c"></a>Azure AD B2C의 로컬 계정에 사용되는 암호 정책은 무엇인가요?
로컬 계정에 대 한 Azure AD B2C 암호 정책을 hello은 Azure AD에 대 한 hello 정책을 기반으로 합니다. Azure AD B2C의 등록, 등록 하거나 로그인 및 암호 정책을 사용 하 여 hello "강력한" 암호 강도 다시 설정 하 고 암호는 만료 되지 않습니다. 읽기 hello [Azure AD 암호 정책](https://msdn.microsoft.com/library/azure/jj943764.aspx) 내용을 확인 합니다.

### <a name="can-i-use-azure-ad-connect-toomigrate-consumer-identities-that-are-stored-on-my-on-premises-active-directory-tooazure-ad-b2c"></a>내 온-프레미스 Active Directory tooAzure AD B2C에 저장 된 Azure AD Connect toomigrate 소비자 id를 사용할 수 있습니까?
아니요, Azure AD Connect와 Azure AD B2C 디자인 된 toowork 않습니다. Hello를 사용 하는 것이 좋습니다 [Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md) 사용자 마이그레이션에 대 한 합니다.

### <a name="can-my-app-open-up-azure-ad-b2c-pages-within-an-iframe"></a>앱의 Azure AD B2C 페이지가 iFrame 내에서 열릴 수 있나요?
아니요. 보안상의 이유로, Azure AD B2C 페이지는 iFrame 내에서 열릴 수 없습니다.  서비스는 hello 브라우저 tooprohibit Iframe와 통신합니다.  보안 커뮤니티 일반적 hello 및 OAUTH2 사양 hello, 클릭 jacking toohello 위험이 인해 identity 경험에 대 한 Iframe을 사용 하는 것이 좋습니다.

### <a name="does-azure-ad-b2c-work-with-crm-systems-such-as-microsoft-dynamics"></a>Azure AD B2C는 Microsoft Dynamics와 같은 CRM 시스템과 함께 작동합니까?
Microsoft Dynamics 365 포털과의 통합을 사용할 수 있습니다.  참조 [인증에 대 한 Azure AD B2C Dynamics 365 포털 구성 toouse](https://docs.microsoft.com/en-us/dynamics365/customer-engagement/portals/azure-ad-b2c)합니다.

### <a name="does-azure-ad-b2c-work-with-sharepoint-on-premises-2016-or-earlier"></a>Azure AD B2C가 SharePoint 온-프레미스 2016 또는 이전 버전과 함께 작동하나요?
Azure AD B2C hello SharePoint 외부 파트너 공유 시나리오;에 적용 되지 않습니다. 참조 [Azure AD B2B](http://blogs.technet.com/b/ad/archive/2015/09/15/learn-all-about-the-azure-ad-b2b-collaboration-preview.aspx) 대신 합니다.

### <a name="should-i-use-azure-ad-b2c-or-b2b-toomanage-external-identities"></a>Azure AD B2C 또는 B2B toomanage 외부 id를 사용 해야 합니까?
이 문서에 대 한 읽기 [외부 id](../active-directory/active-directory-b2b-compare-external-identities.md) toolearn hello를 적용 하는 방법에 대 한 보다 적절 tooyour 외부 id 시나리오를 제공 합니다.

### <a name="what-reporting-and-auditing-features-does-azure-ad-b2c-provide-are-they-hello-same-as-in-azure-ad-premium"></a>Azure AD B2C가 제공하는 보고 및 감사 기능은 무엇인가요? 동일한 Azure AD Premium에서와 같이 hello?
아니요, Azure AD B2C 동일 보고서 집합을 Azure AD Premium으로 hello를 지원 하지 않습니다. 하지만 많은 공통점이 있습니다.

* hello 로그인 보고서의 각 로그인 감소 세부 정보로 레코드를 제공 합니다.
* 감사 보고서 hello Azure Active Directory에서 Azure 포털에서에서 사용할 수 있는 > 활동 감사 로그 > B2C 선택 하 고 필요에 따라 필터를 적용 합니다. 관리 작업 및 응용 프로그램 작업을 모두 다룹니다. 
* 사용자 수, 로그인 수 및 MFA 볼륨을 다루는 사용 보고는 [사용 보고 API](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-usage-reporting-api)에서 제공됩니다.

### <a name="can-i-localize-hello-ui-of-pages-served-by-azure-ad-b2c-what-languages-are-supported"></a>Azure AD B2C에서 제공 하는 페이지의 UI hello를 지역화할 수 있습니까? 어떤 언어가 지원되나요?
예!  공개 미리 보기로 제공되는 [언어 사용자 지정](active-directory-b2c-reference-language-customization.md)을 참조하세요.  36 언어에 대 한 번역을 제공 하 고 모든 문자열 toosuit 사용자의 요구를 재정의할 수 있습니다.

### <a name="can-i-use-my-own-urls-on-my-sign-up-and-sign-in-pages-that-are-served-by-azure-ad-b2c-for-instance-can-i-change-hello-url-from-loginmicrosoftonlinecom-toologincontosocom"></a>Azure AD B2C에서 제공하는 등록 및 로그인 페이지에 고유 URL을 사용할 수 있나요? Hello URL login.microsoftonline.com toologin.contoso.com에서 변경할 수는 예를 들어,
현재는 아닙니다. 이 기능은 우리의 로드맵입니다. Hello에서 도메인 확인 **도메인** hello Azure 클래식 포털에 탭이이 목표를 달성 하지 않습니다.

### <a name="how-do-i-delete-my-azure-ad-b2c-tenant"></a>Azure AD B2C 테넌트를 삭제하려면 어떻게 해야 하나요?
이러한 단계 toodelete Azure AD B2C 테 넌 트를 수행 합니다.

1. 다음 단계를 너무[tooAzure AD B2C 설정을 이동](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) hello Azure 포털에 있습니다.
1. Toohello 이동 **응용 프로그램**, **Id 공급자**, 및 **모든 정책** 각각의 제품에서 모든 hello 항목을 삭제 합니다.
1. 이제 toohello 로그인 [Azure 클래식 포털](https://manage.windowsazure.com/) 구독 관리자 hello으로 합니다. (회사 또는 학교 계정 또는 toosign Azure에 대해 사용 되는 동일한 Microsoft 계정 hello 동일 hello를 사용 합니다.)
1. Hello 왼쪽에서 Active Directory 확장 toohello 이동한 B2C 테 넌 트를 클릭 합니다.
1. Hello 클릭 **사용자** 탭 합니다.
1. (제외 hello 구독 관리자 사용자로 현재 로그인)에 각 사용자를 선택 합니다. 클릭 **삭제** hello 누른 hello 페이지 맨 아래에 **예** 대화 상자가 나타나면 합니다.
1. Hello 클릭 **응용 프로그램** 탭 합니다.
1. 선택 **회사가 보유 한 응용 프로그램** hello에 **표시** 드롭 다운 필드와 클릭 hello 확인 표시 합니다.
1. **b2c-extensions-app**이라는 응용 프로그램. 클릭 **삭제** hello 누른 hello 페이지 맨 아래에 **예** 대화 상자가 나타나면 합니다.
1. Toohello Active Directory 확장을 다시 이동 하 고 B2C 테 넌 트를 선택 합니다.
1. 클릭 **삭제** hello hello 페이지 맨 아래에 있습니다. hello 지침 hello 화면에 따라 toocomplete hello 프로세스입니다.

### <a name="can-i-get-azure-ad-b2c-as-part-of-enterprise-mobility-suite"></a>Enterprise Mobility Suite의 일부로 Azure AD B2C를 가져올 수 있나요?
아니요, Azure AD B2C는 종량제 Azure 서비스이며 Enterprise Mobility Suite의 일부가 아닙니다.

### <a name="how-do-i-report-issues-with-azure-ad-b2c"></a>Azure AD B2C에서 발생한 문제를 보고하려면 어떻게 해야 합니까?
[Azure Active Directory B2C에 대한 파일 지원 요청](active-directory-b2c-support.md)을 참조하세요.
