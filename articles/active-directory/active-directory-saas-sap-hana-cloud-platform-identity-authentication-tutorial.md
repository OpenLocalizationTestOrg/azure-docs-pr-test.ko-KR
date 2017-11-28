---
title: "자습서: SAP HANA Cloud Platform Identity Authentication과 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 Azure Active Directory 사이 로그온 하 고 SAP HANA 클라우드 플랫폼 Id 인증 하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1c1320d1-7ba4-4b5f-926f-4996b44d9b5e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 2142770779ddb745555b47fc85b5457b573f9506
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana-cloud-platform-identity-authentication"></a><span data-ttu-id="2b67c-103">자습서: SAP HANA Cloud Platform Identity Authentication과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="2b67c-103">Tutorial: Azure Active Directory integration with SAP HANA Cloud Platform Identity Authentication</span></span>

<span data-ttu-id="2b67c-104">이 자습서에 알아봅니다 방법을 toointegrate SAP HANA 클라우드 플랫폼 Id Azure Active Directory (Azure AD) 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-104">In this tutorial, you learn how toointegrate SAP HANA Cloud Platform Identity Authentication with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="2b67c-105">SAP HANA 클라우드 플랫폼 Id 인증 된 프록시 IdP tooaccess SAP 응용 프로그램 주 IdP hello 대로 Azure AD를 사용 하 여으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-105">SAP HANA Cloud Platform Identity Authentication is used as a proxy IdP tooaccess SAP applications using Azure AD as hello main IdP.</span></span>

<span data-ttu-id="2b67c-106">SAP HANA 클라우드 플랫폼 Id 인증 Azure AD와 통합 hello 다음 이점을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-106">Integrating SAP HANA Cloud Platform Identity Authentication with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2b67c-107">Access tooSAP 응용 프로그램을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-107">You can control in Azure AD who has access tooSAP application</span></span>
- <span data-ttu-id="2b67c-108">프로그램 사용자가 tooautomatically get 로그온 tooSAP 응용 프로그램 single sign-on (SSO) 자신의 Azure AD 계정으로 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-108">You can enable your users tooautomatically get signed-on tooSAP applications single sign-on (SSO) with their Azure AD accounts</span></span>
- <span data-ttu-id="2b67c-109">하나의 중앙 위치-hello Azure 클래식 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-109">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="2b67c-110">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-110">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="2b67c-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="2b67c-111">Prerequisites</span></span>

<span data-ttu-id="2b67c-112">SAP HANA 클라우드 플랫폼 Id 인증와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-112">tooconfigure Azure AD integration with SAP HANA Cloud Platform Identity Authentication, you need hello following items:</span></span>

- <span data-ttu-id="2b67c-113">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="2b67c-113">An Azure AD subscription</span></span>
- <span data-ttu-id="2b67c-114">**SAP HANA Cloud Platform Identity Authentication** SSO가 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="2b67c-114">A **SAP HANA Cloud Platform Identity Authentication** SSO enabled subscription</span></span>


>[!NOTE] 
><span data-ttu-id="2b67c-115">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
>

<span data-ttu-id="2b67c-116">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2b67c-117">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-117">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="2b67c-118">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-118">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2b67c-119">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="2b67c-119">Scenario description</span></span>
<span data-ttu-id="2b67c-120">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="2b67c-121">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2b67c-122">Hello 갤러리에서 SAP HANA 클라우드 플랫폼 Id 인증 추가</span><span class="sxs-lookup"><span data-stu-id="2b67c-122">Adding SAP HANA Cloud Platform Identity Authentication from hello gallery</span></span>
2. <span data-ttu-id="2b67c-123">Azure AD SSO 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="2b67c-123">Configuring and testing Azure AD SSO</span></span>

