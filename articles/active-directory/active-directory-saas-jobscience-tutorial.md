---
title: "자습서: Jobscience와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Jobscience 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 77282dcc-bbe2-4728-953d-adb4ab6a713b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 4a4c78aad6d324795a15a9569542afc23b4716d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jobscience"></a><span data-ttu-id="0e739-103">자습서: Jobscience와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="0e739-103">Tutorial: Azure Active Directory integration with Jobscience</span></span>

<span data-ttu-id="0e739-104">이 자습서에 설명 어떻게 toointegrate Jobscience와 Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0e739-104">In this tutorial, you learn how toointegrate Jobscience with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0e739-105">Azure AD와 Jobscience 통합 이점을 다음 hello로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-105">Integrating Jobscience with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0e739-106">액세스 tooJobscience을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-106">You can control in Azure AD who has access tooJobscience</span></span>
- <span data-ttu-id="0e739-107">프로그램 사용자 tooautomatically get 로그온 tooJobscience (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-107">You can enable your users tooautomatically get signed-on tooJobscience (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0e739-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="0e739-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0e739-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="0e739-110">Prerequisites</span></span>

<span data-ttu-id="0e739-111">Jobscience와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-111">tooconfigure Azure AD integration with Jobscience, you need hello following items:</span></span>

- <span data-ttu-id="0e739-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="0e739-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0e739-113">Jobscience Single Sign-On이 가능하도록 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="0e739-113">A Jobscience single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0e739-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0e739-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0e739-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="0e739-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0e739-117">Azure AD 평가판 환경이 없으면 [평가판 제품](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0e739-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="0e739-118">Scenario description</span></span>
<span data-ttu-id="0e739-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0e739-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0e739-121">Jobscience는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="0e739-121">Adding Jobscience from hello gallery</span></span>
2. <span data-ttu-id="0e739-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="0e739-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jobscience-from-hello-gallery"></a><span data-ttu-id="0e739-123">Jobscience는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="0e739-123">Adding Jobscience from hello gallery</span></span>
<span data-ttu-id="0e739-124">tooconfigure hello와의 통합 Jobscience Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Jobscience tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-124">tooconfigure hello integration of Jobscience into Azure AD, you need tooadd Jobscience from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0e739-125">**Jobscience hello 갤러리에서 tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="0e739-125">**tooadd Jobscience from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0e739-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0e739-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0e739-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="0e739-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="0e739-133">Hello 검색 상자에 입력 **Jobscience**합니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-133">In hello search box, type **Jobscience**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_search.png)

5. <span data-ttu-id="0e739-135">Hello 결과 패널에서 선택 **Jobscience**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-135">In hello results panel, select **Jobscience**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0e739-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="0e739-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0e739-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Jobscience에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-138">In this section, you configure and test Azure AD single sign-on with Jobscience based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="0e739-139">Single sign on toowork에 대 한 Azure AD는 tooknow Jobscience에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Jobscience is tooa user in Azure AD.</span></span> <span data-ttu-id="0e739-140">즉, Azure AD 사용자와 Jobscience에 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-140">In other words, a link relationship between an Azure AD user and hello related user in Jobscience needs toobe established.</span></span>

<span data-ttu-id="0e739-141">Jobscience에 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-141">In Jobscience, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="0e739-142">tooconfigure와 Jobscience와 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-142">tooconfigure and test Azure AD single sign-on with Jobscience, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0e739-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0e739-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0e739-145">**[Jobscience 테스트 사용자 만들기](#creating-a-jobscience-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 Jobscience에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-145">**[Creating a Jobscience test user](#creating-a-jobscience-test-user)** - toohave a counterpart of Britta Simon in Jobscience that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0e739-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0e739-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="0e739-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0e739-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="0e739-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0e739-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 Jobscience 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Jobscience application.</span></span>

<span data-ttu-id="0e739-150">**Azure AD tooconfigure single sign on와 Jobscience를 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="0e739-150">**tooconfigure Azure AD single sign-on with Jobscience, perform hello following steps:**</span></span>

1. <span data-ttu-id="0e739-151">Hello hello에 Azure 포털에서에서 **Jobscience** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-151">In hello Azure portal, on hello **Jobscience** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="0e739-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_samlbase.png)

