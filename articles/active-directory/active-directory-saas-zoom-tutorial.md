---
title: "자습서: Azure Active Directory와 Zoom 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 확대/축소 합니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0ebdab6c-83a8-4737-a86a-974f37269c31
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 623a1f428ad1f0aa2c8205b79d61720cad5fc6a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zoom"></a><span data-ttu-id="958ec-103">자습서: Azure Active Directory와 Zoom 통합</span><span class="sxs-lookup"><span data-stu-id="958ec-103">Tutorial: Azure Active Directory integration with Zoom</span></span>

<span data-ttu-id="958ec-104">이 자습서에 설명 toointegrate Azure Active Directory (Azure AD)와 확대/축소는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-104">In this tutorial, you learn how toointegrate Zoom with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="958ec-105">확대/축소를 Azure AD와 통합 hello 다음 이점을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-105">Integrating Zoom with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="958ec-106">액세스 tooZoom을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-106">You can control in Azure AD who has access tooZoom.</span></span>
- <span data-ttu-id="958ec-107">에 사용자가 tooautomatically get 로그온 tooZoom (Single Sign-on)는 Azure AD 계정으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-107">You can enable your users tooautomatically get signed-on tooZoom (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="958ec-108">하나의 중앙 위치-hello Azure 포털에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="958ec-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="958ec-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="958ec-110">Prerequisites</span></span>

<span data-ttu-id="958ec-111">다음 항목 hello가 필요 tooconfigure Azure AD와 통합으로 확대/축소 합니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-111">tooconfigure Azure AD integration with Zoom, you need hello following items:</span></span>

- <span data-ttu-id="958ec-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="958ec-112">An Azure AD subscription</span></span>
- <span data-ttu-id="958ec-113">Zoom Single Sign-on이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="958ec-113">A Zoom single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="958ec-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="958ec-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="958ec-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="958ec-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="958ec-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="958ec-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="958ec-118">Scenario description</span></span>
<span data-ttu-id="958ec-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="958ec-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="958ec-121">확대/축소 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="958ec-121">Adding Zoom from hello gallery</span></span>
2. <span data-ttu-id="958ec-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="958ec-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zoom-from-hello-gallery"></a><span data-ttu-id="958ec-123">확대/축소 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="958ec-123">Adding Zoom from hello gallery</span></span>
<span data-ttu-id="958ec-124">Azure AD로 확대/축소, tooconfigure hello 통합 tooadd 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 확대/축소 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-124">tooconfigure hello integration of Zoom into Azure AD, you need tooadd Zoom from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="958ec-125">**hello 갤러리에서 확대/축소 tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="958ec-125">**tooadd Zoom from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="958ec-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![hello Azure Active Directory 단추][1]

2. <span data-ttu-id="958ec-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="958ec-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-129">Then go too**All applications**.</span></span>

    ![hello 엔터프라이즈 응용 프로그램 블레이드][2]
    
3. <span data-ttu-id="958ec-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![hello 새 응용 프로그램 단추][3]

4. <span data-ttu-id="958ec-133">Hello 검색 상자에 입력 **확대/축소**선택, **확대/축소** 결과 패널에서 클릭 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-133">In hello search box, type **Zoom**, select **Zoom** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Hello 결과 목록에서 확대/축소](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="958ec-135">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="958ec-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="958ec-136">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Zoom에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-136">In this section, you configure and test Azure AD single sign-on with Zoom based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="958ec-137">Single sign on toowork에 대 한 Azure AD는 tooknow 확대/축소에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Zoom is tooa user in Azure AD.</span></span> <span data-ttu-id="958ec-138">즉, Azure AD 사용자 및 확대/축소 요구 toobe 설정에서 hello 관련된 사용자 간 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-138">In other words, a link relationship between an Azure AD user and hello related user in Zoom needs toobe established.</span></span>

