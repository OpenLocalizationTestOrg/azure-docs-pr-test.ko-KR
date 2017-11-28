---
title: "자습서: TOPdesk - Public과 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 TOPdesk-Public 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0873299f-ce70-457b-addc-e57c5801275f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: ef0dd06157ecc3b33814590039f5cbae64e8c916
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-topdesk---public"></a><span data-ttu-id="27191-103">자습서: TOPdesk - Public과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="27191-103">Tutorial: Azure Active Directory integration with TOPdesk - Public</span></span>

<span data-ttu-id="27191-104">이 자습서에 설명 어떻게 toointegrate TOPdesk-Public이 Azure Active directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="27191-104">In this tutorial, you learn how toointegrate TOPdesk - Public with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="27191-105">TOPdesk-Public Azure AD와 통합 hello 다음 이점을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="27191-105">Integrating TOPdesk - Public with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="27191-106">공용 액세스 tooTOPdesk-에 있는 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27191-106">You can control in Azure AD who has access tooTOPdesk - Public.</span></span>
- <span data-ttu-id="27191-107">에 사용자가 tooautomatically get 로그온 tooTOPdesk-Public (Single Sign-on)는 Azure AD 계정 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27191-107">You can enable your users tooautomatically get signed-on tooTOPdesk - Public (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="27191-108">하나의 중앙 위치-hello Azure 포털에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27191-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="27191-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="27191-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="27191-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="27191-110">Prerequisites</span></span>

<span data-ttu-id="27191-111">tooconfigure Azure AD 통합와 TOPdesk-Public hello 다음 항목을 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="27191-111">tooconfigure Azure AD integration with TOPdesk - Public, you need hello following items:</span></span>

- <span data-ttu-id="27191-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="27191-112">An Azure AD subscription</span></span>
- <span data-ttu-id="27191-113">TOPdesk - Public Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="27191-113">A TOPdesk - Public single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="27191-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="27191-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="27191-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27191-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="27191-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="27191-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="27191-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27191-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="27191-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="27191-118">Scenario description</span></span>
<span data-ttu-id="27191-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="27191-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="27191-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27191-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="27191-121">TOPdesk-Public hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="27191-121">Adding TOPdesk - Public from hello gallery</span></span>
2. <span data-ttu-id="27191-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="27191-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-topdesk---public-from-hello-gallery"></a><span data-ttu-id="27191-123">TOPdesk-Public hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="27191-123">Adding TOPdesk - Public from hello gallery</span></span>
<span data-ttu-id="27191-124">TOPdesk-Public에 Azure AD의 tooconfigure hello 통합 tooadd TOPdesk-Public이 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="27191-124">tooconfigure hello integration of TOPdesk - Public into Azure AD, you need tooadd TOPdesk - Public from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="27191-125">**tooadd TOPdesk-Public hello 갤러리에서 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="27191-125">**tooadd TOPdesk - Public from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="27191-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="27191-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![hello Azure Active Directory 단추][1]

2. <span data-ttu-id="27191-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="27191-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="27191-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="27191-129">Then go too**All applications**.</span></span>

    ![hello 엔터프라이즈 응용 프로그램 블레이드][2]
    
3. <span data-ttu-id="27191-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="27191-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![hello 새 응용 프로그램 단추][3]

