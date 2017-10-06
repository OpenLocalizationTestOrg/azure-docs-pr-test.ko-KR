---
title: "자습서: SuccessFactors와 Azure Active Directory 통합 | Microsoft 문서"
description: "어떻게 tooenable Azure Active Directory와 SuccessFactors toouse single sign on, 자동화 된 프로비저닝 및 더에 대해 알아봅니다."
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 32bd8898-c2d2-4aa7-8c46-f1f5c2aa05f1
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 3f7895d7d5e26fda27f555ae2f14a1645b50dcba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-successfactors"></a>자습서: SuccessFactors와 Azure Active Directory 통합
이 자습서의 hello 목적은 tooshow 있습니다 어떻게 toointegrate Azure Active Directory (Azure AD)와 SuccessFactors 합니다.

Azure AD와 SuccessFactors 통합 이점을 다음 hello로 제공 합니다.

* 액세스 tooSuccessFactors을 지닌 Azure AD에서 제어할 수 있습니다.
* 프로그램 사용자 tooautomatically get 로그온 tooSuccessFactors (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.
* 하나의 중앙 위치-hello Azure 클래식 포털에서에서 사용자 계정을 관리할 수 있습니다.

Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.

## <a name="prerequisites"></a>필수 조건
SuccessFactors와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.

* 유효한 Azure 구독
* SuccessFactors의 테넌트

> [!NOTE]
> 이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.
> 
> 

이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.

* 꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.
* Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.

## <a name="scenario-description"></a>시나리오 설명
이 자습서의 hello 목적은 tooenable 있습니다 tootest Azure AD에서 single sign-on 테스트 환경에서 합니다.

이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.

1. SuccessFactors는 hello 갤러리 추가
2. Azure AD Single Sign-on 구성 및 테스트

## <a name="adding-successfactors-from-hello-gallery"></a>SuccessFactors는 hello 갤러리 추가
tooconfigure hello와의 통합 SuccessFactors Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 SuccessFactors tooadd가 필요합니다.

**SuccessFactors hello 갤러리에서 tooadd hello 다음 단계를 수행 합니다.**

1. Hello 왼쪽된 탐색 패널의 hello Azure 클래식 포털에서에서 클릭 **Active Directory**합니다.
   
    ![Single Sign-On 구성][1]
2. Hello에서 **디렉터리** 목록, 선택 hello 디렉터리 tooenable 디렉터리 통합을 구하려는 합니다.
3. tooopen hello 응용 프로그램 보기 hello 디렉터리 보기에서 클릭 **응용 프로그램** hello 상단 메뉴에서 합니다.
   
    ![Single Sign-On 구성][2]
4. 클릭 **추가** hello hello 페이지 맨 아래에 있습니다.
   
    ![응용 프로그램][3]
5. Hello에 **하 신 toodo 원하는** 대화 상자에서 클릭 **hello 갤러리에서 응용 프로그램 추가**합니다.
   
    ![Single Sign-On 구성][4]
6. Hello에 **검색 상자**, 형식 **SuccessFactors**합니다.
   
    ![Single Sign-On 구성][5]
7. Hello 결과 패널에서 선택 **SuccessFactors**, 클릭 하 고 **완료** tooadd hello 응용 프로그램입니다.
   
    ![Single Sign-On 구성][6]

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Azure AD Single Sign-on 구성 및 테스트
이 섹션의 hello 목적은 tooshow "Britta Simon" 이라는 테스트 사용자에 따라 tooconfigure와 SuccessFactors 사용 하 여 Azure AD에서 single sign-on 테스트 합니다.

Single sign on toowork에 대 한 Azure AD는 tooknow SuccessFactors tooan 사용자 Azure ad에서에서 어떤 hello 테이블에 해당 사용자가 필요 합니다. 즉, Azure AD 사용자와 SuccessFactors에 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.

Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** SuccessFactors에 합니다.

tooconfigure와 SuccessFactors 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.

1. **[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.
2. **[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.
3. **[SuccessFactors 테스트 사용자 만들기](#creating-a-successfactors-test-user)**  -toohave Britta Simon 그녀의 연결 된 Azure AD toohello 표현인 SuccessFactors에 해당 하는 도구입니다.
4. **[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.
5. **[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성
이 섹션에서는 Azure AD에서 single sign-on hello 클래식 포털의 설정 및 SuccessFactors 응용 프로그램에서 single sign on 구성 합니다.

**Azure AD tooconfigure single sign on와 SuccessFactors를 hello 다음 단계를 수행 합니다.**

1. Hello hello에 Azure 클래식 포털에서에서 **SuccessFactors** 응용 프로그램 통합 페이지에서 클릭 **single sign on 구성** tooopen hello **Single Sign-on 구성** 대화 상자입니다.
   
    ![Single Sign-On 구성][7]
2. Hello에 **어떻게 tooSuccessFactors에 사용자가 toosign 보 시겠습니까** 페이지에서 **Microsoft Azure AD Single Sign-on**, 클릭 하 고 **다음**합니다.
   
    ![Single Sign-On 구성][8]
3. Hello에 **앱 URL 구성** 페이지 hello 다음 단계를 수행 하 고 클릭 **다음**합니다.
   
    ![Single Sign-On 구성][9]
   
    a. Hello에 **로그온 URL** 텍스트 상자에 hello 패턴을 다음 중 하나를 사용 하 여 URL: 
   
    |  |
    | --- |
    | `https://<company name>.successfactors.com/<company name>` |
    | `https://<company name>.sapsf.com/<company name>` |
    | `https://<company name>.successfactors.eu/<company name>` |
    | `https://<company name>.sapsf.eu` |
   
    b. Hello에 **회신 URL** 텍스트 상자에 hello 패턴을 다음 중 하나를 사용 하 여 URL: 
   
    |  |
    | --- |
    | `https://<company name>.successfactors.com/<company name>` |
    | `https://<company name>.sapsf.com/<company name>` |
    | `https://<company name>.successfactors.eu/<company name>` |
    | `https://<company name>.sapsf.eu` |
    | `https://<company name>.sapsf.eu/<company name>` |
   
    c. **다음**을 누릅니다. 

    > [!NOTE]
    > 이러한 없는지 hello 실제 값 note 하십시오. Tooupdate hello 실제 로그온 URL 및 회신 URL 사용 하 여 이러한 값 해야합니다. 이러한 값에 게 문의 tooget [SuccessFactors 지원 팀](https://www.successfactors.com/en_us/support.html)합니다.

1. Hello에 **SuccessFactors에서 single sign on 구성** 페이지 **다운로드 인증서**, hello 인증서 파일을 컴퓨터에 로컬로 저장 합니다.
   
    ![Single Sign-On 구성][10]

2. 다른 웹 브라우저 창에서 **SuccessFactors 관리 포털** 에 관리자로 로그인합니다.

3. 방문 **응용 프로그램 보안** 및 네이티브 너무**단일 기능**합니다. 

4. Hello에 모든 값을 배치 **토큰 재설정** 클릭 **토큰 저장** tooenable SAML SSO 합니다.
   
    ![앱 쪽에서 Single Sign-On 구성][11]

    > [!NOTE] 
    > 이 값은 바로 켜기/끄기 스위치 hello로 사용 됩니다. 모든 값을 저장 하는 경우 SAML SSO hello은 ON입니다. 빈 값이 저장 하는 경우 SAML SSO hello은 OFF입니다.

1. 네이티브 toobelow 스크린 샷 hello 다음 작업을 수행 합니다.
   
    ![앱 쪽에서 Single Sign-On 구성][12]
   
    a. 선택 hello **SAML v2 SSO** 라디오 단추
   
    b. SAML 어설션 파티 Name(e.g. SAml issuer + company name) hello를 설정 합니다.
   
    c. Hello에 **SAML 발급자** textbox 배치의 hello 값 **발급자 URL** Azure AD 응용 프로그램 구성 마법사에서 합니다.
   
    d. **필수 서명 요구**로 **응답(고객 생성/IdP/AP)**을 선택합니다.
   
    e. **SAML 플래그 사용**으로 **사용**을 선택합니다.
   
    f. **로그인 요청 서명(SF 생성/SP/RP)**으로 **아니요**를 선택합니다.
   
    g. **SAML 프로필**로 **브라우저/게시 프로필**을 선택합니다.
   
    h. **인증서 유효 기간 적용**으로 **아니요**를 선택합니다.
   
    i. Hello 다운로드 한 인증서 파일의 hello 콘텐츠를 복사 하 고 hello에 붙여 넣습니다 **SAML 확인 인증서** 텍스트 상자에 붙여넣습니다.

    > [!NOTE] 
    > hello 인증서 내용 인증서 및 끝 인증서 태그 시작가 해야 합니다.

1. TooSAML V2, 이동한 다음 단계를 수행 하는 hello를 수행 합니다.
   
    ![앱 쪽에서 Single Sign-On 구성][13]
   
    a. **SP 시작 전역 로그아웃 지원**으로 **예**를 선택합니다.
   
    b. Hello에 **전역 로그 아웃 서비스 URL (LogoutRequest 대상)** textbox 배치의 hello 값 **원격 로그 아웃 URL** Azure AD 응용 프로그램 구성 마법사에서 합니다.
   
    c. **요청 SP는 모든 NameID 요소를 암호화해야 합니다.**로 **아니요**를 선택합니다.
   
    d. **NameID 형식**으로 **지정되지 않음**을 선택합니다.
   
    e. **SP 시작 로그인 사용(AuthnRequest)**으로 **예**를 선택합니다.
   
    f. Hello에 **회사 전체 발급자로 보내기 요청** textbox 배치의 hello 값 **원격 로그인 URL** Azure AD 응용 프로그램 구성 마법사에서 합니다.
2. Toomake hello 로그인 사용자 이름을 원하는 경우 이러한 단계를 수행 합니다. 대/소문자를 구분 합니다.
   
    a. 방문 **회사 설정**(near hello 아래).
   
    b. **사용자 이름 대/소문자 구분하지 않음 사용**근처의 확인란을 선택합니다.
   
    c. **저장**을 클릭합니다.
   
    ![Single Sign-on 구성][29]

    > [!NOTE] 
    > 이 작업을 수행할 tooenable, hello 시스템 중복 되는 SAML 로그인 이름이 만들어집니다를 확인 합니다. 예를 들어 hello 고객에 게 사용자 1 및 user1 계정 사용자 이름입니다. 대/소문자를 구분하지 않으면 이러한 중복 항목을 만듭니다. hello 시스템 오류 메시지가 제공 됩니다 하 고 hello 기능을 사용 하지 않습니다. hello 고객 할 toochange hello 사용자 이름 중 하나 실제로 च 하므로 서로 다른 수 있습니다. 

1. Azure 클래식 포털 hello에 hello single sign on 구성 확인을 선택한 다음 클릭 **완료** tooclose hello **Single Sign-on 구성** 대화 상자.
   
    ![응용 프로그램][14]
2. Hello에 **Single sign on 확인** 페이지 **완료**합니다.
   
    ![응용 프로그램][15]

### <a name="creating-an-azure-ad-test-user"></a>Azure AD 테스트 사용자 만들기
이 섹션의 hello 목표 Britta Simon 라는 hello 클래식 포털에서 toocreate 테스트 사용자를입니다.

![Azure AD 사용자 만들기][16]

**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**

1. Hello에 **Azure 클래식 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Active Directory**합니다.
   
    ![Azure AD 테스트 사용자 만들기][17]
2. Hello에서 **디렉터리** 목록, 선택 hello 디렉터리 tooenable 디렉터리 통합을 구하려는 합니다.
3. toodisplay hello 목록이 hello 바탕 화면에서 hello 메뉴에서 사용자가 클릭 **사용자**합니다.
   
    ![Azure AD 테스트 사용자 만들기][18]
4. tooopen hello **사용자 추가** hello 아래쪽에 hello 도구 모음에서 대화 상자에서 클릭 **사용자 추가**합니다.
   
    ![Azure AD 테스트 사용자 만들기][19]
5. Hello에 **이 사용자에 대해 알리기** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.
   
    ![Azure AD 테스트 사용자 만들기][20]
   
    a. 사용자 유형에서 조직의 새 사용자를 선택합니다.
   
    b. Hello 사용자 이름에서에서 **textbox**, 형식 **BrittaSimon**합니다.
   
    c. **다음**을 누릅니다.
6. Hello에 **사용자 프로필** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.
   
    ![Azure AD 테스트 사용자 만들기][21]
   
    a. Hello에 **이름** 텍스트 상자에 **Britta**합니다.  
   
    b. Hello에 **성** 텍스트 상자에, **Simon**합니다.
   
    c. Hello에 **표시 이름** 텍스트 상자에 **Britta Simon**합니다.
   
    d. Hello에 **역할** 목록에서 **사용자**합니다.
   
    e. **다음**을 누릅니다.
7. Hello에 **임시 암호 가져오기** 대화 상자 페이지에서 클릭 **만들**합니다.
   
    ![Azure AD 테스트 사용자 만들기][22]
8. Hello에 **임시 암호 가져오기** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.
   
    ![Azure AD 테스트 사용자 만들기][23]
   
    a. Hello hello 값 적어 **새 암호**합니다.
   
    b. **완료**를 클릭합니다.  

### <a name="creating-a-successfactors-test-user"></a>SuccessFactors 테스트 사용자 만들기
Tooenable Azure AD 사용자가 toolog SuccessFactors에 주문 하 고에 SuccessFactors에 이들 프로 비전 해야 합니다.  
Hello SuccessFactors의 경우에서 프로 비전은 수동 작업입니다.

SuccessFactors에서 만든 tooget 사용자가 해야 toocontact hello [SuccessFactors 지원 팀](https://www.successfactors.com/en_us/support.html)합니다.

### <a name="assigning-hello-azure-ad-test-user"></a>Azure AD hello 테스트 사용자를 할당합니다.
이 섹션의 hello 목표에는 자신의 액세스 tooSuccessFactors 권한을 부여 하 여 tooenabling Britta Simon toouse Azure single sign on입니다.

![사용자 할당][24]

**tooassign Britta Simon tooSuccessFactors hello 다음 단계를 수행 합니다.**

1. Hello 클래식 포털에서 tooopen hello 응용 프로그램 보기 hello 디렉터리 보기를 클릭 **응용 프로그램** hello 최상위 메뉴에 있습니다.
   
    ![사용자 할당][25]
2. Hello 응용 프로그램 목록에서 선택 **SuccessFactors**합니다.
   
    ![Single Sign-on 구성][26]
3. Hello 메뉴에서 hello 위에 표시를 클릭 **사용자**합니다.
   
    ![사용자 할당][27]
4. Hello [사용자] 목록에서 선택 **Britta Simon**합니다.
5. Hello 아래쪽에 hello 도구 모음에서 클릭 **할당**합니다.
   
    ![사용자 할당][28]

### <a name="testing-single-sign-on"></a>Single Sign-On 테스트
이 섹션의 hello 목적은 tootest 액세스 패널을 hello 사용 하 여 Azure AD single sign-on 구성 합니다.

Hello SuccessFactors hello 액세스 패널에서에서 타일을 클릭할 때 자동으로 로그온 tooyour SuccessFactors 응용 프로그램을 구해야 합니다.

## <a name="additional-resources"></a>추가 리소스
* [방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와](active-directory-saas-tutorial-list.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[0]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_00.png
[1]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_01.png
[6]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_02.png
[7]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_03.png
[8]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_04.png
[9]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_05.png
[10]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_06.png

[11]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_07.png
[12]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_08.png
[13]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_09.png
[14]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_05.png
[15]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_06.png

[16]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_00.png
[17]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_01.png
[18]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_02.png
[19]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_03.png
[20]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_04.png
[21]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_05.png
[22]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_06.png
[23]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_07.png

[24]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_07.png
[25]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_08.png
[26]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_11.png
[27]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_09.png
[28]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_10.png
[29]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_10.png
