---
title: "자습서: SAP HANA와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 SAP HANA 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: cef4a146-f4b0-4e94-82de-f5227a4b462c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 5ff6bfde0b1d7ab14025a4bc45199f9f826affd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana"></a>자습서: SAP HANA와 Azure Active Directory 통합

이 자습서에 알아봅니다 방법을 toointegrate SAP HANA Azure Active Directory (Azure AD)와 합니다.

SAP HANA Azure AD와 통합 hello 다음 이점을 제공 합니다.

- 액세스 tooSAP HANA 지닌 Azure AD에서 제어할 수 있습니다.
- 프로그램 사용자 tooautomatically get 로그온 tooSAP HANA (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.
- 하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.

Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.

## <a name="prerequisites"></a>필수 조건

SAP HANA와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.

- Azure AD 구독
- SAP HANA Single Sign-On이 설정된 구독
- 공용 IaaS, 온-프레미스, Azure VM 또는 Azure의 SAP 대형 인스턴스에서 실행 중인 HANA 인스턴스
- hello XSA 관리 웹 인터페이스 뿐만 아니라 HANA Studio hello HANA 인스턴스에 설치 되어 있습니다.

> [!NOTE]
> 이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 SAP HANA의 프로덕션 환경을 사용 합니다. 개발 이나 준비 hello 응용 프로그램의 환경 및 사용 하 여 hello 프로덕션 환경에 먼저 hello 통합을 테스트 합니다.

이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.

- 꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.
- Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.

## <a name="scenario-description"></a>시나리오 설명
이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다. 이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.

1. SAP HANA hello 갤러리 추가
2. Azure AD Single Sign-on 구성 및 테스트

## <a name="adding-sap-hana-from-hello-gallery"></a>SAP HANA hello 갤러리 추가
tooconfigure hello와의 통합 SAP HANA Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 SAP HANA tooadd가 필요합니다.

**hello 갤러리에서 SAP HANA tooadd hello 다음 단계를 수행 합니다.**

1. Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다. 

    ![hello Azure Active Directory 단추][1]

2. 너무 이동**엔터프라이즈 응용 프로그램**합니다. 이동 하 여 너무**모든 응용 프로그램**합니다.

    ![hello 엔터프라이즈 응용 프로그램 블레이드][2]
    
3. tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.

    ![hello 새 응용 프로그램 단추][3]

4. Hello 검색 상자에 입력 **SAP HANA**선택, **SAP HANA** 결과 패널에서 클릭 **추가** tooadd hello 응용 프로그램 단추입니다. 

    ![hello 새 응용 프로그램](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Azure AD Single Sign-on 구성 및 테스트
이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 SAP HANA에서 Azure AD Single Sign-On을 구성하고 테스트합니다.

Single sign on toowork에 대 한 Azure AD는 tooknow SAP HANA에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다. 즉, Azure AD 사용자 및 SAP HANA에 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.

SAP HANA에 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.

tooconfigure 및 SAP HANA를 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.

1. **[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.
2. **[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.
3. **[SAP HANA 테스트 사용자 만들기](#creating-a-sap-hana-test-user)**  -toohave Britta Simon 표현인 연결 된 toohello Azure AD 사용자의 SAP HANA에 해당 하는 도구입니다.
4. **[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.
5. **[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성

이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 SAP HANA 응용 프로그램에서 single sign on 구성 합니다.

**tooconfigure Azure AD single sign on와 SAP HANA hello 다음 단계를 수행 합니다.**

1. Hello hello에 Azure 포털에서에서 **SAP HANA** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.

    ![Single Sign-on 구성][4]

2. Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_samlbase.png)

3. Hello에 **SAP HANA 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.

    ![도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_url.png)

    a. Hello에 **식별자** 텍스트 상자도 입력 합니다.`HA100` 

    b. Hello에 **회신 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<Customer-SAP-instance-url>/sap/hana/xs/saml/login.xscfunc`

    > [!NOTE] 
    > 이러한 값은 실제 값이 아닙니다. Hello 실제 식별자 및 회신 URL로이 값을 업데이트 합니다. 연락처 [SAP HANA 클라이언트 지원 팀](https://cloudplatform.sap.com/contact.html) tooget 이러한 값입니다. 

4. Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello 메타 데이터 파일을 컴퓨터에 저장 합니다.

    ![hello 인증서 다운로드 링크](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_certificate.png) 

    >[!Note]
    >인증서가 활성 상태 확인 것 활성 hello를 클릭 하 여 "새 확인 인증서 현재" 확인란 hello Azure AD에서. 

5. SAP HANA 응용 프로그램에는 특정 형식의 hello SAML 어설션 합니다. 다음 스크린 샷 hello이에 대 한 예가 나와 있습니다. 여기에서는 매핑한 hello **사용자 식별자** 와 **ExtractMailPrefix()** 의 기능은 **user.mail**합니다. 이렇게 하면 고유한 사용자 id입니다. hello는 hello 사용자의 전자 메일의 hello 접두사 값 모든 성공적인 응답에 SAP HANA 응용 프로그램 toohello를 보내집니다.

    ![Single Sign-on 구성](./media/active-directory-saas-saphana-tutorial/attribute.png)

6. Hello에 **사용자 특성** hello 섹션 **Single sign on** 대화 상자:

    a. Hello에 **사용자 식별자** 드롭다운 목록에서 선택 **ExtractMailPrefix**합니다.
    
    b. Hello에 **메일** 드롭다운 목록에서 선택 **user.mail**합니다.

7. **저장** 단추를 클릭합니다.

    ![Single Sign-On 구성 저장 단추](./media/active-directory-saas-saphana-tutorial/tutorial_general_400.png)
    
8. tooconfigure single sign on에서 **SAP HANA** 쪽, 로그인 tooyour **HANA XSA 웹 콘솔** toohello 이동 하 여 각 HTTPS 끝점입니다.

    > [!Note]
    > Hello 기본 구성으로 hello URL 인증 된 SAP HANA 데이터베이스 사용자 toocomplete hello 로그온 프로세스의 자격 증명을 hello hello 요청 tooa 로그온 화면을를 리디렉션합니다. hello 로그온 사용자가 hello 권한이 필요한 tooperform SAML 관리 작업에 있어야 합니다.

9. 너무 hello XSA 웹 인터페이스, 이동**SAML Id 공급자** 여기에서 클릭 hello **"+"** -hello 아래쪽의 hello 화면 toodisplay hello 추가 Identity Provider 정보 창에 단추 및 수행 다음 단계는 hello:

    ![ID 공급자 추가](./media/active-directory-saas-saphana-tutorial/sap1.png)

    a. Hello에 **Identity Provider 정보 추가** 창의 hello hello로 Azure 포털에서 다운로드 한 메타 데이터 XML의 붙여넣기 hello 내용 **메타 데이터** 텍스트 상자에 붙여넣습니다.

    ![ID 공급자 설정 추가](./media/active-directory-saas-saphana-tutorial/sap2.png)

    b. Hello XML 문서의 내용을 hello 유효한 경우 프로세스를 구문 분석 하는 hello 추출 하는 데 필요한 정보 tooinsert hello hello **제목과 엔터티 ID, 발급자** hello 일반 데이터의에서 필드 영역에서 화면 및 hello hello의 URL 필드 대상 화면 영역, 예를 들어  **기준 URL 및 SingleSignOn URL (*)** 합니다.

    ![ID 공급자 설정 추가](./media/active-directory-saas-saphana-tutorial/sap3.png)

    c. 일반 데이터 hello hello 이름 상자에 화면 영역 hello 새 SAML SSO id 공급자에 대 한 이름을 입력 합니다.

    > [!Note]
    > SAML IDP hello hello 이름은 필수 이며; 고유 해야 합니다. 선택 하는 경우 SAML SAP HANA XS 응용 프로그램 toouse hello 인증 방법으로 서 예를 들어 hello XS 아티팩트 관리 도구의 hello 인증 화면 영역에 표시 되는 사용할 수 있는 SAML IDPs의 hello 목록에 나타납니다.

10. Hello 새 SAML id 공급자의 hello 세부 정보를 저장 합니다. 선택 **저장** toosave hello hello SAML id 공급자의 세부 정보 및 알려진된 SAML IDPs의 hello 새 SAML IDP toohello 목록을 추가 합니다.

    ![저장 단추](./media/active-directory-saas-saphana-tutorial/sap4.png)

11. HANA Studio hello의 hello 시스템 속성 내에서 **구성** 탭에서 설정 하 여 필터링 하는 것 **saml** hello 조정 **assertion_timeout** 에서**10 초** 너무**120 개**합니다.

    ![assertion_timeout 설정](./media/active-directory-saas-saphana-tutorial/sap7.png)

> [!TIP]
> 이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!  Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션. 자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Azure AD 테스트 사용자 만들기
이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.

![Azure AD 사용자 만들기][100]

**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**

1. Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.

    ![hello Azure Active Directory 단추](./media/active-directory-saas-saphana-tutorial/create_aaduser_01.png) 

2. 사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.
    
    !["사용자 및 그룹" hello 및 "모든 사용자" 링크](./media/active-directory-saas-saphana-tutorial/create_aaduser_02.png) 

3. tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.
 
    ![hello 추가 단추](./media/active-directory-saas-saphana-tutorial/create_aaduser_03.png) 

4. Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.
 
    ![hello 사용자 대화 상자](./media/active-directory-saas-saphana-tutorial/create_aaduser_04.png) 

    a. Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.

    b. Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.

    c. 선택 **암호 표시** hello hello 값 기록 **암호**합니다.

    d. **만들기**를 클릭합니다.
 
### <a name="creating-a-sap-hana-test-user"></a>SAP HANA 테스트 사용자 만들기

tooenable Azure AD 사용자가 toolog HANA tooSAP에서 이러한 해야에 프로 비전 SAP HANA 합니다.
SAP HANA는 Just-In-Time 프로비전을 지원하며 기본적으로 사용하도록 설정됩니다.

Toocreate 사용자를 수동으로 해야 할 경우 hello 다음 단계를 수행 합니다.

>[!Note]
>Hello 외부 인증 hello 사용자에서 사용 하는 변경할 수 있습니다.
외부 사용자는 Kerberos 시스템 같은 외부 시스템을 사용하여 인증됩니다. 외부 ID에 대한 자세한 내용은 [도메인 관리자](https://cloudplatform.sap.com/contact.html)에게 문의하세요.

1. 열기 hello [SAP HANA Studio](https://help.sap.com/viewer/a2a49126a5c546a9864aae22c05c3d0e/2.0.01/en-us) SAML SSO에 대 한 관리자를 사용 하도록 설정한 hello DB 사용자도 합니다.

    ![사용자 만들기](./media/active-directory-saas-saphana-tutorial/sap5.png)

2. 눈금 hello 보이지 않는 확인란 toohello 왼쪽 **SAML** hello 구성 링크를 따릅니다.

3. 클릭 **추가** tooadd SAML IDP hello 및 클릭 **확인** 적절 한 SAML IDP hello 선택 합니다.

4. Hello 추가 **외부 Id** (예: 여기서는 BrittaSimon)를 추가하거나 **"모두"**를 선택하고 **확인**을 클릭합니다.

    >[!Note]
    >"ANY" 확인란을 선택 하지 않으면 다음 HANA hello 사용자 이름이 UPN hello hello 도메인 접미사 앞에 hello 사용자의 tooexactly 일치 hello 이름을 입력 해야 하는 경우 (즉, BrittaSimon@contoso.com HANA에 BrittaSimon 해질 수)입니다.

5. 테스트를 위해 모든 할당 **"XS"** 역할 toohello 사용자입니다.

    ![역할 할당](./media/active-directory-saas-saphana-tutorial/sap6.png)

    > [!TIP]
    > 해당 사용 사례에 적합한 권한만 부여해야 합니다.

6. Hello 사용자를 저장 합니다.

### <a name="assigning-hello-azure-ad-test-user"></a>Azure AD hello 테스트 사용자를 할당합니다.

이 섹션에서는 액세스 tooSAP HANA 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.

![Hello 사용자 역할 할당][200] 

**tooassign Britta Simon tooSAP HANA hello 다음 단계를 수행 합니다.**

1. Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.

    ![사용자 할당][201] 

2. Hello 응용 프로그램 목록에서 선택 **SAP HANA**합니다.

    ![사용자 할당](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_app.png) 

3. Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.

    ![hello "사용자 및 그룹" 링크][202] 

4. **추가** 단추를 클릭합니다. 그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.

    ![hello 할당 추가 창][203]

5. **사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.

6. **사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.

7. **할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.
    
### <a name="testing-single-sign-on"></a>Single Sign-On 테스트

이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.

Hello 액세스 패널에서에서 hello SAP HANA 타일을 클릭할 때 자동으로 로그온 tooyour SAP HANA 응용 프로그램을 구해야 합니다.
액세스 패널에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.

## <a name="additional-resources"></a>추가 리소스

* [방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와](active-directory-saas-tutorial-list.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_203.png

