---
title: "자습서: Hightail과 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Hightail 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e15206ac-74b0-46e4-9329-892c7d242ec0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: 2b36fcf8d5773255fdf89de2dccdceb95c032bd8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hightail"></a><span data-ttu-id="7a97d-103">자습서:Azure Active Directory와 Hightail 통합</span><span class="sxs-lookup"><span data-stu-id="7a97d-103">Tutorial: Azure Active Directory integration with Hightail</span></span>

<span data-ttu-id="7a97d-104">이 자습서에 설명 toointegrate Azure Active Directory (Azure AD)와 Hightail 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-104">In this tutorial, you learn how toointegrate Hightail with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7a97d-105">다음 이점을 hello로 제공 Hightail Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="7a97d-105">Integrating Hightail with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7a97d-106">액세스 tooHightail을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-106">You can control in Azure AD who has access tooHightail</span></span>
- <span data-ttu-id="7a97d-107">프로그램 사용자 tooautomatically get 로그온 tooHightail (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-107">You can enable your users tooautomatically get signed-on tooHightail (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7a97d-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="7a97d-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7a97d-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="7a97d-110">Prerequisites</span></span>

<span data-ttu-id="7a97d-111">다음 항목 hello가 필요 tooconfigure Hightail와 Azure AD 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-111">tooconfigure Azure AD integration with Hightail, you need hello following items:</span></span>

- <span data-ttu-id="7a97d-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="7a97d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7a97d-113">Hightail Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="7a97d-113">A Hightail single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7a97d-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7a97d-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7a97d-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="7a97d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7a97d-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7a97d-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="7a97d-118">Scenario description</span></span>
<span data-ttu-id="7a97d-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7a97d-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7a97d-121">Hightail은 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="7a97d-121">Adding Hightail from hello gallery</span></span>
2. <span data-ttu-id="7a97d-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="7a97d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hightail-from-hello-gallery"></a><span data-ttu-id="7a97d-123">Hightail은 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="7a97d-123">Adding Hightail from hello gallery</span></span>
<span data-ttu-id="7a97d-124">tooconfigure hello와의 통합 Hightail Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Hightail tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-124">tooconfigure hello integration of Hightail into Azure AD, you need tooadd Hightail from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7a97d-125">**hello 갤러리에서 Hightail tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="7a97d-125">**tooadd Hightail from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7a97d-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7a97d-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7a97d-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="7a97d-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="7a97d-133">Hello 검색 상자에 입력 **Hightail**합니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-133">In hello search box, type **Hightail**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_search.png)

5. <span data-ttu-id="7a97d-135">Hello 결과 패널에서 선택 **Hightail**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-135">In hello results panel, select **Hightail**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7a97d-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="7a97d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7a97d-138">이 섹션에서는 “Britta Simon”이라는 테스트 사용자를 기반으로 Hightail에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-138">In this section, you configure and test Azure AD single sign-on with Hightail based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7a97d-139">Single sign on toowork에 대 한 Azure AD는 tooknow Hightail에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Hightail is tooa user in Azure AD.</span></span> <span data-ttu-id="7a97d-140">즉, Azure AD 사용자 및 Hightail에 hello 관련된 사용자 간 링크 관계를 설정할 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-140">In other words, a link relationship between an Azure AD user and hello related user in Hightail needs toobe established.</span></span>

<span data-ttu-id="7a97d-141">Hightail에서 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-141">In Hightail, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="7a97d-142">tooconfigure 및 Hightail 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-142">tooconfigure and test Azure AD single sign-on with Hightail, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7a97d-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7a97d-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7a97d-145">**[Hightail 테스트 사용자 만들기](#creating-a-hightail-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 Hightail에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-145">**[Creating a Hightail test user](#creating-a-hightail-test-user)** - toohave a counterpart of Britta Simon in Hightail that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="7a97d-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7a97d-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="7a97d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7a97d-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="7a97d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7a97d-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 Hightail 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Hightail application.</span></span>

<span data-ttu-id="7a97d-150">**tooconfigure Azure AD single sign on, Hightail와 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="7a97d-150">**tooconfigure Azure AD single sign-on with Hightail, perform hello following steps:**</span></span>

1. <span data-ttu-id="7a97d-151">Hello hello에 Azure 포털에서에서 **Hightail** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-151">In hello Azure portal, on hello **Hightail** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="7a97d-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_samlbase.png)

