---
title: "자습서: Azure Active Directory와 통합 @Task| Microsoft Docs"
description: "단일 로그온 tooconfigure 방법을 알아보려면 Azure Active Directory 간의 및 @Task합니다."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: aab8bd2f-f9dd-42da-a18e-d707865687d7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 0840763622086a02a27cfafff3b741bc66cec498
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-task"></a>자습서: @Task와(과) Azure Active Directory 통합
이 자습서의 hello 목적은 tooshow 있습니다 어떻게 toointegrate @Task Azure Active directory (Azure AD).  
통합 @Task Azure AD와 이점을 다음 hello로 제공 합니다. 

* 액세스할 수 있는 Azure AD에서 제어할 수 있습니다.too@Task
* 로그온 tooautomatically 가져올 사용자가 사용 하도록 설정할 수 too@Task (Single Sign-on)는 Azure AD 계정을 사용
* 하나의 중앙 위치-hello Azure 클래식 포털에서에서 사용자 계정을 관리할 수 있습니다.

Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.

## <a name="prerequisites"></a>필수 조건
tooconfigure Azure AD와의 통합 @Task, hello 다음 항목을 필요 합니다.

* Azure AD 구독
* @Task Single Sign-On이 설정된 구독

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

1. 추가 @Task hello 갤러리에서 
2. Azure AD Single Sign-on 구성 및 테스트

## <a name="adding-task-from-hello-gallery"></a>추가 @Task hello 갤러리에서
tooconfigure hello 통합 @Task tooadd 해야 Azure AD로 @Task 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 합니다.

**tooadd @Task hello 갤러리에서 hello 다음 단계를 수행 합니다.**

1. Hello에 **Azure 클래식 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Active Directory**합니다. 
   
    ![Active Directory][1] 
2. Hello에서 **디렉터리** 목록, 선택 hello 디렉터리 tooenable 디렉터리 통합을 구하려는 합니다.
3. tooopen hello 응용 프로그램 보기 hello 디렉터리 보기에서 클릭 **응용 프로그램** hello 상단 메뉴에서 합니다.
   
    ![응용 프로그램][2] 
4. 클릭 **추가** hello hello 페이지 맨 아래에 있습니다.
   
    ![응용 프로그램][3] 
5. Hello에 **하 신 toodo 원하는** 대화 상자에서 클릭 **hello 갤러리에서 응용 프로그램 추가**합니다.
   
    ![응용 프로그램][4] 
6. Hello 검색 상자에 입력  **@Task** 합니다.
   
    ![응용 프로그램][5] 
7. Hello 결과 창에서 선택  **@Task** , 클릭 하 고 **완료** tooadd hello 응용 프로그램입니다.
   
    ![응용 프로그램][30] 

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Azure AD Single Sign-on 구성 및 테스트
hello이 섹션은 tooconfigure 및 테스트 Azure AD의 단일 하면 사용 하 여 로그온 tooshow @Task "Britta Simon" 이라는 테스트 사용자를 기반 합니다.

Single sign on toowork에 대 한 Azure AD는 필요 tooknow hello 테이블에 해당 사용자의 @Task tooan Azure ad에서는 사용자가 있습니다. 즉, Azure AD 사용자와의 hello 관련된 사용자 간 링크 관계 @Task toobe 설정 해야 합니다.   
Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** 에서 @Task합니다.

tooconfigure 및 테스트 Azure AD single sign on와 @Task, toocomplete hello 구성 요소를 수행 해야 합니다.

