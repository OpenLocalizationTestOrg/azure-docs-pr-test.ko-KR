---
title: "자습서: Adobe Creative Cloud와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Adobe 크리에이티브 클라우드 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9ba1171e-56b1-4475-b308-58637d35e5a7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 5e66255e9785465974a23cd3ef79c24e28c0250f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adobe-creative-cloud"></a>자습서: Adobe Creative Cloud와 Azure Active Directory 통합

배웁니다이 자습서에서는 Azure Active Directory (Azure AD)와 toointegrate Adobe 크리에이티브 클라우드 방법입니다.

Azure AD와 Adobe 크리에이티브 클라우드 통합 이점을 다음 hello 제공:

- 크리에이티브 클라우드 액세스 tooAdobe을 지닌 Azure AD에서 제어할 수 있습니다.
- Azure AD 계정을 사용 하면 사용자가 tooautomatically get 로그온 tooAdobe 크리에이티브 클라우드 (Single Sign-on)를 사용할 수 있습니다.
- 하나의 중앙 위치-hello Azure 관리 포털에서에서 사용자 계정을 관리할 수 있습니다.

Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.

## <a name="prerequisites"></a>필수 조건

Adobe 크리에이티브 클라우드와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.

- Azure AD 구독
- Adobe Creative Cloud Single Sign-On을 사용하도록 설정된 구독

> [!NOTE]
> 이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.

이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.

- 꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.
- Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.

## <a name="scenario-description"></a>시나리오 설명
이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다. 이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.

1. Hello 갤러리에서 Adobe 크리에이티브 클라우드를 추가합니다.
2. Azure AD Single Sign-on 구성 및 테스트

## <a name="adding-adobe-creative-cloud-from-hello-gallery"></a>Hello 갤러리에서 Adobe 크리에이티브 클라우드를 추가합니다.
tooconfigure hello와의 통합 Adobe 크리에이티브 클라우드 Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Adobe 크리에이티브 클라우드 tooadd가 필요합니다.

**hello 갤러리에서 Adobe 크리에이티브 클라우드 tooadd hello 다음 단계를 수행 합니다.**

1. Hello에  **[Azure 관리 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다. 

    ![Active Directory][1]

2. 너무 이동**엔터프라이즈 응용 프로그램**합니다. 이동 하 여 너무**모든 응용 프로그램**합니다.

    ![응용 프로그램][2]
    
3. 클릭 **추가** hello 대화의 hello 위쪽에 단추입니다.

    ![응용 프로그램][3]

4. Hello 검색 상자에 입력 **Adobe 크리에이티브 클라우드**합니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_000.png)

5. Hello 결과 패널에서 선택 **Adobe 크리에이티브 클라우드**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_0001.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Azure AD Single Sign-on 구성 및 테스트
이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Adobe Creative Cloud에서 Azure AD Single Sign-On을 구성하고 테스트합니다.

Single sign on toowork에 대 한 Azure AD는 tooknow Adobe 크리에이티브 클라우드에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다. 즉, Azure AD 사용자 및 Adobe 크리에이티브 클라우드에 hello 관련된 사용자 간 링크 관계를 설정할 toobe가 필요 합니다.

Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** Adobe 크리에이티브 클라우드에 합니다.

tooconfigure 및 Adobe 크리에이티브 클라우드를 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.

