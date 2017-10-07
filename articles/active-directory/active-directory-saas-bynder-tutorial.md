---
title: "자습서: Bynder와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Bynder 사이입니다."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 4fb0ab26-b3b9-420a-8072-a0be80ea021e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: a2a8477580d28fe422f2836f483dff286bc71c93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bynder"></a>자습서: Bynder와 Azure Active Directory 통합
이 자습서의 hello 목적은 tooshow 있습니다 어떻게 toointegrate Bynder Azure Active directory (Azure AD).

다음 이점을 hello로 제공 Bynder Azure AD와 통합:

* 액세스 tooBynder을 지닌 Azure AD에서 제어할 수 있습니다.
* 프로그램 사용자가 tooautomatically get 로그온 tooBynder single sign-on (SSO) 자신의 Azure AD 계정으로 사용 하도록 설정할 수 있습니다.
* 하나의 중앙 위치-hello Azure 클래식 포털에서에서 사용자 계정을 관리할 수 있습니다.

Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.

## <a name="prerequisites"></a>필수 조건
다음 항목 hello가 필요 tooconfigure Bynder와 Azure AD 통합 합니다.

* Azure AD 구독
* Bynder SSO(Single Sign-On)가 설정된 구독

>[!NOTE]
>이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다. 
> 

이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.

* 꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.
* Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.

## <a name="scenario-description"></a>시나리오 설명
이 자습서의 hello 목적은 tooenable 있습니다 tootest Microsoft Azure AD SSO 테스트 환경에서 합니다.

이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.

1. Bynder는 hello 갤러리 추가
2. Microsoft Azure AD SSO 구성 및 테스트

## <a name="add-bynder-from-hello-gallery"></a>Bynder hello 갤러리 추가
tooconfigure hello와의 통합 Bynder Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Bynder tooadd가 필요합니다.

**hello 갤러리에서 Bynder tooadd hello 다음 단계를 수행 합니다.**

1. Hello에 **Azure 클래식 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Active Directory**합니다. 
   
    ![Active Directory][1]
2. Hello에서 **디렉터리** 목록, 선택 hello 디렉터리 tooenable 디렉터리 통합을 구하려는 합니다.
3. tooopen hello 응용 프로그램 보기 hello 디렉터리 보기에서 클릭 **응용 프로그램** hello 상단 메뉴에서 합니다.
   
    ![응용 프로그램][2]
4. 클릭 **추가** hello hello 페이지 맨 아래에 있습니다.
   
    ![응용 프로그램][3]
5. Hello에 **하 신 toodo 원하는** 대화 상자에서 클릭 **hello 갤러리에서 응용 프로그램 추가**합니다.
   
    ![응용 프로그램][4]
6. Hello 검색 상자에 입력 **Bynder**합니다.
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_01.png)
7. Hello 결과 패널에서 선택 **Bynder**, 클릭 하 고 **완료** tooadd hello 응용 프로그램입니다.
   
    ![Hello 갤러리에서 hello 앱 선택](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_001.png)

## <a name="configure-and-test-microsoft-azure-ad-sso"></a>Microsoft Azure AD SSO 구성 및 테스트
이 섹션의 hello 목적은 tooshow "Britta Simon" 이라는 테스트 사용자에 따라 tooconfigure 및 Microsoft Azure AD SSO Bynder 및 테스트 합니다.

SSO toowork에 대 한 Azure AD는 tooknow Bynder tooan 사용자 Azure ad에서에서 어떤 hello 테이블에 해당 사용자가 필요 합니다. 즉, Azure AD 사용자 및 Bynder에 hello 관련된 사용자 간 링크 관계를 설정할 toobe가 필요 합니다.

Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** Bynder에 합니다.

tooconfigure 및 테스트 Bynder와 Microsoft Azure AD SSO 구성 요소를 다음 toocomplete hello가 필요 합니다.

