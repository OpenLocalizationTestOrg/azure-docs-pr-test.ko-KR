---
title: "aaaWhat은 Azure Active Directory와 응용 프로그램 액세스 및 single sign on은? | Microsoft Docs"
description: "Azure Active Directory tooenable single sign on tooall hello SaaS 및 웹 응용 프로그램의 비즈니스에 필요한 사용 합니다."
services: active-directory
documentationcenter: 
author: asmalser-msft
manager: femila
editor: 
ms.assetid: 75d1a3fd-b3c5-4495-a5c8-c4c24145ff00
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: curyand
ms.openlocfilehash: 429522cbd570ab27359c4630c5a6d7b25b692ec5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-application-access-and-single-sign-on-with-azure-active-directory"></a>Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?
Single sign on 의미 수 tooaccess 모든 hello 응용 프로그램 및 리소스를 한 번만 단일 사용자 계정을 사용 하 여 로그인 toodo 비즈니스 해야 합니다. 로그인 한 후 모든 hello 필요한 응용 프로그램을 tooauthenticate 필요는 없지만 액세스할 수 있습니다 (예: 암호 입력)를 두 번입니다.

대부분의 조직에서는 최종 사용자 생산성을 위해 Office 365, Box, Salesforce와 같은 SaaS(Software as a Service) 응용 프로그램에 의존합니다. 지금까지 IT 직원 및 사용자가 tooremember 각 SaaS 응용 프로그램에 대 한 암호 필요 tooindividually 만들고 각 SaaS 응용 프로그램에서 사용자 계정을 업데이트 합니다.

Azure Active Directory 확장 온-프레미스 Active Directory hello 클라우드로 사용자 toouse 사용의 기본 조직 계정 toonot만 로그인 tootheir 도메인에 가입 된 장치 및 회사 리소스 뿐만 아니라 모든 hello 웹 및 SaaS 응용 프로그램 작업에 필요합니다.

따라서 뿐만 아니라 사용자가 없는 toomanage 여러 집합이 사용자 이름 바뀌고는 직원이 자신의 조직 그룹 멤버 및 해당 상태에 따라 암호를 자동으로 프로 비전 하거나 프로 비전 해제 수 액세스 응용 프로그램. Azure Active Directory 보안을 소개 하 고 toocentrally 있습니다 사용할 수 있는 액세스 거 버 넌 스 컨트롤 전체 SaaS 응용 프로그램 사용자의 액세스를 관리 합니다.

Azure AD는 오늘날의 인기 있는 SaaS 응용 프로그램의 손쉬운 통합 toomany 해당 id 및 액세스 관리 기능을 제공 하 고 tooapplications 로그온 toosingle 사용자를 직접 또는 검색 있으며 특정 같은 Office 365 또는 hello Azure AD 액세스 패널 포털에서이 실행 합니다.

hello 통합 hello 아키텍처 hello 다음 4 개의 주요 구성 요소로 이루어져 있습니다.

* Single sign on Azure AD에서 자신의 조직 계정을 기반으로 하는 SaaS 응용 프로그램을 사용 하면 사용자가 tooaccess. Single sign on 사용자 tooauthenticate tooan 응용 프로그램 단일 자신의 조직 계정을 사용 하 여 수립 됩니다.
* 사용자 프로비저닝은 대상 SaaS 응용 프로그램에 사용자 프로비저닝 및 프로비저닝 해제를 가능하게 합니다.  프로 비전 된 계정에 single sign-on을 통해 인증 된 후 사용자 권한을 부여 toobe toouse 응용 프로그램을 수립입니다.
* 단일 지점 SaaS 응용 프로그램 액세스 및 관리를 hello 기능 toodelegate 응용 프로그램 액세스 의사 결정 및 승인 tooanyone hello 조직에 있는 수 있도록 하는 hello Azure 관리 포털의에서 중앙 집중식된 응용 프로그램 액세스 관리
* Azure AD에 사용자 동작 보고 및 모니터링 기능이 통합되었습니다.

