---
title: "자습서: Workday와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Workday 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e9da692e-4a65-4231-8ab3-bc9a87b10bca
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: aaa41e372e45f464c4540a70fc79c98dbc06d6b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workday"></a>자습서: Workday와 Azure Active Directory 통합

이 자습서에 설명 어떻게 toointegrate Workday Azure Active directory (Azure AD).

Azure AD와 Workday 통합 이점을 다음 hello로 제공 합니다.

- 액세스 tooWorkday을 지닌 Azure AD에서 제어할 수 있습니다.
- 프로그램 사용자 tooautomatically get 로그온 tooWorkday (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.
- 하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.

Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.

## <a name="prerequisites"></a>필수 조건

Azure AD 및 Workday 통합 tooconfigure 다음 항목 hello가 필요 합니다.

- Azure AD 구독
- Workday Single Sign-On이 설정된 구독

> [!NOTE]
> 이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.

이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.

- 꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.
- Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.

## <a name="scenario-description"></a>시나리오 설명
이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다. 이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.

1. Workday는 hello 갤러리 추가
2. Azure AD Single Sign-on 구성 및 테스트

## <a name="adding-workday-from-hello-gallery"></a>Workday는 hello 갤러리 추가
tooconfigure hello와의 통합 Workday Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 tooadd Workday 해야 있습니다.

**hello 갤러리에서 Workday tooadd hello 다음 단계를 수행 합니다.**

1. Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다. 

    ![Active Directory][1]

2. 너무 이동**엔터프라이즈 응용 프로그램**합니다. 이동 하 여 너무**모든 응용 프로그램**합니다.

    ![응용 프로그램][2]
    
3. tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.

    ![응용 프로그램][3]

4. Hello 검색 상자에 입력 **Workday**합니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-workday-tutorial/tutorial_workday_search.png)

5. Hello 결과 패널에서 선택 **Workday**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-workday-tutorial/tutorial_workday_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Azure AD Single Sign-on 구성 및 테스트
이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Workday에서 Azure AD Single Sign-On을 구성하고 테스트합니다.

Single sign on toowork에 대 한 Azure AD는 tooknow Workday의 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다. 즉, Azure AD 사용자 및 Workday의 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.

Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** Workday의 합니다.

tooconfigure 및 근무 시간을 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.

