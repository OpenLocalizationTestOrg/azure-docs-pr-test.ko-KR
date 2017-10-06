---
title: "자습서: Azure에서 Google Apps와 Azure Active Directory 통합 | Microsoft 문서"
description: "단일 로그온 tooconfigure 방법을 알아보려면 Azure Active Directory와 Google Apps 사이의 합니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 38a6ca75-7fd0-4cdc-9b9f-fae080c5a016
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 2093b5ab605ec0d7bbefe7a78e1eede34d756f53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-google-apps"></a>자습서: Google Apps와 Azure Active Directory 통합

이 자습서에 설명 어떻게 toointegrate Google Apps와 Azure Active Directory (Azure AD).

Azure AD와 Google Apps 통합 hello 다음 이점을 제공 합니다.

- 앱 액세스 tooGoogle을 지닌 Azure AD에서 제어할 수 있습니다.
- 프로그램 사용자 tooautomatically get 로그온 tooGoogle (Single Sign-on)는 앱의 Azure AD 계정으로 사용 하도록 설정할 수 있습니다.
- 하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.

Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.

## <a name="prerequisites"></a>필수 조건

Azure AD 및 Google Apps 통합 tooconfigure 다음 항목 hello가 필요 합니다.

- Azure AD 구독
- Google Apps Single Sign-On이 설정된 구독

> [!NOTE]
> 이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.

이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.

- 꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.
- Azure AD 평가판 환경이 없으면 [평가판 제품](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.

## <a name="video-tutorial"></a>비디오 자습서
어떻게 tooEnable Single Sign On tooGoogle 2 분 후에는 앱:

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Enable-single-sign-on-to-Google-Apps-in-2-minutes-with-Azure-AD/player]