3. <span data-ttu-id="7a97d-155">Hello에 **Hightail 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-155">On hello **Hightail Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_url.png)

     <span data-ttu-id="7a97d-157">Hello에 **회신 URL** textbox로 hello URL 입력:`https://www.hightail.com/samlLogin?phi_action=app/samlLogin&subAction=handleSamlResponse`</span><span class="sxs-lookup"><span data-stu-id="7a97d-157">In hello **Reply URL** textbox, type hello URL as: `https://www.hightail.com/samlLogin?phi_action=app/samlLogin&subAction=handleSamlResponse`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7a97d-158">hello 이전 값이 실제 값.</span><span class="sxs-lookup"><span data-stu-id="7a97d-158">hello preceding value is not real value.</span></span> <span data-ttu-id="7a97d-159">Hello 자습서의 뒷부분에 설명 되어 hello 실제 회신 URL로 hello 값을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-159">You will update hello value with hello actual Reply URL, which is explained later in hello tutorial.</span></span>
 
4. <span data-ttu-id="7a97d-160">Hello에 **Hightail 도메인 및 Url** 섹션 tooconfigure hello 응용 프로그램에 필요한 경우 **SP 시작 모드**, hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-160">On hello **Hightail Domain and URLs** section, If you wish tooconfigure hello application in **SP initiated mode**, perform hello following steps:</span></span>
    
    ![Single Sign-on 구성](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_url1.png)

    <span data-ttu-id="7a97d-162">a.</span><span class="sxs-lookup"><span data-stu-id="7a97d-162">a.</span></span> <span data-ttu-id="7a97d-163">Hello 클릭 **고급 URL 설정 표시**합니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-163">Click hello **Show advanced URL settings**.</span></span>

    <span data-ttu-id="7a97d-164">b.</span><span class="sxs-lookup"><span data-stu-id="7a97d-164">b.</span></span> <span data-ttu-id="7a97d-165">Hello에 **로그온 URL** textbox로 hello URL 입력:`https://www.hightail.com/loginSSO`</span><span class="sxs-lookup"><span data-stu-id="7a97d-165">In hello **Sign On URL** textbox, type hello URL as: `https://www.hightail.com/loginSSO`</span></span>

