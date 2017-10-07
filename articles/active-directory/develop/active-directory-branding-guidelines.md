---
title: "응용 프로그램에 대 한 지침이 aaaBranding | Microsoft Docs"
description: "포괄적인은 toodeveloper 지향 리소스를 Azure Active Directory에 대 한 가이드"
services: active-directory
documentationcenter: dev-center-name
author: skwan
manager: mbaldwin
editor: 
ms.assetid: 72f4e464-1352-4a49-a18f-c37f58e7d5c4
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: skwan
ms.custom: aaddev
ms.openlocfilehash: e43f884c736a0dcb2e6e51293962ef1e2636ad70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="branding-guidelines-for-applications"></a>응용 프로그램에 대한 브랜딩 지침
이 항목에서는 hello 브랜딩 Azure Active Directory (Azure AD)와 응용 프로그램을 개발할 때 사용 해야 하는 지침을 설명 합니다. 이러한 지침은 원할 때 toouse 직장 또는 학교 계정, Azure AD에서 관리 되는 또는 개인 계정 등록 및 로그인 tooyour 응용 프로그램에 대 한 고객에 게 지시 하는 데 도움이 됩니다.

## <a name="personal-accounts-vs-work-or-school-accounts-from-microsoft"></a>Microsoft의 개인 계정과 회사 또는 학교 계정
Microsoft는 두 종류의 사용자 계정을 관리합니다.

* **개인 계정** (이전의 Windows Live ID). 이러한 계정 간의 hello 관계를 나타내기 *개별* 사용자와 Microsoft, 및는 tooaccess 소비자 장치 및 Microsoft 서비스를에서 사용 합니다. 이 계정은 개인적인 용도를 위한 것입니다.
* **회사 또는 학교 계정.** 이 계정은 Azure Active Directory를 사용하는 조직을 대신하여 Microsoft에서 관리합니다. 이러한 계정은 tooOffice 365 및 다른 비즈니스 서비스를 Microsoft에 사용 되는 toosign 됩니다.

회사 또는 학교 계정을 일반적으로 Microsoft는 조직 (회사, 학교, 정부 기관)에서 tooend 사용자 (직원, 학생, 연방 직원)을 할당 합니다. 이러한 계정 중 하나에서 Azure AD hello 플랫폼 또는 Windows Server Active Directory 등의 온-프레미스 디렉터리에서 동기화 된 tooAzure AD hello 클라우드에서 직접 마스터 됩니다. Microsoft는 hello *보유 하 고* hello 작업 또는 학교 계정 하지만 hello 계정을 소유 하 고 hello 조직에 의해 제어 됩니다.

## <a name="referring-tooazure-ad-accounts-in-your-application"></a>응용 프로그램에서 참조 tooAzure AD 계정
Microsoft 노출 되는 것 최종 사용자에 게 toohello Azure hello Active Directory 브랜드 이름은 및 둘 다 표시 해서는 안 됩니다.

* 사용자가 로그인 hello 조직 이름 및 가능한 한 로고를 사용 해야 합니다. 이것이 "조직"과 같은 일반적인 용어를 사용하는 것보다 좋습니다.
* Tootheir 계정으로 참조 해야 사용자가 로그인 하지 않은 경우 "작업 또는 학교 계정" 및 사용 하 여 hello Microsoft 로고 tooconvey 이러한 계정은 Microsoft에서 관리 됩니다. 사용자에게 혼동을 줄 수 있는 "엔터프라이즈 계정", "비즈니스 계정" 또는 "회사 계정"과 같은 용어는 사용하지 마세요.

## <a name="user-account-pictogram"></a>사용자 계정 픽토그램
이 지침의 이전 버전에서는 "파란색 배지" 픽토그램을 사용하도록 권장했습니다. 사용자와 개발자의 의견에 따라 이제 hello 사용을 좋습니다 hello Microsoft 로고 대신 합니다. 이렇게 하면 사용자가 이해 Office 365 또는 기타 Microsoft 비즈니스 서비스 toosign tooyour 응용 프로그램에서 사용 하는 hello 계정을 다시 사용할 수 있습니다.

## <a name="signing-up-and-signing-in-with-azure-ad"></a>Azure AD를 사용한 등록 및 로그인
앱 등록 및 로그인에 대 한 별도 경로 표시 될 수 있습니다 및 다음 섹션 hello 두 시나리오 모두에 대 한 시각적 지침을 제공 합니다.

**응용 프로그램 (예: 무료 tootrial 또는 freemium 모델) 최종 사용자 등록을 지 원하는 경우**: 표시할 수 있습니다는 **로그인** tooaccess 사용자가 회사 계정 또는 개인 계정으로 사용 하 여 앱을 허용 하는 단추입니다. Azure AD는 앱에 액세스 하는 처음으로 동의 프롬프트 hello를 표시 됩니다.

