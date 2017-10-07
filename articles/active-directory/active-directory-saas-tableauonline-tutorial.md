---
title: "Tableau Online와 Azure Active Directory 통합 | Microsoft Docs"
description: "단일 로그온 tooconfigure 방법을 알아보려면 Azure Active Directory와 Tableau Online 합니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1d4b1149-ba3b-4f4e-8bce-9791316b730d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: jeedes
ms.openlocfilehash: 590b2674270c340b4750c7b6feeaf4f0df4bf853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tableau-online"></a>Tableau Online와 Azure Active Directory 통합

이 자습서에 설명 어떻게 toointegrate Tableau 온라인 Azure Active directory (Azure AD).

다음 이점을 hello로 제공 Tableau 온라인 Azure AD와 통합:

- 온라인 액세스 tooTableau을 지닌 Azure AD에서 제어할 수 있습니다.
- 프로그램 사용자 tooautomatically get 로그온 tooTableau 온라인 (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.
- 하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.

Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.

## <a name="prerequisites"></a>필수 조건

Tableau 온라인와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.

- Azure AD 구독
- Tableau Online Single Sign-On이 설정된 구독

> [!NOTE]
> 이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.

이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.

- 꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.
- Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.

## <a name="scenario-description"></a>시나리오 설명
이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다. 이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.

1. Tableau 온라인 hello 갤러리 추가
2. Azure AD Single Sign-on 구성 및 테스트

## <a name="adding-tableau-online-from-hello-gallery"></a>Tableau 온라인 hello 갤러리 추가
tooconfigure hello와의 통합 Tableau 온라인 Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Tableau 온라인 tooadd가 필요합니다.

**Tableau 온라인 hello 갤러리에서 tooadd hello 다음 단계를 수행 합니다.**

1. Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다. 

    ![Active Directory][1]

2. 너무 이동**엔터프라이즈 응용 프로그램**합니다. 이동 하 여 너무**모든 응용 프로그램**합니다.

    ![응용 프로그램][2]
    
3. tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.

    ![응용 프로그램][3]

4. Hello 검색 상자에 입력 **Tableau 온라인**합니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_search.png)

5. Hello 결과 패널에서 선택 **Tableau 온라인**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Azure AD Single Sign-on 구성 및 테스트
이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Tableau Online에서 Azure AD Single Sign-On을 구성하고 테스트합니다.

Single sign on toowork에 대 한 Azure AD는 tooknow Tableau 온라인에서 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다. 즉, Azure AD 사용자 및 hello Tableau 온라인의 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.

Tableau 온라인에서 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.

tooconfigure 및 Tableau 온라인를 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.

