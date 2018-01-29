---
title: "Azure Active Directory에서 액세스 패널이란? | Microsoft Docs"
description: "다양한 액세스 패널(웹 브라우저, Android 앱, iPhone 및 iPad 앱)을 사용하여 SaaS 앱에 액세스하는 방법을 알아봅니다."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: mtillman
ms.assetid: c0252d01-7e6e-4f79-a70e-600479577dfd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2018
ms.author: markvi
ms.reviewer: asteen
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6b5c139766af9e166b12e8833c2ced8be08e743a
ms.sourcegitcommit: 9292e15fc80cc9df3e62731bafdcb0bb98c256e1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/10/2018
---
# <a name="what-is-the-access-panel"></a>액세스 패널이란?

액세스 패널은 웹 기반 포털입니다. Azure Active Directory에 회사 또는 학교 계정이 있는 사용자는 Azure AD 관리자를 통해 액세스 권한을 부여 받은 클라우드 기반 응용 프로그램을 보고 시작할 수 있습니다. 또한 액세스 패널을 통해 셀프 서비스 그룹 및 앱 관리 기능을 사용할 수도 있습니다.

액세스 패널은 Azure Portal과 별개이며, 사용자에게 Azure 구독을 요구하지 않습니다.

![액세스 패널][1]

액세스 패널을 사용하면 다음 기능을 포함한 프로필 설정 중 일부를 편집할 수 있습니다.

- 회사 또는 학교 계정과 관련된 암호 변경

- 암호 재설정 편집

- 다단계 인증과 관련된 연락처 및 기본 설정 편집(관리자가 사용해야 하는 계정의 경우)

- 사용자 ID, 대체 전자 메일, 모바일 및 사무실 전화 번호 및 장치와 같은 계정 세부 정보 보기

- Azure AD 관리자가 액세스 권한을 부여한 클라우드 기반 응용 프로그램을 보고 시작합니다. 사용자 관점의 액세스 패널에 대한 자세한 내용은 액세스 패널 사용을 참조하세요. 

- 그룹을 셀프 관리합니다. 보다 구체적으로, 관리자는 Azure AD에서 보안 그룹을 만들고 관리할 수 있으며, 보안 그룹 멤버 자격을 요청할 수 있습니다. 자세한 내용은 [Azure AD의 사용자를 위한 셀프 서비스 그룹 관리](active-directory-accessmanagement-self-service-group-management.md)와 [그룹 관리](active-directory-manage-groups.md)를 참조하세요.




## <a name="accessing-the-access-panel"></a>액세스 패널 액세스

웹 브라우저에서 다음의 URL을 방문하여 액세스 패널에 액세스할 수 있습니다. `http://myapps.microsoft.com`

로그인 페이지에서 사용자 지정 브랜딩을 구성한 경우 URL의 끝에 조직의 도메인을 추가하여 해당 브랜딩을 로드할 수 있습니다. `http://myapps.microsoft.com/<your domain>.com`

이 경우 Azure Portal에서 구성된 모든 활성 또는 확인된 도메인 이름을 사용할 수 있습니다.

![Wingtip Toys 도메인 이름][2]  

Azure AD와 통합된 응용 프로그램에 로그인하는 모든 사용자에게 URL을 배포해야 합니다.

## <a name="authentication"></a>인증

액세스 패널에 도달하려면 Azure AD에서 회사 또는 학교 계정을 통해 인증을 받아야 합니다. Azure AD에서 직접 인증을 받을 수 있습니다. 또는 조직에서 AD FS(Active Directory Federation Services) 또는 다른 기술을 사용하여 페더레이션을 구성한 경우 Windows Server Active Directory에서 인증을 받을 수도 있습니다.

Azure 또는 Office 365에 대한 구독을 가지고 있고 Azure Portal 또는 Office 365 응용 프로그램을 사용하고 있으면, 다시 로그인하지 않고 응용 프로그램의 목록을 볼 수 있습니다. 인증되지 않은 경우 Azure AD 계정에 대한 사용자 이름과 암호를 사용하여 로그인하라는 메시지가 표시됩니다. 조직에서 페더레이션을 구성한 경우 사용자 이름만 입력하면 됩니다.

