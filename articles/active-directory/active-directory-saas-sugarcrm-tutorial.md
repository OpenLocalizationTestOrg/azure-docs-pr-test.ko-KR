---
title: "자습서: Sugar CRM과 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Sugar CRM 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3331b9fc-ebc0-4a3a-9f7b-bf20ee35d180
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: 108d2f8125e410743ee7bc48883a1d0b00602615
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sugar-crm"></a><span data-ttu-id="65ef4-103">자습서: Sugar CRM과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="65ef4-103">Tutorial: Azure Active Directory integration with Sugar CRM</span></span>

<span data-ttu-id="65ef4-104">이 자습서에 설명 어떻게 toointegrate Azure Active Directory (Azure AD)와 Sugar CRM 합니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-104">In this tutorial, you learn how toointegrate Sugar CRM with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="65ef4-105">Sugar CRM Azure AD와 통합 hello 다음 이점을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-105">Integrating Sugar CRM with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="65ef4-106">액세스 tooSugar CRM을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-106">You can control in Azure AD who has access tooSugar CRM</span></span>
- <span data-ttu-id="65ef4-107">프로그램 사용자 tooautomatically get 로그온 tooSugar CRM (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-107">You can enable your users tooautomatically get signed-on tooSugar CRM (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="65ef4-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="65ef4-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="65ef4-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="65ef4-110">Prerequisites</span></span>

<span data-ttu-id="65ef4-111">Sugar CRM와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-111">tooconfigure Azure AD integration with Sugar CRM, you need hello following items:</span></span>

- <span data-ttu-id="65ef4-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="65ef4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="65ef4-113">Sugar CRM Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="65ef4-113">A Sugar CRM single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="65ef4-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="65ef4-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="65ef4-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="65ef4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="65ef4-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="65ef4-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="65ef4-118">Scenario description</span></span>
<span data-ttu-id="65ef4-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="65ef4-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="65ef4-121">Sugar CRM hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="65ef4-121">Adding Sugar CRM from hello gallery</span></span>
2. <span data-ttu-id="65ef4-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="65ef4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sugar-crm-from-hello-gallery"></a><span data-ttu-id="65ef4-123">Sugar CRM hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="65ef4-123">Adding Sugar CRM from hello gallery</span></span>
<span data-ttu-id="65ef4-124">tooconfigure hello와의 통합 Sugar CRM Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Sugar CRM tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-124">tooconfigure hello integration of Sugar CRM into Azure AD, you need tooadd Sugar CRM from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="65ef4-125">**Sugar CRM hello 갤러리에서 tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="65ef4-125">**tooadd Sugar CRM from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="65ef4-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="65ef4-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="65ef4-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="65ef4-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="65ef4-133">Hello 검색 상자에 입력 **Sugar CRM**합니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-133">In hello search box, type **Sugar CRM**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_search.png)

5. <span data-ttu-id="65ef4-135">Hello 결과 패널에서 선택 **Sugar CRM**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-135">In hello results panel, select **Sugar CRM**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="65ef4-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="65ef4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="65ef4-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Sugar CRM에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-138">In this section, you configure and test Azure AD single sign-on with Sugar CRM based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="65ef4-139">Single sign on toowork에 대 한 Azure AD는 tooknow Sugar CRM에서 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Sugar CRM is tooa user in Azure AD.</span></span> <span data-ttu-id="65ef4-140">즉, Azure AD 사용자와 Sugar CRM에서 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-140">In other words, a link relationship between an Azure AD user and hello related user in Sugar CRM needs toobe established.</span></span>

<span data-ttu-id="65ef4-141">Sugar CRM에서 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-141">In Sugar CRM, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="65ef4-142">tooconfigure 및 Sugar CRM를 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-142">tooconfigure and test Azure AD single sign-on with Sugar CRM, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="65ef4-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="65ef4-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="65ef4-145">**[Sugar CRM 테스트 사용자 만들기](#creating-a-sugar-crm-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 Sugar CRM에서 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-145">**[Creating a Sugar CRM test user](#creating-a-sugar-crm-test-user)** - toohave a counterpart of Britta Simon in Sugar CRM that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="65ef4-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="65ef4-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="65ef4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="65ef4-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="65ef4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="65ef4-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 Sugar CRM 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Sugar CRM application.</span></span>

<span data-ttu-id="65ef4-150">**tooconfigure Azure AD single sign on Sugar CRM과 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="65ef4-150">**tooconfigure Azure AD single sign-on with Sugar CRM, perform hello following steps:**</span></span>

1. <span data-ttu-id="65ef4-151">Hello hello에 Azure 포털에서에서 **Sugar CRM** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-151">In hello Azure portal, on hello **Sugar CRM** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="65ef4-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_samlbase.png)

