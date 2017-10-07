---
title: "자습서: Mimecast Personal Portal과 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Mimecast Personal Portal 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 345b22be-d87e-45a4-b4c0-70a67eaf9bfd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: ee2a8edcab36f295732ac1ebe641ed7fcfc1f2a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mimecast-personal-portal"></a><span data-ttu-id="1a21f-103">자습서: Mimecast Personal Portal과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="1a21f-103">Tutorial: Azure Active Directory integration with Mimecast Personal Portal</span></span>

<span data-ttu-id="1a21f-104">이 자습서에 설명 어떻게 toointegrate Azure Active Directory (Azure AD)와 Mimecast Personal Portal입니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-104">In this tutorial, you learn how toointegrate Mimecast Personal Portal with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1a21f-105">Azure AD와 Mimecast Personal Portal 통합 이점을 다음 hello로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-105">Integrating Mimecast Personal Portal with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1a21f-106">액세스 tooMimecast Personal Portal을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-106">You can control in Azure AD who has access tooMimecast Personal Portal</span></span>
- <span data-ttu-id="1a21f-107">Azure AD 계정을 사용 하면 사용자가 tooautomatically get 로그온 tooMimecast Personal Portal (Single Sign-on)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-107">You can enable your users tooautomatically get signed-on tooMimecast Personal Portal (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1a21f-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="1a21f-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1a21f-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="1a21f-110">Prerequisites</span></span>

<span data-ttu-id="1a21f-111">Mimecast Personal Portal와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-111">tooconfigure Azure AD integration with Mimecast Personal Portal, you need hello following items:</span></span>

- <span data-ttu-id="1a21f-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="1a21f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1a21f-113">Mimecast Personal Portal에서 Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="1a21f-113">A Mimecast Personal Portal single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1a21f-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1a21f-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1a21f-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="1a21f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1a21f-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1a21f-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="1a21f-118">Scenario description</span></span>
<span data-ttu-id="1a21f-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1a21f-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1a21f-121">Mimecast Personal Portal hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="1a21f-121">Adding Mimecast Personal Portal from hello gallery</span></span>
2. <span data-ttu-id="1a21f-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="1a21f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mimecast-personal-portal-from-hello-gallery"></a><span data-ttu-id="1a21f-123">Mimecast Personal Portal hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="1a21f-123">Adding Mimecast Personal Portal from hello gallery</span></span>
<span data-ttu-id="1a21f-124">tooconfigure hello와의 통합 Mimecast Personal Portal Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Mimecast Personal Portal tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-124">tooconfigure hello integration of Mimecast Personal Portal into Azure AD, you need tooadd Mimecast Personal Portal from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1a21f-125">**Mimecast Personal Portal hello 갤러리에서 tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="1a21f-125">**tooadd Mimecast Personal Portal from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1a21f-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1a21f-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1a21f-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="1a21f-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="1a21f-133">Hello 검색 상자에 입력 **Mimecast Personal Portal**합니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-133">In hello search box, type **Mimecast Personal Portal**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_search.png)

5. <span data-ttu-id="1a21f-135">Hello 결과 패널에서 선택 **Mimecast Personal Portal**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-135">In hello results panel, select **Mimecast Personal Portal**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1a21f-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="1a21f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1a21f-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Mimecast Personal Portal에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-138">In this section, you configure and test Azure AD single sign-on with Mimecast Personal Portal based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1a21f-139">Single sign on toowork에 대 한 Azure AD는 tooknow Mimecast Personal Portal에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Mimecast Personal Portal is tooa user in Azure AD.</span></span> <span data-ttu-id="1a21f-140">즉, Azure AD 사용자와 Mimecast Personal Portal에 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-140">In other words, a link relationship between an Azure AD user and hello related user in Mimecast Personal Portal needs toobe established.</span></span>

