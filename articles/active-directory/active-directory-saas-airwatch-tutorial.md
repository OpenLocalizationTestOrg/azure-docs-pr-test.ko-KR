---
title: "자습서: AirWatch와 Azure Active Directory 통합 | Microsoft Docs"
description: "단일 로그온 tooconfigure 방법을 알아보려면 Azure Active Directory와 AirWatch 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 96a3bb1c-96c6-40dc-8ea0-060b0c2a62e5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: e5230d5a36824778a4d9804dadf9f13a0d11a68d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-airwatch"></a>자습서: AirWatch와 Azure Active Directory 통합

이 자습서에 설명 어떻게 toointegrate Azure Active Directory (Azure AD)와 AirWatch 합니다.

Azure AD와 AirWatch 통합 이점을 다음 hello로 제공 합니다.

- 액세스 tooAirWatch을 지닌 Azure AD에서 제어할 수 있습니다.
- 프로그램 사용자 tooautomatically get 로그온 tooAirWatch (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.
- 하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.

Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.

## <a name="prerequisites"></a>필수 조건

AirWatch와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.

- Azure AD 구독
- AirWatch Single Sign-on이 설정된 구독

> [!NOTE]
> 이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.

이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.

- 꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.
- Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.

## <a name="scenario-description"></a>시나리오 설명
이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다. 이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.

1. AirWatch는 hello 갤러리 추가
2. Azure AD Single Sign-on 구성 및 테스트

## <a name="adding-airwatch-from-hello-gallery"></a>AirWatch는 hello 갤러리 추가
tooconfigure hello와의 통합 AirWatch Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 AirWatch tooadd가 필요합니다.

**hello 갤러리에서 AirWatch tooadd hello 다음 단계를 수행 합니다.**

1. Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다. 

    ![Active Directory][1]

2. 너무 이동**엔터프라이즈 응용 프로그램**합니다. 이동 하 여 너무**모든 응용 프로그램**합니다.

    ![응용 프로그램][2]
    
3. tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.

    ![응용 프로그램][3]

4. Hello 검색 상자에 입력 **AirWatch**합니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_search.png)

5. Hello 결과 패널에서 선택 **AirWatch**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Azure AD Single Sign-on 구성 및 테스트
이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 AirWatch에서 Azure AD Single Sign-On을 구성하고 테스트합니다.

Single sign on toowork에 대 한 Azure AD는 tooknow AirWatch에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다. 즉, Azure AD 사용자와 AirWatch에 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.

Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** AirWatch에 합니다.

tooconfigure와 AirWatch 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.

