---
title: "자습서: Optimizely와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Optimizely 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28ef03e1-9aad-4301-af97-d94e853edc74
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 868aefae27ca155d2963f3dcfcd79bbb564b48ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-optimizely"></a>자습서: Optimizely와 Azure Active Directory 통합

이 자습서에 설명 어떻게 toointegrate Optimizely Azure Active directory (Azure AD).

다음 이점을 hello로 제공 Optimizely Azure AD와 통합:

- 액세스 tooOptimizely을 지닌 Azure AD에서 제어할 수 있습니다.
- 프로그램 사용자 tooautomatically get 로그온 tooOptimizely (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.
- 하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.

Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.

## <a name="prerequisites"></a>필수 조건

다음 항목 hello가 필요 tooconfigure Optimizely와 Azure AD 통합 합니다.

- Azure AD 구독
- Optimizely Single Sign-On이 설정된 구독

> [!NOTE]
> 이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.

이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.

- 꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.
- Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.

## <a name="scenario-description"></a>시나리오 설명
이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다. 이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.

1. Optimizely는 hello 갤러리 추가
2. Azure AD Single Sign-on 구성 및 테스트

## <a name="adding-optimizely-from-hello-gallery"></a>Optimizely는 hello 갤러리 추가
tooconfigure hello와의 통합 Optimizely Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Optimizely tooadd가 필요합니다.

**hello 갤러리에서 Optimizely tooadd hello 다음 단계를 수행 합니다.**

1. Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다. 

    ![Active Directory][1]

2. 너무 이동**엔터프라이즈 응용 프로그램**합니다. 이동 하 여 너무**모든 응용 프로그램**합니다.

    ![응용 프로그램][2]
    
3. tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.

    ![응용 프로그램][3]

4. Hello 검색 상자에 입력 **Optimizely**합니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_search.png)

5. Hello 결과 패널에서 선택 **Optimizely**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Azure AD Single Sign-on 구성 및 테스트
이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Optimizely에서 Azure AD Single Sign-On을 구성하고 테스트합니다.

Single sign on toowork에 대 한 Azure AD는 tooknow Optimizely에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다. 즉, Azure AD 사용자 및 Optimizely에 hello 관련된 사용자 간 링크 관계를 설정할 toobe가 필요 합니다.

Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** Optimizely에 합니다.

tooconfigure 및 Optimizely 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.

