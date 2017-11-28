---
title: "자습서: QuickHelp와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 QuickHelp 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 655c9ad3-2076-4e2c-8e47-9ed3bf04be56
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: jeedes
ms.openlocfilehash: bbde5eb9bdad89680923ccd36c321b6923f91789
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-quickhelp"></a><span data-ttu-id="2577d-103">자습서: QuickHelp와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="2577d-103">Tutorial: Azure Active Directory integration with QuickHelp</span></span>

<span data-ttu-id="2577d-104">이 자습서에 설명 어떻게 toointegrate QuickHelp Azure Active directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2577d-104">In this tutorial, you learn how toointegrate QuickHelp with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2577d-105">다음 이점을 hello로 제공 QuickHelp Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="2577d-105">Integrating QuickHelp with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2577d-106">액세스 tooQuickHelp을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2577d-106">You can control in Azure AD who has access tooQuickHelp</span></span>
- <span data-ttu-id="2577d-107">프로그램 사용자 tooautomatically get 로그온 tooQuickHelp (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2577d-107">You can enable your users tooautomatically get signed-on tooQuickHelp (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2577d-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2577d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="2577d-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2577d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2577d-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="2577d-110">Prerequisites</span></span>

<span data-ttu-id="2577d-111">다음 항목 hello가 필요 tooconfigure QuickHelp와 Azure AD 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="2577d-111">tooconfigure Azure AD integration with QuickHelp, you need hello following items:</span></span>

- <span data-ttu-id="2577d-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="2577d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2577d-113">QuickHelp Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="2577d-113">A QuickHelp single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2577d-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2577d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2577d-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2577d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2577d-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="2577d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2577d-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2577d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2577d-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="2577d-118">Scenario description</span></span>
<span data-ttu-id="2577d-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="2577d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2577d-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2577d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2577d-121">QuickHelp은 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="2577d-121">Adding QuickHelp from hello gallery</span></span>
2. <span data-ttu-id="2577d-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="2577d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-quickhelp-from-hello-gallery"></a><span data-ttu-id="2577d-123">QuickHelp은 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="2577d-123">Adding QuickHelp from hello gallery</span></span>
<span data-ttu-id="2577d-124">tooconfigure hello와의 통합 QuickHelp Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 QuickHelp tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2577d-124">tooconfigure hello integration of QuickHelp into Azure AD, you need tooadd QuickHelp from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2577d-125">**hello 갤러리에서 QuickHelp tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="2577d-125">**tooadd QuickHelp from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2577d-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="2577d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2577d-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="2577d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="2577d-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="2577d-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="2577d-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="2577d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="2577d-133">Hello 검색 상자에 입력 **QuickHelp**합니다.</span><span class="sxs-lookup"><span data-stu-id="2577d-133">In hello search box, type **QuickHelp**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_search.png)

5. <span data-ttu-id="2577d-135">Hello 결과 패널에서 선택 **QuickHelp**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="2577d-135">In hello results panel, select **QuickHelp**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2577d-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="2577d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2577d-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 QuickHelp에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="2577d-138">In this section, you configure and test Azure AD single sign-on with QuickHelp based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2577d-139">Single sign on toowork에 대 한 Azure AD는 tooknow QuickHelp에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2577d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in QuickHelp is tooa user in Azure AD.</span></span> <span data-ttu-id="2577d-140">즉, Azure AD 사용자 및 QuickHelp에 hello 관련된 사용자 간 링크 관계를 설정할 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2577d-140">In other words, a link relationship between an Azure AD user and hello related user in QuickHelp needs toobe established.</span></span>

<span data-ttu-id="2577d-141">QuickHelp에서 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="2577d-141">In QuickHelp, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="2577d-142">tooconfigure 및 QuickHelp 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2577d-142">tooconfigure and test Azure AD single sign-on with QuickHelp, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2577d-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="2577d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2577d-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2577d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2577d-145">**[QuickHelp 테스트 사용자 만들기](#creating-a-quickhelp-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 QuickHelp에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="2577d-145">**[Creating a QuickHelp test user](#creating-a-quickhelp-test-user)** - toohave a counterpart of Britta Simon in QuickHelp that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="2577d-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="2577d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2577d-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="2577d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2577d-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="2577d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2577d-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 QuickHelp 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2577d-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your QuickHelp application.</span></span>

<span data-ttu-id="2577d-150">**tooconfigure Azure AD single sign on, QuickHelp와 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="2577d-150">**tooconfigure Azure AD single sign-on with QuickHelp, perform hello following steps:**</span></span>

1. <span data-ttu-id="2577d-151">Hello hello에 Azure 포털에서에서 **QuickHelp** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="2577d-151">In hello Azure portal, on hello **QuickHelp** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="2577d-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="2577d-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_samlbase.png)

