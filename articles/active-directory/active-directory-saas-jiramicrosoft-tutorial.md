---
title: "자습서: JIRA SAML SSO by Microsoft와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법에 대해 알아봅니다 Azure Active Directory 및 Microsoft에서 JIRA SAML SSO 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0dc847b9-eec4-4c31-845e-0144ddedc4a7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 178c4c040d9939bca271ac185ca5c2feb14f1247
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jira-saml-sso-by-microsoft"></a>자습서: JIRA SAML SSO by Microsoft와 Azure Active Directory 통합

이 자습서에 설명 어떻게 toointegrate JIRA SAML SSO microsoft Azure Active directory (Azure AD).

다음 이점을 hello로 제공 JIRA SAML SSO microsoft Azure AD와 통합:

- Microsoft에서 SAML SSO 액세스 tooJIRA 지닌 Azure AD에서 제어할 수 있습니다.
- Azure AD 계정을 사용 하면 사용자가 tooautomatically get 로그온 tooJIRA SAML SSO (Single Sign-on)는 Microsoft에서 사용할 수 있습니다.
- 하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.

Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.

## <a name="prerequisites"></a>필수 조건

Microsoft에서 JIRA SAML SSO와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.

- Azure AD 구독
- Windows 64 비트 서버 (온-프레미스 또는 클라우드에서 hello IaaS 인프라)에 설치 된 JIRA 서버 응용 프로그램
- JIRA 서버에서 HTTPS를 사용해야 합니다.
- JIRA 플러그 인에 대 한 참고 hello 지원 버전은 아래 섹션에서 언급 됩니다.
- JIRA 서버는 인터넷에 연결할 수 있는 인증을 위해 특히 tooAzure AD 로그인 페이지 및 해야 수 tooreceive Azure AD에서 토큰 hello.
- JIRA에 관리자 자격 증명이 설정되어 있어야 합니다.
- JIRA에서 WebSudo를 사용하지 않아야 합니다.
- Hello JIRA 서버 응용 프로그램에서에서 만든 사용자를 테스트 합니다.

> [!NOTE]
> 이 자습서의 단계를 tootest hello, 권장 하지는 않습니다 JIRA의 프로덕션 환경을 사용 합니다. 개발 이나 준비 hello 응용 프로그램의 환경 및 사용 하 여 hello 프로덕션 환경에 먼저 hello 통합을 테스트 합니다.

이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.

- 꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.
- Azure AD 평가판 환경이 없으면 [평가판 제품](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.

## <a name="supported-versions-of-jira"></a>지원되는 JIRA 버전 

현재 기준으로 다음 버전의 JIRA가 지원됩니다.

- JIRA 코어 및 소프트웨어: 6.0 too7.2.0
- 3.0 too3.2 JIRA 서비스 데스크:

## <a name="scenario-description"></a>시나리오 설명
이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다. 이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.

1. Microsoft에서 JIRA SAML SSO hello 갤러리 추가
2. Azure AD Single Sign-on 구성 및 테스트

## <a name="adding-jira-saml-sso-by-microsoft-from-hello-gallery"></a>Microsoft에서 JIRA SAML SSO hello 갤러리 추가
tooconfigure hello와의 통합 JIRA SAML SSO microsoft Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Microsoft에서 JIRA SAML SSO tooadd가 필요합니다.

**hello 갤러리, Microsoft에서 JIRA SAML SSO tooadd hello 다음 단계를 수행 합니다.**

1. Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다. 

    ![Active Directory][1]

2. 너무 이동**엔터프라이즈 응용 프로그램**합니다. 이동 하 여 너무**모든 응용 프로그램**합니다.

    ![응용 프로그램][2]
    
3. tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.

    ![응용 프로그램][3]

4. Hello 검색 상자에 입력 **Microsoft에서 JIRA SAML SSO**합니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_search.png)

5. Hello 결과 패널에서 선택 **Microsoft에서 JIRA SAML SSO**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Azure AD Single Sign-on 구성 및 테스트
이 섹션에서는 “Britta Simon”이라는 테스트 사용자를 기반으로 JIRA SAML SSO by Microsoft에서 Azure AD Single Sign-On을 구성하고 테스트합니다.

Single sign on toowork에 대 한 Azure AD는 tooknow Microsoft에서 JIRA SAML SSO에서 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다. 즉, Azure AD 사용자와 Microsoft에서 JIRA SAML SSO에서 관련된 사용자 hello 사이의 링크 관계를 설정할 toobe가 필요 합니다.

Microsoft에서 JIRA SAML sso에서는 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.

tooconfigure 및 Microsoft에서 JIRA SAML SSO를 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.