1. **[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.
2. **[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.
3. **[Optimizely 테스트 사용자 만들기](#creating-an-optimizely-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 Optimizely에 해당 하는 도구입니다.
4. **[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.
5. **[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성

이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 Optimizely 응용 프로그램에서 single sign on 구성 합니다.

**tooconfigure Azure AD single sign on, Optimizely와 hello 다음 단계를 수행 합니다.**

1. Hello hello에 Azure 포털에서에서 **Optimizely** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.

    ![Single Sign-on 구성][4]

2. Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.
 
    ![Single Sign-on 구성](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_samlbase.png)

3. Hello에 **Optimizely 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_url.png)

    a. Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://app.optimizely.net/<instance name>`

    b. Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`urn:auth0:optimizely:contoso`

    > [!NOTE] 
    > 이러한 값은 실제 hello 되지 않습니다. Hello 실제 로그온 URL 및 hello 자습서의 뒷부분에 설명 된 식별자를 가진 hello 값을 업데이트 합니다. 

4. Hello에 **SAML 서명 인증서** 섹션에서 클릭 **Certificate(Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_certificate.png) 

5. **저장** 단추를 클릭합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-optimizely-tutorial/tutorial_general_400.png)

6. Hello에 **Optimizely 구성** 섹션에서 클릭 **구성 Optimizely** tooopen **sign on 구성** 창. 복사 hello **SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**

    ![Single Sign-on 구성](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_configure.png) 

7. tooconfigure single sign on에서 **Optimizely** 쪽 Optimizely 계정 관리자에 게 문의 하 고, 다운로드 한 hello **인증서 (Base64)**, 및 **SAML Single Sign-on 서비스 URL** . 

8. 응답 tooyour 전자 메일에서 Optimizely 하면 로그온 URL (SP에서 시작한 SSO) hello 및 hello 식별자 (서비스 공급자 엔터티 ID) 값 있습니다.

    a. 복사 hello **SP 시작 SSO URL** Optimizely, 및 붙여넣기 hello에 의해 제공 된 **로그온 URL** 텍스트 상자로 **Optimizely 도메인 및 Url** Azure 포털에서 섹션 

    b. 복사 hello **서비스 공급자 엔터티 ID가** Optimizely, 및 붙여넣기 hello에 의해 제공 된 **식별자** 텍스트 상자로 **Optimizely 도메인 및 Url** Azure 포털에서 섹션 

9. 다른 브라우저 창에서 로그온 tooyour Optimizely 응용 프로그램입니다.

10. Hello top에 이름 오른쪽 모서리에 있는 계정을 클릭 한 다음 **계정 설정**합니다.
   
    ![Azure AD Single Sign-On](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_09.png)

11. Hello 계정 탭에 확인란 hello **SSO 사용** 에서 Single Sign On hello에 **개요** 섹션.
   
    ![Azure AD Single Sign-On](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_10.png)
    
12. 페이지 맨 아래에 있는 **저장**

> [!TIP]
> 이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!  Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션. 자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Azure AD 테스트 사용자 만들기
이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.

![Azure AD 사용자 만들기][100]

**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**

1. Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-optimizely-tutorial/create_aaduser_01.png) 

2. 사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-optimizely-tutorial/create_aaduser_02.png) 

3. tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-optimizely-tutorial/create_aaduser_03.png) 

4. Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-optimizely-tutorial/create_aaduser_04.png) 

    a. Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.

    b. Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** Britta Simon의 합니다.

    c. 선택 **암호 표시** hello hello 값 기록 **암호**합니다.

    d. **만들기**를 클릭합니다.
 
### <a name="creating-an-optimizely-test-user"></a>Optimizely 테스트 사용자 만들기

이 섹션에서는 Optimizely에서 Britta Simon이라는 사용자를 만듭니다.

1. Hello 홈 페이지에서 선택 **공동 작업자** 탭 합니다.

2. tooadd 새 공동 작업자 toohello 프로젝트 클릭 **새 공동 작업자**합니다.
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-optimizely-tutorial/create_aaduser_10.png)

3. Hello 전자 메일 주소 입력 한 역할을 할당 합니다. **초대**를 클릭합니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-optimizely-tutorial/create_aaduser_11.png)

4. 테스트 사용자는 이메일 초대를 받게 됩니다. Toolog tooOptimizely에서 권한이 hello 전자 메일 주소를 사용 합니다.

### <a name="assigning-hello-azure-ad-test-user"></a>Azure AD hello 테스트 사용자를 할당합니다.

이 섹션에서는 tooOptimizely 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.

![사용자 할당][200] 

**tooassign Britta Simon tooOptimizely hello 다음 단계를 수행 합니다.**

1. Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.

    ![사용자 할당][201] 

2. Hello 응용 프로그램 목록에서 선택 **Optimizely**합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_app.png) 

3. Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.

    ![사용자 할당][202] 

4. **추가** 단추를 클릭합니다. 그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.

    ![사용자 할당][203]

5. **사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.

6. **사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.

7. **할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.
    
### <a name="testing-single-sign-on"></a>Single Sign-On 테스트

이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.

Hello 액세스 패널에서에서 hello Optimizely 타일을 클릭할 때 자동으로 로그온 tooyour Optimizely 응용 프로그램을 구해야 합니다. 

## <a name="additional-resources"></a>추가 리소스

* [방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와](active-directory-saas-tutorial-list.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_203.png

