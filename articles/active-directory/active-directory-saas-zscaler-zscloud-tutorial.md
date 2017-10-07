---
title: "자습서: Azure Active Directory와 Zscaler ZSCloud 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Zscaler ZSCloud 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 411d5684-a780-410a-9383-59f92cf569b5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: af6d5c1994e715cccf959cc9fd3ba998e5b9effa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-zscloud"></a><span data-ttu-id="cd43e-103">자습서: Azure Active Directory와 Zscaler ZSCloud 통합</span><span class="sxs-lookup"><span data-stu-id="cd43e-103">Tutorial: Azure Active Directory integration with Zscaler ZSCloud</span></span>

<span data-ttu-id="cd43e-104">이 자습서에 설명 어떻게 toointegrate (Azure AD) Azure Active Directory와 Zscaler ZSCloud 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-104">In this tutorial, you learn how toointegrate Zscaler ZSCloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cd43e-105">Azure AD와 Zscaler ZSCloud 통합 hello 다음 이점을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-105">Integrating Zscaler ZSCloud with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="cd43e-106">액세스 tooZscaler ZSCloud 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-106">You can control in Azure AD who has access tooZscaler ZSCloud</span></span>
- <span data-ttu-id="cd43e-107">프로그램 사용자 tooautomatically get 로그온 tooZscaler ZSCloud (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-107">You can enable your users tooautomatically get signed-on tooZscaler ZSCloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cd43e-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="cd43e-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cd43e-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="cd43e-110">Prerequisites</span></span>

<span data-ttu-id="cd43e-111">Zscaler ZSCloud와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-111">tooconfigure Azure AD integration with Zscaler ZSCloud, you need hello following items:</span></span>

- <span data-ttu-id="cd43e-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="cd43e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cd43e-113">Zscaler ZSCloud Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="cd43e-113">A Zscaler ZSCloud single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cd43e-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cd43e-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cd43e-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="cd43e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cd43e-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cd43e-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="cd43e-118">Scenario description</span></span>
<span data-ttu-id="cd43e-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cd43e-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cd43e-121">Zscaler ZSCloud hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="cd43e-121">Adding Zscaler ZSCloud from hello gallery</span></span>
2. <span data-ttu-id="cd43e-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="cd43e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zscaler-zscloud-from-hello-gallery"></a><span data-ttu-id="cd43e-123">Zscaler ZSCloud hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="cd43e-123">Adding Zscaler ZSCloud from hello gallery</span></span>
<span data-ttu-id="cd43e-124">tooconfigure hello와의 통합 Zscaler ZSCloud Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Zscaler ZSCloud tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-124">tooconfigure hello integration of Zscaler ZSCloud into Azure AD, you need tooadd Zscaler ZSCloud from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="cd43e-125">**Zscaler ZSCloud hello 갤러리에서 tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="cd43e-125">**tooadd Zscaler ZSCloud from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="cd43e-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="cd43e-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="cd43e-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="cd43e-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="cd43e-133">Hello 검색 상자에 입력 **Zscaler ZSCloud**합니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-133">In hello search box, type **Zscaler ZSCloud**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_search.png)

5. <span data-ttu-id="cd43e-135">Hello 결과 패널에서 선택 **Zscaler ZSCloud**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-135">In hello results panel, select **Zscaler ZSCloud**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cd43e-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="cd43e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cd43e-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Zscaler ZSCloud에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-138">In this section, you configure and test Azure AD single sign-on with Zscaler ZSCloud based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="cd43e-139">Single sign on toowork에 대 한 Azure AD는 tooknow Zscaler ZSCloud에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Zscaler ZSCloud is tooa user in Azure AD.</span></span> <span data-ttu-id="cd43e-140">즉, Azure AD 사용자와 Zscaler ZSCloud에 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-140">In other words, a link relationship between an Azure AD user and hello related user in Zscaler ZSCloud needs toobe established.</span></span>

<span data-ttu-id="cd43e-141">Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** Zscaler ZSCloud에 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Zscaler ZSCloud.</span></span>

