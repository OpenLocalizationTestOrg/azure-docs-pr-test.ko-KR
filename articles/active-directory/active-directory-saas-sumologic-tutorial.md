---
title: "자습서: SumoLogic과 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 SumoLogic 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: fbb76765-92d7-4801-9833-573b11b4d910
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 2ef1bd329f5db8899f0b57744e4c0f6eed1c532f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sumologic"></a>자습서: SumoLogic과 Azure Active Directory 통합

이 자습서에 설명 어떻게 toointegrate Azure Active Directory (Azure AD)와 SumoLogic 합니다.

Azure AD와 SumoLogic를 통합 hello 다음 이점을 제공 합니다.

- 액세스 tooSumoLogic을 지닌 Azure AD에서 제어할 수 있습니다.
- 프로그램 사용자 tooautomatically get 로그온 tooSumoLogic (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.
- 하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.

Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.

## <a name="prerequisites"></a>필수 조건

Azure AD 및 SumoLogic 통합 tooconfigure 다음 항목 hello가 필요 합니다.

- Azure AD 구독
- SumoLogic Single Sign-On이 설정된 구독

> [!NOTE]
> 이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.

이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.

- 꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.
- Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.

## <a name="scenario-description"></a>시나리오 설명
이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다. 이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.

1. SumoLogic는 hello 갤러리 추가
2. Azure AD Single Sign-on 구성 및 테스트

## <a name="adding-sumologic-from-hello-gallery"></a>SumoLogic는 hello 갤러리 추가
tooconfigure hello와의 통합 SumoLogic Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 SumoLogic tooadd가 필요합니다.

**hello 갤러리에서 SumoLogic tooadd hello 다음 단계를 수행 합니다.**

1. Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다. 

    ![Active Directory][1]

2. 너무 이동**엔터프라이즈 응용 프로그램**합니다. 이동 하 여 너무**모든 응용 프로그램**합니다.

    ![응용 프로그램][2]
    
3. tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.

    ![응용 프로그램][3]

4. Hello 검색 상자에 입력 **SumoLogic**합니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_search.png)

5. Hello 결과 패널에서 선택 **SumoLogic**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Azure AD Single Sign-on 구성 및 테스트
이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 SumoLogic에서 Azure AD Single Sign-On을 구성하고 테스트합니다.

Single sign on toowork에 대 한 Azure AD는 tooknow SumoLogic에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다. 즉, Azure AD 사용자와 SumoLogic에 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.

SumoLogic에 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.

tooconfigure와 SumoLogic 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.

1. **[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.
2. **[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.
3. **[SumoLogic 테스트 사용자 만들기](#creating-a-sumologic-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 SumoLogic에 해당 하는 도구입니다.
4. **[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.
5. **[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성

이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 SumoLogic 응용 프로그램에서 single sign on 구성 합니다.

**Azure AD tooconfigure single sign on와 SumoLogic를 hello 다음 단계를 수행 합니다.**

1. Hello hello에 Azure 포털에서에서 **SumoLogic** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.

    ![Single Sign-on 구성][4]

2. Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.
 
    ![Single Sign-on 구성](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_samlbase.png)

3. Hello에 **SumoLogic 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_url.png)

    a. Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<tenantname>.SumoLogic.com`

    b. Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:
    | |
    |--|
    | `https://<tenantname>.us2.sumologic.com` |
    | `https://<tenantname>.sumologic.com` |
    | `https://<tenantname>.us4.sumologic.com` |
    | `https://<tenantname>.eu.sumologic.com` |
    | `https://<tenantname>.au.sumologic.com` |

    > [!NOTE] 
    > 이러한 값은 실제 값이 아닙니다. 이러한 항목을 업데이트 로그온 URL과 식별자 실제 hello로 값입니다. 연락처 [SumoLogic 클라이언트 지원 팀](https://www.sumologic.com/contact-us/) tooget 이러한 값입니다. 
 
4. Hello에 **SAML 서명 인증서** 섹션에서 클릭 **인증서 (Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_certificate.png) 

5. **저장** 단추를 클릭합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-sumologic-tutorial/tutorial_general_400.png)

6. Hello에 **SumoLogic 구성** 섹션에서 클릭 **구성 SumoLogic** tooopen **sign on 구성** 창. 복사 hello **SAML 엔터티 ID, 및 SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**

    ![Single Sign-on 구성](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_configure.png) 

7. 다른 웹 브라우저 창에서 관리자 권한으로 tooyour SumoLogic 회사 사이트에 로그인 합니다.

8. 너무 이동**관리 \> 보안**합니다.
   
    ![관리](./media/active-directory-saas-sumologic-tutorial/ic778556.png "관리")

9. **SAML**을 클릭합니다.
   
    ![전역 보안 설정](./media/active-directory-saas-sumologic-tutorial/ic778557.png "전역 보안 설정")

10. Hello에서 **구성을 선택 하거나 새로 만들** 목록에서 선택 **Azure AD**, 클릭 하 고 **구성**합니다.
   
    ![SAML 2.0 구성](./media/active-directory-saas-sumologic-tutorial/ic778558.png "SAML 2.0 구성")

11. Hello에 **SAML 2.0 구성** 대화 상자에서 hello 다음 단계를 수행 합니다.
   
    ![SAML 2.0 구성](./media/active-directory-saas-sumologic-tutorial/ic778559.png "SAML 2.0 구성")
   
    a. Hello에 **구성 이름** 텍스트 상자에 **Azure AD**합니다. 

    b. **디버그 모드**를 선택합니다.

    c. Hello에 **발급자** 붙여넣기 hello 값의 텍스트 상자 **SAML 엔터티 ID**, Azure 포털에서 복사한입니다. 

    d. Hello에 **인증 요청 URL** 붙여넣기 hello 값의 텍스트 상자 **SAML Single Sign-on 서비스 URL**, Azure 포털에서 복사한입니다.

    e. E-64로 인코딩된 인증서 내용을 클립보드의 콘텐츠 복사 hello 메모장에서 열고 후 전체 인증서를 hello **X.509 인증서** 텍스트 상자에 붙여넣습니다.

    f. **이메일 속성**에서는 **SAML 제목 사용**을 선택합니다.  

    g. **SP 시작 로그인 구성**을 선택합니다.

    h. Hello에 **로그인 경로** 텍스트 상자에 **Azure** 클릭 **저장**합니다.

> [!TIP]
> 이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!  Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션. 자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Azure AD 테스트 사용자 만들기
이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.

![Azure AD 사용자 만들기][100]

**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**

1. Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sumologic-tutorial/create_aaduser_01.png) 

2. 사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sumologic-tutorial/create_aaduser_02.png) 

3. tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sumologic-tutorial/create_aaduser_03.png) 

4. Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sumologic-tutorial/create_aaduser_04.png) 

    a. Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.

    b. Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.

    c. 선택 **암호 표시** hello hello 값 기록 **암호**합니다.

    d. **만들기**를 클릭합니다.
 
