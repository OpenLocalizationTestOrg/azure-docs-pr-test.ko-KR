---
title: "Azure Active directory에서 B2B 공동 작업에 대 한 aaaConfigure SaaS 앱 | Microsoft Docs"
description: "Azure Active Directory B2B 공동 작업을 위한 코드 및 PowerShell 샘플"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/23/2017
ms.author: sasubram
ms.openlocfilehash: c3f22f81567c04ac23ef2316c09de718ecb15d26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-saas-apps-for-b2b-collaboration"></a>B2B 공동 작업을 위한 SaaS 앱 구성

Azure AD(Azure Active Directory) B2B 공동 작업은 Azure AD와 통합되는 대부분의 앱에서 작동합니다. 이 섹션에서는 Azure AD B2B와 함께 사용되는 일부 인기 있는 SaaS 앱을 구성하는 지침을 안내합니다.

앱별 지침을 살펴보기 전에 다음과 같이 경험에 근거한 몇 가지 규칙이 있습니다.

* Hello 앱의 대부분의 경우 사용자 설정을 수동으로 toohappen이 필요합니다. 즉, 사용자가 직접 만들어야 합니다 hello 응용 프로그램의 경우에 합니다.

* Dropbox, 예: 자동 설치를 지원 되는 앱에 대 한 별도 초대 hello 앱에서 생성 됩니다. 사용자가 각 초대 있는지 tooaccept 여야 합니다.

* 게스트 사용자의 변환 된 사용자 프로필 디스크 (UPD)와 문제가 toomitigate hello 사용자 특성에 항상 설정 **사용자 식별자** 너무**user.mail**합니다.


## <a name="dropbox-business"></a>Dropbox Business

자신의 조직 계정을 사용 하 여 tooenable 사용자 toosign, SAML Security Assertion Markup Language () id 공급자로 Dropbox 비즈니스 toouse Azure AD를 수동으로 구성 해야 있습니다. Dropbox 비즈니스 toodo 구성된 되지 않은 경우, 메시지를 표시 하거나 없습니다 허용 하는 Azure AD를 사용 하 여 사용자가 toosign 합니다.

1. 선택 하는 Azure AD에 tooadd hello Dropbox 비즈니스 앱 **엔터프라이즈 응용 프로그램** 왼쪽된 창의 hello와 클릭 **추가**합니다.

  ![hello 엔터프라이즈 응용 프로그램 페이지에서 hello "추가" 단추](media/active-directory-b2b-configure-saas-apps/add-dropbox.png)

2. Hello에 **응용 프로그램 추가** 창 입력 **dropbox** 에 hello 검색 상자를 클릭 한 **Dropbox for Business** hello 결과 목록에 있습니다.

  !["Dropbox" hello에 대 한 검색 응용 프로그램 페이지 추가](media/active-directory-b2b-configure-saas-apps/add-app-dialog.png)

3. Hello에 **Single sign on** 페이지에서 **Single sign on** 에 hello 왼쪽된 창에서 선택한 다음 입력 **user.mail** hello에 **사용자 식별자** 상자입니다. (기본적으로 UPN으로 설정됩니다.)

  ![Single sign on hello 앱에 대 한 구성](media/active-directory-b2b-configure-saas-apps/configure-app-sso.png)

4. toodownload hello 인증서 toouse Dropbox 구성에 대 한 선택 **DropBox 구성**를 선택한 후 **SAML Single Sign-on 서비스 URL** hello 목록에 있습니다.

  ![Dropbox 구성에 대 한 hello 인증서를 다운로드합니다.](media/active-directory-b2b-configure-saas-apps/download-certificate.png)

5. Hello로 tooDropbox 로그인 로그온 URL에서 hello **Single sign on** 페이지.

  ![Dropbox 로그인 hello 페이지](media/active-directory-b2b-configure-saas-apps/sign-in-to-dropbox.png)

6. Hello 메뉴에서 선택 **관리 콘솔**합니다.

  ![hello Dropbox 메뉴의 hello "관리 콘솔" 링크](media/active-directory-b2b-configure-saas-apps/dropbox-menu.png)

