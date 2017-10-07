---
title: "자습서: SensoScientific Wireless Temperature Monitoring System과 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 SensoScientific 무선 온도 모니터링 시스템 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ee9a924d-ccde-45b0-ab40-877f82f5dfa2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: jeedes
ms.openlocfilehash: 4eabf7fc6457c217fd5c0c2539ab88c8110055e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sensoscientific-wireless-temperature-monitoring-system"></a>자습서: SensoScientific Wireless Temperature Monitoring System과 Azure Active Directory 통합

이 자습서에 설명 어떻게 toointegrate Azure Active Directory (Azure AD)와 SensoScientific 무선 온도 모니터링 시스템입니다.

다음 이점을 hello로 제공 SensoScientific 무선 온도 모니터링 시스템을 Azure AD와 통합:

- 액세스 tooSensoScientific 무선 온도 모니터링 시스템을 지닌 Azure AD에서 제어할 수 있습니다.
- Azure AD 계정을 사용 하면 사용자가 tooautomatically get 로그온 tooSensoScientific (Single Sign-on) 무선 온도 모니터링 시스템을 사용할 수 있습니다.
- 하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.

Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.

## <a name="prerequisites"></a>필수 조건

다음 항목 hello가 필요 tooconfigure SensoScientific 무선 온도 모니터링 시스템와 Azure AD 통합 합니다.

- Azure AD 구독
- SensoScientific Wireless Temperature Monitoring System Single Sign-On이 설정된 구독

> [!NOTE]
> 이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.

이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.

- 꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.
- Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.

## <a name="scenario-description"></a>시나리오 설명
이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다. 이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.

1. Hello 갤러리에서 SensoScientific 무선 온도 모니터링 시스템을 추가합니다.
2. Azure AD Single Sign-on 구성 및 테스트

## <a name="adding-sensoscientific-wireless-temperature-monitoring-system-from-hello-gallery"></a>Hello 갤러리에서 SensoScientific 무선 온도 모니터링 시스템을 추가합니다.
tooconfigure hello와의 통합 SensoScientific 무선 온도 모니터링 시스템 Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 SensoScientific 무선 온도 모니터링 시스템 tooadd가 필요합니다.

**hello 갤러리에서 SensoScientific 무선 온도 모니터링 시스템 tooadd hello 다음 단계를 수행 합니다.**

1. Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다. 

    ![Active Directory][1]

2. 너무 이동**엔터프라이즈 응용 프로그램**합니다. 이동 하 여 너무**모든 응용 프로그램**합니다.

    ![응용 프로그램][2]
    
3. tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.

    ![응용 프로그램][3]

4. Hello 검색 상자에 입력 **SensoScientific 무선 온도 모니터링 시스템**합니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_search.png)

5. Hello 결과 패널에서 선택 **SensoScientific 무선 온도 모니터링 시스템**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Azure AD Single Sign-on 구성 및 테스트
이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 SensoScientific Wireless Temperature Monitoring System에서 Azure AD Single Sign-On을 구성하고 테스트합니다.

Single sign on toowork에 대 한 Azure AD는 tooknow SensoScientific 무선 온도 모니터링 시스템에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다. 즉, Azure AD 사용자 및 hello SensoScientific 무선 온도 모니터링 시스템에서 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.

Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** SensoScientific 무선 온도 모니터링 시스템에서 합니다.

tooconfigure 및 SensoScientific 무선 온도 모니터링 시스템을 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.

