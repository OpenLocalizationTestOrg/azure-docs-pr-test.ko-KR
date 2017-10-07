---
title: "응용 프로그램에 대 한 Azure AD SSO aaaConfigure | Microsoft Docs"
description: "Tooself 서비스 앱 tooAzure Active Directory를 연결 하는 방법에 대해 알아봅니다 SAML 및 암호 기반 SSO를 사용 하 여"
services: active-directory
author: asmalser-msft
documentationcenter: na
manager: femila
ms.assetid: 0d42eb0c-6d3f-4557-9030-e88e86709a19
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/20/2017
ms.author: asmalser
ms.reviewer: luleon
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 002a19a6c7ad25ea2f3b9c6a7c7874ed2be23cce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-single-sign-on-tooapplications-that-are-not-in-hello-azure-active-directory-application-gallery"></a>Single sign on tooapplications hello Azure Active Directory 응용 프로그램 갤러리에 없는 구성
이 문서는 관리자가 tooconfigure single sign on tooapplications hello Azure Active Directory 응용 프로그램 갤러리에 표시 되지 않습니다 수 있는 기능에 대 한 *코드를 작성 하지 않고도*합니다. 이 기능은 2015년 11월 18일 Technical Preview에서 발표되었으며 [Azure Active Directory Premium](active-directory-editions.md)에 포함되어 있습니다. 하는 경우 대신 원하는 방법에 대 한 개발자 지침에 대 한 코드를 통해 Azure AD 사용 하 여 사용자 지정 앱 toointegrate 참조 [Azure AD의 인증 시나리오](active-directory-authentication-scenarios.md)합니다.