<span data-ttu-id="1a21f-141">Mimecast Personal Portal에 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-141">In Mimecast Personal Portal, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="1a21f-142">tooconfigure와 Mimecast Personal Portal을 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-142">tooconfigure and test Azure AD single sign-on with Mimecast Personal Portal, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1a21f-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1a21f-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1a21f-145">**[Mimecast Personal Portal 테스트 사용자 만들기](#creating-a-mimecast-personal-portal-test-user)**  -toohave Britta Simon 표현인 연결 된 toohello Azure AD 사용자는 Mimecast Personal Portal에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-145">**[Creating a Mimecast Personal Portal test user](#creating-a-mimecast-personal-portal-test-user)** - toohave a counterpart of Britta Simon in Mimecast Personal Portal that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="1a21f-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1a21f-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="1a21f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1a21f-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="1a21f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1a21f-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 Mimecast Personal Portal 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Mimecast Personal Portal application.</span></span>

<span data-ttu-id="1a21f-150">**Mimecast Personal Portal와 Azure AD에서 single sign-on tooconfigure hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="1a21f-150">**tooconfigure Azure AD single sign-on with Mimecast Personal Portal, perform hello following steps:**</span></span>

1. <span data-ttu-id="1a21f-151">Hello hello에 Azure 포털에서에서 **Mimecast Personal Portal** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-151">In hello Azure portal, on hello **Mimecast Personal Portal** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="1a21f-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_samlbase.png)

