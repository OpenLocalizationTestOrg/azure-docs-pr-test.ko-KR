---
title: "내 응용 프로그램 목록에서 응용 프로그램 aaaUnexpected | Microsoft Docs"
description: "어떻게 toosee 테 넌 트의 모든 응용 프로그램이 고 응용 프로그램이 엔터프라이즈 응용 프로그램에서 모든 응용 프로그램 목록에 나타나는 방식을 이해"
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
ms.openlocfilehash: 2f974046b655bc36a05f002c56511a8a988cd01c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="unexpected-application-in-my-applications-list"></a>내 응용 프로그램 목록에 예기치 않은 응용 프로그램

이 문서가 도움이 응용 프로그램에 표시 되는 방식을 toounderstand 프로그램 **모든 응용 프로그램** 목록에서 **엔터프라이즈 응용 프로그램**합니다. 

## <a name="how-toosee-all-applications-in-your-tenant"></a>어떻게 toosee 테 넌 트의 모든 응용 프로그램

toosee 모든 hello 테 넌 트에 응용 프로그램, toouse hello 필요한 **필터** tooshow 제어 **모든 응용 프로그램** hello에서 **모든 응용 프로그램** 목록입니다. toodo 다음,이 따라 hello 단계:

1.  열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**

2.  열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.

3.  에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.

4.  클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.

5.  클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.

6.  hello 사용 하 여 hello 클릭 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록**합니다.

7.  Hello에 **필터** 블레이드, 집합 hello **표시** 옵션**모든 응용 프로그램입니다.**

## <a name="why-does-a-specific-application-appear-in-my-all-applications-list"></a>내 모든 응용 프로그램 목록에 특정 응용 프로그램이 나타나는 이유는 무엇입니까?

너무 필터링 할 때**모든 응용 프로그램**, hello **모든 응용 프로그램** **목록** 테 넌 트의 모든 서비스 사용자 개체를 보여 줍니다. 서비스 주체 개체는 다양한 방법으로 이 목록에 나타날 수 있습니다.

1.  Hello 응용 프로그램 갤러리에서 모든 응용 프로그램을 추가 하는 경우 포함 하 여:

   1. **Azure AD 갤러리 응용 프로그램** – Single Sign-On에 대해 Azure AD와 사전 통합된 응용 프로그램입니다.

   2. **응용 프로그램 프록시 응용 프로그램** – tooprovide 보안 single sign-on tooexternally 원하는 온-프레미스 환경에서 실행 중인 응용 프로그램입니다.

   3. **사용자 지정 응용 프로그램 개발** – 조직에서 toodevelop 하지 않고자 한다면 응용 프로그램에 Azure AD 응용 프로그램 개발 플랫폼 hello 하지만 아직 존재 하지 않을 수 있습니다.

   4. **비 갤러리 응용 프로그램** – 사용자의 응용 프로그램을 가져옵니다! 원하는 모든 웹 링크 또는 사용자 이름 및 암호 필드를 렌더링 하는 응용 프로그램에는 SAML 또는 OpenID Connect 프로토콜을 지원 또는 Azure ad에서 single sign-on toointegrate 복원할 SCIM를 지원 합니다.

