---
title: "자습서: Druva와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Druva 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ab92b600-1fea-4905-b1c7-ef8e4d8c495c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: a1c36c06d6d005e0aa363fbf34efe630e4cca1ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-druva"></a><span data-ttu-id="e9594-103">자습서: Druva와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="e9594-103">Tutorial: Azure Active Directory integration with Druva</span></span>

<span data-ttu-id="e9594-104">이 자습서에 설명 어떻게 toointegrate Azure Active Directory (Azure AD)와 Druva 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-104">In this tutorial, you learn how toointegrate Druva with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e9594-105">Azure AD와 Druva 통합 이점을 다음 hello로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-105">Integrating Druva with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e9594-106">액세스 tooDruva을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-106">You can control in Azure AD who has access tooDruva.</span></span>
- <span data-ttu-id="e9594-107">에 사용자가 tooautomatically get 로그온 tooDruva (Single Sign-on)는 Azure AD 계정으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-107">You can enable your users tooautomatically get signed-on tooDruva (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="e9594-108">하나의 중앙 위치-hello Azure 포털에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="e9594-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e9594-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="e9594-110">Prerequisites</span></span>

<span data-ttu-id="e9594-111">Druva와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-111">tooconfigure Azure AD integration with Druva, you need hello following items:</span></span>

- <span data-ttu-id="e9594-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="e9594-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e9594-113">Druva Single Sign-on이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="e9594-113">A Druva single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e9594-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e9594-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e9594-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="e9594-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e9594-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e9594-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="e9594-118">Scenario description</span></span>
<span data-ttu-id="e9594-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e9594-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e9594-121">Druva는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="e9594-121">Adding Druva from hello gallery</span></span>
2. <span data-ttu-id="e9594-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="e9594-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-druva-from-hello-gallery"></a><span data-ttu-id="e9594-123">Druva는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="e9594-123">Adding Druva from hello gallery</span></span>
<span data-ttu-id="e9594-124">tooconfigure hello와의 통합 Druva Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Druva tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-124">tooconfigure hello integration of Druva into Azure AD, you need tooadd Druva from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e9594-125">**Druva hello 갤러리에서 tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="e9594-125">**tooadd Druva from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e9594-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![hello Azure Active Directory 단추][1]

2. <span data-ttu-id="e9594-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e9594-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-129">Then go too**All applications**.</span></span>

    ![hello 엔터프라이즈 응용 프로그램 블레이드][2]
    
3. <span data-ttu-id="e9594-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![hello 새 응용 프로그램 단추][3]

4. <span data-ttu-id="e9594-133">Hello 검색 상자에 입력 **Druva**선택, **Druva** 결과 패널에서 클릭 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-133">In hello search box, type **Druva**, select **Druva** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Druva hello 결과 목록에서](./media/active-directory-saas-druva-tutorial/tutorial_druva_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="e9594-135">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="e9594-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="e9594-136">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Druva에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-136">In this section, you configure and test Azure AD single sign-on with Druva based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e9594-137">Single sign on toowork에 대 한 Azure AD는 tooknow Druva에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Druva is tooa user in Azure AD.</span></span> <span data-ttu-id="e9594-138">즉, Azure AD 사용자와 Druva에 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-138">In other words, a link relationship between an Azure AD user and hello related user in Druva needs toobe established.</span></span>