1. **[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.
2. **[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.
3. **[Microsoft 테스트 사용자가 JIRA SAML SSO 만들기](#creating-a-jira-saml-sso-by-microsoft-test-user)**  -toohave Britta Simon JIRA SAML SSO는 사용자의 연결 된 Azure AD toohello 표현 하는 Microsoft에서 해당 하는 도구입니다.
4. **[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.
5. **[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성

이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 Microsoft 응용 프로그램에서 single sign on JIRA SAML SSO에서 구성 합니다.

**microsoft에서 JIRA SAML SSO와 Azure AD에서 single sign-on tooconfigure hello 다음 단계를 수행 합니다.**

1. Hello hello에 Azure 포털에서에서 **Microsoft에서 JIRA SAML SSO** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.

    ![Single Sign-on 구성][4]

2. Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.
 
    ![Single Sign-on 구성](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_samlbase.png)

3. Hello에 **Microsoft 도메인 및 Url에서 JIRA SAML SSO** 섹션를 hello 다음 단계를 수행 합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_url.png)

    a. Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<domain:port>/plugins/servlet/saml/auth`

    b. Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<domain:port>/`

    c. Hello에 **회신 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<domain:port>/plugins/servlet/saml/auth`

    > [!NOTE] 
    > 이러한 값은 실제 값이 아닙니다. 이러한 항목을 업데이트 식별자, 회신 URL 및 로그온 URL 실제 hello로 값입니다. 명명된 URL인 경우 포트는 선택 사항입니다. 이러한 값은 hello 자습서의 뒷부분에 설명 된 Jira 플러그 인의 hello 구성 하는 동안 수신 됩니다.
 
4. toogenerate hello **메타 데이터** url hello 다음 단계를 수행 합니다.

    a. **앱 등록**을 클릭합니다.
    
    ![Single Sign-on 구성](./media/active-directory-saas-jiramicrosoft-tutorial/appregistrations.png)
   
    b. 클릭 **끝점** tooopen **끝점** 대화 상자.  
    
    ![Single Sign-on 구성](./media/active-directory-saas-jiramicrosoft-tutorial/endpointicon.png)

    c. Hello 복사 단추 toocopy 클릭 **페더레이션 메타 데이터 문서** url 메모장에 붙여 넣습니다.
    
    ![Single Sign-on 구성](./media/active-directory-saas-jiramicrosoft-tutorial/endpoint.png)
     
    d. 이제의 toohello 속성 페이지를 이동 **Microsoft에서 JIRA SAML SSO** 및 복사 hello **응용 프로그램 Id** 를 사용 하 여 **복사** 단추를 메모장에 붙여 넣습니다.
 
    ![Single Sign-on 구성](./media/active-directory-saas-jiramicrosoft-tutorial/appid.png)

    e. Hello 생성 **메타 데이터 URL** hello 패턴을 사용 하 여: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>` hello 플러그 인의 hello 구성에 대 한 나중에 사용 중 이므로 메모장에서이 값을 복사 합니다.

5. **저장** 단추를 클릭합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_400.png)

6. 연락처 [Microsoft](mailto:waadpartners@microsoft.com) hello 다음 hello JIRA 플러그 인에 대 한 정보로 합니다.
    
    *   고객 이름:
    *   주 도메인 이름:
    *   Azure AD Premium: 예/아니요 (플러그 인 사용 가능한 tooall hello 고객 Free, Basic 및 Premium SKU를 수 있습니다.)
    *   이 통합을 사용할 사용자의 수:
    *   JIRA 버전:
    *   설명:

7. 다른 웹 브라우저 창에서 관리자 권한으로 tooyour JIRA 인스턴스에 로그인 합니다.

8. Hello를 누르고 선 위에 마우스를 가져가면 **추가 기능**합니다.
    
    ![Single Sign-on 구성](./media/active-directory-saas-jiramicrosoft-tutorial/addon1.png)

9. 추가 기능 탭 섹션에서 **추가 기능 관리**를 클릭합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-jiramicrosoft-tutorial/addon7.png)

10. Microsoft에서 제공 하는 hello 플러그 인을 수동으로 업로드 합니다. 에 나타나는 hello 플러그 인이 설치 되 면 **사용자 설치** 의 추가 기능 섹션 **관리 추가 기능** 섹션.

11. 클릭 **구성** tooconfigure hello 새 플러그 인 합니다.

12. 구성 페이지에서 다음 단계를 수행합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-jiramicrosoft-tutorial/addon5.png)
 
    a. **메타 데이터 URL** hello 붙여 **메타 데이터 URL** hello를 클릭 하 고 Azure AD에서 생성 된 **해결** 단추입니다. Hello IdP 메타 데이터 URL을 읽고 모든 hello 필드 정보를 채웁니다.

    > [!Note]
    > 기본 SAML 사용자 ID 위치는 이름 식별자입니다. 이 tooan 특성 옵션을 변경할 수 있으며 hello 적절 한 특성 이름을 입력 합니다.

    > [!TIP]
    > 인증서를 하나만 해결 hello 메타 데이터에 오류가 발생 하지는 않도록 hello 앱에 대해 매핑된 인지 확인 합니다. Hello 메타 데이터 확인 시 여러 인증서가 있는 경우 관리자는 오류를 가져옵니다.
    
    b. 복사 hello **식별자, 회신 URL 및 로그온 URL** 값을 붙여 넣을에 **식별자, 회신 URL 및 로그온 URL** 텍스트 상자에 각각 **Microsoft 도메인 및 UrlJIRASAMLSSO** Azure 포털에서 섹션.

    c. **로그인 단추 이름** 형식 hello 이름 단추의 조직이 로그인 화면에 사용자가 toosee hello 합니다.

    d. **SAML 사용자 ID 위치** 선택 **hello hello Subject 문의 NameIdentifier 요소에 사용자 ID가** 또는 **사용자 ID는 Attribute 요소에**합니다.  이 ID는 toobe hello JIRA 사용자 id가 있습니다. Hello 사용자 id 일치 하지 않는 경우 시스템에서 사용자가 toolog를 없도록 합니다. 
    
    e. 선택 하는 경우 **사용자 ID는 Attribute 요소에** 옵션을 선택한 다음 **특성 이름** 사용자 Id가 예상한 것 hello 특성의 형식 hello 이름 텍스트 상자에 붙여넣습니다. 

    f. Hello 페더레이션된 도메인 (예: ADFS 등)와 Azure AD를 사용 하는 경우 클릭 hello **사용 홈 영역 검색** hello 구성 및 옵션 **도메인 이름**합니다.
    
    g. **도메인 이름** hello 도메인 이름 입력 hello ADFS 기반 로그인의 경우.

    h. 확인 **사용 Single Sign-out** 시 사용자가 로그 JIRA에서 Azure AD에서 toolog 아웃 하려는 경우. 

    i. 클릭 **저장** toosave hello 설정 단추입니다.

> [!TIP]
> 이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!  Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션. 자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Azure AD 테스트 사용자 만들기
이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.

![Azure AD 사용자 만들기][100]

**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**

1. Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_01.png) 

