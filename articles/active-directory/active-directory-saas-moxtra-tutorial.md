---
title: "자습서: Moxtra와 Azure Active Directory 통합 | Microsoft Docs"
description: "단일 로그온 tooconfigure 방법을 알아보려면 Azure Active Directory와 Moxtra 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2aed2d4b-1dcd-4839-8fed-9419d107c61c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 82e2fcc390ba508e86a3992ec1c81d0a0ffed96b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-moxtra"></a>자습서: Moxtra와 Azure Active Directory 통합

이 자습서에 설명 어떻게 toointegrate Azure Active Directory (Azure AD)와 Moxtra 합니다.

Azure AD와 Moxtra 통합 hello 다음 이점을 제공 합니다.

- 액세스 tooMoxtra을 지닌 Azure AD에서 제어할 수 있습니다.
- 프로그램 사용자 tooautomatically get 로그온 tooMoxtra (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.
- 하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.

Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.

## <a name="prerequisites"></a>필수 조건

Azure AD 통합와 Moxtra tooconfigure 다음 항목 hello가 필요 합니다.

- Azure AD 구독
- Moxtra Single Sign-On이 설정된 구독

> [!NOTE]
> 이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.

이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.

- 꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.
- Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.

## <a name="scenario-description"></a>시나리오 설명
이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다. 이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.

1. Moxtra는 hello 갤러리 추가
2. Azure AD Single Sign-on 구성 및 테스트

## <a name="adding-moxtra-from-hello-gallery"></a>Moxtra는 hello 갤러리 추가
tooconfigure hello와의 통합 Moxtra Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Moxtra tooadd가 필요합니다.

**hello 갤러리에서 Moxtra tooadd hello 다음 단계를 수행 합니다.**

1. Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다. 

    ![Active Directory][1]

2. 너무 이동**엔터프라이즈 응용 프로그램**합니다. 이동 하 여 너무**모든 응용 프로그램**합니다.

    ![응용 프로그램][2]
    
3. tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.

    ![응용 프로그램][3]

4. Hello 검색 상자에 입력 **Moxtra**합니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_search.png)

5. Hello 결과 패널에서 선택 **Moxtra**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Azure AD Single Sign-on 구성 및 테스트
이 섹션에서는 “Britta Simon”이라는 테스트 사용자를 기반으로 Moxtra에서 Azure AD Single Sign-On을 구성하고 테스트합니다.

Single sign on toowork에 대 한 Azure AD는 tooknow Moxtra에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다. 즉, Azure AD 사용자와 Moxtra에 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.

Moxtra에서 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.

tooconfigure 및 Azure AD에서 single sign-on와 Moxtra 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.

