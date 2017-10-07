---
title: "자습서: HR2day by Merces와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법에 대해 알아봅니다 Azure Active Directory와 Merces 여 HR2day 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 853d08c9-27b1-48d4-b8e7-3705140eb67f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/24/2017
ms.author: jeedes
ms.openlocfilehash: 257233767e1fddbaf115878cb0455acf61b2f5f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hr2day-by-merces"></a>자습서: HR2day by Merces와 Azure Active Directory 통합

이 자습서에 설명 방법으로 Azure Active Directory (Azure AD)와 Merces HR2day toointegrate 합니다.

다음 이점을 hello로 제공 HR2day Merces 하 여 Azure AD와 통합:

- Merces 하 여 액세스 tooHR2day을 지닌 Azure AD에서 제어할 수 있습니다.
- 에 로그인 한 사용자 tooautomatically 가져오기 tooHR2day Merces 하 여 자신의 Azure AD 계정으로 사용할 수 있습니다.
- 하나의 중앙 위치-hello Azure 포털에서 계정을 관리할 수 있습니다.

Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory를 사용한 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.

## <a name="prerequisites"></a>필수 조건

Merces 여 HR2day와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.

- Azure AD 구독
- HR2day by Merces Single Sign-On이 설정된 구독

> [!NOTE]
> 이 자습서의 단계를 프로덕션 환경 tootest hello를 사용 하지 않는 것이 좋습니다.

이 자습서의 tootest hello 단계에는 이러한 권장 사항을 따르십시오.

