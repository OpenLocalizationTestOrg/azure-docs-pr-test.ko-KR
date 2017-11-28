---
title: "자습서: Dropbox for Business와 Azure Active Directory 통합 | Microsoft 문서"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Dropbox for Business 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 63502412-758b-4b46-a580-0e8e130791a1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: 3f33a43ca8fbd60486d7a400ae8246af768376ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-dropbox-for-business"></a><span data-ttu-id="24175-103">자습서: Dropbox for Business와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="24175-103">Tutorial: Azure Active Directory integration with Dropbox for Business</span></span>

<span data-ttu-id="24175-104">이 자습서에 설명 어떻게 toointegrate Dropbox for Business와 Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="24175-104">In this tutorial, you learn how toointegrate Dropbox for Business with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="24175-105">Azure AD와 Dropbox for Business 통합 hello 다음 이점을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="24175-105">Integrating Dropbox for Business with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="24175-106">비즈니스에 대 한 액세스 tooDropbox 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24175-106">You can control in Azure AD who has access tooDropbox for Business</span></span>
- <span data-ttu-id="24175-107">Azure AD 계정을 사용 하면 사용자가 tooautomatically get 로그온 tooDropbox (Single Sign-on)는 비즈니스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24175-107">You can enable your users tooautomatically get signed-on tooDropbox for Business (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="24175-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24175-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="24175-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="24175-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="24175-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="24175-110">Prerequisites</span></span>

<span data-ttu-id="24175-111">Dropbox for Business와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="24175-111">tooconfigure Azure AD integration with Dropbox for Business, you need hello following items:</span></span>

- <span data-ttu-id="24175-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="24175-112">An Azure AD subscription</span></span>
- <span data-ttu-id="24175-113">Dropbox for Business Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="24175-113">A Dropbox for Business single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="24175-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="24175-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="24175-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="24175-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="24175-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="24175-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="24175-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24175-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="24175-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="24175-118">Scenario description</span></span>
<span data-ttu-id="24175-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="24175-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="24175-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24175-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="24175-121">Dropbox for Business hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="24175-121">Adding Dropbox for Business from hello gallery</span></span>
2. <span data-ttu-id="24175-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="24175-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-dropbox-for-business-from-hello-gallery"></a><span data-ttu-id="24175-123">Dropbox for Business hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="24175-123">Adding Dropbox for Business from hello gallery</span></span>
<span data-ttu-id="24175-124">tooconfigure hello와의 통합 Dropbox for Business Azure AD로 tooadd Dropbox for Business에서에서 필요한 hello 갤러리 tooyour 관리 되는 SaaS 앱 목록을 합니다.</span><span class="sxs-lookup"><span data-stu-id="24175-124">tooconfigure hello integration of Dropbox for Business into Azure AD, you need tooadd Dropbox for Business from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="24175-125">**Dropbox for Business hello 갤러리에서 tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="24175-125">**tooadd Dropbox for Business from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="24175-126">Hello에 ** [Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="24175-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="24175-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="24175-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="24175-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="24175-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="24175-131">클릭 **새 응용 프로그램** hello 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="24175-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="24175-133">Hello 검색 상자에 입력 **Dropbox for Business**합니다.</span><span class="sxs-lookup"><span data-stu-id="24175-133">In hello search box, type **Dropbox for Business**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_search.png)

5. <span data-ttu-id="24175-135">Hello 결과 패널에서 선택 **Dropbox for Business**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="24175-135">In hello results panel, select **Dropbox for Business**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="24175-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="24175-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="24175-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Dropbox for Business에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="24175-138">In this section, you configure and test Azure AD single sign-on with Dropbox for Business based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="24175-139">Single sign on toowork에 대 한 Azure AD는 tooknow Dropbox for Business에서에서 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="24175-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Dropbox for Business is tooa user in Azure AD.</span></span> <span data-ttu-id="24175-140">즉, Azure AD 사용자와 Dropbox for Business의에서 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="24175-140">In other words, a link relationship between an Azure AD user and hello related user in Dropbox for Business needs toobe established.</span></span>

<span data-ttu-id="24175-141">Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** Dropbox for Business에서에서.</span><span class="sxs-lookup"><span data-stu-id="24175-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Dropbox for Business.</span></span>

