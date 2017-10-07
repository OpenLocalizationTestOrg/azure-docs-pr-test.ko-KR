---
title: "자습서: Salesforce와 Azure Active Directory 통합 | Microsoft 문서"
description: "단일 로그온 tooconfigure 방법을 알아보려면 Azure Active Directory와 Salesforce 사이의 합니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2d7d420-dc91-41b8-a6b3-59579e043b35
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 1d848518ee30910e051cdc4746c599219f3b5a3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce"></a>자습서: Salesforce와 Azure Active Directory 통합

이 자습서에 설명 어떻게 toointegrate Salesforce Azure Active Directory (Azure AD).

Azure AD와 Salesforce를 통합 이점을 다음 hello로 제공 합니다.

- 액세스 tooSalesforce을 지닌 Azure AD에서 제어할 수 있습니다.
- 프로그램 사용자 tooautomatically get 로그온 tooSalesforce (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.
- 하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.

Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.

## <a name="prerequisites"></a>필수 조건

Azure AD 및 Salesforce 통합 tooconfigure 다음 항목 hello가 필요 합니다.

- Azure AD 구독
- Salesforce Single Sign-On이 설정된 구독

> [!NOTE]
> 이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.

이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.

- 꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.
- Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.

## <a name="scenario-description"></a>시나리오 설명
이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다. 이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.

1. Salesforce는 hello 갤러리 추가
2. Azure AD Single Sign-on 구성 및 테스트

## <a name="adding-salesforce-from-hello-gallery"></a>Salesforce는 hello 갤러리 추가
tooconfigure hello와의 통합 Salesforce Azure AD 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Salesforce tooadd가 필요합니다.

**hello 갤러리에서 Salesforce tooadd hello 다음 단계를 수행 합니다.**

1. Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다. 

    ![Active Directory][1]

2. 너무 이동**엔터프라이즈 응용 프로그램**합니다. 이동 하 여 너무**모든 응용 프로그램**합니다.

    ![응용 프로그램][2]
    
3. 클릭 **새 응용 프로그램** hello 대화의 hello 위쪽에 단추입니다.

    ![응용 프로그램][3]

4. Hello 검색 상자에 입력 **Salesforce**합니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_search.png)

5. Hello 결과 패널에서 선택 **Salesforce**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Azure AD Single Sign-on 구성 및 테스트
이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Salesforce에서 Azure AD Single Sign-On을 구성하고 테스트합니다.

Single sign on toowork에 대 한 Azure AD는 tooknow에 Azure AD에서 Salesforce에서 어떤 hello 테이블에 해당 사용자가 tooa 사용자 필요 합니다. 즉, Azure AD 사용자 및 Salesforce의 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.

Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** Salesforce에서 합니다.

tooconfigure 및 Salesforce 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.

