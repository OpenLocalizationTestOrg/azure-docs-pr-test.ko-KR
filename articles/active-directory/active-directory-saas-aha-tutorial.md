---
title: "자습서: Aha!와 Azure Active Directory 통합 | Microsoft Docs"
description: "단일 로그온 tooconfigure 방법을 알아보려면 Azure Active Directory와 Aha!입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ad955d3d-896a-41bb-800d-68e8cb5ff48d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: d844db3c0a035560e6fb275017215171743fba56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-aha"></a><span data-ttu-id="06bce-104">자습서: Aha!와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="06bce-104">Tutorial: Azure Active Directory integration with Aha!</span></span>

<span data-ttu-id="06bce-105">이 자습서에 설명 어떻게 toointegrate Aha!</span><span class="sxs-lookup"><span data-stu-id="06bce-105">In this tutorial, you learn how toointegrate Aha!</span></span> <span data-ttu-id="06bce-106">azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="06bce-106">with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="06bce-107">통합 Aha!</span><span class="sxs-lookup"><span data-stu-id="06bce-107">Integrating Aha!</span></span> <span data-ttu-id="06bce-108">Azure AD와 이점을 다음 hello로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="06bce-108">with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="06bce-109">액세스 tooAha을 지닌 Azure AD에서 제어할 수 있습니다!</span><span class="sxs-lookup"><span data-stu-id="06bce-109">You can control in Azure AD who has access tooAha!</span></span>
- <span data-ttu-id="06bce-110">에 사용자가 tooautomatically get 로그온 tooAha 사용 하도록 설정할 수 있습니다!</span><span class="sxs-lookup"><span data-stu-id="06bce-110">You can enable your users tooautomatically get signed-on tooAha!</span></span> <span data-ttu-id="06bce-111">Azure AD 계정이 포함된 (Single Sign-On)</span><span class="sxs-lookup"><span data-stu-id="06bce-111">(Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="06bce-112">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06bce-112">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="06bce-113">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="06bce-113">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="06bce-114">필수 조건</span><span class="sxs-lookup"><span data-stu-id="06bce-114">Prerequisites</span></span>

<span data-ttu-id="06bce-115">tooconfigure Azure AD 통합와 Aha!, hello 다음 항목을 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="06bce-115">tooconfigure Azure AD integration with Aha!, you need hello following items:</span></span>

- <span data-ttu-id="06bce-116">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="06bce-116">An Azure AD subscription</span></span>
- <span data-ttu-id="06bce-117">Aha!</span><span class="sxs-lookup"><span data-stu-id="06bce-117">An Aha!</span></span> <span data-ttu-id="06bce-118">Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="06bce-118">single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="06bce-119">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="06bce-119">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="06bce-120">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06bce-120">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="06bce-121">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="06bce-121">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="06bce-122">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06bce-122">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="06bce-123">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="06bce-123">Scenario description</span></span>
<span data-ttu-id="06bce-124">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="06bce-124">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="06bce-125">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06bce-125">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="06bce-126">추가 Aha!</span><span class="sxs-lookup"><span data-stu-id="06bce-126">Adding Aha!</span></span> <span data-ttu-id="06bce-127">hello 갤러리에서</span><span class="sxs-lookup"><span data-stu-id="06bce-127">from hello gallery</span></span>
2. <span data-ttu-id="06bce-128">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="06bce-128">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-aha-from-hello-gallery"></a><span data-ttu-id="06bce-129">추가 Aha!</span><span class="sxs-lookup"><span data-stu-id="06bce-129">Adding Aha!</span></span> <span data-ttu-id="06bce-130">hello 갤러리에서</span><span class="sxs-lookup"><span data-stu-id="06bce-130">from hello gallery</span></span>
<span data-ttu-id="06bce-131">Aha tooconfigure hello 통합!</span><span class="sxs-lookup"><span data-stu-id="06bce-131">tooconfigure hello integration of Aha!</span></span> <span data-ttu-id="06bce-132">Azure AD에 필요한 tooadd Aha!</span><span class="sxs-lookup"><span data-stu-id="06bce-132">into Azure AD, you need tooadd Aha!</span></span> <span data-ttu-id="06bce-133">hello 갤러리 tooyour 목록에서 관리 되는 SaaS 앱.</span><span class="sxs-lookup"><span data-stu-id="06bce-133">from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="06bce-134">**tooadd Aha! hello 갤러리 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="06bce-134">**tooadd Aha! from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="06bce-135">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="06bce-135">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="06bce-137">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="06bce-137">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="06bce-138">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="06bce-138">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="06bce-140">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="06bce-140">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="06bce-142">Hello 검색 상자에 입력 **Aha!**합니다.</span><span class="sxs-lookup"><span data-stu-id="06bce-142">In hello search box, type **Aha!**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-aha-tutorial/tutorial_aha_search.png)