1. **[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.
2. **[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.
3. **[Tableau 온라인 테스트 사용자 만들기](#creating-a-tableau-online-test-user)**  -toohave Britta Simon Tableau 온라인 표현인 연결 된 toohello Azure AD의 사용자에 해당 하는 도구입니다.
4. **[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.
5. **[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성

이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 Tableau 온라인 응용 프로그램에서 single sign on 구성 합니다.

**tooconfigure Azure AD single sign on Tableau Online과 hello 다음 단계를 수행 합니다.**

1. Hello hello에 Azure 포털에서에서 **Tableau 온라인** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.

    ![Single Sign-on 구성][4]

2. Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.
 
    ![Single Sign-on 구성](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_samlbase.png)

3. Hello에 **Tableau 온라인 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_url.png)
    
    a. Hello에 **로그온 URL** textbox hello URL 입력:`https://sso.online.tableau.com`

    b. Hello에 **식별자** textbox hello URL 입력:`https://sso.online.tableau.com/public/sp/<instancename>`

4. Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello 메타 데이터 파일을 컴퓨터에 저장 합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_certificate.png) 

5. **저장** 단추를 클릭합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-tableauonline-tutorial/tutorial_general_400.png)

6. 다른 브라우저 창에서 로그온 tooyour Tableau 온라인 응용 프로그램입니다. 너무 이동**설정** 차례로 **인증**합니다.
   
    ![Single Sign-on 구성](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_09.png)
    
7. SAML tooenable 아래 **인증 유형을** 섹션. Hello 확인 **Single sign on saml** 확인란을 선택 합니다.
   
    ![Single Sign-on 구성](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_12.png)

8. **Tableau Online으로 메타데이터 파일 가져오기** 섹션까지 아래로 스크롤합니다.  찾아보기를 클릭 하 고 Azure AD에서 다운로드 한 hello 메타 데이터 파일을 가져옵니다. 그런 후 **Apply**를 클릭합니다.
   
   ![Single Sign-on 구성](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_13.png)

9. Hello에 **어설션을 일치** 섹션에서 hello 해당 Id 공급자 어설션 이름에 대 한 삽입 **전자 메일 주소**, **이름**, 및 **성** . tooget Azure AD에서이 정보: 
  
    a. Hello Azure 포털에서 hello에 **Tableau 온라인** 응용 프로그램 통합 페이지.
    
    b. Hello 특성 섹션에서 선택 hello **"보기 및 다른 모든 사용자 속성을 편집할"** 확인란을 선택 합니다. 
    
   ![Single Sign-on 구성](./media/active-directory-saas-tableauonline-tutorial/attributesection.png)
      
    c. 이러한 특성에 대 한 hello 네임 스페이스 값을 복사: givenname, 전자 메일 및 surname를 사용 하 여 다음 단계 hello:

   ![Azure AD Single Sign-On](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_10.png)
    
    d. **user.givenname** 값을 클릭합니다. 
    
    e. Hello에서 hello 값 복사 **네임 스페이스** 텍스트 상자에 붙여넣습니다.

   ![Single Sign-on 구성](./media/active-directory-saas-tableauonline-tutorial/attributesection2.png)

    f. hello 전자 메일 및 surname toocopy hello 네임 스페이스 값 hello 이전 단계를 따릅니다.

    g. Toohello Tableau 온라인 응용 프로그램 전환 다음 hello 설정 **Tableau 온라인 특성** 다음과 같은 섹션:
     * 전자 메일: **메일** 또는 **userprincipalname**
     * 이름: **givenname**
     * 성: **surname**
   
   ![Single Sign-on 구성](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_14.png)

> [!TIP]
> 이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!  Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션. 자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Azure AD 테스트 사용자 만들기
이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.

![Azure AD 사용자 만들기][100]

**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**

1. Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_01.png) 

2. 사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_02.png) 

3. tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_03.png) 

4. Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_04.png) 

    a. Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.

    b. Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.

    c. 선택 **암호 표시** hello hello 값 기록 **암호**합니다.

    d. **만들기**를 클릭합니다.
 
### <a name="creating-a-tableau-online-test-user"></a>Tableau Online 테스트 사용자 만들기

이 섹션에서는 Tableau Online에서 Britta Simon이라는 사용자를 만듭니다.

1. **Tableau Online**에서 **설정**을 클릭한 후 **인증** 섹션을 클릭합니다. 너무 아래로 스크롤하여**사용자 선택** 섹션. **사용자 추가**를 클릭하고 **이메일 주소 입력**을 클릭합니다.
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_15.png)
2. **SSO(Single Sign-On) 인증에 대한 사용자 추가**를 선택합니다. Hello에 **전자 메일 주소 입력** textbox 추가britta.simon@contoso.com
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_11.png)
3. **만들기**를 클릭합니다.

### <a name="assigning-hello-azure-ad-test-user"></a>Azure AD hello 테스트 사용자를 할당합니다.

이 섹션에서는 액세스 tooTableau 온라인 권한을 부여 하 여 Britta Simon toouse Azure single sign on을 사용 합니다.

![사용자 할당][200] 

**tooassign Britta Simon tooTableau 온라인으로 hello 다음 단계를 수행 합니다.**

1. Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.

    ![사용자 할당][201] 

2. Hello 응용 프로그램 목록에서 선택 **Tableau 온라인**합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_app.png) 

3. Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.

    ![사용자 할당][202] 

4. **추가** 단추를 클릭합니다. 그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.

    ![사용자 할당][203]

5. **사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.

6. **사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.

7. **할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.
    
### <a name="testing-single-sign-on"></a>Single Sign-On 테스트

이 섹션의 hello 목적은 tootest 액세스 패널을 hello 사용 하 여 Azure AD SSO 구성 합니다.

Hello 액세스 패널에서에서 hello Tableau 온라인 타일을 클릭할 때 자동으로 로그온 tooyour Tableau 온라인 응용 프로그램을 구해야 합니다.

## <a name="additional-resources"></a>추가 리소스

* [방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와](active-directory-saas-tutorial-list.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_203.png