<span data-ttu-id="958ec-139">확대/축소에서 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-139">In Zoom, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="958ec-140">tooconfigure 및 확대/축소를 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-140">tooconfigure and test Azure AD single sign-on with Zoom, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="958ec-141">**[Azure AD Single Sign-on 구성](#configure-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="958ec-142">**[Azure AD 테스트를 만들고](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="958ec-143">**[확대/축소 테스트 사용자 만들기](#create-a-zoom-test-user)**  -toohave Britta Simon 표현인 연결 된 toohello Azure AD 사용자의 확대/축소에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-143">**[Create a Zoom test user](#create-a-zoom-test-user)** - toohave a counterpart of Britta Simon in Zoom that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="958ec-144">**[Azure AD hello 테스트 사용자를 할당](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="958ec-145">**[Single sign on 테스트](#test-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="958ec-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="958ec-146">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="958ec-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="958ec-147">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 확대/축소 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Zoom application.</span></span>

<span data-ttu-id="958ec-148">**확대/축소와 Azure AD에서 single sign-on tooconfigure hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="958ec-148">**tooconfigure Azure AD single sign-on with Zoom, perform hello following steps:**</span></span>

1. <span data-ttu-id="958ec-149">Hello hello에 Azure 포털에서에서 **확대/축소** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-149">In hello Azure portal, on hello **Zoom** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-On 구성 링크][4]

2. <span data-ttu-id="958ec-151">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_samlbase.png)

