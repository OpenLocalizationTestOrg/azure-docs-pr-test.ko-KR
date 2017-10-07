---
title: "자습서: Splunk Enterprise and Splunk Cloud와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Splunk 엔터프라이즈 Splunk 클라우드 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b3e2b4a9-749c-4895-813d-db46f8dfdbf8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/09/2017
ms.author: jeedes
ms.openlocfilehash: 9bb6817cb31dce684cd9cc1c567fa3efc8906ad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-splunk-enterprise-and-splunk-cloud"></a>자습서: Splunk Enterprise and Splunk Cloud와 Azure Active Directory 통합

이 자습서에 설명 어떻게 toointegrate Splunk Enterprise와 Azure Active Directory (Azure AD)와 Splunk 클라우드입니다.

이점 다음 hello로 제공 Splunk 엔터프라이즈 및 클라우드 Splunk Azure AD와 통합:

- TooSplunk 엔터프라이즈 및 클라우드 Splunk 액세스할 수 있는 Azure AD에서 제어할 수 있습니다.
- Azure AD 계정을 사용 하면 사용자가 tooautomatically get 로그온 tooSplunk Splunk 클라우드 및 대기업 single sign on (SSO)를 사용할 수 있습니다.
- 하나의 중앙 위치-hello Azure 클래식 포털에서에서 사용자 계정을 관리할 수 있습니다.

Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.

## <a name="prerequisites"></a>필수 조건

다음 항목 hello가 필요 tooconfigure Splunk 엔터프라이즈 및 클라우드 Splunk와 Azure AD 통합 합니다.

- Azure AD 구독
- Splunk Enterprise and Splunk Cloud SSO가 사용하도록 설정된 구독


>[!NOTE]
>이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.
>

이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.

- 꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.
- Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.


## <a name="scenario-description"></a>시나리오 설명
이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.

이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.

1. Hello 갤러리에서 Splunk 엔터프라이즈 및 클라우드 Splunk 추가
2. Azure AD SSO 구성 및 테스트


## <a name="add-splunk-enterprise-and-splunk-cloud-from-hello-gallery"></a>Hello 갤러리에서 Splunk 엔터프라이즈 및 Splunk 클라우드를 추가 합니다.
tooconfigure hello와의 통합 Splunk 엔터프라이즈 및 클라우드 Splunk Azure AD로 tooadd Splunk 엔터프라이즈 및 hello 갤러리 tooyour 목록에서 Splunk 클라우드 SaaS 앱을 관리 합니다.

**hello 갤러리에서 Splunk 클라우드 및 tooadd Splunk 대기업 hello 다음 단계를 수행 합니다.**

1. Hello에 **Azure 클래식 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Active Directory**합니다.

    ![Active Directory][1]

2. Hello에서 **디렉터리** 목록, 선택 hello 디렉터리 tooenable 디렉터리 통합을 구하려는 합니다.

3. tooopen hello 응용 프로그램 보기 hello 디렉터리 보기에서 클릭 **응용 프로그램** hello 상단 메뉴에서 합니다.

    ![응용 프로그램][2]

4. 클릭 **추가** hello hello 페이지 맨 아래에 있습니다.

    ![응용 프로그램][3]

5. Hello에 **하 신 toodo 원하는** 대화 상자에서 클릭 **hello 갤러리에서 응용 프로그램 추가**합니다.

    ![응용 프로그램][4]

6. Hello 검색 상자에 입력 **Splunk Enterprise 또는 Splunk 클라우드**합니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_01.png)

7. Hello 결과 창에서 선택 **Splunk 엔터프라이즈 및 클라우드 Splunk**, 클릭 하 고 **완료** tooadd hello 응용 프로그램입니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_02.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성 및 테스트
이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Splunk Enterprise and Splunk Cloud에서 Azure AD Single Sign-On을 구성하고 테스트합니다.

Single sign on toowork에 대 한 Azure AD는 tooknow Splunk 클라우드 및 Splunk 대기업에서 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다. 즉, Azure AD 사용자 및 Splunk Enterprise 및 Splunk 클라우드 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.

Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** Splunk Enterprise 및 Splunk 클라우드입니다.

tooconfigure 및 Splunk 엔터프라이즈 및 Splunk 클라우드를 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.

