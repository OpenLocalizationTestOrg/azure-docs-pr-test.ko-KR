---
title: "자습서: IBM Kenexa Survey Enterprise와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법에 대해 알아봅니다 Azure Active Directory와 IBM Kenexa 설문 조사 엔터프라이즈 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c7aac6da-f4bf-419e-9e1a-16b460641a52
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: cf7ed886b4418ac396ca7056827ee10fd7a19ef1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ibm-kenexa-survey-enterprise"></a>자습서: IBM Kenexa Survey Enterprise와 Azure Active Directory 통합

이 자습서에 설명 어떻게 toointegrate IBM Kenexa 설문 조사 Enterprise와 Azure Active Directory (Azure AD).

Azure AD와 IBM Kenexa 설문 조사 엔터프라이즈 통합 이점을 다음 hello로 제공 합니다.

- 액세스 tooIBM Kenexa 설문 조사 엔터프라이즈를 지닌 Azure AD에서 제어할 수 있습니다.
- Single sign on (SSO)는 Azure AD 계정을 사용 하 여 tooIBM Kenexa 설문 조사 엔터프라이즈에에서 대 한 사용자가 tooautomatically 로그인을 사용할 수 있습니다.
- 하나의 중앙 위치에 사용자 계정을 관리할 수 있습니다: Azure 포털 hello 합니다.

소프트웨어에 대 한 자세한 tooknow로 Azure AD와 saas () 응용 프로그램 통합 하려는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란?](active-directory-appssoaccess-whatis.md)합니다.

## <a name="prerequisites"></a>필수 조건

IBM Kenexa 설문 조사 Enterprise와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.

- Azure AD 구독
- IBM Kenexa Survey Enterprise SSO가 설정된 구독

> [!NOTE]
> 이 자습서에서는 hello 단계를 테스트할 때에 프로덕션 환경 사용 하지 않는 것이 좋습니다.

이 자습서의 tootest hello 단계에는 이러한 권장 사항을 따르십시오.

- 꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.
- Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.

## <a name="scenario-description"></a>시나리오 설명
이 자습서에서는 테스트 환경에서 Azure AD SSO를 테스트합니다. hello 시나리오 hello 자습서에 설명 된 두 가지 주요 구성 요소로 이루어져 있습니다.

* IBM Kenexa 설문 조사 엔터프라이즈 hello 갤러리 추가
* Azure AD SSO 구성 및 테스트

## <a name="add-ibm-kenexa-survey-enterprise-from-hello-gallery"></a>Hello 갤러리에서 IBM Kenexa 설문 조사 엔터프라이즈를 추가 합니다.
Azure AD로의 IBM Kenexa 설문 조사 Enterprise tooconfigure hello 통합 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 IBM Kenexa 설문 조사 엔터프라이즈를 추가 합니다.

tooadd IBM Kenexa 설문 조사 엔터프라이즈 hello 갤러리에서 다음 hello지 않습니다.

1. Hello에 [Azure 포털](https://portal.azure.com)hello 왼쪽된 창에서 클릭 hello **Azure Active Directory** 단추입니다. 

    ![hello Azure Active Directory 단추][1]

2. **엔터프라이즈 응용 프로그램**을 선택한 다음 **모든 응용 프로그램**을 선택합니다.

    ![hello 엔터프라이즈 응용 프로그램 블레이드][2]
    
3. 응용 프로그램, 프로그램 tooadd hello 클릭 **새 응용 프로그램** 단추입니다.

    ![hello 새 응용 프로그램 단추][3]

4. Hello 검색 상자에 입력 **IBM Kenexa 설문 조사 엔터프라이즈**합니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_search.png)

5. Hello 결과 목록에서 선택 **IBM Kenexa 설문 조사 엔터프라이즈**, hello를 클릭 한 다음 **추가** tooadd hello 응용 프로그램 단추입니다.

    ![Hello 결과 목록에서 IBM Kenexa 설문 조사 Enterprise](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성 및 테스트
이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 IBM Kenexa Survey Enterprise에서 Azure AD SSO를 구성하고 테스트합니다.

SSO toowork에 대 한 Azure AD는 tooidentify hello IBM Kenexa 설문 조사 엔터프라이즈 사용자 테이블에 해당 Azure AD에서 필요 합니다. 즉, Azure AD에서는 Azure AD 사용자와 IBM Kenexa Survey Enterprise의 관련 사용자 간에 연결을 설정해야 합니다.

tooestablish hello 링크 관계의 hello 할당 hello 값 **사용자 이름** hello의 hello 값으로 IBM Kenexa 설문 조사 기업에서 **Username** Azure AD에서 합니다.

hello 다음 두 섹션에서 문서 블록을 완료 hello tooconfigure 및 IBM Kenexa 설문 조사 Enterprise와 Azure AD SSO 테스트 합니다.

### <a name="configure-azure-ad-sso"></a>Azure AD SSO 구성

이 섹션에서는 hello Azure 포털에서에서 Azure AD SSO를 사용 하도록 설정 및 hello 다음을 수행 하 여 IBM Kenexa 설문 조사 엔터프라이즈 응용 프로그램에서 SSO를 구성 합니다.

1. Hello hello에 Azure 포털에서에서 **IBM Kenexa 설문 조사 엔터프라이즈** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.

    ![IBM Kenexa Survey Enterprise 구성 Single Sign-On 링크][4]

2. Hello에 **Single sign on** 대화 상자의 hello **모드** 상자 **SAML 기반 로그온** tooenable SSO 합니다.
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_samlbase.png)

