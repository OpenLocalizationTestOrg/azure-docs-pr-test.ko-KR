---
title: "자습서: T&E Express와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory 및 T E Express 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: B42374E5-2559-4309-8EF2-820BEE7EBB0C
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/03/2017
ms.author: jeedes
ms.openlocfilehash: 9a568ace8dbc75fadbf37554996b1b597a813d56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-te-express"></a>자습서: T&E Express와 Azure Active Directory 통합

이 자습서에 설명 어떻게 toointegrate & Azure Active Directory (Azure AD)와 E Express입니다.

& 전자 Express Azure AD와 통합 이점을 다음 hello로 제공 합니다.

- Azure AD 액세스 tooT 가진 및 E Express에서 제어할 수 있습니다.
- Azure AD 계정을와 tooT 로그온 사용자 tooautomatically get 및 E Express (Single Sign-on)를 사용할 수 있습니다.
- 하나의 중앙 위치-hello Azure 관리 포털에서에서 사용자 계정을 관리할 수 있습니다.

Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.

## <a name="prerequisites"></a>필수 조건

t& E Express와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.

- Azure AD 구독
- T&E Express Single Sign-on이 설정된 구독

> [!NOTE]
> 이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.

이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.

- 꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.
- Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.

## <a name="scenario-description"></a>시나리오 설명
이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다. 이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.

1. & 전자 Express hello 갤러리 추가
2. Azure AD Single Sign-on 구성 및 테스트

## <a name="adding-te-express-from-hello-gallery"></a>& 전자 Express hello 갤러리 추가
tooconfigure hello와의 통합 & 전자 Express Azure AD로 관리 되는 SaaS 앱 목록이 갤러리 tooyour hello에서 tooadd T 및 E Express 필요한 합니다.

**tooadd T & hello 갤러리, 전자 Express hello 다음 단계를 수행 합니다.**

1. Hello에  **[Azure 관리 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다. 

    ![Active Directory][1]

2. 너무 이동**엔터프라이즈 응용 프로그램**합니다. 이동 하 여 너무**모든 응용 프로그램**합니다.

    ![응용 프로그램][2]
    
3. 클릭 **추가** hello 대화의 hello 위쪽에 단추입니다.

    ![응용 프로그램][3]

4. Hello 검색 상자에 입력 **t& E Express**합니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_search.png)

5. Hello 결과 패널에서 선택 **t& E Express**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Azure AD Single Sign-on 구성 및 테스트
이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 T&E Express에서 Azure AD Single Sign-On을 구성하고 테스트합니다.

Single sign on toowork에 대 한 Azure AD는 tooknow t& E Express에서 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다. 즉, Azure AD 사용자 및 설정 t& E Express 요구 toobe에 hello 관련된 사용자 간 링크 관계입니다.

Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **사용자 이름** t& E Express에서 합니다.

tooconfigure 및 t& E Express를 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.

