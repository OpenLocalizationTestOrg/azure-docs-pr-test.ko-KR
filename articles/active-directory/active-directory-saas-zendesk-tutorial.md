---
title: "자습서: Azure Active Directory와 Zendesk 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Zendesk 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9d7c91e5-78f5-4016-862f-0f3242b00680
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 46ccd57a4adeb810af459caaa1e592cf2b62cb8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zendesk"></a>자습서:Azure Active Directory와 Zendesk 통합

이 자습서에 설명 어떻게 toointegrate Zendesk와 Azure Active Directory (Azure AD).

Azure AD와 Zendesk 통합 이점을 다음 hello로 제공 합니다.

- 액세스 tooZendesk을 지닌 Azure AD에서 제어할 수 있습니다.
- 프로그램 사용자 tooautomatically get 로그온 tooZendesk (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.
- 하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.

Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.

## <a name="prerequisites"></a>필수 조건

Zendesk와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.

- Azure AD 구독
- Zendesk Single Sign-On이 설정된 구독


> [!NOTE]
> 이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.


이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.

- 꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.
- Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.


## <a name="scenario-description"></a>시나리오 설명
이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다. 이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.

1. Zendesk은 hello 갤러리 추가
2. Azure AD Single Sign-on 구성 및 테스트


## <a name="adding-zendesk-from-hello-gallery"></a>Zendesk은 hello 갤러리 추가
tooconfigure hello와의 통합 Zendesk Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Zendesk tooadd가 필요합니다.

**hello 갤러리에서 Zendesk tooadd hello 다음 단계를 수행 합니다.**

1. Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다. 

    ![Active Directory][1]

2. 너무 이동**엔터프라이즈 응용 프로그램**합니다. 이동 하 여 너무**모든 응용 프로그램**합니다.

    ![응용 프로그램][2]
    
3. 클릭 **새 응용 프로그램** hello 대화의 hello 위쪽에 단추입니다.

    ![응용 프로그램][3]

4. Hello 검색 상자에 입력 **Zendesk**합니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_search.png)

5. Hello 결과 패널에서 선택 **Zendesk**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Azure AD Single Sign-on 구성 및 테스트
이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Zendesk에서 Azure AD Single Sign-On을 구성하고 테스트합니다.

Single sign on toowork에 대 한 Azure AD는 tooknow Zendesk에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다. 즉, Azure AD 사용자와 Zendesk에 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.

Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** Zendesk에 합니다.

tooconfigure 및 Zendesk와 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.