3. <span data-ttu-id="2577d-155">Hello에 **QuickHelp 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2577d-155">On hello **QuickHelp Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_url.png)

    <span data-ttu-id="2577d-157">a.</span><span class="sxs-lookup"><span data-stu-id="2577d-157">a.</span></span> <span data-ttu-id="2577d-158">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://quickhelp.com/<instancename>/#/Login`</span><span class="sxs-lookup"><span data-stu-id="2577d-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://quickhelp.com/<instancename>/#/Login`</span></span>

    <span data-ttu-id="2577d-159">b.</span><span class="sxs-lookup"><span data-stu-id="2577d-159">b.</span></span> <span data-ttu-id="2577d-160">Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<subdomain>.quickhelp.com`</span><span class="sxs-lookup"><span data-stu-id="2577d-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.quickhelp.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2577d-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="2577d-161">These values are not real.</span></span> <span data-ttu-id="2577d-162">이러한 항목을 업데이트 로그온 URL과 식별자 실제 hello로 값입니다.</span><span class="sxs-lookup"><span data-stu-id="2577d-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="2577d-163">연락처 [QuickHelp 클라이언트 지원 팀](https://support.quickhelp.com/) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="2577d-163">Contact [QuickHelp Client support team](https://support.quickhelp.com/) tooget these values.</span></span> 
 
4. <span data-ttu-id="2577d-164">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello 메타 데이터 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="2577d-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_certificate.png) 

5. <span data-ttu-id="2577d-166">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2577d-166">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-quickhelp-tutorial/tutorial_general_400.png) 

6. <span data-ttu-id="2577d-168">관리자 권한으로 로그온 tooyour QuickHelp 회사 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="2577d-168">Sign-on tooyour QuickHelp company site as administrator.</span></span>

7. <span data-ttu-id="2577d-169">Hello 메뉴에서 hello 위에 표시를 클릭 **Admin**합니다.</span><span class="sxs-lookup"><span data-stu-id="2577d-169">In hello menu on hello top, click **Admin**.</span></span>
   
    ![Single Sign-on 구성][21]

8. <span data-ttu-id="2577d-171">Hello에 **QuickHelp 관리자** 메뉴를 클릭 하 여 **설정을**합니다.</span><span class="sxs-lookup"><span data-stu-id="2577d-171">In hello **QuickHelp Admin** menu, click **Settings**.</span></span>
   
    ![Single Sign-on 구성][22]

9. <span data-ttu-id="2577d-173">**인증 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2577d-173">Click **Authentication Settings**.</span></span>

10. <span data-ttu-id="2577d-174">Hello에 **인증 설정** 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2577d-174">On hello **Authentication Settings** page, perform hello following steps</span></span>
   
    ![Single Sign-on 구성][23]
   
    <span data-ttu-id="2577d-176">a.</span><span class="sxs-lookup"><span data-stu-id="2577d-176">a.</span></span> <span data-ttu-id="2577d-177">**SSO 형식**으로 **WSFederation**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2577d-177">As **SSO Type**, select **WSFederation**.</span></span>
   
    <span data-ttu-id="2577d-178">b.</span><span class="sxs-lookup"><span data-stu-id="2577d-178">b.</span></span> <span data-ttu-id="2577d-179">tooupload Azure 다운로드 한 메타 데이터 파일을 클릭 하 여 **찾아보기**, toohello 파일을 이동, 클릭 한 다음 종료 **메타 데이터 업로드**합니다.</span><span class="sxs-lookup"><span data-stu-id="2577d-179">tooupload your downloaded Azure metadata file, click **Browse**, navigate toohello file, end then click **Upload Metadata**.</span></span>
   
    <span data-ttu-id="2577d-180">c.</span><span class="sxs-lookup"><span data-stu-id="2577d-180">c.</span></span> <span data-ttu-id="2577d-181">Hello에 **전자 메일** 텍스트 상자에 `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`합니다.</span><span class="sxs-lookup"><span data-stu-id="2577d-181">In hello **Email** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>
   
    <span data-ttu-id="2577d-182">d.</span><span class="sxs-lookup"><span data-stu-id="2577d-182">d.</span></span> <span data-ttu-id="2577d-183">Hello에 **이름** textbox `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`합니다.</span><span class="sxs-lookup"><span data-stu-id="2577d-183">In hello **First Name** textbox, `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span></span>
   
    <span data-ttu-id="2577d-184">e.</span><span class="sxs-lookup"><span data-stu-id="2577d-184">e.</span></span> <span data-ttu-id="2577d-185">Hello에 **성** textbox `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`합니다.</span><span class="sxs-lookup"><span data-stu-id="2577d-185">In hello **Last Name** textbox, `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span></span>
   
    <span data-ttu-id="2577d-186">f.</span><span class="sxs-lookup"><span data-stu-id="2577d-186">f.</span></span> <span data-ttu-id="2577d-187">Hello에 **작업 모음**, 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="2577d-187">In hello **Action Bar**, click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="2577d-188">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="2577d-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="2577d-189">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="2577d-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="2577d-190">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2577d-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2577d-191">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="2577d-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="2577d-192">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="2577d-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="2577d-194">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="2577d-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2577d-195">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="2577d-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-quickhelp-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2577d-197">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="2577d-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-quickhelp-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2577d-199">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="2577d-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-quickhelp-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2577d-201">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2577d-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-quickhelp-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2577d-203">a.</span><span class="sxs-lookup"><span data-stu-id="2577d-203">a.</span></span> <span data-ttu-id="2577d-204">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="2577d-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2577d-205">b.</span><span class="sxs-lookup"><span data-stu-id="2577d-205">b.</span></span> <span data-ttu-id="2577d-206">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="2577d-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2577d-207">c.</span><span class="sxs-lookup"><span data-stu-id="2577d-207">c.</span></span> <span data-ttu-id="2577d-208">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="2577d-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="2577d-209">d.</span><span class="sxs-lookup"><span data-stu-id="2577d-209">d.</span></span> <span data-ttu-id="2577d-210">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2577d-210">Click **Create**.</span></span>
 
### <a name="creating-a-quickhelp-test-user"></a><span data-ttu-id="2577d-211">QuickHelp 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="2577d-211">Creating a QuickHelp test user</span></span>

<span data-ttu-id="2577d-212">hello이이 섹션의 목적은 toocreate Britta Simon QuickHelp에서 호출 하는 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="2577d-212">hello objective of this section is toocreate a user called Britta Simon in QuickHelp.</span></span>
<span data-ttu-id="2577d-213">Single sign on toowork에 대 한 Azure AD는 tooknow QuickHelp tooa 사용자 Azure ad에서에서 어떤 hello 테이블에 해당 사용자가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2577d-213">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in QuickHelp tooa user in Azure AD is.</span></span> <span data-ttu-id="2577d-214">즉, Azure AD 사용자 및 QuickHelp에 hello 관련된 사용자 간 링크 관계를 설정할 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2577d-214">In other words, a link relationship between an Azure AD user and hello related user in QuickHelp needs toobe established.</span></span>

<span data-ttu-id="2577d-215">QuickHelp는 Just-In-Time 프로비전을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="2577d-215">QuickHelp supports just-in-time provisioning.</span></span> <span data-ttu-id="2577d-216">즉, 필요한 경우 QuickHelp에 사용자 계정을 자동으로 만들어집니다 및 hello 계정은 연결 된 Azure AD 계정을 toohello입니다.</span><span class="sxs-lookup"><span data-stu-id="2577d-216">This means, if necessary, a user account is automatically created in QuickHelp and hello account is linked toohello Azure AD account.</span></span>

<span data-ttu-id="2577d-217">이 섹션에 작업 항목이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2577d-217">There is no action item for you in this section.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="2577d-218">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="2577d-218">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="2577d-219">이 섹션에서는 tooQuickHelp 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2577d-219">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooQuickHelp.</span></span>

![사용자 할당][200] 

<span data-ttu-id="2577d-221">**tooassign Britta Simon tooQuickHelp hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="2577d-221">**tooassign Britta Simon tooQuickHelp, perform hello following steps:**</span></span>

1. <span data-ttu-id="2577d-222">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="2577d-222">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="2577d-224">Hello 응용 프로그램 목록에서 선택 **QuickHelp**합니다.</span><span class="sxs-lookup"><span data-stu-id="2577d-224">In hello applications list, select **QuickHelp**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_app.png) 

3. <span data-ttu-id="2577d-226">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="2577d-226">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="2577d-228">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2577d-228">Click **Add** button.</span></span> <span data-ttu-id="2577d-229">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2577d-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="2577d-231">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2577d-231">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="2577d-232">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2577d-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2577d-233">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2577d-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2577d-234">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="2577d-234">Testing single sign-on</span></span>

<span data-ttu-id="2577d-235">이 섹션의 hello 목적은 tootest 액세스 패널을 hello 사용 하 여 Azure AD single sign-on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2577d-235">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  

<span data-ttu-id="2577d-236">Hello 액세스 패널에서에서 hello QuickHelp 타일을 클릭할 때 자동으로 로그온 tooyour QuickHelp 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2577d-236">When you click hello QuickHelp tile in hello Access Panel, you should get automatically signed-on tooyour QuickHelp application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="2577d-237">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="2577d-237">Additional resources</span></span>

* [<span data-ttu-id="2577d-238">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="2577d-238">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2577d-239">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="2577d-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_203.png
[21]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_05.png
[22]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_06.png
[23]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_07.png
