---
title: "자습서: Qlik Sense Enterprise와 Azure Active Directory 통합 | Microsoft 문서"
description: "Tooconfigure 단일 로그온 방법에 대해 알아봅니다 Azure Active Directory와 Qlik 의미 엔터프라이즈 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 8c27e340-2b25-47b6-bf1f-438be4c14f93
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: 153edb3f8cd41790d4e9a74f15cfb806e5e9e3b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-qlik-sense-enterprise"></a>자습서: Qlik Sense Enterprise와 Azure Active Directory 통합

이 자습서에 설명 어떻게 toointegrate Qlik 의미 Enterprise와 Azure Active Directory (Azure AD).

Azure AD와 Qlik 의미 엔터프라이즈 통합 이점을 다음 hello 제공:

- Azure ad 액세스 tooQlik 엔터프라이즈 의미를 가진 제어할 수 있습니다.
- Azure AD 계정을 사용 하면 사용자가 tooautomatically get 로그온 tooQlik 의미 Enterprise (Single Sign-on)를 사용할 수 있습니다.
- 하나의 중앙 위치-hello Azure 포털에서 계정을 관리할 수 있습니다.

Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.

## <a name="prerequisites"></a>필수 조건

다음 항목 hello가 필요 tooconfigure Qlik 의미 Enterprise와 Azure AD 통합 합니다.

- Azure AD 구독
- Qlik Sense Enterprise Single Sign-On이 설정된 구독

> [!NOTE]
> 이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.

이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.