## <a name="how-does-single-sign-on-with-azure-active-directory-work"></a>Azure Active Directory에서 Single Sign-On이 작동하는 방식
경우는 사용자 "로그인" tooan 응용 프로그램 들이 본인이 필요한 tooprove 서로 인증 프로세스를 통해 이동 합니다. Single sign on, 없이 일반적으로 이렇게 hello 응용 프로그램에 저장 된 암호를 입력 하 고 hello 사용자가 필요한 tooknow이이 암호입니다.

Azure AD tooapplications의 세 가지 방법으로 toosign를 지원합니다.

* **페더레이션된 Single Sign-on** tooredirect tooAzure는 자신의 암호에 대 한 메시지를 표시 하는 대신 사용자 인증을 위해 AD 응용 프로그램을 사용 하도록 설정 합니다. 이 지원 응용 프로그램에 대 한 지원 프로토콜을 통해 SAML 2.0, OpenID Connect, 또는 WS-페더레이션 같은 및는 single sign-on의 hello 풍부한 모드입니다.
* **암호 기반 Single Sign-On** 을 사용하면 안전한 응용 프로그램 암호 저장소를 사용할 수 있고, 웹 브라우저 확장 또는 모바일 앱에서 저장된 암호로 로그인할 수 있습니다. 이 hello 기존 로그인 프로세스 hello 응용 프로그램에서 제공 활용 하지만 관리자 toomanage hello 암호를 사용 하도록 설정 하며 hello 사용자 tooknow hello 암호가 필요 하지 않습니다.
* **기존 Single Sign-on** 모든 기존 single sign on hello 응용 프로그램에 대해 설정 된 하지만 이러한 응용 프로그램 연결 toobe toohello Office 365 또는 Azure AD 액세스 패널 포털을 사용 하도록 설정 하 고 수도 있도록 tooleverage Azure AD를 사용 하도록 설정 추가 있습니다 hello 응용 프로그램이 시작 되 면 Azure AD의 보고 합니다.

Hello 응용 프로그램에 알리는 hello 응용 프로그램에서 프로 비전 계정 레코드 toohave 해야 사용자가 응용 프로그램으로 인증 되 면 여기서 있습니다 hello 응용 프로그램 내 사용 권한 및 액세스 수준을 합니다. 이 계정 레코드의 프로 비전 hello 발생할 수도 자동으로 또는 hello 사용자가 single sign-on 액세스를 제공 하기 전에 관리자가 수동으로 발생할 수 있습니다.

 이러한 Single Sign-On 모드 및 프로비저닝에 대한 자세한 내용은 아래에서 이어집니다. 

### <a name="federated-single-sign-on"></a>페더레이션된 Single Sign-On
페더레이션된 Single Sign-on tooa 타사 SaaS 응용 프로그램에 Azure AD에서 hello 사용자 계정 정보를 사용 하 여 Azure AD에 의해 자동으로 로그인 하 여 조직 toobe에 로그온 하면 hello 사용자 수 있습니다.

이 시나리오에서는 Azure AD에 이미 로그인 되어 한 타사 SaaS 응용 프로그램에 의해 제어 되는 tooaccess 리소스를 원하는 경우 페더레이션 다시 인증 사용자 toobe hello 필요성을 제거 합니다.

Azure AD는 페더레이션된 single sign-on Ws-federation, SAML 2.0 hello를 지 원하는 응용 프로그램과 함께 지원할 수 있습니다 또는 OpenID connect 프로토콜입니다.

참고 항목: [페더레이션된 Single Sign-On에 대한 인증서 관리](active-directory-sso-certs.md)

### <a name="password-based-single-sign-on"></a>암호 기반 Single Sign-On
암호 기반 single sign on 구성 hello hello 타사 SaaS 응용 프로그램 사용자 계정 정보를 사용 하 여 Azure AD를 통해 tooa 타사 SaaS 응용 프로그램에 자동으로 로그인 하 여 조직 toobe의 hello 사용자 수 있습니다. 이 기능을 사용 하도록 설정 하면 Azure AD는 수집 하 고 hello 사용자 계정 정보와 관련된 암호가 hello 안전 하 게 저장 합니다.