**관리자만 동의할 수 있는 권한을 요구하는 앱 또는 조직 라이선스가 필요한 앱의 경우**: 관리 취득과 사용자 로그인을 분리해야 합니다. hello **"이이 앱을 다운로드" 단추** 는에서 admins toosign 리디렉션 후 조직에서 사용자를 대신해 서 toogrant 동의 요청 합니다. 이 최종 사용자가 동의 프롬프트 tooyour 응용 프로그램을 표시 하지 않는 추가적인된 이점을 hello 했습니다.

## <a name="visual-guidance-for-app-acquisition"></a>앱 구입에 대한 시각적 지침
"Hello 응용 프로그램 가져오기" 링크가 리디렉션하여 hello 사용자 toohello Azure AD 액세스 권한 부여 (권한 부여) 페이지, tooallow 조직의 관리자 tooauthorize 앱 toohave Microsoft에서 호스팅하는 tootheir 조직 데이터에 액세스 합니다. Toorequest 액세스가 hello에 대해서는 설명에 대 한 내용은 [Azure Active Directory와 응용 프로그램 통합](active-directory-integrating-applications.md) 문서.

Tooyour 응용 프로그램 관리자가 동의 후 tooadd 선택할 수 있는 것 tootheir 사용자의 Office 365 앱 시작 관리자 환경을 (및 hello waffle에서 액세스할 수 있는 [https://portal.office.com/myapps](https://portal.office.com/myapps)). 이 기능은 tooadvertise을 원하는 경우 "이 앱 tooyour 조직 추가" 및 다음과 같은 단추 표시와 같은 용어를 사용할 수 있습니다.

![응용 프로그램 종류 및 시나리오](./media/active-directory-branding-guidelines/add-to-my-org.png)

그러나 단추에 의존하는 대신 설명 텍스트를 작성하는 것이 좋습니다. 예:

> *이미 Office 365 또는 Microsoft의 다른 비즈니스 서비스를 사용 하는 경우 단순히 < your_app_name > 액세스 tooyour 조직 데이터를 부여할 수 있습니다. 기존 작업 계정 사용 하면 사용자가 tooaccess < your_app_name > 수 있습니다.*
> 
> 

## <a name="visual-guidance-for-sign-in"></a>로그인에 대한 시각적 지침
앱은 사용자 toohello 로그인에 끝점 toohello 프로토콜 toointegrate를 사용 하 여 Azure AD에 해당 하는 리디렉션하는 단추에 대 한 기호를 표시 되어야 합니다. hello 섹션 뒤 해당 단추의 모양 내용에 대해 자세히 설명 합니다.

### <a name="pictogram-and-sign-in-with-microsoft"></a>픽토그램 및 “Microsoft 로그인”
Azure AD에 앱이 지원할 수 기타 id 공급자를 고유 하 게 나타내는 hello Microsoft 로고 및 hello "Sign in with Microsoft" 조건을 hello 연결의 것입니다. "Sign in with Microsoft"에 대 한 충분 한 공간이 없으면 확인 tooshorten 것 너무 "로그인" 됩니다.

![응용 프로그램 종류 및 시나리오](./media/active-directory-branding-guidelines/sign-in-with-microsoft-light.png)

![응용 프로그램 종류 및 시나리오](./media/active-directory-branding-guidelines/sign-in-light.png)

또한 hello 단추에 대 한 어둡게 색 구성표를 사용할 수 있습니다.

![응용 프로그램 종류 및 시나리오](./media/active-directory-branding-guidelines/sign-in-with-microsoft-dark.png)

![응용 프로그램 종류 및 시나리오](./media/active-directory-branding-guidelines/sign-in-dark.png)

## <a name="branding-dos-and-donts"></a>브랜딩 관련 할 일과 하지 말아야 할 일
**수행** hello "Sign in with Microsoft" 단추 tooprovide 추가 설명 toohelp 최종 사용자와 함께에서 "업무 또는 학교 계정"을 사용 하 여 인식 여부를 사용할 수 있습니다. **권장 안 함** "엔터프라이즈 계정", "비즈니스 계정" 또는 "회사 계정"과 같은 다른 용어는 사용하지 않습니다.

**권장 안 함** “Office 365 ID” 또는 “Azure ID”를 사용하지 않습니다. Office 365 인증에 대 한 Azure AD를 사용 하지 않는 Microsoft에서 제공 하는 소비자의 hello 이름 이기도 합니다.

**안 함** hello Microsoft 로고를 변경 합니다.

**안 함** toohello 또는 Azure Active Directory 브랜드를 최종 사용자가 노출 합니다. 그러나 해도 됩니다 toouse 이러한 단어와 함께 개발자, IT 전문가 및 관리자입니다.

## <a name="navigation-dos-and-donts"></a>탐색 관련 할 일과 하지 말아야 할 일
**수행** 아웃 사용자 toosign는 방법을 제공 하 고 tooanother 사용자 계정 전환 합니다. 대부분의 사람들은 Microsoft/Facebook/Google/Twitter의 단일 개인 계정을 가지고 있지만, 사람들은 종종 여러 조직과 연결됩니다. 여러 명의 로그인한 사용자에 대한 지원이 곧 제공됩니다.