4. <span data-ttu-id="7a97d-166">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **인증서 (Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-166">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_certificate.png) 

5. <span data-ttu-id="7a97d-168">Hightail 응용 프로그램에는 특정 형식의 hello SAML 어설션 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-168">Hightail application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="7a97d-169">이 응용 프로그램에 대 한 클레임을 따라 hello를 구성 하십시오.</span><span class="sxs-lookup"><span data-stu-id="7a97d-169">Please configure hello following claims for this application.</span></span> <span data-ttu-id="7a97d-170">Hello에서 이러한 특성의 hello 값을 관리할 수 있습니다 **"특성"** hello 응용 프로그램을 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-170">You can manage hello values of these attributes from hello **"Atrribute"** tab of hello application.</span></span> <span data-ttu-id="7a97d-171">다음 스크린 샷 hello이에 대 한 예가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-171">hello following screenshot shows an example for this.</span></span> 

    ![Single Sign-on 구성](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_attribute.png) 

6. <span data-ttu-id="7a97d-173">Hello에 **사용자 특성** hello 섹션 **Single sign on** 대화 상자에서 hello 이미지에 나와 있는 것 처럼 SAML 토큰 특성을 구성 하 고 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-173">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="7a97d-174">특성 이름</span><span class="sxs-lookup"><span data-stu-id="7a97d-174">Attribute Name</span></span> | <span data-ttu-id="7a97d-175">특성 값</span><span class="sxs-lookup"><span data-stu-id="7a97d-175">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="7a97d-176">FirstName</span><span class="sxs-lookup"><span data-stu-id="7a97d-176">FirstName</span></span> | <span data-ttu-id="7a97d-177">user.givenname</span><span class="sxs-lookup"><span data-stu-id="7a97d-177">user.givenname</span></span> |
    | <span data-ttu-id="7a97d-178">LastName</span><span class="sxs-lookup"><span data-stu-id="7a97d-178">LastName</span></span> | <span data-ttu-id="7a97d-179">user.surname</span><span class="sxs-lookup"><span data-stu-id="7a97d-179">user.surname</span></span> |
    | <span data-ttu-id="7a97d-180">Email</span><span class="sxs-lookup"><span data-stu-id="7a97d-180">Email</span></span> | <span data-ttu-id="7a97d-181">user.mail</span><span class="sxs-lookup"><span data-stu-id="7a97d-181">user.mail</span></span> |    
    | <span data-ttu-id="7a97d-182">UserIdentity</span><span class="sxs-lookup"><span data-stu-id="7a97d-182">UserIdentity</span></span> | <span data-ttu-id="7a97d-183">user.mail</span><span class="sxs-lookup"><span data-stu-id="7a97d-183">user.mail</span></span> |
    
    <span data-ttu-id="7a97d-184">a.</span><span class="sxs-lookup"><span data-stu-id="7a97d-184">a.</span></span> <span data-ttu-id="7a97d-185">클릭 **특성 추가** tooopen hello **특성 추가** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="7a97d-185">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-hightail-tutorial/tutorial_officespace_04.png)

    ![Single Sign-on 구성](./media/active-directory-saas-hightail-tutorial/tutorial_officespace_05.png)

    <span data-ttu-id="7a97d-188">b.</span><span class="sxs-lookup"><span data-stu-id="7a97d-188">b.</span></span> <span data-ttu-id="7a97d-189">Hello에 **이름** textbox, 해당 행에 대 한 표시 형식 hello 특성 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-189">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="7a97d-190">c.</span><span class="sxs-lookup"><span data-stu-id="7a97d-190">c.</span></span> <span data-ttu-id="7a97d-191">Hello에서 **값** 목록, 해당 행에 대 한 표시 유형 hello 특성 값입니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-191">From hello **Value** list, type hello attribute value shown for that row.</span></span>

    <span data-ttu-id="7a97d-192">d.</span><span class="sxs-lookup"><span data-stu-id="7a97d-192">d.</span></span> <span data-ttu-id="7a97d-193">Hello 둡니다 **Namespace** 비어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-193">Leave hello **Namespace** blank.</span></span>
    
    <span data-ttu-id="7a97d-194">e.</span><span class="sxs-lookup"><span data-stu-id="7a97d-194">e.</span></span> <span data-ttu-id="7a97d-195">**Ok**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-195">Click **Ok**.</span></span>

7. <span data-ttu-id="7a97d-196">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-196">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-hightail-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="7a97d-198">Hello에 **Hightail 구성** 섹션에서 클릭 **Hightail 구성** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="7a97d-198">On hello **Hightail Configuration** section, click **Configure Hightail** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="7a97d-199">복사 hello **SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="7a97d-199">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_configure.png) 

    >[!NOTE] 
    ><span data-ttu-id="7a97d-201">하십시오 Hightail 응용 프로그램에서 Single Sign On hello를 구성 하기 전에 허용 목록을 Hightail와 전자 메일 도메인을이 도메인을 사용 하는 사용자가을 hello 모든 팀 Single Sign On 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-201">Before configuring hello Single Sign On at Hightail app, please white list your email domain with Hightail team so that all hello users who are using this domain can use Single Sign On functionality.</span></span>


