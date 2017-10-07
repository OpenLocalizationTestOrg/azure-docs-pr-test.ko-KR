---
title: "자습서: SAP Cloud for Customer와 Azure Active Directory 통합 | Microsoft Docs"
description: "단일 로그온 tooconfigure 방법을 알아보려면 Azure Active Directory와 고객에 대 한 SAP 클라우드 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 90154dab-eba2-4563-bcf0-f2acc797ea97
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: 0525ea81122458ab3ac24a5bdb0b5f628405dd05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-cloud-for-customer"></a>자습서: SAP Cloud for Customer와 Azure Active Directory 통합

Toointegrate SAP 방법을 배우게이 자습서에서는 Azure Active Directory (Azure AD)와 고객에 대 한 클라우드입니다.

SAP 클라우드 고객 Azure AD와 통합 하는 이점을 다음 hello로 제공 합니다.

- 고객에 대 한 클라우드 액세스 tooSAP 지닌 Azure AD에서 제어할 수 있습니다.
- Azure AD 계정을 사용 하면 사용자가 tooautomatically get 로그온 tooSAP 클라우드 (Single Sign-on)는 고객에 대 한 사용할 수 있습니다.
- 하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.

Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.

## <a name="prerequisites"></a>필수 조건

고객에 대 한 SAP 클라우드와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.

- Azure AD 구독
- SAP Cloud for Customer Single Sign-On이 설정된 구독

> [!NOTE]
> 이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.

이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.

- 꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.
- Azure AD 평가판 환경이 없으면 [평가판 제품](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.

## <a name="scenario-description"></a>시나리오 설명
이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다. 이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.

1. Hello 갤러리에서 SAP 클라우드 고객에 대 한 추가
2. Azure AD Single Sign-on 구성 및 테스트

## <a name="adding-sap-cloud-for-customer-from-hello-gallery"></a>Hello 갤러리에서 SAP 클라우드 고객에 대 한 추가
tooconfigure hello와의 통합 SAP 클라우드 Azure AD로 고객에 대 한 필요한 SAP 클라우드 tooadd 고객에 대 한 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 합니다.

**hello 갤러리에서 고객에 대 한 SAP 클라우드 tooadd hello 다음 단계를 수행 합니다.**

1. Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다. 

    ![Active Directory][1]

2. 너무 이동**엔터프라이즈 응용 프로그램**합니다. 이동 하 여 너무**모든 응용 프로그램**합니다.

    ![응용 프로그램][2]
    
3. tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.

    ![응용 프로그램][3]

4. Hello 검색 상자에 입력 **고객에 대 한 SAP 클라우드**합니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_search.png)

5. Hello 결과 패널에서 선택 **고객에 대 한 SAP 클라우드**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Azure AD Single Sign-on 구성 및 테스트
이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 SAP Cloud for Customer에서 Azure AD Single Sign-On을 구성하고 테스트합니다.

Single sign on toowork에 대 한 Azure AD는 tooknow 고객에 대 한 SAP 클라우드에서 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다. 즉, Azure AD 사용자 및 고객에 대 한 SAP 클라우드에서 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.

고객에 대 한 SAP 클라우드에서 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.

tooconfigure 및 고객에 대 한 SAP 클라우드와 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.

