---
title: "자습서: Azure Active Directory와 MOVEit Transfer - Azure AD 통합 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 MOVEit 전송-Azure AD 통합 합니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 8ff7102d-be73-4888-ae81-d8e3d01dd534
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: 5bbe4f2d952bd45c4d58d55ffc3467b4eb871fd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-moveit-transfer---azure-ad-integration"></a>자습서: Azure Active Directory와 MOVEit Transfer - Azure AD 통합 통합

이 자습서에 설명 어떻게 toointegrate MOVEit 전송-Azure Active Directory (Azure AD)와 Azure AD 통합 합니다.

MOVEit 전송-Azure AD와 Azure AD 통합 통합 이점을 다음 hello로 제공 합니다.

- 액세스 tooMOVEit 전송-Azure AD 통합을 지닌 Azure AD에서 제어할 수 있습니다.
- 에 사용자가 tooautomatically get 로그온 tooMOVEit 전송-Azure AD 통합 (Single Sign-on)는 Azure AD 계정 사용할 수 있습니다.
- 하나의 중앙 위치-hello Azure 포털에서 계정을 관리할 수 있습니다.

Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.

## <a name="prerequisites"></a>필수 조건

다음 항목 hello가 필요 tooconfigure MOVEit 전송-Azure AD 통합와 Azure AD 통합 합니다.

- Azure AD 구독
- MOVEit Transfer - Azure AD 통합 Single Sign-On이 설정된 구독

> [!NOTE]
> 이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.

이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.

- 꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.
- Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.

## <a name="scenario-description"></a>시나리오 설명
이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다. 이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.

1. 추가 MOVEit 전송-hello 갤러리에서 Azure AD 통합
2. Azure AD Single Sign-on 구성 및 테스트

## <a name="adding-moveit-transfer---azure-ad-integration-from-hello-gallery"></a>추가 MOVEit 전송-hello 갤러리에서 Azure AD 통합
MOVEit 전송-Azure AD에 Azure AD 통합의 tooconfigure hello 통합 tooadd MOVEit 전송-hello 갤러리 tooyour 목록에서 관리 되는 SaaS 앱의 Azure AD 통합 해야합니다.

**MOVEit 전송-hello 갤러리에서 Azure AD 통합 tooadd hello 다음 단계를 수행 합니다.**

1. Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다. 

    ![hello Azure Active Directory 단추][1]

2. 너무 이동**엔터프라이즈 응용 프로그램**합니다. 이동 하 여 너무**모든 응용 프로그램**합니다.

    ![hello 엔터프라이즈 응용 프로그램 블레이드][2]
    
3. tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.

    ![hello 새 응용 프로그램 단추][3]