3. <span data-ttu-id="0e739-155">Hello에 **Jobscience 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-155">On hello **Jobscience Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_url.png)

    <span data-ttu-id="0e739-157">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`http://<company name>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="0e739-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern:  `http://<company name>.my.salesforce.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="0e739-158">이 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-158">This value is not real.</span></span> <span data-ttu-id="0e739-159">Hello로이 값을 업데이트 합니다. 실제 로그온 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="0e739-160">이 값을 가져올 [Jobscience 클라이언트 지원 팀](https://www.jobscience.com/support) hello SSO 프로필에서 만들려는 hello 자습서의 뒷부분에서 설명 하는 또는 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-160">Get this value by [Jobscience Client support team](https://www.jobscience.com/support) or from hello SSO profile you will create which is explained later in hello tutorial.</span></span> 
 
4. <span data-ttu-id="0e739-161">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **인증서 (Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_certificate.png) 

5. <span data-ttu-id="0e739-163">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-163">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-jobscience-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0e739-165">Hello에 **Jobscience 구성** 섹션에서 클릭 **구성 Jobscience** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="0e739-165">On hello **Jobscience Configuration** section, click **Configure Jobscience** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="0e739-166">복사 hello **Sign-Out URL, SAML 엔터티 ID, 및 SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="0e739-166">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_configure.png) 

7. <span data-ttu-id="0e739-168">관리자 권한으로 Jobscience 회사 사이트 tooyour에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-168">Log in tooyour Jobscience company site as an administrator.</span></span>

8. <span data-ttu-id="0e739-169">너무 이동**설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-169">Go too**Setup**.</span></span>
   
   <span data-ttu-id="0e739-170">![설치](./media/active-directory-saas-jobscience-tutorial/IC784358.png "설치")</span><span class="sxs-lookup"><span data-stu-id="0e739-170">![Setup](./media/active-directory-saas-jobscience-tutorial/IC784358.png "Setup")</span></span>

9. <span data-ttu-id="0e739-171">Hello 왼쪽된 탐색 창의 hello에 **관리** 섹션에서 클릭 **도메인 관리** tooexpand hello 관련된 섹션을 클릭 하 고 **내 도메인** tooopen hello  **내 도메인** 페이지.</span><span class="sxs-lookup"><span data-stu-id="0e739-171">On hello left navigation pane, in hello **Administer** section, click **Domain Management** tooexpand hello related section, and then click **My Domain** tooopen hello **My Domain** page.</span></span> 
   
   <span data-ttu-id="0e739-172">![내 도메인](./media/active-directory-saas-jobscience-tutorial/ic767825.png "내 도메인")</span><span class="sxs-lookup"><span data-stu-id="0e739-172">![My Domain](./media/active-directory-saas-jobscience-tutorial/ic767825.png "My Domain")</span></span>

10. <span data-ttu-id="0e739-173">도메인에 올바르게 설정 되었는지, tooverify에 있는지 확인 "**단계 4 배포 tooUsers**"를 검토 하 고 프로그램 "**내 도메인 설정**"입니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-173">tooverify that your domain has been set up correctly, make sure that it is in “**Step 4 Deployed tooUsers**” and review your “**My Domain Settings**”.</span></span>

    <span data-ttu-id="0e739-174">![도메인 배포 된 tooUser](./media/active-directory-saas-jobscience-tutorial/ic784377.png "tooUser 도메인 배포")</span><span class="sxs-lookup"><span data-stu-id="0e739-174">![Domain Deployed tooUser](./media/active-directory-saas-jobscience-tutorial/ic784377.png "Domain Deployed tooUser")</span></span>

11. <span data-ttu-id="0e739-175">Hello Jobscience 회사 사이트에서 클릭 **보안 제어**, 클릭 하 고 **Single Sign On 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-175">On hello Jobscience company site, click **Security Controls**, and then click **Single Sign-On Settings**.</span></span>
    
    <span data-ttu-id="0e739-176">![보안 제어](./media/active-directory-saas-jobscience-tutorial/ic784364.png "보안 제어")</span><span class="sxs-lookup"><span data-stu-id="0e739-176">![Security Controls](./media/active-directory-saas-jobscience-tutorial/ic784364.png "Security Controls")</span></span>