5. <span data-ttu-id="06bce-144">Hello 결과 패널에서 선택 **Aha!**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="06bce-144">In hello results panel, select **Aha!**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-aha-tutorial/tutorial_aha_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="06bce-146">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="06bce-146">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="06bce-147">이 섹션에서는 구성 및 Azure AD single sign-on 테스트와 Aha!</span><span class="sxs-lookup"><span data-stu-id="06bce-147">In this section, you configure and test Azure AD single sign-on with Aha!</span></span> <span data-ttu-id="06bce-148">"Britta Simon." 이라는 테스트 사용자</span><span class="sxs-lookup"><span data-stu-id="06bce-148">based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="06bce-149">Single sign on toowork에 대 한 Azure AD에서 Aha hello 테이블에 해당 사용자 tooknow을 해야 합니다!</span><span class="sxs-lookup"><span data-stu-id="06bce-149">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Aha!</span></span> <span data-ttu-id="06bce-150">Azure ad에서는 tooa 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="06bce-150">is tooa user in Azure AD.</span></span> <span data-ttu-id="06bce-151">즉, Azure AD 사용자와 Aha에 hello 관련된 사용자 간의 링크 관계!</span><span class="sxs-lookup"><span data-stu-id="06bce-151">In other words, a link relationship between an Azure AD user and hello related user in Aha!</span></span> <span data-ttu-id="06bce-152">toobe 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06bce-152">needs toobe established.</span></span>

<span data-ttu-id="06bce-153">Aha!, hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계.</span><span class="sxs-lookup"><span data-stu-id="06bce-153">In Aha!, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="06bce-154">단일 로그온 tooconfigure 및 Azure AD 테스트와 Aha!, 구성 요소를 다음 toocomplete hello 필요:</span><span class="sxs-lookup"><span data-stu-id="06bce-154">tooconfigure and test Azure AD single sign-on with Aha!, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="06bce-155">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="06bce-155">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="06bce-156">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="06bce-156">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="06bce-157">**[만들기는 Aha! 테스트 사용자](#creating-an-aha-test-user)**  -toohave Britta Simon Aha에 상응 하는!</span><span class="sxs-lookup"><span data-stu-id="06bce-157">**[Creating an Aha! test user](#creating-an-aha-test-user)** - toohave a counterpart of Britta Simon in Aha!</span></span> <span data-ttu-id="06bce-158">연결 된 toohello 사용자의 Azure AD 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="06bce-158">that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="06bce-159">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="06bce-159">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="06bce-160">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="06bce-160">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="06bce-161">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="06bce-161">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="06bce-162">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 Aha에서 single sign on 구성!</span><span class="sxs-lookup"><span data-stu-id="06bce-162">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Aha!</span></span> <span data-ttu-id="06bce-163">응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="06bce-163">application.</span></span>

<span data-ttu-id="06bce-164">**tooconfigure Azure AD에서 single sign-on와 Aha!, hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="06bce-164">**tooconfigure Azure AD single sign-on with Aha!, perform hello following steps:**</span></span>

1. <span data-ttu-id="06bce-165">Hello hello에 Azure 포털에서에서 **Aha!**</span><span class="sxs-lookup"><span data-stu-id="06bce-165">In hello Azure portal, on hello **Aha!**</span></span> <span data-ttu-id="06bce-166">응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="06bce-166">application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="06bce-168">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="06bce-168">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-aha-tutorial/tutorial_aha_samlbase.png)

3. <span data-ttu-id="06bce-170">Hello에 **Aha! 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="06bce-170">On hello **Aha! Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-aha-tutorial/tutorial_aha_url.png)

    <span data-ttu-id="06bce-172">a.</span><span class="sxs-lookup"><span data-stu-id="06bce-172">a.</span></span> <span data-ttu-id="06bce-173">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<companyname>.aha.io/session/new`</span><span class="sxs-lookup"><span data-stu-id="06bce-173">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.aha.io/session/new`</span></span>

    <span data-ttu-id="06bce-174">b.</span><span class="sxs-lookup"><span data-stu-id="06bce-174">b.</span></span> <span data-ttu-id="06bce-175">Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<companyname>.aha.io`</span><span class="sxs-lookup"><span data-stu-id="06bce-175">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.aha.io`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="06bce-176">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="06bce-176">These values are not real.</span></span> <span data-ttu-id="06bce-177">이러한 항목을 업데이트 로그온 URL과 식별자 실제 hello로 값입니다.</span><span class="sxs-lookup"><span data-stu-id="06bce-177">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="06bce-178">연락처 [Aha! 클라이언트 지원 팀](https://www.aha.io/company/contact) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="06bce-178">Contact [Aha! Client support team](https://www.aha.io/company/contact) tooget these values.</span></span> 
 
4. <span data-ttu-id="06bce-179">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello 메타 데이터 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="06bce-179">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-aha-tutorial/tutorial_aha_certificate.png) 