3. <span data-ttu-id="65ef4-155">Hello에 **Sugar CRM 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-155">On hello **Sugar CRM Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_url.png)

    <span data-ttu-id="65ef4-157">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:</span><span class="sxs-lookup"><span data-stu-id="65ef4-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.sugarondemand.com` |
    | `https://<companyname>.trial.sugarcrm` |

    > [!NOTE] 
    > <span data-ttu-id="65ef4-158">hello 값이 실제 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-158">hello value is not real.</span></span> <span data-ttu-id="65ef4-159">업데이트 hello 값과 실제 로그온 URL hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="65ef4-160">연락처 [Sugar CRM 클라이언트 지원 팀](https://support.sugarcrm.com/) tooget hello 값입니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-160">Contact [Sugar CRM Client support team](https://support.sugarcrm.com/) tooget hello value.</span></span> 
 
4. <span data-ttu-id="65ef4-161">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **인증서 (Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_certificate.png) 

5. <span data-ttu-id="65ef4-163">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-163">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="65ef4-165">Hello에 **Sugar CRM 구성** 섹션에서 클릭 **구성 Sugar CRM** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="65ef4-165">On hello **Sugar CRM Configuration** section, click **Configure Sugar CRM** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="65ef4-166">복사 hello **Sign-Out URL 및 SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="65ef4-166">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_configure.png) 

7. <span data-ttu-id="65ef4-168">다른 웹 브라우저 창에서 관리자 권한으로 tooyour Sugar CRM 회사 사이트에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-168">In a different web browser window, log in tooyour Sugar CRM company site as an administrator.</span></span>

8. <span data-ttu-id="65ef4-169">너무 이동**Admin**합니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-169">Go too**Admin**.</span></span>
   
    <span data-ttu-id="65ef4-170">![관리자](./media/active-directory-saas-sugarcrm-tutorial/ic795888.png "관리자")</span><span class="sxs-lookup"><span data-stu-id="65ef4-170">![Admin](./media/active-directory-saas-sugarcrm-tutorial/ic795888.png "Admin")</span></span>

9. <span data-ttu-id="65ef4-171">Hello에 **관리** 섹션에서 클릭 **암호 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-171">In hello **Administration** section, click **Password Management**.</span></span>
   
    <span data-ttu-id="65ef4-172">![관리](./media/active-directory-saas-sugarcrm-tutorial/ic795889.png "관리")</span><span class="sxs-lookup"><span data-stu-id="65ef4-172">![Administration](./media/active-directory-saas-sugarcrm-tutorial/ic795889.png "Administration")</span></span>

10. <span data-ttu-id="65ef4-173">**SAML 인증 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-173">Select **Enable SAML Authentication**.</span></span>
   
    <span data-ttu-id="65ef4-174">![관리](./media/active-directory-saas-sugarcrm-tutorial/ic795890.png "관리")</span><span class="sxs-lookup"><span data-stu-id="65ef4-174">![Administration](./media/active-directory-saas-sugarcrm-tutorial/ic795890.png "Administration")</span></span>

11. <span data-ttu-id="65ef4-175">Hello에 **SAML 인증** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-175">In hello **SAML Authentication** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="65ef4-176">![SAML 인증](./media/active-directory-saas-sugarcrm-tutorial/ic795891.png "SAML 인증")</span><span class="sxs-lookup"><span data-stu-id="65ef4-176">![SAML Authentication](./media/active-directory-saas-sugarcrm-tutorial/ic795891.png "SAML Authentication")</span></span>  
 
    <span data-ttu-id="65ef4-177">a.</span><span class="sxs-lookup"><span data-stu-id="65ef4-177">a.</span></span> <span data-ttu-id="65ef4-178">Hello에 **로그인 URL** 붙여넣기 hello 값의 텍스트 상자 **SAML Single Sign-on 서비스 URL**, Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-178">In hello **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="65ef4-179">b.</span><span class="sxs-lookup"><span data-stu-id="65ef4-179">b.</span></span> <span data-ttu-id="65ef4-180">Hello에 **SLO URL** 붙여넣기 hello 값의 텍스트 상자 **Sign-Out URL**, Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-180">In hello **SLO URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="65ef4-181">c.</span><span class="sxs-lookup"><span data-stu-id="65ef4-181">c.</span></span> <span data-ttu-id="65ef4-182">E-64로 인코딩된 인증서 내용을 클립보드의 콘텐츠 복사 hello 메모장에서 열고 후 전체 인증서를 hello **X.509 인증서** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-182">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste hello entire Certificate into **X.509 Certificate** textbox.</span></span>
  
    <span data-ttu-id="65ef4-183">d.</span><span class="sxs-lookup"><span data-stu-id="65ef4-183">d.</span></span> <span data-ttu-id="65ef4-184">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-184">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="65ef4-185">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="65ef4-185">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="65ef4-186">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="65ef4-186">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="65ef4-187">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="65ef4-187">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="65ef4-188">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="65ef4-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="65ef4-189">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-189">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="65ef4-191">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="65ef4-191">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="65ef4-192">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-192">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="65ef4-194">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-194">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="65ef4-196">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-196">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="65ef4-198">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-198">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="65ef4-200">a.</span><span class="sxs-lookup"><span data-stu-id="65ef4-200">a.</span></span> <span data-ttu-id="65ef4-201">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-201">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="65ef4-202">b.</span><span class="sxs-lookup"><span data-stu-id="65ef4-202">b.</span></span> <span data-ttu-id="65ef4-203">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-203">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="65ef4-204">c.</span><span class="sxs-lookup"><span data-stu-id="65ef4-204">c.</span></span> <span data-ttu-id="65ef4-205">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-205">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="65ef4-206">d.</span><span class="sxs-lookup"><span data-stu-id="65ef4-206">d.</span></span> <span data-ttu-id="65ef4-207">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-207">Click **Create**.</span></span>
 
### <a name="creating-a-sugar-crm-test-user"></a><span data-ttu-id="65ef4-208">Sugar CRM 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="65ef4-208">Creating a Sugar CRM test user</span></span>

<span data-ttu-id="65ef4-209">Tooenable Azure AD 사용자가 toolog tooSugar CRM에에서 주문 하 고에 프로 비전 된 tooSugar CRM 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-209">In order tooenable Azure AD users toolog in tooSugar CRM, they must be provisioned tooSugar CRM.</span></span>

<span data-ttu-id="65ef4-210">Hello Sugar CRM의 경우에서 프로 비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-210">In hello case of Sugar CRM, provisioning is a manual task.</span></span>

<span data-ttu-id="65ef4-211">**tooprovision 사용자 계정을 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="65ef4-211">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="65ef4-212">Tooyour 로그인 **Sugar CRM** 회사 사이트에서 관리자 권한으로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-212">Log in tooyour **Sugar CRM** company site as administrator.</span></span>

2. <span data-ttu-id="65ef4-213">너무 이동**Admin**합니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-213">Go too**Admin**.</span></span>
   
    <span data-ttu-id="65ef4-214">![관리자](./media/active-directory-saas-sugarcrm-tutorial/ic795888.png "관리자")</span><span class="sxs-lookup"><span data-stu-id="65ef4-214">![Admin](./media/active-directory-saas-sugarcrm-tutorial/ic795888.png "Admin")</span></span>

3. <span data-ttu-id="65ef4-215">Hello에 **관리** 섹션에서 클릭 **사용자 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-215">In hello **Administration** section, click **User Management**.</span></span>
   
    <span data-ttu-id="65ef4-216">![관리](./media/active-directory-saas-sugarcrm-tutorial/ic795893.png "관리")</span><span class="sxs-lookup"><span data-stu-id="65ef4-216">![Administration](./media/active-directory-saas-sugarcrm-tutorial/ic795893.png "Administration")</span></span>

4. <span data-ttu-id="65ef4-217">너무 이동**사용자 \> 새 사용자 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-217">Go too**Users \> Create New User**.</span></span>
   
    <span data-ttu-id="65ef4-218">![새 사용자 만들기](./media/active-directory-saas-sugarcrm-tutorial/ic795894.png "새 사용자 만들기")</span><span class="sxs-lookup"><span data-stu-id="65ef4-218">![Create New User](./media/active-directory-saas-sugarcrm-tutorial/ic795894.png "Create New User")</span></span>

5. <span data-ttu-id="65ef4-219">Hello에 **사용자 프로필** 탭 hello 다음 단계를 수행 하십시오.</span><span class="sxs-lookup"><span data-stu-id="65ef4-219">On hello **User Profile** tab, perform hello following steps:</span></span>
   
    <span data-ttu-id="65ef4-220">![새 사용자](./media/active-directory-saas-sugarcrm-tutorial/ic795895.png "새 사용자")</span><span class="sxs-lookup"><span data-stu-id="65ef4-220">![New User](./media/active-directory-saas-sugarcrm-tutorial/ic795895.png "New User")</span></span>

    <span data-ttu-id="65ef4-221">a.</span><span class="sxs-lookup"><span data-stu-id="65ef4-221">a.</span></span> <span data-ttu-id="65ef4-222">형식 hello **사용자 이름**, **성**, 및 **전자 메일 주소** hello에 유효한 Azure Active Directory 사용자의 관련 텍스트 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-222">Type hello **user name**, **last name**, and **email address** of a valid Azure Active Directory user into hello related textboxes.</span></span>
  
6. <span data-ttu-id="65ef4-223">**상태**는 **활성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-223">As **Status**, select **Active**.</span></span>

7. <span data-ttu-id="65ef4-224">Hello 암호 탭에서 단계를 수행 하는 hello를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-224">On hello Password tab, perform hello following steps:</span></span>
   
    <span data-ttu-id="65ef4-225">![새 사용자](./media/active-directory-saas-sugarcrm-tutorial/ic795896.png "새 사용자")</span><span class="sxs-lookup"><span data-stu-id="65ef4-225">![New User](./media/active-directory-saas-sugarcrm-tutorial/ic795896.png "New User")</span></span>

    <span data-ttu-id="65ef4-226">a.</span><span class="sxs-lookup"><span data-stu-id="65ef4-226">a.</span></span> <span data-ttu-id="65ef4-227">Hello에 대 한 형식 hello 암호를 관련 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-227">Type hello password into hello related textbox.</span></span>

    <span data-ttu-id="65ef4-228">b.</span><span class="sxs-lookup"><span data-stu-id="65ef4-228">b.</span></span> <span data-ttu-id="65ef4-229">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-229">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="65ef4-230">다른 Sugar CRM 사용자 계정 만들기 도구를 사용할 수 있습니다 또는 AAD 사용자 계정을 tooprovision Sugar CRM에서 제공 된 Api입니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-230">You can use any other Sugar CRM user account creation tools or APIs provided by Sugar CRM tooprovision AAD user accounts.</span></span> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="65ef4-231">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-231">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="65ef4-232">이 섹션에서는 액세스 tooSugar CRM을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSugar CRM.</span></span>

![사용자 할당][200] 

<span data-ttu-id="65ef4-234">**tooassign Britta Simon tooSugar CRM, hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="65ef4-234">**tooassign Britta Simon tooSugar CRM, perform hello following steps:**</span></span>

1. <span data-ttu-id="65ef4-235">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-235">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="65ef4-237">Hello 응용 프로그램 목록에서 선택 **Sugar CRM**합니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-237">In hello applications list, select **Sugar CRM**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_app.png) 

3. <span data-ttu-id="65ef4-239">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-239">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="65ef4-241">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-241">Click **Add** button.</span></span> <span data-ttu-id="65ef4-242">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="65ef4-244">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-244">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="65ef4-245">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="65ef4-246">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="65ef4-247">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="65ef4-247">Testing single sign-on</span></span>

<span data-ttu-id="65ef4-248">이 섹션의 hello 목적은 tootest 액세스 패널을 hello 사용 하 여 Azure AD single sign-on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-248">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="65ef4-249">Hello 액세스 패널에서에서 hello Sugar CRM 타일을 클릭할 때 자동으로 로그온 tooyour Sugar CRM 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="65ef4-249">When you click hello Sugar CRM tile in hello Access Panel, you should get automatically signed-on tooyour Sugar CRM application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="65ef4-250">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="65ef4-250">Additional resources</span></span>

* [<span data-ttu-id="65ef4-251">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="65ef4-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="65ef4-252">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="65ef4-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_203.png