<span data-ttu-id="2b67c-124">Hello 기술 세부 정보를 알아보기 전에 중요 한 toounderstand hello 개념에서 toolook 거 것 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-124">Before diving into hello technical details, it is vital toounderstand hello concepts you're going toolook at.</span></span> <span data-ttu-id="2b67c-125">SAP HANA 클라우드 플랫폼 Id 인증 및 Azure Active Directory 페더레이션 hello tooimplement을 SSO 응용 프로그램 또는 SAP 응용 프로그램 및 SAP HANA 클라우드 플랫폼 Id에 의해 보호 되는 서비스 (IdP)으로 AAD로 보호 되는 서비스 간에 수 있습니다. 인증입니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-125">hello SAP HANA Cloud Platform Identity Authentication and Azure Active Directory federation enables you tooimplement SSO across applications or services protected by AAD (as an IdP) with SAP applications and services protected by SAP HANA Cloud Platform Identity Authentication.</span></span>

<span data-ttu-id="2b67c-126">현재 SAP HANA 클라우드 플랫폼 Id 인증 된 프록시 Id 공급자 tooSAP-응용 프로그램으로 동작합니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-126">Currently, SAP HANA Cloud Platform Identity Authentication acts as a Proxy Identity Provider tooSAP-applications.</span></span> <span data-ttu-id="2b67c-127">이 설치 프로그램에서 Id 공급자를 선행 hello azure Active Directory 역할을 다시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-127">Azure Active Directory in turn acts as hello leading Identity Provider in this setup.</span></span> 

<span data-ttu-id="2b67c-128">다음 다이어그램 hello이를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-128">hello following diagram illustrates this:</span></span>    

![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/architecture-01.png)

<span data-ttu-id="2b67c-130">이 설정을 통해 SAP HANA Cloud Platform Identity Authentication 테넌트가 Azure Active Directory에서 신뢰할 수 있는 응용 프로그램으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-130">With this setup, your SAP HANA Cloud Platform Identity Authentication tenant will be configured as a trusted application in Azure Active Directory.</span></span> 

<span data-ttu-id="2b67c-131">모든 SAP 응용 프로그램 및 서비스 tooprotect이이 방법을 통해 원하는 hello SAP HANA 클라우드 플랫폼 Id 인증 관리 콘솔에서 구성 됩니다!</span><span class="sxs-lookup"><span data-stu-id="2b67c-131">All SAP applications and services you want tooprotect through this way are subsequently configured in hello SAP HANA Cloud Platform Identity Authentication management console!</span></span>

<span data-ttu-id="2b67c-132">(Azure Active Directory에서 것과 반대로 tooconfiguring 권한 부여)으로 이러한 설치에 대 한 요구 tootake 위치에서 SAP HANA 클라우드 플랫폼 Id 인증 서비스 이며 tooSAP 응용 프로그램 액세스 허용을 위한 해당 권한 부여를 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-132">This means that authorization for granting access tooSAP applications and services needs tootake place in SAP HANA Cloud Platform Identity Authentication for such a setup (as opposed tooconfiguring authorization in Azure Active Directory).</span></span>

<span data-ttu-id="2b67c-133">SAP HANA 클라우드 플랫폼 Id 인증 hello Azure Active Directory Marketplace를 통해 응용 프로그램을 구성 하 여 필요한 개별 클레임 구성 care of tootake 않아도 / SAML 어설션 및 변환 필요한 tooproduce는 SAP 응용 프로그램에 대 한 유효한 인증 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-133">By configuring SAP HANA Cloud Platform Identity Authentication as an application through hello Azure Active Directory Marketplace, you don't need tootake care of configuring needed individual claims / SAML assertions and transformations needed tooproduce a valid authentication token for SAP applications.</span></span>

>[!NOTE] 
><span data-ttu-id="2b67c-134">현재 웹 SSO는 두 파티에서만 테스트되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-134">Currently Web SSO has been tested by both parties, only.</span></span> <span data-ttu-id="2b67c-135">앱-API 또는 API-API 통신에 필요한 흐름은 작동하지만 아직 테스트되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-135">Flows needed for App-to-API or API-to-API communication should work but have not been tested, yet.</span></span> <span data-ttu-id="2b67c-136">후속 작업의 일부로 테스트될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-136">They will be tested as part of subsequent activities.</span></span>
>