1. **[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.
2. **[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.
3. **[Adobe 크리에이티브 클라우드 테스트 사용자 만들기](#creating-an-adobe-creative-cloud-test-user)**  -toohave Britta Simon 표현인 연결 된 Azure AD toohello 그녀는 Adobe 크리에이티브 클라우드에 해당 하는 도구입니다.
4. **[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.
5. **[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성

이 섹션에서는 Azure AD에서 single sign-on hello Azure 관리 포털에서 설정 및 Adobe 크리에이티브 클라우드 응용 프로그램에서 single sign on 구성 합니다.

**Adobe 크리에이티브 클라우드와 Azure AD에서 single sign-on tooconfigure hello 다음 단계를 수행 합니다.**

1. Hello에 hello Azure 관리 포털에서 **Adobe 크리에이티브 클라우드** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.

    ![Single Sign-on 구성][4]

2. Hello에 **Single sign on** 대화 상자에서으로 **모드** 선택 **SAML 기반 로그온** tooenable single sign-on입니다.
 
    ![Single Sign-on 구성](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_01.png)

3. Hello에 **Adobe 창조적인 클라우드 도메인 및 Url** 섹션를 hello tooconfigure hello 응용 프로그램에 필요한 경우 다음 단계를 수행 **IDP** 시작 모드:

    ![Single Sign-on 구성](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_url1.png)

    a. Hello에 **식별자** 형식 hello 값으로 텍스트 상자:`https://www.okta.com/saml2/service-provider/<token>`

    b. Hello에 **회신 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<company name>.okta.com/auth/saml20/accauthlinktest`

    > [!NOTE] 
    > 이러한 없는지 hello 실제 값 note 하십시오. Tooupdate hello 실제 식별자와 회신 URL 사용 하 여 이러한 값 해야합니다. 여기 있습니다 toouse hello의 고유 값을 hello 식별자의에서 문자열을 사용 하는 것이 좋습니다. Toocreate 된 사용자를 수동으로 해야 할 경우 toocontact hello Adobe 크리에이티브 클라우드 지원 팀을 해야 합니다.

4. Hello에 **Adobe 창조적인 클라우드 도메인 및 Url** 섹션를 hello tooconfigure hello 응용 프로그램에 필요한 경우 다음 단계를 수행 **SP** 시작 모드:

    ![Single Sign-on 구성](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_url2.png)

    a. Hello 클릭 **고급 URL 설정 표시** 옵션

    b. Hello에 **로그온 URL** 형식 hello 값으로 텍스트 상자:`https://adobe.com`

5. Hello에 **SAML 서명 인증서** 섹션에서 클릭 **인증서 (Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_05.png) 

6. Hello에 **Adobe 창조적인 클라우드 구성** 섹션에서 클릭 **Adobe 크리에이티브 클라우드 구성** tooopen **sign on 구성** 창. Hello를 복사 하십시오 **SAML 엔터티 Id** 및 **SAML SSO 서비스 URL** 빠른 참조 섹션에서.

    ![Single Sign-on 구성](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_06.png) 

7. 다른 웹 브라우저 창에서 관리자 권한으로 로그온 tooyour Adobe 크리에이티브 클라우드 테 넌 트입니다.

8.  너무 이동**Identity** 왼쪽된 탐색 창의 hello 되 고 도메인을 클릭 합니다. 다음에 나오는 단계에 따라 hello 수행 **Single Sign 구성이 필요** 섹션.

    ![설정](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_001.png "설정")

9. 클릭 **찾아보기** tooupload hello Azure AD에서 너무 인증서를 다운로드**IDP 인증서**합니다.

10. Hello에 **IDP 발급자** hello 값의 텍스트 상자 **SAML 엔터티 Id** 에서 복사할 **sign on 구성** Azure 포털에서 섹션.

11. Hello에 **IDP 로그인 URL** hello 값의 텍스트 상자 **SAML SSO 서비스 URL** 에서 복사할 **sign on 구성** Azure 포털에서 섹션.

12. **HTTP - 리디렉션**을 **IDP 바인딩**으로 선택합니다.

13. **전자 메일 주소**를 **사용자 로그인 설정**으로 선택합니다.
 
14. **저장** 단추를 클릭합니다.

15. hello XML hello 대시보드를 제공 합니다 **"메타 데이터 다운로드"** 파일입니다. 여기에는 Adobe의 EntityDescriptor URL과 AssertionConsumerService URL이 포함되어 있습니다. Hello 파일을 열고 hello Azure AD 응용 프로그램에서에서 해당 설정을 구성 하십시오.

    ![앱 쪽에서 Single Sign-On 구성](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_002.png)

    ![앱 쪽에서 Single Sign-On 구성](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_003.png)

    a. 사용 하 여 hello Adobe EntityDescriptor 값에 대 한 정보가 제공 **식별자** hello에 **앱 설정 구성** 대화 상자.

    b. 사용 하 여 hello Adobe AssertionConsumerService 값에 대 한 정보가 제공 **회신 URL** hello에 **앱 설정 구성** 대화 상자.
 
### <a name="creating-an-azure-ad-test-user"></a>Azure AD 테스트 사용자 만들기
이 섹션의 hello 목표 toocreate Britta Simon 라는 hello Azure 관리 포털에서 테스트 사용자를입니다.

![Azure AD 사용자 만들기][100]

**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**

1. Hello에 **Azure 관리 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_01.png) 

2. 너무 이동**사용자 및 그룹** 클릭 **모든 사용자에 게** 사용자 toodisplay hello 목록입니다.
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_02.png) 

3. Hello 대화의 hello 위쪽 클릭 **추가** tooopen hello **사용자** 대화 상자.
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_03.png) 

4. Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_04.png) 

    a. Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.

    b. Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.

    c. 선택 **암호 표시** hello hello 값 기록 **암호**합니다.

    d. **만들기**를 클릭합니다. 

### <a name="creating-an-adobe-creative-cloud-test-user"></a>Adobe Creative Cloud 테스트 사용자 만들기

Tooenable Azure AD 사용자가 toolog Adobe 크리에이티브 클라우드로 주문 하 고에 Adobe 크리에이티브 클라우드에 이들 프로 비전 해야 합니다.  
Hello Adobe 크리에이티브 클라우드의 경우에서 프로 비전은 수동 작업입니다.

**사용자 계정 수행 tooprovision hello 다음 단계:**

1. 관리자 권한으로 Adobe 크리에이티브 클라우드 회사 사이트 tooyour에 로그인 합니다.

2. **피플**을 클릭합니다.

    ![사람](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_001.png "사람")

3. **사용자 초대**를 클릭합니다.

    ![사용자 초대](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_002.png "사용자 초대")

4. Hello에 **사용자 초대** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.

    ![피플 초대](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_003.png "피플 초대")

    a. Hello에 **전자 메일** textbox Britta Simon 계정의 hello 전자 메일 주소를 입력 합니다.
    
    b. **초대**를 클릭합니다.

    > [!NOTE]
    > hello Azure Active Directory 계정 소유자 전자 메일을 받게 되 고 링크 tooconfirm 자신의 계정을 활성화 되기 전에 수행 됩니다.

### <a name="assigning-hello-azure-ad-test-user"></a>Azure AD hello 테스트 사용자를 할당합니다.

이 섹션에서는 그녀의 액세스 tooAdobe 크리에이티브 클라우드를 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.

![사용자 할당][200] 

**tooassign Britta Simon tooAdobe 크리에이티브 클라우드 hello 다음 단계를 수행 합니다.**

1. Hello Azure 관리 포털에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.

    ![사용자 할당][201] 

2. Hello 응용 프로그램 목록에서 선택 **Adobe 크리에이티브 클라우드**합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_50.png) 

3. Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.

    ![사용자 할당][202] 

4. **추가** 단추를 클릭합니다. 그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.

    ![사용자 할당][203]

5. **사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.

6. **사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.

7. **할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.
    
### <a name="testing-single-sign-on"></a>Single Sign-On 테스트

이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.

Hello 액세스 패널에서에서 hello Adobe 크리에이티브 클라우드 타일을 클릭할 때 자동으로 로그온 tooyour Adobe 크리에이티브 클라우드 응용 프로그램을 구해야 합니다.


## <a name="additional-resources"></a>추가 리소스

* [방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와](active-directory-saas-tutorial-list.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_203.png