1. **[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.
2. **[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.
3. **[SensoScientific 무선 온도 모니터링 시스템 테스트 사용자 만들기](#creating-a-sensoscientific-wireless-temperature-monitoring-system-test-user)**  -toohave Britta Simon SensoScientific 무선 온도 모니터링 시스템에는 상응 하는 연결의 Azure AD toohello 표현 사용자입니다.
4. **[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.
5. **[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성

이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 SensoScientific 무선 온도 모니터링 시스템 응용 프로그램에서 single sign on 구성 합니다.

**SensoScientific 무선 온도 모니터링 시스템에서는 Azure AD에서 single sign-on tooconfigure hello 다음 단계를 수행 합니다.**

1. Hello hello에 Azure 포털에서에서 **SensoScientific 무선 온도 모니터링 시스템** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.

    ![Single Sign-on 구성][4]

2. Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.
 
    ![Single Sign-on 구성](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_samlbase.png)

3. Hello에 **SensoScientific 무선 온도 모니터링 시스템 도메인 및 Url** 섹션 hello 응용 프로그램에 따라 단계는 Azure와 사전 통합 이미 필요 tooperform 없습니다:

    ![Single Sign-on 구성](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_url.png)

4. Hello에 **SAML 서명 인증서** 섹션에서 클릭 **Certificate(Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_certificate.png) 

5. **저장** 단추를 클릭합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_400.png)

6. Hello에 **SensoScientific 무선 온도 모니터링 시스템 구성** 섹션에서 클릭 **SensoScientific 무선 온도 모니터링 시스템 구성** tooopen  **Sign on 구성** 창. 복사 hello **Sign-Out URL, SAML 엔터티 ID** 및 **SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**

    ![Single Sign-on 구성](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_configure.png) 

7. Tooyour SensoScientific 무선 온도 모니터링 시스템 응용 프로그램 관리자 권한으로 로그인 합니다.

8. Hello 탐색 메뉴에서 hello 위에 표시를 클릭 **구성** 및 goto **구성** 아래 **Single Sign On** tooopen hello Single Sign-on 설정 합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_admin.png) 

9. **Single Sign-on 설정** 양식 hello 다음 단계를 수행 합니다.
 
    a. **Issuer Name(발급자 이름)**을 Azure AD로 선택합니다.
    
    b. 붙여넣기 hello **SAML 엔터티 ID** 발급자 URL 텍스트 상자에 Azure 포털에서 복사한입니다.
    
    c. 붙여넣기 hello **SAML Single Sign-on 서비스 URL** Single Sign-on 서비스 URL 텍스트 상자에 Azure 포털에서 복사한입니다.

    d. 붙여넣기 hello **Sign-Out URL** Single Sign-Out 서비스 URL 텍스트 상자에 Azure 포털에서 복사한입니다.

    e. Azure 포털에서 다운로드 하 고 여기에 업로드 하는 hello 인증서를 찾습니다.
    
    f. **Save**를 클릭합니다.
  
> [!TIP]
> 이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!  Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션. 자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함](https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Azure AD 테스트 사용자 만들기
이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.

![Azure AD 사용자 만들기][100]

**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**

1. Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_01.png) 

2. 사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_02.png) 

3. tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_03.png) 

4. Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_04.png) 

    a. Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.

    b. Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.

    c. 선택 **암호 표시** hello hello 값 기록 **암호**합니다.

    d. **만들기**를 클릭합니다.
 
### <a name="creating-a-sensoscientific-wireless-temperature-monitoring-system-test-user"></a>SensoScientific Wireless Temperature Monitoring System 테스트 사용자 만들기

tooenable Azure AD 사용자가 toolog tooSensoScientific 무선 온도 모니터링 시스템에서에서 이러한 해야에 프로 비전 SensoScientific 무선 온도 모니터링 시스템입니다. 작업할 [SensoScientific 무선 온도 모니터링 시스템 지원 팀](https://www.sensoscientific.com/contact-us/) hello 사용자 hello SensoScientific 무선 온도 모니터링 시스템 플랫폼을 추가할 수 있습니다. Single Sign-On을 사용하려면 먼저 사용자를 만들고 활성화해야 합니다. 

### <a name="assigning-hello-azure-ad-test-user"></a>Azure AD hello 테스트 사용자를 할당합니다.

이 섹션에서는 액세스 tooSensoScientific 무선 온도 모니터링 시스템을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.

![사용자 할당][200] 

**tooassign Britta Simon tooSensoScientific 무선 온도 모니터링 시스템 hello 다음 단계를 수행 합니다.**

1. Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.

    ![사용자 할당][201] 

2. Hello 응용 프로그램 목록에서 선택 **SensoScientific 무선 온도 모니터링 시스템**합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_app.png) 

3. Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.

    ![사용자 할당][202] 

4. **추가** 단추를 클릭합니다. 그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.

    ![사용자 할당][203]

5. **사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.

6. **사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.

7. **할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.
    
### <a name="testing-single-sign-on"></a>Single Sign-On 테스트

이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다. Hello SensoScientific 무선 온도 모니터링 시스템 타일을 클릭 hello 액세스 패널에서에서 자동으로 로그온 tooyour SensoScientific 무선 온도 모니터링 시스템 응용 프로그램 수 있습니다. 액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](https://msdn.microsoft.com/library/dn308586)를 참조하세요.

## <a name="additional-resources"></a>추가 리소스

* [방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와](active-directory-saas-tutorial-list.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_203.png