인증되면 관리자에 의해 디렉터리와 통합된 응용 프로그램과 상호 작용할 수 있습니다. 응용 프로그램을 Azure AD와 통합하는 방법을 보려면 [Azure Active Directory를 사용한 응용 프로그램 액세스 및 Single Sign-On](active-directory-appssoaccess-whatis.md)을 참조하세요.

## <a name="web-browser-requirements"></a>웹 브라우저 요구 사항

액세스 패널에는 최소한 JavaScript를 지원하고 CSS를 사용하도록 설정된 브라우저가 필요합니다. 사용자가 암호 기반 SSO(Single Sign-On)를 통해 응용 프로그램에 로그인하려면 사용자의 브라우저에 액세스 패널 확장이 설치되어 있어야 합니다. 암호 기반 SSO에 구성된 응용 프로그램을 선택할 때 확장이 자동으로 다운로드됩니다.

액세스 패널 확장은 현재 다음과 같은 경우 사용할 수 있습니다.
-   Windows 10 Anniversary Edition 이상 Edge 

-   Chrome - Windows 7 이상 및 Mac OS X 이상

-   Firefox 26.0 이상 - Windows XP SP2 이상 및 Mac OS X 10.6 이상

-   Internet Explorer 8, 9, 10, 11 - Windows 7 이상(지원 제한)

## <a name="my-apps-secure-sign-in-extension"></a>내 앱 보안 로그인 확장
확장은 암호 기반 Single Sign-On에 로그인하는 사용자에게 필요합니다. 설치된 사용자가 **시작할 로그인**을 클릭하면 해당 확장에 로그인하여 추가 기능을 활성화할 수도 있습니다. 

- 사용자가 직접 앱의 **로그온 URL**을 방문하여 앱에 로그인할 수합니다. 사용자가 앱의 로그온 URL을 탐색할 때 확장에서는 이를 감지하고 사용자에게 확장에서 로그인하는 옵션을 제공합니다.
- 사용자가 확장의 **빠른 검색** 기능을 사용하여 액세스 패널에서 해당 앱을 시작할 수도 있습니다. 
- 확장은 사용자에게 **최근에 사용함** 섹션 아래에서 시작한 최근 세 개의 응용 프로그램도 표시합니다.

> [!NOTE]
> 추가 기능은 Edge, Chrome 및 Firefox에서만 사용할 수 있습니다.
>
>

https://myapps.microsoft.com이 아닌 다른 앱 URL을 사용하는 경우 다음 단계를 통해 기본 URL을 구성해야 합니다.
1. 확장에 로그인되지 않은 상태에서 확장 아이콘을 **마우스 오른쪽 단추로 클릭**합니다.
2. 메뉴에서 **내 앱 URL 선택**을 클릭합니다.
3. 기본 URL을 **선택**합니다.
4. 확장 아이콘을 클릭합니다.
5. **시작하려면 로그인하세요.**를 선택하여 확장에 로그인합니다.

## <a name="mobile-app-support"></a>모바일 앱 지원

Azure Active Directory 팀은 My Apps 모바일 앱을 게시합니다. 앱을 설치하면 iOS 및 Android 장치의 암호 기반 SSO 응용 프로그램에 로그인할 수 있습니다.

