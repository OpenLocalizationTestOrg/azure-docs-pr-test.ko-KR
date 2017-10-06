---
title: "자습서: Clarizen과 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Clarizen 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: f24ccda3b90e5df9a203a444dfda905043b30276
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clarizen"></a>자습서: Clarizen과 Azure Active Directory 통합

이 자습서에 설명 어떻게 toointegrate Clarizen로 Azure Active Directory (Azure AD). 이 통합에서는 다음과 같은 이점을 hello:

- 제어할 수 있습니다, 액세스 tooClarizen을 지닌 Azure AD에서.
- 자동으로 로그인 한 tooClarizen (single sign on)는 Azure AD 계정 사용 하 여 사용자가 toobe를 설정할 수 있습니다.
- 하나의 중앙 위치에 hello Azure 포털에서 계정을 관리할 수 있습니다.

이 자습서의 hello 시나리오의 두 가지 주요 작업으로 구성 됩니다.

1. Hello 갤러리에서 Clarizen을 추가 합니다.
2. Azure AD Single Sign-On을 구성하고 테스트합니다.

Azure AD와의 SaaS(Software as a Service) 앱 통합에 대한 자세한 내용은 [Azure Active Directory를 사용한 응용 프로그램 액세스 및 Single Sign-On](active-directory-appssoaccess-whatis.md)을 참조하세요.

## <a name="prerequisites"></a>필수 조건
Clarizen와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.

- Azure AD 구독
- Single Sign-On이 활성화된 Clarizen 구독

이 자습서의 tootest hello 단계에는 이러한 권장 사항을 따르십시오.

- 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다. 꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마십시오.
- Azure AD 테스트 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.

## <a name="add-clarizen-from-hello-gallery"></a>Clarizen hello 갤러리 추가
Clarizen의 tooconfigure hello 통합 Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Clarizen을 추가 합니다.