1. **[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.
2. **[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.
3. **[Moxtra 테스트 사용자 만들기](#creating-a-moxtra-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 Moxtra에 해당 하는 도구입니다.
4. **[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.
5. **[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성

이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 Moxtra 응용 프로그램에서 single sign on 구성 합니다.

**Azure AD tooconfigure single sign on와 Moxtra, hello 다음 단계를 수행 합니다.**

1. Hello hello에 Azure 포털에서에서 **Moxtra** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.

    ![Single Sign-on 구성][4]

2. Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.
 
    ![Single Sign-on 구성](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_samlbase.png)

3. Hello에 **Moxtra 도메인 및 Url** 섹션에서 단계 다음에 나오는 hello 수행:

    ![Single Sign-on 구성](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_url.png)

    Hello에 **로그온 URL** 텍스트 상자에 다음 URL로:`https://www.moxtra.com/service/#login`

4. Moxtra 응용 프로그램에는 특정 형식의 hello SAML 어설션 합니다. 이 응용 프로그램에 대 한 클레임을 따라 hello를 구성 합니다. Hello에서 이러한 특성의 hello 값을 관리할 수 있습니다 "**사용자 특성**" 응용 프로그램 통합 페이지에서 섹션. hello 스크린 샷 뒤에이 구성에 대 한 예가 나와 있습니다. 

    ![Single Sign-on 구성](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_attributes.png)
    
5. Hello에 **사용자 특성** hello 섹션 **Single sign on** 대화 상자에서 hello 이미지에 나와 있는 것 처럼 SAML 토큰 특성을 구성 하 고 hello 다음 단계를 수행 합니다.
    
    | 특성 이름 | 특성 값 |
    | ------------------- | -------------------- |    
    | firstname | user.givenname |
    | lastname | user.surname |
    | idpid    | < SAML 엔터티 ID > 

    > [!Note]
    > 값을 hello **idpid** 특성이 실제있지 않습니다. hello 실제 값을 얻을 수 **빠른 참조** 섹션 아래 **Moxtra 구성**합니다.
    
    a. 클릭 **특성 추가** tooopen hello **특성 추가** 대화 상자.

    ![Single Sign-on 구성](./media/active-directory-saas-moxtra-tutorial/tutorial_attribute_04.png)

    b. Hello에 **이름** textbox, 해당 행에 대 한 표시 형식 hello 특성 이름입니다.

    ![Single Sign-on 구성](./media/active-directory-saas-moxtra-tutorial/tutorial_attribute_05.png)

    c. Hello에서 **값** 목록, 해당 행에 대 한 표시 유형 hello 특성 값입니다.

    d. **Ok**를 클릭합니다.
    
5. Hello에 **SAML 서명 인증서** 섹션에서 클릭 **Certificate(Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_certificate.png) 

6. **저장** 단추를 클릭합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-moxtra-tutorial/tutorial_general_400.png)

7. Hello에 **Moxtra 구성** 섹션에서 클릭 **구성 Moxtra** tooopen **sign on 구성** 창. 복사 hello **SAML 엔터티 ID, 및 SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**

    ![Single Sign-on 구성](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_configure.png) 

8. 다른 브라우저 창에서 관리자 권한으로 tooyour Moxtra 회사 사이트에 로그인 합니다.

9. Hello 왼쪽에 hello 도구 모음에서 클릭 **관리 콘솔 > SAML Single Sign on**, 클릭 하 고 **새로**합니다.
   
    ![Single Sign-on 구성](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_06.png) 

10. Hello에 **SAML** 페이지 hello 다음 단계를 수행 합니다.
   
    ![Single Sign-on 구성](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_08.png)   
 
    a. Hello에 **이름** 텍스트 상자 구성 이름 입력 합니다 (예:: *SAML*). 
  
    b. Hello에 **IdP 엔터티 ID** 붙여넣기 hello 값의 텍스트 상자 **SAML 엔터티 ID** Azure 포털에서 복사한입니다. 
 
    c. **로그인 URL** 붙여넣기 hello 값의 텍스트 상자 **SAML Single Sign-on 서비스 URL** Azure 포털에서 복사한입니다. 
 
    d. Hello에 **AuthnContextClassRef** 텍스트 상자에 **urn: oasis: 이름: tc: SAML:2.0:ac:classes:Password**합니다. 
 
    e. Hello에 **NameID 형식** 텍스트 상자에 **urn: oasis: 이름: tc: SAML:1.1:nameid-: emailAddress**합니다. 
 
    f. 메모장에서 Azure 포털에서 다운로드 한 인증서 열기 hello 내용을 복사 하 고 hello에 붙여 넣습니다 **인증서** 텍스트 상자에 붙여넣습니다.    
 
    g. Hello SAML 전자 메일 도메인 텍스트 상자에 SAML 전자 메일 도메인을 입력 합니다.    
  
    >[!NOTE]
    >toosee hello 단계 tooverify hello 도메인 hello 클릭 "**i**" 아래 합니다.

    h. **업데이트**를 클릭합니다.

> [!TIP]
> 이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!  Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션. 자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Azure AD 테스트 사용자 만들기
이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.

![Azure AD 사용자 만들기][100]

**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**

1. Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-moxtra-tutorial/create_aaduser_01.png) 

2. 사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-moxtra-tutorial/create_aaduser_02.png) 

3. tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-moxtra-tutorial/create_aaduser_03.png) 

4. Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-moxtra-tutorial/create_aaduser_04.png) 

    a. Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.

    b. Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.

    c. 선택 **암호 표시** hello hello 값 기록 **암호**합니다.

    d. **만들기**를 클릭합니다.
 
### <a name="creating-a-moxtra-test-user"></a>Moxtra 테스트 사용자 만들기

hello이이 섹션의 목적은 toocreate Britta Simon Moxtra에서 호출 하는 사용자입니다.

**toocreate Britta Simon Moxtra의 라는 사용자를 만들면 hello 다음 단계를 수행 합니다.**

1. 관리자 권한으로 Moxtra 회사 사이트 tooyour에 로그인 합니다.

2. Hello 왼쪽에 hello 도구 모음에서 클릭 **관리 콘솔 > 사용자 관리**, 차례로 **사용자 추가**합니다.
   
    ![Single Sign-on 구성](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_10.png) 

3. Hello에 **사용자 추가** 대화 상자에서 hello 다음 단계를 수행 합니다.
  
    a. Hello에 **이름** 텍스트 상자에 **Britta**합니다.
  
    b. Hello에 **성** 텍스트 상자에 **Simon**합니다.
  
    c. Hello에 **전자 메일** 텍스트 상자에 Britta의 전자 메일 주소 Azure 포털에서와 동일 합니다.
  
    d. Hello에 **나누기** 텍스트 상자에 **Dev**합니다.
  
    e. Hello에 **부서** 텍스트 상자에 **IT**합니다.
  
    f. **관리자**를 선택합니다.
  
    g. **추가**를 클릭합니다.

### <a name="assigning-hello-azure-ad-test-user"></a>Azure AD hello 테스트 사용자를 할당합니다.

이 섹션에서는 tooMoxtra 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.

![사용자 할당][200] 

**tooassign Britta Simon tooMoxtra hello 다음 단계를 수행 합니다.**

1. Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.

    ![사용자 할당][201] 

2. Hello 응용 프로그램 목록에서 선택 **Moxtra**합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_app.png) 

3. Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.

    ![사용자 할당][202] 

4. **추가** 단추를 클릭합니다. 그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.

    ![사용자 할당][203]

5. **사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.

6. **사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.

7. **할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.
    
### <a name="testing-single-sign-on"></a>Single Sign-On 테스트

이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.

Hello 액세스 패널에서에서 hello Moxtra 타일을 클릭할 때 자동으로 로그온 tooyour Moxtra 응용 프로그램을 구해야 합니다.
액세스 패널 hello에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.

## <a name="additional-resources"></a>추가 리소스

* [방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와](active-directory-saas-tutorial-list.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_203.png

