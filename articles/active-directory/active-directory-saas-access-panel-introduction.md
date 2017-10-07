---
title: "aaaWhat는 Azure Active Directory 액세스 패널 hello? | Microsoft Docs"
description: "Hello의 toouse 변형 (웹 브라우저, Android 앱, iPhone 및 iPad 앱) 패널 tooaccess SaaS 앱을 액세스 하는 방법에 대해 알아봅니다."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: c0252d01-7e6e-4f79-a70e-600479577dfd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: asteen
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 800be6a69f13978c5b88e2fe28a416d4b763656c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-hello-access-panel"></a>Hello 액세스 패널 이란?

hello 액세스 패널은 웹 기반 포털입니다. 회사에 있는 사용자 수 또는 Azure AD 관리자가 부여 해 준 Azure Active Directory tooview 및 시작 클라우드 기반 응용 프로그램에서 학교 계정에 대 한 액세스. 셀프 서비스 그룹 및 hello 액세스 패널을 통해 앱 관리 기능을 사용할 수도 있습니다.

hello 액세스 패널은 hello Azure 포털에서에서 분리 되 고 본인이 아니신가요 toohave Azure 구독이 없습니다.

![액세스 패널][1]

hello 액세스 패널을 사용 하는 기능을 hello 일부 프로필 설정을 포함 하 여, tooedit이 있습니다.

- 회사 또는 학교 계정과 연결 된 hello 암호 변경

- 암호 재설정 편집

- 연락처 및 기본 설정 설정 관련된 toomulti 2 단계 인증 편집 (필수 toouse 된 계정에 대 한 관리자가 해당)

- 사용자 ID, 대체 전자 메일, 모바일 및 사무실 전화 번호 및 장치와 같은 계정 세부 정보 보기

- 보기 및 시작 클라우드 기반 응용 프로그램을 Azure AD 관리자 hello에에 대 한 액세스 권한이 부여 됩니다. Hello 사용자 관점에서 액세스 패널 hello에 대 한 자세한 내용은 hello 액세스 패널을 사용 하 여 참조 합니다. 

- 그룹을 셀프 관리합니다. 보다 구체적으로, 관리자에 게 만들고 Azure AD에서 보안 그룹 및 보안 그룹 구성원 자격 요청을 관리할 수 있습니다. 자세한 내용은 [Azure AD의 사용자를 위한 셀프 서비스 그룹 관리](active-directory-accessmanagement-self-service-group-management.md)와 [그룹 관리](active-directory-manage-groups.md)를 참조하세요.




## <a name="accessing-hello-access-panel"></a>Hello 액세스 패널에 액세스

웹 브라우저에서 URL을 따라 hello를 방문 하 여 hello 액세스 패널에 액세스할 수 있습니다.`http://myapps.microsoft.com`

로그인 페이지에 대해 구성 된 사용자 지정 브랜딩를 설정한 경우에 조직의 도메인 toohello hello URL 끝에 추가 하 여이 브랜딩을 로드할 수 있습니다.`http://myapps.microsoft.com/<your domain>.com`

이 경우 Azure Portal에서 구성된 모든 활성 또는 확인된 도메인 이름을 사용할 수 있습니다.

![Wingtip Toys 도메인 이름][2]  

Toodistribute hello URL tooall 사용자가 Azure AD와 통합 된 tooapplications에 로그인 해야 합니다.

## <a name="authentication"></a>인증

tooreach hello 액세스 패널 하면 Azure ad에서 사용자는 회사 또는 학교 계정을 통해 인증 되어야 합니다. 인증 된 tooAzure AD 직접 할 수 있습니다. 또는 조직에서 AD FS(Active Directory Federation Services) 또는 다른 기술을 사용하여 페더레이션을 구성한 경우 Windows Server Active Directory에서 인증을 받을 수도 있습니다.