1. **[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.
2. **[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.
3. **[T& E Express 테스트 사용자 만들기](#creating-a-te-express-test-user)**  -toohave Britta Simon & 표현인 연결 된 Azure AD toohello 그녀는 E Express에 해당 하는 도구입니다.
4. **[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.
5. **[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성

이 섹션에서는 Azure AD에서 single sign-on hello Azure 관리 포털에서 사용 하도록 설정 및 t& E Express 응용 프로그램에서 single sign on 구성 합니다.

**T 및 E Express, Azure AD에서 single sign-on tooconfigure hello 다음 단계를 수행 합니다.**

1. Hello에 hello Azure 관리 포털에서 **t& E Express** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.

    ![Single Sign-on 구성][4]

2. Hello에 **Single sign on** 대화 상자에서으로 **모드** 선택 **SAML 기반 로그온** tooenable single sign-on입니다.
 
    ![Single Sign-on 구성](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_samlbase.png)

3. Hello에 **T 및 E Express 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_url.png)

    a. Hello에 **식별자** 형식 hello 값으로 텍스트 상자:`https://<domain>.tyeexpress.com`

    b. Hello에 **회신 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<domain>.tyeexpress.com/authorize/samlConsume.aspx`

    > [!NOTE] 
    > 이러한 없는지 hello 실제 값 note 하십시오. Tooupdate hello 실제 식별자와 회신 URL 사용 하 여 이러한 값 해야합니다. 여기 있습니다 toouse hello의 고유 값을 hello 식별자의에서 문자열을 사용 하는 것이 좋습니다. 연락처 [& Express E 지원 팀](http://www.tyeexpress.com/contacto.aspx) tooget 이러한 값입니다.

5. Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello XML 파일을 컴퓨터에 저장 합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_certificate.png) 

6. **저장** 단추를 클릭합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_400.png)

8. tooconfigure single sign on에서 **t& E Express** 쪽, 로그인 toohello T 및 SAML 없이 E 빠른 응용 프로그램에 대 한 single sign-on이 관리자 자격 증명을 사용 하 여 합니다.

9. Hello에서 **Admin** 탭을 클릭 **SAML 도메인** tooOpen hello SAML 설정 페이지.

    ![Single Sign-on 구성](./media/active-directory-saas-tyeexpress-tutorial/tye-SAML.png)

10. 선택 hello **Activar(Activate)** 옵션에서 **아니요** 너무**SI(Yes)**합니다. Hello에 **Id 공급자 메타 데이터** 텍스트 붙여넣기 hello 메타 데이터 XML이 있는 Azure 포털에서 donwloaded 합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-tyeexpress-tutorial/tyeAdmin.png)

11. Hello 클릭 **Guardar(Save)** 단추 toosave hello 설정 합니다. 


### <a name="creating-an-azure-ad-test-user"></a>Azure AD 테스트 사용자 만들기
이 섹션의 hello 목표 toocreate Britta Simon 라는 hello Azure 관리 포털에서 테스트 사용자를입니다.

![Azure AD 사용자 만들기][100]

**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**

1. Hello에 **Azure 관리 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_01.png) 

2. 너무 이동**사용자 및 그룹** 클릭 **모든 사용자에 게** 사용자 toodisplay hello 목록입니다.
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_02.png) 

3. Hello 대화의 hello 위쪽 클릭 **추가** tooopen hello **사용자** 대화 상자.
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_03.png) 

4. Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_04.png) 

    a. Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.

    b. Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.

    c. 선택 **암호 표시** hello hello 값 기록 **암호**합니다.

    d. **만들기**를 클릭합니다.
 
### <a name="creating-a-te-express-test-user"></a>T&E Express 테스트 사용자 만들기

Tooenable Azure AD 사용자가 toolog E Express T로 주문 하 고에 t& E Express에 이들 프로 비전 해야 합니다.  
T&E Express의 경우 프로비전은 수동 작업입니다.

**사용자 계정 수행 tooprovision hello 다음 단계:**

1. 관리자 권한으로 tooyour T 및 E Express 회사 사이트에 로그인 합니다.

2. Admin 태그 아래 사용자 tooopen hello 사용자가 마스터 페이지를 클릭 합니다.

    ![직원 추가](./media/active-directory-saas-tyeexpress-tutorial/tye-adminusers.png)

3. Hello 홈 페이지에서 클릭  **+**  tooadd hello 사용자입니다.

    ![직원 추가](./media/active-directory-saas-tyeexpress-tutorial/tye-usershome.png)

4. Hello 형태로 요청 하는 대로 모든 hello 필수 세부 정보를 입력 하 고 hello 단추 toosave hello 세부 정보 저장을 클릭 합니다.

    ![직원 추가](./media/active-directory-saas-tyeexpress-tutorial/tye-usersadd.png)

    ![직원 추가](./media/active-directory-saas-tyeexpress-tutorial/tye-userssave.png)


### <a name="assigning-hello-azure-ad-test-user"></a>Azure AD hello 테스트 사용자를 할당합니다.

이 섹션에서는 그녀의 액세스 tooT 및 E Express 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.

![사용자 할당][200] 

**tooassign Britta Simon tooT 및 E Express hello 다음 단계를 수행 합니다.**

1. Hello Azure 관리 포털에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.

    ![사용자 할당][201] 

2. Hello 응용 프로그램 목록에서 선택 **t& E Express**합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_app.png) 

3. Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.

    ![사용자 할당][202] 

4. **추가** 단추를 클릭합니다. 그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.

    ![사용자 할당][203]

5. **사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.

6. **사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.

7. **할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.
    
### <a name="testing-single-sign-on"></a>Single Sign-On 테스트

이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.

간단한 T & hello 액세스 패널에서에서 E Express 타일을 클릭할 때 자동으로 로그온 tooyour T 및 E Express 응용 프로그램을 구하십시오.

## <a name="additional-resources"></a>추가 리소스

* [방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와](active-directory-saas-tutorial-list.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_203.png

