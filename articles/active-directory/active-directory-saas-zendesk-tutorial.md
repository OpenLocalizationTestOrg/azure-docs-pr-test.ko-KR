---
title: "자습서: Azure Active Directory와 Zendesk 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Zendesk 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9d7c91e5-78f5-4016-862f-0f3242b00680
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 46ccd57a4adeb810af459caaa1e592cf2b62cb8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zendesk"></a><span data-ttu-id="93840-103">자습서:Azure Active Directory와 Zendesk 통합</span><span class="sxs-lookup"><span data-stu-id="93840-103">Tutorial: Azure Active Directory integration with Zendesk</span></span>

<span data-ttu-id="93840-104">이 자습서에 설명 어떻게 toointegrate Zendesk와 Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="93840-104">In this tutorial, you learn how toointegrate Zendesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="93840-105">Azure AD와 Zendesk 통합 이점을 다음 hello로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="93840-105">Integrating Zendesk with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="93840-106">액세스 tooZendesk을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93840-106">You can control in Azure AD who has access tooZendesk</span></span>
- <span data-ttu-id="93840-107">프로그램 사용자 tooautomatically get 로그온 tooZendesk (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93840-107">You can enable your users tooautomatically get signed-on tooZendesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="93840-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93840-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="93840-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="93840-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="93840-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="93840-110">Prerequisites</span></span>

<span data-ttu-id="93840-111">Zendesk와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="93840-111">tooconfigure Azure AD integration with Zendesk, you need hello following items:</span></span>

- <span data-ttu-id="93840-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="93840-112">An Azure AD subscription</span></span>
- <span data-ttu-id="93840-113">Zendesk Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="93840-113">A Zendesk single sign-on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="93840-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="93840-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="93840-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="93840-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="93840-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="93840-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="93840-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93840-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="93840-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="93840-118">Scenario description</span></span>
<span data-ttu-id="93840-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="93840-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="93840-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93840-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="93840-121">Zendesk은 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="93840-121">Adding Zendesk from hello gallery</span></span>
2. <span data-ttu-id="93840-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="93840-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-zendesk-from-hello-gallery"></a><span data-ttu-id="93840-123">Zendesk은 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="93840-123">Adding Zendesk from hello gallery</span></span>
<span data-ttu-id="93840-124">tooconfigure hello와의 통합 Zendesk Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Zendesk tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="93840-124">tooconfigure hello integration of Zendesk into Azure AD, you need tooadd Zendesk from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="93840-125">**hello 갤러리에서 Zendesk tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="93840-125">**tooadd Zendesk from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="93840-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="93840-126">In hello **[Azure Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="93840-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="93840-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="93840-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="93840-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="93840-131">클릭 **새 응용 프로그램** hello 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="93840-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="93840-133">Hello 검색 상자에 입력 **Zendesk**합니다.</span><span class="sxs-lookup"><span data-stu-id="93840-133">In hello search box, type **Zendesk**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_search.png)

5. <span data-ttu-id="93840-135">Hello 결과 패널에서 선택 **Zendesk**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="93840-135">In hello results panel, select **Zendesk**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="93840-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="93840-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="93840-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Zendesk에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="93840-138">In this section, you configure and test Azure AD single sign-on with Zendesk based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="93840-139">Single sign on toowork에 대 한 Azure AD는 tooknow Zendesk에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="93840-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Zendesk is tooa user in Azure AD.</span></span> <span data-ttu-id="93840-140">즉, Azure AD 사용자와 Zendesk에 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="93840-140">In other words, a link relationship between an Azure AD user and hello related user in Zendesk needs toobe established.</span></span>

<span data-ttu-id="93840-141">Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** Zendesk에 합니다.</span><span class="sxs-lookup"><span data-stu-id="93840-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Zendesk.</span></span>

