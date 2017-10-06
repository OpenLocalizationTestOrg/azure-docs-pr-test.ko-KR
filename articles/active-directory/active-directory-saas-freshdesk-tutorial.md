---
title: "자습서: FreshDesk와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 FreshDesk 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2a3e5aa-7b5a-4fe4-9285-45dbe6e8efcc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 577a5eb6d9b1bc03030a2b47f63d375869c903bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-freshdesk"></a><span data-ttu-id="9401e-103">자습서: FreshDesk와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="9401e-103">Tutorial: Azure Active Directory integration with FreshDesk</span></span>

<span data-ttu-id="9401e-104">이 자습서에 설명 어떻게 toointegrate FreshDesk와 Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9401e-104">In this tutorial, you learn how toointegrate FreshDesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9401e-105">Azure AD와 FreshDesk 통합 이점을 다음 hello로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-105">Integrating FreshDesk with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9401e-106">액세스 tooFreshDesk을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-106">You can control in Azure AD who has access tooFreshDesk</span></span>
- <span data-ttu-id="9401e-107">프로그램 사용자 tooautomatically get 로그온 tooFreshDesk (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-107">You can enable your users tooautomatically get signed-on tooFreshDesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9401e-108">하나의 중앙 위치-hello Azure 관리 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="9401e-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9401e-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="9401e-110">Prerequisites</span></span>

<span data-ttu-id="9401e-111">FreshDesk와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-111">tooconfigure Azure AD integration with FreshDesk, you need hello following items:</span></span>

- <span data-ttu-id="9401e-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="9401e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9401e-113">FreshDesk Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="9401e-113">A FreshDesk single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9401e-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9401e-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9401e-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="9401e-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9401e-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="9401e-118">Scenario description</span></span>
<span data-ttu-id="9401e-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9401e-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9401e-121">FreshDesk은 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="9401e-121">Adding FreshDesk from hello gallery</span></span>
2. <span data-ttu-id="9401e-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="9401e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-freshdesk-from-hello-gallery"></a><span data-ttu-id="9401e-123">FreshDesk은 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="9401e-123">Adding FreshDesk from hello gallery</span></span>
<span data-ttu-id="9401e-124">tooconfigure hello와의 통합 FreshDesk Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 FreshDesk tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-124">tooconfigure hello integration of FreshDesk into Azure AD, you need tooadd FreshDesk from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9401e-125">**FreshDesk hello 갤러리에서 tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="9401e-125">**tooadd FreshDesk from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9401e-126">Hello에 ** [Azure 관리 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9401e-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9401e-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="9401e-131">클릭 **추가** hello 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="9401e-133">Hello 검색 상자에 입력 **FreshDesk**합니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-133">In hello search box, type **FreshDesk**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_search.png)

5. <span data-ttu-id="9401e-135">Hello 결과 패널에서 선택 **FreshDesk**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-135">In hello results panel, select **FreshDesk**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9401e-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="9401e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9401e-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 FreshDesk에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-138">In this section, you configure and test Azure AD single sign-on with FreshDesk based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9401e-139">Single sign on toowork에 대 한 Azure AD는 tooknow FreshDesk에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in FreshDesk is tooa user in Azure AD.</span></span> <span data-ttu-id="9401e-140">즉, Azure AD 사용자와 FreshDesk에 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-140">In other words, a link relationship between an Azure AD user and hello related user in FreshDesk needs toobe established.</span></span>

<span data-ttu-id="9401e-141">Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** FreshDesk에 합니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in FreshDesk.</span></span>

