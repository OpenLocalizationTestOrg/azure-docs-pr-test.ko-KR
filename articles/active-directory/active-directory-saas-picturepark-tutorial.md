---
title: "자습서: Picturepark와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Picturepark 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 31c21cd4-9c00-4cad-9538-a13996dc872f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: jeedes
ms.openlocfilehash: 3d826d3f73aad2f0d123f8697c6caafad7bc926a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-picturepark"></a><span data-ttu-id="d78f6-103">자습서: Picturepark와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="d78f6-103">Tutorial: Azure Active Directory integration with Picturepark</span></span>

<span data-ttu-id="d78f6-104">이 자습서에 설명 어떻게 toointegrate Azure Active Directory (Azure AD)와 Picturepark 합니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-104">In this tutorial, you learn how toointegrate Picturepark with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d78f6-105">Azure AD와 Picturepark 통합 이점을 다음 hello로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-105">Integrating Picturepark with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d78f6-106">액세스 tooPicturepark을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-106">You can control in Azure AD who has access tooPicturepark</span></span>
- <span data-ttu-id="d78f6-107">프로그램 사용자 tooautomatically get 로그온 tooPicturepark (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-107">You can enable your users tooautomatically get signed-on tooPicturepark (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d78f6-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="d78f6-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d78f6-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d78f6-110">Prerequisites</span></span>

<span data-ttu-id="d78f6-111">Picturepark와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-111">tooconfigure Azure AD integration with Picturepark, you need hello following items:</span></span>

- <span data-ttu-id="d78f6-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="d78f6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d78f6-113">Picturepark Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="d78f6-113">A Picturepark single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d78f6-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d78f6-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d78f6-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="d78f6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d78f6-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d78f6-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="d78f6-118">Scenario description</span></span>
<span data-ttu-id="d78f6-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d78f6-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d78f6-121">Picturepark는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="d78f6-121">Adding Picturepark from hello gallery</span></span>
2. <span data-ttu-id="d78f6-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="d78f6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-picturepark-from-hello-gallery"></a><span data-ttu-id="d78f6-123">Picturepark는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="d78f6-123">Adding Picturepark from hello gallery</span></span>
<span data-ttu-id="d78f6-124">tooconfigure hello와의 통합 Picturepark Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Picturepark tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-124">tooconfigure hello integration of Picturepark into Azure AD, you need tooadd Picturepark from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d78f6-125">**Picturepark hello 갤러리에서 tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="d78f6-125">**tooadd Picturepark from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d78f6-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d78f6-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d78f6-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="d78f6-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="d78f6-133">Hello 검색 상자에 입력 **Picturepark**합니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-133">In hello search box, type **Picturepark**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_search.png)

5. <span data-ttu-id="d78f6-135">Hello 결과 패널에서 선택 **Picturepark**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-135">In hello results panel, select **Picturepark**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d78f6-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="d78f6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d78f6-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 사용하여 Picturepark에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-138">In this section, you configure and test Azure AD single sign-on with Picturepark based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d78f6-139">Single sign on toowork에 대 한 Azure AD는 tooknow Picturepark에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Picturepark is tooa user in Azure AD.</span></span> <span data-ttu-id="d78f6-140">즉, Azure AD 사용자와 Picturepark에 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-140">In other words, a link relationship between an Azure AD user and hello related user in Picturepark needs toobe established.</span></span>

<span data-ttu-id="d78f6-141">Picturepark에 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-141">In Picturepark, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="d78f6-142">tooconfigure와 Picturepark 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-142">tooconfigure and test Azure AD single sign-on with Picturepark, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d78f6-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d78f6-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d78f6-145">**[Picturepark 테스트 사용자 만들기](#creating-a-picturepark-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 Picturepark에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-145">**[Creating a Picturepark test user](#creating-a-picturepark-test-user)** - toohave a counterpart of Britta Simon in Picturepark that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="d78f6-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d78f6-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="d78f6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d78f6-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="d78f6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d78f6-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 Picturepark 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Picturepark application.</span></span>

<span data-ttu-id="d78f6-150">**Azure AD tooconfigure single sign on와 Picturepark를 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="d78f6-150">**tooconfigure Azure AD single sign-on with Picturepark, perform hello following steps:**</span></span>

1. <span data-ttu-id="d78f6-151">Hello hello에 Azure 포털에서에서 **Picturepark** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-151">In hello Azure portal, on hello **Picturepark** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="d78f6-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_samlbase.png)