2. 사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_02.png) 

3. tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_03.png) 

4. Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_04.png) 

    a. Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.

    b. Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.

    c. 선택 **암호 표시** hello hello 값 기록 **암호**합니다.

    d. **만들기**를 클릭합니다.
 
### <a name="creating-a-jira-saml-sso-by-microsoft-test-user"></a>JIRA SAML SSO by Microsoft 테스트 사용자 만들기

tooenable Azure AD 사용자가 toolog tooJIRA 온-프레미스 서버에서 이러한 해야에 프로 비전 JIRA SAML SSO Microsoft에서 합니다. JIRA SAML SSO by Microsoft의 경우 프로비전이 수동 작업입니다.

**tooprovision 사용자 계정을 hello 다음 단계를 수행 합니다.**

1. 관리자 권한으로 JIRA 온-프레미스 서버 tooyour에 로그인 합니다.

2. Hello를 누르고 선 위에 마우스를 가져가면 **사용자 관리**합니다.

    ![직원 추가](./media/active-directory-saas-jiramicrosoft-tutorial/user1.png) 

3. 리디렉션된 tooAdministrator 액세스 페이지 tooenter는 **암호** 클릭 **확인** 단추입니다.

    ![직원 추가](./media/active-directory-saas-jiramicrosoft-tutorial/user2.png) 

4. **사용자 관리** 탭 섹션 아래에서  **사용자 만들기**를 클릭합니다.

    ![직원 추가](./media/active-directory-saas-jiramicrosoft-tutorial/user3.png) 

5. Hello에 **"새 사용자 만들기"** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.

    ![직원 추가](./media/active-directory-saas-jiramicrosoft-tutorial/user4.png) 

    a. Hello에 **전자 메일 주소** textbox, 사용자의 hello 전자 메일 주소를 입력 같은 Brittasimon@contoso.com합니다.

    b. Hello에 **전체 이름을** 텍스트 형식 Britta Simon 같은 hello 사용자의 전체 이름입니다.

    c. Hello에 **Username** 텍스트 형식 hello 전자 메일 사용자의 같은 Brittasimon@contoso.com합니다.

    d. Hello에 **암호** textbox, 사용자의 hello 암호를 입력 합니다.

    e. **사용자 만들기**를 클릭합니다.   

### <a name="assigning-hello-azure-ad-test-user"></a>Azure AD hello 테스트 사용자를 할당합니다.

이 섹션에서는 액세스 tooJIRA Microsoft에서 SAML SSO를 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.

![사용자 할당][200] 

**tooassign Britta Simon tooJIRA microsoft에서 SAML SSO hello 다음 단계를 수행 합니다.**

1. Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.

    ![사용자 할당][201] 

2. Hello 응용 프로그램 목록에서 선택 **Microsoft에서 JIRA SAML SSO**합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_app.png) 

3. Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.

    ![사용자 할당][202] 

4. **추가** 단추를 클릭합니다. 그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.

    ![사용자 할당][203]

5. **사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.

6. **사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.

7. **할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.
    
### <a name="testing-single-sign-on"></a>Single Sign-On 테스트

이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.

Microsoft 타일 hello 액세스 패널에에서 의해 hello JIRA SAML SSO를 클릭할 때 자동으로 로그온 tooyour JIRA SAML SSO Microsoft 응용 프로그램에서 가져와야 합니다.
액세스 패널 hello에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.

## <a name="additional-resources"></a>추가 리소스

* [방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와](active-directory-saas-tutorial-list.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_203.png

