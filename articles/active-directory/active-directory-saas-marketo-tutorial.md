---
title: "자습서: Marketo와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Marketo 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b88c45f5-d288-4717-835c-ca965add8735
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 87f88cde4f027f99a83c1ab3b318247bb4d658ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-marketo"></a>자습서:Azure Active Directory와 Marketo 통합

이 자습서에 설명 어떻게 toointegrate Marketo Azure Active directory (Azure AD).

Marketo Azure AD와 통합 hello 다음 이점을 제공 합니다.

- 액세스 tooMarketo을 지닌 Azure AD에서 제어할 수 있습니다.
- 프로그램 사용자 tooautomatically get 로그온 tooMarketo (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.
- 하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.

Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.

## <a name="prerequisites"></a>필수 조건

Marketo와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.

- Azure AD 구독
- Marketo Single Sign-On이 설정된 구독

> [!NOTE]
> 이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.

이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.

- 꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.
- Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.

## <a name="scenario-description"></a>시나리오 설명
이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다. 이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.

1. Marketo는 hello 갤러리 추가
2. Azure AD Single Sign-on 구성 및 테스트

## <a name="adding-marketo-from-hello-gallery"></a>Marketo는 hello 갤러리 추가
tooconfigure hello와의 통합 Marketo Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Marketo tooadd가 필요합니다.

**hello 갤러리에서 Marketo tooadd hello 다음 단계를 수행 합니다.**

1. Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다. 

    ![Active Directory][1]

2. 너무 이동**엔터프라이즈 응용 프로그램**합니다. 이동 하 여 너무**모든 응용 프로그램**합니다.

    ![응용 프로그램][2]
    
3. tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.

    ![응용 프로그램][3]

4. Hello 검색 상자에 입력 **Marketo**합니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_search.png)

5. Hello 결과 패널에서 선택 **Marketo**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Azure AD Single Sign-on 구성 및 테스트
이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Marketo에서 Azure AD Single Sign-On을 구성하고 테스트합니다.

Single sign on toowork에 대 한 Azure AD는 tooknow marketo에서 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다. 즉, Azure AD 사용자 및 marketo에서 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.

Marketo에 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.

tooconfigure 및 Marketo와 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.

