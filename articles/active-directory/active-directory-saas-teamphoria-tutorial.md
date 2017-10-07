---
title: "자습서: Teamphoria와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Teamphoria 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d569c705-6f0f-4ec1-b485-ba82526b5d32
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: jeedes
ms.openlocfilehash: f32be9742b76f7fe464036dadc108c62e4a787a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-teamphoria"></a>자습서: Teamphoria와 Azure Active Directory 통합

이 자습서에 설명 어떻게 toointegrate Teamphoria Azure Active directory (Azure AD).

다음 이점을 hello로 제공 Teamphoria Azure AD와 통합:

- 액세스 tooTeamphoria을 지닌 Azure AD에서 제어할 수 있습니다.
- 프로그램 사용자 tooautomatically get 로그온 tooTeamphoria (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.
- 하나의 중앙 위치-hello Azure 관리 포털에서에서 사용자 계정을 관리할 수 있습니다.

Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.

<!--## Overview

tooenable single sign-on with Teamphoria, it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in Teamphoria.

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a>필수 조건

다음 항목 hello가 필요 tooconfigure Teamphoria와 Azure AD 통합 합니다.

- Azure AD 구독
- Teamphoria Single Sign-On이 설정된 구독

> [!NOTE]
> 이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.

이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.

- 꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.
- Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.

## <a name="scenario-description"></a>시나리오 설명
이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다. 이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.

1. Teamphoria는 hello 갤러리 추가
2. Azure AD Single Sign-on 구성 및 테스트

## <a name="adding-teamphoria-from-hello-gallery"></a>Teamphoria는 hello 갤러리 추가
tooconfigure hello와의 통합 Teamphoria Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Teamphoria tooadd가 필요합니다.

**hello 갤러리에서 Teamphoria tooadd hello 다음 단계를 수행 합니다.**

1. Hello에  **[Azure 관리 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다. 

    ![Active Directory][1]

2. 너무 이동**엔터프라이즈 응용 프로그램**합니다. 이동 하 여 너무**모든 응용 프로그램**합니다.

    ![응용 프로그램][2]
    
3. 클릭 **추가** hello 대화의 hello 위쪽에 단추입니다.

    ![응용 프로그램][3]

4. Hello 검색 상자에 입력 **Teamphoria**합니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_search.png)

5. Hello 결과 패널에서 선택 **Teamphoria**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Azure AD Single Sign-on 구성 및 테스트
이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Teamphoria에서 Azure AD Single Sign-On을 구성하고 테스트합니다.

Single sign on toowork에 대 한 Azure AD는 tooknow Teamphoria에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다. 즉, Azure AD 사용자 및 Teamphoria에 hello 관련된 사용자 간 링크 관계를 설정할 toobe가 필요 합니다.

Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** Teamphoria에 합니다.

tooconfigure 및 Teamphoria 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.

1. **[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.
2. **[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.
3. **[Teamphoria 테스트 사용자 만들기](#creating-a-teamphoria-test-user)**  -toohave Britta Simon 그녀의 연결 된 Azure AD toohello 표현인 Teamphoria에 해당 하는 도구입니다.
4. **[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.
5. **[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성

이 섹션에서는 Azure AD에서 single sign-on hello Azure 관리 포털에서 설정 및 Teamphoria 응용 프로그램에서 single sign on 구성 합니다.

**tooconfigure Azure AD single sign on, Teamphoria와 hello 다음 단계를 수행 합니다.**

1. Hello에 hello Azure 관리 포털에서 **Teamphoria** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.

    ![Single Sign-on 구성][4]

2. Hello에 **Single sign on** 대화 상자에서으로 **모드** 선택 **SAML 기반 로그온** tooenable single sign-on입니다.
 
    ![Single Sign-on 구성](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_samlbase.png)

3. Hello에 **Teamphoria 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_url.png)

    a. Hello에 **로그온 URL** 텍스트 패턴 hello를 사용 하 여 hello URL 입력:`https://<sub-domain>.teamphoria.com/login`  

    > [!NOTE] 
    > 이러한 없는지 hello 실제 값 note 하십시오. Tooupdate hello로 이러한 값이 있는 실제 로그온 URL입니다. 연락처 [Teamphoria 클라이언트 지원 팀](https://www.teamphoria.com/) tooget hello 로그온 URL입니다. 

4. Hello에 **SAML 서명 인증서** 섹션에서 클릭 **인증서 (Base64)** hello 인증서 컴퓨터에 저장 합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_certificate.png) 

5. **저장** 단추를 클릭합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-teamphoria-tutorial/tutorial_general_400.png)

6. Hello에 **Teamphoria 구성** 섹션에서 클릭 **구성 Teamphoria** tooopen **sign on 구성** 창. 복사 hello **SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**

    ![Single Sign-on 구성](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_configure.png) 

7. tooconfigure single sign on에서 **Teamphoria** 쪽, 관리자 권한으로 로그인 tooyour Teamphoria 응용 프로그램입니다.

8. 너무 이동**관리 설정** hello hello 구성 탭에서 클릭 하 고 hello 왼쪽된 도구 모음에서 옵션 **SINGLE SIGN-ON** tooopen hello SSO 구성 창.

    ![Single Sign-on 구성](./media/active-directory-saas-teamphoria-tutorial/admin_sso_configure.png)

9. 클릭 **새 ID 공급자 추가** SSO에 대 한 hello 설정을 추가 하기 위한 hello tooopen hello 양식을 오른쪽 위 모서리에서 옵션입니다.

    ![Single Sign-on 구성](./media/active-directory-saas-teamphoria-tutorial/add_new_identity_provider.png)

10. 아래에서 설명 된 대로 hello 필드에 대 한 hello 세부 정보 입력

    ![Single Sign-on 구성](./media/active-directory-saas-teamphoria-tutorial/Teamphoria_sso_save.png)

    a. **표시 이름** : hello 관리 페이지의 hello 플러그 인의 hello 표시 이름을 입력 합니다.

    b. **단추 이름** : SSO를 통한 로그인에 대 한 hello 로그인 페이지에 표시 하는 hello 탭의 hello 이름입니다.

    c. **인증서** : 열기 hello 인증서 이전에 다운로드 한 hello hello의 복사 hello 내용 메모장에서 Azure 포털에서에서 동일 하 고 여기 hello 상자에 붙여 넣습니다.

    d. **진입점** : 붙여넣기 hello **SAML Single Sign-on 서비스 URL** 이전 양식 hello Azure 포털을 복사 합니다.

    e. Hello 옵션을 너무 전환**ON** 을 클릭할 **저장**합니다. 

<!--### Next steps

tooensure users can sign-in tooTeamphoria after it has been configured toouse Azure Active Directory, review hello following tasks and topics:

- User accounts must be pre-provisioned into Teamphoria prior toosign-in. tooset this up, see Provisioning.
 
- Users must be assigned access tooTeamphoria in Azure AD toosign-in. tooassign users, see Users.
 
- tooconfigure access polices for Teamphoria users, see Access Policies.
 
- For additional information on deploying single sign-on toousers, see [this article](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a>Azure AD 테스트 사용자 만들기
이 섹션의 hello 목표 toocreate Britta Simon 라는 hello Azure 관리 포털에서 테스트 사용자를입니다.

![Azure AD 사용자 만들기][100]

**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**

1. Hello에 **Azure 관리 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_01.png) 

2. 너무 이동**사용자 및 그룹** 클릭 **모든 사용자에 게** 사용자 toodisplay hello 목록입니다.
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_02.png) 

3. Hello 대화의 hello 위쪽 클릭 **추가** tooopen hello **사용자** 대화 상자.
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_03.png) 

4. Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_04.png) 

    a. Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.

    b. Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.

    c. 선택 **암호 표시** hello hello 값 기록 **암호**합니다.

    d. **만들기**를 클릭합니다.
 
### <a name="creating-a-teamphoria-test-user"></a>Teamphoria 테스트 사용자 만들기

Tooenable Azure AD 사용자가 toolog Teamphoria로 주문 하 고에 Teamphoria에 이들 프로 비전 해야 합니다. Hello Teamphoria의 경우에서 프로 비전은 수동 작업입니다.

**사용자 계정 수행 tooprovision hello 다음 단계:**

1. 관리자 권한으로 Teamphoria 회사 사이트 tooyour에 로그인 합니다.

2. 클릭 **관리자** hello 왼쪽된 도구 모음과 hello에서 설정이 **관리** 탭을 클릭 하 여 **사용자** tooopen hello admin 사용자가 페이지를 합니다.

    ![직원 추가](./media/active-directory-saas-teamphoria-tutorial/admin_manage_users.png)

3. Hello 클릭 **수동 초대** 옵션입니다.

    ![피플 초대](./media/active-directory-saas-teamphoria-tutorial/admin_manage_add_users.png)  

4. 이 페이지에서 다음 작업을 수행합니다. 
    
    ![피플 초대](./media/active-directory-saas-teamphoria-tutorial/manual_user_invite.png)  

    a. Hello에 **전자 메일 주소** textbox hello **전자 메일 주소** BrittaSimon입니다.

    b. Hello에 **이름** 텍스트 상자에 **Britta**합니다.

    c. Hello에 **성** 텍스트 상자에 **Simon**합니다.

    d. **1 사용자 초대**를 클릭합니다. 사용자가 tooaccept hello 초대 tooget hello 시스템에서 생성 해야 합니다.

### <a name="assigning-hello-azure-ad-test-user"></a>Azure AD hello 테스트 사용자를 할당합니다.

이 섹션에서는 액세스 tooTeamphoria 그녀의 권한을 부여 하 여 Azure single sign on Britta Simon toouse를 사용 합니다.

![사용자 할당][200] 

**tooassign Britta Simon tooTeamphoria hello 다음 단계를 수행 합니다.**

1. Hello Azure 관리 포털에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.

    ![사용자 할당][201] 

2. Hello 응용 프로그램 목록에서 선택 **Teamphoria**합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_app.png) 

3. Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.

    ![사용자 할당][202] 

4. **추가** 단추를 클릭합니다. 그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.

    ![사용자 할당][203]

5. **사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.

6. **사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.

7. **할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.
    
### <a name="testing-single-sign-on"></a>Single Sign-On 테스트

이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.

Single Sign-On 설정을 테스트하려면 액세스 패널을 엽니다. 액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](https://msdn.microsoft.com/library/dn308586)를 참조하세요. 

## <a name="additional-resources"></a>추가 리소스

* [방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와](active-directory-saas-tutorial-list.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_203.png