3. <span data-ttu-id="d78f6-155">Hello에 **Picturepark 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-155">On hello **Picturepark Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_url.png)

    <span data-ttu-id="d78f6-157">a.</span><span class="sxs-lookup"><span data-stu-id="d78f6-157">a.</span></span> <span data-ttu-id="d78f6-158">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<companyname>.picturepark.com`</span><span class="sxs-lookup"><span data-stu-id="d78f6-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.picturepark.com`</span></span>

    <span data-ttu-id="d78f6-159">b.</span><span class="sxs-lookup"><span data-stu-id="d78f6-159">b.</span></span> <span data-ttu-id="d78f6-160">Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:</span><span class="sxs-lookup"><span data-stu-id="d78f6-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span> 
    
    |  |
    |--|
    | `https://<companyname>.current-picturepark.com`|
    | `https://<companyname>.picturepark.com`|
    | `https://<companyname>.next-picturepark.com`|
    | |

    > [!NOTE] 
    > <span data-ttu-id="d78f6-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-161">These values are not real.</span></span> <span data-ttu-id="d78f6-162">이러한 항목을 업데이트 로그온 URL과 식별자 실제 hello로 값입니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="d78f6-163">연락처 [Picturepark 클라이언트 지원 팀](https://picturepark.com/about/contact/) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-163">Contact [Picturepark Client support team](https://picturepark.com/about/contact/) tooget these values.</span></span> 
 
4. <span data-ttu-id="d78f6-164">Hello에 **SAML 서명 인증서** 섹션을 복사 hello **지문** 인증서의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-164">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_certificate.png) 

5. <span data-ttu-id="d78f6-166">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-166">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-picturepark-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d78f6-168">Hello에 **Picturepark 구성** 섹션에서 클릭 **구성 Picturepark** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="d78f6-168">On hello **Picturepark Configuration** section, click **Configure Picturepark** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="d78f6-169">복사 hello **SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="d78f6-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_configure.png) 

7. <span data-ttu-id="d78f6-171">다른 웹 브라우저 창에서 Picturepark 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-171">In a different web browser window, log into your Picturepark company site as an administrator.</span></span>

8. <span data-ttu-id="d78f6-172">도구 모음의 hello hello 위쪽에 클릭 **관리 도구**, 클릭 하 고 **관리 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-172">In hello toolbar on hello top, click **Administrative tools**, and then click **Management Console**.</span></span>
   
    <span data-ttu-id="d78f6-173">![관리 콘솔](./media/active-directory-saas-picturepark-tutorial/ic795062.png "관리 콘솔")</span><span class="sxs-lookup"><span data-stu-id="d78f6-173">![Management Console](./media/active-directory-saas-picturepark-tutorial/ic795062.png "Management Console")</span></span>

9. <span data-ttu-id="d78f6-174">**인증**을 클릭한 다음 **ID 공급자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-174">Click **Authentication**, and then click **Identity providers**.</span></span>
   
    <span data-ttu-id="d78f6-175">![인증](./media/active-directory-saas-picturepark-tutorial/ic795063.png "인증")</span><span class="sxs-lookup"><span data-stu-id="d78f6-175">![Authentication](./media/active-directory-saas-picturepark-tutorial/ic795063.png "Authentication")</span></span>

10. <span data-ttu-id="d78f6-176">Hello에 **Id 공급자 구성** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-176">In hello **Identity provider configuration** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="d78f6-177">![ID 공급자 구성](./media/active-directory-saas-picturepark-tutorial/ic795064.png "ID 공급자 구성")</span><span class="sxs-lookup"><span data-stu-id="d78f6-177">![Identity provider configuration](./media/active-directory-saas-picturepark-tutorial/ic795064.png "Identity provider configuration")</span></span>
   
    <span data-ttu-id="d78f6-178">a.</span><span class="sxs-lookup"><span data-stu-id="d78f6-178">a.</span></span> <span data-ttu-id="d78f6-179">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-179">Click **Add**.</span></span>
  
    <span data-ttu-id="d78f6-180">b.</span><span class="sxs-lookup"><span data-stu-id="d78f6-180">b.</span></span> <span data-ttu-id="d78f6-181">구성 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-181">Type a name for your configuration.</span></span>
   
    <span data-ttu-id="d78f6-182">c.</span><span class="sxs-lookup"><span data-stu-id="d78f6-182">c.</span></span> <span data-ttu-id="d78f6-183">**기본값으로 설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-183">Select **Set as default**.</span></span>
   
    <span data-ttu-id="d78f6-184">d.</span><span class="sxs-lookup"><span data-stu-id="d78f6-184">d.</span></span> <span data-ttu-id="d78f6-185">**Issuer URI** 붙여넣기 hello 값의 텍스트 상자 **SAML Single Sign-on 서비스 URL** Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-185">In **Issuer URI** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="d78f6-186">e.</span><span class="sxs-lookup"><span data-stu-id="d78f6-186">e.</span></span> <span data-ttu-id="d78f6-187">**신뢰할 수 있는 발급자 지문** 붙여넣기 hello 값의 텍스트 상자 **지문** 에서 복사한 있는 **SAML 서명 인증서** 섹션.</span><span class="sxs-lookup"><span data-stu-id="d78f6-187">In **Trusted Issuer Thumb Print** textbox, paste hello value of **Thumbprint** which you have copied from **SAML Signing Certificate** section.</span></span> 

11. <span data-ttu-id="d78f6-188">**JoinDefaultUsersGroup**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-188">Click **JoinDefaultUsersGroup**.</span></span>

12. <span data-ttu-id="d78f6-189">tooset hello **Emailaddress** hello에 대 한 특성 **클레임** 텍스트 상자에 `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress` 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-189">tooset hello **Emailaddress** attribute in hello **Claim** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress` and click **Save**.</span></span>

      <span data-ttu-id="d78f6-190">![구성](./media/active-directory-saas-picturepark-tutorial/ic795065.png "구성")</span><span class="sxs-lookup"><span data-stu-id="d78f6-190">![Configuration](./media/active-directory-saas-picturepark-tutorial/ic795065.png "Configuration")</span></span>

> [!TIP]
> <span data-ttu-id="d78f6-191">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="d78f6-191">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d78f6-192">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="d78f6-192">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d78f6-193">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d78f6-193">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d78f6-194">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="d78f6-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="d78f6-195">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-195">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="d78f6-197">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="d78f6-197">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d78f6-198">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-198">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-picturepark-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d78f6-200">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-200">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-picturepark-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d78f6-202">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-202">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-picturepark-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d78f6-204">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-204">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-picturepark-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d78f6-206">a.</span><span class="sxs-lookup"><span data-stu-id="d78f6-206">a.</span></span> <span data-ttu-id="d78f6-207">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-207">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d78f6-208">b.</span><span class="sxs-lookup"><span data-stu-id="d78f6-208">b.</span></span> <span data-ttu-id="d78f6-209">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-209">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d78f6-210">c.</span><span class="sxs-lookup"><span data-stu-id="d78f6-210">c.</span></span> <span data-ttu-id="d78f6-211">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-211">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d78f6-212">d.</span><span class="sxs-lookup"><span data-stu-id="d78f6-212">d.</span></span> <span data-ttu-id="d78f6-213">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-213">Click **Create**.</span></span>
 
### <a name="creating-a-picturepark-test-user"></a><span data-ttu-id="d78f6-214">Picturepark 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="d78f6-214">Creating a Picturepark test user</span></span>

<span data-ttu-id="d78f6-215">Tooenable Azure AD 사용자가 toolog Picturepark에 주문 하 고에 Picturepark에 이들 프로 비전 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-215">In order tooenable Azure AD users toolog into Picturepark, they must be provisioned into Picturepark.</span></span> <span data-ttu-id="d78f6-216">Hello Picturepark의 경우에서 프로 비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-216">In hello case of Picturepark, provisioning is a manual task.</span></span>

<span data-ttu-id="d78f6-217">**tooprovision 사용자 계정을 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="d78f6-217">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="d78f6-218">Tooyour 로그인 **Picturepark** 테 넌 트입니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-218">Log in tooyour **Picturepark** tenant.</span></span>

2. <span data-ttu-id="d78f6-219">도구 모음의 hello hello 위쪽에 클릭 **관리 도구**, 클릭 하 고 **사용자**합니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-219">In hello toolbar on hello top, click **Administrative tools**, and then click **Users**.</span></span>
   
    <span data-ttu-id="d78f6-220">![사용자](./media/active-directory-saas-picturepark-tutorial/ic795067.png "사용자")</span><span class="sxs-lookup"><span data-stu-id="d78f6-220">![Users](./media/active-directory-saas-picturepark-tutorial/ic795067.png "Users")</span></span>

3. <span data-ttu-id="d78f6-221">Hello에 **사용자 개요** 탭을 클릭 **새로**합니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-221">In hello **Users overview** tab, click **New**.</span></span>
   
    <span data-ttu-id="d78f6-222">![사용자 관리](./media/active-directory-saas-picturepark-tutorial/ic795068.png "사용자 관리")</span><span class="sxs-lookup"><span data-stu-id="d78f6-222">![User management](./media/active-directory-saas-picturepark-tutorial/ic795068.png "User management")</span></span>

4. <span data-ttu-id="d78f6-223">Hello에 **사용자 만들기** 대화 상자에서 hello 수행 tooprovision 하려는 유효한 Azure Active Directory 사용자의 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-223">On hello **Create User** dialog, perform hello following steps of a valid Azure Active Directory User you want tooprovision:</span></span>
   
    <span data-ttu-id="d78f6-224">![사용자 만들기](./media/active-directory-saas-picturepark-tutorial/ic795069.png "사용자 만들기")</span><span class="sxs-lookup"><span data-stu-id="d78f6-224">![Create User](./media/active-directory-saas-picturepark-tutorial/ic795069.png "Create User")</span></span>
   
    <span data-ttu-id="d78f6-225">a.</span><span class="sxs-lookup"><span data-stu-id="d78f6-225">a.</span></span> <span data-ttu-id="d78f6-226">Hello에 **전자 메일 주소** 텍스트 형식 hello **전자 메일 주소** hello 사용자의  **BrittaSimon@contoso.com** 합니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-226">In hello **Email Address** textbox, type hello **email address** of hello user **BrittaSimon@contoso.com**.</span></span>  
   
    <span data-ttu-id="d78f6-227">b.</span><span class="sxs-lookup"><span data-stu-id="d78f6-227">b.</span></span> <span data-ttu-id="d78f6-228">Hello에 **암호** 및 **암호 확인** 텍스트 상자, 형식 hello **암호** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-228">In hello **Password** and **Confirm Password** textboxes, type hello **password** of BrittaSimon.</span></span> 
   
    <span data-ttu-id="d78f6-229">c.</span><span class="sxs-lookup"><span data-stu-id="d78f6-229">c.</span></span> <span data-ttu-id="d78f6-230">Hello에 **이름** 텍스트 형식 hello **이름** hello 사용자의 **Britta**합니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-230">In hello **First Name** textbox, type hello **First Name** of hello user **Britta**.</span></span> 
   
    <span data-ttu-id="d78f6-231">d.</span><span class="sxs-lookup"><span data-stu-id="d78f6-231">d.</span></span> <span data-ttu-id="d78f6-232">Hello에 **성** 텍스트 형식 hello **성** hello 사용자의 **Simon**합니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-232">In hello **Last Name** textbox, type hello **Last Name** of hello user **Simon**.</span></span>
   
    <span data-ttu-id="d78f6-233">e.</span><span class="sxs-lookup"><span data-stu-id="d78f6-233">e.</span></span> <span data-ttu-id="d78f6-234">Hello에 **회사** 텍스트 형식 hello **회사 이름** hello 사용자의 합니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-234">In hello **Company** textbox, type hello **Company name** of hello user.</span></span> 
   
    <span data-ttu-id="d78f6-235">f.</span><span class="sxs-lookup"><span data-stu-id="d78f6-235">f.</span></span> <span data-ttu-id="d78f6-236">Hello에 **국가** 텍스트 선택 hello **국가** hello 사용자의 합니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-236">In hello **Country** textbox, select hello **Country** of hello user.</span></span>
  
    <span data-ttu-id="d78f6-237">g.</span><span class="sxs-lookup"><span data-stu-id="d78f6-237">g.</span></span> <span data-ttu-id="d78f6-238">Hello에 **ZIP** 텍스트 형식 hello **우편 번호** hello 도시 합니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-238">In hello **ZIP** textbox, type hello **ZIP code** of hello city.</span></span>
   
    <span data-ttu-id="d78f6-239">h.</span><span class="sxs-lookup"><span data-stu-id="d78f6-239">h.</span></span> <span data-ttu-id="d78f6-240">Hello에 **도시** 텍스트 형식 hello **도시 이름을** hello 사용자의 합니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-240">In hello **City** textbox, type hello **City name** of hello user.</span></span>

    <span data-ttu-id="d78f6-241">i.</span><span class="sxs-lookup"><span data-stu-id="d78f6-241">i.</span></span> <span data-ttu-id="d78f6-242">**언어**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-242">Select a **Language**.</span></span>
   
    <span data-ttu-id="d78f6-243">j.</span><span class="sxs-lookup"><span data-stu-id="d78f6-243">j.</span></span> <span data-ttu-id="d78f6-244">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-244">Click **Create**.</span></span>

>[!NOTE]
><span data-ttu-id="d78f6-245">다른 Picturepark 사용자 계정 만들기 도구를 사용할 수 있습니다 또는 Azure AD 사용자 계정을 tooprovision Picturepark에서 제공 된 Api입니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-245">You can use any other Picturepark user account creation tools or APIs provided by Picturepark tooprovision Azure AD user accounts.</span></span>
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d78f6-246">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-246">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d78f6-247">이 섹션에서는 tooPicturepark 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-247">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPicturepark.</span></span>

![사용자 할당][200] 

<span data-ttu-id="d78f6-249">**tooassign Britta Simon tooPicturepark hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="d78f6-249">**tooassign Britta Simon tooPicturepark, perform hello following steps:**</span></span>

1. <span data-ttu-id="d78f6-250">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-250">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="d78f6-252">Hello 응용 프로그램 목록에서 선택 **Picturepark**합니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-252">In hello applications list, select **Picturepark**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_app.png) 

3. <span data-ttu-id="d78f6-254">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-254">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="d78f6-256">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-256">Click **Add** button.</span></span> <span data-ttu-id="d78f6-257">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-257">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="d78f6-259">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-259">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d78f6-260">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-260">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d78f6-261">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-261">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d78f6-262">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="d78f6-262">Testing single sign-on</span></span>

<span data-ttu-id="d78f6-263">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-263">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="d78f6-264">Hello 액세스 패널에서에서 hello Picturepark 타일을 클릭할 때 자동으로 로그온 tooyour Picturepark 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-264">When you click hello Picturepark tile in hello Access Panel, you should get automatically signed-on tooyour Picturepark application.</span></span> <span data-ttu-id="d78f6-265">액세스 패널 hello에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d78f6-265">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d78f6-266">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="d78f6-266">Additional resources</span></span>

* [<span data-ttu-id="d78f6-267">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="d78f6-267">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d78f6-268">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="d78f6-268">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_203.png