1. **[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.
2. **[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.
3. **[Marketo 테스트 사용자 만들기](#creating-a-marketo-test-user)**  -toohave 사용자의 연결 된 Azure AD toohello 표현인 marketo Britta Simon의 해당 하는 도구입니다.
4. **[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.
5. **[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성

이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 Marketo 응용 프로그램에서 single sign on 구성 합니다.

**Azure AD tooconfigure single sign on Marketo와 hello 다음 단계를 수행 합니다.**

1. Hello hello에 Azure 포털에서에서 **Marketo** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.

    ![Single Sign-on 구성][4]

2. Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.
 
    ![Single Sign-on 구성](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_samlbase.png)

3. Hello에 **Marketo 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_url.png)

    a. Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://saml.marketo.com/sp`

    b. Hello에 **회신 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://login.marketo.com/saml/assertion/\<munchkinid\>`

    > [!NOTE] 
    > 이러한 값은 실제 값이 아닙니다. Hello 실제 식별자 및 회신 URL로이 값을 업데이트 합니다. 연락처 [Marketo 지원 팀](http://investors.marketo.com/contactus.cfm) tooget 이러한 값입니다.
 
4. Hello에 **SAML 서명 인증서** 섹션에서 클릭 **인증서 (Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_certificate.png) 

5. **저장** 단추를 클릭합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-marketo-tutorial/tutorial_general_400.png)

6. Hello에 **Marketo 구성** 섹션에서 클릭 **구성 Marketo** tooopen **sign on 구성** 창. 복사 hello **Sign-Out URL, SAML 엔터티 ID, 및 SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**

    ![Single Sign-on 구성](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_configure.png) 

7. tooMarketo 관리자 자격 증명을 사용 하 여 로그인 하 고 다음 작업을 수행 하는 응용 프로그램의 Munchkin Id tooget:
   
    a. 관리자 자격 증명을 사용 하 여 tooMarketo 앱에 로그인 합니다.
   
    b. Hello 클릭 **Admin** hello 위쪽 탐색 창에서 단추입니다.
   
    ![Single Sign-on 구성](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    c. Toohello 통합 메뉴를 탐색 하 고 hello 클릭 **Munchkin 링크**합니다.
   
    ![Single Sign-on 구성](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_11.png)
   
    d. Hello hello 화면에 표시 된 Munchkin Id를 복사 하 고 회신 URL hello Azure AD 구성 마법사에서를 완료 합니다.
   
    ![Single Sign-on 구성](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_12.png) 

8. hello 응용 프로그램에 대 한 SSO tooconfigure hello hello 아래 단계를 수행 합니다.
   
    a. 관리자 자격 증명을 사용 하 여 tooMarketo 앱에 로그인 합니다.
   
    b. Hello 클릭 **Admin** hello 위쪽 탐색 창에서 단추입니다.
   
    ![Single Sign-on 구성](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    c. Toohello 통합 메뉴를 탐색 하 고 클릭 **Single Sign On**합니다.
   
    ![Single Sign-on 구성](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_07.png) 
   
    d. SAML 설정 tooenable hello 클릭 **편집** 단추입니다.
   
    ![Single Sign-on 구성](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_08.png) 
   
    e. Single Sign-On 설정을 사용하도록 **설정**합니다.
   
    f. 붙여넣기 hello **SAML 엔터티 ID**, hello에 **발급자 ID** 텍스트 상자에 붙여넣습니다.
   
    g. Hello에 **엔터티 ID** textbox hello URL로 입력 `http://saml.marketo.com/sp`합니다.
   
    h. 사용자 ID 위치 선택 hello로 **Name Identifier 요소**합니다.
   
    ![Single Sign-on 구성](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_09.png)
   
    > [!NOTE]
    > 사용자 식별자는 UPN 값 다음에 hello 특성 탭 hello 값 변경 되지 않습니다.
   
    i. Azure AD 구성 마법사에서 다운로드 한 hello 인증서를 업로드 합니다. **저장** hello 설정 합니다.
   
    j. Hello 리디렉션 페이지 설정을 편집 합니다.
   
    k. 붙여넣기 hello **SAML Single Sign-on 서비스 URL** hello에 **로그인 URL** 텍스트 상자에 붙여넣습니다.
   
    l. 붙여넣기 hello **Sign-Out URL** hello에 **로그 아웃 URL** 텍스트 상자에 붙여넣습니다.
   
    m. Hello에 **오류 URL**, 복사 하면 **Marketo 인스턴스 URL** 클릭 **저장** toosave 설정 단추입니다.
   
    ![Single Sign-on 구성](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_10.png)

9. tooenable hello SSO 사용자에 대 한 작업을 수행 하는 전체 hello:
   
    a. 관리자 자격 증명을 사용 하 여 tooMarketo 앱에 로그인 합니다.
   
    b. Hello 클릭 **Admin** hello 위쪽 탐색 창에서 단추입니다.
   
    ![Single Sign-on 구성](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    c. Toohello 이동 **보안** 메뉴 **로그인 설정**합니다.
   
    ![Single Sign-on 구성](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_13.png)
   
    d. Hello 확인 **필요 SSO** 옵션 및 **저장** hello 설정 합니다.
   
    ![Single Sign-on 구성](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_14.png)

> [!TIP]
> 이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!  Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션. 자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Azure AD 테스트 사용자 만들기
이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.

![Azure AD 사용자 만들기][100]

**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**

1. Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-marketo-tutorial/create_aaduser_01.png) 

2. 사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-marketo-tutorial/create_aaduser_02.png) 

3. tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-marketo-tutorial/create_aaduser_03.png) 

4. Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-marketo-tutorial/create_aaduser_04.png) 

    a. Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.

    b. Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.

    c. 선택 **암호 표시** hello hello 값 기록 **암호**합니다.

    d. **만들기**를 클릭합니다.
 
### <a name="creating-a-marketo-test-user"></a>Marketo 테스트 사용자 만들기

이 섹션에서는 Marketo에서 Britta Simon이라는 사용자를 만듭니다. 이러한 단계 toocreate Marketo 플랫폼의 사용자를 따릅니다.

1. 관리자 자격 증명을 사용 하 여 tooMarketo 앱에 로그인 합니다.

2. Hello 클릭 **Admin** hello 위쪽 탐색 창에서 단추입니다.
   
    ![Single Sign-on 구성](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 

3. Toohello 이동 **보안** 메뉴 **사용자 및 역할**
   
    ![Single Sign-on 구성](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_19.png)  

4. Hello 클릭 **새 사용자를 초대** hello 사용자 탭의 링크
   
    ![Single Sign-on 구성](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_15.png) 

5. Hello 새 사용자를 초대 마법사 채우기 hello 정보 다음에
   
    a. Hello 사용자 입력 **전자 메일** hello 텍스트 상자에 주소
   
    ![Single Sign-on 구성](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_16.png)
   
    b. Hello 입력 **이름** hello 텍스트 상자에
   
    c. Hello 입력 **성** hello 텍스트 상자에
   
    d. **다음**을 누릅니다

6. Hello에 **권한을** 탭, 선택 hello **userRoles** 클릭 **다음**
   
    ![Single Sign-on 구성](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_17.png)
7. Hello 클릭 **보낼** toosend hello 사용자 초대 단추
   
    ![Single Sign-on 구성](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_18.png)

8. 사용자는 hello 전자 메일 알림을 수신 하 고 tooclick hello에 연결 하 고 hello 암호 tooactivate hello 계정을 변경 합니다. 

### <a name="assigning-hello-azure-ad-test-user"></a>Azure AD hello 테스트 사용자를 할당합니다.

이 섹션에서는 tooMarketo 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.

![사용자 할당][200] 

**tooassign Britta Simon tooMarketo hello 다음 단계를 수행 합니다.**

1. Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.

    ![사용자 할당][201] 

2. Hello 응용 프로그램 목록에서 선택 **Marketo**합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_app.png) 

3. Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.

    ![사용자 할당][202] 

4. **추가** 단추를 클릭합니다. 그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.

    ![사용자 할당][203]

5. **사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.

6. **사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.

7. **할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.
    
### <a name="testing-single-sign-on"></a>Single Sign-On 테스트

이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.

Hello 액세스 패널에서에서 hello Marketo 타일을 클릭할 때 자동으로 로그온 tooyour Marketo 응용 프로그램을 구해야 합니다.

## <a name="additional-resources"></a>추가 리소스

* [방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와](active-directory-saas-tutorial-list.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_203.png