hello Azure Active Directory 응용 프로그램 갤러리의 목록을 제공 toosupport single sign on Azure Active Directory와의 형태 알려진 응용 프로그램에 설명 된 대로 [이 여기서](active-directory-appssoaccess-whatis.md)합니다. 조직의 IT 전문가 또는 시스템 통합자) (으로 찾은 hello 응용 프로그램 tooconnect 5d; Azure 관리 포털 tooenable single sign on hello에 따라 hello 단계별 지침을 시작할 수 있습니다.

또한 [Azure Active Directory Premium](active-directory-editions.md) 라이선스가 있는 고객에게는 다음과 같은 기능이 제공됩니다

* SAML 2.0 ID 공급자를 지원하는 응용 프로그램의 셀프 서비스 통합(SP에서 시작 또는 IdP에서 시작)
* [암호 기반 SSO](active-directory-appssoaccess-whatis.md#password-based-single-sign-on)
* 사용자 프로 비전에 대 한 hello SCIM 프로토콜을 사용 하는 응용 프로그램의 셀프 서비스 연결 ([여기에 설명 된](active-directory-scim-provisioning.md))
* 기능 tooadd hello에서 tooany 응용 프로그램 연결 [Office 365 앱 시작 관리자](https://blogs.office.com/2014/10/16/organize-office-365-new-app-launcher-2/) 또는 hello [Azure AD 액세스 패널](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users)

이 SaaS 응용 프로그램을 사용 하지만 아직 toohello 등록 된 Azure AD 응용 프로그램 갤러리 뿐 아니라 조직이 tooservers hello 클라우드 또는 온-프레미스에 제어를 구축 하는 타사 웹 응용 프로그램에 포함할 수 있습니다.

*앱 통합 템플릿*이라고도 하는 이러한 기능은 SAML, SCIM 또는 폼 기반 인증을 지원하는 앱에 대한 표준 기반 연결점을 제공하며, 다양한 응용 프로그램과의 호환성을 위해 유연한 옵션과 설정을 포함하고 있습니다. 

## <a name="adding-an-unlisted-application"></a>목록에 없는 응용 프로그램 추가
tooconnect 앱 통합 서식 파일을 사용 하 여 응용 프로그램에 Azure Active Directory 관리자 계정을 사용 하 여 hello Azure 관리 포털에 로그인 하 고 toohello 찾아보기 **Active Directory > [Directory] > 응용 프로그램**섹션에서 **추가**, 차례로 **hello 갤러리에서 응용 프로그램 추가**합니다. 

![][1]

Hello 응용 프로그램 갤러리에서 hello를 사용 하 여 목록에 없는 앱을 추가할 수 있습니다 **사용자 지정** hello 왼쪽 또는 hello를 선택 하 여 범주 **응용 프로그램 목록에 없는 추가** hello 검색에 표시 되는 링크 결과 경우 원하는 앱 찾을 수 없습니다. 응용 프로그램에 대 한 이름을 입력 한 후 hello single sign on 옵션 및 동작을 구성할 수 있습니다. 

**유용한 정보**: hello 응용 프로그램이 이미 있으면 hello 응용 프로그램 갤러리에서 모범 사례로, 검색 함수 toocheck toosee hello를 사용 합니다. Hello 앱을 찾아 해당 설명이 "single sign on", 다음 hello 응용 프로그램에 언급 하는 경우 페더레이션된 single sign-on에 이미 지원 됩니다. 

![][2]

이러한 방식으로 응용 프로그램을 추가 사전 통합 된 응용 프로그램에 대해 사용할 수 있는 매우 유사한 환경 toohello를 제공 합니다. toostart, **구성 Single Sign-on**합니다. 다음 화면 hello hello 다음 섹션에서에서 설명 하는 hello 다음에 단일 로그인을 구성 하기 위한 세 가지 옵션을 표시 합니다.

![][3]

## <a name="azure-ad-single-sign-on"></a>Azure AD Single Sign-On
이 옵션 tooconfigure SAML 기반 hello 응용 프로그램에 인증을 선택 합니다. 사용 하려면이 응용 프로그램 지원 SAML 2.0 hello 및 어떻게 toouse hello 계속 하기 전에 hello 응용 프로그램의 SAML 기능에 정보를 수집 해야 합니다. 선택한 후 **다음**, 입력 정보 요청된 tooenter 세 개의 서로 다른 Url hello 응용 프로그램에 대 한 toohello SAML 끝점에 해당 됩니다. 

![][4]

다음과 같습니다.

* **로그온 URL (SP에서 시작한만)** hello 사용자가 응용 프로그램에서 toosign toothis 위치 – 합니다. Hello 응용 프로그램 구성 된 경우 tooperform 서비스 공급자가 시작한 단일 로그인, 다음 사용자 이동 toothis URL을 hello 서비스 공급자를 필요한 리디렉션 tooAzure AD tooauthenticate hello 및 hello 사용자의 로그온 수행 합니다. 이 필드는 채워집니다 경우 Azure AD는이 URL toolaunch hello 응용 프로그램에서 Office 365 및 Azure AD 액세스 패널 hello를 사용 합니다. 이 필드를 ommited 경우 Azure AD id 공급자를 대신 수행-시작 된 로그온 hello 앱 시작 시 hello Azure AD 또는 Office 365, Azure AD 액세스 패널 hello에서에서 single sign on URL (copiable hello 대시보드 탭에서).
* **발급자 URL** -구성 되는 단일 로그온에 대 한 hello 발급자 URL hello 응용 프로그램을 고유 하 게 식별 해야 합니다. 이 값은 Azure AD hello로 백 tooapplication를 전송 하는 hello 값 **Audience** hello SAML 토큰 및 hello 응용 프로그램의 매개 변수는 예상된 toovalidate 것입니다. 이 값은 또한 hello로 표시 **엔터티 ID** hello 응용 프로그램에서 제공 하는 SAML 메타 데이터에 있습니다. Hello 응용 프로그램의 SAML 설명서 내용에 대 한 자세한 내용은 확인은 엔터티 ID 또는 대상 그룹 값이 있습니다. 다음은 hello Audience URL hello SAML 토큰 반환 된 toohello 응용 프로그램에 표시 하는 방법의 예:

```
    <Subject>
    <NameID Format="urn:oasis:names:tc:SAML:2.0:nameid-format:unspecificed">chad.smith@example.com</NameID>
        <SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer" />
      </Subject>
      <Conditions NotBefore="2014-12-19T01:03:14.278Z" NotOnOrAfter="2014-12-19T02:03:14.278Z">
        <AudienceRestriction>
          <Audience>https://tenant.example.com</Audience>
        </AudienceRestriction>
      </Conditions>
```

* **회신 URL** -hello 회신 URL은 hello 응용 프로그램이 tooreceive hello SAML 토큰을 예상 하는 위치입니다. 이 참조 된 tooas hello도 **서비스 ACS (Assertion Consumer) URL**합니다. 자세한 내용은 항목에 해당 SAML 토큰 회신 URL 또는 ACS URL hello 응용 프로그램의 SAML 설명서를 확인 합니다.
  이러한 입력 된 클릭 **다음** tooproceed toohello 다음 화면입니다. 이 화면 어떤 요구 toobe에 구성 된 응용 프로그램 쪽 tooenable hello 것 tooaccept Azure AD에서 SAML 토큰에 대 한 정보를 제공 합니다. 

![][5]

어떤 값이 필요한 hello 응용 프로그램에 따라 달라 집니다, 그리고 되므로 자세한 내용은 hello 응용 프로그램의 SAML 설명서를 확인 합니다. hello **로그온** 및 **Sign-Out** 서비스 URL 해결 toohello Azure AD의 인스턴스에 대 한 hello SAML 요청 처리 끝점 인 동일한 끝점입니다. hello 발급자 URL은 hello SAML 토큰 발급된 toohello 응용 프로그램 내 hello "발급자"으로 표시 되는 hello 값입니다. 

응용 프로그램을 구성한 후 클릭 **다음** 단추를 선택한 다음 hello **완료** tooclose hello 대화 상자. 

## <a name="assigning-users-and-groups-tooyour-saml-application"></a>사용자 및 그룹 tooyour SAML 응용 프로그램 할당
다음 응용 프로그램에 대 한 SAML 기반 id 공급자로 구성된 toouse Azure AD를 수행한 것 같군요 tootest이 있습니다. 보안 제어로 Azure AD는 있도록 toosign hello 응용 프로그램에 권한이 부여 된 Azure AD를 사용 하 여 액세스 하지 않는 한 토큰을 발급 하지 않습니다. 사용자는 직접적으로 또는 멤버인 그룹을 통해 액세스를 부여받을 수 있습니다. 

사용자 또는 그룹 tooyour 응용 tooassign 클릭 hello **사용자 할당** 단추입니다. Hello 사용자 또는 그룹 tooassign를 선택 하 고 hello를 선택 하면 선택 **할당** 단추입니다. 

![][6]

사용자 지정 하면 Azure AD tooissue hello 사용자의 액세스 패널에서이 응용 프로그램 tooappear에 대 한 타일을 일으키는 뿐만 아니라 hello 사용자에 대 한 토큰. 응용 프로그램 타일이 hello 사용자가 Office 365를 사용 하는 경우에 hello Office 365 응용 프로그램 시작 관리자에 표시 됩니다. 

Hello를 사용 하 여 hello 응용 프로그램에 대 한 타일 로고를 업로드할 수 **로고 업로드** hello 단추 **구성** hello 응용 프로그램에 대 한 탭 합니다. 

### <a name="customizing-hello-claims-issued-in-hello-saml-token"></a>Hello SAML 토큰에서 발급 된 hello 클레임을 사용자 지정
사용자 toohello 응용 프로그램을 인증 하는 Azure AD는 고유 하 게 식별 하는 hello 사용자에 대 한 정보 (또는 클레임)를 포함 하는 SAML 토큰 toohello 앱을 발급 합니다. 기본적으로 여기에 hello 사용자의 사용자 이름, 전자 메일 주소, 이름 및 성입니다. 

보거나 hello hello에서 SAML 토큰 toohello 응용 프로그램에에서 전송 하는 hello 클레임을 편집할 수 **특성** 탭 합니다. 

![][7]

두 가지 가능한 원인은 hello SAML 토큰에서 발급 된 tooedit hello 클레임 할 수 있습니다: •hello 응용 프로그램을 다른 클레임 Uri의 설정 또는 값 •Your 응용 프로그램 hello를 필요로 하는 방식으로 배포 된 클레임 toorequire 작성 된 NameIdentifier 클레임 이외의 hello 사용자 이름 (즉, 사용자 계정 이름) Azure Active Directory에 저장 된 toobe입니다. 

이러한 시나리오에 대 한 클레임 tooadd 및 편집에 대 한 내용은 체크 아웃이 [클레임 사용자 지정 문서](active-directory-saml-claims-customization.md)합니다. 

### <a name="testing-hello-saml-application"></a>Hello SAML 응용 프로그램 테스트
Hello SAML Url 및 인증서가 구성 되 면 hello 응용 프로그램 및 Azure AD에서 사용자 또는 그룹 toohello 응용 프로그램이 Azure에서 할당 된 hello 클레임 검토 하 고 필요에 따라 편집 된 힙이고 hello 사용자가 hello에 준비 toosign 응용 프로그램입니다. 

tootest, 단순히에 로그인 https://myapps.microsoft.com toohello 응용 프로그램에 할당 된 사용자 계정을 사용 하 여 Azure AD 액세스 패널로 hello 하 고 hello 단일 로그온 프로세스 오프 응용 프로그램 tookick hello에 대 한 hello 타일을 클릭 합니다. 또는 찾아볼 수 있습니다 직접 hello 응용 프로그램 및 여기에서 한 로그인에 대 한 toohello 로그온 URL. 

디버깅 팁, 참조 [방법에 대 한 문서 toodebug tooapplications 로그온 단일 SAML 기반](active-directory-saml-debugging.md) 

## <a name="password-single-sign-on"></a>암호 Single Sign-On
이 옵션 tooconfigure 선택 [암호 기반 single sign on](active-directory-appssoaccess-whatis.md) HTML 로그인 페이지를 포함 하는 웹 응용 프로그램에 대 한 합니다. 암호 기반 SSO, 보관, 참조 tooas 암호도 toomanage 사용자 액세스 및 암호 tooweb 응용 프로그램을 id 페더레이션을 지원 하지 않는 있습니다. 여러 사용자에 게 tooshare tooyour 조직의 소셜 미디어 응용 프로그램 계정 등의 단일 계정 할 수 있는 시나리오에도 유용 합니다. 

선택한 후 **다음**, hello 응용 프로그램의 웹 기반 로그인 페이지의 hello URL 증명된 tooenter 됩니다. 입력 필드를 참고가 hello 사용자 이름 및 암호를 포함 하는 hello 페이지 여야 합니다. 한 번 입력 한, Azure AD는 프로세스 tooparse hello 로그인 페이지 사용자 이름 입력 및 암호 입력에 대 한 시작합니다. Hello 프로세스가 실패할 경우 다음 과정을 안내는 다른 프로세스 (Internet Explorer, Chrome 또는 Firefox 필요) toomanually 캡처 hello 필드 수 있는 브라우저 확장을 설치 합니다.

Hello 로그인 페이지 캡처됩니다, 사용자 및 그룹을 할당할 수 있습니다 및 자격 증명 정책을 일반와 동일 하 게 설정할 수 있습니다 되 면 [암호 SSO 앱](active-directory-appssoaccess-whatis.md)합니다.

참고: hello를 사용 하 여 hello 응용 프로그램에 대 한 타일 로고를 업로드할 수 있습니다 **로고 업로드** hello 단추 **구성** hello 응용 프로그램에 대 한 탭 합니다. 

## <a name="existing-single-sign-on"></a>기존 Single Sign-On
이 옵션 tooadd을 링크 tooan 응용 프로그램 tooyour 조직의 Azure AD 액세스 패널 또는 Office 365 포털을 선택 합니다. 현재 Azure Active Directory Federation Services (또는 다른 페더레이션 서비스)를 사용 하는이 tooadd 링크 toocustom 웹 앱 인증을 위해 Azure AD는 대신 사용할 수 있습니다. 또는 딥 링크 toospecific SharePoint 페이지 또는 사용자의 액세스 패널에 tooappear 원하는 다른 웹 페이지를 추가할 수 있습니다. 

선택한 후 **다음**에 응용 프로그램 toolink hello의 hello URL 증명된 tooenter 됩니다. 완료 되 면 사용자 및 그룹을 지정할 수도 있습니다 hello에 hello 응용 프로그램 tooappear 시키는 toohello 응용 프로그램 [Office 365 앱 시작 관리자](https://blogs.office.com/2014/10/16/organize-office-365-new-app-launcher-2/) 또는 hello [Azure AD 액세스 패널](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users) 해당 사용자에 대 한 합니다.

참고: hello를 사용 하 여 hello 응용 프로그램에 대 한 타일 로고를 업로드할 수 있습니다 **로고 업로드** hello 단추 **구성** hello 응용 프로그램에 대 한 탭 합니다.

## <a name="related-articles"></a>관련 문서
* [Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스](active-directory-apps-index.md)
* [tooCustomize 클레임 발급 방식 hello Pre-Integrated 앱에 대 한 SAML 토큰](active-directory-saml-claims-customization.md)
* [SAML 기반 Single Sign-On 문제 해결](active-directory-saml-debugging.md)

<!--Image references-->
[1]: ./media/active-directory-saas-custom-apps/customapp1.png
[2]: ./media/active-directory-saas-custom-apps/customapp2.png
[3]: ./media/active-directory-saas-custom-apps/customapp3.png
[4]: ./media/active-directory-saas-custom-apps/customapp4.png
[5]: ./media/active-directory-saas-custom-apps/customapp5.png
[6]: ./media/active-directory-saas-custom-apps/customapp6.png
[7]: ./media/active-directory-saas-custom-apps/customapp7.png