1. **[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.
2. **[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.
3. **[Workday 테스트 사용자 만들기](#creating-a-workday-test-user)**  -toohave Britta Simon 표현인 연결 된 toohello Azure AD 사용자의 업무 시간에 해당 하는 도구입니다.
4. **[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.
5. **[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성

이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 Workday 응용 프로그램에서 single sign on 구성 합니다.

**tooconfigure Azure AD single sign on, workday hello 다음 단계를 수행 합니다.**

1. Hello hello에 Azure 포털에서에서 **Workday** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.

    ![Single Sign-on 구성][4]

2. Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.
 
    ![Single Sign-on 구성](./media/active-directory-saas-workday-tutorial/tutorial_workday_samlbase.png)

3. Hello에 **Workday 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-workday-tutorial/tutorial_workday_url.png)

    a. Hello에 **로그온 URL** 형식 hello 값으로 텍스트 상자:`https://impl.workday.com/<tenant>/login-saml2.htmld`

    b. Hello에 **회신 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://impl.workday.com/<tenant>/login-saml.htmld`

    > [!NOTE] 
    > 이러한 값은 실제 hello 되지 않습니다. Hello 실제 로그온 URL와 회신 URL이 이러한 값을 업데이트 합니다. 회신 URL에 하위 도메인(예: www, wd2, wd3, wd3-impl, wd5, wd5-impl)이 있어야 합니다. "*http://www.myworkday.com*"과 같은 것은 작동하지만 "*http://myworkday.com*"은 작동하지 않습니다. 연락처 [클라이언트 Workday 지원 팀](https://www.workday.com/en-us/partners-services/services/support.html) tooget 이러한 값입니다. 
 

4. Hello에 **SAML 서명 인증서** 섹션에서 클릭 **인증서 (Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-workday-tutorial/tutorial_workday_certificate.png) 

5. **저장** 단추를 클릭합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-workday-tutorial/tutorial_general_400.png)

6. Hello에 **Workday 구성** 섹션에서 클릭 **Workday 구성** tooopen **sign on 구성** 창. 복사 hello **Sign-Out URL, SAML 엔터티 ID, 및 SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**

    ![Single Sign-On 구성](./media/active-directory-saas-workday-tutorial/tutorial_workday_configure.png) 
<CS>
7. 다른 웹 브라우저 창에서 관리자 권한으로 tooyour Workday 회사 사이트에 로그인 합니다.

8. 너무 이동**메뉴 \> 워크 벤치**합니다.
   
    ![워크벤치](./media/active-directory-saas-workday-tutorial/IC782923.png "워크벤치")

9. 너무 이동**계정 관리**합니다.
   
    ![계정 관리](./media/active-directory-saas-workday-tutorial/IC782924.png "계정 관리")

10. 너무 이동**테 넌 트 설정 편집-보안**합니다.
   
    ![테넌트 보안 편집](./media/active-directory-saas-workday-tutorial/IC782925.png "테넌트 보안 편집")

11. Hello에 **리디렉션 Url** 섹션를 hello 다음 단계를 수행 합니다.
   
    ![리디렉션 URL](./media/active-directory-saas-workday-tutorial/IC7829581.png "리디렉션 URL")
   
    a. **행 추가**를 클릭합니다.
   
    b. Hello에 **로그인 리디렉션 URL** 텍스트 상자 및 hello **모바일 리디렉션 URL** 텍스트 형식 hello **로그온 URL** hello에 입력 한 **Workday 도메인 및 Url** hello Azure 포털의 섹션입니다.
   
    c. Hello hello에 Azure 포털에서에서 **sign on 구성** 창, 복사 hello **Sign-Out URL**, 다음 hello에 붙여 넣는 **로그 아웃 리디렉션 URL** 텍스트 상자에 붙여넣습니다.
   
    d.  **환경** 형식 hello 환경 이름 텍스트 상자입니다.  

    >[!NOTE]
    > hello hello 환경 특성의 값은 연결 되어 hello 테 넌 트 URL의 toohello 값:  
    >-Hello Workday 테 넌 트 URL의 hello 도메인 이름이 impl로 예를 들어 시작: *https://impl.workday.com/\<테 넌 트\>/login-saml2.htmld*), hello **환경** 특성 tooImplementation 설정 되어야 합니다.  
    >-Hello 도메인 이름이 이와 다르게 시작, 해야 toocontact [클라이언트 Workday 지원 팀](https://www.workday.com/en-us/partners-services/services/support.html) tooget hello 일치 **환경** 값입니다.

12. Hello에 **SAML 설정** 섹션를 hello 다음 단계를 수행 합니다.
   
    ![SAML 설정](./media/active-directory-saas-workday-tutorial/IC782926.png "SAML 설정")
   
    a.  **SAML 인증 사용**을 선택합니다.
   
    b.  **행 추가**를 클릭합니다.

13. Hello SAML Id 공급자 섹션에서에서 단계를 수행 하는 hello를 수행 합니다.
   
    ![SAML ID 공급자](./media/active-directory-saas-workday-tutorial/IC7829271.png "SAML ID 공급자")
   
    a. Hello Id 공급자 이름 텍스트 상자에 공급자 이름을 입력 합니다 (예: *SPInitiatedSSO*).
   
    b. Hello hello에 Azure 포털에서에서 **sign on 구성** 창, 복사 hello **SAML 엔터티 ID** 값을 복사한 다음 hello에 붙여 넣을 **발급자** 텍스트 상자에 붙여넣습니다.
   
    c. **Enable Workday Initiated Logout**(Workday에서 시작된 로그아웃 사용)을 선택합니다.
   
    d. Hello hello에 Azure 포털에서에서 **sign on 구성** 창, 복사 hello **Sign-Out URL** 값을 복사한 다음 hello에 붙여 넣을 **로그 아웃 요청 URL** 텍스트 상자에 붙여넣습니다.

    e. **ID 공급자 공개 키 인증서**를 클릭한 다음 **만들기**를 클릭합니다. 

    ![만들기](./media/active-directory-saas-workday-tutorial/IC782928.png "만들기")

    f. **x509 공개 키 만들기**를 클릭합니다. 

    ![만들기](./media/active-directory-saas-workday-tutorial/IC782929.png "만들기")


14. Hello에 **x509 공개 키 보기** 섹션를 hello 다음 단계를 수행 합니다. 
   
    ![x509 공개 키 보기](./media/active-directory-saas-workday-tutorial/IC782930.png "x509 공개 키 보기") 
   
    a. Hello에 **이름** 텍스트 상자에, 인증서 이름 입력 (예: *PPE\_SP*).
   
    b. Hello에 **Valid From** 텍스트 형식 hello 인증서의 특성 값에서 유효 합니다.
   
    c.  Hello에 **Valid To** 텍스트 상자에 인증서의 형식 hello 유효한 tooattribute 값입니다.
   
    > [!NOTE]
    > 날짜부터 유효 hello를 가져올 수 있으며 두 번 클릭 하 여 hello 다운로드 한 인증서에서 유효한 toodate hello 있습니다.  hello 날짜 hello 아래에 나열 됩니다 **세부 정보** 탭 합니다.
    > 
    >
   
    d.  메모장을 선택한 다음의 콘텐츠 복사 hello에서 e-64로 인코딩된 인증서를 엽니다.
   
    e.  Hello에 **인증서** 붙여넣기 hello 내용 클립보드의 텍스트입니다.
   
    f.  **확인**을 클릭합니다.

15. Hello 다음 단계를 수행 합니다. 
   
    ![SSO 구성](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguratio.png "SSO 구성")
   
    a.  Hello를 사용 하도록 설정 **x509 개인 키 쌍**합니다.
   
    b.  Hello에 **서비스 공급자 ID** 텍스트 상자에 **http://www.workday.com**합니다.
   
    c.  **SP가 시작한 SAML 인증 사용**을 선택합니다.
   
    d.  Hello hello에 Azure 포털에서에서 **sign on 구성** 창, 복사 hello **SAML Single Sign-on 서비스 URL** 값을 복사한 다음 hello에 붙여 넣을 **IdP SSO 서비스 URL** 텍스트 상자에 붙여넣습니다.
   
    e. **SP에서 시작한 인증 요청을 Deflate하지 않음**을 선택합니다.
   
    f. **인증 요청 서명 메서드**로 **SHA256**을 선택합니다. 
   
    ![인증 요청 서명 메서드](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguration.png "인증 요청 서명 메서드") 
   
    g. **확인**을 클릭합니다. 
   
    ![확인](./media/active-directory-saas-workday-tutorial/IC782933.png "확인")
<CE>

> [!TIP]
> 이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!  Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션. 자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)
>

### <a name="creating-an-azure-ad-test-user"></a>Azure AD 테스트 사용자 만들기
이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.

![Azure AD 사용자 만들기][100]

**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**

1. Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-workday-tutorial/create_aaduser_01.png) 

2. 사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-workday-tutorial/create_aaduser_02.png) 

3. tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-workday-tutorial/create_aaduser_03.png) 

4. Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-workday-tutorial/create_aaduser_04.png) 

    a. Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.

    b. Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.

    c. 선택 **암호 표시** hello hello 값 기록 **암호**합니다.

    d. **만들기**를 클릭합니다.
 
