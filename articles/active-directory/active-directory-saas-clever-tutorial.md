---
title: "자습서: Clever와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Clever 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 069ff13a-310e-4366-a147-d6ec5cca12a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 24430e1e6c750efa5787561aa151201b1fe7d428
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clever"></a>자습서: Clever와 Azure Active Directory 통합

이 자습서에 설명 어떻게 toointegrate Clever Azure Active directory (Azure AD).

다음 이점을 hello로 제공 Clever Azure AD와 통합:

- 액세스 tooClever을 지닌 Azure AD에서 제어할 수 있습니다.
- 에 사용자가 tooautomatically get 로그온 tooClever (Single Sign-on)는 Azure AD 계정으로 설정할 수 있습니다.
- 하나의 중앙 위치-hello Azure 포털에서 계정을 관리할 수 있습니다.

Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.

## <a name="prerequisites"></a>필수 조건

다음 항목 hello가 필요 tooconfigure Clever와 Azure AD 통합 합니다.

- Azure AD 구독
- Clever Single Sign-on이 설정된 구독

> [!NOTE]
> 이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.

이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.

- 꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.
- Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.

## <a name="scenario-description"></a>시나리오 설명
이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다. 이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.

1. Clever는 hello 갤러리 추가
2. Azure AD Single Sign-on 구성 및 테스트

## <a name="adding-clever-from-hello-gallery"></a>Clever는 hello 갤러리 추가
tooconfigure hello와의 통합 Clever Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Clever tooadd가 필요합니다.

**hello 갤러리에서 Clever tooadd hello 다음 단계를 수행 합니다.**

1. Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다. 

    ![hello Azure Active Directory 단추][1]

2. 너무 이동**엔터프라이즈 응용 프로그램**합니다. 이동 하 여 너무**모든 응용 프로그램**합니다.

    ![hello 엔터프라이즈 응용 프로그램 블레이드][2]
    
3. tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.

    ![hello 새 응용 프로그램 단추][3]