<span data-ttu-id="cd43e-142">tooconfigure 및 Zscaler ZSCloud를 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-142">tooconfigure and test Azure AD single sign-on with Zscaler ZSCloud, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="cd43e-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="cd43e-144">**[프록시 설정 구성](#configuring-proxy-settings)**  -Internet Explorer의 tooconfigure hello 프록시 설정</span><span class="sxs-lookup"><span data-stu-id="cd43e-144">**[Configuring proxy settings](#configuring-proxy-settings)** - tooconfigure hello proxy settings in Internet Explorer</span></span>
2. <span data-ttu-id="cd43e-145">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)**  - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cd43e-146">**[Zscaler ZSCloud 테스트 사용자 만들기](#creating-a-zscaler-zscloud-test-user)**  -toohave Britta Simon 표현인 연결 된 toohello Azure AD 사용자는 Zscaler ZSCloud에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-146">**[Creating a Zscaler ZSCloud test user](#creating-a-zscaler-zscloud-test-user)** - toohave a counterpart of Britta Simon in Zscaler ZSCloud that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="cd43e-147">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cd43e-148">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="cd43e-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cd43e-149">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="cd43e-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cd43e-150">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 Zscaler ZSCloud 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Zscaler ZSCloud application.</span></span>

<span data-ttu-id="cd43e-151">**Azure AD tooconfigure single sign on와 Zscaler ZSCloud hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="cd43e-151">**tooconfigure Azure AD single sign-on with Zscaler ZSCloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="cd43e-152">Hello hello에 Azure 포털에서에서 **Zscaler ZSCloud** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-152">In hello Azure portal, on hello **Zscaler ZSCloud** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="cd43e-154">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_samlbase.png)

3. <span data-ttu-id="cd43e-156">Hello에 **Zscaler ZSCloud 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-156">On hello **Zscaler ZSCloud Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_url.png)

     <span data-ttu-id="cd43e-158">Hello에 **로그온 URL** 텍스트 상자에 사용자에 대 한 toosign tooyour ZScaler ZSCloud 응용 프로그램에서 사용 하는 hello URL 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-158">In hello **Sign-on URL** textbox, type hello URL used by your users toosign-on tooyour ZScaler ZSCloud application.</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="cd43e-159">이 값이 hello로 tooupdate 되어 실제 로그온 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-159">You have tooupdate this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="cd43e-160">연락처 [Zscaler ZSCloud 클라이언트 지원 팀](https://support.zscaler.com/hc/articles/210172606-Zscaler-is-Expanding-Its-Zscloud-Global-Footprint) tooget이이 값입니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-160">Contact [Zscaler ZSCloud Client support team](https://support.zscaler.com/hc/articles/210172606-Zscaler-is-Expanding-Its-Zscloud-Global-Footprint) tooget this value.</span></span> 
 
4. <span data-ttu-id="cd43e-161">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **인증서 (Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_certificate.png) 

5. <span data-ttu-id="cd43e-163">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-163">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="cd43e-165">Hello에 **Zscaler ZSCloud 구성** 섹션에서 클릭 **Zscaler ZSCloud 구성** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="cd43e-165">On hello **Zscaler ZSCloud Configuration** section, click **Configure Zscaler ZSCloud** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="cd43e-166">복사 hello **SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="cd43e-166">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_configure.png) 

7. <span data-ttu-id="cd43e-168">다른 웹 브라우저 창에서 tooyour에 ZScaler ZSCloud 회사 사이트는 관리자 권한으로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-168">In a different web browser window, log in tooyour ZScaler ZSCloud company site as an administrator.</span></span>

8. <span data-ttu-id="cd43e-169">Hello 메뉴에서 hello 위에 표시를 클릭 **관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-169">In hello menu on hello top, click **Administration**.</span></span>
   
    <span data-ttu-id="cd43e-170">![관리](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800206.png "관리")</span><span class="sxs-lookup"><span data-stu-id="cd43e-170">![Administration](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800206.png "Administration")</span></span>

9. <span data-ttu-id="cd43e-171">**관리자 & 역할 관리**에서 **사용자 및 인증 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-171">Under **Manage Administrators & Roles**, click **Manage Users & Authentication**.</span></span>   
            
    <span data-ttu-id="cd43e-172">![사용자 및 인증 관리](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800207.png "사용자 및 인증 관리")</span><span class="sxs-lookup"><span data-stu-id="cd43e-172">![Manage Users & Authentication](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800207.png "Manage Users & Authentication")</span></span>

10. <span data-ttu-id="cd43e-173">Hello에 **조직에 대 한 인증 옵션 선택** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-173">In hello **Choose Authentication Options for your Organization** section, perform hello following steps:</span></span>   
                
    <span data-ttu-id="cd43e-174">![인증](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800208.png "인증")</span><span class="sxs-lookup"><span data-stu-id="cd43e-174">![Authentication](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800208.png "Authentication")</span></span>
   
    <span data-ttu-id="cd43e-175">a.</span><span class="sxs-lookup"><span data-stu-id="cd43e-175">a.</span></span> <span data-ttu-id="cd43e-176">**SAML Single Sign-On을 사용하여 인증**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-176">Select **Authenticate using SAML Single Sign-On**.</span></span>

    <span data-ttu-id="cd43e-177">b.</span><span class="sxs-lookup"><span data-stu-id="cd43e-177">b.</span></span> <span data-ttu-id="cd43e-178">**SAML Single Sign-On 매개 변수 구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-178">Click **Configure SAML Single Sign-On Parameters**.</span></span>

11. <span data-ttu-id="cd43e-179">Hello에 **SAML Single Sign-on 매개 변수 구성** 대화 상자 페이지에서 단계에 따라 hello를 수행 하 고 클릭 한 다음 **수행**</span><span class="sxs-lookup"><span data-stu-id="cd43e-179">On hello **Configure SAML Single Sign-On Parameters** dialog page, perform hello following steps, and then click **Done**</span></span>

    <span data-ttu-id="cd43e-180">![Single Sign-On](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800209.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="cd43e-180">![Single Sign-On](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800209.png "Single Sign-On")</span></span>
    
    <span data-ttu-id="cd43e-181">a.</span><span class="sxs-lookup"><span data-stu-id="cd43e-181">a.</span></span> <span data-ttu-id="cd43e-182">붙여넣기 hello **SAML Single Sign-on 서비스 URL** hello에 값 **hello SAML 포털 toowhich 사용자의 URL은 인증을 위해 전송** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-182">Paste hello **SAML Single Sign-On Service URL** value into hello **URL of hello SAML Portal toowhich users are sent for authentication** textbox.</span></span>
    
    <span data-ttu-id="cd43e-183">b.</span><span class="sxs-lookup"><span data-stu-id="cd43e-183">b.</span></span> <span data-ttu-id="cd43e-184">Hello에 **로그인 이름이 포함 된 특성** 텍스트 상자에 **NameID**합니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-184">In hello **Attribute containing Login Name** textbox, type **NameID**.</span></span>
    
    <span data-ttu-id="cd43e-185">c.</span><span class="sxs-lookup"><span data-stu-id="cd43e-185">c.</span></span> <span data-ttu-id="cd43e-186">tooupload 다운로드 한 인증서를 클릭 하 여 **Zscaler pem**합니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-186">tooupload your downloaded certificate, click **Zscaler pem**.</span></span>
    
    <span data-ttu-id="cd43e-187">d.</span><span class="sxs-lookup"><span data-stu-id="cd43e-187">d.</span></span> <span data-ttu-id="cd43e-188">**SAML 자동 프로비전 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-188">Select **Enable SAML Auto-Provisioning**.</span></span>

12. <span data-ttu-id="cd43e-189">Hello에 **사용자 인증 구성** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-189">On hello **Configure User Authentication** dialog page, perform hello following steps:</span></span>

    <span data-ttu-id="cd43e-190">![관리](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800210.png "관리")</span><span class="sxs-lookup"><span data-stu-id="cd43e-190">![Administration](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800210.png "Administration")</span></span>
    
    <span data-ttu-id="cd43e-191">a.</span><span class="sxs-lookup"><span data-stu-id="cd43e-191">a.</span></span> <span data-ttu-id="cd43e-192">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-192">Click **Save**.</span></span>

    <span data-ttu-id="cd43e-193">b.</span><span class="sxs-lookup"><span data-stu-id="cd43e-193">b.</span></span> <span data-ttu-id="cd43e-194">**지금 활성화**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-194">Click **Activate Now**.</span></span>

## <a name="configuring-proxy-settings"></a><span data-ttu-id="cd43e-195">프록시 설정 구성</span><span class="sxs-lookup"><span data-stu-id="cd43e-195">Configuring proxy settings</span></span>
### <a name="tooconfigure-hello-proxy-settings-in-internet-explorer"></a><span data-ttu-id="cd43e-196">Internet Explorer의 tooconfigure hello 프록시 설정</span><span class="sxs-lookup"><span data-stu-id="cd43e-196">tooconfigure hello proxy settings in Internet Explorer</span></span>

1. <span data-ttu-id="cd43e-197">**Internet Explorer**를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-197">Start **Internet Explorer**.</span></span>

2. <span data-ttu-id="cd43e-198">선택 **인터넷 옵션** hello에서 **도구** 열려 hello에 대 한 메뉴 **인터넷 옵션** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="cd43e-198">Select **Internet options** from hello **Tools** menu for open hello **Internet Options** dialog.</span></span>   
    
     <span data-ttu-id="cd43e-199">![인터넷 옵션](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769492.png "인터넷 옵션")</span><span class="sxs-lookup"><span data-stu-id="cd43e-199">![Internet Options](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769492.png "Internet Options")</span></span>

3. <span data-ttu-id="cd43e-200">Hello 클릭 **연결** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-200">Click hello **Connections** tab.</span></span>   
  
     <span data-ttu-id="cd43e-201">![연결](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769493.png "연결")</span><span class="sxs-lookup"><span data-stu-id="cd43e-201">![Connections](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769493.png "Connections")</span></span>

4. <span data-ttu-id="cd43e-202">클릭 **LAN 설정** tooopen hello **LAN 설정** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="cd43e-202">Click **LAN settings** tooopen hello **LAN Settings** dialog.</span></span>

5. <span data-ttu-id="cd43e-203">Hello 모드 해제 프록시 서버 섹션에서에서 단계를 수행 하는 hello를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-203">In hello Proxy server section, perform hello following steps:</span></span>   
   
    <span data-ttu-id="cd43e-204">![프록시 서버](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769494.png "프록시 서버")</span><span class="sxs-lookup"><span data-stu-id="cd43e-204">![Proxy server](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769494.png "Proxy server")</span></span>

    <span data-ttu-id="cd43e-205">a.</span><span class="sxs-lookup"><span data-stu-id="cd43e-205">a.</span></span> <span data-ttu-id="cd43e-206">**사용자 LAN의 프록시 서버 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-206">Select **Use a proxy server for your LAN**.</span></span>

    <span data-ttu-id="cd43e-207">b.</span><span class="sxs-lookup"><span data-stu-id="cd43e-207">b.</span></span> <span data-ttu-id="cd43e-208">Hello 주소 텍스트 상자에 입력 **gateway.zscalerone.net**합니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-208">In hello Address textbox, type **gateway.zscalerone.net**.</span></span>

    <span data-ttu-id="cd43e-209">c.</span><span class="sxs-lookup"><span data-stu-id="cd43e-209">c.</span></span> <span data-ttu-id="cd43e-210">Hello 포트 텍스트 상자에 입력 **80**합니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-210">In hello Port textbox, type **80**.</span></span>

    <span data-ttu-id="cd43e-211">d.</span><span class="sxs-lookup"><span data-stu-id="cd43e-211">d.</span></span> <span data-ttu-id="cd43e-212">**로컬 주소의 바이패스 프록시 서버**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-212">Select **Bypass proxy server for local addresses**.</span></span>

    <span data-ttu-id="cd43e-213">e.</span><span class="sxs-lookup"><span data-stu-id="cd43e-213">e.</span></span> <span data-ttu-id="cd43e-214">클릭 **확인** tooclose hello **Local Area Network (LAN) 설정** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="cd43e-214">Click **OK** tooclose hello **Local Area Network (LAN) Settings** dialog.</span></span>

6. <span data-ttu-id="cd43e-215">클릭 **확인** tooclose hello **인터넷 옵션** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="cd43e-215">Click **OK** tooclose hello **Internet Options** dialog.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cd43e-216">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="cd43e-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="cd43e-217">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-217">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="cd43e-219">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="cd43e-219">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="cd43e-220">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-220">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cd43e-222">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-222">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cd43e-224">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-224">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cd43e-226">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-226">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cd43e-228">a.</span><span class="sxs-lookup"><span data-stu-id="cd43e-228">a.</span></span> <span data-ttu-id="cd43e-229">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-229">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cd43e-230">b.</span><span class="sxs-lookup"><span data-stu-id="cd43e-230">b.</span></span> <span data-ttu-id="cd43e-231">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-231">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cd43e-232">c.</span><span class="sxs-lookup"><span data-stu-id="cd43e-232">c.</span></span> <span data-ttu-id="cd43e-233">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-233">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="cd43e-234">d.</span><span class="sxs-lookup"><span data-stu-id="cd43e-234">d.</span></span> <span data-ttu-id="cd43e-235">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-235">Click **Create**.</span></span>

### <a name="creating-a-zscaler-zscloud-test-user"></a><span data-ttu-id="cd43e-236">Zscaler ZSCloud 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="cd43e-236">Creating a Zscaler ZSCloud test user</span></span>

<span data-ttu-id="cd43e-237">tooenable Azure AD 사용자가 toolog ZSCloud tooZScaler에 프로 비전 된 tooZScaler ZSCloud 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-237">tooenable Azure AD users toolog in tooZScaler ZSCloud, they must be provisioned tooZScaler ZSCloud.</span></span>  
<span data-ttu-id="cd43e-238">Hello ZScaler ZSCloud의 경우에서 프로 비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-238">In hello case of ZScaler ZSCloud, provisioning is a manual task.</span></span>

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a><span data-ttu-id="cd43e-239">tooconfigure 사용자 프로비저닝, hello 다음 단계를 수행:</span><span class="sxs-lookup"><span data-stu-id="cd43e-239">tooconfigure user provisioning, perform hello following steps:</span></span>

1. <span data-ttu-id="cd43e-240">Tooyour 로그인 **Zscaler** 테 넌 트입니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-240">Log in tooyour **Zscaler** tenant.</span></span>

2. <span data-ttu-id="cd43e-241">**관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-241">Click **Administration**.</span></span>   
   
    <span data-ttu-id="cd43e-242">![관리](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781035.png "관리")</span><span class="sxs-lookup"><span data-stu-id="cd43e-242">![Administration](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781035.png "Administration")</span></span>

3. <span data-ttu-id="cd43e-243">**사용자 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-243">Click **User Management**.</span></span>   
        
     <span data-ttu-id="cd43e-244">![추가](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "추가")</span><span class="sxs-lookup"><span data-stu-id="cd43e-244">![Add](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "Add")</span></span>

4. <span data-ttu-id="cd43e-245">Hello에 **사용자** 탭을 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-245">In hello **Users** tab, click **Add**.</span></span>
      
    <span data-ttu-id="cd43e-246">![추가](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "추가")</span><span class="sxs-lookup"><span data-stu-id="cd43e-246">![Add](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "Add")</span></span>

5. <span data-ttu-id="cd43e-247">Hello 사용자 추가 섹션에서에서 단계를 수행 하는 hello를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-247">In hello Add User section, perform hello following steps:</span></span>
        
    <span data-ttu-id="cd43e-248">![사용자 추가](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781038.png "사용자 추가")</span><span class="sxs-lookup"><span data-stu-id="cd43e-248">![Add User](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781038.png "Add User")</span></span>
   
    <span data-ttu-id="cd43e-249">a.</span><span class="sxs-lookup"><span data-stu-id="cd43e-249">a.</span></span> <span data-ttu-id="cd43e-250">형식 hello **UserID**, **사용자 표시 이름**, **암호**, **암호 확인**를 선택한 후 **그룹**및 hello **부서** tooprovision 하려는 유효한 AAD 계정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-250">Type hello **UserID**, **User Display Name**, **Password**, **Confirm Password**, and then select **Groups** and hello **Department** of a valid AAD account you want tooprovision.</span></span>

    <span data-ttu-id="cd43e-251">b.</span><span class="sxs-lookup"><span data-stu-id="cd43e-251">b.</span></span> <span data-ttu-id="cd43e-252">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-252">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="cd43e-253">다른 ZScaler ZSCloud 사용자 계정 만들기 도구를 사용할 수 있습니다 또는 AAD 사용자 계정을 tooprovision ZScaler ZSCloud에서 제공 된 Api입니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-253">You can use any other ZScaler ZSCloud user account creation tools or APIs provided by ZScaler ZSCloud tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="cd43e-254">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-254">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="cd43e-255">이 섹션에서는 액세스 tooZscaler ZSCloud 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-255">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooZscaler ZSCloud.</span></span>

![사용자 할당][200] 

<span data-ttu-id="cd43e-257">**tooassign Britta Simon tooZscaler ZSCloud hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="cd43e-257">**tooassign Britta Simon tooZscaler ZSCloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="cd43e-258">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-258">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="cd43e-260">Hello 응용 프로그램 목록에서 선택 **Zscaler ZSCloud**합니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-260">In hello applications list, select **Zscaler ZSCloud**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_app.png) 

3. <span data-ttu-id="cd43e-262">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-262">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="cd43e-264">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-264">Click **Add** button.</span></span> <span data-ttu-id="cd43e-265">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-265">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="cd43e-267">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-267">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="cd43e-268">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-268">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cd43e-269">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-269">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cd43e-270">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="cd43e-270">Testing single sign-on</span></span>

<span data-ttu-id="cd43e-271">Single sign on 설정 tootest 원하는 hello 액세스 패널을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-271">If you want tootest your single sign-on settings, open hello Access Panel.</span></span>

<span data-ttu-id="cd43e-272">Hello Zscaler ZSCloud hello 액세스 패널에서에서 타일을 클릭할 때 자동으로 로그온 tooyour Zscaler ZSCloud 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-272">When you click hello Zscaler ZSCloud tile in hello Access Panel, you should get automatically signed-on tooyour Zscaler ZSCloud application.</span></span>

<span data-ttu-id="cd43e-273">액세스 패널 hello에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="cd43e-273">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="cd43e-274">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="cd43e-274">Additional resources</span></span>

* [<span data-ttu-id="cd43e-275">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="cd43e-275">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cd43e-276">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="cd43e-276">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_203.png