1. **[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.
2. **[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.
3. **[고객 테스트 사용자에 대 한 SAP 클라우드 만들기](#creating-a-sap-cloud-for-customer-test-user)**  -toohave 표현인 연결 된 toohello Azure AD 사용자의 고객에 대 한 SAP 클라우드에서 Britta Simon의 해당 하는 도구입니다.
4. **[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.
5. **[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성

이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 SAP 클라우드에 고객 응용 프로그램에 대 한 single sign on 구성 합니다.

**Azure AD에서 single sign-on을 고객에 대 한 SAP 클라우드와 tooconfigure hello 다음 단계를 수행 합니다.**

1. Hello hello에 Azure 포털에서에서 **고객에 대 한 SAP 클라우드** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.

    ![Single Sign-on 구성][4]

2. Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.
 
    ![Single Sign-on 구성](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_samlbase.png)

3. Hello에 **고객 도메인 및 Url에 대 한 SAP 클라우드** 섹션를 hello 다음 단계를 수행 합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_url.png)

    a. Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<server name>.crm.ondemand.com`

    b. Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<server name>.crm.ondemand.com`

    > [!NOTE] 
    > 이러한 값은 실제 값이 아닙니다. 이러한 항목을 업데이트 로그온 URL과 식별자 실제 hello로 값입니다. 연락처 [고객 클라이언트 지원 팀에 대 한 SAP 클라우드](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) tooget 이러한 값입니다. 

4. Hello에 **사용자 특성** 섹션를 hello 다음 단계를 수행 합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_attribute.png)

    a. **사용자 식별자** 목록, 선택 hello **ExtractMailPrefix()** 함수입니다.

    b. Hello에서 **메일** 목록, 선택 hello 사용자 특성을 toouse 구현 합니다.
    예를 들어 toouse hello 고유한 사용자 식별자로 EmployeeID 원하고 ExtensionAttribute2 hello에 hello 특성 값을 저장 한 경우 user.extensionattribute2 다음 선택 합니다.  

5. Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello 메타 데이터 파일을 컴퓨터에 저장 합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_certificate.png) 

6. **저장** 단추를 클릭합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_400.png)

7. Hello에 **사용자 구성에 대 한 SAP 클라우드** 섹션에서 클릭 **고객에 대 한 SAP 클라우드 구성** tooopen **sign on 구성** 창. 복사 hello **SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**

    ![Single Sign-on 구성](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_configure.png) 

8. tooget SSO 구성 단계를 수행 하는 hello를 수행 합니다.
   
    a. SAP Cloud for Customer 포털에 관리자 권한으로 로그인합니다.
   
    b. Toohello 이동 **응용 프로그램 및 사용자 관리에 대 한 일반적인 작업** hello 클릭 **Id 공급자** 탭 합니다.
   
    c. 클릭 **새 Id 공급자** 및 hello Azure 포털에서에서 다운로드 한 메타 데이터 XML 파일. hello 선택 합니다. Hello 시스템 hello 메타 데이터를 가져와서 hello 필수 서명 인증서와 암호화 인증서를 자동으로 업로드 합니다.
   
    ![Single Sign-on 구성](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_54.png)
   
    d. Azure Active Directory hello 어설션 소비자 서비스 URL의에서 요소가 hello SAML 요청, hello 선택 **어설션 소비자 서비스 URL 포함** 확인란을 선택 합니다.
   
    e. **Single Sign-on 활성화**를 클릭합니다.
   
    f. 변경 내용을 저장합니다.
   
    g. Hello 클릭 **내 시스템** 탭 합니다.
   
    ![Single Sign-on 구성](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_52.png)
   
    h. Azure Portal에서 복사한 **SAML Single Sign-On 서비스 URL**을 **Azure AD 로그온 URL** 텍스트 상자에 붙여 넣습니다.
   
    ![Single Sign-on 구성](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_53.png)
   
    i. Hello 직원 hello를 선택 하 여 사용자 ID 및 암호 또는 SSO를 사용 하 여 로그온 사이의 수동으로 선택할 수 있는지 여부를 지정 **수동 Identity Provider 선택**합니다.
   
    j. Hello에 **SSO URL** 섹션 프로그램 직원 toosign toohello 시스템에서 사용 해야 하는 hello URL을 지정 합니다. 
    Hello에 **전송 URL tooEmployee** 목록 hello 다음 옵션 중 선택할 수 있습니다.
   
    **SSO가 아닌 URL**
   
    hello 시스템만 hello 정상적인 시스템 URL toohello 직원을 보냅니다. hello 직원이 SSO를 사용 하 여 로그온 수 없습니다 및 암호를 사용 하거나 대신 인증서 해야 합니다.
   
    **SSO URL** 
   
    hello 시스템 hello SSO URL toohello 직원에만 보냅니다. hello 직원이 SSO를 사용 하 여 로그온 할 수 있습니다. Hello IdP 통해 인증 요청이 리디렉션됩니다.
   
    **자동 선택**
   
    SSO 활성 상태 이면 hello 정상적인 시스템 URL toohello 직원을 hello 시스템에 보냅니다. SSO 활성 상태 이면 hello 시스템 hello 직원에 게 암호가 있는지 여부를 확인 합니다. 암호를 사용할 수 있는 경우 SSO URL과 비 SSO URL 모두 toohello 직원을 전송 됩니다. 그러나 hello 직원 암호가 없는 경우 hello SSO URL toohello 직원을 전송 됩니다.
   
    k. 변경 내용을 저장합니다.

> [!TIP]
> 이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!  Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션. 자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Azure AD 테스트 사용자 만들기
이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.

![Azure AD 사용자 만들기][100]

**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**

1. Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_01.png) 

2. 사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_02.png) 

3. tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_03.png) 

4. Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_04.png) 

    a. Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.

    b. Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.

    c. 선택 **암호 표시** hello hello 값 기록 **암호**합니다.

    d. **만들기**를 클릭합니다.
 
### <a name="creating-a-sap-cloud-for-customer-test-user"></a>SAP Cloud for Customer 테스트 사용자 만들기

이 섹션에서는 SAP Cloud for Customer에서 Britta Simon이라는 사용자를 만듭니다. 와 협력 하세요 [고객 지원 팀에 대 한 SAP 클라우드](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) 고객 플랫폼에 대 한 SAP 클라우드 hello에 tooadd hello 사용자입니다. 

> [!NOTE]
> NameID 값 고객 플랫폼에 대 한 SAP 클라우드 hello에 hello 사용자 이름 필드와 일치 해야 하 고 있는지 확인 하십시오.

### <a name="assigning-hello-azure-ad-test-user"></a>Azure AD hello 테스트 사용자를 할당합니다.

이 섹션에서는 액세스 tooSAP 클라우드 고객에 대 한 권한을 부여 하 여 Britta Simon toouse Azure single sign on을 사용 합니다.

![사용자 할당][200] 

**tooassign Britta Simon tooSAP 고객에 대 한 클라우드 hello 다음 단계를 수행 합니다.**

1. Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.

    ![사용자 할당][201] 

2. Hello 응용 프로그램 목록에서 선택 **고객에 대 한 SAP 클라우드**합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_app.png) 

3. Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.

    ![사용자 할당][202] 

4. **추가** 단추를 클릭합니다. 그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.

    ![사용자 할당][203]

5. **사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.

6. **사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.

7. **할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.
    
### <a name="testing-single-sign-on"></a>Single Sign-On 테스트

이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.

Hello 액세스 패널에서에서 타일 고객에 대 한 hello SAP 클라우드를 클릭 하면 고객 응용 프로그램에 대 한 자동으로 로그온 tooyour SAP 클라우드를 가져와야 합니다.
액세스 패널 hello에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.

## <a name="additional-resources"></a>추가 리소스

* [방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와](active-directory-saas-tutorial-list.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_203.png