1. **[Azure AD single sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.
2. **[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.
3. **[Splunk 엔터프라이즈 및 클라우드 Splunk 테스트 사용자 만들기](#creating-a-splunk-enterprise-and-splunk-cloud-test-user)**  -toohave Splunk 기업의 Britta Simon 및 그녀의 연결 된 Azure AD toohello 표현인 Splunk 클라우드 상응 합니다.
4. **[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.
5. **[Single sign on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.

### <a name="configure-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성

이 섹션에서는 hello 클래식 포털에서 Azure AD SSO를 사용 하도록 설정 및 Splunk 엔터프라이즈 및 Splunk 클라우드 응용 프로그램에서 SSO를 구성 합니다.


**Splunk 클라우드 Splunk Enterprise와 Azure AD에서 single sign-on tooconfigure hello 다음 단계를 수행 합니다.**

1. Hello에 hello 클래식 포털에서 **Splunk 엔터프라이즈 및 클라우드 Splunk** 응용 프로그램 통합 페이지에서 클릭 **single sign on 구성** tooopen hello **구성 Single Sign-on** 대화 상자.
     
    ![Single Sign-on 구성][6] 

2. Hello에 **त ु म tooSplunk Enterprise에 사용자가 toosign 및 Splunk 클라우드** 페이지에서 **Azure AD Single Sign-on**, 클릭 하 고 **다음**합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_03.png) 

3. Hello에 **앱 설정 구성** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_04.png) 
  1. Hello에 **로그온 URL** textbox, 사용자에 대 한 toosign tooyour Splunk 엔터프라이즈 및 패턴 hello를 사용 하 여 Splunk 클라우드 응용 프로그램에서 사용 하는 hello URL 입력:`https://<splunkserverUrl>/en-US/app/launcher/home`
  2. Hello에 **식별자** textbox Splunk 서버 hello URL 입력 합니다.
  3. Hello에 **회신 URL** 텍스트 패턴 hello로 hello URL 입력:`https://<splunkserver>/saml/acs`
  4. **다음**을 누릅니다.
 
4. Hello에 **Splunk 클라우드 및 Splunk 대기업에서 single sign on 구성** 페이지 hello 다음 단계를 수행 합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_05.png)
  1. 클릭 **메타 데이터 다운로드**, hello 파일을 컴퓨터에 저장 합니다.
  2. **다음**을 누릅니다.

5. tooget SSO 응용 프로그램에 대해 구성 된 Splunk 엔터프라이즈 및 클라우드 Splunk 지원 팀에 문의 하 고 hello 다음을 제공 합니다.

    * 다운로드 한 hello **federaton 메타 데이터**
6. Hello 클래식 포털의 hello single sign-on 구성 확인을 선택한 다음 클릭 **다음**합니다.
    
    ![Azure AD Single Sign-On][10]

7. Hello에 **Single sign on 확인** 페이지 **완료**합니다.  
 
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a>Azure AD 테스트 사용자 만들기
이 섹션에서는 Britta Simon 라는 hello 클래식 포털의 테스트 사용자를 만듭니다.

![Azure AD 사용자 만들기][20]

**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**

1. Hello에 **Azure 클래식 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Active Directory**합니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_09.png) 

2. Hello에서 **디렉터리** 목록, 선택 hello 디렉터리 tooenable 디렉터리 통합을 구하려는 합니다.

3. toodisplay hello 목록이 hello 바탕 화면에서 hello 메뉴에서 사용자가 클릭 **사용자**합니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_03.png) 

4. tooopen hello **사용자 추가** hello 아래쪽에 hello 도구 모음에서 대화 상자에서 클릭 **사용자 추가**합니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_04.png) 

5. Hello에 **이 사용자에 대해 알리기** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_05.png) 
  1. 사용자 유형에서 조직의 새 사용자를 선택합니다.
  2. Hello 사용자 이름에서에서 **textbox**, 형식 **BrittaSimon**합니다.
  3. **다음**을 누릅니다.

6.  Hello에 **사용자 프로필** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.
  
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_06.png) 
  1. Hello에 **이름** 텍스트 상자에 **Britta**합니다.  
  2. Hello에 **성** 텍스트 상자에, **Simon**합니다.
  3. Hello에 **표시 이름** 텍스트 상자에 **Britta Simon**합니다.
  4. Hello에 **역할** 목록에서 **사용자**합니다.
  5. **다음**을 누릅니다.

7. Hello에 **임시 암호 가져오기** 대화 상자 페이지에서 클릭 **만들**합니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_07.png) 

8. Hello에 **임시 암호 가져오기** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_08.png) 
  1. Hello hello 값 적어 **새 암호**합니다.
  2. 페이지 맨 아래에 있는 **완료**을 참조하세요.   

### <a name="create-a-splunk-enterprise-and-splunk-cloud-test-user"></a>Splunk Enterprise and Splunk Cloud 테스트 사용자 만들기

이 섹션에서는 Splunk Enterprise and Splunk Cloud에서 Britta Simon이라는 사용자를 만듭니다. 하십시오 작업할 Splunk 엔터프라이즈 및 클라우드 Splunk hello Splunk 엔터프라이즈 및 Splunk 클라우드 플랫폼에서 지원 팀 tooadd hello 사용자.


### <a name="assign-hello-azure-ad-test-user"></a>Azure AD hello 테스트 사용자를 할당 합니다.

이 섹션에서는 Azure SSOy 그녀의 액세스 tooSplunk 엔터프라이즈 및 클라우드 Splunk 부여 Britta Simon toouse를 활성화할 수 있습니다.

![사용자 할당][200] 

**tooassign Britta Simon tooSplunk 엔터프라이즈 및 Splunk 클라우드 hello 다음 단계를 수행 합니다.**

1. Hello 클래식 포털에서 tooopen hello 응용 프로그램 보기 hello 디렉터리 보기를 클릭 **응용 프로그램** hello 최상위 메뉴에 있습니다.

    ![사용자 할당][201] 

2. Hello 응용 프로그램 목록에서 선택 **Splunk 엔터프라이즈 및 클라우드 Splunk**합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_50.png) 

3. Hello 메뉴에서 hello 위에 표시를 클릭 **사용자**합니다.

    ![사용자 할당][203]

4. Hello [사용자] 목록에서 선택 **Britta Simon**합니다.

5. Hello 아래쪽에 hello 도구 모음에서 클릭 **할당**합니다.

    ![사용자 할당][205]

### <a name="test-single-sign-on"></a>Single Sign-On 테스트

이 섹션에서는 hello 액세스 패널을 사용 하 여 Azure AD SSOonfiguration 테스트할 수 있습니다.

Hello Splunk 엔터프라이즈 및 hello 액세스 패널에서에서 Splunk 클라우드 타일을 클릭할 때 자동으로 로그온 tooyour Splunk Enterprise 및 Splunk 클라우드 응용 프로그램을 구해야 합니다.


## <a name="additional-resources"></a>추가 리소스

* [방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와](active-directory-saas-tutorial-list.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_205.png
