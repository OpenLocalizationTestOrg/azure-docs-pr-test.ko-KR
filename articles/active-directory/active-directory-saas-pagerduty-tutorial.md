---
title: "자습서: PagerDuty와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 PagerDuty 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0410456a-76f7-42a7-9bb5-f767de75a0e0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: c3cfbedac3bf075e2d8cd833d5de7ca0bc9468b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pagerduty"></a><span data-ttu-id="2b161-103">자습서: PagerDuty와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="2b161-103">Tutorial: Azure Active Directory integration with PagerDuty</span></span>

<span data-ttu-id="2b161-104">이 자습서에 설명 어떻게 toointegrate Azure Active Directory (Azure AD)와 PagerDuty 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-104">In this tutorial, you learn how toointegrate PagerDuty with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2b161-105">Azure AD와 PagerDuty 통합 이점을 다음 hello로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-105">Integrating PagerDuty with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2b161-106">액세스 tooPagerDuty을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-106">You can control in Azure AD who has access tooPagerDuty</span></span>
- <span data-ttu-id="2b161-107">프로그램 사용자 tooautomatically get 로그온 tooPagerDuty (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-107">You can enable your users tooautomatically get signed-on tooPagerDuty (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2b161-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="2b161-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2b161-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="2b161-110">Prerequisites</span></span>

<span data-ttu-id="2b161-111">Azure AD 및 PagerDuty 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-111">tooconfigure Azure AD integration with PagerDuty, you need hello following items:</span></span>

- <span data-ttu-id="2b161-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="2b161-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2b161-113">PagerDuty Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="2b161-113">A PagerDuty single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2b161-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2b161-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2b161-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="2b161-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2b161-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2b161-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="2b161-118">Scenario description</span></span>
<span data-ttu-id="2b161-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2b161-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2b161-121">PagerDuty는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="2b161-121">Adding PagerDuty from hello gallery</span></span>
2. <span data-ttu-id="2b161-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="2b161-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pagerduty-from-hello-gallery"></a><span data-ttu-id="2b161-123">PagerDuty는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="2b161-123">Adding PagerDuty from hello gallery</span></span>
<span data-ttu-id="2b161-124">tooconfigure hello와의 통합 PagerDuty Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 PagerDuty tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-124">tooconfigure hello integration of PagerDuty into Azure AD, you need tooadd PagerDuty from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2b161-125">**hello 갤러리에서 PagerDuty tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="2b161-125">**tooadd PagerDuty from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2b161-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![hello Azure Active Directory 단추][1]

2. <span data-ttu-id="2b161-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="2b161-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-129">Then go too**All applications**.</span></span>

    ![hello 엔터프라이즈 응용 프로그램 블레이드][2]
    
3. <span data-ttu-id="2b161-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![hello 새 응용 프로그램 단추][3]

4. <span data-ttu-id="2b161-133">Hello 검색 상자에 입력 **PagerDuty**선택, **PagerDuty** 결과 패널에서 클릭 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-133">In hello search box, type **PagerDuty**, select  **PagerDuty**  from result panel then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="2b161-135">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="2b161-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="2b161-136">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 하여 PagerDuty에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-136">In this section, you configure and test Azure AD single sign-on with PagerDuty based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2b161-137">Single sign on toowork에 대 한 Azure AD는 tooknow PagerDuty에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in PagerDuty is tooa user in Azure AD.</span></span> <span data-ttu-id="2b161-138">즉, Azure AD 사용자와 PagerDuty에 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-138">In other words, a link relationship between an Azure AD user and hello related user in PagerDuty needs toobe established.</span></span>

<span data-ttu-id="2b161-139">PagerDuty에 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-139">In PagerDuty, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="2b161-140">tooconfigure와 PagerDuty 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-140">tooconfigure and test Azure AD single sign-on with PagerDuty, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2b161-141">**[Azure AD Single Sign-on 구성](#configure-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2b161-142">**[Azure AD 테스트를 만들고](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2b161-143">**[PagerDuty 테스트 사용자 만들기](#create-a-pagerduty-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 PagerDuty에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-143">**[Create a PagerDuty test user](#create-a-pagerduty-test-user)** - toohave a counterpart of Britta Simon in PagerDuty that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="2b161-144">**[Azure AD hello 테스트 사용자를 할당](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2b161-145">**[Single Sign-on 테스트](#test-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="2b161-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="2b161-146">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="2b161-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="2b161-147">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 PagerDuty 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your PagerDuty application.</span></span>

<span data-ttu-id="2b161-148">**Azure AD tooconfigure single sign on와 PagerDuty를 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="2b161-148">**tooconfigure Azure AD single sign-on with PagerDuty, perform hello following steps:**</span></span>

1. <span data-ttu-id="2b161-149">Hello hello에 Azure 포털에서에서 **PagerDuty** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-149">In hello Azure portal, on hello **PagerDuty** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-On 구성 링크][4]

2. <span data-ttu-id="2b161-151">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_samlbase.png)

3. <span data-ttu-id="2b161-153">Hello에 **PagerDuty 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-153">On hello **PagerDuty Domain and URLs** section, perform hello following steps:</span></span>

    ![PagerDuty 도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_url.png)

    <span data-ttu-id="2b161-155">a.</span><span class="sxs-lookup"><span data-stu-id="2b161-155">a.</span></span> <span data-ttu-id="2b161-156">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<tenant-name>.pagerduty.com`</span><span class="sxs-lookup"><span data-stu-id="2b161-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.pagerduty.com`</span></span>

    <span data-ttu-id="2b161-157">b.</span><span class="sxs-lookup"><span data-stu-id="2b161-157">b.</span></span> <span data-ttu-id="2b161-158">Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<tenant-name>.pagerduty.com`</span><span class="sxs-lookup"><span data-stu-id="2b161-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenant-name>.pagerduty.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2b161-159">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-159">These values are not real.</span></span> <span data-ttu-id="2b161-160">이러한 항목을 업데이트 로그온 URL과 식별자 실제 hello로 값입니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="2b161-161">연락처 [PagerDuty 클라이언트 지원 팀](https://www.pagerduty.com/support/) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-161">Contact [PagerDuty Client support team](https://www.pagerduty.com/support/) tooget these values.</span></span> 

4. <span data-ttu-id="2b161-162">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **Certificate(Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-162">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![hello 인증서 다운로드 링크](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_certificate.png) 

5. <span data-ttu-id="2b161-164">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-164">Click **Save** button.</span></span>

    ![Single Sign-On 구성 저장 단추](./media/active-directory-saas-pagerduty-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="2b161-166">Hello에 **PagerDuty 구성** 섹션에서 클릭 **구성 PagerDuty** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="2b161-166">On hello **PagerDuty Configuration** section, click **Configure PagerDuty** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="2b161-167">복사 hello **Sign-Out URL 및 SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="2b161-167">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![PagerDuty 구성](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_configure.png) 

7. <span data-ttu-id="2b161-169">다른 웹 브라우저 창에서 Pagerduty 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-169">In a different web browser window, log into your Pagerduty company site as an administrator.</span></span>

8. <span data-ttu-id="2b161-170">Hello 메뉴에서 hello 위에 표시를 클릭 **계정 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-170">In hello menu on hello top, click **Account Settings**.</span></span>
   
    <span data-ttu-id="2b161-171">![계정 설정](./media/active-directory-saas-pagerduty-tutorial/ic778535.png "계정 설정")</span><span class="sxs-lookup"><span data-stu-id="2b161-171">![Account Settings](./media/active-directory-saas-pagerduty-tutorial/ic778535.png "Account Settings")</span></span>

9. <span data-ttu-id="2b161-172">**Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-172">Click **Single Sign-on**.</span></span>
   
    <span data-ttu-id="2b161-173">![Single Sign-On](./media/active-directory-saas-pagerduty-tutorial/ic778536.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="2b161-173">![Single sign-on](./media/active-directory-saas-pagerduty-tutorial/ic778536.png "Single sign-on")</span></span>

10. <span data-ttu-id="2b161-174">Hello에 **사용 Single sign-on (SSO)** 페이지 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-174">On hello **Enable Single Sign-on (SSO)** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="2b161-175">![Single Sign-On 사용](./media/active-directory-saas-pagerduty-tutorial/ic778537.png "Single Sign-On 사용")</span><span class="sxs-lookup"><span data-stu-id="2b161-175">![Enable single sign-on](./media/active-directory-saas-pagerduty-tutorial/ic778537.png "Enable single sign-on")</span></span>
   
    <span data-ttu-id="2b161-176">a.</span><span class="sxs-lookup"><span data-stu-id="2b161-176">a.</span></span> <span data-ttu-id="2b161-177">메모장에서 콘텐츠를 클립보드에 복사 hello Azure 포털에서 다운로드 한 base 64로 인코딩된 인증서를 열고 다음 toohello **X.509 인증서** textbox</span><span class="sxs-lookup"><span data-stu-id="2b161-177">Open your base-64 encoded certificate downloaded from Azure portal in notepad, copy hello content of it into your clipboard, and then paste it toohello **X.509 Certificate** textbox</span></span>
  
    <span data-ttu-id="2b161-178">b.</span><span class="sxs-lookup"><span data-stu-id="2b161-178">b.</span></span> <span data-ttu-id="2b161-179">Hello에 **로그인 URL** 붙여넣습니다 **SAML Single Sign-on 서비스 URL** Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-179">In hello **Login URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="2b161-180">c.</span><span class="sxs-lookup"><span data-stu-id="2b161-180">c.</span></span> <span data-ttu-id="2b161-181">Hello에 **로그 아웃 URL** 붙여넣습니다 **Sign-Out URL** Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-181">In hello **Logout URL** textbox, paste **Sign-Out URL** which you have copied from Azure portal.</span></span>
 
    <span data-ttu-id="2b161-182">d.</span><span class="sxs-lookup"><span data-stu-id="2b161-182">d.</span></span> <span data-ttu-id="2b161-183">**Single Sign-On 켜기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-183">Select **Turn on Single Sign-on**.</span></span>
 
    <span data-ttu-id="2b161-184">e.</span><span class="sxs-lookup"><span data-stu-id="2b161-184">e.</span></span> <span data-ttu-id="2b161-185">**변경 내용 저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-185">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="2b161-186">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="2b161-186">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="2b161-187">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="2b161-187">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="2b161-188">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2b161-188">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="2b161-189">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="2b161-189">Create an Azure AD test user</span></span>

<span data-ttu-id="2b161-190">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-190">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 테스트 사용자 만들기][100]

<span data-ttu-id="2b161-192">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="2b161-192">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2b161-193">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-193">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![hello Azure Active Directory 단추](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2b161-195">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-195">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    !["사용자 및 그룹" hello 및 "모든 사용자" 링크](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2b161-197">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-197">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![hello 추가 단추](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2b161-199">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-199">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![hello 사용자 대화 상자](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2b161-201">a.</span><span class="sxs-lookup"><span data-stu-id="2b161-201">a.</span></span> <span data-ttu-id="2b161-202">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-202">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2b161-203">b.</span><span class="sxs-lookup"><span data-stu-id="2b161-203">b.</span></span> <span data-ttu-id="2b161-204">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-204">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2b161-205">c.</span><span class="sxs-lookup"><span data-stu-id="2b161-205">c.</span></span> <span data-ttu-id="2b161-206">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-206">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="2b161-207">d.</span><span class="sxs-lookup"><span data-stu-id="2b161-207">d.</span></span> <span data-ttu-id="2b161-208">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-208">Click **Create**.</span></span>
 
### <a name="create-a-pagerduty-test-user"></a><span data-ttu-id="2b161-209">PagerDuty 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="2b161-209">Create a PagerDuty test user</span></span>

<span data-ttu-id="2b161-210">tooenable Azure AD 사용자가 toolog tooPagerDuty에서 프로 비전 해야 PagerDuty에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-210">tooenable Azure AD users toolog in tooPagerDuty, they must be provisioned into PagerDuty.</span></span>  
<span data-ttu-id="2b161-211">Hello PagerDuty의 경우에서 프로 비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-211">In hello case of PagerDuty, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="2b161-212">다른 Pagerduty 사용자 계정 만들기 도구를 사용할 수 있습니다 또는 사용자 계정을 Pagerduty tooprovision Azure Active Directory에서 제공 된 Api입니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-212">You can use any other Pagerduty user account creation tools or APIs provided by Pagerduty tooprovision Azure Active Directory user accounts.</span></span>

<span data-ttu-id="2b161-213">**tooprovision 사용자 계정을 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="2b161-213">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="2b161-214">Tooyour 로그인 **Pagerduty** 테 넌 트입니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-214">Log in tooyour **Pagerduty** tenant.</span></span>

2. <span data-ttu-id="2b161-215">Hello 메뉴에서 hello 위에 표시를 클릭 **사용자**합니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-215">In hello menu on hello top, click **Users**.</span></span>

3. <span data-ttu-id="2b161-216">**사용자 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-216">Click **Add Users**.</span></span>
   
    <span data-ttu-id="2b161-217">![사용자 추가](./media/active-directory-saas-pagerduty-tutorial/ic778539.png "사용자 추가")</span><span class="sxs-lookup"><span data-stu-id="2b161-217">![Add Users](./media/active-directory-saas-pagerduty-tutorial/ic778539.png "Add Users")</span></span>

4.  <span data-ttu-id="2b161-218">Hello에 **팀 초대** 대화 상자에서 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-218">On hello **Invite your team** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="2b161-219">![팀 초대](./media/active-directory-saas-pagerduty-tutorial/ic778540.png "팀 초대")</span><span class="sxs-lookup"><span data-stu-id="2b161-219">![Invite your team](./media/active-directory-saas-pagerduty-tutorial/ic778540.png "Invite your team")</span></span>

    <span data-ttu-id="2b161-220">a.</span><span class="sxs-lookup"><span data-stu-id="2b161-220">a.</span></span> <span data-ttu-id="2b161-221">형식 hello **이름 및 성** 같은 사용자의 **Britta Simon**합니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-221">Type hello **First and Last Name** of user like **Britta Simon**.</span></span> 
   
    <span data-ttu-id="2b161-222">b.</span><span class="sxs-lookup"><span data-stu-id="2b161-222">b.</span></span> <span data-ttu-id="2b161-223">사용자의 **이메일** 주소를 입력합니다(예: **brittasimon@contoso.com**).</span><span class="sxs-lookup"><span data-stu-id="2b161-223">Enter **Email** address of user like **brittasimon@contoso.com**.</span></span>
   
    <span data-ttu-id="2b161-224">c.</span><span class="sxs-lookup"><span data-stu-id="2b161-224">c.</span></span> <span data-ttu-id="2b161-225">**추가**를 클릭한 다음 **초대장 보내기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-225">Click **Add**, and then click **Send Invites**.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="2b161-226">추가 된 모든 사용자는 초대 toocreate PagerDuty 계정을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-226">All added users will receive an invite toocreate a PagerDuty account.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="2b161-227">Azure AD hello 테스트 사용자를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-227">Assign hello Azure AD test user</span></span>

<span data-ttu-id="2b161-228">이 섹션에서는 tooPagerDuty 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-228">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPagerDuty.</span></span>

![Hello 사용자 역할 할당][200]

<span data-ttu-id="2b161-230">**tooassign Britta Simon tooPagerDuty hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="2b161-230">**tooassign Britta Simon tooPagerDuty, perform hello following steps:**</span></span>

1. <span data-ttu-id="2b161-231">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-231">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="2b161-233">Hello 응용 프로그램 목록에서 선택 **PagerDuty**합니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-233">In hello applications list, select **PagerDuty**.</span></span>

    ![hello 응용 프로그램 목록에서 hello PagerDuty 링크](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_app.png) 

3. <span data-ttu-id="2b161-235">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-235">In hello menu on hello left, click **Users and groups**.</span></span>

    ![hello "사용자 및 그룹" 링크][202]

4. <span data-ttu-id="2b161-237">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-237">Click **Add** button.</span></span> <span data-ttu-id="2b161-238">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![hello 할당 추가 창][203]

5. <span data-ttu-id="2b161-240">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-240">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="2b161-241">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2b161-242">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="2b161-243">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="2b161-243">Test single sign-on</span></span>

<span data-ttu-id="2b161-244">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-244">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="2b161-245">클릭할 때 hello PagerDuty 타일 액세스 Panelyou hello에 자동으로 로그온 tooyour PagerDuty 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-245">When you click hello PagerDuty tile in hello Access Panelyou should get automatically signed-on tooyour PagerDuty application.</span></span>

<span data-ttu-id="2b161-246">액세스 패널 hello에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2b161-246">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2b161-247">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="2b161-247">Additional resources</span></span>

* [<span data-ttu-id="2b161-248">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="2b161-248">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2b161-249">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="2b161-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_203.png

