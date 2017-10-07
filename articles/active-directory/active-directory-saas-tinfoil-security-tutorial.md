---
title: "자습서: TINFOIL SECURITY와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 TINFOIL SECURITY 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: da02da92-e3b0-4c09-ad6c-180882b0f9f8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 1a3fa9880d9e026c2d6d6548188df2269ff69139
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tinfoil-security"></a><span data-ttu-id="f89f9-103">자습서: TINFOIL SECURITY와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="f89f9-103">Tutorial: Azure Active Directory integration with TINFOIL SECURITY</span></span>

<span data-ttu-id="f89f9-104">이 자습서에 설명 어떻게 toointegrate Azure Active Directory (Azure AD)와 TINFOIL SECURITY 합니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-104">In this tutorial, you learn how toointegrate TINFOIL SECURITY with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f89f9-105">Azure AD와 TINFOIL SECURITY 통합 이점을 다음 hello로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-105">Integrating TINFOIL SECURITY with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f89f9-106">액세스 tooTINFOIL 보안을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-106">You can control in Azure AD who has access tooTINFOIL SECURITY</span></span>
- <span data-ttu-id="f89f9-107">에 사용자가 tooautomatically get 로그온 tooTINFOIL (Single Sign-on) 보안으로는 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-107">You can enable your users tooautomatically get signed-on tooTINFOIL SECURITY (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f89f9-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f89f9-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f89f9-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="f89f9-110">Prerequisites</span></span>

<span data-ttu-id="f89f9-111">TINFOIL SECURITY와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-111">tooconfigure Azure AD integration with TINFOIL SECURITY, you need hello following items:</span></span>