12. <span data-ttu-id="0e739-177">Hello에 **Single Sign On 설정** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-177">In hello **Single Sign-On Settings** section, perform hello following steps:</span></span>
    
    <span data-ttu-id="0e739-178">![Single Sign-On 설정](./media/active-directory-saas-jobscience-tutorial/ic781026.png "Single Sign-On 설정")</span><span class="sxs-lookup"><span data-stu-id="0e739-178">![Single Sign-On Settings](./media/active-directory-saas-jobscience-tutorial/ic781026.png "Single Sign-On Settings")</span></span>
    
    <span data-ttu-id="0e739-179">a.</span><span class="sxs-lookup"><span data-stu-id="0e739-179">a.</span></span> <span data-ttu-id="0e739-180">**SAML 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-180">Select **SAML Enabled**.</span></span>

    <span data-ttu-id="0e739-181">b.</span><span class="sxs-lookup"><span data-stu-id="0e739-181">b.</span></span> <span data-ttu-id="0e739-182">**새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-182">Click **New**.</span></span>

13. <span data-ttu-id="0e739-183">Hello에 **SAML Single Sign-on 설정 편집** 대화 상자에서 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-183">On hello **SAML Single Sign-On Setting Edit** dialog, perform hello following steps:</span></span>
    
    <span data-ttu-id="0e739-184">![SAML Single Sign-On 설정](./media/active-directory-saas-jobscience-tutorial/ic784365.png "SAML Single Sign-On 설정")</span><span class="sxs-lookup"><span data-stu-id="0e739-184">![SAML Single Sign-On Setting](./media/active-directory-saas-jobscience-tutorial/ic784365.png "SAML Single Sign-On Setting")</span></span>
    
    <span data-ttu-id="0e739-185">a.</span><span class="sxs-lookup"><span data-stu-id="0e739-185">a.</span></span> <span data-ttu-id="0e739-186">Hello에 **이름** 텍스트 상자, 구성에 대 한 이름 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-186">In hello **Name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="0e739-187">b.</span><span class="sxs-lookup"><span data-stu-id="0e739-187">b.</span></span> <span data-ttu-id="0e739-188">**발급자** 붙여넣기 hello 값의 텍스트 상자 **SAML 엔터티 ID**, Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-188">In **Issuer** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="0e739-189">c.</span><span class="sxs-lookup"><span data-stu-id="0e739-189">c.</span></span> <span data-ttu-id="0e739-190">Hello에 **엔터티 Id** 텍스트 상자`https://salesforce-jobscience.com`</span><span class="sxs-lookup"><span data-stu-id="0e739-190">In hello **Entity Id** textbox, type `https://salesforce-jobscience.com`</span></span>

    <span data-ttu-id="0e739-191">d.</span><span class="sxs-lookup"><span data-stu-id="0e739-191">d.</span></span> <span data-ttu-id="0e739-192">클릭 **찾아보기** tooupload Azure AD 인증서입니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-192">Click **Browse** tooupload your Azure AD certificate.</span></span>

    <span data-ttu-id="0e739-193">e.</span><span class="sxs-lookup"><span data-stu-id="0e739-193">e.</span></span> <span data-ttu-id="0e739-194">으로 **SAML Id 유형**선택, **어설션 hello 사용자 개체에서 hello 페더레이션 ID가 포함 되어**합니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-194">As **SAML Identity Type**, select **Assertion contains hello Federation ID from hello User object**.</span></span>

    <span data-ttu-id="0e739-195">f.</span><span class="sxs-lookup"><span data-stu-id="0e739-195">f.</span></span> <span data-ttu-id="0e739-196">으로 **SAML Id 위치**선택, **Id는 Subject 문의 hello의 hello NameIdentfier 요소**합니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-196">As **SAML Identity Location**, select **Identity is in hello NameIdentfier element of hello Subject statement**.</span></span>

    <span data-ttu-id="0e739-197">g.</span><span class="sxs-lookup"><span data-stu-id="0e739-197">g.</span></span> <span data-ttu-id="0e739-198">**Id 공급자 로그인 URL** 붙여넣기 hello 값의 텍스트 상자 **SAML Single Sign-on 서비스 URL**, Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-198">In **Identity Provider Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="0e739-199">h.</span><span class="sxs-lookup"><span data-stu-id="0e739-199">h.</span></span> <span data-ttu-id="0e739-200">**Id 공급자 로그 아웃 URL** 붙여넣기 hello 값의 텍스트 상자 **Sign-Out URL**, Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-200">In **Identity Provider Logout URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="0e739-201">i.</span><span class="sxs-lookup"><span data-stu-id="0e739-201">i.</span></span> <span data-ttu-id="0e739-202">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-202">Click **Save**.</span></span>