Azure 또는 Office 365에 대 한 구독을 있으며 hello Azure 포털 또는 Office 365 응용 프로그램 사용 했던 경우에 로그인 다시 하지 않고 응용 프로그램의 hello 목록을 볼 수 있습니다. 중인 경우 인증 되지 않은 Azure AD의 계정에 대 한 hello 사용자 이름 및 암호를 사용 하 여에서 증명된 toosign 되어도 합니다. 조직에서 페더레이션을 구성한 경우 만으로는 hello 사용자 이름을 입력 합니다.

인증 되 면 관리자가 hello 디렉터리와 통합 하는 hello 응용 프로그램과 상호 작용할 수 있습니다. toointegrate 응용 프로그램과 Azure AD 확인 하려면 어떻게 toolearn [응용 프로그램 액세스 및 single sign on Azure Active directory 란?](active-directory-appssoaccess-whatis.md)합니다.

## <a name="web-browser-requirements"></a>웹 브라우저 요구 사항

여기에 최소한 hello 액세스 패널을 지 원하는 JavaScript 브라우저 필요 하 고 CSS를 활성화 합니다. Hello 사용자 toobe tooapplications 암호 기반 single sign on (SSO)를 통해 로그인에 대 한 hello 액세스 패널 확장이 브라우저에 설치 되어야 합니다. hello 확장은 암호 기반 SSO 용으로 구성 된 응용 프로그램을 선택 하면 자동으로 다운로드 합니다.

hello 액세스 패널 확장이 현재 Internet Explorer 8 이상 Edge, Chrome 및 Firefox 브라우저에 사용할 수는 있습니다.

## <a name="mobile-app-support"></a>모바일 앱 지원

hello Azure Active Directory 팀 게시 hello my apps 모바일 앱입니다. Hello 앱을 설치 하는 경우에 iOS 및 Android 장치에 toopassword 기반 SSO 응용 프로그램에 서명할 수 있습니다.

