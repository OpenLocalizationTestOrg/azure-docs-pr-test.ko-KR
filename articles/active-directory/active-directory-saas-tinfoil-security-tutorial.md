---
title: "자습서: TINFOIL SECURITY와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 TINFOIL SECURITY 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: da02da92-e3b0-4c09-ad6c-180882b0f9f8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 1a3fa9880d9e026c2d6d6548188df2269ff69139
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tinfoil-security"></a>자습서: TINFOIL SECURITY와 Azure Active Directory 통합

이 자습서에 설명 어떻게 toointegrate Azure Active Directory (Azure AD)와 TINFOIL SECURITY 합니다.

Azure AD와 TINFOIL SECURITY 통합 이점을 다음 hello로 제공 합니다.

- 액세스 tooTINFOIL 보안을 지닌 Azure AD에서 제어할 수 있습니다.
- 에 사용자가 tooautomatically get 로그온 tooTINFOIL (Single Sign-on) 보안으로는 Azure AD 계정 사용 하도록 설정할 수 있습니다.
- 하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.

Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.

## <a name="prerequisites"></a>필수 조건

TINFOIL SECURITY와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.

- Azure AD 구독
- TINFOIL SECURITY Single Sign-On이 설정된 구독

> [!NOTE]
> 이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.

이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.

- 꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.
- Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.

## <a name="scenario-description"></a>시나리오 설명
이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다. 이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.

1. Hello 갤러리에서 TINFOIL SECURITY를 추가 합니다.
2. Azure AD Single Sign-On 구성 및 테스트

## <a name="add-tinfoil-security-from-hello-gallery"></a>Hello 갤러리에서 TINFOIL SECURITY를 추가 합니다.
tooconfigure hello와의 통합 TINFOIL SECURITY Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 TINFOIL SECURITY tooadd가 필요합니다.

**TINFOIL SECURITY hello 갤러리에서 tooadd hello 다음 단계를 수행 합니다.**

1. Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다. 

    ![Active Directory][1]

2. 너무 이동**엔터프라이즈 응용 프로그램**합니다. 이동 하 여 너무**모든 응용 프로그램**합니다.

    ![응용 프로그램][2]
    
3. tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.

    ![응용 프로그램][3]

