---
title: "자습서: Cezanne HR 소프트웨어와 Azure Active Directory 통합| Microsoft Docs"
description: "단일 로그온 tooconfigure 방법을 알아보려면 Azure Active Directory와 Cezanne HR 소프트웨어 간의 합니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: fb8f95bf-c3c1-4e1f-b2b3-3b67526be72d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 3675acd8871d62c2277def8074f7aa39ac46e2a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-integrate-azure-active-directory-with-cezanne-hr-software"></a>자습서: Cezanne HR 소프트웨어와 Azure Active Directory 통합

이 자습서에 설명 어떻게 toointegrate Cezanne HR 소프트웨어와 Azure Active Directory (Azure AD).

Cezanne HR 소프트웨어 Azure AD와 통합 hello 다음 이점을 제공 합니다. 다음을 수행할 수 있습니다.

- HR 소프트웨어 액세스 tooCezanne을 지닌 Azure AD에서 제어 합니다.
- Single sign-on에서 SSO ()는 Azure AD 계정을 사용 tooCezanne HR 소프트웨어에 대 한 사용자가 tooautomatically 로그인을 사용 하도록 설정 합니다.
- 하나의 중앙 위치에 계정 관리: hello Azure 포털입니다.

로 Azure AD와 saas () 응용 프로그램 통합 소프트웨어에 대해 자세히 toolearn 참조 [응용 프로그램 액세스 및 SSO 및 Azure Active Directory 란?](active-directory-appssoaccess-whatis.md)합니다.

## <a name="prerequisites"></a>필수 조건

다음 항목 hello가 필요 tooconfigure Cezanne HR software와 Azure AD 통합 합니다.

- Azure AD 구독
- Cezanne HR 소프트웨어 SSO가 설정된 구독

> [!NOTE]
> 이 자습서의 tootest hello 단계, 프로덕션 환경 사용 하지 않으면 두는 것이 좋습니다.

이 자습서의 tootest hello 단계에는 이러한 권장 사항을 따르십시오.

- 꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.
- Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.

## <a name="scenario-description"></a>시나리오 설명
이 자습서에서는 테스트 환경에서 Azure AD SSO를 테스트합니다. 

이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.

* Hello 갤러리에서 Cezanne HR 소프트웨어 추가
* Azure AD SSO 구성 및 테스트

## <a name="add-cezanne-hr-software-from-hello-gallery"></a>Hello 갤러리에서 Cezanne HR 소프트웨어를 추가 합니다.
tooconfigure hello 통합 Cezanne HR 소프트웨어의 Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Cezanne HR 소프트웨어를 추가 합니다.

tooadd hello 갤러리에서 Cezanne HR 소프트웨어 않으면 다음 hello:

1. Hello에 ** [Azure 포털](https://portal.azure.com)**hello 왼쪽된 창에서 선택 hello **Azure Active Directory** 단추입니다. 

    ![hello "Azure Active Directory" 단추][1]

2. **엔터프라이즈 응용 프로그램** > **모든 응용 프로그램**을 선택합니다.

    !["모든 응용 프로그램" 링크를 hello][2]
    
3. tooadd hello hello 위쪽에 새 응용 프로그램 **모든 응용 프로그램** 대화 상자에서 **새 응용 프로그램**합니다.

    !["새 응용 프로그램" hello 단추][3]

4. Hello 검색 상자에 입력 **Cezanne HR 소프트웨어**합니다.

    ![hello 검색 상자](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_search.png)

5. Hello 결과 목록에서 선택 **Cezanne HR 소프트웨어** 선택한 후 hello **추가** tooadd hello 응용 프로그램 단추입니다.

    ![hello 결과 목록](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성 및 테스트
이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Cezanne HR 소프트웨어에서 Azure AD SSO를 구성하고 테스트합니다.

SSO toowork에 대 한 Azure AD tooknow hello Cezanne HR 소프트웨어 대응 toohello Azure AD 사용자는 필요 합니다. 즉, hello Cezanne HR 소프트웨어에에서는 Azure AD 사용자 및 hello 관련된 사용자 간의 링크 관계를 설정 해야 합니다.

tooestablish hello 링크 관계를 할당 hello Cezanne HR 소프트웨어 **사용자 이름** hello Azure AD로 값 **Username** 값입니다.

tooconfigure 및 Azure AD SSO Cezanne HR 소프트웨어, 구성 요소를 다음 전체 hello를 사용 하 여 테스트 합니다.

### <a name="configure-azure-ad-sso"></a>Azure AD SSO 구성

이 섹션에서는 Azure AD SSO hello Azure 포털에서에서 사용 하도록 설정 및 hello 다음을 수행 하 여 Cezanne HR 소프트웨어 응용 프로그램에서 SSO를 구성할 수 있습니다.

1. Hello hello에 Azure 포털에서에서 **Cezanne HR 소프트웨어** 응용 프로그램 통합 페이지에서 선택 **Single sign on**합니다.

    ![명령 "Single sign-on" hello][4]

2. hello에 SSO, tooenable **Single sign on** 대화 상자, 선택 hello **모드** 으로 **SAML 기반 로그온**합니다.
 
    ![hello "모드" 상자](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_samlbase.png)

3. 아래 **Cezanne HR 소프트웨어 도메인 및 Url**, 다음 hello지 않습니다.

    ![hello "Cezanne HR 소프트웨어 도메인 및 Url" 섹션](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_url.png)

    a. Hello에 **로그온 URL** 상자 구문 다음 hello에 URL을 입력 합니다.`https://w3.cezanneondemand.com/cezannehr/-/<tenant id>`

    b. Hello에 **회신 URL** 상자 구문 다음 hello에 URL을 입력 합니다.`https://w3.cezanneondemand.com:443/<tenantid>`    
     
    > [!NOTE] 
    > hello 이전 값이 실제. Hello 실제 회신 URL 및 hello 로그온 URL을 업데이트 합니다. tooobtain hello 값, 연락처 hello [Cezanne HR 소프트웨어 클라이언트 지원 팀](mailto:info@cezannehr.com)합니다.

4. 아래 **SAML 서명 인증서**선택, **인증서 (Base64)**, hello 인증서 파일을 컴퓨터에 저장 합니다.

    ![hello "SAML 서명 인증서" 섹션](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_certificate.png) 

5. **저장**을 선택합니다.

    ![hello "저장" 단추](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_400.png)
    
6. 아래 **Cezanne HR 소프트웨어 구성**선택, **Cezanne HR 소프트웨어 구성** tooopen hello **sign on 구성** 창. 복사 hello **SAML 엔터티 ID** 및 **SAML Single Sign On 서비스** hello에서 URL **빠른 참조** 섹션.

    ![hello "Cezanne HR 소프트웨어 구성" 섹션](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_configure.png) 

7. 다른 웹 브라우저 창에서 관리자 권한으로 tooyour Cezanne HR software 테 넌 트에 로그인 합니다.

8. Hello 왼쪽된 창에서 선택 **System 설치**합니다. **보안 설정** > **Single Sign-on 구성**을 선택합니다.

    ![hello "Single Sign On 구성" 링크](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_000.png)

9. Hello에 **Single Sign-on (SSO) 서비스를 수행 하는 hello를 사용 하 여 사용자가 toolog 허용** 창, 선택 hello **SAML 2.0** 확인란과 선택 hello **고급 구성** 옵션입니다.

    ![Single Sign-On 서비스 옵션](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_001.png)

10. **새로 추가**를 선택합니다.

    ![hello "새로 추가" 단추](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_002.png)

11. 아래 **SAML 2.0 Id 공급자**, 다음 hello지 않습니다.

    ![hello "SAML 2.0 Id 공급자" 섹션](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_003.png)
    
    a. Hello에 **표시 이름** id 공급자의 hello 이름을 입력 합니다.

    b. Hello에 **엔터티 식별자** 상자, 붙여넣기 hello **SAML 엔터티 ID** hello Azure 포털에서에서 복사 합니다. 

    c. Hello에 **SAML 바인딩** 목록 상자 **POST**합니다.

    d. Hello에 **보안 토큰 서비스 끝점** 상자, 붙여넣기 hello **SAML Single Sign On 서비스** hello Azure 포털에서에서 복사한 URL입니다. 
    
    e. Hello에 **사용자 ID 특성 이름** 상자에 입력 `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`합니다.
    
    f. Azure AD를 선택 하는 hello에서 인증서를 다운로드 하는 tooupload hello **업로드** 단추입니다.
    
    g. **확인**을 선택합니다. 

12. **저장**을 선택합니다.

    ![hello "저장" 단추](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_004.png)

> [!TIP]
> Hello 지침 hello에서 앞의 간결한 버전을 읽을 수 hello 앱을 설정할 때 [Azure 포털](https://portal.azure.com)합니다. Hello에서 hello 앱을 추가한 다음 **Active Directory** > **엔터프라이즈 응용 프로그램** 섹션을 선택 하는 hello **Single sign on** 탭 합니다. 액세스 hello hello의 설명서를 포함 하는 후 **구성** 섹션. 

hello 포함 된 설명서 기능에 대해 자세히 toolearn 참조 [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)합니다.
> 

### <a name="create-an-azure-ad-test-user"></a>Azure AD 테스트 사용자 만들기
이 섹션에서는 테스트 사용자 Britta Simon hello Azure 포털에서에서 만들 수 있습니다.

![Britta Simon hello 테스트 사용자][100]

Azure AD에서 테스트 사용자 toocreate 다음 hello지 않습니다.

1. Hello에 **Azure 포털**hello 왼쪽된 창에서 선택 hello **Azure Active Directory** 단추입니다.

    ![hello "Azure Active Directory" 단추](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_01.png) 

2. 사용자 선택 toodisplay hello 목록 **사용자 및 그룹** > **모든 사용자에 게**합니다.
    
    !["모든 사용자" 링크를 hello](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_02.png) 
    
    hello **모든 사용자에 게** 대화 상자가 열립니다.

3. tooopen hello **사용자** 대화 상자에서 **추가**합니다.
 
    ![hello "추가" 단추](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_03.png) 

4. Hello에 **사용자** 대화 상자에서 다음 hello지 않습니다.
 
    ![hello "User" 대화 상자](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_04.png) 

    a. Hello에 **이름** 상자에서 입력 **BrittaSimon**합니다.

    b. Hello에 **사용자 이름** 상자에 입력 사용자 Britta Simon **전자 메일 주소**합니다.

    c. 선택 hello **암호 표시** 확인란을 선택한 다음 참고 hello 생성 된 값을 hello에 **암호** 상자입니다.

    d. **만들기**를 선택합니다.
 
### <a name="create-a-cezanne-hr-software-test-user"></a>Cezanne HR 소프트웨어 테스트 사용자 만들기

tooenable Azure AD 사용자가 toosign tooCezanne HR 소프트웨어에서 이러한 해야에 프로 비전 Cezanne HR 소프트웨어. Hello Cezanne HR 소프트웨어의 경우에서 프로 비전은 수동 작업입니다.

Hello 다음을 수행 하 여 사용자 계정을 프로 비전 합니다.

1.  관리자 권한으로 Cezanne HR software 회사 사이트 tooyour에 로그인 합니다.

2.  Hello 왼쪽된 창에서 선택 **System 설치** > **사용자 관리** > **새 사용자 추가**합니다.

    ![hello "새 사용자 추가" 링크](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_005.png "새 사용자")

3.  **사용자 세부 정보**, 다음 hello지 않습니다.

    !["사용자 세부 정보" 섹션 hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_006.png "새 사용자")
    
    a. **내부 사용자**를 **OFF**로 설정합니다.
    
    b. Hello에 **이름** 상자, 형식 hello 사용자의 이름, 예를 들어 **Britta**합니다.  
 
    c. Hello에 **성** 상자, 형식 hello 사용자의 성, 예를 들어 **Simon**합니다.
    
    d. Hello에 **전자 메일** 상자 예를 들어 hello 사용자의 전자 메일 주소를 입력 합니다 Brittasimon@contoso.com합니다.

4.  아래 **계정 정보**, 다음 hello지 않습니다.

    !["계정 정보" 섹션 hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_007.png "새 사용자")
    
    a. Hello에 **Username** 상자 예를 들어 hello 사용자의 전자 메일 주소를 입력 합니다 Brittasimon@contoso.com합니다.
    
    b. Hello에 **암호** 상자 hello 사용자의 암호를 입력 합니다.
    
    c. Hello에 **보안 역할** 상자 **HR Professional**합니다.
    
    d. **확인**을 선택합니다.

5. Hello에 **Single sign on** 탭 hello **SAML 2.0 식별자** 섹션에서 **새로 추가**합니다.

    ![hello "새로 추가" 단추](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_008.png "사용자")

6. Hello에 **Id 공급자** 목록 상자에서 id 공급자를 선택 합니다. Hello에 **사용자 식별자** 상자 테스트 사용자 Britta Simon의 계정에 대 한 hello 전자 메일 주소를 입력 합니다.

    !["Id 공급자" 및 "사용자 식별자" 상자 hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_009.png "사용자")
    
7. **저장**을 선택합니다.

    ![hello "저장" 단추](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_010.png "사용자")

### <a name="assign-hello-azure-ad-test-user"></a>Azure AD hello 테스트 사용자를 할당 합니다.

이 섹션에서는 액세스 tooCezanne HR 소프트웨어를 부여 하 여 테스트 사용자 Britta Simon toouse Azure SSO를 사용 합니다.

![테스트 사용자 액세스][200] 

1. Azure 포털 hello에 hello 응용 프로그램 보기를 열고 고 toohello 디렉터리 보기를 이동 하십시오. **엔터프라이즈 응용 프로그램** > **모든 응용 프로그램**을 선택합니다.

    !["모든 응용 프로그램" 링크를 hello][201] 

2. Hello 응용 프로그램 목록에서 선택 **Cezanne HR 소프트웨어**합니다.

    ![hello "응용 프로그램" 목록](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_app.png) 

3. Hello hello 왼쪽 메뉴에서 선택 **사용자 및 그룹**합니다.

    ![사용자 할당][202] 

4. **추가**를 선택합니다. 그런 다음 hello **할당 추가** 대화 상자에서 **사용자 및 그룹**합니다.

    !["사용자 및 그룹" 링크][203]

5. Hello에 **사용자 및 그룹** 대화 상자의 hello **사용자** 목록에서 **Britta Simon**합니다.

6. Hello에 **사용자 및 그룹** 대화 상자에서 **선택**합니다.

7. Hello에 **할당 추가** 대화 상자에서 **할당**합니다.
    
### <a name="test-sso"></a>SSO 테스트

이 섹션에서는 hello 액세스 패널을 사용 하 여 Azure AD SSO 구성을 테스트 합니다.

Hello Cezanne HR 소프트웨어 타일 hello 액세스 패널을 선택 하면 자동으로 tooyour Cezanne HR 소프트웨어 응용 프로그램에 로그온 합니다.

## <a name="next-steps"></a>다음 단계

* [방법에 대 한 자습서 목록 toointegrate SaaS 앱 Azure Active Directory와](active-directory-saas-tutorial-list.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 SSO란 무엇입니까?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_203.png