<span data-ttu-id="24175-142">tooconfigure 및 비즈니스에 대 한 Dropbox와 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="24175-142">tooconfigure and test Azure AD single sign-on with Dropbox for Business, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="24175-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on) ** -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="24175-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="24175-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user) ** -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="24175-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="24175-145">**[Dropbox for Business 테스트 사용자 만들기](#creating-a-dropbox-for-business-test-user) ** -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 비지니스 용 Dropbox에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="24175-145">**[Creating a Dropbox for Business test user](#creating-a-dropbox-for-business-test-user)** - toohave a counterpart of Britta Simon in Dropbox for Business that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="24175-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="24175-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="24175-147">**[Single Sign-on 테스트](#testing-single-sign-on) ** -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="24175-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="24175-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="24175-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="24175-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 비즈니스 응용 프로그램에 대 한 Dropbox에 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="24175-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Dropbox for Business application.</span></span>

<span data-ttu-id="24175-150">**Azure AD tooconfigure single sign on와 Dropbox for Business hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="24175-150">**tooconfigure Azure AD single sign-on with Dropbox for Business, perform hello following steps:**</span></span>

1. <span data-ttu-id="24175-151">Hello hello에 Azure 포털에서에서 **Dropbox for Business** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="24175-151">In hello Azure portal, on hello **Dropbox for Business** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="24175-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="24175-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_samlbase.png)

