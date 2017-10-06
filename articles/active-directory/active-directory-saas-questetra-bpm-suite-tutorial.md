---
title: "자습서: Questetra BPM Suite와 Azure Active Directory 통합 | Microsoft 문서"
description: "Tooconfigure 단일 로그온 방법에 대해 알아봅니다 Azure Active Directory와 Questetra BPM 제품군 사이입니다."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: fb6d5b73-e491-4dd2-92d6-94e5aba21465
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/14/2017
ms.author: jeedes
ms.openlocfilehash: 4907e3b5751cd79f994fbd2ebcb7faec4eac34e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-questetra-bpm-suite"></a>자습서: Questetra BPM Suite와 Azure Active Directory 통합
이 자습서의 hello 목적은 tooshow 있습니다 어떻게 toointegrate Questetra BPM Suite Azure Active directory (Azure AD).  
다음 이점을 hello로 제공 Questetra BPM Suite Azure AD와 통합: 

* 액세스 tooQuestetra BPM 도구 모음을 지닌 Azure AD에서 제어할 수 있습니다. 
* Azure AD 계정을 사용 하면 사용자가 tooautomatically get 로그온 tooQuestetra BPM Suite (Single Sign-on)를 사용할 수 있습니다.
* 하나의 중앙 위치-hello Azure 클래식 포털에서에서 사용자 계정을 관리할 수 있습니다.

Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.

## <a name="prerequisites"></a>필수 조건
다음 항목 hello가 필요 tooconfigure Questetra BPM 도구 모음과 Azure AD 통합 합니다.