### <a name="creating-a-sumologic-test-user"></a>SumoLogic 테스트 사용자 만들기

Tooenable Azure AD 사용자가 toolog tooSumoLogic에 주문 하 고에 프로 비전 된 tooSumoLogic 되어야 합니다.  

* Hello SumoLogic의 경우에서 프로 비전은 수동 작업입니다.

**tooprovision 사용자 계정을 hello 다음 단계를 수행 합니다.**

1. Tooyour 로그인 **SumoLogic** 테 넌 트입니다.

2. 너무 이동**관리 \> 사용자**합니다.
   
    ![사용자](./media/active-directory-saas-sumologic-tutorial/ic778561.png "사용자")

3. **추가**를 클릭합니다.
   
    ![사용자](./media/active-directory-saas-sumologic-tutorial/ic778562.png "사용자")

4. Hello에 **새 사용자** 대화 상자에서 hello 다음 단계를 수행 합니다.
   
    ![새 사용자](./media/active-directory-saas-sumologic-tutorial/ic778563.png "새 사용자") 
 
    a. 형식 hello tooprovision hello에 원하는 hello Azure AD 계정의 정보를 관련 **이름**, **성**, 및 **전자 메일** 입력란입니다.
  
    b. 원하는 역할을 선택합니다.
  
    c. **상태**는 **활성**을 선택합니다.
  
    ㄹ. **Save**를 클릭합니다.

>[!NOTE]
>다른 SumoLogic 사용자 계정 만들기 도구를 사용할 수 있습니다 또는 AAD 사용자 계정을 tooprovision SumoLogic에서 제공 된 Api입니다. 
> 

### <a name="assigning-hello-azure-ad-test-user"></a>Azure AD hello 테스트 사용자를 할당합니다.

이 섹션에서는 tooSumoLogic 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.

![사용자 할당][200] 

**tooassign Britta Simon tooSumoLogic hello 다음 단계를 수행 합니다.**

1. Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.

    ![사용자 할당][201] 

2. Hello 응용 프로그램 목록에서 선택 **SumoLogic**합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_app.png) 

3. Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.

    ![사용자 할당][202] 

4. **추가** 단추를 클릭합니다. 그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.

    ![사용자 할당][203]

5. **사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.

6. **사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.

7. **할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.
    
### <a name="testing-single-sign-on"></a>Single Sign-On 테스트

이 섹션의 hello 목적은 tootest 액세스 패널을 hello 사용 하 여 Azure AD single sign-on 구성 합니다.

Hello 액세스 패널에서에서 hello SumoLogic 타일을 클릭할 때 자동으로 로그온 tooyour SumoLogic 응용 프로그램을 구해야 합니다.

## <a name="additional-resources"></a>추가 리소스

* [방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와](active-directory-saas-tutorial-list.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_203.png