3. <span data-ttu-id="24175-155">Hello에 **비즈니스 도메인 및 Url에 대 한 Dropbox** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="24175-155">On hello **Dropbox for Business Domain and URLs** section, perform hello following steps:</span></span>

    <span data-ttu-id="24175-156">a.</span><span class="sxs-lookup"><span data-stu-id="24175-156">a.</span></span> <span data-ttu-id="24175-157">Dropbox for business 테 넌 tooyour 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="24175-157">Sign on tooyour Dropbox for business tenant.</span></span> 
   
    <span data-ttu-id="24175-158">![Single Sign-On 구성](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769509.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="24175-158">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769509.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="24175-159">b.</span><span class="sxs-lookup"><span data-stu-id="24175-159">b.</span></span> <span data-ttu-id="24175-160">Hello 왼쪽에 hello 탐색 창에서 클릭 **관리 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="24175-160">In hello navigation pane on hello left side, click **Admin Console**.</span></span> 
   
    <span data-ttu-id="24175-161">![Single Sign-On 구성](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769510.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="24175-161">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769510.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="24175-162">c.</span><span class="sxs-lookup"><span data-stu-id="24175-162">c.</span></span> <span data-ttu-id="24175-163">Hello에 **관리 콘솔**, 클릭 **인증** hello 왼쪽된 탐색 창에서.</span><span class="sxs-lookup"><span data-stu-id="24175-163">On hello **Admin Console**, click **Authentication** in hello left navigation pane.</span></span> 
   
    <span data-ttu-id="24175-164">![Single Sign-On 구성](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769511.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="24175-164">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769511.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="24175-165">d.</span><span class="sxs-lookup"><span data-stu-id="24175-165">d.</span></span> <span data-ttu-id="24175-166">Hello에 **Single sign on** 섹션에서 **single sign-on 사용**, 클릭 하 고 **자세한** tooexpand이이 섹션.</span><span class="sxs-lookup"><span data-stu-id="24175-166">In hello **Single sign-on** section, select **Enable single sign-on**, and then click **More** tooexpand this section.</span></span>  
   
    <span data-ttu-id="24175-167">![Single Sign-On 구성](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769512.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="24175-167">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769512.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="24175-168">e.</span><span class="sxs-lookup"><span data-stu-id="24175-168">e.</span></span> <span data-ttu-id="24175-169">다음 너무 hello URL을 복사**가 전자 메일 주소를 입력 하 여 사용자가 로그인 할 수 확인 하거나 직접 이동할 수**합니다.</span><span class="sxs-lookup"><span data-stu-id="24175-169">Copy hello URL next too**Users can sign in by entering their email address or they can go directly to**.</span></span> 
    
    ![Single Sign-On 구성](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769513.png)
    
    <span data-ttu-id="24175-171">f.</span><span class="sxs-lookup"><span data-stu-id="24175-171">f.</span></span> <span data-ttu-id="24175-172">Hello hello에서 Azure 포털에서 **로그온 URL** 붙여넣기 hello URL 텍스트 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="24175-172">On hello Azure portal, in hello **Sign-on URL** textbox, paste hello URL.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_url.png)

     <span data-ttu-id="24175-174">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://www.dropbox.com/sso/<id>`</span><span class="sxs-lookup"><span data-stu-id="24175-174">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://www.dropbox.com/sso/<id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="24175-175">이 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="24175-175">This value is not real value.</span></span> <span data-ttu-id="24175-176">Hello 실제 로그온 URL로의 Single sign-on 섹션에서 가져올 hello 값을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="24175-176">Update hello value with hello actual Sign-on URL you get from their Single sign-on section.</span></span> <span data-ttu-id="24175-177">연락처 [비즈니스 클라이언트 지원 팀에 대 한 Dropbox](https://www.dropbox.com/business/contact) tooget이이 값입니다.</span><span class="sxs-lookup"><span data-stu-id="24175-177">Contact [Dropbox for Business Client support team](https://www.dropbox.com/business/contact) tooget this value.</span></span> 
 
4. <span data-ttu-id="24175-178">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **인증서 (Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="24175-178">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_certificate.png) 

5. <span data-ttu-id="24175-180">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="24175-180">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="24175-182">Hello에 **Dropbox for Business 구성** 섹션에서 클릭 **Dropbox for Business 구성** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="24175-182">On hello **Dropbox for Business Configuration** section, click **Configure Dropbox for Business** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="24175-183">복사 hello **SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="24175-183">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_configure.png) 

7. <span data-ttu-id="24175-185">tooconfigure single sign on에서 **Dropbox for Business** 쪽, Dropbox for hello에서 Business 테 넌 트에 **Single sign on** hello 섹션 **인증** 페이지 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="24175-185">tooconfigure single sign-on on **Dropbox for Business** side, Go on your Dropbox for Business tenant, in hello **Single sign-on** section of hello **Authentication** page, perform hello following steps:</span></span> 
   
    <span data-ttu-id="24175-186">![Single Sign-On 구성](./media/active-directory-saas-dropboxforbusiness-tutorial/IC769516.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="24175-186">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/IC769516.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="24175-187">a.</span><span class="sxs-lookup"><span data-stu-id="24175-187">a.</span></span> <span data-ttu-id="24175-188">**필수**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="24175-188">Click **Required**.</span></span>
   
    <span data-ttu-id="24175-189">b.</span><span class="sxs-lookup"><span data-stu-id="24175-189">b.</span></span> <span data-ttu-id="24175-190">Hello hello에 Azure 포털에서에서 **sign on 구성** 창, 복사 hello **SAML Single Sign-on 서비스 URL** 값을 복사한 다음 hello에 붙여 넣을 **로그인 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="24175-190">In hello Azure portal, on hello **Configure sign-on** window, copy hello **SAML Single Sign-On Service URL** value, and then paste it into hello **Sign-in URL** textbox.</span></span>

    <span data-ttu-id="24175-191">c.</span><span class="sxs-lookup"><span data-stu-id="24175-191">c.</span></span> <span data-ttu-id="24175-192">클릭 **인증서 선택**, 한 다음 tooyour **Base64 인코딩된 인증서 파일**합니다.</span><span class="sxs-lookup"><span data-stu-id="24175-192">Click **Choose certificate**, and then browse tooyour **Base64 encoded certificate file**.</span></span>

    <span data-ttu-id="24175-193">d.</span><span class="sxs-lookup"><span data-stu-id="24175-193">d.</span></span> <span data-ttu-id="24175-194">클릭 **ब ा ळ** DropBox for Business 테 넌 트에 toocomplete hello 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="24175-194">Click **Save changes** toocomplete hello configuration on your DropBox for Business tenant.</span></span>

> [!TIP]
> <span data-ttu-id="24175-195">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="24175-195">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="24175-196">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서 ** 구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="24175-196">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="24175-197">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="24175-197">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="24175-198">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="24175-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="24175-199">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="24175-199">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="24175-201">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="24175-201">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="24175-202">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="24175-202">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_01.png) 

2.  <span data-ttu-id="24175-204">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="24175-204">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="24175-206">Hello 대화의 hello 위쪽 클릭 **추가** tooopen hello **사용자** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="24175-206">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="24175-208">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="24175-208">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="24175-210">a.</span><span class="sxs-lookup"><span data-stu-id="24175-210">a.</span></span> <span data-ttu-id="24175-211">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="24175-211">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="24175-212">b.</span><span class="sxs-lookup"><span data-stu-id="24175-212">b.</span></span> <span data-ttu-id="24175-213">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="24175-213">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="24175-214">c.</span><span class="sxs-lookup"><span data-stu-id="24175-214">c.</span></span> <span data-ttu-id="24175-215">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="24175-215">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="24175-216">d.</span><span class="sxs-lookup"><span data-stu-id="24175-216">d.</span></span> <span data-ttu-id="24175-217">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="24175-217">Click **Create**.</span></span>
 
### <a name="creating-a-dropbox-for-business-test-user"></a><span data-ttu-id="24175-218">Dropbox for Business 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="24175-218">Creating a Dropbox for Business test user</span></span>

<span data-ttu-id="24175-219">이 섹션에서는 Dropbox for Business에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="24175-219">In this section, a user called Britta Simon is created in Dropbox for Business.</span></span> <span data-ttu-id="24175-220">Dropbox for Business는 기본적으로 사용하도록 설정된 Just-In-Time 프로비전을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="24175-220">Dropbox for Business supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="24175-221">이 섹션에 작업 항목이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="24175-221">There is no action item for you in this section.</span></span> <span data-ttu-id="24175-222">Dropbox for Business에에서 사용자 없으면 새 tooaccess Dropbox for Business 시도할 때 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="24175-222">If a user doesn't already exist in Dropbox for Business, a new one is created when you attempt tooaccess Dropbox for Business.</span></span>

>[!Note]
><span data-ttu-id="24175-223">Toocreate 수동으로 사용자에 게 문의 해야 할 경우 [Dropbox for Business 클라이언트 지원 팀](https://www.dropbox.com/business/contact)</span><span class="sxs-lookup"><span data-stu-id="24175-223">If you need toocreate a user manually, Contact [Dropbox for Business Client support team](https://www.dropbox.com/business/contact)</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="24175-224">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="24175-224">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="24175-225">이 섹션에서는 액세스 tooDropbox 비즈니스에 대 한 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="24175-225">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooDropbox for Business.</span></span>

![사용자 할당][200] 

<span data-ttu-id="24175-227">**tooassign 비즈니스용 Britta Simon tooDropbox hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="24175-227">**tooassign Britta Simon tooDropbox for Business, perform hello following steps:**</span></span>

1. <span data-ttu-id="24175-228">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="24175-228">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="24175-230">Hello 응용 프로그램 목록에서 선택 **Dropbox for Business**합니다.</span><span class="sxs-lookup"><span data-stu-id="24175-230">In hello applications list, select **Dropbox for Business**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_app.png) 

3. <span data-ttu-id="24175-232">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="24175-232">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="24175-234">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="24175-234">Click **Add** button.</span></span> <span data-ttu-id="24175-235">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="24175-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="24175-237">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24175-237">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="24175-238">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="24175-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="24175-239">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="24175-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="24175-240">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="24175-240">Testing single sign-on</span></span>

<span data-ttu-id="24175-241">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24175-241">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="24175-242">Hello 액세스 패널에서에서 비즈니스 타일에 대 한 hello Dropbox를 클릭 하면 비즈니스 응용 프로그램에 대 한 Dropbox의 로그인 페이지를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="24175-242">When you click hello Dropbox for Business tile in hello Access Panel, you should get login page of your Dropbox for Business application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="24175-243">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="24175-243">Additional resources</span></span>

* [<span data-ttu-id="24175-244">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="24175-244">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="24175-245">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="24175-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="24175-246">사용자 프로비저닝 구성</span><span class="sxs-lookup"><span data-stu-id="24175-246">Configure User Provisioning</span></span>](active-directory-saas-dropboxforbusiness-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_203.png