1. **[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.
2. **[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.
3. **[만들기는 @Tasktest 사용자](#creating-a-halogen-software-test-user)**  -Britta Simon의 상응 하는 toohave @Taskthat 그녀의 연결 된 Azure AD toohello 표현입니다.
4. **[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.
5. **[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성
이 섹션의 hello 목표는 tooenable Azure AD에서 single sign-on hello Azure 클래식 포털에서에서 및 tooconfigure single sign on에서 프로그램 @Task 응용 프로그램입니다.

**와 Azure AD에서 single sign-on tooconfigure @Task, hello 다음 단계를 수행 합니다.**

1. Hello hello에 Azure 클래식 포털에서에서  **@Task**  응용 프로그램 통합 페이지에서 클릭 **single sign on 구성** tooopen hello **구성 Single Sign-on**  대화 상자입니다.
   
    ![Single Sign-on 구성][6] 
2. Hello에 **어떻게에 사용자가 toosign 보 시겠습니까 too@Task**  페이지에서 **Azure AD Single Sign-on**, 클릭 하 고 **다음**합니다.
   
    ![Azure AD Single Sign-On][7] 
3. Hello에 **앱 설정 구성** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.
   
    ![앱 설정 구성][8] 
   
     a. Hello에 **로그온 URL** 텍스트 상자에 toosign tooyour 사용자에서 사용 하는 hello URL 입력 @Task 응용 프로그램 (예::*https://<Tenant name>.attask ondemand.com*).
   
     b. **다음**을 누릅니다.
4. Hello에 **single sign-on 구성에서 @Task**  페이지 **메타 데이터 다운로드**, hello 메타 데이터 파일을 컴퓨터에 로컬로 저장 하 고 클릭 **다음**합니다.
   
    ![Azure AD Connect의 정의][9] 
5. 로그온 tooyour @Task 회사 사이트에서 관리자 권한으로 로그인 합니다.
6. 너무 이동**Single Sign On 구성을**합니다.
7. Hello에 **Single Sign On** 대화 상자에서 hello 다음 단계를 수행 합니다.
   
    ![Single Sign-on 구성][23]
   
    a. **형식**으로 **SAML 2.0**을 선택합니다.
   
    b. **서비스 공급자 ID**를 선택합니다.
   
    c. Hello Azure 클래식 포털에서 복사 hello **원격 로그인 URL**, 다음 hello에 붙여 넣는 **로그인 포털 URL** 텍스트 상자에 붙여넣습니다.
   
    d. Hello Azure 클래식 포털에서 복사 hello **Single Sign-Out 서비스 URL**, 다음 hello에 붙여 넣는 **Sign-Out URL** 텍스트 상자에 붙여넣습니다.
   
    e. Hello Azure 클래식 포털에서 복사 hello **암호 변경 URL**, 다음 hello에 붙여 넣는 **암호 변경 URL** 텍스트 상자에 붙여넣습니다.
   
    f. **Save**를 클릭합니다.
8. Azure 클래식 포털 hello에 hello single sign on 구성 확인을 선택한 다음 클릭 **다음**합니다. 
   
    ![Azure AD Connect의 정의][10]
9. Hello에 **Single sign on 확인** 페이지 **완료**합니다.  
   
    ![Azure AD Connect의 정의][11]

### <a name="creating-an-azure-ad-test-user"></a>Azure AD 테스트 사용자 만들기
이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 클래식 포털의에서 테스트 사용자를입니다.  

![Azure AD 사용자 만들기][20]

**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**

1. Hello에 **Azure 클래식 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Active Directory**합니다.
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-attask-tutorial/create_aaduser_02.png) 
2. Hello에서 **디렉터리** 목록, 선택 hello 디렉터리 tooenable 디렉터리 통합을 구하려는 합니다.
3. toodisplay hello 목록이 hello 바탕 화면에서 hello 메뉴에서 사용자가 클릭 **사용자**합니다.
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-attask-tutorial/create_aaduser_03.png) 
4. tooopen hello **사용자 추가** hello 아래쪽에 hello 도구 모음에서 대화 상자에서 클릭 **사용자 추가**합니다. 
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-attask-tutorial/create_aaduser_04.png) 
5. Hello에 **이 사용자에 대해 알리기** 대화 상자 페이지를 hello 다음 단계를 수행 합니다. 
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-attask-tutorial/create_aaduser_05.png) 
   
    a. 사용자 유형에서 조직의 새 사용자를 선택합니다.
   
    b. Hello 사용자 이름에서에서 **textbox**, 형식 **BrittaSimon**합니다.
   
    c. **다음**을 누릅니다.
6. Hello에 **사용자 프로필** 대화 상자 페이지를 hello 다음 단계를 수행 합니다. 
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-attask-tutorial/create_aaduser_06.png) 
   
    a. Hello에 **이름** 텍스트 상자에 **Britta**합니다.  
   
    b. Hello에 **성** 텍스트 상자에, **Simon**합니다.
   
    c. Hello에 **표시 이름** 텍스트 상자에 **Britta Simon**합니다.
   
    d. Hello에 **역할** 목록에서 **사용자**합니다.

    e. **다음**을 누릅니다.

7. Hello에 **임시 암호 가져오기** 대화 상자 페이지에서 클릭 **만들**합니다.
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-attask-tutorial/create_aaduser_07.png) 
8. Hello에 **임시 암호 가져오기** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-attask-tutorial/create_aaduser_08.png) 
   
    a. Hello hello 값 적어 **새 암호**합니다.
   
    b. **완료**를 클릭합니다.   

