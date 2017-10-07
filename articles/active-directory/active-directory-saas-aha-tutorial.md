---
title: "자습서: Aha!와 Azure Active Directory 통합 | Microsoft Docs"
description: "단일 로그온 tooconfigure 방법을 알아보려면 Azure Active Directory와 Aha!입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ad955d3d-896a-41bb-800d-68e8cb5ff48d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: d844db3c0a035560e6fb275017215171743fba56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-aha"></a>자습서: Aha!와 Azure Active Directory 통합

이 자습서에 설명 어떻게 toointegrate Aha! azure Active Directory (Azure AD).

통합 Aha! Azure AD와 이점을 다음 hello로 제공 합니다.

- 액세스 tooAha을 지닌 Azure AD에서 제어할 수 있습니다!
- 에 사용자가 tooautomatically get 로그온 tooAha 사용 하도록 설정할 수 있습니다! Azure AD 계정이 포함된 (Single Sign-On)
- 하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.

Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.

## <a name="prerequisites"></a>필수 조건

tooconfigure Azure AD 통합와 Aha!, hello 다음 항목을 필요 합니다.

- Azure AD 구독
- Aha! Single Sign-On이 설정된 구독

> [!NOTE]
> 이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.

이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.

- 꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.
- Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.

## <a name="scenario-description"></a>시나리오 설명
이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다. 이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.

1. 추가 Aha! hello 갤러리에서
2. Azure AD Single Sign-on 구성 및 테스트

## <a name="adding-aha-from-hello-gallery"></a>추가 Aha! hello 갤러리에서
Aha tooconfigure hello 통합! Azure AD에 필요한 tooadd Aha! hello 갤러리 tooyour 목록에서 관리 되는 SaaS 앱.

**tooadd Aha! hello 갤러리 hello 다음 단계를 수행 합니다.**

1. Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다. 

    ![Active Directory][1]

2. 너무 이동**엔터프라이즈 응용 프로그램**합니다. 이동 하 여 너무**모든 응용 프로그램**합니다.

    ![응용 프로그램][2]
    
3. tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.

    ![응용 프로그램][3]

4. Hello 검색 상자에 입력 **Aha!**합니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-aha-tutorial/tutorial_aha_search.png)

5. Hello 결과 패널에서 선택 **Aha!**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-aha-tutorial/tutorial_aha_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Azure AD Single Sign-on 구성 및 테스트
이 섹션에서는 구성 및 Azure AD single sign-on 테스트와 Aha! "Britta Simon." 이라는 테스트 사용자

Single sign on toowork에 대 한 Azure AD에서 Aha hello 테이블에 해당 사용자 tooknow을 해야 합니다! Azure ad에서는 tooa 사용자입니다. 즉, Azure AD 사용자와 Aha에 hello 관련된 사용자 간의 링크 관계! toobe 설정 해야 합니다.

Aha!, hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계.

단일 로그온 tooconfigure 및 Azure AD 테스트와 Aha!, 구성 요소를 다음 toocomplete hello 필요:

1. **[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.
2. **[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.
3. **[만들기는 Aha! 테스트 사용자](#creating-an-aha-test-user)**  -toohave Britta Simon Aha에 상응 하는! 연결 된 toohello 사용자의 Azure AD 표현입니다.
4. **[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.
5. **[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성

이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 Aha에서 single sign on 구성! 응용 프로그램입니다.

**tooconfigure Azure AD에서 single sign-on와 Aha!, hello 다음 단계를 수행 합니다.**

1. Hello hello에 Azure 포털에서에서 **Aha!** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.

    ![Single Sign-on 구성][4]

2. Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.
 
    ![Single Sign-on 구성](./media/active-directory-saas-aha-tutorial/tutorial_aha_samlbase.png)

3. Hello에 **Aha! 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-aha-tutorial/tutorial_aha_url.png)

    a. Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<companyname>.aha.io/session/new`

    b. Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<companyname>.aha.io`

    > [!NOTE] 
    > 이러한 값은 실제 값이 아닙니다. 이러한 항목을 업데이트 로그온 URL과 식별자 실제 hello로 값입니다. 연락처 [Aha! 클라이언트 지원 팀](https://www.aha.io/company/contact) tooget 이러한 값입니다. 
 
4. Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello 메타 데이터 파일을 컴퓨터에 저장 합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-aha-tutorial/tutorial_aha_certificate.png) 

5. **저장** 단추를 클릭합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-aha-tutorial/tutorial_general_400.png)

6. 다른 웹 브라우저 창에서 로그인 tooyour Aha! 회사 사이트에 관리자로 로그인합니다.

7. Hello 메뉴에서 hello 위에 표시를 클릭 **설정을**합니다.

    ![설정](./media/active-directory-saas-aha-tutorial/IC798950.png "설정")

8. **계정**을 클릭합니다.
   
    ![프로필](./media/active-directory-saas-aha-tutorial/IC798951.png "프로필")

9. **보안 및 single sign-on**을 클릭합니다.
   
    ![보안 및 Single Sign-On](./media/active-directory-saas-aha-tutorial/IC798952.png "보안 및 Single Sign-On")

10. **Single Sign-On** 섹션에서 **ID 공급자**로 **SAML2.0**을 선택합니다.
   
    ![보안 및 Single Sign-On](./media/active-directory-saas-aha-tutorial/IC798953.png "보안 및 Single Sign-On")

11. Hello에 **Single Sign On** 구성 페이지를 hello 다음 단계를 수행 합니다.
    
    ![Single Sign-On](./media/active-directory-saas-aha-tutorial/IC798954.png "Single Sign-On")
    
       a. Hello에 **이름** 텍스트 상자, 구성에 대 한 이름 입력 합니다.

       b. **구성 사용 형식**에 **메타데이터 파일**을 선택합니다.
   
       c. tooupload 다운로드 한 메타 데이터 파일을 클릭 하 여 **찾아보기**합니다.
   
       d. **업데이트**를 클릭합니다.

> [!TIP]
> 이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!  Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션. 자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Azure AD 테스트 사용자 만들기
이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.

![Azure AD 사용자 만들기][100]

**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**

1. Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-aha-tutorial/create_aaduser_01.png) 

2. 사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-aha-tutorial/create_aaduser_02.png) 

3. tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-aha-tutorial/create_aaduser_03.png) 

4. Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-aha-tutorial/create_aaduser_04.png) 

    a. Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.

    b. Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.

    c. 선택 **암호 표시** hello hello 값 기록 **암호**합니다.

    d. **만들기**를 클릭합니다.
 
### <a name="creating-an-aha-test-user"></a>만들기는 Aha! 테스트 사용자

tooenable Azure AD 사용자가 toolog tooAha에!, Aha에 프로 비전 되어야 합니다.  

Hello 경우 Aha!, 프로 비전은 자동화 된 작업입니다. 작업 항목이 없습니다.

사용자가 필요한 경우 hello 첫 번째 single sign on 시도 하는 동안 자동으로 생성 됩니다.

>[!NOTE]
>다른 Aha! 사용자 계정 생성 도구 또는 Aha!가 제공한 API를 사용하여 AAD 사용자 계정을 tooprovision AAD 사용자 계정을 합니다.

### <a name="assigning-hello-azure-ad-test-user"></a>Azure AD hello 테스트 사용자를 할당합니다.

이 섹션에서는 Azure에서 single sign-on Britta Simon toouse tooAha 액세스 권한을 부여 하 여 사용 하면!입니다.

![사용자 할당][200] 

**tooassign Britta Simon tooAha!, hello 다음 단계를 수행 합니다.**

1. Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.

    ![사용자 할당][201] 

2. Hello 응용 프로그램 목록에서 선택 **Aha!**합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-aha-tutorial/tutorial_aha_app.png) 

3. Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.

    ![사용자 할당][202] 

4. **추가** 단추를 클릭합니다. 그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.

    ![사용자 할당][203]

5. **사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.

6. **사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.

7. **할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.
    
### <a name="testing-single-sign-on"></a>Single Sign-On 테스트

Single sign on 설정 tootest 원하는 hello 액세스 패널을 엽니다. 액세스 패널 hello에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.

## <a name="additional-resources"></a>추가 리소스

* [방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와](active-directory-saas-tutorial-list.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-aha-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-aha-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-aha-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-aha-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-aha-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-aha-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-aha-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-aha-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-aha-tutorial/tutorial_general_203.png