<span data-ttu-id="9401e-142">tooconfigure와 FreshDesk와 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-142">tooconfigure and test Azure AD single sign-on with FreshDesk, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9401e-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on) ** -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9401e-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user) ** -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9401e-145">**[FreshDesk 테스트 사용자 만들기](#creating-a-freshdesk-test-user) ** -toohave Britta Simon 그녀의 연결 된 Azure AD toohello 표현인 FreshDesk에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-145">**[Creating a FreshDesk test user](#creating-a-freshdesk-test-user)** - toohave a counterpart of Britta Simon in FreshDesk that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="9401e-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9401e-147">**[Single Sign-on 테스트](#testing-single-sign-on) ** -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="9401e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9401e-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="9401e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9401e-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 관리 포털에서 설정 및 FreshDesk 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your FreshDesk application.</span></span>

<span data-ttu-id="9401e-150">**Azure AD tooconfigure single sign on와 FreshDesk를 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="9401e-150">**tooconfigure Azure AD single sign-on with FreshDesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="9401e-151">Hello에 hello Azure 관리 포털에서 **FreshDesk** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-151">In hello Azure Management portal, on hello **FreshDesk** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="9401e-153">Hello에 **Single sign on** 대화 상자에서으로 **모드** 선택 **SAML 기반 로그온** tooenable single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_samlbase.png)

3. <span data-ttu-id="9401e-155">Hello에 **FreshDesk 도메인 및 Url** 섹션에서 hello를 입력 하십시오 **로그온 URL** 으로: `https://<tenant-name>.freshdesk.com` 이나 Freshdesk에 제안 된 다른 모든 값입니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-155">On hello **FreshDesk Domain and URLs** section, please enter hello **Sign-on URL** as: `https://<tenant-name>.freshdesk.com` or any other value Freshdesk has suggested.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_url.png)

    > [!NOTE] 
    > <span data-ttu-id="9401e-157">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-157">Please note that this is not the real value.</span></span> <span data-ttu-id="9401e-158">이러한 값은 실제 로그온 URL로 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-158">You have to update the value with the actual Sign-on URL.</span></span> <span data-ttu-id="9401e-159">이 값을 얻으려면 [FreshDesk Client 지원 팀](https://freshdesk.com/helpdesk-software?utm_source=Google-AdWords&utm_medium=Search-IND-Brand&utm_campaign=Search-IND-Brand&utm_term=freshdesk&device=c&gclid=COSH2_LH7NICFVUDvAodBPgBZg)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="9401e-159">Contact [FreshDesk Client support team](https://freshdesk.com/helpdesk-software?utm_source=Google-AdWords&utm_medium=Search-IND-Brand&utm_campaign=Search-IND-Brand&utm_term=freshdesk&device=c&gclid=COSH2_LH7NICFVUDvAodBPgBZg) to get this value.</span></span>  

4. <span data-ttu-id="9401e-160">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **인증서** hello 인증서 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-160">On hello **SAML Signing Certificate** section, click **Certificate** and then save hello certificate on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_certificate.png) 

5. <span data-ttu-id="9401e-162">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-162">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-freshdesk-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9401e-164">Hello에 **FreshDesk 구성** 섹션에서 클릭 **구성 FreshDesk** sign on 구성 tooopen 창.</span><span class="sxs-lookup"><span data-stu-id="9401e-164">On hello **FreshDesk Configuration** section, click **Configure FreshDesk** tooopen Configure sign-on window.</span></span> <span data-ttu-id="9401e-165">Hello에서 hello SAML Single Sign-on 서비스 URL 및 Sign-Out URL 복사 **빠른 참조** 섹션.</span><span class="sxs-lookup"><span data-stu-id="9401e-165">Copy hello SAML Single Sign-On Service URL and Sign-Out URL from hello **Quick Reference** section.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_configure.png)

7. <span data-ttu-id="9401e-167">다른 웹 브라우저 창에서 Freshdesk 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-167">In a different web browser window, log into your Freshdesk company site as an administrator.</span></span>

8. <span data-ttu-id="9401e-168">Hello 메뉴에서 hello 위에 표시를 클릭 **Admin**합니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-168">In hello menu on hello top, click **Admin**.</span></span>
   
   <span data-ttu-id="9401e-169">![관리자](./media/active-directory-saas-freshdesk-tutorial/IC776768.png "관리자")</span><span class="sxs-lookup"><span data-stu-id="9401e-169">![Admin](./media/active-directory-saas-freshdesk-tutorial/IC776768.png "Admin")</span></span>

9. <span data-ttu-id="9401e-170">Hello에 **일반 설정** 탭을 클릭 **보안**합니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-170">In hello **General Settings** tab, click **Security**.</span></span>
   
   <span data-ttu-id="9401e-171">![보안](./media/active-directory-saas-freshdesk-tutorial/IC776769.png "보안")</span><span class="sxs-lookup"><span data-stu-id="9401e-171">![Security](./media/active-directory-saas-freshdesk-tutorial/IC776769.png "Security")</span></span>

10. <span data-ttu-id="9401e-172">Hello에 **보안** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-172">In hello **Security** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="9401e-173">![Single Sign On](./media/active-directory-saas-freshdesk-tutorial/IC776770.png "Single Sign On")</span><span class="sxs-lookup"><span data-stu-id="9401e-173">![Single Sign On](./media/active-directory-saas-freshdesk-tutorial/IC776770.png "Single Sign On")</span></span>
   
    <span data-ttu-id="9401e-174">a.</span><span class="sxs-lookup"><span data-stu-id="9401e-174">a.</span></span> <span data-ttu-id="9401e-175">**SSO(Single Sign On)**의 경우 **On**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-175">For **Single Sign On (SSO)**, select **On**.</span></span>

    <span data-ttu-id="9401e-176">b.</span><span class="sxs-lookup"><span data-stu-id="9401e-176">b.</span></span> <span data-ttu-id="9401e-177">**SAML SSO**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-177">Select **SAML SSO**.</span></span>

    <span data-ttu-id="9401e-178">c.</span><span class="sxs-lookup"><span data-stu-id="9401e-178">c.</span></span> <span data-ttu-id="9401e-179">형식 hello **SAML Single Sign-on 서비스 URL** hello에 Azure 포털에서 복사한 **SAML 로그인 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-179">Type hello **SAML Single Sign-On Service URL** you copied from Azure portal into hello **SAML Login URL** textbox.</span></span>

    <span data-ttu-id="9401e-180">d.</span><span class="sxs-lookup"><span data-stu-id="9401e-180">d.</span></span> <span data-ttu-id="9401e-181">형식 hello **Sign-Out URL** hello에 Azure 포털에서 복사한 **로그 아웃 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-181">Type hello **Sign-Out URL**  you copied from Azure portal into hello **Logout URL** textbox.</span></span>

    <span data-ttu-id="9401e-182">e.</span><span class="sxs-lookup"><span data-stu-id="9401e-182">e.</span></span> <span data-ttu-id="9401e-183">복사 hello **지문** 값 Azure 포털에서 다운로드 한 hello 인증서에서 복사한 hello에 **보안 인증서 지문** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-183">Copy hello **Thumbprint** value from hello downloaded certificate from Azure portal and paste it into hello **Security Certificate Fingerprint** textbox.</span></span>  
 
    >[!TIP]
    ><span data-ttu-id="9401e-184">자세한 내용은 참조 하십시오. [어떻게 tooretrieve 인증서의 지문 값](http://youtu.be/YKQF266SAxI)합니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-184">For more details, see [How tooretrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span></span> 
    
    <span data-ttu-id="9401e-185">f.</span><span class="sxs-lookup"><span data-stu-id="9401e-185">f.</span></span> <span data-ttu-id="9401e-186">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-186">Click **Save**.</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9401e-187">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="9401e-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="9401e-188">이 섹션의 hello 목표 toocreate Britta Simon 라는 hello Azure 관리 포털에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-188">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="9401e-190">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="9401e-190">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9401e-191">Hello에 **Azure 관리 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-191">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9401e-193">너무 이동**사용자 및 그룹** 클릭 **모든 사용자에 게** 사용자 toodisplay hello 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-193">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9401e-195">Hello 대화의 hello 위쪽 클릭 **추가** tooopen hello **사용자** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="9401e-195">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9401e-197">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-197">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9401e-199">a.</span><span class="sxs-lookup"><span data-stu-id="9401e-199">a.</span></span> <span data-ttu-id="9401e-200">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-200">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9401e-201">b.</span><span class="sxs-lookup"><span data-stu-id="9401e-201">b.</span></span> <span data-ttu-id="9401e-202">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-202">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9401e-203">c.</span><span class="sxs-lookup"><span data-stu-id="9401e-203">c.</span></span> <span data-ttu-id="9401e-204">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-204">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="9401e-205">d.</span><span class="sxs-lookup"><span data-stu-id="9401e-205">d.</span></span> <span data-ttu-id="9401e-206">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-206">Click **Create**.</span></span>
 
### <a name="creating-a-freshdesk-test-user"></a><span data-ttu-id="9401e-207">FreshDesk 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="9401e-207">Creating a FreshDesk test user</span></span>

<span data-ttu-id="9401e-208">Tooenable Azure AD 사용자가 toolog FreshDesk에 주문 하 고에 FreshDesk에 이들 프로 비전 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-208">In order tooenable Azure AD users toolog into FreshDesk, they must be provisioned into FreshDesk.</span></span>  
<span data-ttu-id="9401e-209">Hello FreshDesk의 경우에서 프로 비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-209">In hello case of FreshDesk, provisioning is a manual task.</span></span>

<span data-ttu-id="9401e-210">**사용자 계정 수행 tooprovision hello 다음 단계:**</span><span class="sxs-lookup"><span data-stu-id="9401e-210">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="9401e-211">Tooyour 로그인 **Freshdesk** 테 넌 트입니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-211">Log in tooyour **Freshdesk** tenant.</span></span>
2. <span data-ttu-id="9401e-212">Hello 메뉴에서 hello 위에 표시를 클릭 **Admin**합니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-212">In hello menu on hello top, click **Admin**.</span></span>
   
   <span data-ttu-id="9401e-213">![관리자](./media/active-directory-saas-freshdesk-tutorial/IC776772.png "관리자")</span><span class="sxs-lookup"><span data-stu-id="9401e-213">![Admin](./media/active-directory-saas-freshdesk-tutorial/IC776772.png "Admin")</span></span>

3. <span data-ttu-id="9401e-214">Hello에 **일반 설정** 탭을 클릭 **에이전트**합니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-214">In hello **General Settings** tab, click **Agents**.</span></span>
   
   <span data-ttu-id="9401e-215">![에이전트](./media/active-directory-saas-freshdesk-tutorial/IC776773.png "에이전트")</span><span class="sxs-lookup"><span data-stu-id="9401e-215">![Agents](./media/active-directory-saas-freshdesk-tutorial/IC776773.png "Agents")</span></span>

4. <span data-ttu-id="9401e-216">**새 에이전트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-216">Click **New Agent**.</span></span>
   
    <span data-ttu-id="9401e-217">![새 에이전트](./media/active-directory-saas-freshdesk-tutorial/IC776774.png "새 에이전트")</span><span class="sxs-lookup"><span data-stu-id="9401e-217">![New Agent](./media/active-directory-saas-freshdesk-tutorial/IC776774.png "New Agent")</span></span>

5. <span data-ttu-id="9401e-218">Hello 에이전트 정보 대화 상자에서 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-218">On hello Agent Information dialog, perform hello following steps:</span></span>
   
   <span data-ttu-id="9401e-219">![에이전트 정보](./media/active-directory-saas-freshdesk-tutorial/IC776775.png "에이전트 정보")</span><span class="sxs-lookup"><span data-stu-id="9401e-219">![Agent Information](./media/active-directory-saas-freshdesk-tutorial/IC776775.png "Agent Information")</span></span>
   
   <span data-ttu-id="9401e-220">a.</span><span class="sxs-lookup"><span data-stu-id="9401e-220">a.</span></span> <span data-ttu-id="9401e-221">Hello에 **전체 이름을** tooprovision hello Azure AD 계정 형식 hello 이름 텍스트 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-221">In hello **Full Name** textbox, type hello name of hello Azure AD account you want tooprovision.</span></span>

   <span data-ttu-id="9401e-222">b.</span><span class="sxs-lookup"><span data-stu-id="9401e-222">b.</span></span> <span data-ttu-id="9401e-223">Hello에 **전자 메일** 텍스트 형식 hello Azure AD 전자 메일 주소 hello Azure AD 계정 tooprovision 합니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-223">In hello **Email** textbox, type hello Azure AD email address of hello Azure AD account you want tooprovision.</span></span>

   <span data-ttu-id="9401e-224">c.</span><span class="sxs-lookup"><span data-stu-id="9401e-224">c.</span></span> <span data-ttu-id="9401e-225">Hello에 **제목** textbox tooprovision hello Azure AD 계정 hello 제목을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-225">In hello **Title** textbox, type hello title of hello Azure AD account you want tooprovision.</span></span>

   <span data-ttu-id="9401e-226">d.</span><span class="sxs-lookup"><span data-stu-id="9401e-226">d.</span></span> <span data-ttu-id="9401e-227">**에이전트 역할**을 선택한 다음 **할당**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-227">Select **Agents role**, and then click **Assign**.</span></span>
       
   <span data-ttu-id="9401e-228">e.</span><span class="sxs-lookup"><span data-stu-id="9401e-228">e.</span></span> <span data-ttu-id="9401e-229">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-229">Click **Save**.</span></span>     
   
    >[!NOTE]
    ><span data-ttu-id="9401e-230">hello Azure AD 계정 보유자 활성화 되기 전에 tooconfirm hello 계정 연결을 포함 하는 전자 메일을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-230">hello Azure AD account holder will get an email that includes a link tooconfirm hello account before it is activated.</span></span> 
    > 
    
    >[!NOTE]
    ><span data-ttu-id="9401e-231">다른 Freshdesk 사용자 계정 만들기 도구를 사용할 수 있습니다 또는 AAD 사용자 계정을 tooprovision Freshdesk에서 제공 된 Api입니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-231">You can use any other Freshdesk user account creation tools or APIs provided by Freshdesk tooprovision AAD user accounts.</span></span> <span data-ttu-id="9401e-232">tooFreshDesk 합니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-232">tooFreshDesk.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="9401e-233">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-233">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="9401e-234">이 섹션에서는 액세스 tooBox 그녀의 권한을 부여 하 여 Azure single sign on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-234">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooBox.</span></span>

![사용자 할당][200] 

<span data-ttu-id="9401e-236">**tooassign Britta Simon tooFreshDesk hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="9401e-236">**tooassign Britta Simon tooFreshDesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="9401e-237">Hello Azure 관리 포털에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-237">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="9401e-239">Hello 응용 프로그램 목록에서 선택 **FreshDesk**합니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-239">In hello applications list, select **FreshDesk**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_app.png) 

3. <span data-ttu-id="9401e-241">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-241">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="9401e-243">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-243">Click **Add** button.</span></span> <span data-ttu-id="9401e-244">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="9401e-246">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-246">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9401e-247">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9401e-248">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9401e-249">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="9401e-249">Testing single sign-on</span></span>

<span data-ttu-id="9401e-250">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-250">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="9401e-251">Hello 액세스 패널에서에서 hello FreshDesk 타일을 클릭할 때 로그인 페이지 tooget 로그온 tooyour FreshDesk 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9401e-251">When you click hello FreshDesk tile in hello Access Panel, you should get login page tooget signed-on tooyour FreshDesk application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9401e-252">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="9401e-252">Additional resources</span></span>

* [<span data-ttu-id="9401e-253">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="9401e-253">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9401e-254">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="9401e-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_203.png