## <a name="add-sap-hana-cloud-platform-identity-authentication-from-hello-gallery"></a><span data-ttu-id="2b67c-137">Hello 갤러리에서 SAP HANA 클라우드 플랫폼 Id 인증 추가</span><span class="sxs-lookup"><span data-stu-id="2b67c-137">Add SAP HANA Cloud Platform Identity Authentication from hello gallery</span></span>
<span data-ttu-id="2b67c-138">tooconfigure hello와의 통합 SAP HANA 클라우드 플랫폼 Id 인증 Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 SAP HANA 클라우드 플랫폼 Id 인증 tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-138">tooconfigure hello integration of SAP HANA Cloud Platform Identity Authentication into Azure AD, you need tooadd SAP HANA Cloud Platform Identity Authentication from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2b67c-139">**hello 갤러리에서 SAP HANA 클라우드 플랫폼 Id 인증 tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="2b67c-139">**tooadd SAP HANA Cloud Platform Identity Authentication from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2b67c-140">Hello에 [ **Azure 관리 포털**](https://portal.azure.com), 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-140">In hello [**Azure Management portal**](https://portal.azure.com), on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2b67c-142">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-142">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="2b67c-143">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-143">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="2b67c-145">클릭 **추가** hello 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-145">Click **Add** button on hello top of hello dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="2b67c-147">Hello 검색 상자에 입력 **SAP HANA 클라우드 플랫폼 Id 인증**합니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-147">In hello search box, type **SAP HANA Cloud Platform Identity Authentication**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_01.png)

5. <span data-ttu-id="2b67c-149">Hello 결과 패널에서 선택 **SAP HANA 클라우드 플랫폼 Id 인증**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-149">In hello results panel, select **SAP HANA Cloud Platform Identity Authentication**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_02.png)


##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="2b67c-151">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="2b67c-151">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="2b67c-152">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 SAP HANA Cloud Platform Identity Authentication에서 Azure AD SSO를 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-152">In this section, you configure and test Azure AD SSO with SAP HANA Cloud Platform Identity Authentication based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2b67c-153">SSO toowork에 대 한 Azure AD는 tooknow SAP HANA 클라우드 플랫폼 Id 인증에서 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-153">For SSO toowork, Azure AD needs tooknow what hello counterpart user in SAP HANA Cloud Platform Identity Authentication is tooa user in Azure AD.</span></span> <span data-ttu-id="2b67c-154">즉, Azure AD 사용자 및 SAP HANA 클라우드 플랫폼 Id 인증에 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-154">In other words, a link relationship between an Azure AD user and hello related user in SAP HANA Cloud Platform Identity Authentication needs toobe established.</span></span>

<span data-ttu-id="2b67c-155">Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** 에서 SAP HANA 클라우드 플랫폼 Id 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-155">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in SAP HANA Cloud Platform Identity Authentication.</span></span>

<span data-ttu-id="2b67c-156">tooconfigure 및 SAP HANA 클라우드 플랫폼 Id 인증와 Azure AD SSO 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-156">tooconfigure and test Azure AD SSO with SAP HANA Cloud Platform Identity Authentication, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2b67c-157">**[Azure AD single sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-157">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2b67c-158">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-158">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2b67c-159">**[SAP HANA 클라우드 플랫폼 Id 인증 테스트 사용자 만들기](#creating-a-sap-hana-cloud-platform-identity-authentication-test-user)**  -toohave Britta Simon SAP HANA 클라우드 플랫폼 Identity 인증 시 그녀의 연결 된 Azure AD toohello 표현에에서 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-159">**[Creating a SAP HANA Cloud Platform Identity Authentication test user](#creating-a-sap-hana-cloud-platform-identity-authentication-test-user)** - toohave a counterpart of Britta Simon in SAP HANA Cloud Platform Identity Authentication that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="2b67c-160">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-160">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2b67c-161">**[Single sign on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="2b67c-161">**[Testing single sign-on](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-sso"></a><span data-ttu-id="2b67c-162">Azure AD SSO 구성</span><span class="sxs-lookup"><span data-stu-id="2b67c-162">Configuring Azure AD SSO</span></span>

<span data-ttu-id="2b67c-163">이 섹션에서는 hello Azure 관리 포털에서 Azure AD SSO를 사용 하도록 설정 및 SAP HANA 클라우드 플랫폼 Id 인증 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-163">In this section, you enable Azure AD SSO in hello Azure Management portal and configure single sign-on in your SAP HANA Cloud Platform Identity Authentication application.</span></span>

<span data-ttu-id="2b67c-164">SAP HANA 클라우드 플랫폼 Id 인증 응용 프로그램에는 특정 형식의 hello SAML 어설션 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-164">SAP HANA Cloud Platform Identity Authentication application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="2b67c-165">Hello에서 이러한 특성의 hello 값을 관리할 수 있습니다 "**사용자 특성**" 응용 프로그램 통합 페이지에서 섹션.</span><span class="sxs-lookup"><span data-stu-id="2b67c-165">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="2b67c-166">다음 스크린 샷 hello이에 대 한 예가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-166">hello following screenshot shows an example for this.</span></span>

![Single Sign-on 구성](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_03.png)

<span data-ttu-id="2b67c-168">**SAP HANA 클라우드 플랫폼 Id 인증와 Azure AD SSO tooconfigure hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="2b67c-168">**tooconfigure Azure AD SSO with SAP HANA Cloud Platform Identity Authentication, perform hello following steps:**</span></span>

1. <span data-ttu-id="2b67c-169">Hello에 hello Azure 관리 포털에서 **SAP HANA 클라우드 플랫폼 Id 인증** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-169">In hello Azure Management portal, on hello **SAP HANA Cloud Platform Identity Authentication** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="2b67c-171">Hello에 **Single sign on** 대화 상자에서으로 **모드** 선택 **SAML 기반 로그온** tooenable single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-171">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Single Sign-on 구성][5]

3. <span data-ttu-id="2b67c-173">Hello에 **사용자 특성** hello 섹션 **Single sign on** 경우 대화 상자, SAP 응용 프로그램의 예를 들어 "firstName" 특성이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-173">In hello **User Attributes** section on hello **Single sign-on** dialog, if your SAP application expects an attribute for example "firstName".</span></span> <span data-ttu-id="2b67c-174">Hello SAML 토큰 특성 대화 상자에서 hello "firstName" 특성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-174">On hello SAML token attributes dialog, add hello "firstName" attribute.</span></span>
 1. <span data-ttu-id="2b67c-175">클릭 **특성 추가** tooopen hello **특성 추가** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="2b67c-175">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>
 
    ![Single Sign-on 구성][6]

    ![Single Sign-on 구성](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_05.png)
 2. <span data-ttu-id="2b67c-178">Hello에 **특성 이름** 텍스트 형식 hello 특성 이름 "firstName"입니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-178">In hello **Attribute Name** textbox, type hello attribute name "firstName".</span></span>
 3. <span data-ttu-id="2b67c-179">Hello에서 **특성 값** "user.givenname" 선택 hello 특성 값을 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-179">From hello **Attribute Value** list, select hello attribute value "user.givenname".</span></span>
 4. <span data-ttu-id="2b67c-180">**Ok**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-180">Click **Ok**.</span></span>

4. <span data-ttu-id="2b67c-181">Hello에 **SAP HANA 클라우드 플랫폼 Identity 인증 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-181">On hello **SAP HANA Cloud Platform Identity Authentication Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_06.png)
 1. <span data-ttu-id="2b67c-183">Hello에 **로그온 URL** textbox hello SAP 응용 프로그램에 대 한 URL에 hello 기호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-183">In hello **Sign On URL** textbox, type hello sign on URL for hello SAP application.</span></span>
 2. <span data-ttu-id="2b67c-184">Hello에 **식별자** 텍스트 패턴 형식 hello 값:`<entity-id>.accounts.ondemand.com`</span><span class="sxs-lookup"><span data-stu-id="2b67c-184">In hello **Identifier** textbox, type hello value following pattern: `<entity-id>.accounts.ondemand.com`</span></span> 
    * <span data-ttu-id="2b67c-185">이 값을 모르는 경우에 따라 하십시오 hello SAP HANA 클라우드 플랫폼 Id 인증 설명서 [테 넌 트 SAML 2.0 구성](https://help.hana.ondemand.com/cloud_identity/frameset.htm?e81a19b0067f4646982d7200a8dab3ca.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-185">If you don't know this value, please follow hello SAP HANA Cloud Platform Identity Authentication documentation on [Tenant SAML 2.0 Configuration](https://help.hana.ondemand.com/cloud_identity/frameset.htm?e81a19b0067f4646982d7200a8dab3ca.html).</span></span>

5. <span data-ttu-id="2b67c-186">Hello에 **SAP HANA 클라우드 플랫폼 Identity 인증 구성** 섹션에서 클릭 **SAP HANA 클라우드 플랫폼 Id 인증 구성** tooopen **signon구성** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="2b67c-186">On hello **SAP HANA Cloud Platform Identity Authentication Configuration** section, click **Configure SAP HANA Cloud Platform Identity Authentication** tooopen **Configure sign-on** dialog.</span></span> <span data-ttu-id="2b67c-187">그런 다음 클릭 **SAML XML 메타 데이터** hello 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-187">Then, click on **SAML XML Metadata** and save hello file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_07.png) 

    ![Single Sign-on 구성](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_08.png)

6. <span data-ttu-id="2b67c-190">SSO 응용 프로그램에 대해 구성 된 tooget tooSAP HANA 클라우드 플랫폼 Identity 인증 관리 콘솔을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-190">tooget SSO configured for your application, go tooSAP HANA Cloud Platform Identity Authentication Administration Console.</span></span> <span data-ttu-id="2b67c-191">hello URL 패턴 hello에 있습니다.`https://<tenant-id>.accounts.ondemand.com/admin`</span><span class="sxs-lookup"><span data-stu-id="2b67c-191">hello URL has hello following pattern: `https://<tenant-id>.accounts.ondemand.com/admin`</span></span>
 * <span data-ttu-id="2b67c-192">그런 다음 hello 설명서 SAP HANA 클라우드 플랫폼 Id 인증에 너무 따라[SAP HANA 클라우드 플랫폼 Id 인증에 회사 Id 공급자로 구성 Microsoft Azure AD](https://help.hana.ondemand.com/cloud_identity/frameset.htm?626b17331b4d4014b8790d3aea70b240.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-192">Then, follow hello documentation on SAP HANA Cloud Platform Identity Authentication too[Configure Microsoft Azure AD as Corporate Identity Provider at SAP HANA Cloud Platform Identity Authentication](https://help.hana.ondemand.com/cloud_identity/frameset.htm?626b17331b4d4014b8790d3aea70b240.html).</span></span> 

7. <span data-ttu-id="2b67c-193">Hello Azure 관리 포털에서 클릭 **저장** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-193">In hello Azure Management portal, click **Save** button.</span></span>
8. <span data-ttu-id="2b67c-194">Hello tooadd을 다른 SAP 응용 프로그램에 SSO를 사용 하는 경우에 다음 단계를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-194">Continue hello following steps only if you want tooadd and enable SSO for another SAP application.</span></span> <span data-ttu-id="2b67c-195">SAP HANA 클라우드 플랫폼 Id 인증의 다른 인스턴스가 hello 섹션 "추가 SAP HANA 클라우드 플랫폼 Id 인증 hello 갤러리에서" tooadd 아래 단계를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-195">Repeat steps under hello section “Adding SAP HANA Cloud Platform Identity Authentication from hello gallery” tooadd another instance of SAP HANA Cloud Platform Identity Authentication.</span></span>
9. <span data-ttu-id="2b67c-196">Hello에 hello Azure 관리 포털에서 **SAP HANA 클라우드 플랫폼 Id 인증** 응용 프로그램 통합 페이지에서 클릭 **연결 된 로그온**합니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-196">In hello Azure Management portal, on hello **SAP HANA Cloud Platform Identity Authentication** application integration page, click **Linked Sign-on**.</span></span>

    ![연결된 로그온 구성](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/linked_sign_on.png)
10. <span data-ttu-id="2b67c-198">그런 다음 hello 구성을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-198">Then, save hello configuration.</span></span>

>[!NOTE] 
><span data-ttu-id="2b67c-199">hello 새 응용 프로그램 hello 이전 SAP 응용 프로그램에 대 한 hello SSO 구성을 활용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-199">hello new application will leverage hello SSO configuration for hello previous SAP application.</span></span> <span data-ttu-id="2b67c-200">있는지 확인 하십시오 있습니다 사용할 hello hello SAP HANA 클라우드 플랫폼 Identity 인증 관리 콘솔의에서 동일한 회사 Id 공급자입니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-200">Please make sure you use hello same Corporate Identity Providers in hello SAP HANA Cloud Platform Identity Authentication Administration Console.</span></span>
>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="2b67c-201">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="2b67c-201">Create an Azure AD test user</span></span>
<span data-ttu-id="2b67c-202">이 섹션의 hello 목표 Britta Simon 라는 hello 새로운 포털에서 toocreate 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-202">hello objective of this section is toocreate a test user in hello new portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="2b67c-204">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="2b67c-204">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2b67c-205">Hello에 **Azure 관리 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-205">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2b67c-207">너무 이동**사용자 및 그룹** 클릭 **모든 사용자에 게** 사용자 toodisplay hello 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-207">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2b67c-209">Hello 대화의 hello 위쪽 클릭 **추가** tooopen hello **사용자** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="2b67c-209">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2b67c-211">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-211">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_04.png) 
  1. <span data-ttu-id="2b67c-213">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-213">In hello **Name** textbox, type **BrittaSimon**.</span></span>
  2. <span data-ttu-id="2b67c-214">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-214">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>
  3. <span data-ttu-id="2b67c-215">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-215">Select **Show Password** and write down hello value of hello **Password**.</span></span>
  4. <span data-ttu-id="2b67c-216">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-216">Click **Create**.</span></span> 

### <a name="create-a-sap-hana-cloud-platform-identity-authentication-test-user"></a><span data-ttu-id="2b67c-217">SAP HANA Cloud Platform Identity Authentication 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="2b67c-217">Create a SAP HANA Cloud Platform Identity Authentication test user</span></span>

<span data-ttu-id="2b67c-218">SAP HANA 클라우드 플랫폼 Id 인증 된 사용자 toocreate가 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-218">You don't need toocreate an user on SAP HANA Cloud Platform Identity Authentication.</span></span> <span data-ttu-id="2b67c-219">Hello Azure AD 사용자 저장소에 있는 사용자를 hello SSO 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-219">Users who are in hello Azure AD user store can use hello SSO functionality.</span></span>

<span data-ttu-id="2b67c-220">SAP HANA 클라우드 플랫폼 Id 인증 hello Id 페더레이션이 옵션을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-220">SAP HANA Cloud Platform Identity Authentication supports hello Identity Federation option.</span></span> <span data-ttu-id="2b67c-221">이 옵션 hello 회사 id 공급자에 의해 인증 된 hello 사용자의 hello 사용자 저장소의 SAP HANA 클라우드 플랫폼 Id 인증 존재 하는 경우 응용 프로그램 toocheck hello를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-221">This option allows hello application toocheck if hello users authenticated by hello corporate identity provider exist in hello user store of SAP HANA Cloud Platform Identity Authentication.</span></span> 

<span data-ttu-id="2b67c-222">Hello 기본 설정에서 hello Id 페더레이션이 옵션은 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-222">In hello default setting, hello Identity Federation option is disabled.</span></span> <span data-ttu-id="2b67c-223">Id 페더레이션을 사용 하는 경우 SAP HANA 클라우드 플랫폼 Id 인증에서 가져온 hello 사용자만 수 tooaccess hello 응용 프로그램을 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-223">If Identity Federation is enabled, only hello users that are imported in SAP HANA Cloud Platform Identity Authentication are able tooaccess hello application.</span></span> 

<span data-ttu-id="2b67c-224">Tooenable 또는 사용 안 함 Id 페더레이션이 SAP HANA 클라우드 플랫폼 Identity 인증을 확인 하려면 어떻게 해야 Id 페더레이션이 SAP HANA 클라우드 플랫폼 Identity 인증에 사용 하도록 설정 하는 방법에 대 한 자세한 내용은 [Id 페더레이션 구성 사용자 저장소의 SAP HANA 클라우드 플랫폼 Id 인증 안녕하세요와. ](https://help.hana.ondemand.com/cloud_identity/frameset.htm?c029bbbaefbf4350af15115396ba14e2.html).</span><span class="sxs-lookup"><span data-stu-id="2b67c-224">For more information about how tooenable or disable Identity Federation with SAP HANA Cloud Platform Identity Authentication, see Enable Identity Federation with SAP HANA Cloud Platform Identity Authentication in [Configure Identity Federation with hello User Store of SAP HANA Cloud Platform Identity Authentication.](https://help.hana.ondemand.com/cloud_identity/frameset.htm?c029bbbaefbf4350af15115396ba14e2.html).</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="2b67c-225">Azure AD hello 테스트 사용자를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-225">Assign hello Azure AD test user</span></span>

<span data-ttu-id="2b67c-226">이 섹션에서는 그녀의 액세스 tooSAP HANA 클라우드 플랫폼 Id 인증 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooSAP HANA Cloud Platform Identity Authentication.</span></span>

![사용자 할당][200] 

<span data-ttu-id="2b67c-228">**tooassign Britta Simon tooSAP HANA 클라우드 플랫폼 Id 인증 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="2b67c-228">**tooassign Britta Simon tooSAP HANA Cloud Platform Identity Authentication, perform hello following steps:**</span></span>

1. <span data-ttu-id="2b67c-229">Hello Azure 관리 포털에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-229">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="2b67c-231">Hello 응용 프로그램 목록에서 선택 **SAP HANA 클라우드 플랫폼 Id 인증**합니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-231">In hello applications list, select **SAP HANA Cloud Platform Identity Authentication**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_09.png)

3. <span data-ttu-id="2b67c-233">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="2b67c-235">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-235">Click **Add** button.</span></span> <span data-ttu-id="2b67c-236">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="2b67c-238">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="2b67c-239">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2b67c-240">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    

### <a name="test-single-sign-on"></a><span data-ttu-id="2b67c-241">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="2b67c-241">Test single sign-on</span></span>

<span data-ttu-id="2b67c-242">이 섹션에서는 hello 액세스 패널을 사용 하 여 Azure AD SSO 구성을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-242">In this section, you test your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="2b67c-243">Hello 액세스 패널에서에서 hello SAP HANA 클라우드 플랫폼 Id 인증 타일을 클릭할 때 자동으로 로그온 tooyour SAP HANA 클라우드 플랫폼 Id 인증 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b67c-243">When you click hello SAP HANA Cloud Platform Identity Authentication tile in hello Access Panel, you should get automatically signed-on tooyour SAP HANA Cloud Platform Identity Authentication application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="2b67c-244">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="2b67c-244">Additional resources</span></span>

* [<span data-ttu-id="2b67c-245">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="2b67c-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2b67c-246">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="2b67c-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_05.png
[6]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_06.png

[100]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_203.png