* Azure AD 구독
* [Questetra BPM Suite](https://senbon-imadegawa-988.questetra.net/) Single-Sign-On이 설정된 구독

> [!NOTE]
> 이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.
> 
> 

이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.

* 꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.
* Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다. 

## <a name="scenario-description"></a>시나리오 설명
이 자습서의 hello 목적은 tooenable 있습니다 tootest Azure AD에서 single sign-on 테스트 환경에서 합니다.  
이 자습서에 설명 된 hello 시나리오 세 가지 주요 구성 요소로 이루어져 있습니다.

1. Hello 갤러리에서 Questetra BPM 도구 모음 추가 
2. Azure AD Single Sign-on 구성 및 테스트

## <a name="adding-questetra-bpm-suite-from-hello-gallery"></a>Hello 갤러리에서 Questetra BPM 도구 모음 추가
tooconfigure hello와의 통합 Questetra BPM Suite Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Questetra BPM Suite tooadd가 필요합니다.

**hello 갤러리에서 Questetra BPM Suite tooadd hello 다음 단계를 수행 합니다.**

1. Hello에 **Azure 클래식 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Active Directory**합니다. 
   
    ![Active Directory][1]

2. Hello에서 **디렉터리** 목록, 선택 hello 디렉터리 tooenable 디렉터리 통합을 구하려는 합니다.

3. tooopen hello 응용 프로그램 보기 hello 디렉터리 보기에서 클릭 **응용 프로그램** hello 상단 메뉴에서 합니다.
   
    ![응용 프로그램][2]

4. 클릭 **추가** hello hello 페이지 맨 아래에 있습니다.
   
    ![응용 프로그램][3]

5. Hello에 **하 신 toodo 원하는** 대화 상자에서 클릭 **hello 갤러리에서 응용 프로그램 추가**합니다.
   
    ![응용 프로그램][4]

6. Hello 검색 상자에 입력 **Questetra BPM Suite**합니다.
   
    ![응용 프로그램][5]

7. Hello 결과 창에서 선택 **Questetra BPM Suite**, 클릭 하 고 **완료** tooadd hello 응용 프로그램입니다.

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Azure AD Single Sign-on 구성 및 테스트
이 섹션의 hello 목적은 tooshow "Britta Simon" 이라는 테스트 사용자에 따라 tooconfigure 및 Questetra BPM Suite를 사용 하 여 Azure AD에서 single sign-on 테스트 합니다.

Single sign on toowork에 대 한 Azure AD는 tooknow Questetra BPM Suite tooan 사용자 Azure ad에서에서 어떤 hello 테이블에 해당 사용자가 필요 합니다. 즉, Azure AD 사용자 및 hello Questetra BPM 도구 모음에서 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.  
Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** Questetra BPM 도구 모음에서 합니다.

tooconfigure 및 Questetra BPM Suite를 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.

1. **[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.
2. **[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.
3. **[Questetra BPM Suite 테스트 사용자 만들기](#creating-a-questetra-bpm-suite-test-user)**  -toohave Britta Simon 그녀의 연결 된 Azure AD toohello 표현인 Questetra BPM 제품군에 해당 하는 도구입니다.
4. **[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.
5. **[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성
hello이이 섹션에서는 tooenable Azure AD에서 single sign-on hello Azure 클래식 포털에서에서 및 tooconfigure single sign on Questetra BPM Suite 응용 프로그램에 있어야 합니다.

**Questetra BPM 도구 모음과 Azure AD에서 single sign-on tooconfigure hello 다음 단계를 수행 합니다.**

1. Hello hello에 Azure 클래식 포털에서에서 **Questetra BPM Suite** 응용 프로그램 통합 페이지에서 클릭 **single sign on 구성** tooopen hello **구성 Single Sign-on**  대화 상자입니다.
   
    ![Single Sign-on 구성][8]

2. Hello에 **어떻게 tooQuestetra BPM Suite에서 사용자가 toosign 보 시겠습니까** 페이지에서 **Azure AD Single Sign-on**, 클릭 하 고 **다음**합니다.
   
    ![Azure AD Single Sign-On][9]

3. 다른 웹 브라우저 창에서 **Questetra BPM Suite** 회사 사이트에 관리자로 로그인합니다.

4. Hello 메뉴에서 hello 위에 표시를 클릭 **시스템 설정**합니다. 
   
    ![Azure AD Single Sign-On][10]

5. tooopen hello **SingleSignOnSAML** 페이지 **SSO (SAML)**합니다. 
   
    ![Azure AD Single Sign-On][11]

6. Hello hello에 Azure 클래식 포털에서에서 **앱 설정 구성** 대화 상자 페이지를 hello 다음 단계를 수행 합니다. 
   
    ![앱 설정 구성][13]
   
    a. 에 **Questetra BPM Suite** hello SP 정보 섹션에서에서 회사 사이트에서 복사 hello **ACS URL**, 다음 hello에 붙여 넣는 **로그온 URL** 텍스트 상자에 붙여넣습니다.
   
    b. 에 **Questetra BPM Suite** hello SP 정보 섹션에서에서 회사 사이트에서 복사 hello **엔터티 ID**, 다음 hello에 붙여 넣는 **발급자 URL** 텍스트 상자에 붙여넣습니다.
   
    c. 에 **Questetra BPM Suite** hello SP 정보 섹션에서에서 회사 사이트에서 복사 hello **ACS URL**, 다음 hello에 붙여 넣는 **회신 URL** 텍스트 상자에 붙여넣습니다.
   
    d. **다음**을 누릅니다.

7. Hello에 **Questetra BPM Suite에서 single sign on 구성** 페이지 **다운로드 인증서**, hello 인증서 파일을 컴퓨터에 로컬로 저장 합니다.
   
    ![Single Sign-on 구성][14]

8. 에 **Questetra BPM Suite** 회사 사이트 hello 다음 단계를 수행 하십시오. 
   
    ![Single Sign-on 구성][15]
   
    a. **Single Sign-On 사용**을 선택합니다.
   
    b. Hello Azure 클래식 포털에서 복사 hello **발급자 URL** 값을 복사한 다음 hello에 붙여 넣을 **엔터티 ID** 텍스트 상자에 붙여넣습니다.
   
    c. Hello Azure 클래식 포털에서 복사 hello **Single Sign-on 서비스 URL** 값을 복사한 다음 hello에 붙여 넣을 **로그인 페이지 URL** 텍스트 상자에 붙여넣습니다.
   
    d. Hello Azure 클래식 포털에서 복사 hello **Single Sign-Out 서비스 URL** 값을 복사한 다음 hello에 붙여 넣을 **로그 아웃 페이지 URL** 텍스트 상자에 붙여넣습니다.
   
    e. Hello에 **NameID 형식** 텍스트 상자에 **urn: oasis: 이름: tc: SAML:1.1:nameid-: emailAddress**합니다.

    f. 다운로드한 인증서에서 Base-64로 인코딩된 파일을 만듭니다. 

    >[!TIP] 
    >자세한 내용은 참조 하십시오. [어떻게 tooconvert 이진은 텍스트 파일에을 인증서](http://youtu.be/PlgrzUZ-Y1o)합니다.

    g. 콘텐츠를 클립보드에 복사 hello 메모장에서 e-64로 인코딩된 인증서를 열고 hello에 붙여 넣습니다 **유효성 검사 인증서** 텍스트 상자에 붙여넣습니다. 

    h. **Save**를 클릭합니다.

1. Azure 클래식 포털 hello에 hello single sign on 구성 확인을 선택한 다음 클릭 **다음**합니다. 
   
    ![Azure AD Connect의 정의][17]

2. Hello에 **Single sign on 확인** 페이지 **완료**합니다.  
   
    ![Azure AD Connect의 정의][18]


### <a name="creating-an-azure-ad-test-user"></a>Azure AD 테스트 사용자 만들기
이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 클래식 포털의에서 테스트 사용자를입니다.

**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**

1. Hello에 **Azure 클래식 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Active Directory**합니다.
   
    ![Azure AD 테스트 사용자 만들기][100] 

2. Hello에서 **디렉터리** 목록, 선택 hello 디렉터리 tooenable 디렉터리 통합을 구하려는 합니다.

3. toodisplay hello 목록이 hello 바탕 화면에서 hello 메뉴에서 사용자가 클릭 **사용자**합니다.
   
    ![Azure AD 테스트 사용자 만들기][101] 

4. tooopen hello **사용자 추가** hello 아래쪽에 hello 도구 모음에서 대화 상자에서 클릭 **사용자 추가**합니다. 
   
    ![Azure AD 테스트 사용자 만들기][102] 

5. Hello에 **이 사용자에 대해 알리기** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.
   
    ![Azure AD 테스트 사용자 만들기][103]
   
    a. **사용자 유형**에서 **조직의 새 사용자**를 선택합니다.
   
    b. Hello 사용자 이름에서에서 **textbox**, 형식 **BrittaSimon**합니다.
   
    c. 다음을 클릭합니다.

6. Hello에 **사용자 프로필** 대화 상자 페이지를 hello 다음 단계를 수행 합니다. 
   
    ![Azure AD 테스트 사용자 만들기][104] 
   
    a. Hello에 **이름** 텍스트 상자에 **Britta**합니다. 
   
    b. Hello에 **성** 텍스트 상자에, **Simon**합니다.
   
    c. Hello에 **표시 이름** 텍스트 상자에 **Britta Simon**합니다.
   
    d. Hello에 **역할** 목록에서 **사용자**합니다.
   
    e. **다음**을 누릅니다.

7. Hello에 **임시 암호 가져오기** 대화 상자 페이지에서 클릭 **만들**합니다.
   
    ![Azure AD 테스트 사용자 만들기][105]  

8. Hello에 **임시 암호 가져오기** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.
   
    ![Azure AD 테스트 사용자 만들기][106]   
   
    a. Hello hello 값 적어 **새 암호**합니다.
   
    b. **완료**를 클릭합니다.   

### <a name="creating-a-questetra-bpm-suite-test-user"></a>Questetra BPM Suite 테스트 사용자 만들기
이 섹션의 hello 목표 toocreate Britta Simon Questetra BPM 제품군의 라는 사용자를입니다.

**toocreate Britta Simon Questetra BPM 제품군의 라는 사용자를 만들면 hello 다음 단계를 수행 합니다.**

1. 관리자 권한으로 로그온 tooyour Questetra BPM Suite 회사 사이트입니다.
2. 너무 이동**시스템 설정 > 사용자 목록 > 새 사용자**합니다. 
3. Hello 새 사용자 대화 상자에서 hello 다음 단계를 수행 합니다. 
   
    ![테스트 사용자 만들기][300] 
   
    a. Hello에 **이름** textbox를 Azure AD에 Britta의 사용자 이름을 입력 합니다.
   
    b. Hello에 **전자 메일** textbox를 Azure AD에 Britta의 사용자 이름을 입력 합니다.
   
    c. Hello에 **암호** 텍스트 상자에 암호입니다.

4. **새 사용자 추가**를 클릭합니다.

### <a name="assigning-hello-azure-ad-test-user"></a>Azure AD hello 테스트 사용자를 할당합니다.
이 섹션의 hello 목표에는 자신의 액세스 tooQuestetra BPM 제품군을 부여 하 여 tooenabling Britta Simon toouse Azure single sign on입니다.

![Azure AD Connect의 정의][200]

**tooassign Britta Simon tooQuestetra BPM Suite hello 다음 단계를 수행 합니다.**

1. Hello Azure 클래식 포털 tooopen hello 응용 프로그램 보기 hello 디렉터리 보기에서 클릭 **응용 프로그램** hello 최상위 메뉴에 있습니다.
   
    ![Azure AD Connect의 정의][201]
2. Hello 응용 프로그램 목록에서 선택 **Questetra BPM Suite**합니다.
   
    ![Azure AD Connect의 정의][205]
3. Hello 메뉴에서 hello 위에 표시를 클릭 **사용자**합니다.
   
    ![Azure AD Connect의 정의][202]
4. Hello [사용자] 목록에서 선택 **Britta Simon**합니다.
   
    ![Azure AD Connect의 정의][203]
5. Hello 아래쪽에 hello 도구 모음에서 클릭 **할당**합니다.
   
    ![Azure AD Connect의 정의][204]

### <a name="testing-single-sign-on"></a>Single Sign-On 테스트
이 섹션의 hello 목적은 tootest 액세스 패널을 hello 사용 하 여 Azure AD single sign-on 구성 합니다.  
Hello 액세스 패널에서에서 hello Questetra BPM Suite 타일을 클릭할 때 자동으로 로그온 tooyour Questetra BPM Suite 응용 프로그램을 구해야 합니다.

## <a name="additional-resources"></a>추가 리소스
* [방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와](active-directory-saas-tutorial-list.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)

<!--Image references-->
[1]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_01.png


[8]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_06.png
[9]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_02.png
[10]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_03.png
[11]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_04.png
[12]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_05.png
[13]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_06.png
[14]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_07.png
[15]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_08.png
[16]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_09.png
[17]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_10.png
[18]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_08.png


[100]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_09.png 
[101]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_10.png 
[102]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_11.png 
[103]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_12.png 
[104]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_13.png 
[105]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_14.png 
[106]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_15.png 


[200]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_16.png 
[201]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_17.png 
[202]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_18.png
[203]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_19.png
[204]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_20.png
[205]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_12.png

[300]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_11.png 