7. Hello에 **인증** 대화 상자에서 **자세한**, hello 인증서를 업로드 한 다음 hello **로그인 URL** 상자 hello SAML single sign on URL을 입력 합니다.

  ![hello 축소 hello 인증 대화 상자에서 "추가" 링크](media/active-directory-b2b-configure-saas-apps/dropbox-auth-01.png)

  ![hello에 "로그인 URL" hello 확장 인증 대화 상자](media/active-directory-b2b-configure-saas-apps/paste-single-sign-on-URL.png)

8. hello Azure 포털에서에서 설치 프로그램을 tooconfigure 자동 사용자 선택 **프로 비전** hello 왼쪽된 창에서 선택 **자동** hello에 **프로 비전 모드** 상자를 선택한 후 **권한을 부여**합니다.

  ![Hello Azure 포털에에서 자동 사용자 프로비저닝 구성](media/active-directory-b2b-configure-saas-apps/set-up-automatic-provisioning.png)

멤버 또는 게스트 사용자에 게는 hello Dropbox 응용 프로그램에서 설정 되는 Dropbox에서 별도 요청을 받습니다. Dropbox에 single sign-on toouse, 초대 된 사람이 해당 링크를 클릭 하 여 hello 초대를 동의 해야 합니다.

## <a name="box"></a>Box
Hello SAML 프로토콜을 기반으로 하는 페더레이션을 사용 하 여 사용자가 tooauthenticate 상자 게스트 사용자가 Azure AD 계정으로 사용할 수 있습니다. 이 절차에서는 tooBox.com 메타 데이터를 업로드합니다.

1. Hello 엔터프라이즈 응용 프로그램에서 hello 상자 응용 프로그램을 추가 합니다.

2. 순서에 따라 hello에서 single sign on 구성:

  ![Box Single Sign-On 구성](media/active-directory-b2b-configure-saas-apps/configure-box-sso.png)

 a. Hello에 **로그온 URL** hello 로그온 URL에에서 설정 되어 있는지 적절 하 게 상자에 대 한 hello Azure 포털을 확인 합니다. 이 URL은 Box.com 테 넌 트의 hello URL입니다. Hello 명명 규칙을 따라야 *https://.box.com*합니다.  
 hello **식별자** toothis 적용 되지 않습니다 하지만 응용 프로그램을 여전히 필드는 필수로 표시 합니다.

 b. Hello에 **사용자 식별자** 상자에 입력 **user.mail** (게스트 계정에 대 한 SSO)에 대 한 합니다.

 c. **SAML 서명 인증서**에서 **새 인증서 만들기**를 클릭합니다.

 d. Box.com 테 넌 트 toouse Azure AD를 id 공급자로 구성 toobegin hello 메타 데이터 파일을 다운로드 하 고 tooyour 로컬 드라이브 저장 합니다.

 e. Hello 메타 데이터 파일 toohello 상자 지원 팀에 속하는 single sign on을 구성을 전달 합니다.

3. Hello 왼쪽된 창에서 Azure AD 자동 사용자 설치에 대 한 선택 **프로 비전**를 선택한 후 **Authorize**합니다.

  ![Azure AD tooconnect tooBox 권한 부여](media/active-directory-b2b-configure-saas-apps/auth-azure-ad-to-connect-to-box.png)

Dropbox 초대와 같은 상자 초대 된 사람이 hello 상자 응용 프로그램에서 자신의 초대를 교환 해야 합니다.

## <a name="next-steps"></a>다음 단계

Hello 다음 Azure AD B2B 공동 작업에 대 한 문서를 참조 하십시오.

* [Azure AD B2B 공동 작업이란?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [B2B 공동 작업 사용자 속성](active-directory-b2b-user-properties.md)
* [B2B 공동 작업 사용자 tooa 역할 추가](active-directory-b2b-add-guest-to-role.md)
* [B2B 공동 작업 초대 위임](active-directory-b2b-delegate-invitations.md)
* [동적 그룹 및 B2B 공동 작업](active-directory-b2b-dynamic-groups.md)
* [B2B 공동 작업 코드 및 PowerShell 샘플](active-directory-b2b-code-samples.md)
* [B2B 공동 작업 사용자 토큰](active-directory-b2b-user-token.md)
* [B2B 공동 작업 사용자 클레임 매핑](active-directory-b2b-claims-mapping.md)
* [Office 365 외부 공유](active-directory-b2b-o365-external-user.md)
* [B2B 공동 작업 현재 제한](active-directory-b2b-current-limitations.md)