4. Hello 검색 상자에 입력 **Clever**선택, **Clever** 결과 패널에서 클릭 **추가** tooadd hello 응용 프로그램 단추입니다.

    ![효과적인 hello 결과 목록에서](./media/active-directory-saas-clever-tutorial/tutorial_clever_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성 및 테스트

이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Clever에서 Azure AD Single Sign-On을 구성하고 테스트합니다.

Single sign on toowork에 대 한 Azure AD는 tooknow Clever에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다. 즉, Azure AD 사용자 및 Clever에 hello 관련된 사용자 간 링크 관계를 설정할 toobe가 필요 합니다.

Clever에서 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.

tooconfigure 및 Clever 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.

1. **[Azure AD Single Sign-on 구성](#configure-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.
2. **[Azure AD 테스트를 만들고](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.
3. **[효과적인 테스트 사용자 만들기](#create-a-clever-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 Clever에 해당 하는 도구입니다.
4. **[Azure AD hello 테스트 사용자를 할당](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.
5. **[Single sign on 테스트](#test-single-sign-on)**  -tooverify 구성 works를 hello 여부.

### <a name="configure-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성

이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 효과적인 응용 프로그램에서 single sign on 구성 합니다.

**tooconfigure Azure AD single sign on, Clever와 hello 다음 단계를 수행 합니다.**

1. Hello hello에 Azure 포털에서에서 **Clever** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.

    ![Single Sign-On 구성 링크][4]

2. Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-clever-tutorial/tutorial_clever_samlbase.png)

3. Hello에 **효과적인 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.

    ![Clever 도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-clever-tutorial/tutorial_clever_url.png)

    a. Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://clever.com/in/<companyname>`

    b. Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://clever.com/<companyname>`

    > [!NOTE] 
    > 이러한 값은 실제 값이 아닙니다. 이러한 항목을 업데이트 로그온 URL과 식별자 실제 hello로 값입니다. 연락처 [효과적인 클라이언트 지원 팀](https://clever.com/about/contact/) tooget 이러한 값입니다.

4. Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello 메타 데이터 파일을 컴퓨터에 저장 합니다.

    ![hello 인증서 다운로드 링크](./media/active-directory-saas-clever-tutorial/tutorial_clever_certificate.png)

5. hello 효과적인 응용 프로그램에는 사용자 지정 특성 매핑을 tooyour tooadd 요구 하는 특정 형식으로 hello SAML 어설션이 **SAML 토큰 특성** 구성 합니다.

    다음 스크린 샷 hello이에 대 한 예가 나와 있습니다.

    ![Single Sign-on 구성](./media/active-directory-saas-clever-tutorial/tutorial_clever_07.png) 

6. Hello에 **사용자 특성** hello 섹션 **Single sign on** 대화 상자에서 위의 hello 이미지에 나와 있는 것 처럼 SAML 토큰 특성을 구성 하 고 hello 다음 단계를 수행 합니다.
    
    | 특성 이름  | 특성 값 |
    | --------------- | -------------------- |    
    | clever.student.credentials.district\_username  | user.userprincipalname |
    | firstname  | user.givenname |
    | Lastname  | user.surname |    

    a. 클릭 **특성 추가** tooopen hello **특성 추가** 대화 상자.

    ![Single Sign-on 구성](./media/active-directory-saas-clever-tutorial/tutorial_attribute_04.png)
    
    ![Single Sign-on 구성](./media/active-directory-saas-clever-tutorial/tutorial_attribute_05.png)
    
    b. Hello에 **이름** textbox, 해당 행에 대 한 표시 형식 hello 특성 이름입니다.

    c. Hello에서 **값** 목록, 해당 행에 대 한 표시 유형 hello 특성 값입니다.

    d. Hello 둡니다 **Namespace** 빈 텍스트 상자에 붙여넣습니다.
    
    d. **Ok**를 클릭합니다.     

5. **저장** 단추를 클릭합니다.

    ![Single Sign-On 구성 저장 단추](./media/active-directory-saas-clever-tutorial/tutorial_general_400.png)

8. toogenerate hello **메타 데이터** url hello 다음 단계를 수행 합니다.

    a. **앱 등록**을 클릭합니다.
    
    ![Single Sign-on 구성](./media/active-directory-saas-clever-tutorial/tutorial_clever_appregistrations.png)
   
    b. 클릭 **끝점** tooopen **끝점** 대화 상자.  
    
    ![Single Sign-on 구성](./media/active-directory-saas-clever-tutorial/tutorial_clever_endpointicon.png)

    c. Hello 복사 단추 toocopy 클릭 **페더레이션 메타 데이터 문서** url 메모장에 붙여 넣습니다.
    
    ![Single Sign-on 구성](./media/active-directory-saas-clever-tutorial/tutorial_clever_endpoint.png)
     
    d. 이제의 toohello 속성 페이지를 이동 **Clever** 및 복사 hello **응용 프로그램 Id** 를 사용 하 여 **복사** 단추를 메모장에 붙여 넣습니다.
 
    ![Single Sign-on 구성](./media/active-directory-saas-clever-tutorial/tutorial_clever_appid.png)

    e. Hello 생성 **메타 데이터 URL** hello 패턴을 사용 하 여:`<FEDERATION METADATA DOCUMENT url>?appid=<application id>`   

9. 다른 웹 브라우저 창에서 관리자 권한으로 tooyour 효과적인 회사 사이트에 로그인 합니다.

10. Hello 도구 모음에서 클릭 **즉시 로그인**합니다.

    ![인스턴트 로그인](./media/active-directory-saas-clever-tutorial/ic798984.png "인스턴트 로그인")

11. Hello에 **즉시 로그인** 페이지 hello 다음 단계를 수행 합니다.
      
      ![인스턴트 로그인](./media/active-directory-saas-clever-tutorial/ic798985.png "인스턴트 로그인")
      
      a. 형식 hello **로그인 URL**합니다.
      
      >[!NOTE]
      >hello **로그인 URL** 는 사용자 지정 값입니다. 연락처 [효과적인 클라이언트 지원 팀](https://clever.com/about/contact/) tooget이이 값입니다.
      
      b. **ID 시스템**으로 **ADFS**를 선택합니다.

      c. 형식 hello **메타 데이터 URL** hello에 **메타 데이터 URL** 텍스트 상자에 붙여넣습니다.
      
      d. **Save**를 클릭합니다.

> [!TIP]
> 이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!  Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션. 자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Azure AD 테스트 사용자 만들기

이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.

   ![Azure AD 테스트 사용자 만들기][100]

**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**

1. Hello hello 왼쪽된 창에서 Azure 포털에서에서 클릭 hello **Azure Active Directory** 단추입니다.

    ![hello Azure Active Directory 단추](./media/active-directory-saas-clever-tutorial/create_aaduser_01.png)

2. 사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹**, 클릭 하 고 **모든 사용자가**합니다.

    !["사용자 및 그룹" hello 및 "모든 사용자" 링크](./media/active-directory-saas-clever-tutorial/create_aaduser_02.png)

3. tooopen hello **사용자** 대화 상자를 클릭 **추가** hello hello 맨 **모든 사용자에 게** 대화 상자.

    ![hello 추가 단추](./media/active-directory-saas-clever-tutorial/create_aaduser_03.png)

4. Hello에 **사용자** 대화 상자를 hello 다음 단계를 수행 합니다.

    ![hello 사용자 대화 상자](./media/active-directory-saas-clever-tutorial/create_aaduser_04.png)

    a. Hello에 **이름** 상자에서 입력 **BrittaSimon**합니다.

    b. Hello에 **사용자 이름** 상자의 사용자 Britta Simon의 hello 전자 메일 주소를 입력 합니다.

    c. 선택 hello **암호 표시** 확인란을 선택한 다음 hello에 표시 되는 hello 값 기록 **암호** 상자입니다.

    d. **만들기**를 클릭합니다.
 
### <a name="create-a-clever-test-user"></a>Clever 테스트 사용자 만들기

tooenable Azure AD 사용자가 toolog tooClever에서 이러한 해야에 프로 비전 Clever 합니다.

작업할 Clever, 발생 한 경우 [효과적인 클라이언트 지원 팀](https://clever.com/about/contact/) hello 사용자 효과적인 플랫폼 hello에서 추가할 수 있습니다. Single Sign-On을 사용하려면 먼저 사용자를 만들고 활성화해야 합니다. 

>[!NOTE]
>다른 효과적인 사용자 계정 만들기 도구를 사용할 수 있습니다 또는 Azure AD 사용자 계정을 효과적인 tooprovision에서 제공 된 Api입니다.

### <a name="assign-hello-azure-ad-test-user"></a>Azure AD hello 테스트 사용자를 할당 합니다.

이 섹션에서는 tooClever 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.

![Hello 사용자 역할 할당][200] 

**tooassign Britta Simon tooClever hello 다음 단계를 수행 합니다.**

1. Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.

    ![사용자 할당][201] 

2. Hello 응용 프로그램 목록에서 선택 **Clever**합니다.

    ![hello Clever hello 응용 프로그램 목록에서 링크](./media/active-directory-saas-clever-tutorial/tutorial_clever_app.png)  

3. Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.

    ![hello "사용자 및 그룹" 링크][202]

4. **추가** 단추를 클릭합니다. 그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.

    ![hello 할당 추가 창][203]

5. **사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.

6. **사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.

7. **할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.
    
### <a name="test-single-sign-on"></a>Single Sign-On 테스트

이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.

Hello 효과적인 타일을 클릭할 때 hello 액세스 패널에서 자동으로 로그온 tooyour 효과적인 응용 프로그램을 얻어야 합니다.
액세스 패널에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다. 

## <a name="additional-resources"></a>추가 리소스

* [방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와](active-directory-saas-tutorial-list.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-clever-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clever-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clever-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clever-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clever-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clever-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clever-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clever-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clever-tutorial/tutorial_general_203.png

