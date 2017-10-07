---
title: "자습서: Slack과 Azure Active Directory 통합 | Microsoft 문서"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Slack 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ffc5e73f-6c38-4bbb-876a-a7dd269d4e1c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 7f0151401af4dc63d2f714d4b4f66380c4b51e0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-slack"></a>자습서: Slack과 Azure Active Directory 통합

이 자습서에 설명 Azure Active Directory (Azure AD)와 toointegrate 여유 하는 방법입니다.

Azure AD와 Slack 통합 이점을 다음 hello로 제공 합니다.

- 액세스 tooSlack을 지닌 Azure AD에서 제어할 수 있습니다.
- 프로그램 사용자 tooautomatically get 로그온 tooSlack (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.
- 하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.

Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.

## <a name="prerequisites"></a>필수 조건

Slack와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.

- Azure AD 구독
- Slack Single Sign-On이 설정된 구독

> [!NOTE]
> 이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.

이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.

- 꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.
- Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.

## <a name="scenario-description"></a>시나리오 설명
이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다. 이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.

1. Slack은 hello 갤러리 추가
2. Azure AD Single Sign-on 구성 및 테스트

## <a name="adding-slack-from-hello-gallery"></a>Slack은 hello 갤러리 추가
Azure AD로 여유 tooconfigure hello 통합을 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Slack tooadd가 필요합니다.

**hello 갤러리에서 Slack tooadd hello 다음 단계를 수행 합니다.**

1. Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다. 

    ![Active Directory][1]

2. 너무 이동**엔터프라이즈 응용 프로그램**합니다. 이동 하 여 너무**모든 응용 프로그램**합니다.

    ![응용 프로그램][2]
    
3. tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.

    ![응용 프로그램][3]

4. Hello 검색 상자에 입력 **Slack**합니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-slack-tutorial/tutorial_slack_search.png)

5. Hello 결과 패널에서 선택 **Slack**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-slack-tutorial/tutorial_slack_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Azure AD Single Sign-on 구성 및 테스트
이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Slack에서 Azure AD Single Sign-On을 구성하고 테스트합니다.

Single sign on toowork에 대 한 Azure AD는 tooknow Slack에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다. 즉, Azure AD 사용자와 Slack에 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.

여유 시간에 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.

tooconfigure 및 여유 시간을 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.