### <a name="creating-a-workday-test-user"></a>Workday 테스트 사용자 만들기

테스트 사용자가 Workday에 프로 비전 tooget 해야 toocontact hello [클라이언트 Workday 지원 팀](https://www.workday.com/en-us/partners-services/services/support.html)합니다.
hello [클라이언트 Workday 지원 팀](https://www.workday.com/en-us/partners-services/services/support.html) hello 사용자를 만듭니다.

### <a name="assigning-hello-azure-ad-test-user"></a>Azure AD hello 테스트 사용자를 할당합니다.

이 섹션에서는 tooWorkday 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.

![사용자 할당][200] 

**tooassign Britta Simon tooWorkday hello 다음 단계를 수행 합니다.**

1. Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.

    ![사용자 할당][201] 

2. Hello 응용 프로그램 목록에서 선택 **Workday**합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-workday-tutorial/tutorial_workday_app.png) 

3. Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.

    ![사용자 할당][202] 

4. **추가** 단추를 클릭합니다. 그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.

    ![사용자 할당][203]

5. **사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.

6. **사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.

7. **할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.
    
### <a name="testing-single-sign-on"></a>Single Sign-On 테스트

Single sign on 설정 tootest 원하는 hello 액세스 패널을 엽니다. 액세스 패널 hello에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.

## <a name="additional-resources"></a>추가 리소스

* [방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와](active-directory-saas-tutorial-list.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)
* [사용자 프로비저닝 구성](active-directory-saas-workday-inbound-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workday-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workday-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workday-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workday-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workday-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workday-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workday-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workday-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workday-tutorial/tutorial_general_203.png