9. <span data-ttu-id="7a97d-202">SSO 응용 프로그램에 대해 구성 된 tooget toosign에 tooyour Hightail 테 넌 트 관리자 권한으로 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-202">tooget SSO configured for your application, you need toosign-on tooyour Hightail tenant as an administrator.</span></span>
   
    <span data-ttu-id="7a97d-203">a.</span><span class="sxs-lookup"><span data-stu-id="7a97d-203">a.</span></span> <span data-ttu-id="7a97d-204">Hello 메뉴에서 hello 위에 표시를 클릭 hello **계정** 탭을 선택한 **SAML 구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-204">In hello menu on hello top, click hello **Account** tab and select **Configure SAML**.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_001.png) 

    <span data-ttu-id="7a97d-206">b.</span><span class="sxs-lookup"><span data-stu-id="7a97d-206">b.</span></span> <span data-ttu-id="7a97d-207">Hello 확인란 선택 **SAML 인증 사용**합니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-207">Select hello checkbox of **Enable SAML Authentication**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_002.png) 

    <span data-ttu-id="7a97d-209">c.</span><span class="sxs-lookup"><span data-stu-id="7a97d-209">c.</span></span> <span data-ttu-id="7a97d-210">콘텐츠를 클립보드에 복사 hello Azure 포털에서 다운로드 한 메모장에서 e-64로 인코딩된 인증서를 열고 toohello 붙여 **SAML 토큰 서명 인증서** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-210">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **SAML Token Signing Certificate** textbox.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_003.png) 

    <span data-ttu-id="7a97d-212">d.</span><span class="sxs-lookup"><span data-stu-id="7a97d-212">d.</span></span> <span data-ttu-id="7a97d-213">Hello에 **SAML 기관 (Id 공급자)** 붙여넣기 hello 값의 텍스트 상자 **SAML Single Sign-on 서비스 URL** Azure 포털에서 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-213">In hello **SAML Authority (Identity Provider)** textbox, paste hello value of **SAML Single Sign-On Service URL** copied from Azure portal.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_004.png)

    <span data-ttu-id="7a97d-215">e.</span><span class="sxs-lookup"><span data-stu-id="7a97d-215">e.</span></span> <span data-ttu-id="7a97d-216">Tooconfigure hello 응용 프로그램에 필요한 경우 **IDP 시작 모드** 선택 **"IdP (Id 공급자)에 대 한 로그를 시작한"**합니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-216">If you wish tooconfigure hello application in **IDP initiated mode** select **"Identity Provider (IdP) initiated log in"**.</span></span> <span data-ttu-id="7a97d-217">**SP 시작 모드**로 응용 프로그램을 구성하려는 경우 **"SP(서비스 공급자) 시작 로그인"**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-217">If **SP initiated mode** select **"Service Provider (SP) initiated log in"**.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_006.png)

    <span data-ttu-id="7a97d-219">f.</span><span class="sxs-lookup"><span data-stu-id="7a97d-219">f.</span></span> <span data-ttu-id="7a97d-220">인스턴스에 대 한 hello SAML 소비자 URL을 복사 하 고에 붙여 **회신 URL** 텍스트 상자로 **Hightail 도메인 및 Url** Azure 포털에서 섹션.</span><span class="sxs-lookup"><span data-stu-id="7a97d-220">Copy hello SAML consumer URL for your instance and paste it in **Reply URL** textbox in **Hightail Domain and URLs** section on Azure portal.</span></span>
    
    <span data-ttu-id="7a97d-221">g.</span><span class="sxs-lookup"><span data-stu-id="7a97d-221">g.</span></span> <span data-ttu-id="7a97d-222">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-222">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="7a97d-223">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="7a97d-223">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7a97d-224">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="7a97d-224">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7a97d-225">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7a97d-225">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7a97d-226">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="7a97d-226">Creating an Azure AD test user</span></span>