1. Hello에 [Azure 포털](https://portal.azure.com)hello 왼쪽된 창에서 클릭 hello **Azure Active Directory** 아이콘입니다.

    ![Azure Active Directory 아이콘][1]

2. **엔터프라이즈 응용 프로그램**을 클릭합니다. 그런 후 **모든 응용 프로그램**을 클릭합니다.

    ![“엔터프라이즈 응용 프로그램” 및 “모든 응용 프로그램” 클릭][2]

3. Hello 클릭 **추가** hello hello 대화 상자 위쪽에 단추입니다.

    ![hello "추가" 단추][3]

4. Hello 검색 상자에 입력 **Clarizen**합니다.

    !["Clarizen" hello 검색 상자에 입력](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_000.png)

5. Hello 결과 창에서 선택 **Clarizen**, 클릭 하 고 **추가** tooadd hello 응용 프로그램입니다.

    ![Clarizen hello 결과 창에서 선택](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_0001.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성 및 테스트
다음 섹션 hello, 구성 하 고와 Clarizen Britta Simon hello 테스트 사용자에 따라 Azure AD에서 single sign-on 테스트 합니다.

Single sign on toowork에 대 한 Azure AD는 tooknow Clarizen에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다. 즉, Azure AD 사용자와 Clarizen에 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다. Hello 값을 할당 하 여이 링크 관계를 설정할 **사용자 이름** 의 hello 값으로 Azure AD에서 **Username** Clarizen에 있습니다.

tooconfigure와 Clarizen 빌딩 블록을 다음 전체 hello 사용 하 여 Azure AD에서 single sign-on 테스트:

1. **[Azure AD single sign-on 구성](#configure-azure-ad-single-sign-on) ** tooenable 사용자 toouse이이 기능입니다.
2. **[Azure AD 테스트를 만들고](#create-an-azure-ad-test-user) ** Britta Simon와 Azure AD에서 single sign-on tootest 합니다.
3. **[Clarizen 테스트 사용자 만들기](#create-a-clarizen-test-user) ** toohave Britta Simon 그녀의 연결 된 Azure AD toohello 표현인 Clarizen에 해당 하는 도구입니다.
4. **[Azure AD hello 테스트 사용자를 할당](#assign-the-azure-ad-test-user) ** tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.
5. **[Single sign on 테스트](#test-single-sign-on) ** tooverify 구성 works를 hello 여부.

### <a name="configure-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성
Azure AD에서 single sign-on hello Azure 포털에서에서 사용 하도록 설정 하 고 Clarizen 응용 프로그램에서 single sign on 구성 합니다.

1. Hello hello에 Azure 포털에서에서 **Clarizen** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.

    !["Single sign-on" 클릭][4]

2. Hello에 **Single sign on** 대화 상자에 대 한 **모드**선택, **SAML 기반 로그온** tooenable single sign on입니다.

    !["SAML 기반 로그온" 선택](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_01.png)

3. Hello에 **Clarizen 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.

    ![식별자 및 회신 URL 상자](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_02.png)

    a. Hello에 **식별자** 으로 유형 hello 값 상자의: **Clarizen**

    b. Hello에 **회신 URL** hello 패턴을 사용 하 여 URL을 입력 합니다: **https://<company name>.clarizen.com/Clarizen/Pages/Integrations/SAML/SamlResponse.aspx**

    > [!NOTE]
    > 이들은 hello 실제 값입니다. Toouse hello 실제 id를 포함 하 고 회신 URL입니다. 여기 hello 식별자 대로 문자열 hello 고유 값을 사용 하는 것이 좋습니다. tooget hello 실제 값, 연락처 hello [Clarizen 지원 팀](https://success.clarizen.com/hc/en-us/requests/new)합니다.

4. Hello에 **SAML 서명 인증서** 섹션에서 클릭 **새 인증서 만들기**합니다.

    !["새 인증서 만들기" 클릭](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_03.png)  

5. Hello에 **새 인증서 만들기** 대화 상자, hello 달력 아이콘을 클릭 하 고 만료 날짜를 선택 합니다. 그런 다음 **Save**를 클릭합니다.

    ![만료 날짜 선택 및 저장](./media/active-directory-saas-clarizen-tutorial/tutorial_general_300.png)

6. Hello에 **SAML 서명 인증서** 섹션에서 **새 인증서를 활성화할**, 클릭 하 고 **저장**합니다.

    ![Hello 활성화 될 때 새 인증서 hello에 대 한 확인란을 선택 하면](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_04.png)

7. Hello에 **롤오버 인증서** 대화 상자를 클릭 **확인**합니다.

    ![원하는 toomake hello 인증서 활성 tooconfirm "확인"을 클릭 하면](./media/active-directory-saas-clarizen-tutorial/tutorial_general_400.png)

8. Hello에 **SAML 서명 인증서** 섹션에서 클릭 **인증서 (Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.

    !["(Base64) 인증서" toostart hello 다운로드를 클릭 하면](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_05.png)

9. Hello에 **Clarizen 구성** 섹션에서 클릭 **구성 Clarizen** tooopen hello **sign on 구성** 창.

    !["Clarizen 구성" 클릭](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_06.png)

    ![파일 및 URL을 포함하는 "로그온 구성" 창](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_07.png)

10. 다른 웹 브라우저 창에서 관리자 권한으로 tooyour Clarizen 회사 사이트에 로그인 합니다.

11. 사용자 이름을 클릭한 다음 **설정**을 클릭합니다.

    ![사용자 이름 아래에서 "설정" 클릭](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_001.png "설정")

12. Hello 클릭 **전역 설정** 탭 합니다. 그런 다음 다음 너무**페더레이션 인증**, 클릭 **편집**합니다.

    ![“전역 설정” 탭](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_002.png "전역 설정")

13. Hello에 **페더레이션 인증** 대화 상자를 hello 다음 단계를 수행 합니다.

    ![“페더레이션 인증” 대화 상자](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_003.png "페더레이션 인증")

    a. **페더레이션 인증 사용**을 선택합니다.

    b. 클릭 **업로드** tooupload 다운로드 한 인증서입니다.

    c. Hello에 **로그인 URL** 의 hello 값 입력 **SAML Single Sign-on 서비스 URL** hello Azure AD 응용 프로그램 구성 창에서.

    d. Hello에 **Sign-out URL** 의 hello 값 입력 **Sign-Out URL** hello Azure AD 응용 프로그램 구성 창에서.

    e. **POST 사용**을 선택합니다.

    f. **Save**를 클릭합니다.

### <a name="create-an-azure-ad-test-user"></a>Azure AD 테스트 사용자 만들기
Azure 포털 hello Britta Simon 이라는 테스트 사용자를 만듭니다.

![Azure AD hello 테스트 사용자의 이름 및 전자 메일 주소][100]

1. Hello hello 왼쪽된 창에서 Azure 포털에서에서 클릭 hello **Azure Active Directory** 아이콘입니다.

    ![Azure Active Directory 아이콘](./media/active-directory-saas-clarizen-tutorial/create_aaduser_01.png)

2. 클릭 **사용자 및 그룹**, 클릭 하 고 **모든 사용자에 게** 사용자 toodisplay hello 목록입니다.

    !["사용자 및 그룹" 및 "모든 사용자" 클릭](./media/active-directory-saas-clarizen-tutorial/create_aaduser_02.png)

3. Hello 대화 상자의 hello 위쪽 클릭 **추가** tooopen hello **사용자** 대화 상자.

    ![hello "추가" 단추](./media/active-directory-saas-clarizen-tutorial/create_aaduser_03.png)

4. Hello에 **사용자** 대화 상자를 hello 다음 단계를 수행 합니다.

    ![이름, 전자 메일 주소 및 암호가 입력된 "사용자" 대화 상자](./media/active-directory-saas-clarizen-tutorial/create_aaduser_04.png)

    a. Hello에 **이름** 상자에서 입력 **BrittaSimon**합니다.

    b. Hello에 **사용자 이름** 상자의의 hello Britta Simon 계정 hello 전자 메일 주소를 입력 합니다.

    c. 선택 **암호 표시** hello 값 기록 **암호**합니다.

    d. **만들기**를 클릭합니다.

### <a name="create-a-clarizen-test-user"></a>Clarizen 테스트 사용자 만들기
tooClarizen에 Azure AD 사용자가 toosign tooenable, 사용자 계정을 프로 비전 해야 합니다. Hello Clarizen의 경우에서 프로 비전은 수동 작업입니다.

1. 관리자 권한으로 Clarizen 회사 사이트 tooyour에 로그인 합니다.

2. **피플**을 클릭합니다.

    !["피플" 클릭](./media/active-directory-saas-clarizen-tutorial/create_aaduser_001.png "피플")

3. **사용자 초대**를 클릭합니다.

    !["사용자 초대" 단추](./media/active-directory-saas-clarizen-tutorial/create_aaduser_002.png "사용자 초대")

4. Hello에 **사용자 초대** 대화 상자를 hello 다음 단계를 수행 합니다.

    !["피플 초대" 대화 상자](./media/active-directory-saas-clarizen-tutorial/create_aaduser_003.png "피플 초대")

    a. Hello에 **전자 메일** 상자의의 hello Britta Simon 계정 hello 전자 메일 주소를 입력 합니다.

    b. **초대**를 클릭합니다.

    > [!NOTE]
    > hello Azure Active Directory 계정 소유자 전자 메일을 받게 되 고 링크 tooconfirm 자신의 계정을 활성화 되기 전에 수행 됩니다.

### <a name="assign-hello-azure-ad-test-user"></a>Azure AD hello 테스트 사용자를 할당 합니다.
그녀의 액세스 tooClarizen 권한을 부여 하 여 Britta Simon toouse Azure single sign on을 사용 합니다.

![할당된 테스트 사용자][200]

1. Azure 포털 hello hello 응용 프로그램 보기를 열고, toohello 디렉터리 보기 찾아보기를 클릭 **엔터프라이즈 응용 프로그램**, 클릭 하 고 **모든 응용 프로그램**합니다.

    ![“엔터프라이즈 응용 프로그램” 및 “모든 응용 프로그램” 클릭][201]

2. Hello 응용 프로그램 목록에서 선택 **Clarizen**합니다.

    ![Clarizen hello 목록에 선택](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_50.png)

3. Hello 왼쪽된 창에서 클릭 **사용자 및 그룹**합니다.

    ![“사용자 및 그룹” 클릭][202]

4. Hello 클릭 **추가** 단추입니다. 그런 다음, hello **할당 추가** 대화 상자에서 **사용자 및 그룹**합니다.

    ![hello "추가" 단추 및 hello "할당 추가" 대화 상자][203]

5. Hello에 **사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.

6. Hello에 **사용자 및 그룹** 대화 상자를 클릭 hello **선택** 단추입니다.

7. Hello에 **할당 추가** 대화 상자를 클릭 hello **할당** 단추입니다.

### <a name="test-single-sign-on"></a>Single Sign-On 테스트
Hello 액세스 패널을 사용 하 여 Azure AD single sign on 구성을 테스트 합니다.

Hello 액세스 패널에서에서 hello Clarizen 타일을 클릭 하면 해야 자동으로 로그인 될 tooyour Clarizen 응용 프로그램입니다.

## <a name="additional-resources"></a>추가 리소스

* [방법에 대 한 자습서 목록 toointegrate SaaS 앱 Azure Active Directory와](active-directory-saas-tutorial-list.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_203.png
