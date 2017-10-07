---
title: "자습서: Halosys와 Azure Active Directory 통합 | Microsoft Docs"
description: "방법을 toouse Halosys tooenable Azure Active Directory와 single sign on, 자동화 된 프로비저닝 및 더에 대해 알아봅니다."
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 42a0eb7c-5cb7-44a9-b00b-b0e7df4b63e8
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 18043ed1b6f7ab45c59cfd36252bef1621618e51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-halosys"></a>자습서: Halosys와 Azure Active Directory 통합

이 자습서에 설명 어떻게 toointegrate Halosys Azure Active directory (Azure AD).

다음 이점을 hello로 제공 Halosys Azure AD와 통합:

- 액세스 tooHalosys을 지닌 Azure AD에서 제어할 수 있습니다.
- 프로그램 사용자 tooautomatically get 로그온 tooHalosys (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.
- 하나의 중앙 위치-hello Azure 클래식 포털에서에서 사용자 계정을 관리할 수 있습니다.

Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.

## <a name="prerequisites"></a>필수 조건

다음 항목 hello가 필요 tooconfigure Halosys와 Azure AD 통합 합니다.

- Azure AD 구독
- Halosys Single Sign-On이 설정된 구독


> [!NOTE] 
> 이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.


이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.

- 꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.
- Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.


## <a name="scenario-description"></a>시나리오 설명
이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.

이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.

1. Halosys는 hello 갤러리 추가
2. Azure AD Single Sign-on 구성 및 테스트


## <a name="adding-halosys-from-hello-gallery"></a>Halosys는 hello 갤러리 추가
tooconfigure hello와의 통합 Halosys Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Halosys tooadd가 필요합니다.

**hello 갤러리에서 Halosys tooadd hello 다음 단계를 수행 합니다.**

1. Hello에 **Azure 클래식 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Active Directory**합니다.

    ![Active Directory][1]
2. Hello에서 **디렉터리** 목록, 선택 hello 디렉터리 tooenable 디렉터리 통합을 구하려는 합니다.

3. tooopen hello 응용 프로그램 보기 hello 디렉터리 보기에서 클릭 **응용 프로그램** hello 상단 메뉴에서 합니다.

    ![응용 프로그램][2]

4. 클릭 **추가** hello hello 페이지 맨 아래에 있습니다.

    ![응용 프로그램][3]

5. Hello에 **하 신 toodo 원하는** 대화 상자에서 클릭 **hello 갤러리에서 응용 프로그램 추가**합니다.

    ![응용 프로그램][4]

6. Hello 검색 상자에 입력 **Halosys**합니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_01.png)
    
7. Hello 결과 창에서 선택 **Halosys**, 클릭 하 고 **완료** tooadd hello 응용 프로그램입니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_011.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Azure AD Single Sign-on 구성 및 테스트
이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Halosys에서 Azure AD Single Sign-On을 구성하고 테스트합니다.

Single sign on toowork에 대 한 Azure AD는 tooknow Halosys에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다. 즉, Azure AD 사용자 및 Halosys에 hello 관련된 사용자 간 링크 관계를 설정할 toobe가 필요 합니다.

Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** Halosys에 합니다.

tooconfigure 및 Halosys 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.

1. **[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.
2. **[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.
3. **[Halosys 테스트 사용자 만들기](#creating-a-halosys-test-user)**  -toohave Britta Simon 그녀의 연결 된 Azure AD toohello 표현인 Halosys에 해당 하는 도구입니다.
4. **[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.
5. **[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성

이 섹션에서는 Azure AD에서 single sign-on hello 클래식 포털의 설정 및 Halosys 응용 프로그램에서 single sign on 구성 합니다.


**tooconfigure Azure AD single sign on, Halosys와 hello 다음 단계를 수행 합니다.**

1. Hello에 hello 클래식 포털에서 **Halosys** 응용 프로그램 통합 페이지에서 클릭 **single sign on 구성** tooopen hello **구성 Single Sign-on** 대화 상자.
     
    ![Single Sign-on 구성][6] 

2. Hello에 **어떻게 tooHalosys에 사용자가 toosign 보 시겠습니까** 페이지에서 **Azure AD Single Sign-on**, 클릭 하 고 **다음**합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_03.png) 

3. Hello에 **앱 설정 구성** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_04.png) 

    a. Hello에 **로그온 URL** 텍스트 패턴 hello를 사용 하 여 사용자에 대 한 toosign tooyour Halosys 응용 프로그램에서 사용 하는 hello URL 입력: `https://<company-name>.Halosys.com/client-api/api`합니다.

    임시로 hello **식별자 URL** 텍스트 패턴 hello에 hello URL 입력: `https://<company-name>.Halosys.com`합니다. 
         
4. Hello에 **Halosys에서 single sign on 구성** 페이지 **메타 데이터 다운로드**, hello 파일을 컴퓨터에 저장 합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_05.png)
   
5. tooget SSO 응용 프로그램에 대해 구성 된 Halosys 지원 팀에 문의 하 고 hello 다음을 제공 합니다.

    다운로드 한 • hello **메타 데이터 파일**
    
    • hello **SAML SSO URL**
    

6. Hello 클래식 포털의 hello single sign-on 구성 확인을 선택한 다음 클릭 **다음**합니다.
    
    ![Azure AD Single Sign-On][10]

7. Hello에 **Single sign on 확인** 페이지 **완료**합니다.  
 
    ![Azure AD Single Sign-On][11]


### <a name="creating-an-azure-ad-test-user"></a>Azure AD 테스트 사용자 만들기
이 섹션에서는 Britta Simon 라는 hello 클래식 포털의 테스트 사용자를 만듭니다.


![Azure AD 사용자 만들기][20]

**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**

1. Hello에 **Azure 클래식 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Active Directory**합니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-Halosys-tutorial/create_aaduser_09.png) 

2. Hello에서 **디렉터리** 목록, 선택 hello 디렉터리 tooenable 디렉터리 통합을 구하려는 합니다.

3. toodisplay hello 목록이 hello 바탕 화면에서 hello 메뉴에서 사용자가 클릭 **사용자**합니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-Halosys-tutorial/create_aaduser_03.png) 

