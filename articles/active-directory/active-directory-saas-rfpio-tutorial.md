---
title: "자습서: RFPIO와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 RFPIO 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 87187076-7b50-4247-814f-f217b052703f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: e0c692276276edd8f859e73d81cf54d75a65957a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rfpio"></a>자습서: RFPIO와 Azure Active Directory 통합

이 자습서에 설명 어떻게 toointegrate RFPIO Azure Active directory (Azure AD).

다음 이점을 hello로 제공 RFPIO Azure AD와 통합:

- 액세스 tooRFPIO을 지닌 Azure AD에서 사용자를 제어할 수 있습니다.
- 에 사용자가 tooautomatically get 로그온 tooRFPIO (Single Sign-on)는 Azure AD 계정으로 설정할 수 있습니다.
- 하나의 중앙 위치-hello Azure 포털에서 계정을 관리할 수 있습니다.

Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.

## <a name="prerequisites"></a>필수 조건

다음 항목 hello가 필요 tooconfigure RFPIO와 Azure AD 통합 합니다.

- Azure AD 구독
- RFPIO Single Sign-on이 설정된 구독

> [!NOTE]
> 이 자습서에서는 프로덕션 환경 tootest hello 단계를 사용 하지 않는 것이 좋습니다.

이 자습서의 tootest hello 단계에는 이러한 권장 사항을 따르십시오.

- 꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.
- Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.

## <a name="scenario-description"></a>시나리오 설명
이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다. 이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.

1. Hello 갤러리에서 RFPIO를 추가 합니다.
2. Azure AD Single Sign-on 구성 및 테스트

## <a name="add-rfpio-from-hello-gallery"></a>RFPIO hello 갤러리 추가
tooconfigure hello와의 통합 RFPIO Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 RFPIO tooadd가 필요합니다.

### <a name="tooadd-rfpio-from-hello-gallery"></a>tooadd RFPIO hello 갤러리에서

1. Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 창의 hello, hello 선택 **Azure Active Directory** 아이콘입니다. 

    ![Active Directory][1]

2. **엔터프라이즈 응용 프로그램**을 선택한 다음 **모든 응용 프로그램**을 선택합니다.

    ![응용 프로그램][2]
    
3. tooadd 새 응용 프로그램을 선택 하는 hello **새 응용 프로그램** hello 대화 상자 위쪽에 단추입니다.

    ![응용 프로그램][3]

4. Hello 검색 상자에 입력 **RFPIO**합니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_search.png)

5. Hello 결과 패널에서 선택 **RFPIO**를 선택한 후 hello **추가** tooadd hello 응용 프로그램 단추입니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성 및 테스트
이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 RFPIO에서 Azure AD Single Sign-On을 구성하고 테스트합니다.

Single sign on toowork에 대 한 Azure AD는 tooknow RFPIO에서 테이블에 해당 사용자와 Azure AD에서 사용자 간에 어떤 hello 관계는 필요 합니다. 즉, Azure AD 사용자 및 RFPIO에 hello 관련된 사용자 간 링크 관계를 설정할 toobe가 필요 합니다.

RFPIO에서 hello 값을 할당 **사용자 이름** 의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.

tooconfigure 및 RFPIO 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.

1. **[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**-tooenable 사용자 toouse이이 기능입니다.
2. **[Azure AD 테스트를 만들고](#creating-an-azure-ad-test-user)**-Britta Simon와 Azure AD에서 single sign-on tootest 합니다.
3. **[RFPIO 테스트 사용자 만들기](#creating-a-rfpio-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 RFPIO에 해당 하는 도구입니다.
4. **[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**-tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.
5. **[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify hello 구성이 작동 합니다.

### <a name="configure-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성

이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 RFPIO 응용 프로그램에서 single sign on 구성 합니다.

**tooconfigure Azure AD single sign on, RFPIO와 hello 다음 단계를 수행 합니다.**

1. Hello hello에 Azure 포털에서에서 **RFPIO** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.

    ![Single Sign-on 구성][4]

2. Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.
 
    ![Single Sign-on 구성](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_samlbase.png)

3. Hello에 **RFPIO 도메인 및 Url** tooconfigure hello 응용 프로그램에 필요한 경우 섹션 **IDP** 시작 모드:

    ![Single Sign-on 구성](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url.png)

    a. Hello에 **식별자** textbox hello URL 입력:`https://www.rfpio.com`

    ![Single Sign-on 구성](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url1.png)

    b. **고급 URL 설정 표시**를 선택합니다.

    c. Hello에 **릴레이 상태** 텍스트 상자에 문자열 값을 입력 합니다. 연락처 [RFPIO 지원 팀](https://www.rfpio.com/contact/) tooget이이 값입니다. 

4. **고급 URL 설정 표시**를 선택합니다. Tooconfigure hello 응용 프로그램에 필요한 경우 **SP** 시작 모드:   

    ![Single Sign-on 구성](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url2.png)

    Hello에 **로그온 URL** textbox hello URL 입력:`https://www.app.rfpio.com`

5. Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello 메타 데이터 파일을 컴퓨터에 저장 합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_certificate.png) 

6. **저장** 단추를 클릭합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-rfpio-tutorial/tutorial_general_400.png)

7. 로그인 toohello 다른 웹 브라우저 창에서 **RFPIO** 관리자 권한으로 웹 사이트입니다.

8. Hello 하단 왼쪽된 모서리 드롭다운을 클릭 합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-rfpio-tutorial/app1.png)

9. Hello 클릭 **조직 설정**합니다. 

    ![Single Sign-on 구성](./media/active-directory-saas-rfpio-tutorial/app2.png)

10. Hello 클릭 **기능 및 통합**합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-rfpio-tutorial/app4.png)

11. Hello에 **SAML SSO 구성** 클릭 **편집**합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-rfpio-tutorial/app3.png)

12. 이 섹션에서 다음 작업을 수행합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-rfpio-tutorial/app5.png)
    
    a. Hello의 hello 콘텐츠 복사 **다운로드 한 메타 데이터 XML** hello에 붙여 넣습니다 **id 구성** 필드입니다.

    > [!NOTE]
    >toocopy hello의 콘텐츠 다운로드 **메타 데이터 XML** 사용 **메모장 + +** 또는 적절 한 **XML 편집기**합니다. 

    b. **유효성 검사**를 클릭합니다.

    c. 클릭 한 후 **유효성 검사**플립, **SAML(Enabled)** tooon 합니다.

    d. **제출**을 클릭합니다.