4. <span data-ttu-id="27191-133">Hello 검색 상자에 입력 **TOPdesk-Public**선택, **TOPdesk-Public** 결과 패널에서 클릭 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="27191-133">In hello search box, type **TOPdesk - Public**, select **TOPdesk - Public** from result panel then click **Add** button tooadd hello application.</span></span>

    ![TOPdesk-Public hello 결과 목록에서](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="27191-135">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="27191-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="27191-136">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 하여 TOPdesk-Public에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="27191-136">In this section, you configure and test Azure AD single sign-on with TOPdesk - Public based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="27191-137">Single sign on toowork에 대 한 Azure AD tooknow TOPdesk에 hello 테이블에 해당 사용자는 필요-Azure AD의 공개가 tooa 사용자.</span><span class="sxs-lookup"><span data-stu-id="27191-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in TOPdesk - Public is tooa user in Azure AD.</span></span> <span data-ttu-id="27191-138">즉, Azure AD 사용자와 TOPdesk-에 hello 관련된 사용자 간 링크 관계를 공개 toobe 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27191-138">In other words, a link relationship between an Azure AD user and hello related user in TOPdesk - Public needs toobe established.</span></span>

<span data-ttu-id="27191-139">TOPdesk-Public, hello hello 값 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계.</span><span class="sxs-lookup"><span data-stu-id="27191-139">In TOPdesk - Public, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="27191-140">tooconfigure Azure AD single sign-on 테스트와 TOPdesk-Public toocomplete hello 빌딩 블록을 다음 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27191-140">tooconfigure and test Azure AD single sign-on with TOPdesk - Public, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="27191-141">**[Azure AD Single Sign-on 구성](#configure-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="27191-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="27191-142">**[Azure AD 테스트를 만들고](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="27191-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="27191-143">**[TOPdesk-Public 테스트 사용자 만들기](#create-a-topdesk---public-test-user)**  -toohave Britta Simon TOPdesk에 해당 하는 도구-사용자의 연결 된 Azure AD toohello 표현인 공개 합니다.</span><span class="sxs-lookup"><span data-stu-id="27191-143">**[Create a TOPdesk - Public test user](#create-a-topdesk---public-test-user)** - toohave a counterpart of Britta Simon in TOPdesk - Public that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="27191-144">**[Azure AD hello 테스트 사용자를 할당](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="27191-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="27191-145">**[Single sign on 테스트](#test-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="27191-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="27191-146">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="27191-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="27191-147">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 TOPdesk-Public 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="27191-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your TOPdesk - Public application.</span></span>

<span data-ttu-id="27191-148">**tooconfigure Azure AD에서 single sign-on와 TOPdesk-Public hello 다음 단계를 수행:**</span><span class="sxs-lookup"><span data-stu-id="27191-148">**tooconfigure Azure AD single sign-on with TOPdesk - Public, perform hello following steps:**</span></span>

1. <span data-ttu-id="27191-149">Hello hello에 Azure 포털에서에서 **TOPdesk-Public** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="27191-149">In hello Azure portal, on hello **TOPdesk - Public** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-On 구성 링크][4]

2. <span data-ttu-id="27191-151">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="27191-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_samlbase.png)

3. <span data-ttu-id="27191-153">Hello에 **TOPdesk-공용 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="27191-153">On hello **TOPdesk - Public Domain and URLs** section, perform hello following steps:</span></span>

    ![TOPdesk-Public 도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_url.png)

    <span data-ttu-id="27191-155">a.</span><span class="sxs-lookup"><span data-stu-id="27191-155">a.</span></span> <span data-ttu-id="27191-156">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<companyname>.topdesk.net`</span><span class="sxs-lookup"><span data-stu-id="27191-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.topdesk.net`</span></span>
    
    <span data-ttu-id="27191-157">b.</span><span class="sxs-lookup"><span data-stu-id="27191-157">b.</span></span> <span data-ttu-id="27191-158">Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<companyname>.topdesk.net/tas/public/login/verify`</span><span class="sxs-lookup"><span data-stu-id="27191-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.topdesk.net/tas/public/login/verify`</span></span>

    <span data-ttu-id="27191-159">c.</span><span class="sxs-lookup"><span data-stu-id="27191-159">c.</span></span> <span data-ttu-id="27191-160">Hello에 **회신 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<companyname>.topdesk.net/tas/public/login/saml`</span><span class="sxs-lookup"><span data-stu-id="27191-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyname>.topdesk.net/tas/public/login/saml`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="27191-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="27191-161">These values are not real.</span></span> <span data-ttu-id="27191-162">이러한 항목을 업데이트 식별자, 회신 URL 및 로그온 URL 실제 hello로 값입니다.</span><span class="sxs-lookup"><span data-stu-id="27191-162">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="27191-163">회신 URL은 자습서의 뒷부분에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="27191-163">Reply URL is explaned later in tutorial.</span></span> <span data-ttu-id="27191-164">연락처 [TOPdesk-Public 클라이언트 지원 팀](https://help.topdesk.com/saas/enterprise/user/) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="27191-164">Contact [TOPdesk - Public Client support team](https://help.topdesk.com/saas/enterprise/user/) tooget these values.</span></span>  

4. <span data-ttu-id="27191-165">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello 메타 데이터 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="27191-165">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![hello 인증서 다운로드 링크](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_certificate.png) 

5. <span data-ttu-id="27191-167">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="27191-167">Click **Save** button.</span></span>

    ![Single Sign-On 구성 저장 단추](./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="27191-169">Hello에 **TOPdesk-Public 구성** 섹션에서 클릭 **구성 TOPdesk-Public** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="27191-169">On hello **TOPdesk - Public Configuration** section, click **Configure TOPdesk - Public** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="27191-170">복사 hello **Sign-Out URL, SAML 엔터티 ID, 및 SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="27191-170">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![TOPdesk-Public 구성](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_configure.png) 

7. <span data-ttu-id="27191-172">Tooyour 로그온 **TOPdesk-Public** 회사 사이트에 관리자 권한으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="27191-172">Sign on tooyour **TOPdesk - Public** company site as an administrator.</span></span>

8. <span data-ttu-id="27191-173">Hello에 **TOPdesk** 메뉴를 클릭 하 여 **설정을**합니다.</span><span class="sxs-lookup"><span data-stu-id="27191-173">In hello **TOPdesk** menu, click **Settings**.</span></span>
   
    <span data-ttu-id="27191-174">![설정](./media/active-directory-saas-topdesk-public-tutorial/ic790598.png "설정")</span><span class="sxs-lookup"><span data-stu-id="27191-174">![Settings](./media/active-directory-saas-topdesk-public-tutorial/ic790598.png "Settings")</span></span>

9. <span data-ttu-id="27191-175">**로그인 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="27191-175">Click **Login Settings**.</span></span>
   
    <span data-ttu-id="27191-176">![로그인 설정](./media/active-directory-saas-topdesk-public-tutorial/ic790599.png "로그인 설정")</span><span class="sxs-lookup"><span data-stu-id="27191-176">![Login Settings](./media/active-directory-saas-topdesk-public-tutorial/ic790599.png "Login Settings")</span></span>

10. <span data-ttu-id="27191-177">Hello 확장 **로그인 설정** 메뉴를 차례로 클릭 **일반**합니다.</span><span class="sxs-lookup"><span data-stu-id="27191-177">Expand hello **Login Settings** menu, and then click **General**.</span></span>
   
    <span data-ttu-id="27191-178">![일반](./media/active-directory-saas-topdesk-public-tutorial/ic790600.png "일반")</span><span class="sxs-lookup"><span data-stu-id="27191-178">![General](./media/active-directory-saas-topdesk-public-tutorial/ic790600.png "General")</span></span>

11. <span data-ttu-id="27191-179">Hello에 **공용** hello의 섹션 **SAML 로그인** 구성 섹션에서 단계를 수행 하는 hello를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="27191-179">In hello **Public** section of hello **SAML login** configuration section, perform hello following steps:</span></span>
   
    <span data-ttu-id="27191-180">![기술 설정](./media/active-directory-saas-topdesk-public-tutorial/ic790601.png "기술 설정")</span><span class="sxs-lookup"><span data-stu-id="27191-180">![Technical Settings](./media/active-directory-saas-topdesk-public-tutorial/ic790601.png "Technical Settings")</span></span>
   
    <span data-ttu-id="27191-181">a.</span><span class="sxs-lookup"><span data-stu-id="27191-181">a.</span></span> <span data-ttu-id="27191-182">클릭 **다운로드** toodownload hello 공용 메타 데이터 파일을 한 다음 컴퓨터에 로컬로 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="27191-182">Click **Download** toodownload hello public metadata file, and then save it locally on your computer.</span></span>
   
    <span data-ttu-id="27191-183">b.</span><span class="sxs-lookup"><span data-stu-id="27191-183">b.</span></span> <span data-ttu-id="27191-184">Hello 다운로드 한 메타 데이터 파일을 열고 찾은 후 hello **AssertionConsumerService** 노드.</span><span class="sxs-lookup"><span data-stu-id="27191-184">Open hello downloaded metadata file, and then locate hello **AssertionConsumerService** node.</span></span>

    <span data-ttu-id="27191-185">![AssertionConsumerService](./media/active-directory-saas-topdesk-public-tutorial/ic790619.png "AssertionConsumerService")</span><span class="sxs-lookup"><span data-stu-id="27191-185">![AssertionConsumerService](./media/active-directory-saas-topdesk-public-tutorial/ic790619.png "AssertionConsumerService")</span></span>
   
    <span data-ttu-id="27191-186">c.</span><span class="sxs-lookup"><span data-stu-id="27191-186">c.</span></span> <span data-ttu-id="27191-187">복사 hello **AssertionConsumerService** hello에이 값을 붙여, 값 **회신 URL** 텍스트 상자로 **TOPdesk-공용 도메인 및 Url** 섹션.</span><span class="sxs-lookup"><span data-stu-id="27191-187">Copy hello **AssertionConsumerService** value, paste this value in hello **Reply URL** textbox in **TOPdesk - Public Domain and URLs** section.</span></span>      
   
12. <span data-ttu-id="27191-188">toocreate 인증서 파일을 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="27191-188">toocreate a certificate file, perform hello following steps:</span></span>
    
    <span data-ttu-id="27191-189">![인증서](./media/active-directory-saas-topdesk-public-tutorial/ic790606.png "인증서")</span><span class="sxs-lookup"><span data-stu-id="27191-189">![Certificate](./media/active-directory-saas-topdesk-public-tutorial/ic790606.png "Certificate")</span></span>
    
    <span data-ttu-id="27191-190">a.</span><span class="sxs-lookup"><span data-stu-id="27191-190">a.</span></span> <span data-ttu-id="27191-191">열기 hello Azure 포털에서 메타 데이터 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="27191-191">Open hello downloaded metadata file from Azure portal.</span></span>
    
    <span data-ttu-id="27191-192">b.</span><span class="sxs-lookup"><span data-stu-id="27191-192">b.</span></span> <span data-ttu-id="27191-193">Hello 확장 **RoleDescriptor** 노드에 **xsi: type** 의 **fed: ApplicationServiceType**합니다.</span><span class="sxs-lookup"><span data-stu-id="27191-193">Expand hello **RoleDescriptor** node that has a **xsi:type** of **fed:ApplicationServiceType**.</span></span>
    
    <span data-ttu-id="27191-194">c.</span><span class="sxs-lookup"><span data-stu-id="27191-194">c.</span></span> <span data-ttu-id="27191-195">Hello의 hello 값을 복사 **X509Certificate** 노드.</span><span class="sxs-lookup"><span data-stu-id="27191-195">Copy hello value of hello **X509Certificate** node.</span></span>
    
    <span data-ttu-id="27191-196">d.</span><span class="sxs-lookup"><span data-stu-id="27191-196">d.</span></span> <span data-ttu-id="27191-197">복사 저장 hello **X509Certificate** 파일에서 컴퓨터에 로컬로 값입니다.</span><span class="sxs-lookup"><span data-stu-id="27191-197">Save hello copied **X509Certificate** value locally on your computer in a file.</span></span>

13. <span data-ttu-id="27191-198">Hello에 **공용** 섹션에서 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="27191-198">In hello **Public** section, click **Add**.</span></span>
    
    <span data-ttu-id="27191-199">![SAML 로그인](./media/active-directory-saas-topdesk-public-tutorial/ic790625.png "SAML 로그인")</span><span class="sxs-lookup"><span data-stu-id="27191-199">![SAML Login](./media/active-directory-saas-topdesk-public-tutorial/ic790625.png "SAML Login")</span></span>

14. <span data-ttu-id="27191-200">Hello에 **SAML 구성 도우미** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="27191-200">On hello **SAML configuration assistant** dialog page, perform hello following steps:</span></span>
    
    <span data-ttu-id="27191-201">![SAML 구성 도우미](./media/active-directory-saas-topdesk-public-tutorial/ic790608.png "SAML 구성 도우미")</span><span class="sxs-lookup"><span data-stu-id="27191-201">![SAML Configuration Assistant](./media/active-directory-saas-topdesk-public-tutorial/ic790608.png "SAML Configuration Assistant")</span></span>
    
    <span data-ttu-id="27191-202">a.</span><span class="sxs-lookup"><span data-stu-id="27191-202">a.</span></span> <span data-ttu-id="27191-203">tooupload 다운로드 한 메타 데이터에서에서 파일을 Azure 포털에서 **페더레이션 메타 데이터**, 클릭 **찾아보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="27191-203">tooupload your downloaded metadata file from Azure portal, under **Federation Metadata**, click **Browse**.</span></span>

    <span data-ttu-id="27191-204">b.</span><span class="sxs-lookup"><span data-stu-id="27191-204">b.</span></span> <span data-ttu-id="27191-205">인증서 파일 tooupload **Certificate (RSA)**, 클릭 **찾아보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="27191-205">tooupload your certificate file, under **Certificate (RSA)**, click **Browse**.</span></span>

    <span data-ttu-id="27191-206">c.</span><span class="sxs-lookup"><span data-stu-id="27191-206">c.</span></span> <span data-ttu-id="27191-207">아래에서 hello TOPdesk 지원 팀에서 받은 tooupload hello 로고 파일 **로고 아이콘**, 클릭 **찾아보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="27191-207">tooupload hello logo file you got from hello TOPdesk support team, under **Logo icon**, click **Browse**.</span></span>

    <span data-ttu-id="27191-208">d.</span><span class="sxs-lookup"><span data-stu-id="27191-208">d.</span></span> <span data-ttu-id="27191-209">Hello에 **사용자 이름 특성** 텍스트 상자에 `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`합니다.</span><span class="sxs-lookup"><span data-stu-id="27191-209">In hello **User name attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>

    <span data-ttu-id="27191-210">e.</span><span class="sxs-lookup"><span data-stu-id="27191-210">e.</span></span> <span data-ttu-id="27191-211">Hello에 **표시 이름** 텍스트 상자, 구성에 대 한 이름 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="27191-211">In hello **Display name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="27191-212">f.</span><span class="sxs-lookup"><span data-stu-id="27191-212">f.</span></span> <span data-ttu-id="27191-213">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="27191-213">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="27191-214">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="27191-214">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="27191-215">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="27191-215">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="27191-216">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="27191-216">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="27191-217">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="27191-217">Create an Azure AD test user</span></span>

<span data-ttu-id="27191-218">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="27191-218">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Azure AD 테스트 사용자 만들기][100]

<span data-ttu-id="27191-220">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="27191-220">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="27191-221">Hello hello 왼쪽된 창에서 Azure 포털에서에서 클릭 hello **Azure Active Directory** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="27191-221">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![hello Azure Active Directory 단추](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="27191-223">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹**, 클릭 하 고 **모든 사용자가**합니다.</span><span class="sxs-lookup"><span data-stu-id="27191-223">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    !["사용자 및 그룹" hello 및 "모든 사용자" 링크](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="27191-225">tooopen hello **사용자** 대화 상자를 클릭 **추가** hello hello 맨 **모든 사용자에 게** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="27191-225">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![hello 추가 단추](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="27191-227">Hello에 **사용자** 대화 상자를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="27191-227">In hello **User** dialog box, perform hello following steps:</span></span>

    ![hello 사용자 대화 상자](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_04.png)

    <span data-ttu-id="27191-229">a.</span><span class="sxs-lookup"><span data-stu-id="27191-229">a.</span></span> <span data-ttu-id="27191-230">Hello에 **이름** 상자에서 입력 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="27191-230">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="27191-231">b.</span><span class="sxs-lookup"><span data-stu-id="27191-231">b.</span></span> <span data-ttu-id="27191-232">Hello에 **사용자 이름** 상자의 사용자 Britta Simon의 hello 전자 메일 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="27191-232">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="27191-233">c.</span><span class="sxs-lookup"><span data-stu-id="27191-233">c.</span></span> <span data-ttu-id="27191-234">선택 hello **암호 표시** 확인란을 선택한 다음 hello에 표시 되는 hello 값 기록 **암호** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="27191-234">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="27191-235">d.</span><span class="sxs-lookup"><span data-stu-id="27191-235">d.</span></span> <span data-ttu-id="27191-236">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="27191-236">Click **Create**.</span></span>
 
### <a name="create-a-topdesk---public-test-user"></a><span data-ttu-id="27191-237">TOPdesk-Public 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="27191-237">Create a TOPdesk - Public test user</span></span>

<span data-ttu-id="27191-238">TOPdesk-에 순서 tooenable Azure AD 사용자가 toolog에서 공용 TOPdesk-Public에 프로 비전 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27191-238">In order tooenable Azure AD users toolog into TOPdesk - Public, they must be provisioned into TOPdesk - Public.</span></span>  
<span data-ttu-id="27191-239">Hello 경우 TOPdesk-Public 프로 비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="27191-239">In hello case of TOPdesk - Public, provisioning is a manual task.</span></span>

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a><span data-ttu-id="27191-240">tooconfigure 사용자 프로비저닝, hello 다음 단계를 수행:</span><span class="sxs-lookup"><span data-stu-id="27191-240">tooconfigure user provisioning, perform hello following steps:</span></span>
1. <span data-ttu-id="27191-241">Tooyour 로그온 **TOPdesk-Public** 회사 사이트에서 관리자 권한으로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="27191-241">Sign on tooyour **TOPdesk - Public** company site as administrator.</span></span>

2. <span data-ttu-id="27191-242">Hello 메뉴에서 hello 위에 표시를 클릭 **TOPdesk \> 새로 \> 지원 파일 \> 사람**합니다.</span><span class="sxs-lookup"><span data-stu-id="27191-242">In hello menu on hello top, click **TOPdesk \> New \> Support Files \> Person**.</span></span>
   
    <span data-ttu-id="27191-243">![사람](./media/active-directory-saas-topdesk-public-tutorial/ic790628.png "사람")</span><span class="sxs-lookup"><span data-stu-id="27191-243">![Person](./media/active-directory-saas-topdesk-public-tutorial/ic790628.png "Person")</span></span>

3. <span data-ttu-id="27191-244">Hello New Person 대화 상자에서 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="27191-244">On hello New Person dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="27191-245">![새로운 사람](./media/active-directory-saas-topdesk-public-tutorial/ic790629.png "새로운 사람")</span><span class="sxs-lookup"><span data-stu-id="27191-245">![New Person](./media/active-directory-saas-topdesk-public-tutorial/ic790629.png "New Person")</span></span>
   
    <span data-ttu-id="27191-246">a.</span><span class="sxs-lookup"><span data-stu-id="27191-246">a.</span></span> <span data-ttu-id="27191-247">Hello 일반 탭을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="27191-247">Click hello General tab.</span></span>

    <span data-ttu-id="27191-248">b.</span><span class="sxs-lookup"><span data-stu-id="27191-248">b.</span></span> <span data-ttu-id="27191-249">Hello에 **Surname** textbox Simon 같은 hello 사용자의 성을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="27191-249">In hello **Surname** textbox, type Surname of hello user like Simon</span></span>
 
    <span data-ttu-id="27191-250">c.</span><span class="sxs-lookup"><span data-stu-id="27191-250">c.</span></span> <span data-ttu-id="27191-251">선택 된 **사이트** hello 계정에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="27191-251">Select a **Site** for hello account.</span></span>
 
    <span data-ttu-id="27191-252">d.</span><span class="sxs-lookup"><span data-stu-id="27191-252">d.</span></span> <span data-ttu-id="27191-253">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="27191-253">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="27191-254">다른 TOPdesk-Public 사용자 계정 만들기 도구 또는 TOPdesk-Public tooprovision Azure AD 사용자 계정에서 제공 된 Api를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27191-254">You can use any other TOPdesk - Public user account creation tools or APIs provided by TOPdesk - Public tooprovision Azure AD user accounts.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="27191-255">Azure AD hello 테스트 사용자를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="27191-255">Assign hello Azure AD test user</span></span>

<span data-ttu-id="27191-256">이 섹션에서는 액세스 tooTOPdesk-Public에 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="27191-256">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTOPdesk - Public.</span></span>

![Hello 사용자 역할 할당][200] 

<span data-ttu-id="27191-258">**tooassign Britta Simon tooTOPdesk-Public hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="27191-258">**tooassign Britta Simon tooTOPdesk - Public, perform hello following steps:**</span></span>

1. <span data-ttu-id="27191-259">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="27191-259">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="27191-261">Hello 응용 프로그램 목록에서 선택 **TOPdesk-Public**합니다.</span><span class="sxs-lookup"><span data-stu-id="27191-261">In hello applications list, select **TOPdesk - Public**.</span></span>

    ![hello TOPdesk-Public hello 응용 프로그램 목록에 연결](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_app.png)  

3. <span data-ttu-id="27191-263">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="27191-263">In hello menu on hello left, click **Users and groups**.</span></span>

    ![hello "사용자 및 그룹" 링크][202]

4. <span data-ttu-id="27191-265">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="27191-265">Click **Add** button.</span></span> <span data-ttu-id="27191-266">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="27191-266">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![hello 할당 추가 창][203]

5. <span data-ttu-id="27191-268">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27191-268">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="27191-269">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="27191-269">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="27191-270">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="27191-270">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="27191-271">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="27191-271">Test single sign-on</span></span>

<span data-ttu-id="27191-272">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27191-272">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="27191-273">TOPdesk-hello를 클릭할 때 공용 hello 액세스 패널에서에서 타일을 자동으로 로그온 tooyour TOPdesk-Public 응용 프로그램을 얻어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27191-273">When you click hello TOPdesk - Public tile in hello Access Panel, you should get automatically signed-on tooyour TOPdesk - Public application.</span></span>
<span data-ttu-id="27191-274">액세스 패널에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="27191-274">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="27191-275">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="27191-275">Additional resources</span></span>

* [<span data-ttu-id="27191-276">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="27191-276">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="27191-277">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="27191-277">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_203.png

