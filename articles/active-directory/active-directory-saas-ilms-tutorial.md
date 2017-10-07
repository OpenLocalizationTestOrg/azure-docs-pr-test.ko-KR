---
title: "자습서: Azure Active Directory와 iLMS 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 iLMS 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d6e11639-6cea-48c9-b008-246cf686e726
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/13/2017
ms.author: jeedes
ms.openlocfilehash: da0936de23afcd5a4213aa6f699165f9bfa82c35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ilms"></a>자습서: iLMS와 Azure Active Directory 통합

이 자습서에 설명 어떻게 toointegrate iLMS Azure Active directory (Azure AD).

다음 이점을 hello로 제공 iLMS Azure AD와 통합:

- 액세스 tooiLMS을 지닌 Azure AD에서 제어할 수 있습니다.
- 프로그램 사용자 tooautomatically get 로그온 tooiLMS (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.
- 하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.

Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.

## <a name="prerequisites"></a>필수 조건

다음 항목 hello가 필요 tooconfigure iLMS와 Azure AD 통합 합니다.

- Azure AD 구독
- iLMS Single Sign-On이 설정된 구독

> [!NOTE]
> 이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.

이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.

- 꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.
- Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.

## <a name="scenario-description"></a>시나리오 설명
이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다. 이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.

1. ILMS hello 갤러리 추가
2. Azure AD Single Sign-on 구성 및 테스트

## <a name="adding-ilms-from-hello-gallery"></a>ILMS hello 갤러리 추가
tooconfigure hello와의 통합 iLMS Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 tooadd iLMS 필요합니다.

**hello 갤러리에서 tooadd iLMS hello 다음 단계를 수행 합니다.**

1. Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다. 

    ![Active Directory][1]

2. 너무 이동**엔터프라이즈 응용 프로그램**합니다. 이동 하 여 너무**모든 응용 프로그램**합니다.

    ![응용 프로그램][2]
    
3. tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** hello 대화의 hello 위쪽에 단추입니다.

    ![응용 프로그램][3]

4. Hello 검색 상자에 입력 **iLMS**합니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_search.png)

5. Hello 결과 패널에서 선택 **iLMS**, 클릭 **추가** tooadd hello 응용 프로그램 단추입니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Azure AD Single Sign-on 구성 및 테스트
이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 iLMS에서 Azure AD Single Sign-On을 구성하고 테스트합니다.

Single sign on toowork에 대 한 Azure AD는 tooknow iLMS에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다. 즉, Azure AD 사용자 및 iLMS에 hello 관련된 사용자 간 링크 관계를 설정할 toobe가 필요 합니다.

Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** iLMS에 합니다.

tooconfigure 및 iLMS 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.

