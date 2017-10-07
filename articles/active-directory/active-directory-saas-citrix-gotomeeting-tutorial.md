---
title: "자습서: Citrix GoToMeeting과 Azure Active Directory 통합 | Microsoft 문서"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Citrix GoToMeeting 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7d7897f6-b88e-4dd5-8f3a-e612337b1413
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 46a5da7504806202a5ec29f73c504e772c61bc2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-citrix-gotomeeting"></a><span data-ttu-id="cdc34-103">자습서: Citrix GoToMeeting과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="cdc34-103">Tutorial: Azure Active Directory integration with Citrix GoToMeeting</span></span>

<span data-ttu-id="cdc34-104">이 자습서에 설명 어떻게 toointegrate Azure Active Directory (Azure AD)와 Citrix GoToMeeting 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc34-104">In this tutorial, you learn how toointegrate Citrix GoToMeeting with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cdc34-105">Azure AD와 Citrix GoToMeeting을 통합 hello 다음 이점을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc34-105">Integrating Citrix GoToMeeting with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="cdc34-106">액세스 tooCitrix GoToMeeting을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdc34-106">You can control in Azure AD who has access tooCitrix GoToMeeting</span></span>
- <span data-ttu-id="cdc34-107">프로그램 사용자 tooautomatically get 로그온 tooCitrix GoToMeeting (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdc34-107">You can enable your users tooautomatically get signed-on tooCitrix GoToMeeting (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cdc34-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdc34-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="cdc34-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc34-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cdc34-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="cdc34-110">Prerequisites</span></span>

<span data-ttu-id="cdc34-111">Citrix GoToMeeting과 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc34-111">tooconfigure Azure AD integration with Citrix GoToMeeting, you need hello following items:</span></span>

- <span data-ttu-id="cdc34-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="cdc34-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cdc34-113">Citrix GoToMeeting Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="cdc34-113">A Citrix GoToMeeting single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cdc34-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc34-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cdc34-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc34-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cdc34-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="cdc34-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cdc34-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdc34-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cdc34-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="cdc34-118">Scenario description</span></span>
<span data-ttu-id="cdc34-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc34-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cdc34-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdc34-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cdc34-121">Citrix GoToMeeting hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="cdc34-121">Adding Citrix GoToMeeting from hello gallery</span></span>
2. <span data-ttu-id="cdc34-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="cdc34-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-citrix-gotomeeting-from-hello-gallery"></a><span data-ttu-id="cdc34-123">Citrix GoToMeeting hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="cdc34-123">Adding Citrix GoToMeeting from hello gallery</span></span>
<span data-ttu-id="cdc34-124">tooconfigure hello와의 통합 Citrix GoToMeeting Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Citrix GoToMeeting tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc34-124">tooconfigure hello integration of Citrix GoToMeeting into Azure AD, you need tooadd Citrix GoToMeeting from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="cdc34-125">**hello 갤러리에서 Citrix GoToMeeting tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="cdc34-125">**tooadd Citrix GoToMeeting from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="cdc34-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="cdc34-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="cdc34-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc34-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="cdc34-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc34-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="cdc34-131">클릭 **새 응용 프로그램** hello 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="cdc34-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="cdc34-133">Hello 검색 상자에 입력 **Citrix GoToMeeting**합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc34-133">In hello search box, type **Citrix GoToMeeting**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_search.png)

5. <span data-ttu-id="cdc34-135">Hello 결과 패널에서 선택 **Citrix GoToMeeting**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="cdc34-135">In hello results panel, select **Citrix GoToMeeting**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cdc34-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="cdc34-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cdc34-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Citrix GoToMeeting에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc34-138">In this section, you configure and test Azure AD single sign-on with Citrix GoToMeeting based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="cdc34-139">Single sign on toowork에 대 한 Azure AD는 tooknow Citrix GoToMeeting의 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc34-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Citrix GoToMeeting is tooa user in Azure AD.</span></span> <span data-ttu-id="cdc34-140">즉, Azure AD 사용자와 Citrix GoToMeeting의 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc34-140">In other words, a link relationship between an Azure AD user and hello related user in Citrix GoToMeeting needs toobe established.</span></span>

<span data-ttu-id="cdc34-141">Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** Citrix GoToMeeting의 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc34-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Citrix GoToMeeting.</span></span>

<span data-ttu-id="cdc34-142">tooconfigure와 Citrix GoToMeeting과 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc34-142">tooconfigure and test Azure AD single sign-on with Citrix GoToMeeting, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="cdc34-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="cdc34-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="cdc34-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc34-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cdc34-145">**[Citrix GoToMeeting 테스트 사용자 만들기](#creating-a-citrix-gotomeeting-test-user)**  -toohave Britta Simon 표현인 연결 된 toohello Azure AD 사용자의 Citrix GoToMeeting에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="cdc34-145">**[Creating a Citrix GoToMeeting test user](#creating-a-citrix-gotomeeting-test-user)** - toohave a counterpart of Britta Simon in Citrix GoToMeeting that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="cdc34-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="cdc34-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cdc34-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="cdc34-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cdc34-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="cdc34-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cdc34-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 Citrix GoToMeeting 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc34-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Citrix GoToMeeting application.</span></span>

<span data-ttu-id="cdc34-150">**Azure AD tooconfigure single sign on와 Citrix GoToMeeting hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="cdc34-150">**tooconfigure Azure AD single sign-on with Citrix GoToMeeting, perform hello following steps:**</span></span>

1. <span data-ttu-id="cdc34-151">Hello hello에 Azure 포털에서에서 **Citrix GoToMeeting** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc34-151">In hello Azure portal, on hello **Citrix GoToMeeting** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="cdc34-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="cdc34-153">On hello **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_samlbase.png)