<span data-ttu-id="93840-142">tooconfigure 및 Zendesk와 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="93840-142">tooconfigure and test Azure AD single sign-on with Zendesk, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="93840-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="93840-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="93840-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="93840-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="93840-145">**[Zendesk 테스트 사용자 만들기](#creating-a-zendesk-test-user)**  -toohave Britta Simon 표현인 연결 된 toohello Azure AD 사용자의 Zendesk에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="93840-145">**[Creating a Zendesk test user](#creating-a-zendesk-test-user)** - toohave a counterpart of Britta Simon in Zendesk that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="93840-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="93840-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="93840-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="93840-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="93840-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="93840-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="93840-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 Zendesk 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="93840-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Zendesk application.</span></span>

<span data-ttu-id="93840-150">**Azure AD tooconfigure single sign on와 Zendesk를 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="93840-150">**tooconfigure Azure AD single sign-on with Zendesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="93840-151">Hello hello에 Azure 포털에서에서 **Zendesk** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="93840-151">In hello Azure portal, on hello **Zendesk** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="93840-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="93840-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_samlbase.png)

3. <span data-ttu-id="93840-155">Hello에 **Zendesk 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="93840-155">On hello **Zendesk Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_url.png)

    <span data-ttu-id="93840-157">a.</span><span class="sxs-lookup"><span data-stu-id="93840-157">a.</span></span> <span data-ttu-id="93840-158">Hello에 **로그온 URL** hello 패턴을 사용 하 여 형식 hello 값 텍스트 상자:`https://<subdomain>.zendesk.com`</span><span class="sxs-lookup"><span data-stu-id="93840-158">In hello **Sign-on URL** textbox, type hello value using hello following pattern: `https://<subdomain>.zendesk.com`</span></span>

    <span data-ttu-id="93840-159">b.</span><span class="sxs-lookup"><span data-stu-id="93840-159">b.</span></span> <span data-ttu-id="93840-160">Hello에 **식별자** hello 패턴을 사용 하 여 형식 hello 값 텍스트 상자:`https://<subdomain>.zendesk.com`</span><span class="sxs-lookup"><span data-stu-id="93840-160">In hello **Identifier** textbox, type hello value using hello following pattern: `https://<subdomain>.zendesk.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="93840-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="93840-161">These values are not real.</span></span> <span data-ttu-id="93840-162">Hello 실제 로그온 URL과 식별자 URL 이러한 값을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="93840-162">Update these values with hello actual Sign-on URL and Identifier URL.</span></span> <span data-ttu-id="93840-163">연락처 [Zendesk 지원 팀](https://support.zendesk.com/hc/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="93840-163">Contact [Zendesk support team](https://support.zendesk.com/hc/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise) tooget these values.</span></span> 

4. <span data-ttu-id="93840-164">Zendesk에는 특정 형식의 hello SAML 어설션 합니다.</span><span class="sxs-lookup"><span data-stu-id="93840-164">Zendesk expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="93840-165">필수 SAML 특성이 없으면 하지만에서 특성을 추가할 수는 필요에 따라 **사용자 특성** 아래 단계 다음 hello 섹션:</span><span class="sxs-lookup"><span data-stu-id="93840-165">There are no mandatory SAML attributes but optionally you can add an attribute from **User Attributes** section by following hello below steps:</span></span> 

     ![Single Sign-on 구성](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_attributes1.png)

    <span data-ttu-id="93840-167">a.</span><span class="sxs-lookup"><span data-stu-id="93840-167">a.</span></span> <span data-ttu-id="93840-168">Hello 클릭 **보기 및 편집 hello 다른 특성** 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="93840-168">Click hello **View and edit all hello other attributes** check box.</span></span>
     
    ![Single Sign-on 구성](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_attributes2.png)
   
    <span data-ttu-id="93840-170">b.</span><span class="sxs-lookup"><span data-stu-id="93840-170">b.</span></span> <span data-ttu-id="93840-171">Hello 클릭 **특성 추가** tooopen **특성 추가** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="93840-171">Click hello **Add Attribute** tooopen **Add attribute** dialog.</span></span>
    
    ![Single Sign-on 구성](./media/active-directory-saas-zendesk-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="93840-173">c.</span><span class="sxs-lookup"><span data-stu-id="93840-173">c.</span></span> <span data-ttu-id="93840-174">Hello에 **이름** 형식 hello 특성 이름 텍스트 상자 (예를 들어 **emailaddress**).</span><span class="sxs-lookup"><span data-stu-id="93840-174">In hello **Name** textbox, type hello attribute name (for example **emailaddress**).</span></span>
    
    <span data-ttu-id="93840-175">d.</span><span class="sxs-lookup"><span data-stu-id="93840-175">d.</span></span> <span data-ttu-id="93840-176">Hello에서 **값** 선택 hello 특성 값 목록 (으로 **user.mail**).</span><span class="sxs-lookup"><span data-stu-id="93840-176">From hello **Value** list, select hello attribute value (as **user.mail**).</span></span>
    
    <span data-ttu-id="93840-177">e.</span><span class="sxs-lookup"><span data-stu-id="93840-177">e.</span></span> <span data-ttu-id="93840-178">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="93840-178">Click **Ok**</span></span>
 
    > [!NOTE] 
    > <span data-ttu-id="93840-179">기본적으로 Azure AD에 없는 확장 특성 tooadd 특성을 사용 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="93840-179">You use extension attributes tooadd attributes that are not in Azure AD by default.</span></span> <span data-ttu-id="93840-180">클릭 [saml에서 설정 될 수 있는 사용자 특성](https://support.zendesk.com/hc/en-us/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise-) tooget hello 전체 목록은 SAML 특성을 **Zendesk** 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="93840-180">Click [User attributes that can be set in SAML](https://support.zendesk.com/hc/en-us/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise-) tooget hello complete list of SAML attributes that **Zendesk** accepts.</span></span> 

5. <span data-ttu-id="93840-181">Hello에 **SAML 서명 인증서** 섹션을 복사 hello **지문** 인증서의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="93840-181">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_certificate.png) 

6. <span data-ttu-id="93840-183">Hello에 **Zendesk 구성** 섹션에서 클릭 **구성 Zendesk** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="93840-183">On hello **Zendesk Configuration** section, click **Configure Zendesk** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="93840-184">복사 hello **Sign-Out URL 및 SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="93840-184">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_configure.png) 

7. <span data-ttu-id="93840-186">다른 웹 브라우저 창에서 관리자 권한으로 Zendesk 회사 사이트에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="93840-186">In a different web browser window, log into your Zendesk company site as an administrator.</span></span>

8. <span data-ttu-id="93840-187">**Admin**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="93840-187">Click **Admin**.</span></span>

9. <span data-ttu-id="93840-188">Hello 왼쪽된 탐색 창에서 클릭 **설정**, 클릭 하 고 **보안**합니다.</span><span class="sxs-lookup"><span data-stu-id="93840-188">In hello left navigation pane, click **Settings**, and then click **Security**.</span></span>

10. <span data-ttu-id="93840-189">Hello에 **보안** 페이지 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="93840-189">On hello **Security** page, perform hello following steps:</span></span> 
   
     <span data-ttu-id="93840-190">![보안](./media/active-directory-saas-zendesk-tutorial/ic773089.png "보안")</span><span class="sxs-lookup"><span data-stu-id="93840-190">![Security](./media/active-directory-saas-zendesk-tutorial/ic773089.png "Security")</span></span>

    <span data-ttu-id="93840-191">![Single Sign-On](./media/active-directory-saas-zendesk-tutorial/ic773090.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="93840-191">![Single sign-on](./media/active-directory-saas-zendesk-tutorial/ic773090.png "Single sign-on")</span></span>

     <span data-ttu-id="93840-192">a.</span><span class="sxs-lookup"><span data-stu-id="93840-192">a.</span></span> <span data-ttu-id="93840-193">Hello 클릭 **관리 및 에이전트** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="93840-193">Click hello **Admin & Agents** tab.</span></span>

     <span data-ttu-id="93840-194">b.</span><span class="sxs-lookup"><span data-stu-id="93840-194">b.</span></span> <span data-ttu-id="93840-195">**SSO(Single Sign-On) 및 SAML**을 선택하고**SAML**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="93840-195">Select **Single sign-on (SSO) and SAML**, and then select **SAML**.</span></span>

     <span data-ttu-id="93840-196">c.</span><span class="sxs-lookup"><span data-stu-id="93840-196">c.</span></span> <span data-ttu-id="93840-197">**SAML SSO URL** 붙여넣기 hello 값의 텍스트 상자 **SAML Single Sign-on 서비스 URL** Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="93840-197">In **SAML SSO URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 

     <span data-ttu-id="93840-198">d.</span><span class="sxs-lookup"><span data-stu-id="93840-198">d.</span></span> <span data-ttu-id="93840-199">**원격 로그 아웃 URL** 붙여넣기 hello 값의 텍스트 상자 **Sign-Out URL** Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="93840-199">In **Remote Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
        
     <span data-ttu-id="93840-200">e.</span><span class="sxs-lookup"><span data-stu-id="93840-200">e.</span></span> <span data-ttu-id="93840-201">**인증서 지문** 텍스트 붙여넣기 hello **지문** Azure 포털에서 복사 하는 인증서의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="93840-201">In **Certificate Fingerprint** textbox, paste hello **Thumbprint** value of certificate which you have copied from Azure portal.</span></span>
     
     <span data-ttu-id="93840-202">f.</span><span class="sxs-lookup"><span data-stu-id="93840-202">f.</span></span> <span data-ttu-id="93840-203">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="93840-203">Click **Save**.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="93840-204">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="93840-204">Creating an Azure AD test user</span></span>
<span data-ttu-id="93840-205">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="93840-205">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="93840-207">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="93840-207">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="93840-208">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="93840-208">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-zendesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="93840-210">사용자의 toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="93840-210">toodisplay hello list of users go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-zendesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="93840-212">Hello 대화의 hello 위쪽 클릭 **추가** tooopen hello **사용자** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="93840-212">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-zendesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="93840-214">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="93840-214">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-zendesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="93840-216">a.</span><span class="sxs-lookup"><span data-stu-id="93840-216">a.</span></span> <span data-ttu-id="93840-217">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="93840-217">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="93840-218">b.</span><span class="sxs-lookup"><span data-stu-id="93840-218">b.</span></span> <span data-ttu-id="93840-219">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="93840-219">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="93840-220">c.</span><span class="sxs-lookup"><span data-stu-id="93840-220">c.</span></span> <span data-ttu-id="93840-221">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="93840-221">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="93840-222">d.</span><span class="sxs-lookup"><span data-stu-id="93840-222">d.</span></span> <span data-ttu-id="93840-223">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="93840-223">Click **Create**.</span></span> 

### <a name="creating-a-zendesk-test-user"></a><span data-ttu-id="93840-224">Zendesk 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="93840-224">Creating a Zendesk test user</span></span>

<span data-ttu-id="93840-225">에 tooenable Azure AD 사용자가 toolog **Zendesk**에 제공 해야 **Zendesk**합니다.</span><span class="sxs-lookup"><span data-stu-id="93840-225">tooenable Azure AD users toolog into **Zendesk**, they must be provisioned into **Zendesk**.</span></span>  
<span data-ttu-id="93840-226">Hello 앱에 할당 된 hello 역할에 따라 hello의 예상 되는 동작:</span><span class="sxs-lookup"><span data-stu-id="93840-226">Depending on hello role assigned in hello apps, it's hello expected behavior:</span></span>

 1. <span data-ttu-id="93840-227">**최종 사용자** 계정은 로그인할 때 자동으로 프로비전됩니다.</span><span class="sxs-lookup"><span data-stu-id="93840-227">**End-user** accounts are automatically provisioned when signing in.</span></span>
 2. <span data-ttu-id="93840-228">**에이전트** 및 **Admin** toobe에서 수동으로 프로 비전 해야 하는 계정이 **Zendesk** 로그인 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="93840-228">**Agent** and **Admin** accounts need toobe manually provisioned in **Zendesk** before signing in.</span></span>
 
<span data-ttu-id="93840-229">**tooprovision 사용자 계정을 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="93840-229">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="93840-230">Tooyour 로그인 **Zendesk** 테 넌 트입니다.</span><span class="sxs-lookup"><span data-stu-id="93840-230">Log in tooyour **Zendesk** tenant.</span></span>

2. <span data-ttu-id="93840-231">선택 hello **고객 목록** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="93840-231">Select hello **Customer List** tab.</span></span>

3. <span data-ttu-id="93840-232">선택 hello **사용자** 탭을 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="93840-232">Select hello **User** tab, and click **Add**.</span></span>
   
    <span data-ttu-id="93840-233">![사용자 추가](./media/active-directory-saas-zendesk-tutorial/ic773632.png "사용자 추가")</span><span class="sxs-lookup"><span data-stu-id="93840-233">![Add user](./media/active-directory-saas-zendesk-tutorial/ic773632.png "Add user")</span></span>
4. <span data-ttu-id="93840-234">Tooprovision을 클릭 한 다음 기존 Azure AD 계정의 전자 메일 주소 hello 입력 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="93840-234">Type hello email address of an existing Azure AD account you want tooprovision, and then click **Save**.</span></span>
   
    <span data-ttu-id="93840-235">![새 사용자](./media/active-directory-saas-zendesk-tutorial/ic773633.png "새 사용자")</span><span class="sxs-lookup"><span data-stu-id="93840-235">![New user](./media/active-directory-saas-zendesk-tutorial/ic773633.png "New user")</span></span>

> [!NOTE]
> <span data-ttu-id="93840-236">다른 Zendesk 사용자 계정 만들기 도구를 사용할 수 있습니다 또는 AAD 사용자 계정을 tooprovision Zendesk에서 제공 된 Api입니다.</span><span class="sxs-lookup"><span data-stu-id="93840-236">You can use any other Zendesk user account creation tools or APIs provided by Zendesk tooprovision AAD user accounts.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="93840-237">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="93840-237">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="93840-238">이 섹션에서는 tooZendesk 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="93840-238">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooZendesk.</span></span>

![사용자 할당][200] 

<span data-ttu-id="93840-240">**tooassign Britta Simon tooZendesk hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="93840-240">**tooassign Britta Simon tooZendesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="93840-241">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="93840-241">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="93840-243">Hello 응용 프로그램 목록에서 선택 **Zendesk**합니다.</span><span class="sxs-lookup"><span data-stu-id="93840-243">In hello applications list, select **Zendesk**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_app.png) 

3. <span data-ttu-id="93840-245">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="93840-245">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="93840-247">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="93840-247">Click **Add** button.</span></span> <span data-ttu-id="93840-248">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="93840-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="93840-250">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93840-250">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="93840-251">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="93840-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="93840-252">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="93840-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="93840-253">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="93840-253">Testing single sign-on</span></span>

<span data-ttu-id="93840-254">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93840-254">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="93840-255">Hello 액세스 패널에서에서 hello Zendesk 타일을 클릭할 때 자동으로 로그온 tooyour Zendesk 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="93840-255">When you click hello Zendesk tile in hello Access Panel, you should get automatically signed-on tooyour Zendesk application.</span></span>
<span data-ttu-id="93840-256">액세스 패널 hello에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="93840-256">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="93840-257">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="93840-257">Additional resources</span></span>

* [<span data-ttu-id="93840-258">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="93840-258">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="93840-259">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="93840-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_203.png