5. <span data-ttu-id="06bce-181">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="06bce-181">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-aha-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="06bce-183">다른 웹 브라우저 창에서 로그인 tooyour Aha!</span><span class="sxs-lookup"><span data-stu-id="06bce-183">In a different web browser window, log in tooyour Aha!</span></span> <span data-ttu-id="06bce-184">회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="06bce-184">company site as an administrator.</span></span>

7. <span data-ttu-id="06bce-185">Hello 메뉴에서 hello 위에 표시를 클릭 **설정을**합니다.</span><span class="sxs-lookup"><span data-stu-id="06bce-185">In hello menu on hello top, click **Settings**.</span></span>

    <span data-ttu-id="06bce-186">![설정](./media/active-directory-saas-aha-tutorial/IC798950.png "설정")</span><span class="sxs-lookup"><span data-stu-id="06bce-186">![Settings](./media/active-directory-saas-aha-tutorial/IC798950.png "Settings")</span></span>

8. <span data-ttu-id="06bce-187">**계정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="06bce-187">Click **Account**.</span></span>
   
    <span data-ttu-id="06bce-188">![프로필](./media/active-directory-saas-aha-tutorial/IC798951.png "프로필")</span><span class="sxs-lookup"><span data-stu-id="06bce-188">![Profile](./media/active-directory-saas-aha-tutorial/IC798951.png "Profile")</span></span>