Azure AD는 HTML 기반 로그인 페이지가 있는 모든 클라우드 기반 앱에 대한 암호 기반 Single Sign-On을 지원할 수 있습니다. 사용자 지정 브라우저 플러그 인을 사용 하 여 AAD hello 사용자의 로그인을 통해 안전 하 게 hello 디렉터리에서 hello 사용자 이름 및 hello 암호와 같은 응용 프로그램 자격 증명을 검색 하는 프로세스를 자동화 하 고 hello 응용 프로그램의 로그인 페이지에 이러한 자격 증명 입력 대신 하 여 hello 사용자입니다. 두 가지 사용 사례가 있습니다. 

1. **관리자 자격 증명을 관리** – 관리자 수 만들고 관리 응용 프로그램 자격 증명을 하며 해당 자격 증명 toousers 또는 toohello 응용 프로그램에 액세스 해야 하는 그룹을 할당 합니다. 이러한 경우 hello 최종 사용자 tooknow hello 자격 증명 필요 하지는 않지만 여전히 단순히가 액세스 패널에서 또는 제공 된 링크를 통해에 클릭 하 여 single sign-on 액세스 toohello 응용 프로그램을 향상 합니다. 그러면 최종 사용자가 그에 따라 이러한 않습니다 tooremember 필요 하거나 관리 하지 않으므로 앱 별 암호에 대 한 편의 뿐만 아니라, 관리자에 게 hello 자격 증명의 수명 주기를 관리할 수 있습니다. hello 자격 증명 hello 자동화 된 프로세스; 로그인 시 hello 최종 사용자 로부터 난독 처리 하지만 기술적으로 hello 사용자 웹 디버깅 도구 및 사용자가 사용 하 여 검색할 수 있으며 관리자가 수행 해야 동일한 보안 정책을 마치 hello 자격 증명 hello hello 사용자가 직접 표시 되었습니다. 관리자가 제공한 자격 증명은 소셜 미디어 또는 문서 공유 응용 프로그램과 같이 많은 사용자 간에 공유되는 계정 액세스를 제공할 때 매우 유용합니다.
2. **사용자 자격 증명을 관리** – 관리자가 응용 프로그램 tooend 사용자 또는 그룹을 할당할 수 있으며 hello 최종 사용자가 tooenter hello 응용 프로그램 hello에 대 한 액세스 패널에서 처음으로 액세스할 때 직접 자신의 자격 증명을 허용 합니다. 이렇게 하면 최종 사용자에 게 그에 따라 필요 하지 않은 toocontinually hello 응용 프로그램에 액세스할 때마다 hello 앱 별 암호를 입력에 대 한 편의 위해를 만들어집니다. 이 사용 사례를 그에 따라 관리자에 게 설정할 수 hello 응용 프로그램에 대 한 새 자격 증명 미래 날짜에 hello 최종 사용자의 hello 앱 액세스 환경을 변경 하지 않고 hello 자격 증명의 단계별 실행 돌 tooadministrative 관리로 사용할 수도 있습니다.

두 경우 모두 자격 증명 hello 디렉터리에 암호화 된 상태로 저장 되 고 자동화 된 hello 로그인 프로세스 중만 HTTPS를 통해 전달 됩니다. Azure AD는 암호 기반 Single Sign-On을 사용하여, 페더레이션 프로토콜을 지원할 수 없는 앱을 위한 편리한 ID 액세스 관리 솔루션을 제공합니다. 

암호 기반 SSO는 브라우저 확장 toosecurely hello 응용 프로그램 및 사용자 관련 정보를 검색할 Azure AD에서에 의존 하며 toohello 서비스를 적용 합니다. Azure AD에서 지원하는 대부분의 타사 SaaS 응용 프로그램은 이 기능을 지원합니다.

암호 기반 SSO에 대 한 hello 최종 사용자의 브라우저 될 수 있습니다.

* Internet Explorer 8, 9, 10, 11 - Windows 7 이상( [IE 확장 배포 가이드](active-directory-saas-ie-group-policy.md)참조)
* Chrome - Windows 7 이상 및 Mac OS X 이상
* Firefox 26.0 이상 - Windows XP SP2 이상 및 Mac OS X 10.6 이상

**참고:** hello 암호 기반 SSO 확장을 사용할 수 있는 Windows 10의 Edge에 대 한 브라우저 확장 될 지에 대해 지원 되는 경우.