3. <span data-ttu-id="1a21f-155">Hello에 **Mimecast 개인 포털 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-155">On hello **Mimecast Personal Portal Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_url.png)

    <span data-ttu-id="1a21f-157">a.</span><span class="sxs-lookup"><span data-stu-id="1a21f-157">a.</span></span> <span data-ttu-id="1a21f-158">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:</span><span class="sxs-lookup"><span data-stu-id="1a21f-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span> 
    | |     
    | ----------------------------------------|
    | `https://webmail-uk.mimecast.com`|
    | `https://webmail-us.mimecast.com`|
    | |
   
    <span data-ttu-id="1a21f-159">b.</span><span class="sxs-lookup"><span data-stu-id="1a21f-159">b.</span></span> <span data-ttu-id="1a21f-160">Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:</span><span class="sxs-lookup"><span data-stu-id="1a21f-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>

    | |     
    | --- |
    | `https://webmail-us.mimecast.com/sso/<companyname>`|
    | `https://webmail-uk.mimecast.com/sso/<companyname>`|    
    | `https://webmail-za.mimecast.com/sso/<companyname>`|
    | `https://webmail.mimecast-offshore.com/sso/<companyname>`|
    ||                                                 
    
    > [!NOTE] 
    > <span data-ttu-id="1a21f-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-161">These values are not real.</span></span> <span data-ttu-id="1a21f-162">이러한 항목을 업데이트 로그온 URL과 식별자 실제 hello로 값입니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="1a21f-163">연락처 [Mimecast 개인 포털 클라이언트 지원 팀](https://www.mimecast.com/customer-success/technical-support/) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-163">Contact [Mimecast Personal Portal Client support team](https://www.mimecast.com/customer-success/technical-support/) tooget these values.</span></span> 
 


4. <span data-ttu-id="1a21f-164">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **Certificate(Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_certificate.png) 

5. <span data-ttu-id="1a21f-166">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-166">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1a21f-168">Hello에 **Mimecast 개인 포털 구성** 섹션에서 클릭 **구성 Mimecast Personal Portal** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="1a21f-168">On hello **Mimecast Personal Portal Configuration** section, click **Configure Mimecast Personal Portal** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="1a21f-169">복사 hello **Sign-Out URL, SAML 엔터티 ID, 및 SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="1a21f-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_configure.png) 

7. <span data-ttu-id="1a21f-171">다른 웹 브라우저 창에서 Mimecast Personal Portal 포털에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-171">In a different web browser window, log into your Mimecast Personal Portal as an administrator.</span></span>

8. <span data-ttu-id="1a21f-172">너무 이동**서비스 \> 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-172">Go too**Services \> Applications**.</span></span>
   
    <span data-ttu-id="1a21f-173">![응용 프로그램](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794998.png "응용 프로그램")</span><span class="sxs-lookup"><span data-stu-id="1a21f-173">![Applications](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794998.png "Applications")</span></span>

9. <span data-ttu-id="1a21f-174">**인증 프로필**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-174">Click **Authentication Profiles**.</span></span>
   
    <span data-ttu-id="1a21f-175">![인증 프로필](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794999.png "인증 프로필")</span><span class="sxs-lookup"><span data-stu-id="1a21f-175">![Authentication Profiles](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794999.png "Authentication Profiles")</span></span>

10. <span data-ttu-id="1a21f-176">**새 인증 프로필**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-176">Click **New Authentication Profile**.</span></span>
   
    <span data-ttu-id="1a21f-177">![새 인증 프로필](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795000.png "새 인증 프로필")</span><span class="sxs-lookup"><span data-stu-id="1a21f-177">![New Authentication Profile](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795000.png "New Authentication Profile")</span></span>

11. <span data-ttu-id="1a21f-178">Hello에 **인증 프로필** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-178">In hello **Authentication Profile** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="1a21f-179">![인증 프로필](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795001.png "인증 프로필")</span><span class="sxs-lookup"><span data-stu-id="1a21f-179">![Authentication Profile](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795001.png "Authentication Profile")</span></span>
   
    <span data-ttu-id="1a21f-180">a.</span><span class="sxs-lookup"><span data-stu-id="1a21f-180">a.</span></span> <span data-ttu-id="1a21f-181">Hello에 **설명** 텍스트 상자, 구성에 대 한 이름 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-181">In hello **Description** textbox, type a name for your configuration.</span></span>
   
    <span data-ttu-id="1a21f-182">b.</span><span class="sxs-lookup"><span data-stu-id="1a21f-182">b.</span></span> <span data-ttu-id="1a21f-183">**Mimecast Personal Portal에 대한 SAML 인증 적용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-183">Select **Enforce SAML Authentication for Mimecast Personal Portal**.</span></span>
   
    <span data-ttu-id="1a21f-184">c.</span><span class="sxs-lookup"><span data-stu-id="1a21f-184">c.</span></span> <span data-ttu-id="1a21f-185">**공급자**로 **Azure Active Directory**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-185">As **Provider**, select **Azure Active Directory**.</span></span>
   
    <span data-ttu-id="1a21f-186">d.</span><span class="sxs-lookup"><span data-stu-id="1a21f-186">d.</span></span> <span data-ttu-id="1a21f-187">**발급자 URL** 붙여넣기 hello 값의 텍스트 상자 **SAML 엔터티 ID** Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-187">In **Issuer URL** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="1a21f-188">e.</span><span class="sxs-lookup"><span data-stu-id="1a21f-188">e.</span></span> <span data-ttu-id="1a21f-189">**로그인 URL** 붙여넣기 hello 값의 텍스트 상자 **SAML Single Sign-on 서비스 URL** Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-189">In **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="1a21f-190">f.</span><span class="sxs-lookup"><span data-stu-id="1a21f-190">f.</span></span> <span data-ttu-id="1a21f-191">**로그 아웃 URL** 붙여넣기 hello 값의 텍스트 상자 **Sign-Out URL** Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-191">In **Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="1a21f-192">g.</span><span class="sxs-lookup"><span data-stu-id="1a21f-192">g.</span></span> <span data-ttu-id="1a21f-193">Open 프로그램 **base64** 로 인코딩된 인증서 내용을 클립보드의 콘텐츠 복사 hello Azure 포털에서 다운로드 한 메모장에 복사한 후 toohello **Id 공급자 인증서 (메타 데이터)** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-193">Open your **base-64** encoded certificate in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **Identity Provider Certificate (Metadata)** textbox.</span></span>

    <span data-ttu-id="1a21f-194">h.</span><span class="sxs-lookup"><span data-stu-id="1a21f-194">h.</span></span> <span data-ttu-id="1a21f-195">**Single Sign-On 허용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-195">Select **Allow Single Sign On**.</span></span>
   
    <span data-ttu-id="1a21f-196">i.</span><span class="sxs-lookup"><span data-stu-id="1a21f-196">i.</span></span> <span data-ttu-id="1a21f-197">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-197">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="1a21f-198">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="1a21f-198">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="1a21f-199">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="1a21f-199">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="1a21f-200">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1a21f-200">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1a21f-201">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="1a21f-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="1a21f-202">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-202">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="1a21f-204">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="1a21f-204">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1a21f-205">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-205">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1a21f-207">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-207">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1a21f-209">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-209">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1a21f-211">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-211">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1a21f-213">a.</span><span class="sxs-lookup"><span data-stu-id="1a21f-213">a.</span></span> <span data-ttu-id="1a21f-214">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-214">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1a21f-215">b.</span><span class="sxs-lookup"><span data-stu-id="1a21f-215">b.</span></span> <span data-ttu-id="1a21f-216">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-216">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1a21f-217">c.</span><span class="sxs-lookup"><span data-stu-id="1a21f-217">c.</span></span> <span data-ttu-id="1a21f-218">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-218">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="1a21f-219">d.</span><span class="sxs-lookup"><span data-stu-id="1a21f-219">d.</span></span> <span data-ttu-id="1a21f-220">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-220">Click **Create**.</span></span>
 
### <a name="creating-a-mimecast-personal-portal-test-user"></a><span data-ttu-id="1a21f-221">Mimecast Personal Portal 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="1a21f-221">Creating a Mimecast Personal Portal test user</span></span>

<span data-ttu-id="1a21f-222">Tooenable Azure AD 사용자가 toolog Mimecast Personal Portal에 주문 하 고에 Mimecast Personal Portal에 이들 프로 비전 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-222">In order tooenable Azure AD users toolog into Mimecast Personal Portal, they must be provisioned into Mimecast Personal Portal.</span></span> <span data-ttu-id="1a21f-223">Hello Mimecast Personal Portal의 경우에서 프로 비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-223">In hello case of Mimecast Personal Portal, provisioning is a manual task.</span></span>

<span data-ttu-id="1a21f-224">있어야만 tooregister 도메인 사용자를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-224">You need tooregister a domain before you can create users.</span></span>

<span data-ttu-id="1a21f-225">**tooconfigure 사용자 프로비저닝, hello 다음 단계를 수행:**</span><span class="sxs-lookup"><span data-stu-id="1a21f-225">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="1a21f-226">Tooyour 로그온 **Mimecast Personal Portal** 관리자 권한으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-226">Sign on tooyour **Mimecast Personal Portal** as administrator.</span></span>

2. <span data-ttu-id="1a21f-227">너무 이동**디렉터리 \> 내부**합니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-227">Go too**Directories \> Internal**.</span></span>
   
    <span data-ttu-id="1a21f-228">![디렉터리](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795003.png "디렉터리")</span><span class="sxs-lookup"><span data-stu-id="1a21f-228">![Directories](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795003.png "Directories")</span></span>

3. <span data-ttu-id="1a21f-229">**새 도메인에 등록**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-229">Click **Register New Domain**.</span></span>
   
    <span data-ttu-id="1a21f-230">![새 도메인에 등록](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795004.png "새 도메인에 등록")</span><span class="sxs-lookup"><span data-stu-id="1a21f-230">![Register New Domain](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795004.png "Register New Domain")</span></span>

4. <span data-ttu-id="1a21f-231">새 도메인을 만든 후 **새 주소**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-231">After your new domain has been created, click **New Address**.</span></span>
   
    <span data-ttu-id="1a21f-232">![새 주소](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795005.png "새 주소")</span><span class="sxs-lookup"><span data-stu-id="1a21f-232">![New Address](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795005.png "New Address")</span></span>

5. <span data-ttu-id="1a21f-233">Hello 새 주소 대화 상자에서 다음 단계 유효한 Azure의 hello 수행 tooprovision 원하는 AD 계정:</span><span class="sxs-lookup"><span data-stu-id="1a21f-233">In hello new address dialog, perform hello following steps of a valid Azure AD account you want tooprovision:</span></span>
   
    <span data-ttu-id="1a21f-234">![저장](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795006.png "저장")</span><span class="sxs-lookup"><span data-stu-id="1a21f-234">![Save](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795006.png "Save")</span></span>
   
    <span data-ttu-id="1a21f-235">a.</span><span class="sxs-lookup"><span data-stu-id="1a21f-235">a.</span></span> <span data-ttu-id="1a21f-236">Hello에 **전자 메일 주소** 텍스트 상자에 **전자 메일 주소** hello 사용자에 게의  **BrittaSimon@contoso.com** 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-236">In hello **Email Address** textbox, type **Email Address** of hello user as **BrittaSimon@contoso.com**.</span></span>
    
    <span data-ttu-id="1a21f-237">b.</span><span class="sxs-lookup"><span data-stu-id="1a21f-237">b.</span></span> <span data-ttu-id="1a21f-238">Hello에 **전역 이름** 텍스트 형식 hello **username** 으로 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-238">In hello **Global Name** textbox, type hello **username** as **BrittaSimon**.</span></span>

    <span data-ttu-id="1a21f-239">c.</span><span class="sxs-lookup"><span data-stu-id="1a21f-239">c.</span></span> <span data-ttu-id="1a21f-240">Hello에 **암호**, 및 **암호 확인** 텍스트 상자, 형식 hello **암호** hello 사용자의 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-240">In hello **Password**, and **Confirm Password** textboxes, type hello **Password** of hello user.</span></span>
   
    <span data-ttu-id="1a21f-241">b.</span><span class="sxs-lookup"><span data-stu-id="1a21f-241">b.</span></span> <span data-ttu-id="1a21f-242">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-242">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="1a21f-243">다른 Mimecast Personal Portal 사용자 계정 만들기 도구 또는 Mimecast Personal Portal tooprovision Azure AD 사용자 계정에서 제공 된 Api를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-243">You can use any other Mimecast Personal Portal user account creation tools or APIs provided by Mimecast Personal Portal tooprovision Azure AD user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="1a21f-244">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-244">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="1a21f-245">이 섹션에서는 액세스 tooMimecast Personal Portal을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-245">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMimecast Personal Portal.</span></span>

![사용자 할당][200] 

<span data-ttu-id="1a21f-247">**tooassign Britta Simon tooMimecast Personal Portal hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="1a21f-247">**tooassign Britta Simon tooMimecast Personal Portal, perform hello following steps:**</span></span>

1. <span data-ttu-id="1a21f-248">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-248">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="1a21f-250">Hello 응용 프로그램 목록에서 선택 **Mimecast Personal Portal**합니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-250">In hello applications list, select **Mimecast Personal Portal**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_app.png) 

3. <span data-ttu-id="1a21f-252">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-252">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="1a21f-254">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-254">Click **Add** button.</span></span> <span data-ttu-id="1a21f-255">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-255">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="1a21f-257">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-257">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1a21f-258">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-258">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1a21f-259">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-259">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1a21f-260">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="1a21f-260">Testing single sign-on</span></span>
<span data-ttu-id="1a21f-261">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-261">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="1a21f-262">Hello 액세스 패널에서에서 hello Mimecast Personal Portal 타일을 클릭할 때 자동으로 로그온 tooyour Mimecast Personal Portal 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-262">When you click hello Mimecast Personal Portal tile in hello Access Panel, you should get automatically signed-on tooyour Mimecast Personal Portal application.</span></span> <span data-ttu-id="1a21f-263">액세스 패널 hello에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1a21f-263">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1a21f-264">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="1a21f-264">Additional resources</span></span>

* [<span data-ttu-id="1a21f-265">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="1a21f-265">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1a21f-266">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="1a21f-266">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_203.png