9. <span data-ttu-id="06bce-189">**보안 및 single sign-on**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="06bce-189">Click **Security and single sign-on**.</span></span>
   
    <span data-ttu-id="06bce-190">![보안 및 Single Sign-On](./media/active-directory-saas-aha-tutorial/IC798952.png "보안 및 Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="06bce-190">![Security and single sign-on](./media/active-directory-saas-aha-tutorial/IC798952.png "Security and single sign-on")</span></span>

10. <span data-ttu-id="06bce-191">**Single Sign-On** 섹션에서 **ID 공급자**로 **SAML2.0**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="06bce-191">In **Single Sign-On** section, as **Identity Provider**, select **SAML2.0**.</span></span>
   
    <span data-ttu-id="06bce-192">![보안 및 Single Sign-On](./media/active-directory-saas-aha-tutorial/IC798953.png "보안 및 Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="06bce-192">![Security and single sign-on](./media/active-directory-saas-aha-tutorial/IC798953.png "Security and single sign-on")</span></span>

11. <span data-ttu-id="06bce-193">Hello에 **Single Sign On** 구성 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="06bce-193">On hello **Single Sign-On** configuration page, perform hello following steps:</span></span>
    
    <span data-ttu-id="06bce-194">![Single Sign-On](./media/active-directory-saas-aha-tutorial/IC798954.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="06bce-194">![Single Sign-On](./media/active-directory-saas-aha-tutorial/IC798954.png "Single Sign-On")</span></span>
    
       <span data-ttu-id="06bce-195">a.</span><span class="sxs-lookup"><span data-stu-id="06bce-195">a.</span></span> <span data-ttu-id="06bce-196">Hello에 **이름** 텍스트 상자, 구성에 대 한 이름 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="06bce-196">In hello **Name** textbox, type a name for your configuration.</span></span>

       <span data-ttu-id="06bce-197">b.</span><span class="sxs-lookup"><span data-stu-id="06bce-197">b.</span></span> <span data-ttu-id="06bce-198">**구성 사용 형식**에 **메타데이터 파일**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="06bce-198">For **Configure using**, select **Metadata File**.</span></span>
   
       <span data-ttu-id="06bce-199">c.</span><span class="sxs-lookup"><span data-stu-id="06bce-199">c.</span></span> <span data-ttu-id="06bce-200">tooupload 다운로드 한 메타 데이터 파일을 클릭 하 여 **찾아보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="06bce-200">tooupload your downloaded metadata file, click **Browse**.</span></span>
   
       <span data-ttu-id="06bce-201">d.</span><span class="sxs-lookup"><span data-stu-id="06bce-201">d.</span></span> <span data-ttu-id="06bce-202">**업데이트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="06bce-202">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="06bce-203">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="06bce-203">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="06bce-204">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="06bce-204">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="06bce-205">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="06bce-205">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="06bce-206">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="06bce-206">Creating an Azure AD test user</span></span>
<span data-ttu-id="06bce-207">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="06bce-207">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="06bce-209">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="06bce-209">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="06bce-210">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="06bce-210">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-aha-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="06bce-212">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="06bce-212">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-aha-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="06bce-214">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="06bce-214">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-aha-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="06bce-216">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="06bce-216">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-aha-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="06bce-218">a.</span><span class="sxs-lookup"><span data-stu-id="06bce-218">a.</span></span> <span data-ttu-id="06bce-219">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="06bce-219">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="06bce-220">b.</span><span class="sxs-lookup"><span data-stu-id="06bce-220">b.</span></span> <span data-ttu-id="06bce-221">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="06bce-221">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="06bce-222">c.</span><span class="sxs-lookup"><span data-stu-id="06bce-222">c.</span></span> <span data-ttu-id="06bce-223">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="06bce-223">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="06bce-224">d.</span><span class="sxs-lookup"><span data-stu-id="06bce-224">d.</span></span> <span data-ttu-id="06bce-225">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="06bce-225">Click **Create**.</span></span>
 
### <a name="creating-an-aha-test-user"></a><span data-ttu-id="06bce-226">만들기는 Aha!</span><span class="sxs-lookup"><span data-stu-id="06bce-226">Creating an Aha!</span></span> <span data-ttu-id="06bce-227">테스트 사용자</span><span class="sxs-lookup"><span data-stu-id="06bce-227">test user</span></span>

<span data-ttu-id="06bce-228">tooenable Azure AD 사용자가 toolog tooAha에!, Aha에 프로 비전 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06bce-228">tooenable Azure AD users toolog in tooAha!, they must be provisioned into Aha!.</span></span>  

<span data-ttu-id="06bce-229">Hello 경우 Aha!, 프로 비전은 자동화 된 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="06bce-229">In hello case of Aha!, provisioning is an automated task.</span></span> <span data-ttu-id="06bce-230">작업 항목이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="06bce-230">There is no action item for you.</span></span>

<span data-ttu-id="06bce-231">사용자가 필요한 경우 hello 첫 번째 single sign on 시도 하는 동안 자동으로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="06bce-231">Users are automatically created if necessary during hello first single sign-on attempt.</span></span>

>[!NOTE]
><span data-ttu-id="06bce-232">다른 Aha! 사용자 계정 생성 도구</span><span class="sxs-lookup"><span data-stu-id="06bce-232">You can use any other Aha!</span></span> <span data-ttu-id="06bce-233">또는 Aha!가 제공한 API를 사용하여 AAD 사용자 계정을</span><span class="sxs-lookup"><span data-stu-id="06bce-233">user account creation tools or APIs provided by Aha!</span></span> <span data-ttu-id="06bce-234">tooprovision AAD 사용자 계정을 합니다.</span><span class="sxs-lookup"><span data-stu-id="06bce-234">tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="06bce-235">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="06bce-235">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="06bce-236">이 섹션에서는 Azure에서 single sign-on Britta Simon toouse tooAha 액세스 권한을 부여 하 여 사용 하면!입니다.</span><span class="sxs-lookup"><span data-stu-id="06bce-236">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAha!.</span></span>

![사용자 할당][200] 

<span data-ttu-id="06bce-238">**tooassign Britta Simon tooAha!, hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="06bce-238">**tooassign Britta Simon tooAha!, perform hello following steps:**</span></span>

1. <span data-ttu-id="06bce-239">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="06bce-239">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="06bce-241">Hello 응용 프로그램 목록에서 선택 **Aha!**합니다.</span><span class="sxs-lookup"><span data-stu-id="06bce-241">In hello applications list, select **Aha!**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-aha-tutorial/tutorial_aha_app.png) 

3. <span data-ttu-id="06bce-243">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="06bce-243">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="06bce-245">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="06bce-245">Click **Add** button.</span></span> <span data-ttu-id="06bce-246">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="06bce-246">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="06bce-248">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06bce-248">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="06bce-249">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="06bce-249">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="06bce-250">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="06bce-250">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="06bce-251">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="06bce-251">Testing single sign-on</span></span>

<span data-ttu-id="06bce-252">Single sign on 설정 tootest 원하는 hello 액세스 패널을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="06bce-252">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="06bce-253">액세스 패널 hello에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="06bce-253">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="06bce-254">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="06bce-254">Additional resources</span></span>

* [<span data-ttu-id="06bce-255">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="06bce-255">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="06bce-256">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="06bce-256">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-aha-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-aha-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-aha-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-aha-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-aha-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-aha-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-aha-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-aha-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-aha-tutorial/tutorial_general_203.png

