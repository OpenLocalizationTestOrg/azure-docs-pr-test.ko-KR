---
title: "자습서: Absorb LMS와 Azure Active Directory 통합 | Microsoft 문서"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory 및 LMS 흡수 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ba9f1b3d-a4a0-4ff7-b0e7-428e0ed92142
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: a140a78a3a9474a6372a3ad4fb8251bd2452c990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-absorb-lms"></a>자습서: Absorb LMS와 Azure Active Directory 통합

이 자습서에 설명 어떻게 toointegrate 흡수 LMS Azure Active directory (Azure AD).

Azure AD와 흡수 LMS 통합 이점을 다음 hello 제공:

- 액세스 tooAbsorb LMS을 지닌 Azure AD에서 제어할 수 있습니다.
- 프로그램 사용자 tooautomatically get 로그온 tooAbsorb LMS (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.
- 하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.

Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 참조 tooknow 하려는 경우. [Azure Active Directory를 사용한 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.

## <a name="prerequisites"></a>필수 조건

흡수 LMS와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.

- Azure AD 구독
- Absorb LMS Single Sign-On이 설정된 구독

> [!NOTE]
> 이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.

이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.

- 꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.
- Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.

## <a name="scenario-description"></a>시나리오 설명
이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다. 이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.

1. 흡수 LMS hello 갤러리 추가
2. Azure AD Single Sign-on 구성 및 테스트

## <a name="adding-absorb-lms-from-hello-gallery"></a>흡수 LMS hello 갤러리 추가
tooconfigure hello와의 통합을 완화할 LMS tooAzure AD에서에서 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 흡수 LMS tooadd가 필요합니다.

**tooadd 흡수 hello 갤러리에서 LMS hello 다음 단계를 수행 합니다.**

1. Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다. 

    ![hello Azure Active Directory 단추][1]

2. 너무 이동**엔터프라이즈 응용 프로그램**합니다. 이동 하 여 너무**모든 응용 프로그램**합니다.

    ![hello 엔터프라이즈 응용 프로그램 블레이드][2]
    
3. tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.

    ![hello 새 응용 프로그램 단추][3]

4. Hello 검색 상자에 입력 **흡수 LMS**선택, **흡수 LMS** 결과 패널에서 클릭 **추가** tooadd hello 응용 프로그램 단추입니다.

    ![Hello 결과 목록에서 LMS 흡수](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성 및 테스트

이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Absorb LMS에서 Azure AD Single Sign-On을 구성하고 테스트합니다.

Single sign on toowork에 대 한 Azure AD는 tooknow 흡수 LMS에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다. 즉, Azure AD 사용자 및 LMS 흡수에 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.

Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **사용자 이름** 흡수 LMS에 합니다.

tooconfigure 및 LMS 흡수를 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.

1. **[Azure AD Single Sign-on 구성](#configure-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.
2. **[Azure AD 테스트를 만들고](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.
3. **[흡수 LMS 테스트 사용자 만들기](#create-an-absorb-lms-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 흡수 LMS에 해당 하는 도구입니다.
4. **[Azure AD hello 테스트 사용자를 할당](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.
5. **[Single sign on 테스트](#test-single-sign-on)**  -tooverify 구성 works를 hello 여부.

### <a name="configure-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성

이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 사용 하도록 설정 및 LMS 흡수 응용 프로그램에서 single sign on 구성 합니다.

**tooconfigure Azure AD single sign on 흡수 LMS와 hello 다음 단계를 수행 합니다.**

1. Hello hello에 Azure 포털에서에서 **흡수 LMS** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.

    ![Single Sign-On 구성 링크][4]

2. Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_samlbase.png)

3. Hello에 **흡수 LMS 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.

    ![Absorb LMS 도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_url.png)

    a. Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<subdomain>.myabsorb.com/Account/SAML`

    b. Hello에 **회신 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<subdomain>.myabsorb.com/Account/SAML`
     
    > [!NOTE] 
    > 이러한 값은 실제 hello 되지 않습니다. Hello 실제 식별자 및 회신 URL로이 값을 업데이트 합니다. 연락처 [흡수 LMS 클라이언트 지원 팀](https://www.absorblms.com/support) tooget 이러한 값입니다. 

4. Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello 메타 데이터 파일을 컴퓨터에 저장 합니다.

    ![hello 인증서 다운로드 링크](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_certificate.png) 

6. **저장** 단추를 클릭합니다.

    ![Single Sign-On 구성 저장 단추](./media/active-directory-saas-absorblms-tutorial/tutorial_general_400.png)
    
7. Hello에 **LMS 구성 흡수** 섹션에서 클릭 **흡수 LMS 구성** tooopen **sign on 구성** 창. 복사 hello **Sign-Out URL 및 SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**

    ![Absorb LMS 구성](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_configure.png) 

8. 다른 웹 브라우저 창에서 관리자 권한으로 tooyour 흡수 LMS 회사 사이트에 로그인 합니다.

9. Hello 클릭 **계정 아이콘** hello 관리 인터페이스에 있습니다. 

    ![Single Sign-on 구성](./media/active-directory-saas-absorblms-tutorial/1.png)

10. **포털 설정**을 클릭합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-absorblms-tutorial/2.png)
    
11. Hello 클릭 **사용자** 탭 합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-absorblms-tutorial/3.png)

12. Hello 구성 필드 Single Sign On 단계 tooaccess hello 다음을 수행 합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-absorblms-tutorial/4.png)

    a. 적절 한 선택 hello **모드**합니다.

    b. 열기 hello hello 메모장에서 Azure 포털에서에서 다운로드 한 인증서 제거 hello **---BEGIN 인증서---** 및 **---END 인증서---** 태그를 복사한 후에 콘텐츠 남은 hello hello **키** 텍스트 상자에 붙여넣습니다.
    
    c. Hello에 **Id 속성**, 선택 hello hello hello (예를 들어 hello userprinciplename에서에서 선택 하지 않으면 Azure AD 사용자 이름 여기 선택 합니다.) Azure AD에서에서 사용자 id에 따라 구성 해야 하는 적절 한 특성

    d. Hello에 **로그인 URL**, hello 붙여 **"SAML Single Sign-on 서비스 URL"** hello에서 복사한 값 **sign on 구성** hello Azure 포털의 창.

    e. Hello에 **로그 아웃 URL**, hello 붙여 **"Sign-Out URL"** hello에서 복사한 값 **sign on 구성** hello Azure 포털의 창.

13. **‘Only Allow SSO Login’**(SSO 로그인만 허용)을 사용하도록 설정합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-absorblms-tutorial/5.png)

14. **"저장"**을 클릭합니다.

> [!TIP]
> 이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!  Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션. 자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Azure AD 테스트 사용자 만들기

이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.

![Azure AD 테스트 사용자 만들기][100]

**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**

1. Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.

    ![hello Azure Active Directory 단추](./media/active-directory-saas-absorblms-tutorial/create_aaduser_01.png) 

2. 사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.
    
    !["사용자 및 그룹" hello 및 "모든 사용자" 링크](./media/active-directory-saas-absorblms-tutorial/create_aaduser_02.png) 

3. Hello 대화의 hello 위쪽 클릭 **추가** tooopen hello **사용자** 대화 상자.
 
    ![hello 추가 단추](./media/active-directory-saas-absorblms-tutorial/create_aaduser_03.png) 

4. Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.
 
    ![hello 사용자 대화 상자](./media/active-directory-saas-absorblms-tutorial/create_aaduser_04.png) 

    a. Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.

    b. Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.

    c. 선택 **암호 표시** hello hello 값 기록 **암호**합니다.

    d. **만들기**를 클릭합니다.

### <a name="create-an-absorb-lms-test-user"></a>Absorb LMS 테스트 사용자 만들기

tooenable Azure AD 사용자가 toolog LMS tooAbsorb에서은 프로 비전 해야 tooAbsorb LMS에에서 있습니다.  
Absorb LMS의 경우 프로비전은 수동 작업입니다.

**tooprovision 사용자 계정을 hello 다음 단계를 수행 합니다.**

1. 관리자 권한으로 흡수 LMS 회사 사이트 tooyour에 로그인 합니다.

2. **사용자** 탭을 클릭합니다.

    ![피플 초대](./media/active-directory-saas-absorblms-tutorial/absorblms_users.png)

3. 클릭 **사용자** hello에서 **사용자** 탭 합니다.

    ![피플 초대](./media/active-directory-saas-absorblms-tutorial/absorblms_userssub.png)

4.  **새로 추가** 드롭다운에서 **사용자**를 선택합니다.

    ![피플 초대](./media/active-directory-saas-absorblms-tutorial/absorblms_createuser.png)

5. Hello에 **사용자 추가** 페이지 hello 다음 단계를 수행 합니다.

    ![피플 초대](./media/active-directory-saas-absorblms-tutorial/user.png)

    a. Hello에 **이름** 형식 Britta 같은 hello 이름 텍스트 상자입니다.

    b. Hello에 **성** Simon 같은 형식 hello 마지막 이름 텍스트 상자입니다.
    
    c. Hello에 **Username** textbox hello Britta Simon와 같은 사용자 이름 입력 합니다.

    d. Hello에 **암호** textbox Britta Simon의 hello 암호를 입력 합니다.

    e. Hello에 **암호 확인** 형식 hello 텍스트 상자 같은 암호입니다.
    
    f. **활성**으로 설정합니다.   

6. **"저장"**을 클릭합니다.
 
### <a name="assign-hello-azure-ad-test-user"></a>Azure AD hello 테스트 사용자를 할당 합니다.

이 섹션에서는 액세스 tooAbsorb LMS 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.

![Hello 사용자 역할 할당][200]

**tooassign Britta Simon tooAbsorb LMS hello 다음 단계를 수행 합니다.**

1. Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.

    ![사용자 할당][201] 

2. Hello 응용 프로그램 목록에서 선택 **흡수 LMS**합니다.

    ![hello 응용 프로그램 목록에서 hello 흡수 LMS 링크](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_app.png) 

3. Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.

    ![hello "사용자 및 그룹" 링크][202] 

4. **추가** 단추를 클릭합니다. 그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.

    ![hello 할당 추가 창][203]

5. **사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.

6. **사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.

7. **할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.
    
### <a name="test-single-sign-on"></a>Single Sign-On 테스트

이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.

Hello 흡수 LMS hello 액세스 패널에서에서 타일을 클릭 합니다. 자동으로 로그온 tooyour 흡수 LMS 응용 프로그램을 얻게 됩니다. 액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](https://msdn.microsoft.com/library/dn308586)를 참조하세요.

## <a name="additional-resources"></a>추가 리소스

* [방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와](active-directory-saas-tutorial-list.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_203.png