1. **[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.
2. **[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.
3. **[ILMS 테스트 사용자 만들기](#creating-an-ilms-test-user)**  -toohave 그녀의 연결 된 Azure AD toohello 표현인 iLMS에 Britta Simon 해당 하는 도구입니다.
4. **[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.
5. **[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성

이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 iLMS 응용 프로그램에서 single sign on 구성 합니다.

**tooconfigure Azure AD single sign on, iLMS와 hello 다음 단계를 수행 합니다.**

1. Hello hello에 Azure 포털에서에서 **iLMS** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.

    ![Single Sign-on 구성][4]

2. Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.
 
    ![Single Sign-on 구성](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_samlbase.png)

3. Hello에 **iLMS 도메인 및 Url** 섹션를 hello tooconfigure hello 응용 프로그램에 필요한 경우 다음 단계를 수행 **IDP** 시작 모드:

    ![Single Sign-on 구성](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_url.png)

    a. Hello에 **식별자** 텍스트 붙여넣기 hello **식별자** 값에서 복사 **서비스 공급자** iLMS 관리자 포털에서 SAML 설정 섹션입니다.

    b. Hello에 **회신 URL** 텍스트 붙여넣기 hello **끝점 (URL)** 값에서 복사 **서비스 공급자** hello 다음을 있는 iLMS 관리자 포털에서 SAML 설정 섹션 패턴`https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`

    >[!Note]
    >여기서 '123456'은 식별자 값의 예입니다.

4. 확인 **고급 URL 설정 표시**tooconfigure hello 응용 프로그램에 필요한 경우, **SP** 시작 모드:

    ![Single Sign-on 구성](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_url1.png)

    Hello에 **로그온 URL** 텍스트 붙여넣기 hello **끝점 (URL)** 값에서 복사 **서비스 공급자** 으로 iLMS 관리자 포털에서 SAML 설정 섹션`https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`     

5. tooenable JIT 프로 비전, iLMS 응용 프로그램에는 hello SAML 어설션이 특정 형식입니다. 이 응용 프로그램에 대 한 클레임을 따라 hello를 구성 합니다. Hello에서 이러한 특성의 hello 값을 관리할 수 있습니다 **사용자 특성** 응용 프로그램 통합 페이지에서 섹션. 다음 스크린 샷 hello이에 대 한 예가 나와 있습니다.
    
    ![Single Sign-on 구성](./media/active-directory-saas-ilms-tutorial/4.png)
    
    만들 **부서, 지역** 및 **나누기** 특성과 iLMS에서 이러한 특성의 hello 이름을 추가 합니다. 위에 표시된 모든 특성이 필요합니다.    

    > [!NOTE] 
    > Tooenable 있는 **Un-recognized 사용자 계정 만들기** iLMS toomap에서 이러한 특성입니다. Hello 지침에 따라 [여기](http://support.inspiredelearning.com/customer/portal/articles/2204526) tooget hello 특성 구성에 배웁니다.

6. Hello에 **사용자 특성** hello 섹션 **Single sign on** 대화 상자에서 위의 hello 이미지에 나와 있는 것 처럼 SAML 토큰 특성을 구성 하 고 hello 다음 단계를 수행 합니다.
    
    | 특성 이름 | 특성 값 |
    | ---------------| --------------- |    
    | division | user.department |
    | region | user.state |
    | department | user.jobtitle |

    a. 클릭 **특성 추가** tooopen hello **특성 추가** 대화 상자.

    ![Single Sign-on 구성](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_04.png)

    ![Single Sign-on 구성](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_05.png)
    
    b. Hello에 **이름** textbox, 해당 행에 대 한 표시 형식 hello 특성 이름입니다.
    
    c. Hello에서 **값** 목록, 해당 행에 대 한 표시 유형 hello 특성 값입니다.
    
    d. **확인**을 클릭합니다.

7. Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello XML 파일을 컴퓨터에 저장 합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_certificate.png) 

8. **저장** 단추를 클릭합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-iLMS-tutorial/tutorial_general_400.png)

9. 다른 웹 브라우저 창에서 tooyour에 로그인 **iLMS 관리자 포털** 관리자 권한으로 합니다.

10. 클릭 **SSO:SAML** 아래 **설정** tooopen SAML 설정 탭 하 고 hello 다음 단계를 수행 합니다.
    
    ![Single Sign-on 구성](./media/active-directory-saas-ilms-tutorial/1.png) 

    a. Hello 확장 **서비스 공급자** 섹션 및 복사 hello **식별자** 및 **끝점 (URL)** 값입니다.

    ![Single Sign-on 구성](./media/active-directory-saas-ilms-tutorial/2.png) 

    b. **Identity Provider(ID 공급자)** 섹션에서 **Import Metadata(메타데이터 가져오기)**를 클릭합니다.
    
    c. 선택 hello **메타 데이터** 에서 Azure 포털에서 다운로드 한 파일 **SAML 서명 인증서** 섹션.

    ![Single Sign-on 구성](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_ssoconfig1.png) 

    d. JIT tooenable 하려는 경우 계정 프로 비전 toocreate iLMS 취소에 대 한-사용자가 인식 아래 단계를 수행 하십시오.
        
       - **Create Un-recognized User Account(인식할 수 없는 사용자 계정 만들기)**를 선택합니다.
       
       ![Single Sign-on 구성](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_ssoconfig2.png)

       -  Hello 특성을 iLMS의 hello 특성으로 Azure AD에 매핑하십시오. Hello 특성 열의 hello 특성 이름이 나 hello 기본값을 지정 합니다.

    e. 너무 이동**비즈니스 규칙** 탭 하 고 hello 다음 단계를 수행 합니다. 
        
       ![Single Sign-on 구성](./media/active-directory-saas-ilms-tutorial/5.png)

       - 확인 **Un-recognized 영역 만들기, 사업부 및 부서가** toocreate 영역, 사업부와의 Single sign-on hello 시 아직 존재 하지 않는 부서입니다.
        
       - 확인 **업데이트 사용자 프로필 중 로그인** toospecify hello 사용자의 프로필 각 Single sign-on으로 업데이트 되는지 여부를 합니다. 
        
       - 경우 hello **"업데이트 빈 값에 대 한 비 필수 필드에 사용자 프로필"** 선택적 프로필 필드는 로그인 시 비어 있는 발생 하면 hello 사용자 iLMS 프로필 toocontain 빈 값이 해당 필드에 대 한, 옵션을 선택 합니다.
        
       - 확인 **오류 알림 전자 메일 보내기** tooreceive hello 오류 알림 전자 메일을 원하는 hello 사용자의 hello 전자 메일을 입력 합니다.

11. 클릭 **저장** toosave hello 설정 단추입니다.

    ![Single Sign-on 구성](./media/active-directory-saas-ilms-tutorial/save.png)

> [!TIP]
> 이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!  Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션. 자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)
    
### <a name="creating-an-azure-ad-test-user"></a>Azure AD 테스트 사용자 만들기
이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.

![Azure AD 사용자 만들기][100]

**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**

1. Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-ilms-tutorial/create_aaduser_01.png) 

2. 너무 이동**사용자 및 그룹** 클릭 **모든 사용자에 게** 사용자 toodisplay hello 목록입니다.
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-ilms-tutorial/create_aaduser_02.png) 

3. Hello 대화의 hello 위쪽 클릭 **추가** tooopen hello **사용자** 대화 상자.
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-ilms-tutorial/create_aaduser_03.png) 

4. Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-ilms-tutorial/create_aaduser_04.png) 

    a. Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.

    b. Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.

    c. 선택 **암호 표시** hello hello 값 기록 **암호**합니다.

    d. **만들기**를 클릭합니다.
 
### <a name="creating-an-ilms-test-user"></a>iLMS 테스트 사용자 만들기

응용 프로그램 적시 사용자 프로 비전 및 인증 사용자가 hello 응용 프로그램에서 자동으로 생성 한 후 마법사를 지원 합니다. hello를 클릭 한 경우 작동 JIT **Un-recognized 사용자 계정 만들기** iLMS 관리자 포털에서 SAML 구성 설정 하는 동안 확인란을 선택 합니다.

Toocreate 된 사용자를 수동으로 필요한 경우 아래 단계에 따라 다음:

1. 관리자 권한으로 tooyour iLMS 회사 사이트에 로그인 합니다.

2. 클릭 **"사용자 등록"** 아래 **사용자** tooopen 탭 **사용자 등록** 페이지. 
   
   ![직원 추가](./media/active-directory-saas-ilms-tutorial/3.png)

3. Hello에 **"사용자 등록"** 페이지 hello 다음 단계를 수행 합니다.

    ![직원 추가](./media/active-directory-saas-ilms-tutorial/create_testuser_add.png)

    a. Hello에 **이름** 형식 hello 이름 Britta 텍스트입니다.
   
    b. Hello에 **성** 텍스트 형식 hello 성 Simon 합니다.

    c. Hello에 **전자 메일 ID** textbox Britta Simon 계정의 hello 전자 메일 주소를 입력 합니다.

    d. Hello에 **지역** 드롭다운에서 선택 hello 값 영역에 대 한 합니다.

    e. Hello에 **나누기** 드롭다운에서 선택 hello 부문에 대해서는 값입니다.

    f. Hello에 **부서** 드롭다운에서 부서에 대 한 선택 hello 값입니다.

    g. **Save**를 클릭합니다.

    > [!NOTE] 
    > 선택 하 여 등록 메일 toouser를 보낼 수 있습니다 **등록 메일 보내기** 확인란을 선택 합니다.

### <a name="assigning-hello-azure-ad-test-user"></a>Azure AD hello 테스트 사용자를 할당합니다.

이 섹션에서는 액세스 tooiLMS 그녀의 권한을 부여 하 여 Azure single sign on Britta Simon toouse를 사용 합니다.

![사용자 할당][200] 

**tooassign Britta Simon tooiLMS hello 다음 단계를 수행 합니다.**

1. Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.

    ![사용자 할당][201] 

2. Hello 응용 프로그램 목록에서 선택 **iLMS**합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_app.png) 

3. Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.

    ![사용자 할당][202] 

4. **추가** 단추를 클릭합니다. 그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.

    ![사용자 할당][203]

5. **사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.

6. **사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.

7. **할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.
    
### <a name="testing-single-sign-on"></a>Single Sign-On 테스트

이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.

Hello iLMS hello 액세스 패널에서에서 타일을 클릭할 때 자동으로 로그온 tooyour iLMS 응용 프로그램을 구해야 합니다.

## <a name="additional-resources"></a>추가 리소스

* [방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와](active-directory-saas-tutorial-list.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_203.png

