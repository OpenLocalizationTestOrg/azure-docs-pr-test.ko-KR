---
title: "자습서: xMatters OnDemand와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 xMatters OnDemand 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ca0633db-4f95-432e-b3db-0168193b5ce9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 7cc8f9f0d8cefc8a60b9514027437ced50c66242
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-xmatters-ondemand"></a><span data-ttu-id="f48da-103">자습서: xMatters OnDemand와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="f48da-103">Tutorial: Azure Active Directory integration with xMatters OnDemand</span></span>

<span data-ttu-id="f48da-104">이 자습서에 설명 어떻게 toointegrate xMatters OnDemand와 Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f48da-104">In this tutorial, you learn how toointegrate xMatters OnDemand with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f48da-105">Azure AD와 xMatters OnDemand를 통합 이점을 다음 hello로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-105">Integrating xMatters OnDemand with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f48da-106">Azure ad 액세스 tooxMatters OnDemand를 가진 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-106">You can control in Azure AD who has access tooxMatters OnDemand</span></span>
- <span data-ttu-id="f48da-107">프로그램 사용자 tooautomatically get 로그온 tooxMatters OnDemand (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-107">You can enable your users tooautomatically get signed-on tooxMatters OnDemand (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f48da-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f48da-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f48da-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="f48da-110">Prerequisites</span></span>

<span data-ttu-id="f48da-111">xMatters OnDemand와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-111">tooconfigure Azure AD integration with xMatters OnDemand, you need hello following items:</span></span>

- <span data-ttu-id="f48da-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="f48da-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f48da-113">xMatters OnDemand Single Sign-on이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="f48da-113">A xMatters OnDemand single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f48da-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f48da-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f48da-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="f48da-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f48da-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f48da-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="f48da-118">Scenario description</span></span>
<span data-ttu-id="f48da-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f48da-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f48da-121">XMatters OnDemand hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="f48da-121">Adding xMatters OnDemand from hello gallery</span></span>
2. <span data-ttu-id="f48da-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="f48da-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-xmatters-ondemand-from-hello-gallery"></a><span data-ttu-id="f48da-123">XMatters OnDemand hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="f48da-123">Adding xMatters OnDemand from hello gallery</span></span>
<span data-ttu-id="f48da-124">tooconfigure hello와의 통합 xMatters OnDemand Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 tooadd xMatters OnDemand 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-124">tooconfigure hello integration of xMatters OnDemand into Azure AD, you need tooadd xMatters OnDemand from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f48da-125">**tooadd xMatters OnDemand hello 갤러리에서 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="f48da-125">**tooadd xMatters OnDemand from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f48da-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f48da-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f48da-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="f48da-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="f48da-133">Hello 검색 상자에 입력 **xMatters OnDemand**합니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-133">In hello search box, type **xMatters OnDemand**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_search.png)

5. <span data-ttu-id="f48da-135">Hello 결과 패널에서 선택 **xMatters OnDemand**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-135">In hello results panel, select **xMatters OnDemand**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f48da-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="f48da-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f48da-138">이 섹션에서는 Britta Simon이라는 테스트 사용자를 기반으로 xMatters OnDemand에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-138">In this section, you configure and test Azure AD single sign-on with xMatters OnDemand based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f48da-139">Single sign on toowork에 대 한 Azure AD는 필요 tooknow 어떤 hello xMatters OnDemand에서에서 테이블에 해당 사용자가 Azure AD에서 tooa 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in xMatters OnDemand is tooa user in Azure AD.</span></span> <span data-ttu-id="f48da-140">즉, Azure AD 사용자와 xMatters에 hello 관련된 사용자 간 링크 관계를 OnDemand toobe 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-140">In other words, a link relationship between an Azure AD user and hello related user in xMatters OnDemand needs toobe established.</span></span>

<span data-ttu-id="f48da-141">XMatters OnDemand에에서 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-141">In xMatters OnDemand, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f48da-142">tooconfigure와 xMatters OnDemand와 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-142">tooconfigure and test Azure AD single sign-on with xMatters OnDemand, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f48da-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f48da-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f48da-145">**[XMatters OnDemand 테스트 사용자 만들기](#creating-a-xmatters-ondemand-test-user)**  -toohave xMatters OnDemand 표현인 연결 된 toohello Azure AD 사용자의에서 Britta Simon 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-145">**[Creating a xMatters OnDemand test user](#creating-a-xmatters-ondemand-test-user)** - toohave a counterpart of Britta Simon in xMatters OnDemand that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f48da-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f48da-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="f48da-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f48da-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="f48da-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f48da-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 프로그램 xMatters OnDemand 응용 프로그램에서에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your xMatters OnDemand application.</span></span>

<span data-ttu-id="f48da-150">**Azure AD tooconfigure single sign on와 xMatters OnDemand hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="f48da-150">**tooconfigure Azure AD single sign-on with xMatters OnDemand, perform hello following steps:**</span></span>

1. <span data-ttu-id="f48da-151">Hello hello에 Azure 포털에서에서 **xMatters OnDemand** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-151">In hello Azure portal, on hello **xMatters OnDemand** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="f48da-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_samlbase.png)