<span data-ttu-id="7a97d-227">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-227">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="7a97d-229">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="7a97d-229">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7a97d-230">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-230">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-hightail-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7a97d-232">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-232">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-hightail-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7a97d-234">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-234">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-hightail-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7a97d-236">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-236">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-hightail-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7a97d-238">a.</span><span class="sxs-lookup"><span data-stu-id="7a97d-238">a.</span></span> <span data-ttu-id="7a97d-239">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-239">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7a97d-240">b.</span><span class="sxs-lookup"><span data-stu-id="7a97d-240">b.</span></span> <span data-ttu-id="7a97d-241">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-241">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7a97d-242">c.</span><span class="sxs-lookup"><span data-stu-id="7a97d-242">c.</span></span> <span data-ttu-id="7a97d-243">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-243">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="7a97d-244">d.</span><span class="sxs-lookup"><span data-stu-id="7a97d-244">d.</span></span> <span data-ttu-id="7a97d-245">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-245">Click **Create**.</span></span>
 
### <a name="creating-a-hightail-test-user"></a><span data-ttu-id="7a97d-246">Hightail 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="7a97d-246">Creating a Hightail test user</span></span>

<span data-ttu-id="7a97d-247">hello이이 섹션의 목적은 toocreate Britta Simon Hightail에서 호출 하는 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-247">hello objective of this section is toocreate a user called Britta Simon in Hightail.</span></span> 

<span data-ttu-id="7a97d-248">이 섹션에 작업 항목이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-248">There is no action item for you in this section.</span></span> <span data-ttu-id="7a97d-249">Hightail hello 사용자 지정 클레임에 따라 적시에 사용자 프로 비전을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-249">Hightail supports just-in-time user provisioning based on hello custom claims.</span></span> <span data-ttu-id="7a97d-250">Hello 섹션에 나와 있는 것 처럼 hello 사용자 지정 클레임을 구성한 경우  **[구성 Azure AD Single Sign-on](#configuring-azure-ad-single-sign-on)**  위, 사용자가 자동으로 생성 아직 존재 하지 않는 hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-250">If you have configured hello custom claims as shown in hello section **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** above, a user is automatically created in hello application it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="7a97d-251">Toocontact hello toocreate 사용자를 수동으로 필요한 경우 필요한 [Hightail 지원 팀](mailto:support@hightail.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-251">If you need toocreate a user manually, you need toocontact hello [Hightail support team](mailto:support@hightail.com).</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="7a97d-252">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-252">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="7a97d-253">이 섹션에서는 tooHightail 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-253">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHightail.</span></span>

![사용자 할당][200] 

<span data-ttu-id="7a97d-255">**tooassign Britta Simon tooHightail hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="7a97d-255">**tooassign Britta Simon tooHightail, perform hello following steps:**</span></span>

1. <span data-ttu-id="7a97d-256">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-256">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="7a97d-258">Hello 응용 프로그램 목록에서 선택 **Hightail**합니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-258">In hello applications list, select **Hightail**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_app.png) 

3. <span data-ttu-id="7a97d-260">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-260">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="7a97d-262">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-262">Click **Add** button.</span></span> <span data-ttu-id="7a97d-263">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-263">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="7a97d-265">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-265">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7a97d-266">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-266">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7a97d-267">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-267">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7a97d-268">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="7a97d-268">Testing single sign-on</span></span>

<span data-ttu-id="7a97d-269">이 섹션의 hello 목적은 tootest 액세스 패널을 hello 사용 하 여 Azure AD single sign-on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-269">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="7a97d-270">Hello 액세스 패널에서에서 hello Hightail 타일을 클릭할 때 자동으로 로그온 tooyour Hightail 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a97d-270">When you click hello Hightail tile in hello Access Panel, you should get automatically signed-on tooyour Hightail application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="7a97d-271">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="7a97d-271">Additional resources</span></span>

* [<span data-ttu-id="7a97d-272">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="7a97d-272">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7a97d-273">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="7a97d-273">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_203.png