### <a name="creating-an-task-test-user"></a>@Task 테스트 사용자 만들기
이 섹션의 hello 목적은 toocreate Britta Simon 라는 사용자를 만들면 @Task합니다.

**toocreate Britta Simon 라는 사용자를 만들면 @Task, hello 다음 단계를 수행 합니다.**

1. Tooyour 로그온 @Task 회사 사이트에서 관리자 권한으로 로그인 합니다.
2. Hello 메뉴에서 hello 위에 표시를 클릭 **사람**합니다.
3. **새 사람**을 클릭합니다. 
4. Hello New Person 대화 상자에서 hello 다음 단계를 수행 합니다.
   
    ![@Task 테스트 사용자 만들기][21] 
   
    a. Hello에 **이름** textbox "Britta"를 입력 합니다.
   
    b. Hello에 **성** textbox "Simon"를 입력 합니다.
   
    c. Hello에 **전자 메일 주소** 텍스트 상자에 Azure Active Directory Britta Simon의 전자 메일 주소를 입력 합니다.
   
    d. **사람 추가**를 클릭합니다.

### <a name="assigning-hello-azure-ad-test-user"></a>Azure AD hello 테스트 사용자를 할당합니다.
이 섹션의 hello 목표 그녀의 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse tooenabling는 too@Task합니다.

![사용자 할당][200] 

**tooassign Britta Simon too@Task, hello 다음 단계를 수행 합니다.**

1. Hello Azure 클래식 포털 tooopen hello 응용 프로그램 보기 hello 디렉터리 보기에서 클릭 **응용 프로그램** hello 최상위 메뉴에 있습니다.
   
    ![사용자 할당][201] 
2. Hello 응용 프로그램 목록에서 선택  **@Task** 합니다.
   
    ![사용자 할당][202] 
3. Hello 메뉴에서 hello 위에 표시를 클릭 **사용자**합니다.
   
    ![사용자 할당][203] 
4. Hello [사용자] 목록에서 선택 **Britta Simon**합니다.
5. Hello 아래쪽에 hello 도구 모음에서 클릭 **할당**합니다.
   
    ![사용자 할당][205]

### <a name="testing-single-sign-on"></a>Single Sign-On 테스트
이 섹션의 hello 목적은 tootest 액세스 패널을 hello 사용 하 여 Azure AD single sign-on 구성 합니다.  
Hello를 클릭할 때 @Task 타일에 액세스 패널 hello, 자동으로 로그온 tooyour 얻어야 @Task 응용 프로그램입니다.

## <a name="additional-resources"></a>추가 리소스
* [방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와](active-directory-saas-tutorial-list.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-attask-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-attask-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-attask-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-attask-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_01.png
[30]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_02.png


[6]: ./media/active-directory-saas-attask-tutorial/tutorial_general_05.png
[7]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_03.png
[8]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_04.png
[9]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_05.png
[10]: ./media/active-directory-saas-attask-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-attask-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-attask-tutorial/tutorial_general_100.png
[21]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_08.png


[23]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_06.png

[200]: ./media/active-directory-saas-attask-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-attask-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_09.png
[203]: ./media/active-directory-saas-attask-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-attask-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-attask-tutorial/tutorial_general_205.png