> [!TIP]
> 이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!  Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션. 자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Azure AD 테스트 사용자 만들기
이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.

![Azure AD 사용자 만들기][100]

**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**

1. Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-rfpio-tutorial/create_aaduser_01.png) 

2. 사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-rfpio-tutorial/create_aaduser_02.png) 

3. tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-rfpio-tutorial/create_aaduser_03.png) 

4. Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-rfpio-tutorial/create_aaduser_04.png) 

    a. Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.

    b. Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.

    c. 선택 **암호 표시** hello hello 값 기록 **암호**합니다.

    d. **만들기**를 클릭합니다.
 
### <a name="create-a-rfpio-test-user"></a>RFPIO 테스트 사용자 만들기

tooenable Azure AD 사용자가 toolog tooRFPIO에서 이러한 해야에 프로 비전 RFPIO 합니다.  
Hello RFPIO의 경우에서 프로 비전은 수동 작업입니다.

**tooprovision 사용자 계정을 hello 다음 단계를 수행 합니다.**

1. 관리자 권한으로 RFPIO 회사 사이트 tooyour에 로그인 합니다.

2. Hello 하단 왼쪽된 모서리 드롭다운을 클릭 합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-rfpio-tutorial/app1.png)

3. Hello 클릭 **조직 설정**합니다. 

    ![Single Sign-on 구성](./media/active-directory-saas-rfpio-tutorial/app2.png)

4. **TEAM MEMBERS**(팀 멤버)를 클릭합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-rfpio-tutorial/app6.png)

5. **멤버 추가**를 클릭합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-rfpio-tutorial/app7.png)

6. Hello에 **새 멤버 추가** 섹션. 다음 작업을 수행합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-rfpio-tutorial/app8.png)

    a. Enter **전자 메일 주소** hello에 **줄당 하나의 전자 메일을 입력** 필드입니다.

    b. 요구 사항에 따라 **역할**을 선택합니다.

    c. **멤버 추가**를 클릭합니다.
        
    > [!NOTE]
    > hello Azure Active Directory 계정 소유자는 전자 메일을 수신 하을 따라 활성화 링크 tooconfirm 자신의 계정의 따릅니다.

### <a name="assign-hello-azure-ad-test-user"></a>Azure AD hello 테스트 사용자를 할당 합니다.

이 섹션에서는 tooRFPIO 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.

![사용자 할당][200] 

**tooassign Britta Simon tooRFPIO hello 다음 단계를 수행 합니다.**

1. Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.

    ![사용자 할당][201] 

2. Hello 응용 프로그램 목록에서 선택 **RFPIO**합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_app.png) 

3. Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.

    ![사용자 할당][202] 

4. **추가** 단추를 클릭합니다. 그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.

    ![사용자 할당][203]

5. **사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.

6. **사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.

7. **할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.
    
### <a name="test-single-sign-on"></a>Single Sign-On 테스트

이 섹션에서는 hello 액세스 패널을 사용 하 여 Azure AD single sign on 구성을 테스트 합니다.

Hello RFPIO hello 액세스 패널에서에서 타일을 클릭할 때 자동으로 로그온 tooyour RFPIO 응용 프로그램을 구해야 합니다.
액세스 패널에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.

## <a name="additional-resources"></a>추가 리소스

* [방법에 대 한 자습서 목록 toointegrate SaaS 앱 Azure Active Directory와](active-directory-saas-tutorial-list.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_203.png