- 꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.
- Azure AD 평가판 환경이 없으면 [평가판 제품](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.

## <a name="scenario-description"></a>시나리오 설명
이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다. 이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.

1. Qlik 의미 엔터프라이즈 hello 갤러리 추가
2. Azure AD Single Sign-on 구성 및 테스트

## <a name="adding-qlik-sense-enterprise-from-hello-gallery"></a>Qlik 의미 엔터프라이즈 hello 갤러리 추가
tooconfigure hello와의 통합 Qlik 의미 엔터프라이즈 Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Qlik 의미 엔터프라이즈 tooadd가 필요합니다.

**hello 갤러리에서 Qlik 의미 엔터프라이즈 tooadd hello 다음 단계를 수행 합니다.**

1. Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다. 

    ![hello Azure Active Directory 단추][1]

2. 너무 이동**엔터프라이즈 응용 프로그램**합니다. 이동 하 여 너무**모든 응용 프로그램**합니다.

    ![hello 엔터프라이즈 응용 프로그램 블레이드][2]
    
3. tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.

    ![hello 새 응용 프로그램 단추][3]

4. Hello 검색 상자에 입력 **Qlik 의미 엔터프라이즈**선택, **Qlik 의미 엔터프라이즈** 결과 패널에서 클릭 **추가** tooadd hello 응용 프로그램 단추입니다.

    ![Hello 결과 목록에서 Qlik 의미 Enterprise](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성 및 테스트

이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Qlik Sense Enterprise에서 Azure AD Single Sign-On을 구성하고 테스트합니다.

Single sign on toowork에 대 한 Azure AD는 tooknow Qlik 의미 기업에서 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다. 즉, Azure AD 사용자 및 Qlik 의미 기업의 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.

Qlik 의미 기업에서는 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.

tooconfigure 및 Qlik 의미 Enterprise를 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.

1. **[Azure AD Single Sign-on 구성](#configure-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.
2. **[Azure AD 테스트를 만들고](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.
3. **[Qlik 의미 엔터프라이즈 테스트 사용자 만들기](#create-a-qlik-sense-enterprise-test-user)**  -toohave 사용자의 연결 된 Azure AD toohello 표현인 Qlik 의미 enterprise Britta Simon의 해당 하는 도구입니다.
4. **[Azure AD hello 테스트 사용자를 할당](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.
5. **[Single sign on 테스트](#test-single-sign-on)**  -tooverify 구성 works를 hello 여부.

### <a name="configure-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성

이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 사용 하도록 설정 및 Qlik 의미 엔터프라이즈 응용 프로그램에서 single sign on 구성 합니다.

**Qlik 의미 엔터프라이즈와 Azure AD에서 single sign-on tooconfigure hello 다음 단계를 수행 합니다.**

1. Hello hello에 Azure 포털에서에서 **Qlik 의미 엔터프라이즈** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.

    ![Single Sign-On 구성 링크][4]

2. Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_samlbase.png)

3. Hello에 **Qlik 의미 엔터프라이즈 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.

    ![Qlik Sense Enterprise 도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_url.png)

    a. Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<Qlik Sense Fully Qualifed Hostname>:443//samlauthn/`
    
    > [!NOTE]
    > Note hello 뒤에이 URI의 hello 끝에 슬래시가 있습니다. 필수입니다.
    
    b. Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:
    | |
    |--|
    | `https://<Qlik Sense Fully Qualifed Hostname>.qlikpoc.com`|
    | `https://<Qlik Sense Fully Qualifed Hostname>.qliksense.com`|

    > [!NOTE] 
    > 이러한 값은 실제 값이 아닙니다. 이러한 값은 실제 로그온 URL과 식별자,이 자습서 또는 연락처의 뒷부분에 설명 된 hello 업데이트 [Qlik 의미 엔터프라이즈 클라이언트 지원 팀](https://www.qlik.com/us/services/support) tooget 이러한 값입니다. 

4. Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello 메타 데이터 파일을 컴퓨터에 저장 합니다.

    ![hello 인증서 다운로드 링크](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_certificate.png) 

5. **저장** 단추를 클릭합니다.

    ![Single Sign-On 구성 저장 단추](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_400.png)

6. 해당 tooQlik 의미 서버를 업로드할 수 있도록 hello 페더레이션 메타 데이터 XML 파일을 준비 합니다.
   
    > [!NOTE]
    > Hello IdP 메타 데이터 toohello Qlik 의미 서버에 업로드 하기 전에 hello가 필요한 지 편집할 toobe tooremove 정보 tooensure 적절 한 작업을 Azure AD 간의 및 서버 Qlik 의미 합니다.
    
    ![QlikSense][qs24]
   
    a. 텍스트 편집기에서 Azure 포털에서 다운로드 한 hello FederationMetaData.xml 파일을 엽니다.
   
    b. Hello 값에 대 한 검색 **RoleDescriptor**합니다.  네 개의 항목(열고 닫는 요소 태그의 두 쌍)이 있습니다.
   
    c. Hello RoleDescriptor 태그와 모든 정보를 중간에 hello 파일에서 삭제 합니다.
   
    d. Hello 파일을 저장 하 고이 문서의 뒷부분에서 사용 하기 위해 근처 유지 합니다.

7. Toohello Qlik 감지 Qlik 관리 콘솔 (QMC) 가상 프록시 구성을 만들 수 있는 사용자로 이동 합니다.

8. Hello QMC hello 클릭 **가상 프록시** 메뉴 항목입니다.
   
    ![QlikSense][qs6] 

9. Hello hello 화면 맨 클릭 hello **새로 만들기** 단추입니다.
   
    ![QlikSense][qs7]

10. hello 가상 프록시 편집 화면이 나타납니다.  Hello에 hello 화면 오른쪽에는 구성 옵션을 표시 하기에 메뉴입니다.
   
    ![QlikSense][qs9]

11. Hello 식별 메뉴 옵션을 선택 하면 hello hello Azure 가상 프록시 구성에 대 한 식별 정보를 입력 합니다.
    
    ![QlikSense][qs8]  
    
    a. hello **설명** 필드는 hello 가상 프록시 구성에 대 한 알기 쉬운 이름.  설명에 대한 값을 입력합니다.
    
    b. hello **접두사** 필드와 Azure AD Single Sign-on tooQlik 의미를 연결 하기 위한 hello 가상 프록시 끝점을 식별 합니다.  이 가상 프록시에 대한 고유한 접두사 이름을 입력합니다.
    
    c. **세션 비활성 제한 시간 (분)** 가상이 프록시를 통한 연결에 대 한 hello 시간 제한입니다.
    
    d. hello **세션 쿠키 헤더 이름** 은 인증을 거친 후 사용자 Qlik 의미 세션은 수신 하는 hello에 대 한 세션 식별자 hello hello 쿠키 이름을 저장 합니다.  이 이름은 고유해야 합니다.

12. 클릭 hello 인증 메뉴 옵션 toomake에 표시 됩니다.  hello 인증 화면이 나타납니다.
    
    ![QlikSense][qs10]
    
    a. hello **익명 액세스 모드** 드롭 다운 결정 하는 경우 익명 사용자에 게 hello 가상 프록시를 통해 Qlik 의미를 액세스할 수 있습니다.  hello 기본 옵션은 익명 사용자 없음.
    
    b. hello **인증 방법** 드롭 다운 결정 hello hello 가상 프록시 인증 체계를 사용 합니다.  SAML hello 드롭 다운 목록에서 선택 합니다.  그 결과 더 많은 옵션이 표시됩니다.
    
    c. Hello에 **SAML 호스트 URI 필드**, 입력된 hello 호스트 이름을 사용자가이 SAML 가상 프록시를 통해 tooaccess Qlik 의미를 입력 합니다.  hello hostname은 Qlik 의미 서버 hello의 hello uri입니다.
    
    d. Hello에 **SAML 엔터티 ID**, hello SAML 호스트 URI 필드에 동일한 값을 입력 하는 hello를 입력 합니다.
    
    e. hello **SAML IdP 메타 데이터** hello의 앞부분에 나오는 편집 hello 파일은 **Azure AD 구성에서 페더레이션 메타 데이터 편집** 섹션.  **Hello IdP 메타 데이터를 업로드 하기 전에 hello가 필요한 지 toobe 편집** tooremove 정보 tooensure Azure AD 간의 적절 한 작업 및 서버 Qlik 의미 합니다.  **Hello 파일에 아직 toobe 편집할 경우 위의 toohello 지침을 참조 하십시오.**  Hello 파일을 편집한 경우 클릭 hello 찾아보기 단추 및 선택 hello 편집 된 메타 데이터 파일 tooupload toohello 가상 프록시 구성.
    
    f. Hello SAML 특성이 나타내는 hello에 대 한 hello 특성 이름이 나 스키마 참조 입력 **UserID** Azure AD toohello Qlik 의미 서버 보냅니다.  스키마 참조 정보는 hello 구성 후 Azure 응용 프로그램 화면에서에서 사용할 수 있습니다.  toouse hello name 특성이 입력 `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`합니다.
    
    g. Hello에 대 한 hello 값을 입력 **사용자 디렉터리** Azure AD 통해 tooQlik 의미 서버를 인증 하는 경우 연결 된 toousers 사용 됩니다.  하드 코드된 값은 **[](대괄호)**로 묶어야 합니다.  hello Azure AD SAML 어설션 전송 특성 toouse이 텍스트 상자에 hello 특성의 hello 이름을 입력 **없이** 대괄호입니다.
    
    h. hello **SAML 서명 알고리즘** 집합 hello hello 가상 프록시 구성에 대 한 서명 하는 서비스 공급자 (이 서버에 있는 사례 Qlik 의미) 인증서입니다.  Qlik 의미 서버 Microsoft Enhanced RSA and AES Cryptographic Provider를 사용 하 여 생성 하는 신뢰할 수 있는 인증서를 사용 하는 경우 hello SAML 서명 알고리즘도 변경**s h A-256**합니다.
    
    i. SAML 특성 매핑 섹션 hello 그룹 보안 규칙에서 사용 하기 위해 전송 toobe tooQlik 감지와 같은 추가 특성을 허용합니다.

13. Hello 클릭 **부하 분산** 메뉴 옵션 toomake 표시 하는 것입니다.  hello 부하 분산 화면이 나타납니다.
    
    ![QlikSense][qs11]

14. Hello 클릭 **새 서버 노드 추가** 단추를 선택 엔진 노드 또는 노드 Qlik 의미 세션 toofor 로드 균형 조정을 위해, 보내고 hello 클릭 **추가** 단추입니다.
    
    ![QlikSense][qs12]

15. 클릭 hello 고급 메뉴 옵션 toomake에 표시 됩니다. hello 고급 화면이 나타납니다.
    
    ![QlikSense][qs13]
    
    hello 호스트 허용 목록을 toohello Qlik 의미 서버를 연결할 때 허용 되는 호스트 이름을 식별 합니다.  **TooQlik 의미 서버에 연결 하는 경우 사용자가 지정 하는 hello 호스트 이름을 입력 하십시오.** hello 호스트 이름에는 hello hello https:// 없는 SAML 호스트 uri hello와 동일한 값입니다.

16. Hello 클릭 **적용** 단추입니다.
    
    ![QlikSense][qs14]

17. 확인 tooaccept hello 경고 메시지를 프록시 연결 된 toohello 가상 프록시를 다시 시작을 클릭 합니다.
    
    ![QlikSense][qs15]

18. Hello hello 화면 오른쪽, hello 관련 된 항목 메뉴가 나타납니다.  Hello 클릭 **프록시** 메뉴 옵션입니다.
    
    ![QlikSense][qs16]

19. hello 프록시 화면이 나타납니다.  Hello 클릭 **링크** 프록시 toohello 가상 프록시 hello 아래쪽 toolink에서 단추입니다.
    
    ![QlikSense][qs17]

20. 이 가상 프록시 연결을 지 원하는 한 hello 클릭 선택 hello 프록시 노드 **링크** 단추입니다.  링크의 경우, 한 후 관련된 프록시 hello 프록시 나열 됩니다.
    
    ![QlikSense][qs18]
  
    ![QlikSense][qs19]

21. 후 약 5 tooten 초 마다 새로 고침 QMC 메시지 hello 표시 됩니다.  Hello 클릭 **새로 고침 QMC** 단추입니다.
    
    ![QlikSense][qs20]

22. Hello QMC 새로 고쳐지면 클릭 hello **가상 프록시** 메뉴 항목입니다. 새 SAML 가상 프록시 항목 hello hello 화면에 hello 테이블에 나열 됩니다.  단일 hello 가상 프록시 항목을 클릭 합니다.
    
    ![QlikSense][qs51]

23. Hello 화면 hello 아래쪽 hello 다운로드 SP 메타 데이터 단추가 활성화 됩니다.  Hello 클릭 **다운로드 SP 메타 데이터** 단추 toosave hello 메타 데이터 tooa 파일입니다.
    
    ![QlikSense][qs52]

24. 열기 hello sp 메타 데이터 파일입니다.  Hello 관찰 **entityID** 항목과 hello **AssertionConsumerService** 항목입니다.  이러한 값은 해당 toohello **식별자** 및 hello **로그온 URL** hello Azure AD 응용 프로그램 구성에서 합니다. Hello에 이러한 값을 붙여 넣습니다. **Qlik 의미 엔터프라이즈 도메인 및 Url** hello Azure AD 응용 프로그램 구성 하지, 일치 하 다음 hello Azure AD 앱 구성 마법사에서 대체 해야 하는 경우에 섹션입니다.
    
    ![QlikSense][qs53]

> [!TIP]
> 이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!  Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션. 자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Azure AD 테스트 사용자 만들기
이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.

![Azure AD 테스트 사용자 만들기][100]

**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**

1. Hello hello 왼쪽된 창에서 Azure 포털에서에서 클릭 hello **Azure Active Directory** 단추입니다.

   ![hello Azure Active Directory 단추](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_01.png)

2. 사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹**, 클릭 하 고 **모든 사용자가**합니다.

   !["사용자 및 그룹" hello 및 "모든 사용자" 링크](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_02.png)

3. tooopen hello **사용자** 대화 상자를 클릭 **추가** hello hello 맨 **모든 사용자에 게** 대화 상자.

   ![hello 추가 단추](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_03.png)

4. Hello에 **사용자** 대화 상자를 hello 다음 단계를 수행 합니다.

   ![hello 사용자 대화 상자](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_04.png)

   a. Hello에 **이름** 상자에서 입력 **BrittaSimon**합니다.

   b. Hello에 **사용자 이름** 상자의 사용자 Britta Simon의 hello 전자 메일 주소를 입력 합니다.

   c. 선택 hello **암호 표시** 확인란을 선택한 다음 hello에 표시 되는 hello 값 기록 **암호** 상자입니다.

   d. **만들기**를 클릭합니다.
 
### <a name="create-a-qlik-sense-enterprise-test-user"></a>Qlik Sense Enterprise 테스트 사용자 만들기

이 섹션에서는 Qlik Sense Enterprise에서 Britta Simon이라는 사용자를 만듭니다. 작업할 [Qlik 의미 엔터프라이즈 클라이언트 지원 팀](https://www.qlik.com/us/services/support) hello 사용자 hello Qlik 감지 엔터프라이즈 플랫폼을 추가할 수 있습니다. Single Sign-On을 사용하려면 먼저 사용자를 만들고 활성화해야 합니다. 

### <a name="assign-hello-azure-ad-test-user"></a>Azure AD hello 테스트 사용자를 할당 합니다.

이 섹션에서는 액세스 tooQlik 엔터프라이즈 의미를 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.

![Hello 사용자 역할 할당][200] 

**tooassign Britta Simon tooQlik 의미 엔터프라이즈 hello 다음 단계를 수행 합니다.**

1. Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.

    ![사용자 할당][201] 

2. Hello 응용 프로그램 목록에서 선택 **Qlik 의미 엔터프라이즈**합니다.

    ![hello 응용 프로그램 목록에서 hello Qlik 감지 Enterprise 링크](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_app.png)  

3. Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.

    ![hello "사용자 및 그룹" 링크][202]

4. **추가** 단추를 클릭합니다. 그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.

    ![hello 할당 추가 창][203]

5. **사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.

6. **사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.

7. **할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.
    
### <a name="test-single-sign-on"></a>Single Sign-On 테스트

이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.

Hello 액세스 패널에서에서 hello Qlik 감지 Enterprise 타일을 클릭할 때 자동으로 로그온 tooyour Qlik 감지 엔터프라이즈 응용 프로그램을 구해야 합니다. 

## <a name="additional-resources"></a>추가 리소스

* [방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와](active-directory-saas-tutorial-list.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_203.png

[qs6]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_06.png
[qs7]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_07.png
[qs8]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_08.png
[qs9]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_09.png
[qs10]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_10.png
[qs11]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_11.png
[qs12]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_12.png
[qs13]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_13.png
[qs14]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_14.png
[qs15]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_15.png
[qs16]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_16.png
[qs17]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_17.png
[qs18]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_18.png
[qs19]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_19.png
[qs20]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_20.png
[qs24]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_24.png
[qs51]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_51.png
[qs52]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_52.png
[qs53]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_53.png