## <a name="frequently-asked-questions"></a>질문과 대답
1. **Q: Chromebooks 및 기타 크롬 장치는 Azure AD Single Sign-On과 호환되나요?**
   
    A: 예, 사용자가 자신의 Azure AD 자격 증명을 사용 하 여 자신의 Chromebook 장치에 수 toosign. 사용자가 자격 증명을 두 번 입력해야 하는 이유는 이 [Google Apps 지원 문서](https://support.google.com/chrome/a/answer/6060880) 를 참조하세요.

2. **Q: 경우 single sign-on 사용 하려면 사용자는 Google 강의실, GMail, Google 드라이브, YouTube, 등의 모든 Google 제품으로 자신의 Azure AD 자격 증명 toosign 수 toouse 수 있습니까?**
   
    A: 예,에 따라 [는 Google apps](https://support.google.com/a/answer/182442?hl=en&ref_topic=1227583) tooenable를 선택 하거나 조직에 대해 사용 하지 않도록 설정 합니다.

3. **Q: 내 Google 앱 사용자의 하위 집합에만 Single Sign-On을 사용할 수 있나요?**
   
    A: 아니요, 즉시 single sign on를 설정 하면 Google Apps 사용자가 Azure AD 자격 증명으로 모든 tooauthenticate가 필요 합니다. Google Apps 환경에 대 한 hello id 공급자로 Azure AD Google Apps을 지원 하지 않으므로 여러 id 공급자에 있는 일 수 있습니다 또는 Google-하나만 hello에서 같은 시간입니다.

4. **Q: 경우 사용자가 Windows를 통해 로그인 tooGoogle 앱 암호를 입력 시작 하지 않고 자동으로 인증 것인가요?**
   
    A: 이 시나리오에는 두 가지 옵션을 사용할 수 있습니다. 첫째, [Azure Active Directory 조인](active-directory-azureadjoin-overview.md)을 통해 Windows 10 장치에 로그인할 수 있습니다. 사용자는 도메인에 가입 된 tooan 온-프레미스 Active Directory가 single sign on tooAzure AD 통해에 대해 설정 된 Windows 장치에 로그인 수 또는 [Active Directory Federation Services (AD FS)](active-directory-aadconnect-user-signin.md) 배포 합니다. 두 옵션 모두 필요 hello 자습서 tooenable single sign on Azure AD 간의 뒤의 tooperform hello 단계 및 Google Apps 합니다.

## <a name="scenario-description"></a>시나리오 설명
이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다. 이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.

1. Google Apps hello 갤러리 추가
2. Azure AD Single Sign-on 구성 및 테스트

## <a name="adding-google-apps-from-hello-gallery"></a>Google Apps hello 갤러리 추가
tooconfigure hello와의 통합 Google Apps Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Google Apps tooadd가 필요합니다.

**hello 갤러리에서 Google Apps tooadd hello 다음 단계를 수행 합니다.**

1. Hello에 ** [Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다. 

    ![Active Directory][1]

2. 너무 이동**엔터프라이즈 응용 프로그램**합니다. 이동 하 여 너무**모든 응용 프로그램**합니다.

    ![응용 프로그램][2]
    
3. tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.

    ![응용 프로그램][3]

4. Hello 검색 상자에 입력 **Google Apps**합니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_search.png)

5. Hello 결과 패널에서 선택 **Google Apps**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Azure AD Single Sign-on 구성 및 테스트
이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Google Apps에서 Azure AD Single Sign-On을 구성하고 테스트합니다.

Single sign on toowork에 대 한 Azure AD는 tooknow에 Google Apps에서 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다. 즉, Azure AD 사용자 및 Google Apps에 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.

Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** Google Apps에서 합니다.

tooconfigure 및 Google Apps를 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.

1. **[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on) ** -tooenable 사용자 toouse이이 기능입니다.
2. **[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user) ** -tootest Azure AD single sign on Britta Simon 사용 합니다.
3. **[Google Apps 테스트 사용자 만들기](#creating-a-google-apps-test-user) ** -toohave Britta Simon 표현인 연결 된 toohello Azure AD 사용자의 Google Apps에서 해당 하는 도구입니다.
4. **[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.
5. **[Single Sign-on 테스트](#testing-single-sign-on) ** -tooverify 구성 works를 hello 여부.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성

이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 Google Apps 응용 프로그램에서 single sign on 구성 합니다.

**Azure AD tooconfigure single sign on를 Google Apps와 hello 다음 단계를 수행 합니다.**

1. Hello hello에 Azure 포털에서에서 **Google Apps** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.

    ![Single Sign-on 구성][4]

2. Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.
 
    ![Single Sign-on 구성](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_samlbase.png)

3. Hello에 **Google Apps 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_url.png)

    Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://mail.google.com/a/<yourdomain>`

    > [!NOTE] 
    > 이 값은 실제 값이 아닙니다. Hello 실제 로그온 URL으로 hello 값을 업데이트 합니다. hello 문의 [Google 지원 팀](https://www.google.com/contact/)합니다.
 
4. Hello에 **SAML 서명 인증서** 섹션에서 클릭 **인증서** hello 인증서 컴퓨터에 저장 합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_certificate.png) 

5. **저장** 단추를 클릭합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-google-apps-tutorial/tutorial_general_400.png)

6. Hello에 **Google 앱 구성** 섹션에서 클릭 **Google Apps 구성** tooopen **sign on 구성** 창. 복사 hello **Sign-Out URL, SAML Single Sign-on 서비스 URL 및 변경 암호 URL** hello에서 **빠른 참조 섹션.**

    ![Single Sign-on 구성](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_configure.png) 

7. 브라우저에서 새 탭을 열고 hello에 로그인 [Google 앱 관리 콘솔](http://admin.google.com/) 관리자 계정을 사용 합니다.

8. **보안**을 클릭합니다. Hello 링크 보이지 않으면 hello 아래 숨겨질 수 있습니다 **기타 컨트롤** hello hello 화면 맨 아래에 메뉴입니다.
   
    ![보안을 클릭합니다.][10]

9. Hello에 **보안** 페이지 **single sign on (SSO)를 설정 합니다.**
   
    ![SSO를 클릭합니다.][11]

10. Hello 구성 변경 내용을 다음을 수행 합니다.
   
    ![SSL 구성][12]
   
    a. **Setup SSO with third party identity provider**(타사 ID 공급자로 SSO 설정)을 선택합니다.

    b. 에 **로그인 페이지 URL** Google Apps에 필드를 hello 값을 붙여 넣습니다 **Single Sign-on 서비스 URL**, Azure 포털에서 복사한입니다.

    c. Hello에 **로그 아웃 페이지 URL** Google Apps에 필드를 hello 값을 붙여 넣습니다 **Sign-Out URL**, Azure 포털에서 복사한입니다. 

    d. Hello에 **암호 URL 변경** 필드를 Google Apps의 hello 값을 붙여 **암호 URL 변경**, Azure 포털에서 복사한입니다. 

    e. Hello에 대 한 Google Apps에서 **확인 인증서**, Azure 포털에서 다운로드 한 hello 인증서를 업로드 합니다.

    f. **변경 내용 저장**을 클릭합니다.

> [!TIP]
> 이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!  Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서 ** 구성** hello 아래쪽 섹션. 자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)
 
### <a name="creating-an-azure-ad-test-user"></a>Azure AD 테스트 사용자 만들기
이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.

![Azure AD 사용자 만들기][100]

**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**

1. Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-google-apps-tutorial/create_aaduser_01.png) 

2. 사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-google-apps-tutorial/create_aaduser_02.png) 

3. tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-google-apps-tutorial/create_aaduser_03.png) 

4. Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-google-apps-tutorial/create_aaduser_04.png) 

    a. Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.

    b. Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.

    c. 선택 **암호 표시** hello hello 값 기록 **암호**합니다.

    d. **만들기**를 클릭합니다.
 
### <a name="creating-a-google-apps-test-user"></a>Google Apps 테스트 사용자 만들기

hello이이 섹션의 목적은 toocreate Britta Simon Google 앱 소프트웨어에서 호출 하는 사용자입니다. Google Apps는 자동 프로비전을 지원하며 기본적으로 사용하도록 설정됩니다. 이 섹션에는 사용자의 작업이 없습니다. 사용자는 Google 앱 소프트웨어에 존재 하지 않는, 경우에 새 tooaccess Google 앱 소프트웨어를 시도할 때 만들어집니다.

>[!NOTE] 
>Toocreate 사용자를 수동으로 필요한 경우 문의 hello [Google 지원 팀](https://www.google.com/contact/)합니다.

### <a name="assigning-hello-azure-ad-test-user"></a>Azure AD hello 테스트 사용자를 할당합니다.

이 섹션에서는 Azure에서 single sign-on Britta Simon toouse 사용 하도록 설정 tooGoogle 앱 액세스를 부여 합니다.

![사용자 할당][200] 

**tooassign Britta Simon tooGoogle 앱 hello 다음 단계를 수행 합니다.**

1. Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.

    ![사용자 할당][201] 

2. Hello 응용 프로그램 목록에서 선택 **Google Apps**합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_app.png) 

3. Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.

    ![사용자 할당][202] 

4. **추가** 단추를 클릭합니다. 그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.

    ![사용자 할당][203]

5. **사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.

6. **사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.

7. **할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.
    
### <a name="testing-single-sign-on"></a>Single Sign-On 테스트

이 단원의 single sign on 설정을 열고 액세스 패널에 hello tootest [https://myapps.microsoft.com](active-directory-saas-access-panel-introduction.md)hello 테스트 계정에 로그인 한 다음을 클릭 **Google Apps** hello 액세스 패널에서에서 타일입니다.

## <a name="additional-resources"></a>추가 리소스

* [방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와](active-directory-saas-tutorial-list.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)
* [사용자 프로비저닝 구성](active-directory-saas-google-apps-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_203.png

[0]: ./media/active-directory-saas-google-apps-tutorial/azure-active-directory.png

[5]: ./media/active-directory-saas-google-apps-tutorial/gapps-added.png
[6]: ./media/active-directory-saas-google-apps-tutorial/config-sso.png
[7]: ./media/active-directory-saas-google-apps-tutorial/sso-gapps.png
[8]: ./media/active-directory-saas-google-apps-tutorial/sso-url.png
[9]: ./media/active-directory-saas-google-apps-tutorial/download-cert.png
[10]: ./media/active-directory-saas-google-apps-tutorial/gapps-security.png
[11]: ./media/active-directory-saas-google-apps-tutorial/security-gapps.png
[12]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-config.png
[13]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-confirm.png
[14]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-email.png
[15]: ./media/active-directory-saas-google-apps-tutorial/gapps-api.png
[16]: ./media/active-directory-saas-google-apps-tutorial/gapps-api-enabled.png
[17]: ./media/active-directory-saas-google-apps-tutorial/add-custom-domain.png
[18]: ./media/active-directory-saas-google-apps-tutorial/specify-domain.png
[19]: ./media/active-directory-saas-google-apps-tutorial/verify-domain.png
[20]: ./media/active-directory-saas-google-apps-tutorial/gapps-domains.png
[21]: ./media/active-directory-saas-google-apps-tutorial/gapps-add-domain.png
[22]: ./media/active-directory-saas-google-apps-tutorial/gapps-add-another.png
[23]: ./media/active-directory-saas-google-apps-tutorial/apps-gapps.png
[24]: ./media/active-directory-saas-google-apps-tutorial/gapps-provisioning.png
[25]: ./media/active-directory-saas-google-apps-tutorial/gapps-provisioning-auth.png
[26]: ./media/active-directory-saas-google-apps-tutorial/gapps-admin.png
[27]: ./media/active-directory-saas-google-apps-tutorial/gapps-admin-privileges.png
[28]: ./media/active-directory-saas-google-apps-tutorial/gapps-auth.png
[29]: ./media/active-directory-saas-google-apps-tutorial/assign-users.png
[30]: ./media/active-directory-saas-google-apps-tutorial/assign-confirm.png