4. Hello 검색 상자에 입력 **MOVEit 전송-Azure AD 통합**선택, **MOVEit 전송-Azure AD 통합** 결과 패널에서 클릭 **추가** 단추 tooadd hello 응용 프로그램입니다.

    ![MOVEit 전송-hello 결과 목록에서 Azure AD 통합](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성 및 테스트

이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 MOVEit Transfer - Azure AD 통합에서 Azure AD Single Sign-On을 구성하고 테스트합니다.

Single sign on toowork에 대 한 Azure AD는 tooknow hello 대응 사용자 MOVEit 전송에 필요-Azure AD에서 Azure AD 통합은 tooa 사용자. 즉, Azure AD 사용자 및 MOVEit 전송-에 hello 관련된 사용자 간 링크 관계를 Azure AD 통합 toobe 설정 해야 합니다.

MOVEit 전송-Azure AD 통합의에서 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.

tooconfigure 및 MOVEit 전송-Azure AD 통합을 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.

1. **[Azure AD Single Sign-on 구성](#configure-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.
2. **[Azure AD 테스트를 만들고](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.
3. **[MOVEit 전송-Azure AD 통합 테스트 사용자 만들기](#create-a-moveit-transfer---azure-ad-integration-test-user)**  사용자의 연결 된 Azure AD toohello 표현인-toohave Britta Simon MOVEit 전송에 해당 하는 도구-Azure AD 통합 합니다.
4. **[Azure AD hello 테스트 사용자를 할당](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.
5. **[Single sign on 테스트](#test-single-sign-on)**  -tooverify 구성 works를 hello 여부.

### <a name="configure-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성

이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 프로그램 MOVEit 전송-Azure AD 통합 응용 프로그램에서에서 single sign on 구성 합니다.

**tooconfigure Azure AD single sign on MOVEit 전송-Azure AD 통합 된 hello 다음 단계를 수행 합니다.**

1. Hello hello에 Azure 포털에서에서 **MOVEit 전송-Azure AD 통합** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.

    ![Single Sign-On 구성 링크][4]

2. Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_samlbase.png)

3. Hello에 **MOVEit 전송-Azure AD 통합 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_url.png)

    a. Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://contoso.com`

    b. Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://contoso.com/<tenatid>`

    c. Hello에 **회신 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://contoso.com/<tenatid>/SAML/SSO/HTTP-Post`    
     
    > [!NOTE] 
    > 이러한 값은 실제 값이 아닙니다. 이러한 항목을 업데이트 식별자, 회신 URL 및 로그온 URL 실제 hello로 값입니다. 이러한 값 나중에 참조할 수 있습니다 **서비스 공급자 메타 데이터 URL** 섹션 또는 연락처 [MOVEit 전송-Azure AD 통합 클라이언트 지원 팀](https://community.ipswitch.com/s/support) tooget 이러한 값입니다.

4. Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello 메타 데이터 파일을 컴퓨터에 저장 합니다.

    ![hello 인증서 다운로드 링크](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_certificate.png) 

5. **저장** 단추를 클릭합니다.

    ![Single Sign-On 구성 저장 단추](./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_400.png)
    
6. 관리자 권한으로 테 넌 트 MOVEit 전송 tooyour 로그인 합니다.

7. Hello 왼쪽된 탐색 창에서 클릭 **설정을**합니다.

    ![앱 쪽의 설정 섹션](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_000.png)

8. **보안 정책 -> 사용자 인증** 아래의 **Single Sign On** 링크를 클릭합니다.

    ![앱 쪽의 보안 정책](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_001.png)

9. Hello 메타 데이터 URL 링크 toodownload hello 메타 데이터 문서를 클릭 합니다.

    ![서비스 공급자 메타데이터 URL](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_002.png)
    
    * 확인 **entityID** 일치 **식별자** hello에 **MOVEit 전송-Azure AD 통합 도메인 및 Url** 섹션.
    * 확인 **AssertionConsumerService** 위치 URL 일치 **회신 URL** hello에 **MOVEit 전송-Azure AD 통합 도메인 및 Url** 섹션.
    
    ![앱 쪽에서 Single Sign-On 구성](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_007.png)

10. 클릭 **Id 공급자 추가** tooadd 새 페더레이션 Id 공급자 단추입니다.

    ![ID 공급자 추가](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_003.png)

11. 클릭 **찾아보기...**  tooselect hello 메타 데이터 파일을 Azure 포털에서 다운로드 한 다음 클릭 **Id 공급자 추가** tooupload hello 파일을 다운로드 합니다.

    ![SAML ID 공급자](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_004.png)

12. 선택 "**예**"으로 **Enabled** hello에 **페더레이션 Id 공급자 설정 편집...**  페이지 클릭 하 여 **저장**합니다.

    ![페더레이션 ID 공급자 설정](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_005.png)

13. Hello에 **편집 페더레이션 Id 공급자 사용자 설정을** 페이지 hello 다음 작업을 수행 합니다.
    
    ![페더레이션 ID 공급자 설정 편집](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_006.png)
    
    a. **로그인 이름**으로 **SAML NameID**를 선택합니다.
    
    b. 선택 **다른** 으로 **전체 이름을** 및 hello **특성 이름** textbox hello 값 입력: `http://schemas.microsoft.com/identity/claims/displayname`합니다.
    
    c. 선택 **다른** 으로 **전자 메일** 및 hello **특성 이름** textbox hello 값 입력: `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`합니다.
    
    d. **SignOn에서 계정 자동 만들기**로 **예**를 선택합니다.
    
    e. **저장** 단추를 클릭합니다.

> [!TIP]
> 이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!  Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션. 자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Azure AD 테스트 사용자 만들기

이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.

   ![Azure AD 테스트 사용자 만들기][100]

**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**

1. Hello hello 왼쪽된 창에서 Azure 포털에서에서 클릭 hello **Azure Active Directory** 단추입니다.

    ![hello Azure Active Directory 단추](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_01.png)

2. 사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹**, 클릭 하 고 **모든 사용자가**합니다.

    !["사용자 및 그룹" hello 및 "모든 사용자" 링크](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_02.png)

3. tooopen hello **사용자** 대화 상자를 클릭 **추가** hello hello 맨 **모든 사용자에 게** 대화 상자.

    ![hello 추가 단추](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_03.png)

4. Hello에 **사용자** 대화 상자를 hello 다음 단계를 수행 합니다.

    ![hello 사용자 대화 상자](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_04.png)

    a. Hello에 **이름** 상자에서 입력 **BrittaSimon**합니다.

    b. Hello에 **사용자 이름** 상자의 사용자 Britta Simon의 hello 전자 메일 주소를 입력 합니다.

    c. 선택 hello **암호 표시** 확인란을 선택한 다음 hello에 표시 되는 hello 값 기록 **암호** 상자입니다.

    d. **만들기**를 클릭합니다.
 
### <a name="create-a-moveit-transfer---azure-ad-integration-test-user"></a>MOVEit Transfer - Azure AD 통합 테스트 사용자 만들기

이 섹션의 hello 목표 toocreate Britta Simon MOVEit 전송-Azure AD 통합의에서 라는 사용자를입니다. MOVEit Transfer - Azure AD 통합은 적시에 프로비전을 지원하며 사용하도록 설정되었습니다. 이 섹션에 작업 항목이 없습니다. 새 사용자를 시도 tooaccess MOVEit 전송-아직 존재 하지 않는 경우 Azure AD 통합 하는 동안 만들어집니다.

>[!NOTE]
>Toocontact hello toocreate 사용자를 수동으로 필요한 경우 필요한 [MOVEit 전송-Azure AD 통합 클라이언트 지원 팀](https://community.ipswitch.com/s/support)합니다.

### <a name="assign-hello-azure-ad-test-user"></a>Azure AD hello 테스트 사용자를 할당 합니다.

이 섹션에서는 tooMOVEit 전송-Azure AD 통합 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.

![Hello 사용자 역할 할당][200] 

**tooassign Britta Simon tooMOVEit 전송-Azure AD 통합 hello 다음 단계를 수행 합니다.**

1. Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.

    ![사용자 할당][201] 

2. Hello 응용 프로그램 목록에서 선택 **MOVEit 전송-Azure AD 통합**합니다.

    ![hello MOVEit 전송-hello 응용 프로그램 목록에 연결 된 Azure AD 통합](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_app.png)  

3. Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.

    ![hello "사용자 및 그룹" 링크][202]

4. **추가** 단추를 클릭합니다. 그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.

    ![hello 할당 추가 창][203]

5. **사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.

6. **사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.

7. **할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.
    
### <a name="test-single-sign-on"></a>Single Sign-On 테스트

이 섹션의 hello 목적은 tootest 액세스 패널을 hello 사용 하 여 Azure AD SSO 구성 합니다.

Hello MOVEit 전송-Azure AD 통합 타일을 클릭할 때 자동으로 로그온 tooyour MOVEit 전송-Azure AD 통합 응용 프로그램 액세스 패널 hello에서 가져와야 합니다. 

## <a name="additional-resources"></a>추가 리소스

* [방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와](active-directory-saas-tutorial-list.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_203.png