3. Hello에 **IBM Kenexa 설문 조사 엔터프라이즈 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.

    ![IBM Kenexa Survey Enterprise 도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_url.png)

    a. Hello에 **식별자** 텍스트 상자에 URL 패턴 hello로:`https://surveys.kenexa.com/<companycode>`

    b. Hello에 **회신 URL** 텍스트 상자에 URL 패턴 hello로:`https://surveys.kenexa.com/<companycode>/tools/sso.asp`

    > [!NOTE] 
    > hello 이전 값이 실제. 실제 hello 식별자로 업데이트 하 고 회신 URL입니다. tooobtain hello 실제 값, 연락처 hello [IBM Kenexa 설문 조사 엔터프라이즈 지원 팀](https://www.ibm.com/support/home/?lnk=fcw)합니다.

4. 아래 **SAML 서명 인증서**, 클릭 **인증서 (Base64)**, hello 인증서 파일 tooyour 컴퓨터를 저장 합니다.

    ![hello 인증서 (Base64) 다운로드 링크](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_certificate.png) 

    hello IBM Kenexa 설문 조사 엔터프라이즈 응용 프로그램 tooreceive hello SAML Security Assertions Markup Language () 어설션을 있습니다 tooadd 사용자 지정 특성 매핑을 toohello 구성이 필요한 SAML 토큰 특성의 특정 형식으로 필요 합니다. hello hello에 대 한 응답 hello 식별자가 사용자 클레임의 값 일치 해야 hello hello Kenexa 시스템에 구성 된 SSO ID입니다. toomap hello 조직으로 SSO 인터넷 데이터 그램 프로토콜 IDP ()에서 적절 한 사용자 식별자, hello 작동 [IBM Kenexa 설문 조사 엔터프라이즈 지원 팀](https://www.ibm.com/support/home/?lnk=fcw)합니다. 

    기본적으로 Azure AD는 hello 사용자 식별자를 hello 사용자 계정 이름 (UPN) 값으로 설정합니다. Hello에이 값을 변경할 수 있습니다 **특성** hello 스크린 샷 뒤에 나와 있는 것 처럼 탭 합니다. hello 통합 올바르게 매핑 hello를 완료 한 후에 작동 합니다.
    
    ![hello 사용자 특성 대화 상자](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_attribute.png) 

5. **Save**를 클릭합니다.

    ![hello 단추 저장에서 single sign-on 구성](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_400.png)

6. tooopen hello **sign on 구성** 창 아래에서 **IBM Kenexa 설문 조사 엔터프라이즈 구성**, 클릭 **IBM Kenexa 설문 조사 엔터프라이즈 구성**합니다. 
 
    ![hello IBM Kenexa 설문 조사 엔터프라이즈 구성 링크](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_configure.png)

7. 복사 hello **Sign-Out URL**, **SAML 엔터티 ID**, 및 **SAML single sign on 서비스 URL** hello 값 **빠른 참조** 섹션.

8. Hello에 **sign on 구성** 창 아래에서 **빠른 참조**, 복사 hello **Sign-Out URL**, **SAML 엔터티 ID**, 및  **SAML single sign on 서비스 URL** 값입니다.

9. hello에 SSO tooconfigure **IBM Kenexa 설문 조사 엔터프라이즈** 쪽, 다운로드 한 hello 송신 **인증서 (Base64)**, **Sign-Out URL**, **SAML엔터티ID**, 및 **SAML single sign on 서비스 URL** toohello 값 [IBM Kenexa 설문 조사 엔터프라이즈 지원 팀](https://www.ibm.com/support/home/?lnk=fcw)합니다.

> [!TIP]
> Hello에이 지침의 tooa 간결한 버전을 참조할 수 있습니다 [Azure 포털](https://portal.azure.com) hello 앱을 설정 하는 동안 합니다. Hello에서 hello 앱을 추가한 다음 **Active Directory** > **엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **단일 로그온** 탭을 클릭 한 다음에 액세스 hello 포함 hello 통해 설명서 **구성** hello 끝 섹션. hello 포함 된 설명서 기능에 대해 자세히 toolearn 참조 [Azure AD 설명서 포함](https://go.microsoft.com/fwlink/?linkid=845985)합니다.
> 

### <a name="create-an-azure-ad-test-user"></a>Azure AD 테스트 사용자 만들기
이 섹션에서는 hello 다음을 수행 하 여 hello Azure 포털에서에서 Britta Simon 테스트 사용자를 만듭니다.

![Azure AD 테스트 사용자 만들기][100]

1. Hello hello 왼쪽된 창에서 Azure 포털에서에서 클릭 hello **Azure Active Directory** 단추입니다.

    ![hello Azure Active Directory 단추](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_01.png) 

2. 사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹**, 클릭 하 고 **모든 사용자가**합니다.
    
    !["사용자 및 그룹" hello 및 "모든 사용자" 링크](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_02.png) 

3. tooopen hello **사용자** 대화 상자를 클릭 **추가** hello hello 맨 **모든 사용자에 게** 대화 상자.
 
    ![hello 추가 단추](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_03.png) 

4. Hello에 **사용자** 대화 상자를 hello 다음 단계를 수행 합니다.
 
    ![hello 사용자 대화 상자](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_04.png) 

    a. Hello에 **이름** 상자에서 입력 **BrittaSimon**합니다.

    b. Hello에 **사용자 이름** 상자의 사용자 Britta Simon의 hello 전자 메일 주소를 입력 합니다.

    c. 선택 hello **암호 표시** 확인란을 선택한 다음 hello에 표시 되는 hello 값 기록 **암호** 상자입니다.

    d. **만들기**를 클릭합니다.
 
### <a name="create-an-ibm-kenexa-survey-enterprise-test-user"></a>IBM Kenexa Survey Enterprise 테스트 사용자 만들기

이 섹션에서는 IBM Kenexa Survey Enterprise에서 Britta Simon이라는 사용자를 만듭니다. 

hello IBM Kenexa 설문 조사 엔터프라이즈 시스템 및 지도 hello SSO ID 하에서 toocreate 사용자 작업할 수 있는 hello [IBM Kenexa 설문 조사 엔터프라이즈 지원 팀](https://www.ibm.com/support/home/?lnk=fcw)합니다. 이 SSO ID 값도 있어야 Azure AD에서 toohello 사용자 식별자 값에 매핑됩니다. Hello에서이 기본 설정을 변경할 수 있습니다 **특성** 탭 합니다.

### <a name="assign-hello-azure-ad-test-user"></a>Azure AD hello 테스트 사용자를 할당 합니다.

이 섹션에서는 액세스 tooIBM Kenexa 설문 조사 엔터프라이즈에 권한을 부여 하 여 사용자 Britta Simon toouse Azure SSO를 사용 합니다.

![Hello 사용자 역할 할당][200] 

tooassign 사용자 Britta Simon tooIBM Kenexa 설문 조사 엔터프라이즈 다음 hello지 않습니다.

1. Hello Azure 포털을 열고 hello **응용 프로그램** 보기, toohello 이동 **디렉터리** 뷰의 **엔터프라이즈 응용 프로그램**, 클릭 하 고 **모든 응용 프로그램**합니다.

    ![hello "엔터프라이즈 응용 프로그램"과 "모든 응용 프로그램" 링크][201] 

2. Hello에 **응용 프로그램** 목록에서 **IBM Kenexa 설문 조사 엔터프라이즈**합니다.

    ![hello 응용 프로그램 목록에서 hello IBM Kenexa 설문 조사 Enterprise 링크](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_app.png) 

3. Hello 왼쪽된 창에서 클릭 **사용자 및 그룹**합니다.

    ![hello "사용자 및 그룹" 링크][202] 

4. Hello 클릭 **추가** 단추를 선택한 후 hello **할당 추가** 창 선택 **사용자 및 그룹**합니다.

    ![hello 할당 추가 창][203]

5. Hello에 **사용자 및 그룹** 대화 상자의 hello **사용자** 목록에서 **Britta Simon**합니다.

6. Hello에 **사용자 및 그룹** 대화 상자를 클릭 hello **선택** 단추입니다.

7. Hello에 **할당 추가** 대화 상자를 클릭 hello **할당** 단추입니다.
    
### <a name="test-single-sign-on"></a>Single Sign-On 테스트

이 섹션에서는 hello 액세스 패널을 사용 하 여 Azure AD SSO 구성을 테스트 합니다.

Hello를 클릭할 때 **IBM Kenexa 설문 조사 엔터프라이즈** 타일에 액세스 패널 hello, tooyour IBM Kenexa 설문 조사 엔터프라이즈 응용 프로그램에서에서 자동으로 서명할 해야 있습니다.

## <a name="additional-resources"></a>추가 리소스

* [방법에 대 한 자습서 목록 toointegrate SaaS 앱 Azure Active Directory와](active-directory-saas-tutorial-list.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_203.png

 