- 꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.
- 아직 없는 경우 [Azure AD의 1개월 평가판](https://azure.microsoft.com/pricing/free-trial/)을 사용합니다.  

## <a name="scenario-description"></a>시나리오 설명
이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다. 여기서 설명 하는 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.

1. Hello 갤러리에서 Merces 여 HR2day를 추가 합니다.
2. Azure AD Single Sign-on 구성 및 테스트

## <a name="add-hr2day-by-merces-from-hello-gallery"></a>Hello 갤러리에서 Merces 여 HR2day를 추가 합니다.
tooconfigure hello 통합 Merces 여 HR2day의 Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Merces 여 HR2day를 추가 합니다.

**hello 갤러리에서 Merces 여 HR2day tooadd hello 다음 단계를 수행 합니다.**

1. Hello에 [Azure 포털](https://portal.azure.com), 왼쪽된 탐색 창의 hello, hello 선택 **Azure Active Directory** 아이콘입니다. 

    ![Active Directory][1]

2. 너무 이동**엔터프라이즈 응용 프로그램**합니다. 이동 하 여 너무**모든 응용 프로그램**합니다.

    ![응용 프로그램][2]
    
3. tooadd 새 응용 프로그램을 선택 하는 hello **새 응용 프로그램** hello hello 대화 상자 위쪽에 단추입니다.

    ![응용 프로그램][3]

4. Hello 검색 상자에 입력 **Merces 여 HR2day**합니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_search.png)

5. Hello 결과 패널에서 선택 **Merces 여 HR2day**를 선택한 후 hello **추가** tooadd hello 응용 프로그램 단추입니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성 및 테스트
이 섹션에서는 “Britta Simon”이라는 테스트 사용자를 기반으로 HR2day by Merces에서 Azure AD Single Sign-On을 구성하고 테스트합니다.

Single sign on toowork에 대 한 Azure AD는 tooknow hello 테이블에 해당 사용자에 HR2day Merces 하 여 Azure AD에서 tooa 사용자가이 필요 합니다. 즉, tooestablish Azure AD 사용자와 Merces 여 HR2day에 hello 관련된 사용자 사이 연결 해야합니다.

Merces 여 HR2day, 할당 hello **사용자 이름** Azure AD에서 너무 **Username** tooestablish hello 관계입니다.

tooconfigure 및 Merces 여 HR2day 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.

1. [Azure AD single sign-on 구성](#configuring-azure-ad-single-sign-on): 사용자가 toouse이이 기능을 사용 합니다.
2. [Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user): Britta Simon으로 Azure AD Single Sign-On을 테스트합니다.
3. [Merces 테스트 사용자가 HR2day 만들기](#creating-an-hr2day-by-merces-test-user): Britta Simon의 해당 하는 도구 사용자의 연결 된 Azure AD toohello 표현인 Merces 여 HR2day에 만듭니다.
4. [Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user): Azure AD에서 single sign-on toouse Britta Simon 사용 하도록 설정 합니다.
5. [Single sign on 테스트](#testing-single-sign-on): hello 구성이 작동 하는지 여부를 확인 합니다.

### <a name="configure-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성

이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 Merces 응용 프로그램에 의해 프로그램 HR2day에서 single sign on 구성 합니다.

**tooconfigure Azure AD single sign on, Merces 여 HR2day와 hello 다음 단계를 수행 합니다.**

1. Hello hello에 Azure 포털에서에서 **Merces 여 HR2day** 응용 프로그램 통합 페이지에서 선택 **Single sign on**합니다.

    ![Single Sign-on 구성][4]

2. tooenable single sign on, hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온**합니다.
 
    ![Single Sign-On 구성](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_samlbase.png)

3. Hello에 **Merces 도메인 및 Url HR2day** 섹션에서 단계를 수행 하는 hello를 사용 합니다.

    ![Single Sign-On 구성](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_url.png)

    a. Hello에 **로그온 URL** 상자 hello 패턴을 사용 하 여 URL을 입력 합니다: `https://<tenantname>.force.com/<instancename>`합니다.

    b. Hello에 **식별자** 상자 hello 패턴을 사용 하 여 URL을 입력 합니다: `https://hr2day.force.com/<companyname>`합니다.

    > [!NOTE] 
    > 이러한 값은 실제 값이 아닙니다. Hello 실제 로그온 URL과 식별자와 이러한 값을 업데이트 합니다. 연락처 hello [Merces 클라이언트 지원 팀에서 HR2day](mailto:servicedesk@merces.nl) tooget 이러한 값입니다. 
 


4. Hello에 **SAML 서명 인증서** 섹션에서 **Certificate(Base64)**, hello 인증서 파일을 컴퓨터에 저장 합니다.

    ![Single Sign-On 구성](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_certificate.png) 

5. 이 섹션에서는 설명 방법을 Azure AD에서 자신의 계정으로 tooenable 사용자 tooauthenticate tooHR2day Merces 여 합니다. Hello SAML 프로토콜을 기반으로 하는 페더레이션을 사용 하 여이 수행 합니다.

    Merces 응용 프로그램에 의해 프로그램 HR2day tooadd 사용자 지정 특성 매핑을 tooyour SAML 토큰을 요구 하는 특정 형식으로 hello SAML 어설션이 필요 합니다. hello 스크린 샷 다음이 예를 보여 줍니다. 

    ![Single Sign-On 구성](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2day_00.png)
    
    > [!NOTE] 
    Hello를 문의 해야 합니다. SAML 어설션이 hello를 구성 하려면 먼저 [Merces 클라이언트 지원 팀에서 HR2day](mailto:servicedesk@merces.nl) 및 테 넌 트에 대 한 hello 고유 식별자 특성의 hello 값을 요청 합니다. 이 값 toocomplete hello 단계 hello 다음 섹션에 필요합니다. 

6. Hello에 **Single sign on** 대화 상자의 hello **사용자 특성** 섹션에서 다음 이미지는 hello와 같이 hello SAML 토큰 특성을 구성 합니다. 다음 단계를 수행 하는 hello를 수행 합니다.
    
      | 특성 이름    |   특성 값 |  
    | ------------------- | -------------------- |    
    | ATTR_LOGINCLAIM | join([mail],"102938475Z","@" |
    
      a. tooopen hello **특성 추가** 대화 상자에서 **특성 추가**합니다.

    ![Single Sign-On 구성](./media/active-directory-saas-hr2day-tutorial/tutorial_attribute_04.png)

    ![Single Sign-on 구성](./media/active-directory-saas-hr2day-tutorial/tutorial_attribute_05.png)

    b. Hello에 **이름** 상자에서 입력 **ATTR_LOGINCLAIM**합니다.

    c. Hello에서 **값** 목록에서 **join ()**합니다.

    d. Hello에서 **String1** 목록에서 **user.mail**합니다.

    e. 에 대 한 **String2**, hello HR2day 팀에서 제공 되는 고유 식별자를 입력 합니다.

    f. Hello에 **구분 기호** 상자에서 입력  **@** 합니다.
    
    g. **확인**을 선택합니다.

7. 선택 hello **저장** 단추입니다.

    ![Single Sign-On 구성](./media/active-directory-saas-hr2day-tutorial/tutorial_general_400.png)

8. Hello에 **Merces 구성에 의해 HR2day** 섹션에서 **Merces 여 HR2day 구성** tooopen hello **sign on 구성** 창. 복사 hello **Sign-Out URL**, **SAML 엔터티 ID**, 및 **SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조** 섹션.

    ![Single Sign-On 구성](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_configure.png) 

9. 응용 프로그램, 연락처 hello에 대 한 SSO tooconfigure [Merces 클라이언트 지원 팀에서 HR2day](mailTo:servicedesk@merces.nl)합니다. 다운로드 한 hello 연결 **Certificate(Base64)** tooyour 전자 메일 파일입니다. 또한 hello 제공 **Sign-Out URL**, **SAML 엔터티 ID**, 및 **SAML Single Sign-on 서비스 URL** SSO 통합에 대해 구성할 수 있습니다.

    > [!NOTE]
    >이 통합 hello 패턴을 사용 하 여 설정 하는 엔터티 ID toobe hello 필요한 toohello Merces 팀 언급 **https://hr2day.force.com/INSTANCENAME**합니다.

    > [!TIP]
    >이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!  Hello에서이 앱을 추가한 다음 **Active Directory** > **엔터프라이즈 응용 프로그램** 섹션을 선택 하는 hello **Single Sign On** 탭 합니다. 액세스 hello hello 통해 문서를 포함 하는 후 **구성** hello 아래쪽 섹션. 자세한 내용은 hello 포함 된 설명서 기능 hello에 대 한 [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)합니다.
> 

### <a name="create-an-azure-ad-test-user"></a>Azure AD 테스트 사용자 만들기
이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.

![Azure AD 사용자 만들기][100]

**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**

1. Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, hello 선택 **Azure Active Directory** 아이콘입니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-hr2day-tutorial/create_aaduser_01.png) 

2. 사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹**를 선택한 후 **모든 사용자**합니다.
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-hr2day-tutorial/create_aaduser_02.png) 

3. tooopen hello **사용자** 대화 상자에서 **추가** hello hello 대화 상자 위쪽에 있습니다.
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-hr2day-tutorial/create_aaduser_03.png) 

4. Hello에 **사용자** 대화 상자에서 다음 단계는 take hello:
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-hr2day-tutorial/create_aaduser_04.png) 

    a. Hello에 **이름** 상자에서 입력 **BrittaSimon**합니다.

    b. Hello에 **사용자 이름** 상자, 형식 hello **전자 메일 주소** BrittaSimon입니다.

    c. 선택 **암호 표시**, hello 암호 다음 기록 합니다.

    d. **만들기**를 선택합니다.
 
### <a name="create-an-hr2day-by-merces-test-user"></a>HR2day by Merces 테스트 사용자 만들기

hello이이 섹션의 목적은 toocreate HR2day에 Merces Britta Simon 호출한 사용자입니다. hello HR2day 계정에서 tooadd hello 사용자가 hello에서 작업할 [Merces 클라이언트 지원 팀에서 HR2day](mailto:servicedesk@merces.nl)합니다. 

> [!NOTE]
> Toocreate 사용자를 수동으로 필요한 경우 문의 hello [Merces 클라이언트 지원 팀에서 HR2day](mailto:servicedesk@merces.nl)합니다.

### <a name="assign-hello-azure-ad-test-user"></a>Azure AD hello 테스트 사용자를 할당 합니다.

이 섹션에서는 Merces 여 그녀의 액세스 tooHR2day 권한을 부여 하 여 Azure single sign on Britta Simon toouse를 사용 합니다.

![사용자 할당][200] 

**tooassign Britta Simon tooHR2day Merces, 하 여 hello 다음 단계를 수행 합니다.**

1. hello Azure 포털을 열고 hello 응용 프로그램 보기, toohello 디렉터리 보기 이동한 다음 이동 하 여 너무**엔터프라이즈 응용 프로그램**합니다. 다음으로 **모든 응용 프로그램**을 선택합니다.

    ![사용자 할당][201] 

2. Hello 응용 프로그램 목록에서 선택 **Merces 여 HR2day**합니다.

    ![Single Sign-On 구성](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_app.png) 

3. Hello hello 왼쪽 메뉴에서 선택 **사용자 및 그룹**합니다.

    ![사용자 할당][202] 

4. 선택 hello **추가** 단추입니다. 그런 다음, hello **할당 추가** 대화 상자에서 **사용자 및 그룹**합니다.

    ![사용자 할당][203]

5. Hello에 **사용자 및 그룹** 대화 상자의 hello **사용자** 목록에서 **Britta Simon**합니다.

6. Hello 클릭 **선택** 단추입니다.

7. Hello에 **할당 추가** 대화 상자에서 **할당**합니다.
    
### <a name="test-single-sign-on"></a>Single Sign-On 테스트

hello이 섹션은 tootest Azure AD single sign on 구성을 사용 하 여 hello 액세스 패널입니다.  

Hello 액세스 패널에서에서 타일 Merces 여 HR2day hello를 선택 하면 자동으로 가져오기 로그인 tooyour HR2day Merces 응용 프로그램에 의해.

## <a name="additional-resources"></a>추가 리소스

* [방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와](active-directory-saas-tutorial-list.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_203.png

