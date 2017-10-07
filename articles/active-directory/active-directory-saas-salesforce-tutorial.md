---
title: "자습서: Salesforce와 Azure Active Directory 통합 | Microsoft 문서"
description: "단일 로그온 tooconfigure 방법을 알아보려면 Azure Active Directory와 Salesforce 사이의 합니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2d7d420-dc91-41b8-a6b3-59579e043b35
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 1d848518ee30910e051cdc4746c599219f3b5a3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce"></a><span data-ttu-id="9847f-103">자습서: Salesforce와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="9847f-103">Tutorial: Azure Active Directory integration with Salesforce</span></span>

<span data-ttu-id="9847f-104">이 자습서에 설명 어떻게 toointegrate Salesforce Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9847f-104">In this tutorial, you learn how toointegrate Salesforce with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9847f-105">Azure AD와 Salesforce를 통합 이점을 다음 hello로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-105">Integrating Salesforce with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9847f-106">액세스 tooSalesforce을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-106">You can control in Azure AD who has access tooSalesforce</span></span>
- <span data-ttu-id="9847f-107">프로그램 사용자 tooautomatically get 로그온 tooSalesforce (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-107">You can enable your users tooautomatically get signed-on tooSalesforce (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9847f-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="9847f-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9847f-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="9847f-110">Prerequisites</span></span>

<span data-ttu-id="9847f-111">Azure AD 및 Salesforce 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-111">tooconfigure Azure AD integration with Salesforce, you need hello following items:</span></span>

- <span data-ttu-id="9847f-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="9847f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9847f-113">Salesforce Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="9847f-113">A Salesforce single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9847f-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9847f-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9847f-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="9847f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9847f-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9847f-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="9847f-118">Scenario description</span></span>
<span data-ttu-id="9847f-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9847f-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9847f-121">Salesforce는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="9847f-121">Adding Salesforce from hello gallery</span></span>
2. <span data-ttu-id="9847f-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="9847f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-salesforce-from-hello-gallery"></a><span data-ttu-id="9847f-123">Salesforce는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="9847f-123">Adding Salesforce from hello gallery</span></span>
<span data-ttu-id="9847f-124">tooconfigure hello와의 통합 Salesforce Azure AD 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Salesforce tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-124">tooconfigure hello integration of Salesforce into Azure AD, you need tooadd Salesforce from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9847f-125">**hello 갤러리에서 Salesforce tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="9847f-125">**tooadd Salesforce from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9847f-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9847f-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9847f-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="9847f-131">클릭 **새 응용 프로그램** hello 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="9847f-133">Hello 검색 상자에 입력 **Salesforce**합니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-133">In hello search box, type **Salesforce**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_search.png)

5. <span data-ttu-id="9847f-135">Hello 결과 패널에서 선택 **Salesforce**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-135">In hello results panel, select **Salesforce**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9847f-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="9847f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9847f-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Salesforce에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-138">In this section, you configure and test Azure AD single sign-on with Salesforce based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="9847f-139">Single sign on toowork에 대 한 Azure AD는 tooknow에 Azure AD에서 Salesforce에서 어떤 hello 테이블에 해당 사용자가 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Salesforce is tooa user in Azure AD.</span></span> <span data-ttu-id="9847f-140">즉, Azure AD 사용자 및 Salesforce의 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-140">In other words, a link relationship between an Azure AD user and hello related user in Salesforce needs toobe established.</span></span>

<span data-ttu-id="9847f-141">Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** Salesforce에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Salesforce.</span></span>

<span data-ttu-id="9847f-142">tooconfigure 및 Salesforce 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-142">tooconfigure and test Azure AD single sign-on with Salesforce, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9847f-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9847f-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9847f-145">**[Salesforce 테스트 사용자 만들기](#creating-a-salesforce-test-user)**  -toohave 표현인 연결 된 toohello Azure AD 사용자의 Salesforce에서 Britta Simon의 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-145">**[Creating a Salesforce test user](#creating-a-salesforce-test-user)** - toohave a counterpart of Britta Simon in Salesforce that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="9847f-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9847f-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="9847f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9847f-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="9847f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9847f-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 Salesforce 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Salesforce application.</span></span>

<span data-ttu-id="9847f-150">**tooconfigure Azure AD single sign on와 Salesforce를 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="9847f-150">**tooconfigure Azure AD single sign-on with Salesforce, perform hello following steps:**</span></span>

1. <span data-ttu-id="9847f-151">Hello hello에 Azure 포털에서에서 **Salesforce** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-151">In hello Azure portal, on hello **Salesforce** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="9847f-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_samlbase.png)

3. <span data-ttu-id="9847f-155">Hello에 **Salesforce 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-155">On hello **Salesforce Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_url.png)

    <span data-ttu-id="9847f-157">Hello에 **로그온 URL** hello 패턴을 사용 하 여 형식 hello 값 텍스트 상자:</span><span class="sxs-lookup"><span data-stu-id="9847f-157">In hello **Sign-on URL** textbox, type hello value using hello following pattern:</span></span> 
   * <span data-ttu-id="9847f-158">엔터프라이즈 계정: `https://<subdomain>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="9847f-158">Enterprise account: `https://<subdomain>.my.salesforce.com`</span></span>
   * <span data-ttu-id="9847f-159">개발자 계정: `https://<subdomain>-dev-ed.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="9847f-159">Developer account: `https://<subdomain>-dev-ed.my.salesforce.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9847f-160">이러한 값은 실제 hello 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-160">These values are not hello real.</span></span> <span data-ttu-id="9847f-161">Hello 실제 로그온 URL으로 이러한 값을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-161">Update these values with hello actual Sign-on URL.</span></span> <span data-ttu-id="9847f-162">연락처 [Salesforce 클라이언트 지원 팀](https://help.salesforce.com/support) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-162">Contact [Salesforce Client support team](https://help.salesforce.com/support) tooget these values.</span></span> 
 
4. <span data-ttu-id="9847f-163">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **인증서** hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-163">On hello **SAML Signing Certificate** section, click **Certificate** and then save hello certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_certificate.png) 

5. <span data-ttu-id="9847f-165">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-165">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-salesforce-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9847f-167">Hello에 **Salesforce 구성** 섹션에서 클릭 **Salesforce 구성** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="9847f-167">On hello **Salesforce Configuration** section, click **Configure Salesforce** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="9847f-168">복사 hello **SAML Single Sign-on 서비스 URL 및 엔터티 ID가 SAML** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="9847f-168">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span> 

    <span data-ttu-id="9847f-169">![Single Sign-On 구성](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="9847f-169">![Configure Single Sign-On](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_configure.png) 
<CS></span></span>
7.  <span data-ttu-id="9847f-170">브라우저에서 새 탭을 열고 tooyour Salesforce 관리자 계정에에서 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-170">Open a new tab in your browser and log in tooyour Salesforce administrator account.</span></span>

8.  <span data-ttu-id="9847f-171">Hello에서 **관리자** 탐색 창에서 클릭 **보안 제어** tooexpand hello 관련 섹션.</span><span class="sxs-lookup"><span data-stu-id="9847f-171">Under hello **Administrator** navigation pane, click **Security Controls** tooexpand hello related section.</span></span> <span data-ttu-id="9847f-172">그런 다음 **Single Sign-On 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-172">Then click **Single Sign-On Settings**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso.png)

9.  <span data-ttu-id="9847f-174">Hello에 **Single Sign On 설정** 페이지에서 hello **편집** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-174">On hello **Single Sign-On Settings** page, click hello **Edit** button.</span></span>
    <span data-ttu-id="9847f-175">![Single Sign-On 구성](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-edit.png)</span><span class="sxs-lookup"><span data-stu-id="9847f-175">![Configure Single Sign-On](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-edit.png)</span></span>

      > [!NOTE]
      > <span data-ttu-id="9847f-176">Toocontact를 할 수 없습니다 tooenable Single Sign On 설정 Salesforce 계정에 대 한 경우 [Salesforce 클라이언트 지원 팀](https://help.salesforce.com/support)합니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-176">If you are unable tooenable Single Sign-On settings for your Salesforce account, you may need toocontact [Salesforce Client support team](https://help.salesforce.com/support).</span></span> 

10. <span data-ttu-id="9847f-177">**SAML 사용**을 선택한 다음 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-177">Select **SAML Enabled**, and then click **Save**.</span></span>

      ![Single Sign-on 구성](./media/active-directory-saas-salesforce-tutorial/sf-enable-saml.png)
11. <span data-ttu-id="9847f-179">tooconfigure SAML single sign on 설정을, 클릭 **새로**합니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-179">tooconfigure your SAML single sign-on settings, click **New**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-new.png)

12. <span data-ttu-id="9847f-181">Hello에 **SAML Single Sign-on 설정 편집** 페이지에서 확인 하는 구성을 따르고 hello:</span><span class="sxs-lookup"><span data-stu-id="9847f-181">On hello **SAML Single Sign-On Setting Edit** page, make hello following configurations:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-salesforce-tutorial/sf-saml-config.png)

    <span data-ttu-id="9847f-183">a.</span><span class="sxs-lookup"><span data-stu-id="9847f-183">a.</span></span> <span data-ttu-id="9847f-184">Hello에 대 한 **이름** 필드에서이 구성에 대 한 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-184">For hello **Name** field, type in a friendly name for this configuration.</span></span> <span data-ttu-id="9847f-185">에 대 한 값을 제공 하 **이름** hello를 자동으로 채울 **API 이름** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-185">Providing a value for **Name** automatically populate hello **API Name** textbox.</span></span>

    <span data-ttu-id="9847f-186">b.</span><span class="sxs-lookup"><span data-stu-id="9847f-186">b.</span></span> <span data-ttu-id="9847f-187">붙여넣기 **SMAL 엔터티 ID** hello에 값 **발급자** Salesforce에서 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-187">Paste **SMAL Entity ID** value into hello **Issuer** field in Salesforce.</span></span>

    <span data-ttu-id="9847f-188">c.</span><span class="sxs-lookup"><span data-stu-id="9847f-188">c.</span></span> <span data-ttu-id="9847f-189">Hello에 **엔터티 Id 텍스트 상자에 붙여넣습니다**를 hello 패턴을 사용 하 여 Salesforce 도메인 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-189">In hello **Entity Id textbox**, type your Salesforce domain name using hello following pattern:</span></span>
      
      * <span data-ttu-id="9847f-190">엔터프라이즈 계정: `https://<subdomain>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="9847f-190">Enterprise account: `https://<subdomain>.my.salesforce.com`</span></span>
      * <span data-ttu-id="9847f-191">개발자 계정: `https://<subdomain>-dev-ed.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="9847f-191">Developer account: `https://<subdomain>-dev-ed.my.salesforce.com`</span></span>
      
    <span data-ttu-id="9847f-192">d.</span><span class="sxs-lookup"><span data-stu-id="9847f-192">d.</span></span> <span data-ttu-id="9847f-193">클릭 **찾아보기** 또는 **파일 선택** tooopen hello **파일 선택 tooUpload** 대화 상자에서 Salesforce 인증서를 선택한 다음 클릭 **열고**tooupload hello 인증서입니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-193">Click **Browse** or **Choose File** tooopen hello **Choose File tooUpload** dialog, select your Salesforce certificate, and then click **Open** tooupload hello certificate.</span></span>

    <span data-ttu-id="9847f-194">e.</span><span class="sxs-lookup"><span data-stu-id="9847f-194">e.</span></span> <span data-ttu-id="9847f-195">**SAML ID 형식**에서 **어설션에 사용자의 salesforce.com 사용자 이름 포함**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-195">For **SAML Identity Type**, select **Assertion contains User's salesforce.com username**.</span></span>

    <span data-ttu-id="9847f-196">f.</span><span class="sxs-lookup"><span data-stu-id="9847f-196">f.</span></span> <span data-ttu-id="9847f-197">에 대 한 **SAML Id 위치**선택, **hello hello Subject 문의 NameIdentifier 요소에 Id가**</span><span class="sxs-lookup"><span data-stu-id="9847f-197">For **SAML Identity Location**, select **Identity is in hello NameIdentifier element of hello Subject statement**</span></span>

    <span data-ttu-id="9847f-198">g.</span><span class="sxs-lookup"><span data-stu-id="9847f-198">g.</span></span> <span data-ttu-id="9847f-199">붙여넣기 **Single Sign-on 서비스 URL** hello에 **Id 공급자 로그인 URL** Salesforce에서 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-199">Paste **Single Sign-On Service URL** into hello **Identity Provider Login URL** field in Salesforce.</span></span>
    
    <span data-ttu-id="9847f-200">h.</span><span class="sxs-lookup"><span data-stu-id="9847f-200">h.</span></span> <span data-ttu-id="9847f-201">**서비스 공급자가 시작한 요청 바인딩**에서 **HTTP 리디렉션**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-201">For **Service Provider Initiated Request Binding**, select **HTTP Redirect**.</span></span>
    
    <span data-ttu-id="9847f-202">i.</span><span class="sxs-lookup"><span data-stu-id="9847f-202">i.</span></span> <span data-ttu-id="9847f-203">마지막으로, 클릭 **저장** tooapply 프로그램 SAML single sign on 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-203">Finally, click **Save** tooapply your SAML single sign-on settings.</span></span>

13. <span data-ttu-id="9847f-204">Salesforce에서 hello 왼쪽된 탐색 창에서 클릭 **도메인 관리** tooexpand hello 관련된 섹션을 클릭 하 고 **내 도메인**합니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-204">On hello left navigation pane in Salesforce, click **Domain Management** tooexpand hello related section, and then click **My Domain**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-salesforce-tutorial/sf-my-domain.png)

14. <span data-ttu-id="9847f-206">Toohello 아래로 스크롤하여 **인증 구성** 섹션을 hello 클릭 **편집** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-206">Scroll down toohello **Authentication Configuration** section, and click hello **Edit** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-salesforce-tutorial/sf-edit-auth-config.png)

15. <span data-ttu-id="9847f-208">Hello에 **인증 서비스** 섹션 hello SAML SSO 구성의 이름을 선택한 다음 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-208">In hello **Authentication Service** section, select hello friendly name of your SAML SSO configuration, and then click **Save**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-salesforce-tutorial/sf-auth-config.png)

    > [!NOTE]
    > <span data-ttu-id="9847f-210">둘 이상의 인증 서비스를 선택 하면 사용자가 원하는 되는 인증 서비스 증명된 tooselect single sign on tooyour Salesforce 환경을 시작 하는 동안 사용 하 여 toosign 합니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-210">If more than one authentication service is selected, users are prompted tooselect which authentication service they like toosign in with while initiating single sign-on tooyour Salesforce environment.</span></span> <span data-ttu-id="9847f-211">Toohappen, 원하는 하지 않는 경우 다음을 수행 해야 **다른 모든 인증 서비스를 선택 된 상태로 유지**합니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-211">If you don’t want it toohappen, then you should **leave all other authentication services unchecked**.</span></span>
<CE>    
> [!TIP]
> <span data-ttu-id="9847f-212">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="9847f-212">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="9847f-213">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="9847f-213">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="9847f-214">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9847f-214">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9847f-215">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="9847f-215">Creating an Azure AD test user</span></span>
<span data-ttu-id="9847f-216">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-216">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="9847f-218">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="9847f-218">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9847f-219">왼쪽된 탐색 창의 hello에 hello **Azure 포털**, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-219">On hello left navigation pane in hello **Azure portal**, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-salesforce-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9847f-221">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-221">toodisplay hello list of users, Go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-salesforce-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9847f-223">Hello 대화의 hello 위쪽 클릭 **추가** tooopen hello **사용자** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="9847f-223">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-salesforce-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9847f-225">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-225">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-salesforce-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9847f-227">a.</span><span class="sxs-lookup"><span data-stu-id="9847f-227">a.</span></span> <span data-ttu-id="9847f-228">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-228">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9847f-229">b.</span><span class="sxs-lookup"><span data-stu-id="9847f-229">b.</span></span> <span data-ttu-id="9847f-230">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-230">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9847f-231">c.</span><span class="sxs-lookup"><span data-stu-id="9847f-231">c.</span></span> <span data-ttu-id="9847f-232">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-232">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="9847f-233">d.</span><span class="sxs-lookup"><span data-stu-id="9847f-233">d.</span></span> <span data-ttu-id="9847f-234">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-234">Click **Create**.</span></span>
 
### <a name="creating-a-salesforce-test-user"></a><span data-ttu-id="9847f-235">Salesforce 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="9847f-235">Creating a Salesforce test user</span></span>

<span data-ttu-id="9847f-236">이 섹션에서는 Salesforce에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-236">In this section, a user called Britta Simon is created in Salesforce.</span></span> <span data-ttu-id="9847f-237">Salesforce는 기본적으로 설정되는 Just-In-Time 프로비전을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-237">Salesforce supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="9847f-238">이 섹션에 작업 항목이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-238">There is no action item for you in this section.</span></span> <span data-ttu-id="9847f-239">사용자는 Salesforce에서 존재 하지 않는, 경우에 새 tooaccess Salesforce를 시도할 때 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-239">If a user doesn't already exist in Salesforce, a new one is created when you attempt tooaccess Salesforce.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="9847f-240">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-240">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="9847f-241">이 섹션에서는 tooSalesforce 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-241">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSalesforce.</span></span>

![사용자 할당][200] 

<span data-ttu-id="9847f-243">**tooassign Britta Simon tooSalesforce hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="9847f-243">**tooassign Britta Simon tooSalesforce, perform hello following steps:**</span></span>

1. <span data-ttu-id="9847f-244">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-244">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="9847f-246">Hello 응용 프로그램 목록에서 선택 **Salesforce**합니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-246">In hello applications list, select **Salesforce**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_app.png) 

3. <span data-ttu-id="9847f-248">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-248">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="9847f-250">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-250">Click **Add** button.</span></span> <span data-ttu-id="9847f-251">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-251">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="9847f-253">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-253">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9847f-254">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-254">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9847f-255">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-255">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9847f-256">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="9847f-256">Testing single sign-on</span></span>

<span data-ttu-id="9847f-257">tootest single sign on 설정에 열기 hello 액세스 패널에 [https://myapps.microsoft.com](https://myapps.microsoft.com/)hello 테스트의 계정으로 로그인 하 고 클릭 **Salesforce**합니다.</span><span class="sxs-lookup"><span data-stu-id="9847f-257">tootest your single sign-on settings, open hello Access Panel at [https://myapps.microsoft.com](https://myapps.microsoft.com/), then sign into hello test account, and click **Salesforce**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9847f-258">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="9847f-258">Additional resources</span></span>

* [<span data-ttu-id="9847f-259">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="9847f-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9847f-260">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="9847f-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="9847f-261">사용자 프로비저닝 구성</span><span class="sxs-lookup"><span data-stu-id="9847f-261">Configure User Provisioning</span></span>](active-directory-saas-salesforce-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_203.png