> [!NOTE]
> 플러그 인이나 모바일 앱 없이 모든 장치의 거의 모든 웹 브라우저(Salesforce, Google Apps, Dropbox, Box, Concur, Workday, Office 365 및 기타 70개 이상 포함)에서 Azure AD를 사용하여 페더레이션을 지원하는 응용 프로그램에 로그인할 수 있습니다. 또한 다른 [액세스 패널 환경](https://myapps.microsoft.com/)에서도 My Apps 모바일 앱을 모바일 장치에서 사용할 필요가 없습니다.
>
>

### <a name="my-apps-for-android"></a>Android 용 My Apps

Android용 My Apps는 Android 버전 4.1 이상을 실행하는 모든 Android 장치에서 지원됩니다.  
[Google Play 스토어](https://play.google.com/store/apps/details?id=com.microsoft.myapps)에서 사용할 수 있습니다.

![Android 용 My Apps][3]   

### <a name="my-apps-for-iphone-and-ipad"></a>iPhone 및 iPad 용 My Apps

iOS용 My Apps는 iOS 버전 7 이상을 실행하는 iPhone 또는 iPad에서 지원됩니다.  
[Apple 앱 스토어](https://itunes.apple.com/us/app/my-apps-azure-active-directory/id824048653?mt=8)에서 사용할 수 있습니다.

![iOS용 My Apps][4]    



## <a name="managed-browser-for-my-apps"></a>My Apps에 대한 관리되는 브라우저

My Apps는 Intune Managed Browser에도 통합됩니다. iOS 및 Android 장치용 Intune Managed Browser는 모바일 장치의 데이터를 안전하게 유지되도록 하는 핵심적인 역할을 합니다. 회사 정보를 포함할 수 있는 웹 페이지를 안전하게 보고 탐색할 수 있도록 하고 안전한 웹 브라우징 환경을 제공합니다.  
액세스하려는 응용 프로그램에 도달하는 데 적은 클릭 수를 제공하여 Managed Browser 홈페이지 및 책갈피에서 My Apps에 빠르게 액세스할 수 있습니다.

[Apple 앱 스토어](https://itunes.apple.com/us/app/microsoft-intune-managed-browser/id943264951?mt=8) 및 [Google Play 스토어](https://play.google.com/store/apps/details?id=com.microsoft.intune.mam.managedbrowser&hl=en)에서 사용할 수 있습니다.

![My Apps에 대한 관리되는 브라우저][5]    





## <a name="tips-for-testing-the-user-experience"></a>최종 사용자 환경 테스트를 위한 팁

Azure 관리자이고 디렉터리에 있는 계정을 사용하여 Azure Portal에 로그인하면 액세스 패널에 현재 계정으로 자동 로그인됩니다. 이 경우 사용자에게 할당된 모든 응용 프로그램을 볼 수 있습니다.

***다른* 사용자 계정으로 테스트하려면:**

1. Azure Portal 또는 액세스 패널의 오른쪽 위 모서리에 있는 사용자 메뉴를 클릭한 다음 **로그아웃**을 선택합니다. 
2. [액세스 패널](http://myapps.microsoft.com)로 이동합니다.
3. 로그인 페이지에서 테스트하려는 디렉터리의 계정에 대한 사용자 이름과 암호를 입력합니다.


## <a name="starting-applications"></a>응용 프로그램 시작

액세스 패널에는 여러 유형의 응용 프로그램이 표시될 수 있습니다.

### <a name="office-365-applications"></a>Office 365 응용 프로그램

조직에서 Office 365 응용 프로그램을 사용하고 있고 해당 라이선스가 있는 경우 Office 365 응용 프로그램이 액세스 패널에 표시됩니다.

Office 365 응용 프로그램에 대한 응용 프로그램 타일을 클릭하면 해당 응용 프로그램으로 리디렉션되고 자동으로 로그인됩니다.

### <a name="microsoft-and-third-party-applications-configured-with-federation-based-sso"></a>페더레이션 기반 SSO로 구성된 Microsoft 및 타사 응용 프로그램

관리자는 Azure Portal의 Active Directory 섹션에서 **Azure AD Single Sign-On**으로 설정된 SSO 모드로 응용 프로그램을 추가할 수 있습니다. 관리자가 응용 프로그램에 대한 액세스 권한을 명시적으로 부여한 경우에만 이러한 응용 프로그램을 볼 수 있습니다.

이러한 응용 프로그램 중 하나에 대한 응용 프로그램 타일을 클릭하면 해당 응용 프로그램으로 리디렉션되고 자동으로 로그인됩니다.

### <a name="password-based-sso-without-identity-provisioning"></a>ID 프로비전 없는 암호 기반 SSO

관리자는 Azure Portal의 Active Directory 섹션에서 **암호 기반 Single Sign-On**으로 설정된 SSO 모드로 응용 프로그램을 추가할 수 있습니다. 디렉터리의 모든 사용자는 이 모드에서 구성된 모든 응용 프로그램을 볼 수 있습니다.

이러한 응용 프로그램 중 하나에 대한 타일을 처음 클릭하면 Internet Explorer 또는 Chrome용 암호 SSO 플러그 인을 설치하라는 메시지가 표시됩니다. 설치 시 웹 브라우저를 다시 시작해야 할 수도 있습니다. 액세스 패널로 돌아와 응용 프로그램 타일을 다시 클릭하면 해당 응용 프로그램에 대한 사용자 이름과 및 암호를 묻는 메시지가 표시됩니다. 사용자 이름과 암호를 입력하면 이러한 자격 증명이 Azure AD의 해당 계정에 안전하게 저장되고 연결됩니다.

다음에 해당 응용 프로그램 타일을 클릭하면 이 응용 프로그램에 자동으로 로그인됩니다.  
자격 증명을 다시 입력하거나 암호 SSO 플러그 인을 설치할 필요가 없습니다.

자격 증명이 대상 타사 응용 프로그램에서 변경된 경우 Azure AD에 저장된 자격 증명도 업데이트해야 합니다. 

**자격 증명을 업데이트하려면:**

1. 응용 프로그램 타일에 있는 아이콘을 선택합니다.
2. **자격 증명 업데이트**를 선택하여 응용 프로그램에 대한 사용자 이름 및 암호를 다시 입력합니다.


### <a name="password-based-sso-with-identity-provisioning"></a>ID 프로비전을 사용한 암호 기반 SSO

관리자는 Azure Portal의 **Active Directory** 섹션에서 ID 프로비전과 함께 **암호 기반 Single Sign-On**으로 설정된 SSO 모드로 응용 프로그램을 추가할 수 있습니다.

이러한 응용 프로그램 중 하나에 대한 응용 프로그램 타일을 처음 클릭하면 **Internet Explorer 또는 Chrome용 암호 SSO 플러그 인**을 설치하라는 메시지가 표시됩니다. 설치 시 웹 브라우저를 다시 시작해야 할 수도 있습니다.  
액세스 패널로 돌아와 응용 프로그램 타일을 다시 클릭하면 응용 프로그램에 자동으로 로그인됩니다.

일부 응용 프로그램에서는 처음 로그인할 때 암호를 변경해야 할 수도 있습니다. 자격 증명이 대상 타사 응용 프로그램에서 변경된 경우 Azure AD에 저장된 자격 증명도 업데이트해야 합니다. 

**자격 증명을 업데이트하려면:**

1. 응용 프로그램 타일에 있는 아이콘을 선택합니다.
2. **자격 증명 업데이트**를 선택하여 응용 프로그램에 대한 사용자 이름 및 암호를 다시 입력합니다.


### <a name="application-with-existing-sso-solutions"></a>기존 SSO 솔루션을 사용한 응용 프로그램

응용 프로그램에 대해 SSO를 구성하려면 Azure Portal에서 **기존 Single Sign-On**이라는 세 번째 옵션을 제공합니다. 이 옵션을 사용하면 관리자가 응용 프로그램에 대한 링크를 만들어 선택한 사용자의 액세스 패널에 배치할 수 있습니다.

예를 들어 응용 프로그램이 AD FS 2.0을 사용하여 사용자를 인증하도록 구성되어 있는 경우 관리자는 **기존 Single Sign-On** 옵션을 사용하여 액세스 패널에서 해당 응용 프로그램에 대한 링크를 만들 수 있습니다. 이 링크에 액세스하면 AD FS 2.0 또는 응용 프로그램에서 제공하는 기존 SSO 솔루션을 통해 인증됩니다.


## <a name="next-steps"></a>다음 단계

- 응용 프로그램 관리와 관련된 모든 항목의 목록을 보려면 [Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스](active-directory-apps-index.md)를 참조하세요.
 
- SaaS 앱을 Azure AD로 통합하는 방법을 알아보려면 [SaaS 앱을 통합하는 방법에 대한 자습서 목록](active-directory-saas-tutorial-list.md)을 참조하세요.
 
- Azure AD를 사용하여 앱 관리에 대한 자세한 내용은 [Azure Active Directory로 SSO(Single Sign-On) 및 앱 액세스 관리 소개](active-directory-appssoaccess-whatis.md)를 참조하세요.
 
- 사용자 프로비저닝에 대한 자세한 내용은 [SaaS 응용 프로그램에 자동화된 사용자 프로비저닝 및 프로비저닝 해제](active-directory-saas-app-provisioning.md)를 참조하세요.

<!--Image references-->
[1]: ./media/active-directory-saas-access-panel-introduction/01.png
[2]: ./media/active-directory-saas-access-panel-introduction/02.png
[3]: ./media/active-directory-saas-access-panel-introduction/03.png
[4]: ./media/active-directory-saas-access-panel-introduction/04.png
[5]: ./media/active-directory-saas-access-panel-introduction/05.png
