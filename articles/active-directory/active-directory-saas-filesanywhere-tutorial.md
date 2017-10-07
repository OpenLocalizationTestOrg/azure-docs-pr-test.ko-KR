---
title: "자습서: FilesAnywhere와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 FilesAnywhere 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: jeedes
ms.openlocfilehash: 376364a5c75f8d069ea6390c58586acb378cd8b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-filesanywhere"></a>자습서:FilesAnywhere와 Azure Active Directory 통합

이 자습서에 설명 어떻게 toointegrate FilesAnywhere Azure Active directory (Azure AD).

다음 이점을 hello로 제공 FilesAnywhere Azure AD와 통합:

- 액세스 tooFilesAnywhere을 지닌 Azure AD에서 제어할 수 있습니다.
- 프로그램 사용자 tooautomatically get 로그온 tooFilesAnywhere (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.
- 하나의 중앙 위치-hello Azure 관리 포털에서에서 사용자 계정을 관리할 수 있습니다.

Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.

## <a name="prerequisites"></a>필수 조건

다음 항목 hello가 필요 tooconfigure FilesAnywhere와 Azure AD 통합 합니다.

- Azure AD 구독
- FilesAnywhere Single Sign-On을 사용하도록 설정된 구독


> [!NOTE]
> 이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.


이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.

- 꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.
- Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.


## <a name="scenario-description"></a>시나리오 설명
이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다. 이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.

1. FilesAnywhere는 hello 갤러리 추가
2. Azure AD Single Sign-on 구성 및 테스트


## <a name="adding-filesanywhere-from-hello-gallery"></a>FilesAnywhere는 hello 갤러리 추가
tooconfigure hello와의 통합 FilesAnywhere Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 FilesAnywhere tooadd가 필요합니다.

**hello 갤러리에서 FilesAnywhere tooadd hello 다음 단계를 수행 합니다.**

1. Hello에  **[Azure 관리 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다. 

    ![Active Directory][1]

2. 너무 이동**엔터프라이즈 응용 프로그램**합니다. 이동 하 여 너무**모든 응용 프로그램**합니다.

    ![응용 프로그램][2]
    
3. 클릭 **추가** hello 대화의 hello 위쪽에 단추입니다.

    ![응용 프로그램][3]

4. Hello 검색 상자에 입력 **FilesAnywhere**합니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_search.png)

5. Hello 결과 패널에서 선택 **FilesAnywhere**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_addfromgallery.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Azure AD Single Sign-on 구성 및 테스트
이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 FilesAnywhere에서 Azure AD Single Sign-On을 구성하고 테스트합니다.

Single sign on toowork에 대 한 Azure AD는 tooknow FilesAnywhere에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다. 즉, Azure AD 사용자 및 FilesAnywhere에 hello 관련된 사용자 간 링크 관계를 설정할 toobe가 필요 합니다.

Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** FilesAnywhere에 합니다.

tooconfigure 및 FilesAnywhere 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.

1. **[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.
2. **[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.
3. **[FilesAnywhere 테스트 사용자 만들기](#creating-a-filesanywhere-test-user)**  -toohave Britta Simon 그녀의 연결 된 Azure AD toohello 표현인 FilesAnywhere에 해당 하는 도구입니다.
3. **[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.
4. **[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성

이 섹션에서는 Azure AD에서 single sign-on hello Azure 관리 포털에서 설정 및 FilesAnywhere 응용 프로그램에서 single sign on 구성 합니다.

**tooconfigure Azure AD single sign on, FilesAnywhere와 hello 다음 단계를 수행 합니다.**

1. Hello에 hello Azure 관리 포털에서 **FilesAnywhere** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.

    ![Single Sign-on 구성][4]

2. Hello에 **Single sign on** 대화 상자에서으로 **모드** 선택 **SAML 기반 로그온** tooenable single sign-on입니다.
 
    ![Single Sign-on 구성](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_samlbase.png)

3. Hello에 **FilesAnywhere 도메인 및 Url** tooconfigure hello 응용 프로그램에 필요한 경우 섹션 **IDP 시작 모드**:

    ![Single Sign-on 구성](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_url.png)
    
    a. Hello에 **회신 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<company name>.filesanywhere.com/saml20.aspx?c=215`
> [!NOTE]
> 해당 hello 값 점에 유의 하십시오 **215** 는 **clientid** 은 예 시일 뿐 하 고 있습니다. Tooreplace 필요한 hello 실제 clientid 값을 가진 것입니다.

4. Hello에 **FilesAnywhere 도메인 및 Url** 섹션 tooconfigure hello 응용 프로그램에 필요한 경우 **SP 시작 모드**, hello 다음 단계를 수행 합니다.
    
    ![Single Sign-on 구성](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_url1.png)

    a. Hello 클릭 **고급 URL 설정 표시** 옵션

    b. Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<sub domain>.filesanywhere.com/`

    > [!NOTE] 
    > 이러한 없는지 hello 실제 값 note 하십시오. Tooupdate hello 실제 로그온 URL 및 회신 URL 사용 하 여 이러한 값 해야합니다. 연락처 [FilesAnywhere 지원 팀](mailto:support@FilesAnywhere.com) tooget 이러한 값입니다. 

5. FilesAnywhere 소프트웨어 응용 프로그램에는 특정 형식의 hello SAML 어설션 합니다. 이 응용 프로그램에 대 한 클레임을 따라 hello를 구성 하십시오. Hello에서 이러한 특성의 hello 값을 관리할 수 있습니다 "**사용자 특성**" 응용 프로그램 통합 페이지에서 섹션. 다음 스크린 샷 hello이에 대 한 예가 나와 있습니다.
    
    ![Single Sign-on 구성](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_attribute.png)
    
    FilesAnywhere 러 워 hello 값을 사용자가 로그인 하면 hello **clientid** 에서 특성 [FilesAnywhere 팀](mailto:support@FilesAnywhere.com)합니다. Hello FilesAnywhere에서 제공 되는 고유 값을 가진 tooadd hello "클라이언트 Id" 특성을 해야 합니다. 위에 표시된 모든 특성이 필요합니다.
    > [!NOTE] 
    > 해당 hello 값 참고 **2331** 의 **clientid** 은 예 시일 뿐입니다. Tooprovide hello에 대 한 실제 값이 필요합니다.


6. Hello에 **사용자 특성** hello 섹션 **Single sign on** 대화 상자에서 위의 hello 이미지에 나와 있는 것 처럼 SAML 토큰 특성을 구성 하 고 hello 다음 단계를 수행 합니다.
    
    | 특성 이름 | 특성 값 |
    | ---------------| --------------- |    
    | clientid | *"uniquevalue"* |

    a. 클릭 **특성 추가** tooopen hello **특성 추가** 대화 상자.

    ![Single Sign-on 구성](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_04.png)

    ![Single Sign-on 구성](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_05.png)
    
    b. Hello에 **이름** textbox, 해당 행에 대 한 표시 형식 hello 특성 이름입니다.
    
    c. Hello에서 **값** 목록, 해당 행에 대 한 표시 유형 hello 특성 값입니다.
    
    d. **확인**을 클릭합니다.

7. **저장** 단추를 클릭합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_400.png)

8. Hello에 **SAML 서명 인증서** 섹션에서 클릭 **인증서 (Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_certificate.png) 

9. Hello에 **FilesAnywhere 구성** 섹션에서 클릭 **구성 FilesAnywhere** tooopen **sign on 구성** 창.

    ![Single Sign-on 구성](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_configure.png) 

    ![Single Sign-on 구성](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_configuresignon.png)

10. tooget SSO 구성 연락처 FilesAnywhere 끝 응용 프로그램에 대 한 완료 [FilesAnywhere 지원 팀](mailto:support@FilesAnywhere.com) 다운로드 하는 hello SAML 토큰 서명 인증서 및 단일 로그인 (SSO) URL을 제공 합니다.

### <a name="creating-an-azure-ad-test-user"></a>Azure AD 테스트 사용자 만들기
이 섹션의 hello 목표 toocreate Britta Simon 라는 hello Azure 관리 포털에서 테스트 사용자를입니다.

![Azure AD 사용자 만들기][100]

**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**

1. Hello에 **Azure 관리 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_01.png) 

2. 너무 이동**사용자 및 그룹** 클릭 **모든 사용자에 게** 사용자 toodisplay hello 목록입니다.
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_02.png) 

3. Hello 대화의 hello 위쪽 클릭 **추가** tooopen hello **사용자** 대화 상자.
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_03.png) 

4. Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_04.png) 

    a. Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.

    b. Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.

    c. 선택 **암호 표시** hello hello 값 기록 **암호**합니다.

    d. **만들기**를 클릭합니다. 



### <a name="creating-a-filesanywhere-test-user"></a>FilesAnywhere 테스트 사용자 만들기

응용 프로그램 적시 사용자 프로 비전 및 인증 사용자 hello 응용 프로그램에서에 자동으로 생성 한 후 마법사를 지원 합니다. 


### <a name="assigning-hello-azure-ad-test-user"></a>Azure AD hello 테스트 사용자를 할당합니다.

이 섹션에서는 액세스 tooFilesAnywhere 그녀의 권한을 부여 하 여 Azure single sign on Britta Simon toouse를 사용 합니다.

![사용자 할당][200] 

**tooassign Britta Simon tooFilesAnywhere hello 다음 단계를 수행 합니다.**

1. Hello Azure 관리 포털에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.

    ![사용자 할당][201] 

2. Hello 응용 프로그램 목록에서 선택 **FilesAnywhere**합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_app.png) 

3. Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.

    ![사용자 할당][202] 

4. **추가** 단추를 클릭합니다. 그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.

    ![사용자 할당][203]

5. **사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.

6. **사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.

7. **할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.
    


### <a name="testing-single-sign-on"></a>Single Sign-On 테스트

이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.

Hello 액세스 패널에서에서 hello FilesAnywhere 타일을 클릭할 때 자동으로 로그온 tooyour FilesAnywhere 응용 프로그램을 구해야 합니다.


## <a name="additional-resources"></a>추가 리소스

* [방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와](active-directory-saas-tutorial-list.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_203.png