3. <span data-ttu-id="f48da-155">Hello에 **xMatters OnDemand 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-155">On hello **xMatters OnDemand Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_url.png)
    
    <span data-ttu-id="f48da-157">a.</span><span class="sxs-lookup"><span data-stu-id="f48da-157">a.</span></span> <span data-ttu-id="f48da-158">Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:</span><span class="sxs-lookup"><span data-stu-id="f48da-158">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>   
    | |
    |--|
    | `https://<companyname>.au1.xmatters.com.au/`|
    | `https://<companyname>.cs1.xmatters.com/`|
    | `https://<companyname>.xmatters.com/`|
    | `https://www.xmatters.com`|
    | `https://<companyname>.xmatters.com.au/`|

    <span data-ttu-id="f48da-159">b.</span><span class="sxs-lookup"><span data-stu-id="f48da-159">b.</span></span> <span data-ttu-id="f48da-160">Hello에 **회신 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:</span><span class="sxs-lookup"><span data-stu-id="f48da-160">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.au1.xmatters.com.au`|
    | `https://<companyname>.xmatters.com/sp/<instancename>`|
    | `https://<companyname>.cs1.xmatters.com/sp/<instancename>`|
    | `https://<companyname>.au1.xmatters.com.au/<instancename>`|

    > [!NOTE] 
    > <span data-ttu-id="f48da-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-161">These values are not real.</span></span> <span data-ttu-id="f48da-162">Hello 실제 식별자 및 회신 URL로이 값을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="f48da-163">연락처 [xMatters OnDemand 지원 팀](https://www.xmatters.com/company/contact-us/) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-163">Contact [xMatters OnDemand support team](https://www.xmatters.com/company/contact-us/) tooget these values.</span></span>

4. <span data-ttu-id="f48da-164">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **Certificate(Base64)** hello 인증서 파일을 로컬에 저장 합니다 **c:\\XMatters OnDemand.cer**.</span><span class="sxs-lookup"><span data-stu-id="f48da-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file locally as **c:\\XMatters OnDemand.cer**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_certificate.png)
    
    > [!IMPORTANT]
    > <span data-ttu-id="f48da-166">Tooforward hello 인증서 toohello 필요한 [xMatters OnDemand 지원 팀](https://www.xmatters.com/company/contact-us/)합니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-166">You need tooforward hello certificate toohello [xMatters OnDemand support team](https://www.xmatters.com/company/contact-us/).</span></span> <span data-ttu-id="f48da-167">hello 인증서 toobe hello single sign-on 구성을 완료 하기 전에 hello xMatters 지원 팀에서 업로드 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-167">hello certificate needs toobe uploaded by hello xMatters support team before you can finalize hello single sign-on configuration.</span></span> 

5. <span data-ttu-id="f48da-168">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-168">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f48da-170">Hello에 **xMatters OnDemand 구성** 섹션에서 클릭 **xMatters OnDemand 구성** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="f48da-170">On hello **xMatters OnDemand Configuration** section, click **Configure xMatters OnDemand** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="f48da-171">복사 hello **Sign-Out URL, SAML 엔터티 ID, 및 SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="f48da-171">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_configure.png) 

7. <span data-ttu-id="f48da-173">다른 웹 브라우저 창에서 tooyour에 XMatters OnDemand 회사 사이트는 관리자 권한으로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-173">In a different web browser window, log in tooyour XMatters OnDemand company site as an administrator.</span></span>

8. <span data-ttu-id="f48da-174">도구 모음의 hello hello 위쪽에 클릭 **관리자**, 클릭 하 고 **회사 정보** hello hello 왼쪽 탐색 모음에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-174">In hello toolbar on hello top, click **Admin**, and then click **Company Details** in hello navigation bar on hello left side.</span></span>
   
    <span data-ttu-id="f48da-175">![관리자](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776795.png "관리자")</span><span class="sxs-lookup"><span data-stu-id="f48da-175">![Admin](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776795.png "Admin")</span></span>

9. <span data-ttu-id="f48da-176">Hello에 **SAML 구성** 페이지 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-176">On hello **SAML Configuration** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="f48da-177">![SAML 구성](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776796.png "SAML 구성")</span><span class="sxs-lookup"><span data-stu-id="f48da-177">![SAML configuration](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776796.png "SAML configuration")</span></span>
   
    <span data-ttu-id="f48da-178">a.</span><span class="sxs-lookup"><span data-stu-id="f48da-178">a.</span></span> <span data-ttu-id="f48da-179">**SAML 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-179">Select **Enable SAML**.</span></span>
   
    <span data-ttu-id="f48da-180">b.</span><span class="sxs-lookup"><span data-stu-id="f48da-180">b.</span></span> <span data-ttu-id="f48da-181">붙여넣기 **SAML 엔터티 ID**, hello에 hello Azure 포털에서에서 복사한 있는 **Id 공급자 ID** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-181">Paste **SAML Entity ID**, which you have copied from hello Azure portal into hello **Identity Provider ID** textbox.</span></span>
   
    <span data-ttu-id="f48da-182">c.</span><span class="sxs-lookup"><span data-stu-id="f48da-182">c.</span></span> <span data-ttu-id="f48da-183">붙여넣기 **SAML Single Sign-on 서비스 URL**, hello에 hello Azure 포털에서에서 복사한 있는 **Single Sign On URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-183">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal into hello **Single Sign On URL** textbox.</span></span>
   
    <span data-ttu-id="f48da-184">d.</span><span class="sxs-lookup"><span data-stu-id="f48da-184">d.</span></span> <span data-ttu-id="f48da-185">붙여넣기 **Sign-Out URL**, hello에 hello Azure 포털에서에서 복사한 있는 **단일 로그 아웃 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-185">Paste **Sign-Out URL**, which you have copied from hello Azure portal into hello **Single Logout URL** textbox.</span></span>
   
    <span data-ttu-id="f48da-186">e.</span><span class="sxs-lookup"><span data-stu-id="f48da-186">e.</span></span> <span data-ttu-id="f48da-187">Hello 위쪽에, hello 회사 정보 페이지에서 클릭 **변경 내용 저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-187">On hello Company Details page, at hello top, click **Save Changes**.</span></span>
    
    <span data-ttu-id="f48da-188">![회사 상세 정보](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776797.png "회사 상세 정보")</span><span class="sxs-lookup"><span data-stu-id="f48da-188">![Company details](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776797.png "Company details")</span></span>

> [!TIP]
> <span data-ttu-id="f48da-189">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="f48da-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f48da-190">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="f48da-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f48da-191">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f48da-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f48da-192">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="f48da-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="f48da-193">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="f48da-195">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="f48da-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f48da-196">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f48da-198">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f48da-200">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f48da-202">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f48da-204">a.</span><span class="sxs-lookup"><span data-stu-id="f48da-204">a.</span></span> <span data-ttu-id="f48da-205">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f48da-206">b.</span><span class="sxs-lookup"><span data-stu-id="f48da-206">b.</span></span> <span data-ttu-id="f48da-207">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f48da-208">c.</span><span class="sxs-lookup"><span data-stu-id="f48da-208">c.</span></span> <span data-ttu-id="f48da-209">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f48da-210">d.</span><span class="sxs-lookup"><span data-stu-id="f48da-210">d.</span></span> <span data-ttu-id="f48da-211">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-211">Click **Create**.</span></span>
 
### <a name="creating-a-xmatters-ondemand-test-user"></a><span data-ttu-id="f48da-212">xMatters OnDemand 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="f48da-212">Creating a xMatters OnDemand test user</span></span>

<span data-ttu-id="f48da-213">Tooenable Azure AD 사용자가 toolog tooXMatters OnDemand에에서 주문 하 고에 XMatters OnDemand에 이들 프로 비전 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-213">In order tooenable Azure AD users toolog in tooXMatters OnDemand, they must be provisioned into XMatters OnDemand.</span></span> <span data-ttu-id="f48da-214">Hello XMatters OnDemand의 경우에서 프로 비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-214">In hello case of XMatters OnDemand, provisioning is a manual task.</span></span>

### <a name="tooprovision-a-user-accounts-perform-hello-following-steps"></a><span data-ttu-id="f48da-215">사용자 계정 수행 tooprovision hello 다음 단계:</span><span class="sxs-lookup"><span data-stu-id="f48da-215">tooprovision a user accounts, perform hello following steps:</span></span>
1. <span data-ttu-id="f48da-216">Tooyour 로그인 **XMatters OnDemand** 테 넌 트입니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-216">Log in tooyour **XMatters OnDemand** tenant.</span></span>

2.  <span data-ttu-id="f48da-217">클릭 **사용자** 탭을 클릭 한 다음 **사용자 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-217">Click **Users** tab. and then click **Add User**.</span></span>
  
    <span data-ttu-id="f48da-218">![사용자](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781048.png "사용자")</span><span class="sxs-lookup"><span data-stu-id="f48da-218">![Users](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781048.png "Users")</span></span>

3. <span data-ttu-id="f48da-219">Hello에 **사용자 추가** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-219">In hello **Add a User** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="f48da-220">![사용자 추가](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781049.png "사용자 추가")</span><span class="sxs-lookup"><span data-stu-id="f48da-220">![Add a User](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781049.png "Add a User")</span></span>

    <span data-ttu-id="f48da-221">a.</span><span class="sxs-lookup"><span data-stu-id="f48da-221">a.</span></span> <span data-ttu-id="f48da-222">**활성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-222">Select **Active**.</span></span>

    <span data-ttu-id="f48da-223">b.</span><span class="sxs-lookup"><span data-stu-id="f48da-223">b.</span></span> <span data-ttu-id="f48da-224">Hello에 **사용자 ID** 형식 hello 사용자 id와 같은 사용자의 텍스트 상자 Brittasimon@contoso.com합니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-224">In hello **User ID** textbox, type hello user id of user like Brittasimon@contoso.com.</span></span>
   
    <span data-ttu-id="f48da-225">c.</span><span class="sxs-lookup"><span data-stu-id="f48da-225">c.</span></span> <span data-ttu-id="f48da-226">Hello에 **이름** textbox Britta 같은 hello 사용자의 형식 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-226">In hello **First Name** textbox, type first name of hello user like Britta.</span></span>

    <span data-ttu-id="f48da-227">d.</span><span class="sxs-lookup"><span data-stu-id="f48da-227">d.</span></span> <span data-ttu-id="f48da-228">Hello에 **성** textbox Simon 같은 hello 사용자의 성 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-228">In hello **Last Name** textbox, type last name of hello user like Simon.</span></span>
    
    <span data-ttu-id="f48da-229">e.</span><span class="sxs-lookup"><span data-stu-id="f48da-229">e.</span></span> <span data-ttu-id="f48da-230">Hello에 **사이트** textbox, Enter 유효한 Azure의 hello 올바른 사이트 tooprovision 원하는 AD 계정.</span><span class="sxs-lookup"><span data-stu-id="f48da-230">In hello **Site** textbox, Enter hello valid site of a valid Azure AD account you want tooprovision.</span></span>
    
    <span data-ttu-id="f48da-231">f.</span><span class="sxs-lookup"><span data-stu-id="f48da-231">f.</span></span> <span data-ttu-id="f48da-232">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-232">Click **Save**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f48da-233">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-233">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f48da-234">이 섹션에서는 액세스 tooxMatters OnDemand를 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-234">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooxMatters OnDemand.</span></span>

![사용자 할당][200] 

<span data-ttu-id="f48da-236">**tooassign Britta Simon tooxMatters OnDemand hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="f48da-236">**tooassign Britta Simon tooxMatters OnDemand, perform hello following steps:**</span></span>

1. <span data-ttu-id="f48da-237">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-237">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="f48da-239">Hello 응용 프로그램 목록에서 선택 **xMatters OnDemand**합니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-239">In hello applications list, select **xMatters OnDemand**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_app.png) 

3. <span data-ttu-id="f48da-241">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-241">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="f48da-243">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-243">Click **Add** button.</span></span> <span data-ttu-id="f48da-244">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="f48da-246">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-246">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f48da-247">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f48da-248">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f48da-249">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="f48da-249">Testing single sign-on</span></span>

<span data-ttu-id="f48da-250">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-250">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="f48da-251">Hello xMatters OnDemand hello 액세스 패널에에서는 타일을 클릭할 때 자동으로 로그온 tooyour xMatters OnDemand 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-251">When you click hello xMatters OnDemand tile in hello Access Panel, you should get automatically signed-on tooyour xMatters OnDemand application.</span></span>
<span data-ttu-id="f48da-252">액세스 패널에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f48da-252">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f48da-253">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="f48da-253">Additional resources</span></span>

* [<span data-ttu-id="f48da-254">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="f48da-254">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f48da-255">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="f48da-255">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_203.png