1. **[Microsoft Azure AD single sign-on 구성](#configuring-azure-ad-single-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.
2. **[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -Microsoft Azure AD Single Sign-on Britta Simon와 tootest 합니다.
3. **[Bynder 테스트 사용자 만들기](#creating-a-bynder-test-user)**  -toohave Britta Simon 그녀의 연결 된 Azure AD toohello 표현인 Bynder에 해당 하는 도구입니다.
4. **[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -Microsoft Azure AD Single Sign-on Britta Simon toouse tooenable 합니다.
5. **[Single sign on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.

### <a name="configuring-microsoft-azure-ad-sso"></a>Microsoft Azure AD SSO 구성
이 섹션에서는 Microsoft Azure AD SSO hello 클래식 포털에서 사용 하도록 설정 및 Bynder 응용 프로그램에서 SSO를 구성 합니다.

**tooconfigure Bynder와 Microsoft Azure AD SSO hello 다음 단계를 수행 합니다.**

1. Hello에 hello 클래식 포털에서 **Bynder** 응용 프로그램 통합 페이지에서 클릭 **single sign on 구성** tooopen hello **구성 Single Sign-on** 대화 상자.
   
    ![Single Sign-on 구성][6] 
2. Hello에 **어떻게 tooBynder에 사용자가 toosign 보 시겠습니까** 페이지에서 **Microsoft Azure AD Single Sign-on**, 클릭 하 고 **다음**합니다.
   
    ![Single Sign-on 구성](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_03.png)
3. Hello에 **앱 설정 구성** 대화 상자 페이지에서 tooconfigure hello 응용 프로그램에 필요한 경우 **IDP 시작 모드**hello 다음 단계를 수행 하 고 클릭, **다음**:
   
    ![Single Sign-on 구성](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_04.png)
  1. Hello에 **회신 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<company name>.getbynder.com/sso/SAML/authenticate/`
  2. **다음**을 누릅니다.
4. Tooconfigure hello 응용 프로그램에 필요한 경우 **SP 시작 모드** hello에 **앱 설정 구성** hello에는 클릭 하 여 대화 상자 페이지에서 **"표시 고급 설정 (선택 사항)"**hello를 입력 한 다음 **로그온 URL** 클릭 **다음**합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_10.png)
  1. Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<company name>.getbynder.com/login/`
  2. **다음**을 누릅니다.
  
   >[!NOTE]
   >이 자습서에서는 로그온 URL hello hello 값은 placeholfer 뿐입니다. tooget hello 실제 값입니다 사용자 환경에 대 한 Bynder를 문의 하십시오.
   >

5. Hello에 **Bynder에서 single sign on 구성** 페이지 hello 다음 단계를 수행 하 고 클릭 **다음**:
   
    ![Single Sign-on 구성](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_05.png)  
  1. 클릭 **메타 데이터 다운로드**, hello 파일을 컴퓨터에 저장 합니다.
  2. **다음**을 누릅니다.
6. SSO 응용 프로그램에 대해 구성 된 tooget Bynder 지원 팀에 문의 합니다. Hello 다운로드 한 메타 데이터 파일을 첨부 하 고 편인 SSO Bynder 팀 tooset와 공유 합니다.
7. Hello 클래식 포털의 hello single sign-on 구성 확인을 선택한 다음 클릭 **다음**합니다.
   
    ![Azure AD Single Sign-On][10]
8. Hello에 **Single sign on 확인** 페이지 **완료**합니다.  
   
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a>Azure AD 테스트 사용자 만들기
이 섹션의 hello 목표 Britta Simon 라는 hello 클래식 포털에서 toocreate 테스트 사용자를입니다.

![Azure AD 사용자 만들기][20]

**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**

1. Hello에 **Azure 클래식 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Active Directory**합니다.
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-bynder-tutorial/create_aaduser_09.png)
2. Hello에서 **디렉터리** 목록, 선택 hello 디렉터리 tooenable 디렉터리 통합을 구하려는 합니다.
3. toodisplay hello 목록이 hello 바탕 화면에서 hello 메뉴에서 사용자가 클릭 **사용자**합니다.
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-bynder-tutorial/create_aaduser_03.png)
4. tooopen hello **사용자 추가** hello 아래쪽에 hello 도구 모음에서 대화 상자에서 클릭 **사용자 추가**합니다.
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-bynder-tutorial/create_aaduser_04.png)
5. Hello에 **이 사용자에 대해 알리기** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-bynder-tutorial/create_aaduser_05.png)
  1. 사용자 유형에서 조직의 새 사용자를 선택합니다.
  2. Hello 사용자 이름에서에서 **textbox**, 형식 **BrittaSimon**합니다.
  3. **다음**을 누릅니다.
6. Hello에 **사용자 프로필** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.
   
   ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-bynder-tutorial/create_aaduser_06.png)
  1. Hello에 **이름** 텍스트 상자에 **Britta**합니다.  
  2. Hello에 **성** 텍스트 상자에, **Simon**합니다. 
  3. Hello에 **표시 이름** 텍스트 상자에 **Britta Simon**합니다.
  4. Hello에 **역할** 목록에서 **사용자**합니다.
  5. **다음**을 누릅니다.