3. <span data-ttu-id="958ec-153">Hello에 **확대/축소 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-153">On hello **Zoom Domain and URLs** section, perform hello following steps:</span></span>

    ![Zoom 도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_url.png)

    <span data-ttu-id="958ec-155">a.</span><span class="sxs-lookup"><span data-stu-id="958ec-155">a.</span></span> <span data-ttu-id="958ec-156">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<companyname>.zoom.us`</span><span class="sxs-lookup"><span data-stu-id="958ec-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.zoom.us`</span></span>

    <span data-ttu-id="958ec-157">b.</span><span class="sxs-lookup"><span data-stu-id="958ec-157">b.</span></span> <span data-ttu-id="958ec-158">Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<companyname>.zoom.us`</span><span class="sxs-lookup"><span data-stu-id="958ec-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.zoom.us`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="958ec-159">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-159">These values are not real.</span></span> <span data-ttu-id="958ec-160">이러한 항목을 업데이트 로그온 URL과 식별자 실제 hello로 값입니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="958ec-161">연락처 [클라이언트 확대/축소 지원 팀](https://support.zoom.us/hc) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-161">Contact [Zoom Client support team](https://support.zoom.us/hc) tooget these values.</span></span> 
 
4. <span data-ttu-id="958ec-162">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **인증서 (Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-162">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![hello 인증서 다운로드 링크](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_certificate.png) 

5. <span data-ttu-id="958ec-164">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-164">Click **Save** button.</span></span>

    ![Single Sign-On 구성 저장 단추](./media/active-directory-saas-zoom-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="958ec-166">Hello에 **확대/축소 구성** 섹션에서 클릭 **구성 확대/축소** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="958ec-166">On hello **Zoom Configuration** section, click **Configure Zoom** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="958ec-167">복사 hello **Sign-Out URL, SAML 엔터티 ID, 및 SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="958ec-167">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Zoom 구성](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_configure.png) 

7. <span data-ttu-id="958ec-169">다른 웹 브라우저 창에서 관리자 권한으로 tooyour Zoom 회사 사이트에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-169">In a different web browser window, log in tooyour Zoom company site as an administrator.</span></span>

8. <span data-ttu-id="958ec-170">Hello 클릭 **Single Sign On** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-170">Click hello **Single Sign-On** tab.</span></span>
   
    <span data-ttu-id="958ec-171">![Single Sign-On 탭](./media/active-directory-saas-zoom-tutorial/IC784700.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="958ec-171">![Single sign-on tab](./media/active-directory-saas-zoom-tutorial/IC784700.png "Single sign-on")</span></span>

9. <span data-ttu-id="958ec-172">Hello 클릭 **보안 제어** 탭을 클릭 한 다음 toohello 이동 **Single Sign On** 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-172">Click hello **Security Control** tab, and then go toohello **Single Sign-On** settings.</span></span>

10. <span data-ttu-id="958ec-173">Hello Single Sign-on 섹션에서에서 단계를 수행 하는 hello를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-173">In hello Single Sign-On section, perform hello following steps:</span></span>
   
    <span data-ttu-id="958ec-174">![Single Sign-On 섹션](./media/active-directory-saas-zoom-tutorial/IC784701.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="958ec-174">![Single sign-on section](./media/active-directory-saas-zoom-tutorial/IC784701.png "Single sign-on")</span></span>
   
    <span data-ttu-id="958ec-175">a.</span><span class="sxs-lookup"><span data-stu-id="958ec-175">a.</span></span> <span data-ttu-id="958ec-176">Hello에 **로그인 페이지 URL** 붙여넣기 hello 값의 텍스트 상자 **SAML Single Sign-on 서비스 URL**, Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-176">In hello **Sign-in page URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="958ec-177">b.</span><span class="sxs-lookup"><span data-stu-id="958ec-177">b.</span></span> <span data-ttu-id="958ec-178">Hello에 **로그 아웃 페이지 URL** 붙여넣기 hello 값의 텍스트 상자 **Sign-Out URL**, Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-178">In hello **Sign-out page URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>
     
    <span data-ttu-id="958ec-179">c.</span><span class="sxs-lookup"><span data-stu-id="958ec-179">c.</span></span> <span data-ttu-id="958ec-180">콘텐츠를 클립보드에 복사 hello 메모장에서 e-64로 인코딩된 인증서를 열고 toohello 붙여 **Id 공급자 인증서** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-180">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **Identity provider certificate** textbox.</span></span>

    <span data-ttu-id="958ec-181">d.</span><span class="sxs-lookup"><span data-stu-id="958ec-181">d.</span></span> <span data-ttu-id="958ec-182">Hello에 **발급자** 붙여넣기 hello 값의 텍스트 상자 **SAML 엔터티 ID**, Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-182">In hello **Issuer** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="958ec-183">e.</span><span class="sxs-lookup"><span data-stu-id="958ec-183">e.</span></span> <span data-ttu-id="958ec-184">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-184">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="958ec-185">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="958ec-185">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="958ec-186">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="958ec-186">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="958ec-187">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="958ec-187">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="958ec-188">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="958ec-188">Create an Azure AD test user</span></span>

<span data-ttu-id="958ec-189">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-189">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Azure AD 테스트 사용자 만들기][100]

<span data-ttu-id="958ec-191">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="958ec-191">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="958ec-192">Hello hello 왼쪽된 창에서 Azure 포털에서에서 클릭 hello **Azure Active Directory** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-192">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![hello Azure Active Directory 단추](./media/active-directory-saas-zoom-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="958ec-194">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹**, 클릭 하 고 **모든 사용자가**합니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-194">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    !["사용자 및 그룹" hello 및 "모든 사용자" 링크](./media/active-directory-saas-zoom-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="958ec-196">tooopen hello **사용자** 대화 상자를 클릭 **추가** hello hello 맨 **모든 사용자에 게** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="958ec-196">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![hello 추가 단추](./media/active-directory-saas-zoom-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="958ec-198">Hello에 **사용자** 대화 상자를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-198">In hello **User** dialog box, perform hello following steps:</span></span>

    ![hello 사용자 대화 상자](./media/active-directory-saas-zoom-tutorial/create_aaduser_04.png)

    <span data-ttu-id="958ec-200">a.</span><span class="sxs-lookup"><span data-stu-id="958ec-200">a.</span></span> <span data-ttu-id="958ec-201">Hello에 **이름** 상자에서 입력 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-201">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="958ec-202">b.</span><span class="sxs-lookup"><span data-stu-id="958ec-202">b.</span></span> <span data-ttu-id="958ec-203">Hello에 **사용자 이름** 상자의 사용자 Britta Simon의 hello 전자 메일 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-203">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="958ec-204">c.</span><span class="sxs-lookup"><span data-stu-id="958ec-204">c.</span></span> <span data-ttu-id="958ec-205">선택 hello **암호 표시** 확인란을 선택한 다음 hello에 표시 되는 hello 값 기록 **암호** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-205">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="958ec-206">d.</span><span class="sxs-lookup"><span data-stu-id="958ec-206">d.</span></span> <span data-ttu-id="958ec-207">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-207">Click **Create**.</span></span>
 
### <a name="create-a-zoom-test-user"></a><span data-ttu-id="958ec-208">Zoom 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="958ec-208">Create a Zoom test user</span></span>

<span data-ttu-id="958ec-209">TooZoom에 순서 tooenable Azure AD 사용자가 toolog에서 확대/축소에 이들 프로 비전 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-209">In order tooenable Azure AD users toolog in tooZoom, they must be provisioned into Zoom.</span></span> <span data-ttu-id="958ec-210">확대/축소의 hello 경우에서 프로 비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-210">In hello case of Zoom, provisioning is a manual task.</span></span>

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a><span data-ttu-id="958ec-211">tooprovision 사용자 계정을 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-211">tooprovision a user account, perform hello following steps:</span></span>

1. <span data-ttu-id="958ec-212">Tooyour 로그인 **확대/축소** 회사 사이트에 관리자 권한으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-212">Log in tooyour **Zoom** company site as an administrator.</span></span>
 
2. <span data-ttu-id="958ec-213">Hello 클릭 **계정 관리** 탭을 클릭 한 다음 **사용자 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-213">Click hello **Account Management** tab, and then click **User Management**.</span></span>

3. <span data-ttu-id="958ec-214">Hello 사용자 관리 섹션에서에서 클릭 **사용자 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-214">In hello User Management section, click **Add users**.</span></span>
   
    <span data-ttu-id="958ec-215">![사용자 관리](./media/active-directory-saas-zoom-tutorial/IC784703.png "사용자 관리")</span><span class="sxs-lookup"><span data-stu-id="958ec-215">![User management](./media/active-directory-saas-zoom-tutorial/IC784703.png "User management")</span></span>

4. <span data-ttu-id="958ec-216">Hello에 **사용자 추가** 페이지 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-216">On hello **Add users** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="958ec-217">![사용자 추가](./media/active-directory-saas-zoom-tutorial/IC784704.png "사용자 추가")</span><span class="sxs-lookup"><span data-stu-id="958ec-217">![Add users](./media/active-directory-saas-zoom-tutorial/IC784704.png "Add users")</span></span>
   
    <span data-ttu-id="958ec-218">a.</span><span class="sxs-lookup"><span data-stu-id="958ec-218">a.</span></span> <span data-ttu-id="958ec-219">**사용자 유형**으로 **기본**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-219">As **User Type**, select **Basic**.</span></span>

    <span data-ttu-id="958ec-220">b.</span><span class="sxs-lookup"><span data-stu-id="958ec-220">b.</span></span> <span data-ttu-id="958ec-221">Hello에 **메일** textbox 유효한 Azure의 hello 전자 메일 주소를 입력 tooprovision 원하는 AD 계정.</span><span class="sxs-lookup"><span data-stu-id="958ec-221">In hello **Emails** textbox, type hello email address of a valid Azure AD account you want tooprovision.</span></span>

    <span data-ttu-id="958ec-222">c.</span><span class="sxs-lookup"><span data-stu-id="958ec-222">c.</span></span> <span data-ttu-id="958ec-223">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-223">Click **Add**.</span></span>

> [!NOTE]
> <span data-ttu-id="958ec-224">다른 확대/축소 사용자 계정 만들기 도구를 사용할 수 있습니다 또는 사용자 계정을 확대/축소 tooprovision Azure Active Directory에서 제공 된 Api입니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-224">You can use any other Zoom user account creation tools or APIs provided by Zoom tooprovision Azure Active Directory user accounts.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="958ec-225">Azure AD hello 테스트 사용자를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-225">Assign hello Azure AD test user</span></span>

<span data-ttu-id="958ec-226">이 섹션에서는 tooZoom 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooZoom.</span></span>

![Hello 사용자 역할 할당][200] 

<span data-ttu-id="958ec-228">**tooassign Britta Simon tooZoom hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="958ec-228">**tooassign Britta Simon tooZoom, perform hello following steps:**</span></span>

1. <span data-ttu-id="958ec-229">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-229">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="958ec-231">Hello 응용 프로그램 목록에서 선택 **확대/축소**합니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-231">In hello applications list, select **Zoom**.</span></span>

    ![hello 응용 프로그램 목록에서 hello 확대/축소 링크](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_app.png)  

3. <span data-ttu-id="958ec-233">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![hello "사용자 및 그룹" 링크][202]

4. <span data-ttu-id="958ec-235">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-235">Click **Add** button.</span></span> <span data-ttu-id="958ec-236">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![hello 할당 추가 창][203]

5. <span data-ttu-id="958ec-238">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="958ec-239">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="958ec-240">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="958ec-241">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="958ec-241">Test single sign-on</span></span>

<span data-ttu-id="958ec-242">이 섹션의 hello 목적은 tootest 액세스 패널을 hello 사용 하 여 Azure AD single sign-on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-242">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="958ec-243">Hello 액세스 패널에서에서 hello 확대/축소 타일을 클릭할 때 자동으로 로그온 tooyour 확대/축소 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="958ec-243">When you click hello Zoom tile in hello Access Panel, you should get automatically signed-on tooyour Zoom application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="958ec-244">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="958ec-244">Additional resources</span></span>

* [<span data-ttu-id="958ec-245">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="958ec-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="958ec-246">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="958ec-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_203.png

