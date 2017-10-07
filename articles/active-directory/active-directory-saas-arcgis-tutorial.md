---
title: "자습서: ArcGIS Online과 Azure Active Directory 통합 | Microsoft Docs"
description: "단일 로그온 tooconfigure 방법을 알아보려면 Azure Active Directory와 ArcGIS Online 합니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a9e132a4-29e7-48bf-beb9-4148e617c8a9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: f3dd55d798cf3256fb2758e011f33946baa405ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-arcgis-online"></a>자습서: ArcGIS Online과 Azure Active Directory 통합

이 자습서에 설명 어떻게 toointegrate ArcGIS에서 온라인으로 Azure Active Directory (Azure AD).

Azure AD와 ArcGIS 온라인 통합 이점을 다음 hello 제공:

- 온라인 액세스 tooArcGIS을 지닌 Azure AD에서 제어할 수 있습니다.
- 프로그램 사용자 tooautomatically get 로그온 tooArcGIS 온라인 (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.
- 하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.

Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.

<!--## Overview

tooenable single sign-on with ArcGIS Online, it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in ArcGIS Online.

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a>필수 조건

ArcGIS 온라인와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.

- Azure AD 구독
- ArcGIS Online Single Sign-On이 설정된 구독

> [!NOTE]
> 이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.

이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.

- 꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.
- Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.

## <a name="scenario-description"></a>시나리오 설명
이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다. 이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.

1. ArcGIS 온라인 hello 갤러리 추가
2. Azure AD Single Sign-on 구성 및 테스트

## <a name="adding-arcgis-online-from-hello-gallery"></a>ArcGIS 온라인 hello 갤러리 추가
tooconfigure hello와의 통합 ArcGIS 온라인 Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 ArcGIS 온라인 tooadd가 필요합니다.

**ArcGIS 온라인 hello 갤러리에서 tooadd hello 다음 단계를 수행 합니다.**

1. Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다. 

    ![Active Directory][1]

2. 너무 이동**엔터프라이즈 응용 프로그램**합니다. 이동 하 여 너무**모든 응용 프로그램**합니다.

    ![응용 프로그램][2]
    
3. 클릭 **새 응용 프로그램** hello 대화 tooadd 새 응용 프로그램의 hello 맨 위의 단추를 합니다.

    ![응용 프로그램][3]

4. Hello 검색 상자에 입력 **ArcGIS 온라인**합니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_search.png)

5. Hello 결과 패널에서 선택 **ArcGIS 온라인**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Azure AD Single Sign-on 구성 및 테스트
이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 ArcGIS Online에서 Azure AD Single Sign-On을 구성하고 테스트합니다.

Single sign on toowork에 대 한 Azure AD는 tooknow ArcGIS 온라인에서 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다. 즉, Azure AD 사용자와 ArcGIS 온라인의 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.

Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** ArcGIS 온라인에서 합니다.

tooconfigure 및 온라인 ArcGIS를 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.

1. **[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.
2. **[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.
3. **[ArcGIS 온라인 테스트 사용자를 만들려면](#creating-an-arcgis-online-test-user)**  -toohave Britta Simon ArcGIS 온라인 표현인 연결 된 toohello Azure AD의 사용자에 해당 하는 도구입니다.
4. **[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.
5. **[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성

이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 ArcGIS 온라인 응용 프로그램에서 single sign on 구성 합니다.

**tooconfigure Azure AD single sign on ArcGIS Online과 hello 다음 단계를 수행 합니다.**

1. Hello hello에 Azure 포털에서에서 **ArcGIS 온라인** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.

    ![Single Sign-on 구성][4]

2. Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.
 
    ![Single Sign-on 구성](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_samlbase.png)

3. Hello에 **ArcGIS 온라인 도메인 및 Url** 섹션에서 단계 다음에 나오는 hello 수행:

    ![Single Sign-on 구성](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_url.png)

    Hello에 **로그온 URL** hello 패턴을 사용 하 여 형식 hello 값 텍스트 상자:`https://<company>.maps.arcgis.com`

    > [!NOTE] 
    > 이 값은 실제 hello 되지 않습니다. Hello로이 값을 업데이트 합니다. 실제 로그온 URL입니다. 연락처 [ArcGIS 온라인 클라이언트 지원 팀](http://support.esri.com/) tooget이이 값입니다. 

4. Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello XML 파일을 컴퓨터에 저장 합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_certificate.png) 

5. **저장** 단추를 클릭합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-arcgis-tutorial/tutorial_general_400.png)

6. 다른 웹 브라우저 창에서 ArcGIS 회사 사이트에 관리자로 로그인합니다.

7. **설정 편집**을 클릭합니다.

    ![설정 편집](./media/active-directory-saas-arcgis-tutorial/ic784742.png "설정 편집")

8. **보안**을 클릭합니다.

    ![보안](./media/active-directory-saas-arcgis-tutorial/ic784743.png "보안")

9. **회사 로그인**에서 **ID 공급자 설정**을 클릭합니다.

    ![회사 로그인](./media/active-directory-saas-arcgis-tutorial/ic784744.png "회사 로그인")

10. Hello에 **Id 공급자 설정** 구성 페이지를 hello 다음 단계를 수행 합니다.
   
    ![ID 공급자 설정](./media/active-directory-saas-arcgis-tutorial/ic784745.png "ID 공급자 설정")
   
    a. Hello에 **이름** textbox 조직 이름을 입력 합니다.

    b. 에 대 한 **hello 엔터프라이즈 Id 공급자에 대 한 메타 데이터를 사용 하 여 제공 됩니다**선택, **A 파일**합니다.

    c. tooupload 다운로드 한 메타 데이터 파일을 클릭 하 여 **파일 선택**합니다.

    d. **ID 공급자 설정**을 클릭합니다.

> [!TIP]
> 이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!  Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션. 자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)


### <a name="creating-an-azure-ad-test-user"></a>Azure AD 테스트 사용자 만들기
이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.

![Azure AD 사용자 만들기][100]

**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**

1. Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-arcgis-tutorial/create_aaduser_01.png) 

2. 너무 이동**사용자 및 그룹** 클릭 **모든 사용자에 게** 사용자 toodisplay hello 목록입니다.
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-arcgis-tutorial/create_aaduser_02.png) 

3. Hello 대화의 hello 위쪽 클릭 **추가** tooopen hello **사용자** 대화 상자.
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-arcgis-tutorial/create_aaduser_03.png) 

4. Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-arcgis-tutorial/create_aaduser_04.png) 

    a. Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.

    b. Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** Britta Simon의 합니다.

    c. 선택 **암호 표시** hello hello 값 기록 **암호**합니다.

    d. **만들기**를 클릭합니다.
 
### <a name="creating-an-arcgis-online-test-user"></a>ArcGIS Online 테스트 사용자 만들기

Tooenable Azure AD 사용자가 toolog Online ArcGIS에 주문 하 고에 Online ArcGIS에 이들 프로 비전 해야 합니다.  
Hello 온라인 ArcGIS의 경우에서 프로 비전은 수동 작업입니다.

**tooprovision 사용자 계정을 hello 다음 단계를 수행 합니다.**

1. Tooyour 로그인 **ArcGIS** 테 넌 트입니다.

2. **멤버 초대**를 클릭합니다.
   
    ![멤버 초대](./media/active-directory-saas-arcgis-tutorial/ic784747.png "멤버 초대")

3. **전자 메일을 보내지 않고 멤버를 자동으로 추가**를 선택하고 **다음**을 클릭합니다.
   
    ![멤버를 자동으로 추가](./media/active-directory-saas-arcgis-tutorial/ic784748.png "멤버를 자동으로 추가")

4. Hello에 **멤버** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.
   
     ![추가 및 검토](./media/active-directory-saas-arcgis-tutorial/ic784749.png "추가 및 검토")
    
     a. Hello 입력 **전자 메일**, **이름**, 및 **성** tooprovision 하려는 유효한 AAD 계정의 합니다.
  
     b. **추가 및 검토**를 클릭합니다.
5. 입력 한 다음 클릭 hello 데이터를 검토 **구성원 추가**합니다.
   
    ![멤버 추가](./media/active-directory-saas-arcgis-tutorial/ic784750.png "멤버 추가")
        
    > [!NOTE]
    > hello Azure Active Directory 계정 소유자 전자 메일을 받게 되 고 링크 tooconfirm 자신의 계정을 활성화 되기 전에 수행 됩니다.

### <a name="assigning-hello-azure-ad-test-user"></a>Azure AD hello 테스트 사용자를 할당합니다.

이 섹션에서는 액세스 tooArcGIS 온라인 권한을 부여 하 여 Britta Simon toouse Azure single sign on을 사용 합니다.

![사용자 할당][200] 

**tooassign Britta Simon tooArcGIS 온라인으로 hello 다음 단계를 수행 합니다.**

1. Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.

    ![사용자 할당][201] 

2. Hello 응용 프로그램 목록에서 선택 **ArcGIS 온라인**합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_app.png) 

3. Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.

    ![사용자 할당][202] 

4. **추가** 단추를 클릭합니다. 그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.

    ![사용자 할당][203]

5. **사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.

6. **사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.

7. **할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.
    
### <a name="testing-single-sign-on"></a>Single Sign-On 테스트

이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.

Hello 액세스 패널에서에서 hello ArcGIS 온라인 타일을 클릭할 때 자동으로 로그온 tooyour ArcGIS 온라인 응용 프로그램을 구해야 합니다.
액세스 패널 hello에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.

## <a name="additional-resources"></a>추가 리소스

* [방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와](active-directory-saas-tutorial-list.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_203.png