1. **[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.
2. **[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.
3. **[Zendesk 테스트 사용자 만들기](#creating-a-zendesk-test-user)**  -toohave Britta Simon 표현인 연결 된 toohello Azure AD 사용자의 Zendesk에 해당 하는 도구입니다.
4. **[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.
5. **[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성

이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 Zendesk 응용 프로그램에서 single sign on 구성 합니다.

**Azure AD tooconfigure single sign on와 Zendesk를 hello 다음 단계를 수행 합니다.**

1. Hello hello에 Azure 포털에서에서 **Zendesk** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.

    ![Single Sign-on 구성][4]

2. Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.
 
    ![Single Sign-on 구성](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_samlbase.png)

3. Hello에 **Zendesk 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_url.png)

    a. Hello에 **로그온 URL** hello 패턴을 사용 하 여 형식 hello 값 텍스트 상자:`https://<subdomain>.zendesk.com`

    b. Hello에 **식별자** hello 패턴을 사용 하 여 형식 hello 값 텍스트 상자:`https://<subdomain>.zendesk.com`

    > [!NOTE] 
    > 이러한 값은 실제 값이 아닙니다. Hello 실제 로그온 URL과 식별자 URL 이러한 값을 업데이트 합니다. 연락처 [Zendesk 지원 팀](https://support.zendesk.com/hc/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise) tooget 이러한 값입니다. 

4. Zendesk에는 특정 형식의 hello SAML 어설션 합니다. 필수 SAML 특성이 없으면 하지만에서 특성을 추가할 수는 필요에 따라 **사용자 특성** 아래 단계 다음 hello 섹션: 

     ![Single Sign-on 구성](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_attributes1.png)

    a. Hello 클릭 **보기 및 편집 hello 다른 특성** 확인란 합니다.
     
    ![Single Sign-on 구성](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_attributes2.png)
   
    b. Hello 클릭 **특성 추가** tooopen **특성 추가** 대화 상자.
    
    ![Single Sign-on 구성](./media/active-directory-saas-zendesk-tutorial/tutorial_attribute_05.png)

    c. Hello에 **이름** 형식 hello 특성 이름 텍스트 상자 (예를 들어 **emailaddress**).
    
    d. Hello에서 **값** 선택 hello 특성 값 목록 (으로 **user.mail**).
    
    e. **확인**을 클릭합니다.
 
    > [!NOTE] 
    > 기본적으로 Azure AD에 없는 확장 특성 tooadd 특성을 사용 하는 경우. 클릭 [saml에서 설정 될 수 있는 사용자 특성](https://support.zendesk.com/hc/en-us/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise-) tooget hello 전체 목록은 SAML 특성을 **Zendesk** 허용 합니다. 

5. Hello에 **SAML 서명 인증서** 섹션을 복사 hello **지문** 인증서의 값입니다.

    ![Single Sign-on 구성](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_certificate.png) 

6. Hello에 **Zendesk 구성** 섹션에서 클릭 **구성 Zendesk** tooopen **sign on 구성** 창. 복사 hello **Sign-Out URL 및 SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**

    ![Single Sign-on 구성](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_configure.png) 

7. 다른 웹 브라우저 창에서 관리자 권한으로 Zendesk 회사 사이트에 로그인합니다.

8. **Admin**을 클릭합니다.

9. Hello 왼쪽된 탐색 창에서 클릭 **설정**, 클릭 하 고 **보안**합니다.

10. Hello에 **보안** 페이지 hello 다음 단계를 수행 합니다. 
   
     ![보안](./media/active-directory-saas-zendesk-tutorial/ic773089.png "보안")

    ![Single Sign-On](./media/active-directory-saas-zendesk-tutorial/ic773090.png "Single Sign-On")

     a. Hello 클릭 **관리 및 에이전트** 탭 합니다.

     b. **SSO(Single Sign-On) 및 SAML**을 선택하고**SAML**을 선택합니다.

     c. **SAML SSO URL** 붙여넣기 hello 값의 텍스트 상자 **SAML Single Sign-on 서비스 URL** Azure 포털에서 복사한입니다. 

     d. **원격 로그 아웃 URL** 붙여넣기 hello 값의 텍스트 상자 **Sign-Out URL** Azure 포털에서 복사한입니다.
        
     e. **인증서 지문** 텍스트 붙여넣기 hello **지문** Azure 포털에서 복사 하는 인증서의 값입니다.
     
     f. **Save**를 클릭합니다.

### <a name="creating-an-azure-ad-test-user"></a>Azure AD 테스트 사용자 만들기
이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.

![Azure AD 사용자 만들기][100]

**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**

1. Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-zendesk-tutorial/create_aaduser_01.png) 

2. 사용자의 toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-zendesk-tutorial/create_aaduser_02.png) 

3. Hello 대화의 hello 위쪽 클릭 **추가** tooopen hello **사용자** 대화 상자.
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-zendesk-tutorial/create_aaduser_03.png) 

4. Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-zendesk-tutorial/create_aaduser_04.png) 

    a. Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.

    b. Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.

    c. 선택 **암호 표시** hello hello 값 기록 **암호**합니다.

    d. **만들기**를 클릭합니다. 

### <a name="creating-a-zendesk-test-user"></a>Zendesk 테스트 사용자 만들기

에 tooenable Azure AD 사용자가 toolog **Zendesk**에 제공 해야 **Zendesk**합니다.  
Hello 앱에 할당 된 hello 역할에 따라 hello의 예상 되는 동작:

 1. **최종 사용자** 계정은 로그인할 때 자동으로 프로비전됩니다.
 2. **에이전트** 및 **Admin** toobe에서 수동으로 프로 비전 해야 하는 계정이 **Zendesk** 로그인 하기 전에.
 
**tooprovision 사용자 계정을 hello 다음 단계를 수행 합니다.**

1. Tooyour 로그인 **Zendesk** 테 넌 트입니다.

2. 선택 hello **고객 목록** 탭 합니다.

3. 선택 hello **사용자** 탭을 클릭 **추가**합니다.
   
    ![사용자 추가](./media/active-directory-saas-zendesk-tutorial/ic773632.png "사용자 추가")
4. Tooprovision을 클릭 한 다음 기존 Azure AD 계정의 전자 메일 주소 hello 입력 **저장**합니다.
   
    ![새 사용자](./media/active-directory-saas-zendesk-tutorial/ic773633.png "새 사용자")

> [!NOTE]
> 다른 Zendesk 사용자 계정 만들기 도구를 사용할 수 있습니다 또는 AAD 사용자 계정을 tooprovision Zendesk에서 제공 된 Api입니다.


### <a name="assigning-hello-azure-ad-test-user"></a>Azure AD hello 테스트 사용자를 할당합니다.

이 섹션에서는 tooZendesk 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.

![사용자 할당][200] 

**tooassign Britta Simon tooZendesk hello 다음 단계를 수행 합니다.**

1. Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.

    ![사용자 할당][201] 

2. Hello 응용 프로그램 목록에서 선택 **Zendesk**합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_app.png) 

3. Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.

    ![사용자 할당][202] 

4. **추가** 단추를 클릭합니다. 그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.

    ![사용자 할당][203]

5. **사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.

6. **사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.

7. **할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.
    
### <a name="testing-single-sign-on"></a>Single Sign-On 테스트

이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.

Hello 액세스 패널에서에서 hello Zendesk 타일을 클릭할 때 자동으로 로그온 tooyour Zendesk 응용 프로그램을 구해야 합니다.
액세스 패널 hello에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.

## <a name="additional-resources"></a>추가 리소스

* [방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와](active-directory-saas-tutorial-list.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_203.png