2.  Azure Active Directory와 통합된 타<sup>사</sup> 응용 프로그램에 등록하거나 로그인하는 경우. 한 가지 예로 [Smartsheet](https://app.smartsheet.com/b/home) 또는 [DocuSign](https://www.docusign.net/member/MemberLogin.aspx)이 있습니다.

3.  에 등록, 라이선스 tooa 사용자 또는 그룹 tooa 첫 번째 파티 응용을 추가 하거나 때와 같은 [Microsoft Office 365](http://products.office.com/)합니다.

4.  Hello를 사용 하 여 개발 된 응용 프로그램을 만들어 새 응용 프로그램 등록을 추가 하면 [응용 프로그램 레지스트리](https://docs.microsoft.com/azure/active-directory/active-directory-app-registration)합니다.

5.  Hello를 사용 하 여 개발 된 응용 프로그램을 만들어 새 응용 프로그램 등록을 추가 하면 [V2.0 응용 프로그램 등록 포털](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-app-registration#visit-the-microsoft-app-registration-portal)합니다.

6.  Visual Studio의 [ASP.net 인증 방법](http://www.asp.net/visual-studio/overview/2013/creating-web-projects-in-visual-studio#orgauthoptions) 또는 [연결된 서비스](http://blogs.msdn.com/b/visualstudio/archive/2014/11/19/connecting-to-cloud-services.aspx)를 사용하여 개발 중인 응용 프로그램을 추가하는 경우.

7.  Hello를 사용 하 여 서비스 사용자 개체를 만들 때 [Azure AD PowerShell 모듈이](/powershell/azure/install-adv2?view=azureadps-2.0)합니다.

8.  때 있습니다 [tooan 응용 프로그램 동의](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) 테 넌 트의 관리자 toouse 데이터로 합니다.

9.  경우는 [사용자가 tooan 응용 프로그램을 승인](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) toouse 데이터 테 넌 트에 있습니다.

10. 테넌트에 데이터를 저장하는 특정 서비스를 활성화하는 경우. 이 한 가지 예로 모델링 되는 암호 재설정 서비스 보안 주체 toostore로 암호 재설정 정책을 안전 하 게 합니다.

tooget 앱 tooyour 디렉터리를 추가 하는 방법을 대 한 자세한 내용은 읽기 [응용 프로그램을 AD tooAzure 추가 방법과 이유](https://docs.microsoft.com/azure/active-directory/develop/active-directory-how-applications-are-added)합니다.

## <a name="i-want-tooremove-a-specific-users-or-groups-assignment-tooan-application"></a>특정 사용자 또는 그룹의 할당 tooan 응용 프로그램 tooremove 원합니다

hello에 나열 된 hello 단계를 수행 하는 사용자 또는 그룹 할당 tooan 응용, tooremove [에서 Azure Active Directory에서 엔터프라이즈 응용 프로그램에서 사용자 또는 그룹 할당을 제거할](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) 문서.

## <a name="i-want-toodisable-all-access-tooan-application-for-every-user"></a>모든 사용자에 대 한 모든 액세스 tooan 응용 프로그램이 toodisable 원합니다

toodisable 모든 사용자 로그인 tooan 응용 프로그램 hello에 나열 된 hello 단계를 수행 [Azure Active Directory에서 엔터프라이즈 응용 프로그램에 대 한 사용자 로그인을 사용 하지 않도록 설정](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) 문서.

## <a name="i-want-toodelete-an-application-entirely"></a>응용 프로그램 toodelete를 완전히 낮음

너무**응용 프로그램을 삭제할**, 아래 hello 지침에 따라:

1.  열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**

2.  열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.

3.  에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.

4.  클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.

5.  클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.

  * 여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**

6.  원하는 toodelete hello 응용 프로그램을 선택 합니다.

7.  Hello 응용 프로그램 로드 되 면 클릭 **삭제** hello 최고 응용 프로그램에서 아이콘 **개요** 블레이드입니다.

## <a name="i-want-toodisable-all-future-user-consent-operations-tooany-application"></a>모든 향후 사용자 동의 작업 tooany 응용 프로그램 toodisable 원합니다

전체 디렉터리 승인 tooany 응용 프로그램에서 최종 사용자가 방지에 대 한 사용자 동의 사용 하지 않도록 설정 합니다. 관리자는 여전히 사용자의 동작에 동의할 수 있습니다. 응용 프로그램에 대해 자세히 toolearn 동의 및 이유 있거나 하지 않을 toodo이,이 읽기 [이해 사용자 및 관리자 동의](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent)합니다.

너무**전체 디렉터리의 모든 이후 사용자 동의 작업을 사용 하지 않도록 설정**, 아래 hello 지침에 따라:

1.  열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**

2.  열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.

3.  에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.

4.  클릭 **사용자 및 그룹** hello 탐색 메뉴에 있습니다.

5.  **사용자 설정**을 클릭합니다.

6.  Hello 설정 하 여 모든 이후 사용자 동의 작업을 사용 하지 않도록 설정 **사용자가 앱 tooaccess 데이터 허용 수** 너무 설정/해제**아니요** hello를 클릭 하 고 **저장** 단추입니다.

## <a name="next-steps"></a>다음 단계
[Azure Active Directory로 응용 프로그램 관리](active-directory-enable-sso-scenario.md)
