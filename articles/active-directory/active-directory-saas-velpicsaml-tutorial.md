---
title: "자습서: Velpic SAML과 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Velpic SAML 사이입니다."
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
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 613947d8fe95113382a2cdc0f79ce9eda85a0127
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-velpic-saml"></a>자습서: Velpic SAML과 Azure Active Directory 통합

이 자습서에 설명 어떻게 toointegrate Velpic SAML Azure Active directory (Azure AD).

다음 이점을 hello로 제공 Velpic SAML Azure AD와 통합:

- 액세스 tooVelpic SAML을 지닌 Azure AD에서 제어할 수 있습니다.
- 에 사용자가 tooautomatically get 로그온 tooVelpic (Single Sign-on)는 SAML 자신의 Azure AD 계정으로 사용 하도록 설정할 수 있습니다.
- 하나의 중앙 위치-hello Azure 관리 포털에서에서 사용자 계정을 관리할 수 있습니다.

Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.

## <a name="prerequisites"></a>필수 조건

다음 항목 hello가 필요 tooconfigure Velpic SAML와 Azure AD 통합 합니다.

- Azure AD 구독
- Velpic SAML Single Sign-On이 설정된 구독

> [!NOTE]
> 이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.

이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.

- 꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.
- Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.

## <a name="scenario-description"></a>시나리오 설명
이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다. 이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.

1. Hello 갤러리에서 Velpic SAML 추가
2. Azure AD Single Sign-on 구성 및 테스트

## <a name="adding-velpic-saml-from-hello-gallery"></a>Hello 갤러리에서 Velpic SAML 추가
tooconfigure hello와의 통합 Velpic SAML Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Velpic SAML tooadd가 필요합니다.

**hello 갤러리에서 Velpic SAML tooadd hello 다음 단계를 수행 합니다.**

1. Hello에  **[Azure 관리 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다. 

    ![Active Directory][1]

2. 너무 이동**엔터프라이즈 응용 프로그램**합니다. 이동 하 여 너무**모든 응용 프로그램**합니다.

    ![응용 프로그램][2]
    
3. 클릭 **추가** hello 대화의 hello 위쪽에 단추입니다.

    ![응용 프로그램][3]

4. Hello 검색 상자에 입력 **Velpic SAML**합니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_search.png)

5. Hello 결과 패널에서 선택 **Velpic SAML**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Azure AD Single Sign-on 구성 및 테스트
이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Velpic SAML에서 Azure AD Single Sign-On을 구성하고 테스트합니다.

Single sign on toowork에 대 한 Azure AD는 tooknow Velpic saml에서 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다. 즉, Azure AD 사용자 및 Velpic saml에서 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.

Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** Velpic saml에서 합니다.

tooconfigure 및 Velpic SAML을 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.

1. **[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.
2. **[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.
3. **[Velpic SAML 테스트 사용자 만들기](#creating-a-velpic-saml-test-user)**  -toohave 그녀의 연결 된 Azure AD toohello 표현인 Velpic saml Britta Simon의 해당 하는 도구입니다.
4. **[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.
5. **[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성

이 섹션에서는 Azure AD에서 single sign-on hello Azure 관리 포털에서 설정 및 Velpic SAML 응용 프로그램에서 single sign on 구성 합니다.

**Azure AD tooconfigure single sign on Velpic saml hello 다음 단계를 수행 합니다.**

1. Hello에 hello Azure 관리 포털에서 **Velpic SAML** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.

    ![Single Sign-on 구성][4]

2. Hello에 **Single sign on** 대화 상자에서으로 **모드** 선택 **SAML 기반 로그온** tooenable single sign-on입니다.
 
    ![Single Sign-on 구성](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_samlbase.png)

3. Hello에 hello 세부 사항을 입력 **Velpic SAML 도메인 및 Url** 섹션-

    ![Single Sign-on 구성](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_url.png)

    a. Hello에 **로그온 URL** 형식 hello 값으로 텍스트 상자:`https://<sub-domain>.velpicsaml.net`

    b. Hello에 **식별자** 텍스트 붙여넣기 hello **'Single sign on URL'** 값`https://auth.velpic.com/saml/v2/<entity-id>/login`
    
    > [!NOTE]
    > Hello Velpic SAML 팀이 hello 로그온 URL 제공 하 고 Velpic SAML 쪽 hello SSO 플러그 인을 구성할 때 식별자 값에 사용할 수 있습니다 note 하십시오. Toocopy Velpic SAML 응용 프로그램 페이지에서 값는 여기에 붙여 넣이 필요 합니다.

4. Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello XML 파일을 컴퓨터에 저장 합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_certificate.png) 

5. **저장** 단추를 클릭합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_400.png)

6. Hello Velpic SAML 구성 섹션에서 창 로그온 Velpic SAML 구성 tooopen 구성을 클릭 합니다. Hello 빠른 참조 섹션에서에서 hello SAML 엔터티 ID를 복사 합니다.

7. 다른 웹 브라우저 창에서 Velpic SAML 회사 사이트에 관리자 권한으로 로그인합니다.

8. 클릭 **관리** 탭 하 고 이동 너무**통합** 에 tooclick 해야 하는 섹션 **플러그 인** 단추 toocreate 새 플러그 인 로그인에 대 한 합니다.

    ![플러그 인](./media/active-directory-saas-velpicsaml-tutorial/velpic_1.png)

9. Hello 클릭 **'플러그 인을 추가 합니다.'** 단추입니다.
    
    ![플러그 인](./media/active-directory-saas-velpicsaml-tutorial/velpic_2.png)

10. Hello 클릭 **SAML** hello 플러그 인 추가 페이지에 바둑판식으로 배열 합니다.
    
    ![플러그 인](./media/active-directory-saas-velpicsaml-tutorial/velpic_3.png)

11. Hello 새 SAML 플러그 인의 hello 이름을 입력 하 고 hello 클릭 **'Add'** 단추입니다.

    ![플러그 인](./media/active-directory-saas-velpicsaml-tutorial/velpic_4.png)

12. 다음과 같이 hello 세부 정보를 입력 합니다.

    ![플러그 인](./media/active-directory-saas-velpicsaml-tutorial/velpic_5.png)

    a. Hello에 **이름** SAML 플러그 인의 형식 hello 이름 텍스트 상자입니다.

    b. Hello에 **발급자 URL** 텍스트 붙여넣기 hello **SAML 엔터티 ID** hello에서 복사한 **sign on 구성** hello Azure 포털의 창.

    c. Hello에 **공급자 메타 데이터 구성** hello Azure 포털에서 다운로드 한 메타 데이터 XML 파일을 업로드 합니다.

    d. Hello를 사용 하 여 프로 비전 시간에만 있는 tooenable SAML을 선택할 수도 있습니다 **'자동 새 사용자를 만들고'** 확인란을 선택 합니다. 사용자 Velpic에 존재 하지 않는 경우이 플래그는 해제 되어 Azure의 hello 로그인 실패 합니다. Hello 플래그는 활성화 된 hello 사용자가 자동으로 하는 경우에 프로 비전 Velpic hello 시 로그인 합니다. 

    e. 복사 hello **Single sign-on URL** Azure 포털에서 hello hello 텍스트 상자 및 붙여넣기 합니다.
    
    f. **Save**를 클릭합니다.

### <a name="creating-an-azure-ad-test-user"></a>Azure AD 테스트 사용자 만들기
이 섹션의 hello 목표 toocreate Britta Simon 라는 hello Azure 관리 포털에서 테스트 사용자를입니다.

![Azure AD 사용자 만들기][100]

**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**

1. Hello에 **Azure 관리 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_01.png) 

2. 너무 이동**사용자 및 그룹** 클릭 **모든 사용자에 게** 사용자 toodisplay hello 목록입니다.
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_02.png) 

3. Hello 대화의 hello 위쪽 클릭 **추가** tooopen hello **사용자** 대화 상자.
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_03.png) 

4. Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_04.png) 

    a. Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.

    b. Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.

    c. 선택 **암호 표시** hello hello 값 기록 **암호**합니다.

    d. **만들기**를 클릭합니다.
 
### <a name="creating-a-velpic-saml-test-user"></a>Velpic SAML 테스트 사용자 만들기

이 단계는 일반적으로 하지 않습니다 필요한 hello 응용 프로그램은 적시 사용자 프로 비전만 지원 합니다. Hello 자동 사용자 프로비저닝을 사용 하지 않는 경우 다음 수동 사용자 만들기 가능 아래에서 설명 합니다.

Velpic SAML 회사 사이트에 관리자 권한으로 로그인하고 다음 단계를 수행합니다.
    
1. 관리 탭 및 tooUsers 섹션 이동 클릭 한 다음 새 단추 tooadd 사용자입니다.

    ![사용자 추가](./media/active-directory-saas-velpicsaml-tutorial/velpic_7.png)

2. Hello에 **"새 사용자 만들기"** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.

    ![사용자](./media/active-directory-saas-velpicsaml-tutorial/velpic_8.png)
    
    a. Hello에 **이름** 형식 Britta Simon의 hello 이름 텍스트 상자입니다.

    b. Hello에 **성** Britta Simon의 형식 hello 마지막 이름 텍스트 상자입니다.

    c. Hello에 **사용자 이름** textbox Britta Simon의 hello 사용자 이름 입력 합니다.

    d. Hello에 **전자 메일** textbox Britta Simon 계정의 hello 전자 메일 주소를 입력 합니다.

    e. 나머지 hello 정보는 선택 사항이 고 필요한 경우를 채울 수 있습니다.
    
    f. **저장**을 클릭합니다.  

### <a name="assigning-hello-azure-ad-test-user"></a>Azure AD hello 테스트 사용자를 할당합니다.

이 섹션에서는 그녀의 액세스 tooVelpic SAML을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.

![사용자 할당][200] 

**tooassign Britta Simon tooVelpic SAML hello 다음 단계를 수행 합니다.**

1. Hello Azure 관리 포털에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.

    ![사용자 할당][201] 

2. Hello 응용 프로그램 목록에서 선택 **Velpic SAML**합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_app.png) 

3. Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.

    ![사용자 할당][202] 

4. **추가** 단추를 클릭합니다. 그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.

    ![사용자 할당][203]

5. **사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.

6. **사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.

7. **할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.
    
### <a name="testing-single-sign-on"></a>Single Sign-On 테스트

이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.

1. Hello Velpic SAML hello 액세스 패널에서에서 타일을 클릭할 때 Velpic SAML 응용 프로그램의 로그인 페이지를 가져와야 합니다. Hello 표시 되어야 **'Azure AD 로그인'** hello 로그인 페이지에서 단추입니다.

    ![플러그 인](./media/active-directory-saas-velpicsaml-tutorial/velpic_6.png)

2. Hello 클릭 **'Azure AD 로그인'** 에 Azure AD 계정을 사용 하 여 tooVelpic 단추 toolog 합니다.


## <a name="additional-resources"></a>추가 리소스

* [방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와](active-directory-saas-tutorial-list.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_203.png

