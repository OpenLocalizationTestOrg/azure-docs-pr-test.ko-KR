---
title: "자습서: Ariba와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Asana 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 837e38fe-8f55-475c-87f4-6394dc1fee2b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: jeedes
ms.openlocfilehash: 9ac35dedc809b2b3dfb461d92a5afb066ccdedde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-asana"></a>자습서: Asana와 Azure Active Directory 통합

이 자습서에 설명 어떻게 toointegrate Asana Azure Active directory (Azure AD).

다음 이점을 hello로 제공 Asana Azure AD와 통합:

- 액세스 tooAsana을 지닌 Azure AD에서 제어할 수 있습니다.
- 프로그램 사용자 tooautomatically get 로그온 tooAsana (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.
- 하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.

Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.

## <a name="prerequisites"></a>필수 조건

다음 항목 hello가 필요 tooconfigure Asana와 Azure AD 통합 합니다.

- Azure AD 구독
- Asana Single Sign-On이 설정된 구독

> [!NOTE]
> 이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.

이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.

- 꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.
- Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.

## <a name="scenario-description"></a>시나리오 설명
이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다. 이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.

1. Asana는 hello 갤러리 추가
2. Azure AD Single Sign-on 구성 및 테스트

## <a name="adding-asana-from-hello-gallery"></a>Asana는 hello 갤러리 추가
tooconfigure hello와의 통합 Asana Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Asana tooadd가 필요합니다.

**hello 갤러리에서 Asana tooadd hello 다음 단계를 수행 합니다.**

1. Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다. 

    ![hello Azure Active Directory 단추][1]

2. 너무 이동**엔터프라이즈 응용 프로그램**합니다. 이동 하 여 너무**모든 응용 프로그램**합니다.

    ![hello 엔터프라이즈 응용 프로그램 블레이드][2]
    
3. tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.

    ![hello 새 응용 프로그램 단추][3]

4. Hello 검색 상자에 입력 **Asana**선택, **Asana** 결과 패널에서 클릭 **추가** tooadd hello 응용 프로그램 단추입니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-asana-tutorial/tutorial_asana_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성 및 테스트

이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Asana에서 Azure AD Single Sign-On을 구성하고 테스트합니다.

Single sign on toowork에 대 한 Azure AD는 tooknow Asana에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다. 즉, Azure AD 사용자 및 Asana에 hello 관련된 사용자 간 링크 관계를 설정할 toobe가 필요 합니다.

Asana에서 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.

tooconfigure 및 Asana 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.

1. **[Azure AD Single Sign-on 구성](#configure-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.
2. **[Azure AD 테스트를 만들고](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.
3. **[Asana 테스트 사용자 만들기](#create-an-asana-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 Asana에 해당 하는 도구입니다.
4. **[Azure AD hello 테스트 사용자를 할당](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.
5. **[Single sign on 테스트](#test-single-sign-on)**  -tooverify 구성 works를 hello 여부.

### <a name="configure-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성

이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 Asana 응용 프로그램에서 single sign on 구성 합니다.

**tooconfigure Azure AD single sign on, Asana와 hello 다음 단계를 수행 합니다.**

1. Hello hello에 Azure 포털에서에서 **Asana** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.

    ![Single Sign-on 구성][4]

2. Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-asana-tutorial/tutorial_asana_samlbase.png)

3. Hello에 **Asana 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.

    ![Asana 도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-asana-tutorial/tutorial_asana_url.png)

    a. Hello에 **로그온 URL** textbox URL 입력:`https://app.asana.com/`

    b. Hello에 **식별자** 유형 값 텍스트 상자:`https://app.asana.com/`
 
4. Hello에 **SAML 서명 인증서** 섹션에서 클릭 **Certificate(Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.

    ![hello 인증서 다운로드 링크](./media/active-directory-saas-asana-tutorial/tutorial_asana_certificate.png)
    
5. **저장** 단추를 클릭합니다.

    ![Single Sign-On 구성 저장 단추](./media/active-directory-saas-asana-tutorial/tutorial_general_400.png)

6. Hello에 **Asana 구성** 섹션에서 클릭 **구성 Asana** tooopen **sign on 구성** 창. 복사 hello **SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**

    ![Asana 구성](./media/active-directory-saas-asana-tutorial/tutorial_asana_configure.png) 

7. 다른 브라우저 창에서 로그온 tooyour Asana 응용 프로그램입니다. tooconfigure Asana, hello의 오른쪽 위 모서리 hello 화면에 hello 작업 영역 이름을 클릭 하 여 액세스 hello 작업 영역 설정에서에서 s S. 그런 다음 **\<작업 영역 이름\> 설정**을 클릭합니다. 
   
    ![Asana SSO 설정](./media/active-directory-saas-asana-tutorial/tutorial_asana_09.png)

8. Hello에 **조직 설정** 창 클릭 **관리**합니다. 클릭 **멤버 SAML을 통해 로그인 해야** tooenable hello SSO 구성 합니다. hello hello 다음 단계를 수행 합니다.
   
    ![Single Sign-On 조직 설정 구성](./media/active-directory-saas-asana-tutorial/tutorial_asana_10.png)  

     a. Hello에 **로그인 페이지 URL** 텍스트 붙여넣기 hello **SAML Single Sign-on 서비스 URL**합니다.

     b. Azure 포털에서 다운로드 한 hello 인증서를 마우스 오른쪽 단추로 클릭 한 다음 메모장 이나 원하는 텍스트 편집기를 사용 하 여 hello 인증서 파일을 엽니다. Hello 간 hello 콘텐츠 복사 시작 및 끝 인증서 제목 hello 및 hello에 붙여 **X.509 인증서** 텍스트 상자에 붙여넣습니다.

9. **Save**를 클릭합니다. 너무 이동[SSO를 설정 하기 위한 Asana 가이드](https://asana.com/guide/help/premium/authentication#gl-saml) 추가 지원이 필요한 경우.

> [!TIP]
> 이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!  Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션. 자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Azure AD 테스트 사용자 만들기

이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.

![Azure AD 테스트 사용자 만들기][100]

**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**

1. Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.

    ![hello Azure Active Directory 단추](./media/active-directory-saas-asana-tutorial/create_aaduser_01.png) 

2. 사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.
    
    !["사용자 및 그룹" hello 및 "모든 사용자" 링크](./media/active-directory-saas-asana-tutorial/create_aaduser_02.png) 

3. tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-asana-tutorial/create_aaduser_03.png) 

4. Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.
 
    ![hello 추가 단추](./media/active-directory-saas-asana-tutorial/create_aaduser_04.png) 

    a. Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.

    b. Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.

    c. 선택 **암호 표시** hello hello 값 기록 **암호**합니다.

    d. **만들기**를 클릭합니다.
 
### <a name="create-an-asana-test-user"></a>Asana 테스트 사용자 만들기

이 섹션에서는 Asana에서 Britta Simon이라는 사용자를 만듭니다.

1. **Asana**, toohello 이동 **팀** hello 왼쪽된 창에서 섹션. Hello 클릭 및 단추에 서명 합니다. 
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-asana-tutorial/tutorial_asana_12.png) 

2. Hello 전자 메일을 입력 britta.simon@contoso.com 에 hello 텍스트 상자를 클릭 한 **초대**합니다.

3. **초대 보내기**를 클릭합니다. hello 새 사용자의 전자 메일 계정에 전자 메일을 받게 됩니다. 그녀가 toocreate 필요 하 고 hello 계정의 유효성을 검사 합니다.

### <a name="assign-hello-azure-ad-test-user"></a>Azure AD hello 테스트 사용자를 할당 합니다.

이 섹션에서는 tooAsana 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.

![Hello 사용자 역할 할당][200]

**tooassign Britta Simon tooAsana hello 다음 단계를 수행 합니다.**

1. Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.

    ![사용자 할당][201] 

2. Hello 응용 프로그램 목록에서 선택 **Asana**합니다.

    ![hello 응용 프로그램 목록에서 hello Asana 링크](./media/active-directory-saas-asana-tutorial/tutorial_asana_app.png) 

3. Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.

    ![hello "사용자 및 그룹" 링크][202]

4. **추가** 단추를 클릭합니다. 그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.

    ![hello 할당 추가 창][203]

5. **사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.

6. **사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.

7. **할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.
    
### <a name="test-single-sign-on"></a>Single Sign-On 테스트

이 섹션의 hello 목표 tootest 하면 Azure AD에서 single sign-on이 있습니다.

TooAsana 로그인 페이지로 이동 합니다. Hello 전자 메일 주소 텍스트 상자에 hello 전자 메일 주소 삽입 britta.simon@contoso.com합니다. Hello 암호 텍스트 상자 비워 두고 클릭 **로그인**합니다. 리디렉션된 tooAzure AD 로그인 페이지 됩니다. Azure AD 자격 증명을 완료합니다. 이제 Asana에 로그인되었습니다.

## <a name="additional-resources"></a>추가 리소스

* [방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와](active-directory-saas-tutorial-list.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-asana-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-asana-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-asana-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-asana-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-asana-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-asana-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-asana-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-asana-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-asana-tutorial/tutorial_general_203.png
[10]: ./media/active-directory-saas-asana-tutorial/tutorial_general_060.png
[11]: ./media/active-directory-saas-asana-tutorial/tutorial_general_070.png