> [!NOTE]
> 플러그 인 또는 모바일 앱 없이 모든 장치에서 거의 모든 웹 브라우저에서 페더레이션을 지 원하는 Azure AD (Salesforce, Google Apps, Dropbox, Box, Concur, Workday, Office 365 및 기타 70 개 이상의 포함)와 tooapplications에 서명할 수 있습니다. 다른 모든 [액세스 패널 경험](https://myapps.microsoft.com/) 내 앱 모바일 앱 toobe 모바일 장치에서 사용 되는 hello도 필요 하지 않습니다.
>
>

### <a name="my-apps-for-android"></a>Android 용 My Apps

Android용 My Apps는 Android 버전 4.1 이상을 실행하는 모든 Android 장치에서 지원됩니다.  
Hello에서 사용할 수 [Google Play 스토어](https://play.google.com/store/apps/details?id=com.microsoft.myapps)합니다.

![Android 용 My Apps][3]   

### <a name="my-apps-for-iphone-and-ipad"></a>iPhone 및 iPad 용 My Apps

iOS용 My Apps는 iOS 버전 7 이상을 실행하는 iPhone 또는 iPad에서 지원됩니다.  
Hello에서 사용할 수 [Apple 앱 스토어](https://itunes.apple.com/us/app/my-apps-azure-active-directory/id824048653?mt=8)합니다.

![iOS용 My Apps][4]    



## <a name="managed-browser-for-my-apps"></a>My Apps에 대한 관리되는 브라우저

응용 프로그램은 또한 hello Intune Managed Browser에에서 통합 됩니다. iOS 및 Android 장치에 대 한 Intune Managed Browser hello 모바일 장치의 데이터를 안전 하 게 유지 되도록 하는 핵심적인 역할을 재생 합니다. 회사 정보를 포함할 수 있는 웹 페이지를 안전하게 보고 탐색할 수 있도록 하고 안전한 웹 브라우징 환경을 제공합니다.  
Managed Browser 홈 페이지 및 적은 제공 하 여 책갈피에 모두 빠르게 액세스할 toomy 앱 클릭 tooreach tooaccess 원하는 모든 응용 프로그램을 찾을 있습니다.

Hello에서 사용할 수 [Apple 앱 스토어](https://itunes.apple.com/us/app/microsoft-intune-managed-browser/id943264951?mt=8) 및 [Google Play 스토어](https://play.google.com/store/apps/details?id=com.microsoft.intune.mam.managedbrowser&hl=en)합니다.

![My Apps에 대한 관리되는 브라우저][5]    





## <a name="tips-for-testing-hello-user-experience"></a>테스트 hello 사용자 경험에 대 한 팁

Azure 관리자가 Azure 포털 toohello hello 디렉터리에 계정을 사용 하 여 로그인 하는 경우 자동으로로 로그인 되어 있습니다 toohello 액세스 패널에서 현재 계정. 이 경우 tooyou 할당 된 모든 응용 프로그램을 볼 수 있습니다.

**으로 tootest는 *다른* 사용자 계정:**

1. Hello Azure 포털 또는 hello 액세스 패널의 오른쪽 위 모서리 hello에에서 hello 사용자 메뉴를 클릭 한 다음 선택 **로그 아웃**합니다. 
2. Toohello 이동 [액세스 패널](http://myapps.microsoft.com)합니다.
3. Hello 로그인 페이지, 형식 hello 사용자 이름 및 디렉터리에 hello 계정에 대 한 암호 tootest을 할 수 있습니다.


## <a name="starting-applications"></a>응용 프로그램 시작

여러 종류의 응용 프로그램 hello 액세스 패널에 나타날 수 있습니다.

### <a name="office-365-applications"></a>Office 365 응용 프로그램

조직에 Office 365 응용 프로그램 사용 하는 경우에 사용이 허가 hello Office 365 응용 프로그램 액세스 패널에 나타납니다.

Office 365 응용 프로그램에 대 한 프로그램 타일을 클릭 하면 리디렉션된 toohello 응용 프로그램과 자동으로 로그인 됩니다.

### <a name="microsoft-and-third-party-applications-configured-with-federation-based-sso"></a>페더레이션 기반 SSO로 구성된 Microsoft 및 타사 응용 프로그램

관리자가 너무 설정 hello SSO 모드와 함께 hello hello Azure 포털의 Active Directory 섹션에서에서 응용 프로그램에 추가할 수**Azure AD Single Sign-on**합니다. 관리자가 명시적으로 부여 하 여 toohello 응용 프로그램에 액세스 하는 경우에 이러한 응용 프로그램을 볼 수 있습니다.

이러한 응용 프로그램에 대 한 타일을 클릭할 때 리디렉션할 하 toohello 응용 프로그램에 자동으로 로그인 합니다.

### <a name="password-based-sso-without-identity-provisioning"></a>ID 프로비전 없는 암호 기반 SSO

관리자가 너무 설정 hello SSO 모드와 함께 hello hello Azure 포털의 Active Directory 섹션에서에서 응용 프로그램에 추가할 수**암호 기반 Single Sign-on**합니다. Hello 디렉터리의 모든 사용자는이 모드로 구성 된 모든 응용 프로그램을 볼 수 있습니다.

hello 처음으로 클릭 하면 이러한 응용 프로그램에 대 한 타일, 증명된 tooinstall hello 암호 SSO 플러그 인을 Internet Explorer 또는 Chrome 됩니다. hello 설치 웹 브라우저가 있습니다 toorestart 필요할 수 있습니다. 반환할 toohello 액세스 패널 및 hello 응용 프로그램 타일을 다시 클릭 하 여 사용자 이름 및 암호 hello 응용 프로그램에 대 한 메시지가 표시 됩니다. 사용자 이름 및 암호를 입력 하는 경우 이러한 자격 증명 안전 하 게 저장 하 고 Azure AD에 연결 된 tooyour 계정.

hello 다음 번 toohello 응용 프로그램에 자동 로그인 됩니다 hello 응용 프로그램 타일을 클릭 합니다.  
하지 tooenter 자격 증명 다시 및 했거나 hello 암호 SSO 플러그 인을 설치 합니다.

자격 증명 hello 대상 타사 응용 프로그램에 변경 되 면 Azure AD에 저장 된 자격 증명도 업데이트 해야 합니다. 

**tooupdate 자격 증명:**

1. Hello 아이콘 hello 응용 프로그램 타일을 선택 합니다.
2. 선택 **자격 증명을 업데이트** tooreenter hello 사용자 이름 및 암호에 대 한 hello 응용 프로그램입니다.


### <a name="password-based-sso-with-identity-provisioning"></a>ID 프로비전을 사용한 암호 기반 SSO

관리자는 hello에 응용 프로그램을 추가할 수 **Active Directory** hello hello SSO 모드와 Azure 포털의 섹션은 너무 설정할**암호 기반 Single Sign-on**, id 프로비저닝 기능이 함께 합니다.

hello 처음으로 클릭 하면 이러한 응용 프로그램에 대 한 응용 프로그램 타일이, 입력 정보 요청된 tooinstall hello는 **암호 SSO 플러그 인을 Internet Explorer 또는 Chrome**합니다. hello 설치 웹 브라우저가 있습니다 toorestart 필요할 수 있습니다.  
반환할 toohello 액세스 패널 및 hello 응용 프로그램 타일을 다시 클릭 하 여 toohello 응용 프로그램에 자동 로그인 됩니다.

일부 응용 프로그램에서는 hello 첫 번째 로그인의 암호를 있습니다 toochange 필요할 수 있습니다. Hello 대상 타사 응용 프로그램에 사용자의 자격 증명 변경 되 면 Azure AD에 저장 하는 hello 자격 증명도 업데이트 해야 합니다. 

**tooupdate 자격 증명:**

1. Hello 아이콘 hello 응용 프로그램 타일을 선택 합니다.
2. 선택 **자격 증명을 업데이트** tooreenter hello 사용자 이름 및 암호에 대 한 hello 응용 프로그램입니다.


### <a name="application-with-existing-sso-solutions"></a>기존 SSO 솔루션을 사용한 응용 프로그램

SSO 응용 프로그램에 대 한 tooconfigure, hello Azure 포털 이라는 세 번째 옵션을 제공 **기존 Single Sign-on**합니다. 이 옵션 사용자 관리자 toocreate 링크 tooan 응용 프로그램을 사용 하면 선택한 사용자에 대 한 hello 액세스 패널에 배치 합니다.

예를 들어 응용 프로그램의 AD FS 2.0을 사용 하 여 구성 된 tooauthenticate 사용자 이면 관리자 צ ְ ײ hello **기존 Single Sign-on** 옵션 toocreate hello 액세스 패널에 링크 tooit 합니다. Hello 링크에 액세스 하는 경우에 AD FS 2.0 또는 제공 하는 모든 기존 SSO 솔루션 hello 응용 프로그램을 통해 인증 됩니다.


## <a name="next-steps"></a>다음 단계

- toosee 관련된 tooapplication 관리 되는 모든 항목의 목록이 참조 hello [Azure Active Directory에 응용 프로그램 관리용 문서 인덱스](active-directory-apps-index.md)합니다.
 
- toolearn toointegrate는 SaaS 앱 Azure AD로 hello를 참조 하는 방법을 [방법에 대 한 자습서 목록 toointegrate SaaS 앱](active-directory-saas-tutorial-list.md)합니다.
 
- Azure AD 사용 하 여 앱 관리에 대 한 더 toolearn 참조 hello [소개 toosingle 로그온 및 Azure Active Directory와 응용 프로그램 액세스 관리](active-directory-appssoaccess-whatis.md)합니다.
 
- 사용자 프로 비전에 대 한 더 toolearn 참조 [사용자 프로 비전 및 tooSaaS 응용 프로그램을 프로 비전 해제 자동화](active-directory-saas-app-provisioning.md)합니다.

<!--Image references-->
[1]: ./media/active-directory-saas-access-panel-introduction/01.png
[2]: ./media/active-directory-saas-access-panel-introduction/02.png
[3]: ./media/active-directory-saas-access-panel-introduction/03.png
[4]: ./media/active-directory-saas-access-panel-introduction/04.png
[5]: ./media/active-directory-saas-access-panel-introduction/05.png