4. Hello 검색 상자에 입력 **TINFOIL SECURITY**선택, **TINFOIL SECURITY** 결과 패널에서 클릭 **추가** tooadd hello 응용 프로그램 단추입니다.

    ![갤러리의 TINFOIL SECURITY](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성 및 테스트
이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 TINFOIL SECURITY에서 Azure AD Single Sign-On을 구성하고 테스트합니다.

Single sign on toowork에 대 한 Azure AD는 tooknow TINFOIL SECURITY에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다. 즉, Azure AD 사용자와 TINFOIL SECURITY에 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.

TINFOIL SECURITY에 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.

tooconfigure 및 TINFOIL SECURITY를 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.

1. **[Azure AD Single Sign-on 구성](#configure-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.
2. **[Azure AD 테스트를 만들고](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.
3. **[TINFOIL SECURITY 테스트 사용자 만들기](#create-a-tinfoil-security-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 TINFOIL SECURITY에 해당 하는 도구입니다.
4. **[Azure AD hello 테스트 사용자를 할당](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.
5. **[Single Sign-on 테스트](#test-single-sign-on)**  -tooverify 구성 works를 hello 여부.

### <a name="configure-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성

이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 TINFOIL SECURITY 응용 프로그램에서 single sign on 구성 합니다.

**Azure AD tooconfigure single sign on와 TINFOIL SECURITY hello 다음 단계를 수행 합니다.**

1. Hello hello에 Azure 포털에서에서 **TINFOIL SECURITY** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.

    ![Single Sign-on 구성][4]

2. Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.
 
    ![SAML 기반 로그온](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_samlbase.png)

3. Hello에 **TINFOIL 보안 도메인 및 Url** 섹션에서 hello 사용자 tooperform 모든 단계와 서로 hello 앱 Azure로 이미 사전 통합 되어 있습니다.

    ![Single Sign-on 구성](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_url.png)


4. Hello에 **SAML 서명 인증서** 섹션을 복사 hello **지문** 값입니다.

    ![SAML 서명 인증서 섹션](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_certificate.png) 

5. tooadd hello 필요한 특성 매핑을 hello 다음 단계를 수행 합니다.
    
    ![특성](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute1.png "특성")
    
    | 특성 이름    |   특성 값 |
    | ------------------- | -------------------- |
    | accountid | UXXXXXXXXXXXXX |
    
    a. **사용자 특성 추가**를 클릭합니다.
    
    ![특성 추가](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute.png "특성")
    
    ![특성 추가](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_addatt.png "특성")
    
    b. Hello에 **특성 이름** 텍스트 상자에 **accountid**합니다.
    
    c. Hello에 **특성 값** 텍스트 붙여넣기 hello 계정 ID 값 hello 자습서 나중에 발생 합니다.
    
    d. **Ok**를 클릭합니다.    

6. **저장** 단추를 클릭합니다.

    ![저장 단추](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_400.png)

7. Hello에 **TINFOIL 보안 구성** 섹션에서 클릭 **TINFOIL SECURITY 구성** tooopen **sign on 구성** 창. 복사 hello **SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**

    ![TINFOIL SECURITY 구성](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_configure.png) 

8. 다른 웹 브라우저 창에서 TINFOIL SECURITY 회사 사이트에 관리자로 로그인합니다.

9. 도구 모음의 hello hello 위쪽에 클릭 **내 계정**합니다.
   
    ![대시보드](./media/active-directory-saas-tinfoil-security-tutorial/ic798971.png "대시보드")

10. **보안**을 클릭합니다.
   
    ![보안](./media/active-directory-saas-tinfoil-security-tutorial/ic798972.png "보안")

11. Hello에 **Single Sign On** 구성 페이지를 hello 다음 단계를 수행 합니다.
   
    ![Single Sign-On](./media/active-directory-saas-tinfoil-security-tutorial/ic798973.png "Single Sign-On")
   
    a. **SAML 사용**을 선택합니다.
   
    b. **수동 구성**을 클릭합니다.
   
    c. **SAML 게시 URL** 붙여넣기 hello 값의 텍스트 상자 **SAML Single Sign-on 서비스 URL** Azure 포털에서 복사한입니다
   
    d. **SAML 인증서 지문** 붙여넣기 hello 값의 텍스트 상자 **지문** 에서 복사한 있는 **SAML 서명 인증서** 섹션.
  
    e. 복사 **Your 계정 ID** 값 hello 값에 복사한 **특성 값** 아래 텍스트 상자에 붙여넣습니다 **특성 추가** Azure 포털에서 섹션.
   
    f. **Save**를 클릭합니다.

> [!TIP]
> 이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!  Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션. 자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Azure AD 테스트 사용자 만들기
이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.

![Azure AD 사용자 만들기][100]

**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**

1. Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_01.png) 

2. 사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.
    
    ![사용자 및 그룹 -> 모든 사용자 ](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_02.png) 

3. tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.
 
    ![사용자](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_03.png) 

4. Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_04.png) 

    a. Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.

    b. Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.

    c. 선택 **암호 표시** hello hello 값 기록 **암호**합니다.

    d. **만들기**를 클릭합니다.
 
### <a name="create-a-tinfoil-security-test-user"></a>TINFOIL SECURITY 테스트 사용자 만들기

Tooenable Azure AD 사용자가 toolog TINFOIL SECURITY에 주문 하 고에 TINFOIL SECURITY에 이들 프로 비전 해야 합니다. Hello TINFOIL SECURITY의 경우에서 프로 비전은 수동 작업입니다.

**사용자가 프로 비전, tooget 단계를 수행 하는 hello를 수행 합니다.**

1. 너무 필요한 hello 사용자 엔터프라이즈 계정의 일부인 경우[hello TINFOIL SECURITY 지원 팀에 문의](https://www.tinfoilsecurity.com/contact) 만든 tooget hello 사용자 계정입니다.

2. Hello 사용자가 일반 TINFOIL SECURITY SaaS 사용자 인 경우 hello 사용자 hello 사용자의 사이트의 공동 작업자 tooany를 추가할 수 있습니다. 이 트리거는 초대 toohello 지정 된 프로세스 toosend 메일 toocreate 새로운 TINFOIL SECURITY 사용자 계정입니다.

> [!NOTE]
> 다른 TINFOIL SECURITY 사용자 계정 만들기 도구를 사용할 수 있습니다 또는 Azure AD 사용자 계정을 tooprovision TINFOIL SECURITY에서 제공 된 Api입니다.
> 
> 

### <a name="assign-hello-azure-ad-test-user"></a>Azure AD hello 테스트 사용자를 할당 합니다.

이 섹션에서는 액세스 tooTINFOIL 보안 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.

![사용자 할당][200] 

**tooassign Britta Simon tooTINFOIL 보안을 hello 다음 단계를 수행 합니다.**

1. Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.

    ![사용자 할당][201] 

2. Hello 응용 프로그램 목록에서 선택 **TINFOIL SECURITY**합니다.

    ![TINFOIL SECURITY 선택](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_app.png) 

3. Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.

    ![사용자 할당][202] 

4. **추가** 단추를 클릭합니다. 그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.

    ![사용자 할당][203]

5. **사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.

6. **사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.

7. **할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.
    
### <a name="test-single-sign-on"></a>Single Sign-On 테스트

이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.

Hello 액세스 패널에서에서 hello TINFOIL SECURITY 타일을 클릭할 때 자동으로 로그온 tooyour TINFOIL SECURITY 응용 프로그램을 구해야 합니다. 액세스 패널 hello에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.

## <a name="additional-resources"></a>추가 리소스

* [방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와](active-directory-saas-tutorial-list.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_203.png