### <a name="existing-single-sign-on"></a>기존 Single Sign-On
Single sign on 응용 프로그램을 구성할 때 hello Azure 관리 포털의 "기존 Single Sign-on" 세 번째 옵션을 제공 합니다. 이 옵션 하 hello 관리자 toocreate 링크 tooan 응용 프로그램을 허용 하 고 선택한 사용자에 대 한 hello 액세스 패널에 배치 됩니다.

예를 들어 응용 프로그램을 Active Directory Federation Services 2.0을 사용 하 여 tooauthenticate 사용자가 구성을 있으면는 관리자는 hello 액세스 패널에 hello "기존 Single Sign-on" 옵션 toocreate 링크 tooit을 사용할 수 있습니다. 사용자가 hello 링크에 액세스 하면 Active Directory Federation Services 2.0 또는 기존의 single sign on 솔루션 hello 응용 프로그램에서 제공 되를 사용 하 여 인증 됩니다.

### <a name="user-provisioning"></a>사용자 프로비저닝
Select 응용 프로그램에 대 한 Azure AD에 자동된 사용자 프로 비전 및의 타사 SaaS 응용 프로그램에서 Azure 관리 포털, Windows Server Active Directory 또는 Azure AD id 정보를 사용 하 여 hello 내에서 계정 프로 비전 해제 수 있습니다. 이러한 응용 프로그램에 대 한 Azure AD에서 사용자 권한을 제공 하는 경우 계정은 수 자동으로 만들어집니다 (프로 비전 할) hello 대상 SaaS 응용 프로그램입니다.

에서 사용자가 삭제 되거나 사용자 정보가 변경 Azure AD에서 이러한 변경 내용은 hello SaaS 응용 프로그램에에서도 반영 됩니다. 즉, 자동화 된 id 수명 주기 관리 구성 관리자 toocontrol 있으며 특정 자동 프로 비전 및 SaaS 응용 프로그램에서 프로 비전 해제를 제공 합니다. Azure AD에서 이러한 ID 수명 주기 관리의 자동화는 사용자 프로비저닝에 의해 활성화됩니다. 

toolearn 더 참조 [자동 사용자 프로 비전 및 프로 비전 해제 tooSaaS 응용 프로그램](active-directory-saas-app-provisioning.md)

## <a name="get-started-with-hello-azure-ad-application-gallery"></a>Hello Azure AD 응용 프로그램 갤러리 시작
준비 tooget 시작 합니까? toodeploy single sign on Azure AD 간의 다음이 지침을 따르는 조직을 사용 하는 SaaS 응용 프로그램 및입니다.