1. **[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.
2. **[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.
3. **[Salesforce 테스트 사용자 만들기](#creating-a-salesforce-test-user)**  -toohave 표현인 연결 된 toohello Azure AD 사용자의 Salesforce에서 Britta Simon의 해당 하는 도구입니다.
4. **[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.
5. **[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성

이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 Salesforce 응용 프로그램에서 single sign on 구성 합니다.

**tooconfigure Azure AD single sign on와 Salesforce를 hello 다음 단계를 수행 합니다.**

1. Hello hello에 Azure 포털에서에서 **Salesforce** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.

    ![Single Sign-on 구성][4]

2. Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.
 
    ![Single Sign-on 구성](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_samlbase.png)

3. Hello에 **Salesforce 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_url.png)

    Hello에 **로그온 URL** hello 패턴을 사용 하 여 형식 hello 값 텍스트 상자: 
   * 엔터프라이즈 계정: `https://<subdomain>.my.salesforce.com`
   * 개발자 계정: `https://<subdomain>-dev-ed.my.salesforce.com`

    > [!NOTE] 
    > 이러한 값은 실제 hello 되지 않습니다. Hello 실제 로그온 URL으로 이러한 값을 업데이트 합니다. 연락처 [Salesforce 클라이언트 지원 팀](https://help.salesforce.com/support) tooget 이러한 값입니다. 
 
4. Hello에 **SAML 서명 인증서** 섹션에서 클릭 **인증서** hello 인증서 파일을 컴퓨터에 저장 합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_certificate.png) 

5. **저장** 단추를 클릭합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-salesforce-tutorial/tutorial_general_400.png)

6. Hello에 **Salesforce 구성** 섹션에서 클릭 **Salesforce 구성** tooopen **sign on 구성** 창. 복사 hello **SAML Single Sign-on 서비스 URL 및 엔터티 ID가 SAML** hello에서 **빠른 참조 섹션.** 

    ![Single Sign-On 구성](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_configure.png) 
<CS>
7.  브라우저에서 새 탭을 열고 tooyour Salesforce 관리자 계정에에서 로그인 합니다.

8.  Hello에서 **관리자** 탐색 창에서 클릭 **보안 제어** tooexpand hello 관련 섹션. 그런 다음 **Single Sign-On 설정**을 클릭합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso.png)

9.  Hello에 **Single Sign On 설정** 페이지에서 hello **편집** 단추입니다.
    ![Single Sign-On 구성](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-edit.png)

      > [!NOTE]
      > Toocontact를 할 수 없습니다 tooenable Single Sign On 설정 Salesforce 계정에 대 한 경우 [Salesforce 클라이언트 지원 팀](https://help.salesforce.com/support)합니다. 

10. **SAML 사용**을 선택한 다음 **저장**을 클릭합니다.

      ![Single Sign-on 구성](./media/active-directory-saas-salesforce-tutorial/sf-enable-saml.png)
11. tooconfigure SAML single sign on 설정을, 클릭 **새로**합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-new.png)

12. Hello에 **SAML Single Sign-on 설정 편집** 페이지에서 확인 하는 구성을 따르고 hello:

    ![Single Sign-on 구성](./media/active-directory-saas-salesforce-tutorial/sf-saml-config.png)

    a. Hello에 대 한 **이름** 필드에서이 구성에 대 한 이름을 입력 합니다. 에 대 한 값을 제공 하 **이름** hello를 자동으로 채울 **API 이름** 텍스트 상자에 붙여넣습니다.

    b. 붙여넣기 **SMAL 엔터티 ID** hello에 값 **발급자** Salesforce에서 필드입니다.

    c. Hello에 **엔터티 Id 텍스트 상자에 붙여넣습니다**를 hello 패턴을 사용 하 여 Salesforce 도메인 이름을 입력 합니다.
      
      * 엔터프라이즈 계정: `https://<subdomain>.my.salesforce.com`
      * 개발자 계정: `https://<subdomain>-dev-ed.my.salesforce.com`
      
    d. 클릭 **찾아보기** 또는 **파일 선택** tooopen hello **파일 선택 tooUpload** 대화 상자에서 Salesforce 인증서를 선택한 다음 클릭 **열고**tooupload hello 인증서입니다.

    e. **SAML ID 형식**에서 **어설션에 사용자의 salesforce.com 사용자 이름 포함**을 선택합니다.

    f. 에 대 한 **SAML Id 위치**선택, **hello hello Subject 문의 NameIdentifier 요소에 Id가**

    g. 붙여넣기 **Single Sign-on 서비스 URL** hello에 **Id 공급자 로그인 URL** Salesforce에서 필드입니다.
    
    h. **서비스 공급자가 시작한 요청 바인딩**에서 **HTTP 리디렉션**을 선택합니다.
    
    i. 마지막으로, 클릭 **저장** tooapply 프로그램 SAML single sign on 설정 합니다.

13. Salesforce에서 hello 왼쪽된 탐색 창에서 클릭 **도메인 관리** tooexpand hello 관련된 섹션을 클릭 하 고 **내 도메인**합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-salesforce-tutorial/sf-my-domain.png)

14. Toohello 아래로 스크롤하여 **인증 구성** 섹션을 hello 클릭 **편집** 단추입니다.

    ![Single Sign-on 구성](./media/active-directory-saas-salesforce-tutorial/sf-edit-auth-config.png)

15. Hello에 **인증 서비스** 섹션 hello SAML SSO 구성의 이름을 선택한 다음 클릭 **저장**합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-salesforce-tutorial/sf-auth-config.png)

    > [!NOTE]
    > 둘 이상의 인증 서비스를 선택 하면 사용자가 원하는 되는 인증 서비스 증명된 tooselect single sign on tooyour Salesforce 환경을 시작 하는 동안 사용 하 여 toosign 합니다. Toohappen, 원하는 하지 않는 경우 다음을 수행 해야 **다른 모든 인증 서비스를 선택 된 상태로 유지**합니다.
<CE>    
> [!TIP]
> 이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!  Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션. 자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)


### <a name="creating-an-azure-ad-test-user"></a>Azure AD 테스트 사용자 만들기
이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.

![Azure AD 사용자 만들기][100]

**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**

1. 왼쪽된 탐색 창의 hello에 hello **Azure 포털**, 클릭 **Azure Active Directory** 아이콘입니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-salesforce-tutorial/create_aaduser_01.png) 

2. 사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-salesforce-tutorial/create_aaduser_02.png) 

3. Hello 대화의 hello 위쪽 클릭 **추가** tooopen hello **사용자** 대화 상자.
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-salesforce-tutorial/create_aaduser_03.png) 

4. Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-salesforce-tutorial/create_aaduser_04.png) 

    a. Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.

    b. Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.

    c. 선택 **암호 표시** hello hello 값 기록 **암호**합니다.

    d. **만들기**를 클릭합니다.
 
### <a name="creating-a-salesforce-test-user"></a>Salesforce 테스트 사용자 만들기

이 섹션에서는 Salesforce에서 Britta Simon이라는 사용자를 만듭니다. Salesforce는 기본적으로 설정되는 Just-In-Time 프로비전을 지원합니다.
이 섹션에 작업 항목이 없습니다. 사용자는 Salesforce에서 존재 하지 않는, 경우에 새 tooaccess Salesforce를 시도할 때 만들어집니다.

### <a name="assigning-hello-azure-ad-test-user"></a>Azure AD hello 테스트 사용자를 할당합니다.

이 섹션에서는 tooSalesforce 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.

![사용자 할당][200] 

**tooassign Britta Simon tooSalesforce hello 다음 단계를 수행 합니다.**

1. Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.

    ![사용자 할당][201] 

2. Hello 응용 프로그램 목록에서 선택 **Salesforce**합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_app.png) 

3. Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.

    ![사용자 할당][202] 

4. **추가** 단추를 클릭합니다. 그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.

    ![사용자 할당][203]

5. **사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.

6. **사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.

7. **할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.
    
### <a name="testing-single-sign-on"></a>Single Sign-On 테스트

tootest single sign on 설정에 열기 hello 액세스 패널에 [https://myapps.microsoft.com](https://myapps.microsoft.com/)hello 테스트의 계정으로 로그인 하 고 클릭 **Salesforce**합니다.

## <a name="additional-resources"></a>추가 리소스

* [방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와](active-directory-saas-tutorial-list.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)
* [사용자 프로비저닝 구성](active-directory-saas-salesforce-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_203.png

