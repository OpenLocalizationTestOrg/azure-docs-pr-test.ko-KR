---
title: "자습서: Azure Active Directory와 Zscaler One 통합| Microsoft Azure"
description: "단일 로그온 tooconfigure 방법을 알아보려면 Azure Active Directory와 Zscaler One 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f352e00d-68d3-4a77-bb92-717d055da56f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 5179cb2cc54482334d574951a1ac64e722e5f578
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-one"></a>자습서: Azure Active Directory와 Zscaler One 통합

이 자습서에 설명 방법 (Azure AD) Azure Active Directory와 Zscaler One toointegrate 합니다.

Azure AD와 Zscaler One 통합 hello 다음 이점을 제공 합니다.

- Azure ad 액세스 tooZscaler 하나를 가진 제어할 수 있습니다.
- 프로그램 사용자 tooautomatically get 로그온 tooZscaler 하나 (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.
- 하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.

Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.

## <a name="prerequisites"></a>필수 조건

Zscaler One와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.

- Azure AD 구독
- ZScaler One Single Sign-On이 설정된 구독

> [!NOTE]
> 이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.

이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.

- 꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.
- Azure AD 평가판 환경이 없으면 [평가판 제품](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.

## <a name="scenario-description"></a>시나리오 설명
이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다. 이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.

1. Zscaler One hello 갤러리 추가
2. Azure AD Single Sign-on 구성 및 테스트

## <a name="adding-zscaler-one-from-hello-gallery"></a>Zscaler One hello 갤러리 추가
tooconfigure hello와의 통합 Zscaler One Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Zscaler One tooadd가 필요합니다.

**Zscaler One hello 갤러리에서 tooadd hello 다음 단계를 수행 합니다.**

1. Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다. 

    ![Active Directory][1]

2. 너무 이동**엔터프라이즈 응용 프로그램**합니다. 이동 하 여 너무**모든 응용 프로그램**합니다.

    ![응용 프로그램][2]
    
3. tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.

    ![응용 프로그램][3]

4. Hello 검색 상자에 입력 **Zscaler One**합니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-zscaler-one-tutorial/tutorial_zscalerone_search.png)

5. Hello 결과 패널에서 선택 **Zscaler One**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-zscaler-one-tutorial/tutorial_zscalerone_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Azure AD Single Sign-on 구성 및 테스트
이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 사용하여 Zscaler One에서 Azure AD Single Sign-On을 구성하고 테스트합니다.

Single sign on toowork에 대 한 Azure AD는 tooknow Zscaler One에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다. 즉, Azure AD 사용자와 Zscaler one hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.

Zscaler one hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.

tooconfigure 및 Zscaler One을 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.

1. **[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.
2. **[프록시 설정 구성](#configuring-proxy-settings)**  -Internet Explorer의 tooconfigure hello 프록시 설정
3. **[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.
4. **[Zscaler One 테스트 사용자 만들기](#creating-a-zscaler-one-test-user)**  -toohave Zscaler one 표현인 연결 된 toohello Azure AD 사용자의 Britta Simon의 해당 하는 도구입니다.
5. **[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.
6. **[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성

이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 사용 하도록 설정 및 응용 프로그램 Zscaler One에서 single sign on 구성 합니다.

**tooconfigure Azure AD single sign on와 Zscaler One hello 다음 단계를 수행 합니다.**

1. Hello hello에 Azure 포털에서에서 **Zscaler One** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.

    ![Single Sign-on 구성][4]

2. Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.
 
    ![Single Sign-on 구성](./media/active-directory-saas-zscaler-one-tutorial/tutorial_zscalerone_samlbase.png)

3. Hello에 **Zscaler 한 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-zscaler-one-tutorial/tutorial_zscalerone_url.png)

    Hello 로그온 URL 텍스트 상자에서에 사용자에 대 한 toosign tooyour Zscaler One 응용 프로그램에서 사용 하는 hello URL을 입력 합니다.

    > [!NOTE] 
    > 이 값이 hello로 tooupdate 되어 실제 로그온 URL입니다. 연락처 [하나의 클라이언트 Zscaler 지원 팀](https://www.zscaler.com/company/contact) tooget 이러한 값입니다.

4. Hello에 **SAML 서명 인증서** 섹션에서 클릭 **Certificate(Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-zscaler-one-tutorial/tutorial_zscalerone_certificate.png) 

5. **저장** 단추를 클릭합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_400.png)

6. Hello에 **Zscaler 하나의 구성** 섹션에서 클릭 **Zscaler One 구성** tooopen **sign on 구성** 창. 복사 hello **SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**

    ![Single Sign-on 구성](./media/active-directory-saas-zscaler-one-tutorial/tutorial_zscalerone_configure.png) 

7. 다른 웹 브라우저 창에서 관리자 권한으로 tooyour Zscaler One 회사 사이트에 로그인 합니다.

8. Hello 메뉴에서 hello 위에 표시를 클릭 **관리**합니다.
   
    ![관리](./media/active-directory-saas-zscaler-one-tutorial/ic800206.png "관리")

9. **관리자 & 역할 관리**에서 **사용자 및 인증 관리**를 클릭합니다.   
            
    ![사용자 및 인증 관리](./media/active-directory-saas-zscaler-one-tutorial/ic800207.png "사용자 및 인증 관리")

10. Hello에 **조직에 대 한 인증 옵션 선택** 섹션를 hello 다음 단계를 수행 합니다.   
                
    ![인증](./media/active-directory-saas-zscaler-one-tutorial/ic800208.png "인증")
   
    a. **SAML Single Sign-On을 사용하여 인증**을 선택합니다.

    b. **SAML Single Sign-On 매개 변수 구성**을 클릭합니다.

11. Hello에 **SAML Single Sign-on 매개 변수 구성** 대화 상자 페이지에서 단계에 따라 hello를 수행 하 고 클릭 한 다음 **수행**

    ![Single Sign-On](./media/active-directory-saas-zscaler-one-tutorial/ic800209.png "Single Sign-On")
    
    a. 붙여넣기 hello **SAML Single Sign-on 서비스 URL** hello에 hello Azure 포털에서에서 복사한 값 **hello SAML 포털 toowhich 사용자의 URL은 인증을 위해 전송** 텍스트 상자에 붙여넣습니다.
    
    b. Hello에 **로그인 이름이 포함 된 특성** 텍스트 상자에 **NameID**합니다.
    
    c. tooupload 다운로드 한 인증서를 클릭 하 여 **Zscaler pem**합니다.
    
    d. **SAML 자동 프로비전 사용**을 선택합니다.

12. Hello에 **사용자 인증 구성** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.

    ![관리](./media/active-directory-saas-zscaler-one-tutorial/ic800210.png "관리")
    
    a. **Save**를 클릭합니다.

    b. **지금 활성화**를 클릭합니다.

## <a name="configuring-proxy-settings"></a>프록시 설정 구성
### <a name="tooconfigure-hello-proxy-settings-in-internet-explorer"></a>Internet Explorer의 tooconfigure hello 프록시 설정

1. **Internet Explorer**를 시작합니다.

2. 선택 **인터넷 옵션** hello에서 **도구** 열려 hello에 대 한 메뉴 **인터넷 옵션** 대화 상자.   
    
     ![인터넷 옵션](./media/active-directory-saas-zscaler-one-tutorial/ic769492.png "인터넷 옵션")

3. Hello 클릭 **연결** 탭 합니다.   
  
     ![연결](./media/active-directory-saas-zscaler-one-tutorial/ic769493.png "연결")

4. 클릭 **LAN 설정** tooopen hello **LAN 설정** 대화 상자.

5. Hello 모드 해제 프록시 서버 섹션에서에서 단계를 수행 하는 hello를 수행 합니다.   
   
    ![프록시 서버](./media/active-directory-saas-zscaler-one-tutorial/ic769494.png "프록시 서버")

    a. **사용자 LAN의 프록시 서버 사용**을 선택합니다.

    b. Hello 주소 텍스트 상자에 입력 **gateway.zscalerone.net**합니다.

    c. Hello 포트 텍스트 상자에 입력 **80**합니다.

    d. **로컬 주소의 바이패스 프록시 서버**를 선택합니다.

    e. 클릭 **확인** tooclose hello **Local Area Network (LAN) 설정** 대화 상자.

6. 클릭 **확인** tooclose hello **인터넷 옵션** 대화 상자.

> [!TIP]
> 이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!  Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션. 자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Azure AD 테스트 사용자 만들기
이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.

![Azure AD 사용자 만들기][100]

**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**

1. Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-zscaler-one-tutorial/create_aaduser_01.png) 

2. 사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-zscaler-one-tutorial/create_aaduser_02.png) 

3. tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-zscaler-one-tutorial/create_aaduser_03.png) 

4. Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-zscaler-one-tutorial/create_aaduser_04.png) 

    a. Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.

    b. Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.

    c. 선택 **암호 표시** hello hello 값 기록 **암호**합니다.

    d. **만들기**를 클릭합니다.
 
### <a name="creating-a-zscaler-one-test-user"></a>Zscaler One 테스트 사용자 만들기

tooenable Azure AD 사용자가 toolog 하나 프로 비전 된 tooZscaler tooZscaler 하나에에서 있어야 합니다. Hello Zscaler One의 경우에서 프로 비전은 수동 작업입니다.

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a>tooconfigure 사용자 프로비저닝, hello 다음 단계를 수행:

1. Tooyour 로그인 **Zscaler One** 테 넌 트입니다.

2. **관리**를 클릭합니다.   
   
    ![관리](./media/active-directory-saas-zscaler-one-tutorial/ic781035.png "관리")

3. **사용자 관리**를 클릭합니다.   
        
     ![추가](./media/active-directory-saas-zscaler-one-tutorial/ic781036.png "추가")

4. Hello에 **사용자** 탭을 클릭 **추가**합니다.
      
    ![추가](./media/active-directory-saas-zscaler-one-tutorial/ic781037.png "추가")

5. Hello 사용자 추가 섹션에서에서 단계를 수행 하는 hello를 수행 합니다.
        
    ![사용자 추가](./media/active-directory-saas-zscaler-one-tutorial/ic781038.png "사용자 추가")
   
    a. 형식 hello **UserID**, **사용자 표시 이름**, **암호**, **암호 확인**를 선택한 후 **그룹**및 hello **부서** 유효한 azure AD 계정 tooprovision 원하는 합니다.

    b. **Save**를 클릭합니다.

> [!NOTE]
> 다른 Zscaler One 사용자 계정 만들기 도구를 사용할 수 있습니다 또는 Azure AD 사용자 계정을 tooprovision Zscaler One에서 제공 된 Api입니다.

### <a name="assigning-hello-azure-ad-test-user"></a>Azure AD hello 테스트 사용자를 할당합니다.

이 섹션에서는 액세스 tooZscaler 하나를 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.

![사용자 할당][200] 

**tooassign 하나, Britta Simon tooZscaler hello 다음 단계를 수행 합니다.**

1. Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.

    ![사용자 할당][201] 

2. Hello 응용 프로그램 목록에서 선택 **Zscaler One**합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-zscaler-one-tutorial/tutorial_zscalerone_app.png) 

3. Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.

    ![사용자 할당][202] 

4. **추가** 단추를 클릭합니다. 그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.

    ![사용자 할당][203]

5. **사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.

6. **사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.

7. **할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.
    
### <a name="testing-single-sign-on"></a>Single Sign-On 테스트

이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.

Hello 액세스 패널에서에서 hello Zscaler One 타일을 클릭할 때 자동으로 로그온 tooyour Zscaler One 응용 프로그램을 구해야 합니다.
액세스 패널 hello에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.

## <a name="additional-resources"></a>추가 리소스

* [방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와](active-directory-saas-tutorial-list.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_203.png

