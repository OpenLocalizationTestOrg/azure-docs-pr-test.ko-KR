---
title: "자습서: Wdesk와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Wdesk 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 06900a91-a326-4663-8ba6-69ae741a536e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 2c278a5e4f50cc362663efc0f826ff0c0fcf6e7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wdesk"></a>자습서: Wdesk와 Azure Active Directory 통합

이 자습서에 설명 어떻게 toointegrate Wdesk Azure Active directory (Azure AD).

다음 이점을 hello로 제공 Wdesk Azure AD와 통합:

- 액세스 tooWdesk을 지닌 Azure AD에서 제어할 수 있습니다.
- 프로그램 사용자 tooautomatically get 로그온 tooWdesk (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.
- 하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.

Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 참조 tooknow 하려는 경우. [Azure Active Directory를 사용한 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.

## <a name="prerequisites"></a>필수 조건

다음 항목 hello가 필요 tooconfigure Wdesk와 Azure AD 통합 합니다.

- Azure AD 구독
- Wdesk Single Sign-On이 설정된 구독

> [!NOTE]
> 이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.

이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.

- 꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.
- Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.

## <a name="scenario-description"></a>시나리오 설명
이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다. 이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.

1. Wdesk은 hello 갤러리 추가
2. Azure AD Single Sign-on 구성 및 테스트

## <a name="adding-wdesk-from-hello-gallery"></a>Wdesk은 hello 갤러리 추가
tooconfigure hello와의 통합 Wdesk Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Wdesk tooadd가 필요합니다.

**hello 갤러리에서 Wdesk tooadd hello 다음 단계를 수행 합니다.**

1. Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다. 

    ![Active Directory][1]

2. 너무 이동**엔터프라이즈 응용 프로그램**합니다. 이동 하 여 너무**모든 응용 프로그램**합니다.

    ![응용 프로그램][2]
    
3. tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.

    ![응용 프로그램][3]

4. Hello 검색 상자에 입력 **Wdesk**합니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_search.png)

5. Hello 결과 패널에서 선택 **Wdesk**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Azure AD Single Sign-on 구성 및 테스트
이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Wdesk에서 Azure AD Single Sign-On을 구성하고 테스트합니다.

Single sign on toowork에 대 한 Azure AD는 tooknow Wdesk에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다. 즉, Azure AD 사용자 및 Wdesk에 hello 관련된 사용자 간 링크 관계를 설정할 toobe가 필요 합니다.

Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** Wdesk에 합니다.

tooconfigure 및 Wdesk 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.

1. **[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.
2. **[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.
3. **[Wdesk 테스트 사용자 만들기](#creating-a-wdesk-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 Wdesk에 해당 하는 도구입니다.
4. **[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.
5. **[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성

이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 Wdesk 응용 프로그램에서 single sign on 구성 합니다.

**tooconfigure Azure AD single sign on, Wdesk와 hello 다음 단계를 수행 합니다.**

1. Hello hello에 Azure 포털에서에서 **Wdesk** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.

    ![Single Sign-on 구성][4]

2. Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.
 
    ![Single Sign-on 구성](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_samlbase.png)

3. Hello에 **Wdesk 도메인 및 Url** tooconfigure hello 응용 프로그램에 필요한 경우 섹션 **IDP** 시작된 모드 hello 다음 단계를 수행:

    ![Single Sign-on 구성](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_url.png)

    a. Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<subdomain>.wdesk.com/auth/saml/sp/metadata/<instancename>`

    b. Hello에 **회신 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<subdomain>.wdesk.com/auth/saml/sp/consumer/<instancename>`

4. **고급 URL 설정 표시**를 선택합니다. Tooconfigure hello 응용 프로그램에 필요한 경우 **SP** 시작 모드를 hello 단계 다음에 수행:

    ![Single Sign-on 구성](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_url1.png)

    Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<subdomain>.wdesk.com/auth/login/saml/<instancename>`
     
    > [!NOTE] 
    > 이러한 값은 실제 값이 아닙니다. 이러한 항목을 업데이트 식별자, 회신 URL 및 로그온 URL 실제 hello로 값입니다. Hello SSO를 구성할 때 WDesk 포털에서 이러한 값을 가져옵니다. 
  
5. Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello 메타 데이터 파일을 컴퓨터에 저장 합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_certificate.png) 

6. **저장** 단추를 클릭합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-wdesk-tutorial/tutorial_general_400.png)
    
7. 다른 웹 브라우저 창에서 로그인 tooWdesk 보안 관리자는 합니다.

8. Hello 아래 왼쪽에서 클릭 **Admin** 선택 **계정 관리자**:
 
     ![Single Sign-on 구성](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig1.png)

9. 너무 Wdesk Admin 이동**보안**, 다음 **SAML** > **SAML 설정**:

    ![Single Sign-on 구성](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig2.png)

10. 아래 **일반 설정**, hello 확인 **사용 SAML Single Sign On**:

    ![Single Sign-on 구성](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig3.png)

11. 아래 **서비스 공급자 세부 정보**, hello 다음 단계를 수행 합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig4.png)

      a. 복사 hello **로그인 URL** 붙여 넣습니다 **로그온 Url** Azure 포털에서 텍스트 상자에 붙여넣습니다.
   
      b. 복사 hello **메타 데이터 Url** 붙여 넣습니다 **식별자** Azure 포털에서 텍스트 상자에 붙여넣습니다.
       
      c. 복사 hello **소비자 url** 붙여 넣습니다 **회신 Url** Azure 포털에서 텍스트 상자에 붙여넣습니다.
   
      d. 클릭 **저장** Azure 포털 toosave hello 달라 집니다.      

12. 클릭 **IdP 설정 구성** tooopen **IdP 설정 편집** 대화 상자. 클릭 **파일 선택** toolocate hello **Metadata.xml** 저장 한 파일을 Azure 포털에서 다음 업로드 합니다.
    
    ![Single Sign-on 구성](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig5.png)
  
13. **변경 내용 저장**을 클릭합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfigsavebutton.png)

> [!TIP]
> 이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!  Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션. 자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Azure AD 테스트 사용자 만들기
이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.

![Azure AD 사용자 만들기][100]

**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**

1. Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-wdesk-tutorial/create_aaduser_01.png) 

2. 사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-wdesk-tutorial/create_aaduser_02.png) 

3. tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-wdesk-tutorial/create_aaduser_03.png) 

4. Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-wdesk-tutorial/create_aaduser_04.png) 

    a. Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.

    b. Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.

    c. 선택 **암호 표시** hello hello 값 기록 **암호**합니다.

    d. **만들기**를 클릭합니다.
 
### <a name="creating-a-wdesk-test-user"></a>Wdesk 테스트 사용자 만들기

tooenable Azure AD 사용자가 toolog tooWdesk에서 이러한 해야에 프로 비전 Wdesk 합니다. Wdesk의 경우, 수동으로 프로비전합니다.

**tooprovision 사용자 계정을 hello 다음 단계를 수행 합니다.**

1. 보안 관리자는 tooWdesk에 로그인 합니다.
2. 너무 이동**Admin** > **계정 관리자**합니다.

     ![Single Sign-on 구성](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig1.png)

3. **피플** 아래에서 **구성원**을 클릭합니다.

4. 클릭 하 여 지금 **멤버 추가** tooopen **멤버 추가** 대화 상자. 
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-wdesk-tutorial/createuser1.png)  

5. **사용자** 텍스트 상자와 같은 사용자의 hello 사용자 이름을 입력 합니다  **brittasimon@contoso.com**  클릭 **계속** 단추입니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-wdesk-tutorial/createuser3.png)

6.  아래와 같이 hello 세부 정보를 입력 합니다.
  
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-wdesk-tutorial/createuser4.png)
 
    a. **전자 메일** 텍스트 상자에 입력와 같은 사용자의 전자 메일 hello  **brittasimon@contoso.com** 합니다.

    b. **이름** 텍스트 상자에 hello와 같은 사용자 이름을 입력 합니다 **Britta**합니다.

    c. **성** 텍스트 상자에서 hello와 같은 사용자의 성을 입력 **Simon**합니다.

7. **구성원 저장** 단추를 클릭합니다.  

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-wdesk-tutorial/createuser5.png)

### <a name="assigning-hello-azure-ad-test-user"></a>Azure AD hello 테스트 사용자를 할당합니다.

이 섹션에서는 tooWdesk 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.

![사용자 할당][200] 

**tooassign Britta Simon tooWdesk hello 다음 단계를 수행 합니다.**

1. Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.

    ![사용자 할당][201] 

2. Hello 응용 프로그램 목록에서 선택 **Wdesk**합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_app.png) 

3. Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.

    ![사용자 할당][202] 

4. **추가** 단추를 클릭합니다. 그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.

    ![사용자 할당][203]

5. **사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.

6. **사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.

7. **할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.
    
### <a name="testing-single-sign-on"></a>Single Sign-On 테스트

이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.

Hello 액세스 패널에서에서 hello Wdesk 타일을 클릭할 때 자동으로 로그온 tooyour Wdesk 응용 프로그램을 구해야 합니다.
액세스 패널에 대한 자세한 내용은 [Azure 시작](active-directory-saas-access-panel-introduction.md)을 참조하세요.


## <a name="additional-resources"></a>추가 리소스

* [방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와](active-directory-saas-tutorial-list.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_203.png