3. <span data-ttu-id="cdc34-155">Hello에 **Citrix GoToMeeting 도메인 및 Url** 섹션 없습니다 필요 tooperform 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="cdc34-155">On hello **Citrix GoToMeeting Domain and URLs** section, no need tooperform any steps.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_url.png)


3. <span data-ttu-id="cdc34-157">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **인증서 (Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc34-157">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_certificate.png) 

4. <span data-ttu-id="cdc34-159">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc34-159">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_400.png)
    
5. <span data-ttu-id="cdc34-161">Citrix GoToMeeting SAML 구성 섹션 hello 창 로그온 Citrix GoToMeeting SAML 구성 tooopen 구성을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc34-161">On hello Citrix GoToMeeting SAML Configuration section, click Configure Citrix GoToMeeting SAML tooopen Configure sign-on window.</span></span> <span data-ttu-id="cdc34-162">복사 hello **Sign-Out URL, SAML 엔터티 ID, 및 SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="cdc34-162">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

6. <span data-ttu-id="cdc34-163">다른 브라우저 창에서 tooyour에 로그인 [Citrix 조직 센터](https://account.citrixonline.com/organization/administration/)합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc34-163">In a different browser window, log in tooyour [Citrix Organization Center](https://account.citrixonline.com/organization/administration/).</span></span>

7. <span data-ttu-id="cdc34-164">Hello 클릭 **Id 공급자** 탭을 클릭 한 다음 단계를 수행 하는 hello를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc34-164">Click hello **Identity Provider** tab, and then perform hello following steps:</span></span>  
   
    <span data-ttu-id="cdc34-165">![SAML 설정](./media/active-directory-saas-citrix-gotomeeting-tutorial/IC6892321.png "SAML 설정")</span><span class="sxs-lookup"><span data-stu-id="cdc34-165">![SAML setup](./media/active-directory-saas-citrix-gotomeeting-tutorial/IC6892321.png "SAML setup")</span></span>
   
    <span data-ttu-id="cdc34-166">a.</span><span class="sxs-lookup"><span data-stu-id="cdc34-166">a.</span></span> <span data-ttu-id="cdc34-167">**수동**</span><span class="sxs-lookup"><span data-stu-id="cdc34-167">Select **Manual**</span></span>

    <span data-ttu-id="cdc34-168">b.</span><span class="sxs-lookup"><span data-stu-id="cdc34-168">b.</span></span> <span data-ttu-id="cdc34-169">Hello hello에 Azure 포털에서에서 **Citrix GoToMeeting에서 single sign on 구성** 대화 상자 페이지에서 복사 hello **SAML Single Sign-on 서비스 URL** 값을 복사한 다음 hello에 붙여 넣을 **로그인 페이지 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="cdc34-169">In hello Azure portal, on hello **Configure single sign-on at Citrix GoToMeeting** dialog page, copy hello **SAML Single Sign-On Service URL** value, and then paste it into hello **Sign-in page URL** textbox.</span></span> 

    <span data-ttu-id="cdc34-170">c.</span><span class="sxs-lookup"><span data-stu-id="cdc34-170">c.</span></span> <span data-ttu-id="cdc34-171">Hello hello에 Azure 포털에서에서 **Citrix GoToMeeting에서 single sign on 구성** 대화 상자 페이지에서 복사 hello **Sign-Out URL** 값을 복사한 다음 hello에 붙여 넣을 **로그 아웃 페이지 URL**텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="cdc34-171">In hello Azure portal, on hello **Configure single sign-on at Citrix GoToMeeting** dialog page, copy hello **Sign-Out URL** value, and then paste it into hello **Sign-out page URL** textbox.</span></span>

    <span data-ttu-id="cdc34-172">d.</span><span class="sxs-lookup"><span data-stu-id="cdc34-172">d.</span></span> <span data-ttu-id="cdc34-173">Hello hello에 Azure 포털에서에서 **Citrix GoToMeeting에서 single sign on 구성** 대화 상자 페이지에서 복사 hello **SAML 엔터티 ID** 값을 복사한 다음 hello에 붙여 넣을 **Id 공급자 엔터티 ID**  텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="cdc34-173">In hello Azure portal, on hello **Configure single sign-on at Citrix GoToMeeting** dialog page, copy hello **SAML Entity ID** value, and then paste it into hello **Identity Provider Entity ID** textbox.</span></span>

    <span data-ttu-id="cdc34-174">e.</span><span class="sxs-lookup"><span data-stu-id="cdc34-174">e.</span></span> <span data-ttu-id="cdc34-175">tooupload 다운로드 한 인증서를 클릭 하 여 **인증서 업로드**합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc34-175">tooupload your downloaded certificate, click **Upload Certificate**.</span></span>

    <span data-ttu-id="cdc34-176">f.</span><span class="sxs-lookup"><span data-stu-id="cdc34-176">f.</span></span> <span data-ttu-id="cdc34-177">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc34-177">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="cdc34-178">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="cdc34-178">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="cdc34-179">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="cdc34-179">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="cdc34-180">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cdc34-180">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cdc34-181">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="cdc34-181">Creating an Azure AD test user</span></span>
<span data-ttu-id="cdc34-182">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="cdc34-182">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="cdc34-184">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="cdc34-184">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="cdc34-185">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="cdc34-185">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cdc34-187">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc34-187">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cdc34-189">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc34-189">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cdc34-191">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc34-191">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cdc34-193">a.</span><span class="sxs-lookup"><span data-stu-id="cdc34-193">a.</span></span> <span data-ttu-id="cdc34-194">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc34-194">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cdc34-195">b.</span><span class="sxs-lookup"><span data-stu-id="cdc34-195">b.</span></span> <span data-ttu-id="cdc34-196">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc34-196">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cdc34-197">c.</span><span class="sxs-lookup"><span data-stu-id="cdc34-197">c.</span></span> <span data-ttu-id="cdc34-198">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc34-198">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="cdc34-199">d.</span><span class="sxs-lookup"><span data-stu-id="cdc34-199">d.</span></span> <span data-ttu-id="cdc34-200">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc34-200">Click **Create**.</span></span>
 
### <a name="creating-a-citrix-gotomeeting-test-user"></a><span data-ttu-id="cdc34-201">Citrix GoToMeeting 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="cdc34-201">Creating a Citrix GoToMeeting test user</span></span>

<span data-ttu-id="cdc34-202">이 섹션에서는 Citrix GoToMeeting에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cdc34-202">In this section, a user called Britta Simon is created in Citrix GoToMeeting.</span></span> <span data-ttu-id="cdc34-203">Citrix GoToMeeting은 기본적으로 설정되는 Just-In-Time 프로비전을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc34-203">Citrix GoToMeeting supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="cdc34-204">이 섹션에 작업 항목이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cdc34-204">There is no action item for you in this section.</span></span> <span data-ttu-id="cdc34-205">Citrix GoToMeeting에 사용자 없으면 새 tooaccess Citrix GoToMeeting을 시도할 때 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="cdc34-205">If a user doesn't already exist in Citrix GoToMeeting, a new one is created when you attempt tooaccess Citrix GoToMeeting.</span></span>

>[!Note]
><span data-ttu-id="cdc34-206">Toocreate 수동으로 사용자에 게 문의 해야 할 경우 [Citrix GoToMeeting 지원 팀](https://care.citrixonline.com/gotomeeting)</span><span class="sxs-lookup"><span data-stu-id="cdc34-206">If you need toocreate a user manually, Contact [Citrix GoToMeeting support team](https://care.citrixonline.com/gotomeeting)</span></span> 


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="cdc34-207">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc34-207">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="cdc34-208">이 섹션에서는 액세스 tooCitrix GoToMeeting 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc34-208">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCitrix GoToMeeting.</span></span>

![사용자 할당][200] 

<span data-ttu-id="cdc34-210">**tooassign Britta Simon tooCitrix GoToMeeting, hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="cdc34-210">**tooassign Britta Simon tooCitrix GoToMeeting, perform hello following steps:**</span></span>

1. <span data-ttu-id="cdc34-211">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc34-211">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="cdc34-213">Hello 응용 프로그램 목록에서 선택 **Citrix GoToMeeting**합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc34-213">In hello applications list, select **Citrix GoToMeeting**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_app.png) 

3. <span data-ttu-id="cdc34-215">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc34-215">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="cdc34-217">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc34-217">Click **Add** button.</span></span> <span data-ttu-id="cdc34-218">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc34-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="cdc34-220">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdc34-220">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="cdc34-221">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc34-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cdc34-222">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc34-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cdc34-223">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="cdc34-223">Testing single sign-on</span></span>

<span data-ttu-id="cdc34-224">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdc34-224">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="cdc34-225">Single sign on 설정 tootest 원하는 hello 액세스 패널을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="cdc34-225">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="cdc34-226">액세스 패널 hello에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc34-226">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cdc34-227">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="cdc34-227">Additional resources</span></span>

* [<span data-ttu-id="cdc34-228">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="cdc34-228">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cdc34-229">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="cdc34-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="cdc34-230">사용자 프로비저닝 구성</span><span class="sxs-lookup"><span data-stu-id="cdc34-230">Configure User Provisioning</span></span>](active-directory-saas-citrixgotomeeting-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_203.png

