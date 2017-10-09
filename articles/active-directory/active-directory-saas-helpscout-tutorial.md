---
title: "자습서: Help Scout와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 도움말 Scout 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0aad9910-0bc1-4394-9f73-267cf39973ab
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: jeedes
ms.openlocfilehash: 58edd140eb1eb5980796ca743b5f7acd891729a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-help-scout"></a>자습서: Help Scout와 Azure Active Directory 통합

이 자습서에서는 toointegrate 도움말 Azure Active Directory (Azure AD)와 정찰 하는 방법을 배웁니다.

도움말 Scout를 Azure AD와 통합에서 혜택을 따라 hello를 발생할 수 있습니다.

- Azure AD에서 액세스 tooHelp Scout를가지고 있는 사람을 제어할 수 있습니다.
- Single sign on 및 사용자의 Azure AD 계정을 사용 하 여 사용자가 tooHelp Scout 프로그램에 자동으로 서명할 수 있습니다.
- 프로그램을 하나의 중앙 위치에 hello Azure 포털에서 계정을 관리할 수 있습니다.

참조로 Azure AD와 saas () 응용 프로그램 통합 소프트웨어에 대해 자세히 toolearn [응용 프로그램 액세스 및 single sign on Azure Active directory 란?](active-directory-appssoaccess-whatis.md)합니다.

## <a name="prerequisites"></a>필수 조건

Azure AD와 통합 된 도움말 Scout을 tooset, 다음 항목 hello가 필요 합니다.

- Azure AD 구독
- Single Sign-On이 설정된 Help Scout 구독 

> [!NOTE]
> 이 자습서에서는 hello 단계를 테스트 하는 경우는 프로덕션 환경에서 테스트할 하지 있습니다 하는 것이 좋습니다.

이 자습서에서는 hello 단계를 테스트 하기 위한 권장 사항:

- 꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.
- Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.

## <a name="scenario-description"></a>시나리오 설명
이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다. 

이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.

1. Hello 갤러리에서 Scout 도움말을 추가 합니다.
2. Azure AD Single Sign-On 설정 및 테스트

## <a name="add-help-scout-from-hello-gallery"></a>도움말 Scout hello 갤러리 추가
hello와 도움말 Scout hello 갤러리에서 Azure AD와의 통합을 tooset 도움말 Scout tooyour 목록은 관리 되는 SaaS 앱을 추가 합니다.

tooadd hello 갤러리에서 Scout 도움말:

1. Hello에 [Azure 포털](https://portal.azure.com)hello 왼쪽된 메뉴에서 선택 **Azure Active Directory**합니다. 

    ![hello Azure Active Directory 단추][1]

2. **엔터프라이즈 응용 프로그램**을 선택한 다음 **모든 응용 프로그램**을 선택합니다.

    ![hello 엔터프라이즈 응용 프로그램 페이지][2]
    
3. 새 응용 프로그램을 tooadd 선택 **새 응용 프로그램**합니다.

    ![hello 새 응용 프로그램 단추][3]

4. Hello 검색 상자에 입력 **도움말 Scout**합니다. Hello 검색 결과에서 선택 **도움말 Scout**를 선택한 후 **추가**합니다.

    ![Hello 결과 목록에서 Scout 도움말](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_addfromgallery.png)

## <a name="set-up-and-test-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 설정 및 테스트

이 섹션에서는 *Britta Simon*이라는 테스트 사용자를 기반으로 Help Scout에서 Azure AD Single Sign-On을 설정하고 테스트합니다.

Azure AD single sign on toowork에 대 한 도움말 Scout tooknow hello Azure AD에 관련 사용자는 필요 합니다. Azure AD 사용자 및 도움말 Scout에 hello 관련된 사용자 간 링크 관계를 설정 해야 합니다.

tooestablish hello에 대 한 관계에 Scout 도움말 링크 **Username**, hello hello 값을 할당 **사용자 이름** Azure AD에서 합니다.

tooconfigure 및 도움말 정찰, 작업을 수행 하는 전체 hello 사용 하 여 Azure AD에서 single sign-on 테스트:

1. [Azure AD Single Sign-On 설정](#set-up-azure-ad-single-sign-on). 이 기능은 사용자 toouse를 설정합니다.
2. [Azure AD 테스트 사용자 만들기](#create-an-azure-ad-test-user). 테스트 Azure AD single sign on hello 사용자 Britta Simon와 합니다.
3. [Help Scout 테스트 사용자 만들기](#create-a-help-scout-test-user) 연결 된 toohello hello 사용자의 Azure AD 표현 되는 데 도움이 Scout에 Britta Simon의 해당 하는 도구를 만듭니다.
4. [Azure AD hello 테스트 사용자를 할당](#assign-the-azure-ad-test-user)합니다. Azure AD에서 single sign-on Britta Simon toouse를 설정합니다.
5. [Single Sign-On 테스트](#test-single-sign-on). 해당 hello 구성이 작동을 확인 합니다.

### <a name="set-up-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 설정

이 섹션에서는 Azure AD single sign-on을 hello Azure 포털에서에서 설정 합니다. 그런 다음 Help Scout 응용 프로그램에서 Single Sign-On을 설정합니다.

Azure AD single sign-on을 도움말 Scout와 tooset:

1. Hello hello에 Azure 포털에서에서 **도움말 Scout** 응용 프로그램 통합 페이지에서 선택 **Single sign on**합니다.
 
    ![Single Sign-On 설정 링크][4]

2. Hello에 **Single sign on** 페이지에 대 한 **모드**선택, **SAML 기반 로그온**합니다.
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_samlbase.png)

3. 아래 **도움말 Scout 도메인 및 Url**IDP 시작 모드에서는 단계를 수행 하는 전체 hello tooset hello 응용 프로그램을 설치 하려는 경우:

    1. Hello에 **식별자** 상자에 URL hello 패턴을 입력 합니다.`urn:auth0:helpscout:<instancename>`

    2. Hello에 **회신 URL** 상자에 URL hello 패턴을 입력 합니다.`https://helpscout.auth0.com/login/callback?connection=<instancename>`

    ![Help Scout 도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_url.png)

4. SP에서 시작한 모드로 tooset hello 응용 프로그램을 설치 하려는 경우 선택 hello **고급 URL 설정 표시** 확인란을 선택한 수행가 다음를 hello 다음:

    * Hello에 **로그온 URL** 상자 형식에 따라 hello에 하는 URL을 입력 합니다.`https://secure.helpscout.net/members/login/`

    ![Help Scout 도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_url1.png)
 
    > [!NOTE] 
    > 이러한 Url hello 값 데모 목적 으로만 사용 됩니다. Hello 실제 식별자 URL 및 회신 URL hello 값으로 업데이트 합니다. 이러한 값에 게 문의 tooget [Scout 도움말 지원 팀](mailto:help@helpscout.com)합니다. 

5. 아래 **SAML 서명 인증서**선택, **메타 데이터 XML**, hello 메타 데이터 파일을 컴퓨터에 저장 합니다.

    ![hello 인증서 다운로드 링크](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_certificate.png) 

6. **저장**을 선택합니다.

    ![Single Sign-On 구성 저장 단추](./media/active-directory-saas-helpscout-tutorial/tutorial_general_400.png)
    
7. 단일을 tooset 로그온 hello 도움말 Scout 쪽, 송신 hello 다운로드 한 메타 데이터 XML 파일 toohello [Scout 도움말 지원 팀](mailto:help@helpscout.com)합니다. hello Scout 도움말 지원 팀 hello SAML single sign on 연결 양쪽 모두 올바르게 설정 되도록이 설정을 적용 합니다.

> [!TIP]
> Hello에이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)응용 프로그램을 설정 하는 반면,! 선택 하 여 hello 앱을 추가한 후 **Active Directory** > **엔터프라이즈 응용 프로그램**선택, hello **Single Sign On** 탭 합니다. Hello에 포함 된 hello 설명서에 액세스할 수 있습니다 **구성** 섹션 hello hello 페이지 맨 아래에 있습니다. 자세한 내용은 [Azure AD 포함 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)를 참조하세요.

### <a name="create-an-azure-ad-test-user"></a>Azure AD 테스트 사용자 만들기

Hello Azure 포털에서에서이 섹션에서는 Britta Simon 이라는 테스트 사용자를 만듭니다.

![Azure AD 테스트 사용자 만들기][100]

Azure AD에서 테스트 사용자 toocreate:

1. Hello hello 왼쪽된 메뉴에 Azure 포털에서에서 선택 **Azure Active Directory**합니다.

    ![hello Azure Active Directory 단추](./media/active-directory-saas-helpscout-tutorial/create_aaduser_01.png)

2. 사용자 선택 toodisplay hello 목록 **사용자 및 그룹**, 선택한 후 **모든 사용자에 게**합니다.

    ![사용자 및 그룹 선택 및 모든 사용자 선택](./media/active-directory-saas-helpscout-tutorial/create_aaduser_02.png)

3. tooopen hello **사용자** hello 위쪽 hello에 대화 상자에서 **모든 사용자에 게** 페이지에서 **추가**합니다.

    ![hello 추가 단추](./media/active-directory-saas-helpscout-tutorial/create_aaduser_03.png)

4. Hello에 **사용자** 대화 상자에서 다음 단계 완료 hello:

    1. Hello에 **이름** 상자에 입력 **BrittaSimon**합니다.

    2. Hello에 **사용자 이름** 상자에 사용자 Britta Simon의 hello 전자 메일 주소를 입력 합니다.

    3. 선택 hello **암호 표시** 확인란을 선택한 다음 hello에 표시 되는 hello 값 기록 **암호** 상자입니다.

    4. **만들기**를 선택합니다.

        ![hello 사용자 대화 상자](./media/active-directory-saas-helpscout-tutorial/create_aaduser_04.png)

 
### <a name="create-a-help-scout-test-user"></a>Help Scout 테스트 사용자 만들기

이 섹션의 hello 목표 toocreate Britta Simon Scout 도움말의 라는 사용자를입니다. Help Scout는 JIT(Just-In-Time) 프로비전을 지원하며 이 기능은 기본적으로 설정됩니다.

이 섹션에는 액션 또는 작업 toocomplete 없습니다. 사용자 도움말 Scout에 존재 하지 않으면 새 tooaccess Scout 도움말을 시도할 때 만들어집니다.

### <a name="assign-hello-azure-ad-test-user"></a>Azure AD hello 테스트 사용자를 할당 합니다.

이 섹션에서는 hello 사용자 계정 액세스 tooHelp Scout 권한을 부여 하 여 toouse Azure AD에서 single sign-on hello 사용자 Britta Simon를 허용 합니다.

![Hello 사용자 역할 할당][200] 

tooassign Britta Simon tooHelp Scout:

1. Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 고 toohello 디렉터리 보기를 이동 하십시오. **엔터프라이즈 응용 프로그램**을 선택한 다음 **모든 응용 프로그램**을 선택합니다.

    ![사용자 할당][201] 

2. Hello 응용 프로그램 목록에서 선택 **도움말 Scout**합니다.

    ![hello 응용 프로그램 목록에서 hello Scout 도움말 링크](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_app.png)  

3. Hello 왼쪽된 메뉴에서 선택 **사용자 및 그룹**합니다.

    ![hello 사용자 및 그룹 링크][202]

4. **추가**를 선택합니다. 그런 다음 hello **할당 추가** 페이지에서 **사용자 및 그룹**합니다.

    ![hello 할당 추가 창][203]

5. Hello에 **사용자 및 그룹** 페이지의 사용자를 hello 목록 **Britta Simon**합니다.

6. Hello에 **사용자 및 그룹** 페이지에서 **선택**합니다.

7. Hello에 **할당 추가** 페이지에서 **할당**합니다.
    
### <a name="test-single-sign-on"></a>Single Sign-On 테스트

이 섹션에서는 hello 액세스 패널을 사용 하 여 Azure AD single sign on 구성을 테스트 합니다.

Hello 액세스 패널에서 hello 도움말 Scout 타일을 선택 하면 해야 자동으로 로그인 됩니다 tooyour 도움말 Scout 응용 프로그램입니다.

액세스 패널에 대 한 자세한 내용은 참조 [toohello 액세스 패널 소개](active-directory-saas-access-panel-introduction.md)합니다. 

## <a name="additional-resources"></a>추가 리소스

* [방법에 대 한 자습서 목록 toointegrate SaaS 앱 Azure Active Directory와](active-directory-saas-tutorial-list.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_203.png