14. <span data-ttu-id="0e739-203">Hello 왼쪽된 탐색 창의 hello에 **관리** 섹션에서 클릭 **도메인 관리** tooexpand hello 관련된 섹션을 클릭 하 고 **내 도메인** tooopen hello  **내 도메인** 페이지.</span><span class="sxs-lookup"><span data-stu-id="0e739-203">On hello left navigation pane, in hello **Administer** section, click **Domain Management** tooexpand hello related section, and then click **My Domain** tooopen hello **My Domain** page.</span></span> 
    
    <span data-ttu-id="0e739-204">![내 도메인](./media/active-directory-saas-jobscience-tutorial/ic767825.png "내 도메인")</span><span class="sxs-lookup"><span data-stu-id="0e739-204">![My Domain](./media/active-directory-saas-jobscience-tutorial/ic767825.png "My Domain")</span></span>

15. <span data-ttu-id="0e739-205">Hello에 **내 도메인** 페이지 hello **로그인 페이지 브랜딩** 섹션에서 클릭 **편집**합니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-205">On hello **My Domain** page, in hello **Login Page Branding** section, click **Edit**.</span></span>
    
    <span data-ttu-id="0e739-206">![로그인 페이지 브랜딩](./media/active-directory-saas-jobscience-tutorial/ic767826.png "로그인 페이지 브랜딩")</span><span class="sxs-lookup"><span data-stu-id="0e739-206">![Login Page Branding](./media/active-directory-saas-jobscience-tutorial/ic767826.png "Login Page Branding")</span></span>

16. <span data-ttu-id="0e739-207">Hello에 **로그인 페이지 브랜딩** 페이지 hello **인증 서비스** 섹션의 hello 이름, 프로그램 **SAML SSO 설정** 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-207">On hello **Login Page Branding** page, in hello **Authentication Service** section, hello name of your **SAML SSO Settings** is displayed.</span></span> <span data-ttu-id="0e739-208">이름을 선택하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-208">Select it, and then click **Save**.</span></span>
    
    <span data-ttu-id="0e739-209">![로그인 페이지 브랜딩](./media/active-directory-saas-jobscience-tutorial/ic784366.png "로그인 페이지 브랜딩")</span><span class="sxs-lookup"><span data-stu-id="0e739-209">![Login Page Branding](./media/active-directory-saas-jobscience-tutorial/ic784366.png "Login Page Branding")</span></span>