- <span data-ttu-id="f89f9-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="f89f9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f89f9-113">TINFOIL SECURITY Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="f89f9-113">A TINFOIL SECURITY single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f89f9-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f89f9-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f89f9-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="f89f9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f89f9-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f89f9-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="f89f9-118">Scenario description</span></span>
<span data-ttu-id="f89f9-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f89f9-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f89f9-121">Hello 갤러리에서 TINFOIL SECURITY를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-121">Add TINFOIL SECURITY from hello gallery</span></span>
2. <span data-ttu-id="f89f9-122">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="f89f9-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-tinfoil-security-from-hello-gallery"></a><span data-ttu-id="f89f9-123">Hello 갤러리에서 TINFOIL SECURITY를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-123">Add TINFOIL SECURITY from hello gallery</span></span>
<span data-ttu-id="f89f9-124">tooconfigure hello와의 통합 TINFOIL SECURITY Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 TINFOIL SECURITY tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-124">tooconfigure hello integration of TINFOIL SECURITY into Azure AD, you need tooadd TINFOIL SECURITY from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f89f9-125">**TINFOIL SECURITY hello 갤러리에서 tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="f89f9-125">**tooadd TINFOIL SECURITY from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f89f9-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f89f9-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f89f9-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="f89f9-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="f89f9-133">Hello 검색 상자에 입력 **TINFOIL SECURITY**선택, **TINFOIL SECURITY** 결과 패널에서 클릭 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-133">In hello search box, type **TINFOIL SECURITY**, select  **TINFOIL SECURITY** from result panel then click **Add** button tooadd hello application.</span></span>

    ![갤러리의 TINFOIL SECURITY](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="f89f9-135">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="f89f9-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="f89f9-136">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 TINFOIL SECURITY에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-136">In this section, you configure and test Azure AD single sign-on with TINFOIL SECURITY based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f89f9-137">Single sign on toowork에 대 한 Azure AD는 tooknow TINFOIL SECURITY에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in TINFOIL SECURITY is tooa user in Azure AD.</span></span> <span data-ttu-id="f89f9-138">즉, Azure AD 사용자와 TINFOIL SECURITY에 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-138">In other words, a link relationship between an Azure AD user and hello related user in TINFOIL SECURITY needs toobe established.</span></span>

<span data-ttu-id="f89f9-139">TINFOIL SECURITY에 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-139">In TINFOIL SECURITY, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f89f9-140">tooconfigure 및 TINFOIL SECURITY를 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-140">tooconfigure and test Azure AD single sign-on with TINFOIL SECURITY, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f89f9-141">**[Azure AD Single Sign-on 구성](#configure-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f89f9-142">**[Azure AD 테스트를 만들고](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f89f9-143">**[TINFOIL SECURITY 테스트 사용자 만들기](#create-a-tinfoil-security-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 TINFOIL SECURITY에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-143">**[Create a TINFOIL SECURITY test user](#create-a-tinfoil-security-test-user)** - toohave a counterpart of Britta Simon in TINFOIL SECURITY that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f89f9-144">**[Azure AD hello 테스트 사용자를 할당](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f89f9-145">**[Single Sign-on 테스트](#test-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="f89f9-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="f89f9-146">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="f89f9-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="f89f9-147">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 TINFOIL SECURITY 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your TINFOIL SECURITY application.</span></span>

<span data-ttu-id="f89f9-148">**Azure AD tooconfigure single sign on와 TINFOIL SECURITY hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="f89f9-148">**tooconfigure Azure AD single sign-on with TINFOIL SECURITY, perform hello following steps:**</span></span>

1. <span data-ttu-id="f89f9-149">Hello hello에 Azure 포털에서에서 **TINFOIL SECURITY** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-149">In hello Azure portal, on hello **TINFOIL SECURITY** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="f89f9-151">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![SAML 기반 로그온](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_samlbase.png)

3. <span data-ttu-id="f89f9-153">Hello에 **TINFOIL 보안 도메인 및 Url** 섹션에서 hello 사용자 tooperform 모든 단계와 서로 hello 앱 Azure로 이미 사전 통합 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-153">On hello **TINFOIL SECURITY Domain and URLs** section, hello user does not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_url.png)


4. <span data-ttu-id="f89f9-155">Hello에 **SAML 서명 인증서** 섹션을 복사 hello **지문** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-155">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value.</span></span>

    ![SAML 서명 인증서 섹션](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_certificate.png) 

5. <span data-ttu-id="f89f9-157">tooadd hello 필요한 특성 매핑을 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-157">tooadd hello required attribute mappings, perform hello following steps:</span></span>
    
    <span data-ttu-id="f89f9-158">![특성](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute1.png "특성")</span><span class="sxs-lookup"><span data-stu-id="f89f9-158">![Attributes](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute1.png "Attributes")</span></span>
    
    | <span data-ttu-id="f89f9-159">특성 이름</span><span class="sxs-lookup"><span data-stu-id="f89f9-159">Attribute Name</span></span>    |   <span data-ttu-id="f89f9-160">특성 값</span><span class="sxs-lookup"><span data-stu-id="f89f9-160">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="f89f9-161">accountid</span><span class="sxs-lookup"><span data-stu-id="f89f9-161">accountid</span></span> | <span data-ttu-id="f89f9-162">UXXXXXXXXXXXXX</span><span class="sxs-lookup"><span data-stu-id="f89f9-162">UXXXXXXXXXXXXX</span></span> |
    
    <span data-ttu-id="f89f9-163">a.</span><span class="sxs-lookup"><span data-stu-id="f89f9-163">a.</span></span> <span data-ttu-id="f89f9-164">**사용자 특성 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-164">Click **add user attribute**.</span></span>
    
    <span data-ttu-id="f89f9-165">![특성 추가](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute.png "특성")</span><span class="sxs-lookup"><span data-stu-id="f89f9-165">![ADD Attribute](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute.png "Attributes")</span></span>
    
    <span data-ttu-id="f89f9-166">![특성 추가](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_addatt.png "특성")</span><span class="sxs-lookup"><span data-stu-id="f89f9-166">![ADD Attribute](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_addatt.png "Attributes")</span></span>
    
    <span data-ttu-id="f89f9-167">b.</span><span class="sxs-lookup"><span data-stu-id="f89f9-167">b.</span></span> <span data-ttu-id="f89f9-168">Hello에 **특성 이름** 텍스트 상자에 **accountid**합니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-168">In hello **Attribute Name** textbox, type **accountid**.</span></span>
    
    <span data-ttu-id="f89f9-169">c.</span><span class="sxs-lookup"><span data-stu-id="f89f9-169">c.</span></span> <span data-ttu-id="f89f9-170">Hello에 **특성 값** 텍스트 붙여넣기 hello 계정 ID 값 hello 자습서 나중에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-170">In hello **Attribute Value** textbox, paste hello account ID value which you will get later on hello tutorial.</span></span>
    
    <span data-ttu-id="f89f9-171">d.</span><span class="sxs-lookup"><span data-stu-id="f89f9-171">d.</span></span> <span data-ttu-id="f89f9-172">**Ok**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-172">Click **Ok**.</span></span>    

6. <span data-ttu-id="f89f9-173">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-173">Click **Save** button.</span></span>

    ![저장 단추](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="f89f9-175">Hello에 **TINFOIL 보안 구성** 섹션에서 클릭 **TINFOIL SECURITY 구성** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="f89f9-175">On hello **TINFOIL SECURITY Configuration** section, click **Configure TINFOIL SECURITY** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="f89f9-176">복사 hello **SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="f89f9-176">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![TINFOIL SECURITY 구성](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_configure.png) 

8. <span data-ttu-id="f89f9-178">다른 웹 브라우저 창에서 TINFOIL SECURITY 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-178">In a different web browser window, log into your TINFOIL SECURITY company site as an administrator.</span></span>

9. <span data-ttu-id="f89f9-179">도구 모음의 hello hello 위쪽에 클릭 **내 계정**합니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-179">In hello toolbar on hello top, click **My Account**.</span></span>
   
    <span data-ttu-id="f89f9-180">![대시보드](./media/active-directory-saas-tinfoil-security-tutorial/ic798971.png "대시보드")</span><span class="sxs-lookup"><span data-stu-id="f89f9-180">![Dashboard](./media/active-directory-saas-tinfoil-security-tutorial/ic798971.png "Dashboard")</span></span>

10. <span data-ttu-id="f89f9-181">**보안**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-181">Click **Security**.</span></span>
   
    <span data-ttu-id="f89f9-182">![보안](./media/active-directory-saas-tinfoil-security-tutorial/ic798972.png "보안")</span><span class="sxs-lookup"><span data-stu-id="f89f9-182">![Security](./media/active-directory-saas-tinfoil-security-tutorial/ic798972.png "Security")</span></span>

11. <span data-ttu-id="f89f9-183">Hello에 **Single Sign On** 구성 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-183">On hello **Single Sign-On** configuration page, perform hello following steps:</span></span>
   
    <span data-ttu-id="f89f9-184">![Single Sign-On](./media/active-directory-saas-tinfoil-security-tutorial/ic798973.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="f89f9-184">![Single Sign-On](./media/active-directory-saas-tinfoil-security-tutorial/ic798973.png "Single Sign-On")</span></span>
   
    <span data-ttu-id="f89f9-185">a.</span><span class="sxs-lookup"><span data-stu-id="f89f9-185">a.</span></span> <span data-ttu-id="f89f9-186">**SAML 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-186">Select **Enable SAML**.</span></span>
   
    <span data-ttu-id="f89f9-187">b.</span><span class="sxs-lookup"><span data-stu-id="f89f9-187">b.</span></span> <span data-ttu-id="f89f9-188">**수동 구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-188">Click **Manual Configuration**.</span></span>
   
    <span data-ttu-id="f89f9-189">c.</span><span class="sxs-lookup"><span data-stu-id="f89f9-189">c.</span></span> <span data-ttu-id="f89f9-190">**SAML 게시 URL** 붙여넣기 hello 값의 텍스트 상자 **SAML Single Sign-on 서비스 URL** Azure 포털에서 복사한입니다</span><span class="sxs-lookup"><span data-stu-id="f89f9-190">In **SAML Post URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal</span></span>
   
    <span data-ttu-id="f89f9-191">d.</span><span class="sxs-lookup"><span data-stu-id="f89f9-191">d.</span></span> <span data-ttu-id="f89f9-192">**SAML 인증서 지문** 붙여넣기 hello 값의 텍스트 상자 **지문** 에서 복사한 있는 **SAML 서명 인증서** 섹션.</span><span class="sxs-lookup"><span data-stu-id="f89f9-192">In **SAML Certificate Fingerprint** textbox, paste hello value of **Thumbprint** which you have copied from **SAML Signing Certificate** section.</span></span>
  
    <span data-ttu-id="f89f9-193">e.</span><span class="sxs-lookup"><span data-stu-id="f89f9-193">e.</span></span> <span data-ttu-id="f89f9-194">복사 **Your 계정 ID** 값 hello 값에 복사한 **특성 값** 아래 텍스트 상자에 붙여넣습니다 **특성 추가** Azure 포털에서 섹션.</span><span class="sxs-lookup"><span data-stu-id="f89f9-194">Copy **Your Account ID** value and paste hello value in **Attribute Value** textbox under **Add Attribute** section in Azure portal.</span></span>
   
    <span data-ttu-id="f89f9-195">f.</span><span class="sxs-lookup"><span data-stu-id="f89f9-195">f.</span></span> <span data-ttu-id="f89f9-196">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-196">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="f89f9-197">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="f89f9-197">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f89f9-198">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="f89f9-198">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f89f9-199">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f89f9-199">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="f89f9-200">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="f89f9-200">Create an Azure AD test user</span></span>
<span data-ttu-id="f89f9-201">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-201">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="f89f9-203">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="f89f9-203">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f89f9-204">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-204">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f89f9-206">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-206">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![<span data-ttu-id="f89f9-207">사용자 및 그룹 -> 모든 사용자</span><span class="sxs-lookup"><span data-stu-id="f89f9-207">Users and groups -> All users</span></span> ](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f89f9-208">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-208">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![사용자](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f89f9-210">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-210">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f89f9-212">a.</span><span class="sxs-lookup"><span data-stu-id="f89f9-212">a.</span></span> <span data-ttu-id="f89f9-213">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-213">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f89f9-214">b.</span><span class="sxs-lookup"><span data-stu-id="f89f9-214">b.</span></span> <span data-ttu-id="f89f9-215">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-215">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f89f9-216">c.</span><span class="sxs-lookup"><span data-stu-id="f89f9-216">c.</span></span> <span data-ttu-id="f89f9-217">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-217">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f89f9-218">d.</span><span class="sxs-lookup"><span data-stu-id="f89f9-218">d.</span></span> <span data-ttu-id="f89f9-219">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-219">Click **Create**.</span></span>
 
### <a name="create-a-tinfoil-security-test-user"></a><span data-ttu-id="f89f9-220">TINFOIL SECURITY 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="f89f9-220">Create a TINFOIL SECURITY test user</span></span>

<span data-ttu-id="f89f9-221">Tooenable Azure AD 사용자가 toolog TINFOIL SECURITY에 주문 하 고에 TINFOIL SECURITY에 이들 프로 비전 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-221">In order tooenable Azure AD users toolog into TINFOIL SECURITY, they must be provisioned into TINFOIL SECURITY.</span></span> <span data-ttu-id="f89f9-222">Hello TINFOIL SECURITY의 경우에서 프로 비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-222">In hello case of TINFOIL SECURITY, provisioning is a manual task.</span></span>

<span data-ttu-id="f89f9-223">**사용자가 프로 비전, tooget 단계를 수행 하는 hello를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="f89f9-223">**tooget a user provisioned, perform hello following steps:**</span></span>

1. <span data-ttu-id="f89f9-224">너무 필요한 hello 사용자 엔터프라이즈 계정의 일부인 경우[hello TINFOIL SECURITY 지원 팀에 문의](https://www.tinfoilsecurity.com/contact) 만든 tooget hello 사용자 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-224">If hello user is a part of an Enterprise account, you need too[contact hello TINFOIL SECURITY support team](https://www.tinfoilsecurity.com/contact) tooget hello user account created.</span></span>

2. <span data-ttu-id="f89f9-225">Hello 사용자가 일반 TINFOIL SECURITY SaaS 사용자 인 경우 hello 사용자 hello 사용자의 사이트의 공동 작업자 tooany를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-225">If hello user is a regular TINFOIL SECURITY SaaS user, then hello user can add a collaborator tooany of hello user’s sites.</span></span> <span data-ttu-id="f89f9-226">이 트리거는 초대 toohello 지정 된 프로세스 toosend 메일 toocreate 새로운 TINFOIL SECURITY 사용자 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-226">This triggers a process toosend an invitation toohello specified email toocreate a new TINFOIL SECURITY user account.</span></span>

> [!NOTE]
> <span data-ttu-id="f89f9-227">다른 TINFOIL SECURITY 사용자 계정 만들기 도구를 사용할 수 있습니다 또는 Azure AD 사용자 계정을 tooprovision TINFOIL SECURITY에서 제공 된 Api입니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-227">You can use any other TINFOIL SECURITY user account creation tools or APIs provided by TINFOIL SECURITY tooprovision Azure AD user accounts.</span></span>
> 
> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="f89f9-228">Azure AD hello 테스트 사용자를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-228">Assign hello Azure AD test user</span></span>

<span data-ttu-id="f89f9-229">이 섹션에서는 액세스 tooTINFOIL 보안 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-229">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTINFOIL SECURITY.</span></span>

![사용자 할당][200] 

<span data-ttu-id="f89f9-231">**tooassign Britta Simon tooTINFOIL 보안을 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="f89f9-231">**tooassign Britta Simon tooTINFOIL SECURITY, perform hello following steps:**</span></span>

1. <span data-ttu-id="f89f9-232">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-232">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="f89f9-234">Hello 응용 프로그램 목록에서 선택 **TINFOIL SECURITY**합니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-234">In hello applications list, select **TINFOIL SECURITY**.</span></span>

    ![TINFOIL SECURITY 선택](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_app.png) 

3. <span data-ttu-id="f89f9-236">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-236">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="f89f9-238">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-238">Click **Add** button.</span></span> <span data-ttu-id="f89f9-239">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="f89f9-241">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-241">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f89f9-242">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f89f9-243">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="f89f9-244">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="f89f9-244">Test single sign-on</span></span>

<span data-ttu-id="f89f9-245">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-245">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="f89f9-246">Hello 액세스 패널에서에서 hello TINFOIL SECURITY 타일을 클릭할 때 자동으로 로그온 tooyour TINFOIL SECURITY 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-246">When you click hello TINFOIL SECURITY tile in hello Access Panel, you should get automatically signed-on tooyour TINFOIL SECURITY application.</span></span> <span data-ttu-id="f89f9-247">액세스 패널 hello에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f89f9-247">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f89f9-248">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="f89f9-248">Additional resources</span></span>

* [<span data-ttu-id="f89f9-249">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="f89f9-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f89f9-250">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="f89f9-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_203.png