4. tooopen hello **사용자 추가** hello 아래쪽에 hello 도구 모음에서 대화 상자에서 클릭 **사용자 추가**합니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-Halosys-tutorial/create_aaduser_04.png) 

5. Hello에 **이 사용자에 대해 알리기** 대화 상자 페이지에서 수행할 단계를 수행 하는 hello: ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-Halosys-tutorial/create_aaduser_05.png) 

    a. 사용자 유형에서 조직의 새 사용자를 선택합니다.

    b. Hello 사용자 이름에서에서 **textbox**, 형식 **BrittaSimon**합니다.

    c. **다음**을 누릅니다.

6.  Hello에 **사용자 프로필** 대화 상자 페이지에서 수행할 단계를 수행 하는 hello: ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-Halosys-tutorial/create_aaduser_06.png) 

    a. Hello에 **이름** 텍스트 상자에 **Britta**합니다.  

    b. Hello에 **성** 텍스트 상자에, **Simon**합니다.

    c. Hello에 **표시 이름** 텍스트 상자에 **Britta Simon**합니다.

    d. Hello에 **역할** 목록에서 **사용자**합니다.

    e. **다음**을 누릅니다.

7. Hello에 **임시 암호 가져오기** 대화 상자 페이지에서 클릭 **만들**합니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-Halosys-tutorial/create_aaduser_07.png) 

8. Hello에 **임시 암호 가져오기** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-Halosys-tutorial/create_aaduser_08.png) 

    a. Hello hello 값 적어 **새 암호**합니다.

    b. **완료**를 클릭합니다.   



### <a name="creating-a-halosys-test-user"></a>Halosys 테스트 사용자 만들기

이 섹션에서는 Halosys에서 Britta Simon이라는 사용자를 만듭니다. 와 협력 하세요 Halosys hello Halosys 플랫폼에서 지원 팀 tooadd hello 사용자.


### <a name="assigning-hello-azure-ad-test-user"></a>Azure AD hello 테스트 사용자를 할당합니다.

이 섹션에서는 액세스 tooHalosys 그녀의 권한을 부여 하 여 Azure single sign on Britta Simon toouse를 사용 합니다.

![사용자 할당][200] 

**tooassign Britta Simon tooHalosys hello 다음 단계를 수행 합니다.**

1. Hello 클래식 포털에서 tooopen hello 응용 프로그램 보기 hello 디렉터리 보기를 클릭 **응용 프로그램** hello 최상위 메뉴에 있습니다.

    ![사용자 할당][201] 

2. Hello 응용 프로그램 목록에서 선택 **Halosys**합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_50.png) 

3. Hello 메뉴에서 hello 위에 표시를 클릭 **사용자**합니다.

    ![사용자 할당][203]

4. Hello [사용자] 목록에서 선택 **Britta Simon**합니다.

5. Hello 아래쪽에 hello 도구 모음에서 클릭 **할당**합니다.

    ![사용자 할당][205]


### <a name="testing-single-sign-on"></a>Single Sign-On 테스트

이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.

Hello Halosys hello 액세스 패널에서에서 타일을 클릭할 때 자동으로 로그온 tooyour Halosys 응용 프로그램을 구해야 합니다.


## <a name="additional-resources"></a>추가 리소스

* [방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와](active-directory-saas-tutorial-list.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_205.png