<span data-ttu-id="e9594-139">Druva에 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-139">In Druva, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="e9594-140">tooconfigure와 Druva 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-140">tooconfigure and test Azure AD single sign-on with Druva, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e9594-141">**[Azure AD Single Sign-on 구성](#configure-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e9594-142">**[Azure AD 테스트를 만들고](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e9594-143">**[Druva 테스트 사용자 만들기](#create-a-druva-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 Druva에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-143">**[Create a Druva test user](#create-a-druva-test-user)** - toohave a counterpart of Britta Simon in Druva that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e9594-144">**[Azure AD hello 테스트 사용자를 할당](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e9594-145">**[Single sign on 테스트](#test-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="e9594-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="e9594-146">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="e9594-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="e9594-147">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 Druva 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Druva application.</span></span>

<span data-ttu-id="e9594-148">**Azure AD tooconfigure single sign on와 Druva를 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="e9594-148">**tooconfigure Azure AD single sign-on with Druva, perform hello following steps:**</span></span>

1. <span data-ttu-id="e9594-149">Hello hello에 Azure 포털에서에서 **Druva** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-149">In hello Azure portal, on hello **Druva** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-On 구성 링크][4]

2. <span data-ttu-id="e9594-151">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-druva-tutorial/tutorial_druva_samlbase.png)

3. <span data-ttu-id="e9594-153">Hello에 **Druva 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-153">On hello **Druva Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-druva-tutorial/tutorial_druva_url.png)

    <span data-ttu-id="e9594-155">Hello에 **로그온 URL** textbox hello URL 입력:`https://cloud.druva.com/home`</span><span class="sxs-lookup"><span data-stu-id="e9594-155">In hello **Sign-on URL** textbox, type hello URL: `https://cloud.druva.com/home`</span></span>

4. <span data-ttu-id="e9594-156">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **Certificate(Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-156">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![hello 인증서 다운로드 링크](./media/active-directory-saas-druva-tutorial/tutorial_druva_certificate.png) 

5. <span data-ttu-id="e9594-158">Druva 응용 프로그램에 사용자 지정 특성 매핑을 tooyour tooadd 요구 하는 특정 형식으로 hello SAML 어설션이 **SAML 토큰 특성** 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-158">Your Druva application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour **SAML Token Attributes** configuration.</span></span> 

    ![Single Sign-on 구성](./media/active-directory-saas-druva-tutorial/tutorial_druva_attribute.png)

6. <span data-ttu-id="e9594-160">Hello에 **사용자 특성** hello 섹션 **Single sign on** 대화 상자에서 hello 이미지 앞에 표시 된 대로 SAML 토큰 특성을 구성 하 고 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-160">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello preceding image and perform hello following steps:</span></span>

    | <span data-ttu-id="e9594-161">특성 이름</span><span class="sxs-lookup"><span data-stu-id="e9594-161">Attribute Name</span></span>      | <span data-ttu-id="e9594-162">특성 값</span><span class="sxs-lookup"><span data-stu-id="e9594-162">Attribute Value</span></span>      |
    | ------------------- | -------------------- |
    | <span data-ttu-id="e9594-163">insync\_auth\_token</span><span class="sxs-lookup"><span data-stu-id="e9594-163">insync\_auth\_token</span></span> |<span data-ttu-id="e9594-164">Hello 토큰 생성 된 값 입력</span><span class="sxs-lookup"><span data-stu-id="e9594-164">Enter hello token generated value</span></span> |
    
    <span data-ttu-id="e9594-165">a.</span><span class="sxs-lookup"><span data-stu-id="e9594-165">a.</span></span> <span data-ttu-id="e9594-166">클릭 **특성 추가** tooopen hello **특성 추가** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="e9594-166">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>
    
    ![Single Sign-on 구성](./media/active-directory-saas-druva-tutorial/tutorial_attribute_04.png)
    
    ![Single Sign-on 구성](./media/active-directory-saas-druva-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="e9594-169">b.</span><span class="sxs-lookup"><span data-stu-id="e9594-169">b.</span></span> <span data-ttu-id="e9594-170">Hello에 **이름** textbox, 해당 행에 대 한 표시 형식 hello 특성 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-170">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="e9594-171">c.</span><span class="sxs-lookup"><span data-stu-id="e9594-171">c.</span></span> <span data-ttu-id="e9594-172">Hello에서 **값** 목록, 해당 행에 대 한 표시 유형 hello 특성 값입니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-172">From hello **Value** list, type hello attribute value shown for that row.</span></span> <span data-ttu-id="e9594-173">hello 토큰 생성 된 값이 자습서의 뒷부분에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-173">hello token generated value is explained later in tutorial.</span></span>
    
    <span data-ttu-id="e9594-174">d.</span><span class="sxs-lookup"><span data-stu-id="e9594-174">d.</span></span> <span data-ttu-id="e9594-175">**Ok**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-175">Click **Ok**.</span></span>    

7. <span data-ttu-id="e9594-176">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-176">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-druva-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="e9594-178">Hello에 **Druva 구성** 섹션에서 클릭 **구성 Druva** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="e9594-178">On hello **Druva Configuration** section, click **Configure Druva** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="e9594-179">복사 hello **Sign-Out URL 및 SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="e9594-179">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-druva-tutorial/tutorial_druva_configure.png) 

9. <span data-ttu-id="e9594-181">다른 웹 브라우저 창에서 관리자 권한으로 tooyour Druva 회사 사이트에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-181">In a different web browser window, log in tooyour Druva company site as an administrator.</span></span>

10. <span data-ttu-id="e9594-182">너무 이동**관리 \> 설정을**합니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-182">Go too**Manage \> Settings**.</span></span>

    <span data-ttu-id="e9594-183">![설정](./media/active-directory-saas-druva-tutorial/ic795091.png "설정")</span><span class="sxs-lookup"><span data-stu-id="e9594-183">![Settings](./media/active-directory-saas-druva-tutorial/ic795091.png "Settings")</span></span>

11. <span data-ttu-id="e9594-184">Hello Single Sign-on 설정 대화 상자에서 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-184">On hello Single Sign-On Settings dialog, perform hello following steps:</span></span>

    <span data-ttu-id="e9594-185">![Single Sign-On 설정](./media/active-directory-saas-druva-tutorial/ic795092.png "Single Sign-On 설정")</span><span class="sxs-lookup"><span data-stu-id="e9594-185">![Single Sign-On Settings](./media/active-directory-saas-druva-tutorial/ic795092.png "Single Sign-On Settings")</span></span>
    
    <span data-ttu-id="e9594-186">a.</span><span class="sxs-lookup"><span data-stu-id="e9594-186">a.</span></span> <span data-ttu-id="e9594-187">붙여넣기 **SAML Single Sign-on 서비스 URL** hello에 hello Azure 포털에서에서 복사한 값 **ID 공급자 로그인 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-187">Paste **SAML Single Sign-On Service URL** value, which you have copied from hello Azure portal into hello **ID Provider Login URL** textbox.</span></span>
    
    <span data-ttu-id="e9594-188">b.</span><span class="sxs-lookup"><span data-stu-id="e9594-188">b.</span></span> <span data-ttu-id="e9594-189">붙여넣기 **Sign-Out URL** hello에 hello Azure 포털에서에서 복사한 값 **ID 공급자 로그 아웃 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-189">Paste **Sign-Out URL** value, which you have copied from hello Azure portal into hello **ID Provider Logout URL** textbox.</span></span>
    
     <span data-ttu-id="e9594-190">c.</span><span class="sxs-lookup"><span data-stu-id="e9594-190">c.</span></span> <span data-ttu-id="e9594-191">콘텐츠를 클립보드에 복사 hello 메모장에서 e-64로 인코딩된 인증서를 열고 toohello 붙여 **ID 공급자 인증서** textbox</span><span class="sxs-lookup"><span data-stu-id="e9594-191">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **ID Provider Certificate** textbox</span></span>
     
     <span data-ttu-id="e9594-192">d.</span><span class="sxs-lookup"><span data-stu-id="e9594-192">d.</span></span> <span data-ttu-id="e9594-193">tooopen hello **설정** 페이지 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-193">tooopen hello **Settings** page, click **Save**.</span></span>

12. <span data-ttu-id="e9594-194">Hello에 **설정** 페이지 **SSO 토큰 생성**합니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-194">On hello **Settings** page, click **Generate SSO Token**.</span></span>

    <span data-ttu-id="e9594-195">![설정](./media/active-directory-saas-druva-tutorial/ic795093.png "설정")</span><span class="sxs-lookup"><span data-stu-id="e9594-195">![Settings](./media/active-directory-saas-druva-tutorial/ic795093.png "Settings")</span></span>

13. <span data-ttu-id="e9594-196">Hello에 **Single Sign on 인증 토큰** 대화 상자에서 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-196">On hello **Single Sign-on Authentication Token** dialog, perform hello following steps:</span></span>

    <span data-ttu-id="e9594-197">![SSO 토큰](./media/active-directory-saas-druva-tutorial/ic795094.png "SSO 토큰")</span><span class="sxs-lookup"><span data-stu-id="e9594-197">![SSO Token](./media/active-directory-saas-druva-tutorial/ic795094.png "SSO Token")</span></span>
    
    <span data-ttu-id="e9594-198">a.</span><span class="sxs-lookup"><span data-stu-id="e9594-198">a.</span></span> <span data-ttu-id="e9594-199">클릭 **복사**, 붙여넣기 hello에서 값을 복사한 **값** hello 텍스트 상자로 **특성 추가** 섹션.</span><span class="sxs-lookup"><span data-stu-id="e9594-199">Click **Copy**, Paste copied value in hello **Value** textbox in hello **Add Attribute** section.</span></span>
    
    <span data-ttu-id="e9594-200">b.</span><span class="sxs-lookup"><span data-stu-id="e9594-200">b.</span></span> <span data-ttu-id="e9594-201">**닫기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-201">Click **Close**.</span></span>

> [!TIP]
> <span data-ttu-id="e9594-202">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="e9594-202">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e9594-203">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="e9594-203">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e9594-204">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e9594-204">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="e9594-205">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="e9594-205">Create an Azure AD test user</span></span>

<span data-ttu-id="e9594-206">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-206">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Azure AD 테스트 사용자 만들기][100]

<span data-ttu-id="e9594-208">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="e9594-208">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e9594-209">Hello hello 왼쪽된 창에서 Azure 포털에서에서 클릭 hello **Azure Active Directory** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-209">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![hello Azure Active Directory 단추](./media/active-directory-saas-druva-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="e9594-211">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹**, 클릭 하 고 **모든 사용자가**합니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-211">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    !["사용자 및 그룹" hello 및 "모든 사용자" 링크](./media/active-directory-saas-druva-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="e9594-213">tooopen hello **사용자** 대화 상자를 클릭 **추가** hello hello 맨 **모든 사용자에 게** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="e9594-213">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![hello 추가 단추](./media/active-directory-saas-druva-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="e9594-215">Hello에 **사용자** 대화 상자를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-215">In hello **User** dialog box, perform hello following steps:</span></span>

    ![hello 사용자 대화 상자](./media/active-directory-saas-druva-tutorial/create_aaduser_04.png)

    <span data-ttu-id="e9594-217">a.</span><span class="sxs-lookup"><span data-stu-id="e9594-217">a.</span></span> <span data-ttu-id="e9594-218">Hello에 **이름** 상자에서 입력 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-218">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e9594-219">b.</span><span class="sxs-lookup"><span data-stu-id="e9594-219">b.</span></span> <span data-ttu-id="e9594-220">Hello에 **사용자 이름** 상자의 사용자 Britta Simon의 hello 전자 메일 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-220">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="e9594-221">c.</span><span class="sxs-lookup"><span data-stu-id="e9594-221">c.</span></span> <span data-ttu-id="e9594-222">선택 hello **암호 표시** 확인란을 선택한 다음 hello에 표시 되는 hello 값 기록 **암호** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-222">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="e9594-223">d.</span><span class="sxs-lookup"><span data-stu-id="e9594-223">d.</span></span> <span data-ttu-id="e9594-224">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-224">Click **Create**.</span></span>
 
### <a name="create-a-druva-test-user"></a><span data-ttu-id="e9594-225">Druva 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="e9594-225">Create a Druva test user</span></span>

<span data-ttu-id="e9594-226">Tooenable Azure AD 사용자가 toolog tooDruva에 주문 하 고에 Druva에 이들 프로 비전 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-226">In order tooenable Azure AD users toolog in tooDruva, they must be provisioned into Druva.</span></span> <span data-ttu-id="e9594-227">Hello Druva의 경우에서 프로 비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-227">In hello case of Druva, provisioning is a manual task.</span></span>

<span data-ttu-id="e9594-228">**tooconfigure 사용자 프로비저닝, hello 다음 단계를 수행:**</span><span class="sxs-lookup"><span data-stu-id="e9594-228">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="e9594-229">Tooyour 로그인 **Druva** 회사 사이트에서 관리자 권한으로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-229">Log in tooyour **Druva** company site as administrator.</span></span>

2. <span data-ttu-id="e9594-230">너무 이동**관리 \> 사용자**합니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-230">Go too**Manage \> Users**.</span></span>
   
   <span data-ttu-id="e9594-231">![사용자 관리](./media/active-directory-saas-druva-tutorial/ic795097.png "사용자 관리")</span><span class="sxs-lookup"><span data-stu-id="e9594-231">![Manage Users](./media/active-directory-saas-druva-tutorial/ic795097.png "Manage Users")</span></span>

3. <span data-ttu-id="e9594-232">**새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-232">Click **Create New**.</span></span>
   
   <span data-ttu-id="e9594-233">![사용자 관리](./media/active-directory-saas-druva-tutorial/ic795098.png "사용자 관리")</span><span class="sxs-lookup"><span data-stu-id="e9594-233">![Manage Users](./media/active-directory-saas-druva-tutorial/ic795098.png "Manage Users")</span></span>

4. <span data-ttu-id="e9594-234">Hello 새 사용자 만들기 대화 상자에서 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-234">On hello Create New User dialog, perform hello following steps:</span></span>
   
   <span data-ttu-id="e9594-235">![NewUser 만들기](./media/active-directory-saas-druva-tutorial/ic795099.png "NewUser 만들기")</span><span class="sxs-lookup"><span data-stu-id="e9594-235">![Create NewUser](./media/active-directory-saas-druva-tutorial/ic795099.png "Create NewUser")</span></span>
   
   <span data-ttu-id="e9594-236">a.</span><span class="sxs-lookup"><span data-stu-id="e9594-236">a.</span></span> <span data-ttu-id="e9594-237">Hello에 **전자 메일 주소** 텍스트 상자와 같은 사용자의 전자 메일을 hello 입력  **brittasimon@contoso.com** 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-237">In hello **Email address** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>
   
   <span data-ttu-id="e9594-238">b.</span><span class="sxs-lookup"><span data-stu-id="e9594-238">b.</span></span> <span data-ttu-id="e9594-239">Hello에 **이름** 텍스트 상자와 같은 사용자의 hello 이름 입력 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-239">In hello **Name** textbox, enter hello name of user like **BrittaSimon**.</span></span>
   
   <span data-ttu-id="e9594-240">c.</span><span class="sxs-lookup"><span data-stu-id="e9594-240">c.</span></span> <span data-ttu-id="e9594-241">**사용자 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-241">Click **Create User**.</span></span>

>[!NOTE]
><span data-ttu-id="e9594-242">다른 Druva 사용자 계정 만들기 도구를 사용할 수 있습니다 또는 Azure AD 사용자 계정을 tooprovision Druva에서 제공 된 Api입니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-242">You can use any other Druva user account creation tools or APIs provided by Druva tooprovision Azure AD user accounts.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="e9594-243">Azure AD hello 테스트 사용자를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-243">Assign hello Azure AD test user</span></span>

<span data-ttu-id="e9594-244">이 섹션에서는 tooDruva 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-244">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooDruva.</span></span>

![Hello 사용자 역할 할당][200] 

<span data-ttu-id="e9594-246">**tooassign Britta Simon tooDruva hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="e9594-246">**tooassign Britta Simon tooDruva, perform hello following steps:**</span></span>

1. <span data-ttu-id="e9594-247">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-247">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="e9594-249">Hello 응용 프로그램 목록에서 선택 **Druva**합니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-249">In hello applications list, select **Druva**.</span></span>

    ![hello 응용 프로그램 목록에서 hello Druva 링크](./media/active-directory-saas-druva-tutorial/tutorial_druva_app.png)  

3. <span data-ttu-id="e9594-251">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-251">In hello menu on hello left, click **Users and groups**.</span></span>

    ![hello "사용자 및 그룹" 링크][202]

4. <span data-ttu-id="e9594-253">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-253">Click **Add** button.</span></span> <span data-ttu-id="e9594-254">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![hello 할당 추가 창][203]

5. <span data-ttu-id="e9594-256">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-256">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e9594-257">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e9594-258">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="e9594-259">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="e9594-259">Test single sign-on</span></span>

<span data-ttu-id="e9594-260">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-260">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="e9594-261">Hello 액세스 패널에서에서 hello Druva 타일을 클릭할 때 자동으로 로그온 tooyour Druva 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-261">When you click hello Druva tile in hello Access Panel, you should get automatically signed-on tooyour Druva application.</span></span>
<span data-ttu-id="e9594-262">액세스 패널에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e9594-262">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="e9594-263">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="e9594-263">Additional resources</span></span>

* [<span data-ttu-id="e9594-264">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="e9594-264">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e9594-265">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="e9594-265">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-druva-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-druva-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-druva-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-druva-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-druva-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-druva-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-druva-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-druva-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-druva-tutorial/tutorial_general_203.png