7. Hello에 **임시 암호 가져오기** 대화 상자 페이지에서 클릭 **만들**합니다.
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-bynder-tutorial/create_aaduser_07.png)
8. Hello에 **임시 암호 가져오기** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-bynder-tutorial/create_aaduser_08.png)
   1. Hello hello 값 적어 **새 암호**합니다.
   2. 페이지 맨 아래에 있는 **완료**을 참조하세요.   

### <a name="create-a-bynder-test-user"></a>Bynder 테스트 사용자 만들기
hello이이 섹션의 목적은 toocreate Britta Simon Bynder에서 호출 하는 사용자입니다. Bynder는 적시에 프로비전을 지원하며 기본적으로 사용하도록 설정합니다.

이 섹션에 작업 항목이 없습니다. 새 사용자를 아직 존재 하지 않는 경우 시도 tooaccess Bynder 중 만들어질 수 있습니다.

>[!NOTE]
>Toocreate 된 사용자를 수동으로 해야 할 경우 toocontact hello Bynder 지원 팀을 해야 합니다. 
> 

### <a name="assign-hello-azure-ad-test-user"></a>Azure AD hello 테스트 사용자를 할당 합니다.
이 섹션의 hello 목표 액세스 tooBynder 그녀의 권한을 부여 하 여 tooenabling Britta Simon toouse Azure SSO를입니다.

   ![사용자 할당][200]

**tooassign Britta Simon tooBynder hello 다음 단계를 수행 합니다.**

1. Hello 클래식 포털에서 tooopen hello 응용 프로그램 보기 hello 디렉터리 보기를 클릭 **응용 프로그램** hello 최상위 메뉴에 있습니다.
   
    ![사용자 할당][201]
2. Hello 응용 프로그램 목록에서 선택 **Bynder**합니다.
   
    ![Single Sign-on 구성](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_50.png)
3. Hello 메뉴에서 hello 위에 표시를 클릭 **사용자**합니다.
   
    ![사용자 할당][203]
4. Hello [사용자] 목록에서 선택 **Britta Simon**합니다.
5. Hello 아래쪽에 hello 도구 모음에서 클릭 **할당**합니다.
   
    ![사용자 할당][205]

### <a name="test-single-sign-on"></a>Single Sign-On 테스트
이 섹션의 hello 목적은 tootest 액세스 패널을 hello 사용 하 여 Microsoft Azure AD SSO 구성 합니다.

Hello 액세스 패널에서에서 hello Bynder 타일을 클릭할 때 자동으로 로그온 tooyour Bynder 응용 프로그램을 구해야 합니다.

## <a name="additional-resources"></a>추가 리소스
* [방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와](active-directory-saas-tutorial-list.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_205.png