1. **[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.
2. **[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.
3. **[Slack 테스트 사용자 만들기](#creating-a-slack-test-user)**  -toohave Britta Simon 표현인 연결 된 toohello Azure AD 사용자의 여유 시간에 해당 하는 도구입니다.
4. **[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.
5. **[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성

이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 사용 하도록 설정 및 응용 프로그램 Slack에서 single sign on 구성 합니다.

**Azure AD tooconfigure single sign on 여유를 두고 hello 다음 단계를 수행 합니다.**

1. Hello hello에 Azure 포털에서에서 **Slack** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.

    ![Single Sign-on 구성][4]

2. Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.
 
    ![Single Sign-on 구성](./media/active-directory-saas-slack-tutorial/tutorial_slack_samlbase.png)

3. Hello에 **Slack 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-slack-tutorial/tutorial_slack_url.png)

    a. Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<companyname>.slack.com`

    b. Hello에 **식별자** textbox hello URL 입력:`https://slack.com`

    > [!NOTE] 
    > hello 값이 실제 아닙니다. 실제 로그온 URL hello와 tooupdate hello 값을 해야 합니다. 연락처 [Slack 지원 팀](https://slack.com/help/contact) tooget hello 값
     
4. Slack 응용 프로그램에는 특정 형식의 hello SAML 어설션 합니다. 이 응용 프로그램에 대 한 클레임을 따라 hello를 구성 합니다. Hello에서 이러한 특성의 hello 값을 관리할 수 있습니다 "**사용자 특성**" 응용 프로그램 통합 페이지에서 섹션. 다음 스크린 샷 hello이에 대 한 예가 나와 있습니다.
    
    ![Single Sign-on 구성](./media/active-directory-saas-slack-tutorial/tutorial_slack_attribute.png)

5. Hello에 **사용자 특성** hello 섹션 **Single sign on** 대화 상자에서 **user.mail** 으로 **사용자 식별자** 표시 된 각 행에 대해 hello 테이블 아래에 hello 다음 단계를 수행 합니다.
    
    | 특성 이름 | 특성 값 |
    | --- | --- |
    | first_name | user.givenname |
    | last_name | user.surname |
    | User.Email | user.mail |  
    | User.Username | user.userprincipalname |

    a. 클릭 **특성** tooopen **특성 편집** 대화 상자 및 hello 다음 단계를 수행 합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-slack-tutorial/tutorial_slack_attribute1.png)

    a. Hello에 **이름** textbox, 해당 행에 대 한 표시 형식 hello 특성 이름입니다.
    
    b. Hello에서 **값** 목록, 해당 행에 대해 표시 된 선택 hello 특성 값입니다.
    
    c. **확인**

6. Hello에 **SAML 서명 인증서** 섹션에서 클릭 **인증서 (Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-slack-tutorial/tutorial_slack_certificate.png)

7. **저장** 단추를 클릭합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-slack-tutorial/tutorial_general_400.png)

8. Hello에 **Slack 구성** 섹션에서 클릭 **구성 Slack** tooopen **sign on 구성** 창. 복사 hello **SAML 엔터티 ID, 및 SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**

    ![Single Sign-on 구성](./media/active-directory-saas-slack-tutorial/tutorial_slack_configure.png) 

9.  다른 웹 브라우저 창에서 관리자 권한으로 tooyour Slack 회사 사이트에 로그인 합니다.

10.  너무 이동**Microsoft Azure AD** 이동 하 여 너무**팀 설정**합니다.

     ![앱 쪽에서 Single Sign-On 구성](./media/active-directory-saas-slack-tutorial/tutorial_slack_001.png)

11.  Hello에 **팀 설정** 섹션에서 hello **인증** 탭을 클릭 한 다음 **설정 변경**합니다.

     ![앱 쪽에서 Single Sign-On 구성](./media/active-directory-saas-slack-tutorial/tutorial_slack_002.png)

12. Hello에 **SAML 인증 설정** 대화 상자에서 hello 다음 단계를 수행 합니다.

    ![앱 쪽에서 Single Sign-On 구성](./media/active-directory-saas-slack-tutorial/tutorial_slack_003.png)

    a.  Hello에 **SAML 2.0 끝점 (HTTP)** 붙여넣기 hello 값의 텍스트 상자 **SAML Single Sign-on 서비스 URL**, Azure 포털에서 복사한입니다.

    b.  Hello에 **Id 공급자 발급자** 붙여넣기 hello 값의 텍스트 상자 **SAML 엔터티 ID**, Azure 포털에서 복사한입니다.

    c.  콘텐츠를 클립보드에 복사 hello 메모장에서 다운로드 한 인증서 파일을 열고 toohello 붙여 **공용 인증서** 텍스트 상자에 붙여넣습니다.

    d. 위의 세 가지 설정 hello Slack 팀에 대해 적절 하 게 구성 합니다. Hello 설정에 대 한 자세한 내용은 hello를 확인해 주세요 **Slack의 SSO 구성 가이드** 여기 합니다. `https://get.slack.help/hc/articles/220403548-Guide-to-single-sign-on-with-Slack%60`

    e.  **구성 저장**을 클릭하십시오.
     
    <!-- Deselect **Allow users toochange their email address**.

    e.  Select **Allow users toochoose their own username**.

    f.  As **Authentication for your team must be used by**, select **It’s optional**. -->

> [!TIP]
> 이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!  Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션. 자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Azure AD 테스트 사용자 만들기
이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.

![Azure AD 사용자 만들기][100]

**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**

1. Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-slack-tutorial/create_aaduser_01.png) 

2. 사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-slack-tutorial/create_aaduser_02.png) 

3. tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-slack-tutorial/create_aaduser_03.png) 

4. Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-slack-tutorial/create_aaduser_04.png) 

    a. Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.

    b. Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.

    c. 선택 **암호 표시** hello hello 값 기록 **암호**합니다.

    d. **만들기**를 클릭합니다.
 
### <a name="creating-a-slack-test-user"></a>Slack 테스트 사용자 만들기

이 섹션의 hello 목표 toocreate Slack에 Britta Simon 이라는 사용자를입니다. Slack은 just-in-time 프로비전을 지원하며 기본적으로 사용하도록 설정됩니다.

이 섹션에 작업 항목이 없습니다. 새 사용자는 아직 존재 하지 않는 경우 시도 tooaccess 여유 시간 동안 생성 됩니다.

> [!NOTE]
> TooContact toocreate 사용자를 수동으로 필요한 경우 필요한 [Slack 지원 팀](https://slack.com/help/contact)합니다.

### <a name="assigning-hello-azure-ad-test-user"></a>Azure AD hello 테스트 사용자를 할당합니다.

이 섹션에서는 tooSlack 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.

![사용자 할당][200] 

**tooassign Britta Simon tooSlack hello 다음 단계를 수행 합니다.**

1. Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.

    ![사용자 할당][201] 

2. Hello 응용 프로그램 목록에서 선택 **Slack**합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-slack-tutorial/tutorial_slack_app.png) 

3. Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.

    ![사용자 할당][202] 

4. **추가** 단추를 클릭합니다. 그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.

    ![사용자 할당][203]

5. **사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.

6. **사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.

7. **할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.
    
### <a name="testing-single-sign-on"></a>Single Sign-On 테스트

이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.

Hello Slack 타일을 클릭할 때 hello 액세스 패널에서 자동으로 로그온 tooyour Slack 응용 프로그램을 얻어야 합니다.

## <a name="additional-resources"></a>추가 리소스

* [방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와](active-directory-saas-tutorial-list.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-slack-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-slack-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-slack-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-slack-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-slack-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-slack-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-slack-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-slack-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-slack-tutorial/tutorial_general_203.png