17. <span data-ttu-id="0e739-210">tooget hello SP에서 시작한 Single Sign-on 로그인 URL 클릭 hello **Single Sign On 설정** hello에 **보안 제어** 메뉴 섹션.</span><span class="sxs-lookup"><span data-stu-id="0e739-210">tooget hello SP initiated Single Sign on Login URL click on hello **Single Sign On settings** in hello **Security Controls** menu section.</span></span>

    <span data-ttu-id="0e739-211">![보안 제어](./media/active-directory-saas-jobscience-tutorial/ic784368.png "보안 제어")</span><span class="sxs-lookup"><span data-stu-id="0e739-211">![Security Controls](./media/active-directory-saas-jobscience-tutorial/ic784368.png "Security Controls")</span></span>
    
    <span data-ttu-id="0e739-212">위의 hello 단계에서 만든 hello SSO 프로필을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-212">Click hello SSO profile you have created in hello step above.</span></span> <span data-ttu-id="0e739-213">이 페이지 URL에서 귀사에 대 한 Single Sign hello에 표시 (예를 들어 [https://companyname.my.salesforce.com?so=companyid](https://companyname.my.salesforce.com?so=companyid)합니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-213">This page shows hello Single Sign on URL for your company (for example, [https://companyname.my.salesforce.com?so=companyid](https://companyname.my.salesforce.com?so=companyid).</span></span>    

> [!TIP]
> <span data-ttu-id="0e739-214">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="0e739-214">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0e739-215">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="0e739-215">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0e739-216">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0e739-216">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0e739-217">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="0e739-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="0e739-218">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-218">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="0e739-220">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="0e739-220">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0e739-221">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-221">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-jobscience-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0e739-223">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-223">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-jobscience-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0e739-225">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-225">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-jobscience-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0e739-227">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-227">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-jobscience-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0e739-229">a.</span><span class="sxs-lookup"><span data-stu-id="0e739-229">a.</span></span> <span data-ttu-id="0e739-230">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-230">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0e739-231">b.</span><span class="sxs-lookup"><span data-stu-id="0e739-231">b.</span></span> <span data-ttu-id="0e739-232">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-232">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0e739-233">c.</span><span class="sxs-lookup"><span data-stu-id="0e739-233">c.</span></span> <span data-ttu-id="0e739-234">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-234">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0e739-235">d.</span><span class="sxs-lookup"><span data-stu-id="0e739-235">d.</span></span> <span data-ttu-id="0e739-236">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-236">Click **Create**.</span></span>
 
### <a name="creating-a-jobscience-test-user"></a><span data-ttu-id="0e739-237">Jobscience 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="0e739-237">Creating a Jobscience test user</span></span>

<span data-ttu-id="0e739-238">Tooenable Azure AD 사용자가 toolog tooJobscience에 주문 하 고에 Jobscience에 이들 프로 비전 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-238">In order tooenable Azure AD users toolog in tooJobscience, they must be provisioned into Jobscience.</span></span> <span data-ttu-id="0e739-239">Hello Jobscience의 경우에서 프로 비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-239">In hello case of Jobscience, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="0e739-240">다른 Jobscience 사용자 계정 만들기 도구를 사용할 수 있습니다 또는 사용자 계정을 Jobscience tooprovision Azure Active Directory에서 제공 된 Api입니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-240">You can use any other Jobscience user account creation tools or APIs provided by Jobscience tooprovision Azure Active Directory user accounts.</span></span>
>  
        
<span data-ttu-id="0e739-241">**tooconfigure 사용자 프로비저닝, hello 다음 단계를 수행:**</span><span class="sxs-lookup"><span data-stu-id="0e739-241">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="0e739-242">Tooyour 로그인 **Jobscience** 회사 사이트에서 관리자 권한으로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-242">Log in tooyour **Jobscience** company site as administrator.</span></span>

2. <span data-ttu-id="0e739-243">TooSetup 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-243">Go tooSetup.</span></span>
   
   <span data-ttu-id="0e739-244">![설치](./media/active-directory-saas-jobscience-tutorial/ic784358.png "설치")</span><span class="sxs-lookup"><span data-stu-id="0e739-244">![Setup](./media/active-directory-saas-jobscience-tutorial/ic784358.png "Setup")</span></span>
3. <span data-ttu-id="0e739-245">너무 이동**사용자 관리 \> 사용자**합니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-245">Go too**Manage Users \> Users**.</span></span>
   
   <span data-ttu-id="0e739-246">![사용자](./media/active-directory-saas-jobscience-tutorial/ic784369.png "사용자")</span><span class="sxs-lookup"><span data-stu-id="0e739-246">![Users](./media/active-directory-saas-jobscience-tutorial/ic784369.png "Users")</span></span>
4. <span data-ttu-id="0e739-247">**새 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-247">Click **New User**.</span></span>
   
   <span data-ttu-id="0e739-248">![모든 사용자](./media/active-directory-saas-jobscience-tutorial/ic784370.png "모든 사용자")</span><span class="sxs-lookup"><span data-stu-id="0e739-248">![All Users](./media/active-directory-saas-jobscience-tutorial/ic784370.png "All Users")</span></span>
5. <span data-ttu-id="0e739-249">Hello에 **사용자 편집** 대화 상자에서 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-249">On hello **Edit User** dialog, perform hello following steps:</span></span>
   
   <span data-ttu-id="0e739-250">![사용자 편집](./media/active-directory-saas-jobscience-tutorial/ic784371.png "사용자 편집")</span><span class="sxs-lookup"><span data-stu-id="0e739-250">![User Edit](./media/active-directory-saas-jobscience-tutorial/ic784371.png "User Edit")</span></span>
   
   <span data-ttu-id="0e739-251">a.</span><span class="sxs-lookup"><span data-stu-id="0e739-251">a.</span></span> <span data-ttu-id="0e739-252">Hello에 **이름** 텍스트 상자 Britta 같은 hello 사용자의 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-252">In hello **First Name** textbox, type a first name of hello user like Britta.</span></span>
   
   <span data-ttu-id="0e739-253">b.</span><span class="sxs-lookup"><span data-stu-id="0e739-253">b.</span></span> <span data-ttu-id="0e739-254">Hello에 **성** textbox Simon 같은 hello 사용자의 성을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-254">In hello **Last Name** textbox, type a last name of hello user like Simon.</span></span>
   
   <span data-ttu-id="0e739-255">c.</span><span class="sxs-lookup"><span data-stu-id="0e739-255">c.</span></span> <span data-ttu-id="0e739-256">Hello에 **별칭** textbox brittas 같은 hello 사용자의 별칭 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-256">In hello **Alias** textbox, type an alias name of hello user like brittas.</span></span>

   <span data-ttu-id="0e739-257">d.</span><span class="sxs-lookup"><span data-stu-id="0e739-257">d.</span></span> <span data-ttu-id="0e739-258">Hello에 **전자 메일** textbox, 사용자의 hello 전자 메일 주소를 입력 같은 Brittasimon@contoso.com합니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-258">In hello **Email** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>

   <span data-ttu-id="0e739-259">e.</span><span class="sxs-lookup"><span data-stu-id="0e739-259">e.</span></span> <span data-ttu-id="0e739-260">Hello에 **사용자 이름** 텍스트 상자에 사용자의 사용자 이름을 같은 Brittasimon@contoso.com합니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-260">In hello **User Name** textbox, type a user name of user like Brittasimon@contoso.com.</span></span>

   <span data-ttu-id="0e739-261">f.</span><span class="sxs-lookup"><span data-stu-id="0e739-261">f.</span></span> <span data-ttu-id="0e739-262">Hello에 **Nick 이름** textbox nick Simon와 같은 사용자의 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-262">In hello **Nick Name** textbox, type a nick name of user like Simon.</span></span>

   <span data-ttu-id="0e739-263">g.</span><span class="sxs-lookup"><span data-stu-id="0e739-263">g.</span></span> <span data-ttu-id="0e739-264">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-264">Click **Save**.</span></span>

    
> [!NOTE]
> <span data-ttu-id="0e739-265">hello Azure Active Directory 계정 소유자는 전자 메일을 수신 하을 따라 활성화 링크 tooconfirm 자신의 계정의 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-265">hello Azure Active Directory account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="0e739-266">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-266">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="0e739-267">이 섹션에서는 tooJobscience 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-267">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooJobscience.</span></span>

![사용자 할당][200] 

<span data-ttu-id="0e739-269">**tooassign Britta Simon tooJobscience hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="0e739-269">**tooassign Britta Simon tooJobscience, perform hello following steps:**</span></span>

1. <span data-ttu-id="0e739-270">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-270">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="0e739-272">Hello 응용 프로그램 목록에서 선택 **Jobscience**합니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-272">In hello applications list, select **Jobscience**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_app.png) 

3. <span data-ttu-id="0e739-274">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-274">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="0e739-276">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-276">Click **Add** button.</span></span> <span data-ttu-id="0e739-277">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-277">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="0e739-279">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-279">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0e739-280">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-280">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0e739-281">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-281">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0e739-282">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="0e739-282">Testing single sign-on</span></span>

<span data-ttu-id="0e739-283">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-283">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="0e739-284">Hello 액세스 패널에서에서 hello Jobscience 타일을 클릭할 때 자동으로 로그온 tooyour Jobscience 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-284">When you click hello Jobscience tile in hello Access Panel, you should get automatically signed-on tooyour Jobscience application.</span></span>
<span data-ttu-id="0e739-285">액세스 패널 hello에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0e739-285">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0e739-286">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="0e739-286">Additional resources</span></span>

* [<span data-ttu-id="0e739-287">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="0e739-287">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0e739-288">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="0e739-288">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_203.png