### <a name="using-hello-azure-ad-application-gallery"></a>Hello Azure AD 응용 프로그램 갤러리를 사용 하 여
hello [Azure Active Directory 응용 프로그램 갤러리](https://azure.microsoft.com/marketplace/active-directory/all/) toosupport single sign on Azure Active Directory와의 형태 알려진 응용 프로그램의 목록을 제공 합니다.

![][1]

다음은 이들이 지원하는 기능별 앱 찾기에 대한 몇 가지 팁입니다.

* Azure AD에 자동으로 프로 비전 하 고 hello에서 모든 "주요" 앱에 대 한 프로 비전 해제 지원 [Azure Active Directory 응용 프로그램 갤러리](https://azure.microsoft.com/marketplace/active-directory/all/)합니다.
* SAML, WS-Federation 또는 OpenID Connect와 같은 프로토콜을 사용하여 페더레이션된 Single Sign-On을 지원하는 페더레이션된 응용 프로그램 목록은 [여기](http://social.technet.microsoft.com/wiki/contents/articles/20235.azure-active-directory-application-gallery-federated-saas-apps.aspx)서 확인할 수 있습니다.

응용 프로그램에 도달 하면, hello 응용 프로그램 갤러리에 제공 된 다음 hello 단계별 지침을 시작할 수 있습니다 및 hello Azure 관리 포털 tooenable에서 single sign on입니다.

### <a name="application-not-in-hello-gallery"></a>Hello 갤러리에 없는 응용 프로그램?
Hello Azure AD 응용 프로그램 갤러리에서 응용 프로그램이 없으면 다음 같은 옵션이 있습니다.

* **사용 하는 목록에 없는 앱 추가** -hello 사용자 지정 범주 hello Azure 관리 포털 tooconnect 조직에서 사용 하는 목록에 없는 응용 프로그램 내에서 응용 프로그램 갤러리 hello에에서 사용 합니다. SAML 2.0을 페더레이션된 앱으로 지원하는 모든 응용 프로그램 또는 HTML 기반 로그인 페이지가 암호 SSO 앱으로 있는 모든 응용 프로그램을 추가할 수 있습니다. 자세한 내용은 [고유한 응용 프로그램 추가](active-directory-saas-custom-apps.md)에 대한 이 문서를 참조하세요.
* **사용자 고유의 응용 프로그램을 개발 하는 추가** hello 응용 프로그램을 개발한 경우-hello 지침 hello Azure AD 개발자 설명서 tooimplement 페더레이션 single sign on에 따라 직접 또는 Azure AD graph API를 환영 프로 비전을 사용 합니다. 이러한 응용 프로그램은 Azure AD Graph API를 사용할 수 있습니다. 자세한 내용은 다음 리소스를 참조하세요. 
  
  * [Azure AD의 인증 시나리오](active-directory-authentication-scenarios.md)
  * [https://github.com/AzureADSamples/WebApp-MultiTenant-OpenIdConnect-DotNet](https://github.com/AzureADSamples/WebApp-MultiTenant-OpenIdConnect-DotNet)
  * [https://github.com/AzureADSamples/WebApp-WebAPI-MultiTenant-OpenIdConnect-DotNet](https://github.com/AzureADSamples/WebApp-WebAPI-MultiTenant-OpenIdConnect-DotNet)
  * [https://github.com/AzureADSamples/NativeClient-WebAPI-MultiTenant-WindowsStore](https://github.com/AzureADSamples/NativeClient-WebAPI-MultiTenant-WindowsStore)
* **응용 프로그램 통합을 요청** -를 사용 하 여 필요한 hello 응용 프로그램에 대 한 지원을 요청 hello [Azure AD 피드백 포럼](https://feedback.azure.com/forums/169401-azure-active-directory/)합니다.

### <a name="using-hello-azure-management-portal"></a>Hello Azure 관리 포털을 사용 하 여
Azure 관리 포털 tooconfigure hello 응용 프로그램에 single sign-on hello에 hello Active Directory 확장을 사용할 수 있습니다. 첫 번째 단계로, tooselect hello hello 포털에서 Active Directory 섹션에서에서 디렉터리를 필요합니다.

![][2]

toomanage 타사 SaaS 응용 프로그램 hello 선택 된 디렉터리의 응용 프로그램 탭 hello 전환할 수 있습니다. 응용 프로그램 탭에서는 관리자가 다음을 수행할 수 있습니다. 

* 앱을 개발 하는 hello Azure AD 갤러리에서 새 응용 프로그램 추가
* 통합된 응용 프로그램 삭제
* 이미 통합 된 hello 응용 프로그램 관리

타사 SaaS 응용 프로그램에 대한 일반적인 관리 작업은 다음과 같습니다.

* Single sign on 암호 SSO를 사용 하 여 또는 페더레이션 SSO hello 대상 SaaS에 대해 사용할 수 있는 경우 Azure ad를 사용 하도록 설정
* 필요에 따라 사용자 프로비저닝 및 프로비저닝 해제에 대해 사용자 프로비저닝을 사용하도록 설정(ID 수명 주기 관리)
* 응용 프로그램의 사용자 프로비저닝이 활성화 되어 있는 경우 액세스할 수 있는 사용자 선택 하면 toothat 응용 프로그램

페더레이션된 single sign-on 지원 갤러리 앱의 경우 구성 보통 해야 인증서, 메타 데이터 toocreate 등 추가 구성 설정을 tooprovide hello 타사 앱과 Azure AD 간의 페더레이션된 트러스트 합니다. hello 구성 마법사 hello 세부 정보를 안내 하 고 쉽게 액세스할 수 있도록 toohello SaaS 응용 프로그램 관련 데이터를 사용 하 고 지침을 제공 합니다.

자동 사용자 프로 비전을 지 원하는 갤러리 앱, 그러려면 있습니다 toogive Azure AD 권한 toomanage hello SaaS 응용 프로그램에서 계정을 합니다. 여기에 최소한 tooprovide toohello 대상 응용 프로그램에 대해 인증할 때 Azure AD 자격 증명 사용 해야 할 수 있습니다. 추가 구성 설정을 제공 toobe 필요한 여부를 hello 응용 프로그램의 hello 요구 사항에 따라 달라 집니다.

## <a name="deploying-azure-ad-integrated-applications-toousers"></a>응용 프로그램 toousers를 통합 Azure AD를 배포 합니다.
Azure AD에서는 사용자 지정 가능한 여러 가지 방법으로 toodeploy 응용 프로그램 tooend-조직의 사용자가 제공합니다.

* Azure AD 액세스 패널
* Office 365 응용 프로그램 실행 프로그램
* 직접 로그온 toofederated 앱
* 암호 기반 딥 링크 toofederated, 또는 기존 앱

조직에서 toodeploy를 선택 메서드는 판단 합니다.

### <a name="azure-ad-access-panel"></a>Azure AD 액세스 패널
액세스 패널에서 https://myapps.microsoft.com hello tooview Azure Active Directory에에서 조직 계정이 있는 최종 사용자를 허용 하는 웹 기반 포털 이며 시작 클라우드 기반 응용 프로그램 toowhich 있다가 hello Azure AD에 의해 액세스 부여 관리자가입니다. 최종 사용자 인 경우 [Azure Active Directory Premium](https://azure.microsoft.com/pricing/details/active-directory/), hello 액세스 패널을 통해 셀프 서비스 그룹 관리 기능을 사용할 수 있습니다.

![][3]

액세스 패널 hello는 hello Azure 관리 포털에서에서 분리 되 고 Azure 구독 또는 Office 365 구독 사용자 toohave 필요 하지 않습니다.

Hello Azure AD 액세스 패널에 대 한 자세한 내용은 참조 hello [toohello 액세스 패널 소개](active-directory-saas-access-panel-introduction.md)합니다.

### <a name="office-365-application-launcher"></a>Office 365 응용 프로그램 실행 프로그램
Office 365 배포의 조직에서 Azure AD 통해 toousers 할당 된 응용 프로그램 https://portal.office.com/myapps hello Office 365 포털에도 표시 됩니다. 따라서 쉽고 편리 하 게 사용자에 대 한 조직 toolaunch에 앱 toouse 두 번째 포털 필요 없이 한 hello Office 365를 사용 하 여 조직에 대 한 솔루션을 시작 하는 응용 프로그램 좋습니다.

![][4]

Hello Office 365 응용 프로그램 시작 관리자에 대 한 자세한 내용은 참조 [hello Office 365 앱 시작 관리자에 표시 앱](https://msdn.microsoft.com/office/office365/howto/connect-your-app-to-o365-app-launcher)합니다.

### <a name="direct-sign-on-toofederated-apps"></a>직접 로그온 toofederated 앱
연결도 hello 응용 프로그램에서 사용자가 toostart hello 수 있는 기능이 지원 하 고 로그 Azure AD를 통해 자동 리디렉션 하거나에서 링크 toosign에서을 클릭 하 여 하는 가장 페더레이션된 응용 프로그램에 SAML 2.0, Ws-federation, OpenID 지원. 서비스 공급자로도 알려져-로그온을 시작 하 고 가장 페더레이션된 응용 프로그램 hello Azure AD 응용 프로그램 갤러리에서이 지원 합니다. (-에 대 한 hello Azure 관리 포털의 hello 응용 프로그램의 single sign on 구성 마법사에서 연결 된 hello 설명서를 참조 하는 중 세부 정보)입니다.

![][5]

### <a name="direct-sign-on-links-for-federated-password-based-or-existing-apps"></a>페더레이션된 앱, 암호로 보호된 앱 또는 기존 앱에 대한 직접 로그온 링크
또한 azure AD 암호 기반 single sign on, 기존 single sign-on 및 페더레이션된 single sign-on의 모든 형태 지 원하는 직접 single sign on 링크 tooindividual 응용 프로그램을 지원 합니다.

이러한 링크는 hello Azure 통해 사용자를 전송 하는 구체적으로 조작 Url AD 로그인 hello 사용자 필요 없이 특정 응용 프로그램에 대 한 프로세스 hello Azure AD 액세스 패널 또는 Office 365에서 시작 합니다. Hello 화면 아래에 나와 있는 것 처럼 이러한 Single Sign-on Url hello hello Azure 관리 포털의 Active Directory 섹션에서에서 미리 통합 된 응용 프로그램의 hello 대시보드 탭 아래에서 찾을 수 있습니다.

![][6]

이러한 링크 복사 될 수 있습니다 및 로그인에 tooprovide 링크 toohello 선택한 응용 프로그램을 원하는 위치에 붙여 넣은 합니다. 이 링크는 전자 메일 또는 사용자 응용 프로그램 액세스에 대해 설정한 사용자 지정 웹 기반 포털에 있을 수 있습니다. 다음은 Twitter에 대한 Azure AD Single Sign-On URL의 예제입니다.

`https://myapps.microsoft.com/signin/Twitter/230848d52c8745d4b05a60d29a40fced`

Hello 액세스 패널에 대 한 유사한 tooorganization 별 Url을 hello myapps.microsoft.com 도메인 후 디렉터리에 대 한 hello 활성 상태 인지 확인 된 도메인 중 하나를 추가 하 여이 URL를 추가로 지정할 수 있습니다. 이렇게 하면 hello 사용자 tooenter가 사용자 ID를 먼저 필요 없이 hello 로그인 페이지에서 즉시 로드 조직 브랜딩:

`https://myapps.microsoft.com/contosobuild.com/signin/Twitter/230848d52c8745d4b05a60d29a40fced`

이러한 응용 프로그램 관련 링크 중 하나에서 권한이 부여 된 사용자가 먼저 자신의 조직 로그인 페이지 (에 이미 로그인 하지 않고는 가정)를 참조 하며는 hello 액세스 패널에서 먼저 중지 하지 않고 리디렉션된 tootheir 앱으로 로그인 합니다. Hello 사용자 tooaccess hello hello 암호 기반 single sign 브라우저 확장이 같은 응용 프로그램 필수 구성 요소를 누락 된 경우 hello 링크 hello 사용자 tooinstall hello 누락 된 확장을 라는 됩니다. 또한 hello 링크 URL은 hello single sign on 구성 hello 응용 프로그램에 대 한 변경 되 면 일정 합니다.

이러한 링크 hello를 사용 하 여 hello와 같은 액세스 제어 메커니즘 패널 및 Office 365에 액세스 하 고 toosuccessfully 인증만 해당 사용자 또는 그룹 hello Azure 관리 포털에서 toohello 응용 프로그램에 지정 된 수 있습니다. 그러나 모든 사용자에 게 권한이 부여 되어 액세스를 부여 되지 않은 하 고는 링크 tooload hello 액세스 패널 tooview 사용할 수 있는 응용 프로그램 액세스를 권한이 부여 됩니다 설명 하는 메시지가 나타납니다.

## <a name="related-articles"></a>관련 문서
* [Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스](active-directory-apps-index.md)
* [방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와](active-directory-saas-tutorial-list.md)
* [클라우드 앱 검색을 사용하여 허용되지 않은 클라우드 응용 프로그램 찾기](active-directory-cloudappdiscovery-whatis.md)
* [소개 tooManaging 액세스 tooApps](active-directory-managing-access-to-apps.md)
* [Azure AD에서 외부 ID 관리 기능 비교](active-directory-b2b-compare-external-identities.md)

<!--Image references-->
[1]: ./media/active-directory-appssoaccess-whatis/onlineappgallery.png
[2]: ./media/active-directory-appssoaccess-whatis/azuremgmtportal.png
[3]: ./media/active-directory-appssoaccess-whatis/accesspanel.png
[4]: ./media/active-directory-appssoaccess-whatis/officeapphub.png
[5]: ./media/active-directory-appssoaccess-whatis/workdaymobile.png
[6]: ./media/active-directory-appssoaccess-whatis/deeplink.png