1. **[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.
2. **[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.
3. **[AirWatch 테스트 사용자 만들기](#creating-a-airwatch-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 AirWatch에 해당 하는 도구입니다.
4. **[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.
5. **[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성

이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 AirWatch 응용 프로그램에서 single sign on 구성 합니다.

**Azure AD tooconfigure single sign on와 AirWatch를 hello 다음 단계를 수행 합니다.**

1. Hello hello에 Azure 포털에서에서 **AirWatch** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.

    ![Single Sign-on 구성][4]

2. Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.
 
    ![Single Sign-on 구성](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_samlbase.png)

3. Hello에 **AirWatch 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_url.png)

    a. Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<subdomain>.awmdm.com/AirWatch/Login?gid=companycode`

    b. Hello에 **식별자** 형식 hello 값으로 텍스트 상자`AirWatch`

    > [!NOTE] 
    > 이 값은 실제 hello 되지 않습니다. Hello 실제 로그온 url을이 값을 업데이트 합니다. 연락처 [AirWatch 클라이언트 지원 팀](http://www.air-watch.com/company/contact-us/) tooget이이 값입니다. 
 
4. Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello XML 파일을 컴퓨터에 저장 합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_certificate.png) 

5. Hello에 **AirWatch 구성** 섹션에서 클릭 **구성 AirWatch** tooopen **sign on 구성** 창. 복사 hello **SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**

    ![Single Sign-on 구성](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_configure.png) 

6. **저장** 단추를 클릭합니다.

    ![Single Sign-On 구성](./media/active-directory-saas-airwatch-tutorial/tutorial_general_400.png)
<CS>
7. 다른 웹 브라우저 창에서 관리자 권한으로 tooyour AirWatch 회사 사이트에 로그인 합니다.

8. Hello 왼쪽된 탐색 창에서 클릭 **계정**, 클릭 하 고 **관리자**합니다.
   
   ![관리자](./media/active-directory-saas-airwatch-tutorial/ic791920.png "관리자")

9. Hello 확장 **설정** 메뉴를 차례로 클릭 **디렉터리 서비스**합니다.
   
   ![설정](./media/active-directory-saas-airwatch-tutorial/ic791921.png "설정")

10. Hello 클릭 **사용자** 탭 hello **Base DN** 텍스트 상자에서 도메인 이름을 입력 하 고 클릭 **저장**합니다.
   
   ![사용자](./media/active-directory-saas-airwatch-tutorial/ic791922.png "사용자")

11. Hello 클릭 **서버** 탭 합니다.
   
   ![서버](./media/active-directory-saas-airwatch-tutorial/ic791923.png "서버")

12. Hello 다음 단계를 수행 합니다.
    
    ![업로드](./media/active-directory-saas-airwatch-tutorial/ic791924.png "업로드")   
    
    a. **디렉터리 유형**으로 **없음**을 선택합니다.

    b. **인증에 SAML 사용**을 선택합니다.

    c. tooupload hello 다운로드 한 인증서를 클릭 **업로드**합니다.

13. Hello에 **요청** 섹션를 hello 다음 단계를 수행 합니다.
    
    ![요청](./media/active-directory-saas-airwatch-tutorial/ic791925.png "요청")  

    a. **요청 바인딩 형식**으로 **POST**를 선택합니다.

    b. Hello hello에 Azure 포털에서에서 **Airwatch에서 single sign on 구성** 대화 상자 페이지에서 복사 hello **SAML Single Sign-on 서비스 URL** 값을 복사한 다음 hello에 붙여 넣을 **Id 공급자 Single Sign-on URL** 텍스트 상자에 붙여넣습니다.

    c. **NameID 형식**으로 **전자 메일 주소**를 선택합니다.

    d. **Save**를 클릭합니다.

14. Hello 클릭 **사용자** 탭을 다시 합니다.
    
    ![사용자](./media/active-directory-saas-airwatch-tutorial/ic791926.png "사용자")

15. Hello에 **특성** 섹션를 hello 다음 단계를 수행 합니다.
    
    ![특성](./media/active-directory-saas-airwatch-tutorial/ic791927.png "특성")

    a. Hello에 **개체 식별자** 텍스트 상자에 **http://schemas.microsoft.com/identity/claims/objectidentifier**합니다.

    b. Hello에 **Username** 텍스트 상자에 **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**합니다.

    c. Hello에 **표시 이름** 텍스트 상자에 **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**합니다.

    d. Hello에 **이름** 텍스트 상자에 **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**합니다.

    e. Hello에 **성** 텍스트 상자에 **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**합니다.

    f. Hello에 **전자 메일** 텍스트 상자에 **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**합니다.

    g. **Save**를 클릭합니다.

<CE>

### <a name="creating-an-azure-ad-test-user"></a>Azure AD 테스트 사용자 만들기
이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.

![Azure AD 사용자 만들기][100]

**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**

1. Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-airwatch-tutorial/create_aaduser_01.png) 

2. 사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-airwatch-tutorial/create_aaduser_02.png) 

3. tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-airwatch-tutorial/create_aaduser_03.png) 

4. Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-airwatch-tutorial/create_aaduser_04.png) 

    a. Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.

    b. Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** Britta Simon의 합니다.

    c. 선택 **암호 표시** hello hello 값 기록 **암호**합니다.

    d. **만들기**를 클릭합니다.
 
### <a name="creating-a-airwatch-test-user"></a>AirWatch 테스트 사용자 만들기

tooenable Azure AD 사용자가 toolog tooAirWatch에서 프로 비전 해야 tooAirWatch에 있습니다.

* AirWatch의 경우 프로비전은 수동 작업입니다.

**tooprovision 사용자 계정을 hello 다음 단계를 수행 합니다.**

1. Tooyour 로그인 **AirWatch** 회사 사이트에서 관리자 권한으로 로그인 합니다.
2. Hello 왼쪽에 hello 탐색 창에서 클릭 **계정**, 클릭 하 고 **사용자**합니다.
   
   ![사용자](./media/active-directory-saas-airwatch-tutorial/ic791929.png "사용자")
3. Hello에 **사용자** 메뉴를 클릭 하 여 **목록 보기**, 클릭 하 고 **추가 \> 사용자 추가**합니다.
   
   ![사용자 추가](./media/active-directory-saas-airwatch-tutorial/ic791930.png "사용자 추가")
4. Hello에 **사용자 추가 / 편집** 대화 상자에서 hello 다음 단계를 수행 합니다.

   ![사용자 추가](./media/active-directory-saas-airwatch-tutorial/ic791931.png "사용자 추가")   
   1. 형식 hello **Username**, **암호**, **암호 확인**, **이름**, **성**,  **전자 메일 주소** 유효한 Azure의 hello tooprovision 원하는 Active Directory 계정 관련 텍스트 상자입니다.
   2. **Save**를 클릭합니다.

>[!NOTE]
>다른 AirWatch 사용자 계정 만들기 도구를 사용할 수 있습니다 또는 AAD 사용자 계정을 tooprovision AirWatch에서 제공 된 Api입니다.
>  

### <a name="assigning-hello-azure-ad-test-user"></a>Azure AD hello 테스트 사용자를 할당합니다.

이 섹션에서는 tooAirWatch 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.

![사용자 할당][200] 

**tooassign Britta Simon tooAirWatch hello 다음 단계를 수행 합니다.**

1. Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.

    ![사용자 할당][201] 

2. Hello 응용 프로그램 목록에서 선택 **AirWatch**합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_app.png) 

3. Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.

    ![사용자 할당][202] 

4. **추가** 단추를 클릭합니다. 그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.

    ![사용자 할당][203]

5. **사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.

6. **사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.

7. **할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.
    
### <a name="testing-single-sign-on"></a>Single Sign-On 테스트

이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.

Single sign on 설정 tootest 원하는 hello 액세스 패널을 엽니다. 액세스 패널 hello에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.


## <a name="additional-resources"></a>추가 리소스

* [방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와](active-directory-saas-tutorial-list.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_203.png

