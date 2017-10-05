---
title: "자습서: Origami Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 Origami 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a28bb0ba-b564-46ba-accc-e587699295d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 3420409b72ff032e64ac59365083dd141dfc3c1b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-origami"></a><span data-ttu-id="3744a-103">자습서: Azure Active Directory와 Origami 통합</span><span class="sxs-lookup"><span data-stu-id="3744a-103">Tutorial: Azure Active Directory integration with Origami</span></span>

<span data-ttu-id="3744a-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Origami를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-104">In this tutorial, you learn how to integrate Origami with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3744a-105">Origami를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-105">Integrating Origami with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3744a-106">Origami에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-106">You can control in Azure AD who has access to Origami</span></span>
- <span data-ttu-id="3744a-107">사용자가 해당 Azure AD 계정으로 Origami에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-107">You can enable your users to automatically get signed-on to Origami (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3744a-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="3744a-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3744a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3744a-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="3744a-110">Prerequisites</span></span>

<span data-ttu-id="3744a-111">Origami와의 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-111">To configure Azure AD integration with Origami, you need the following items:</span></span>

- <span data-ttu-id="3744a-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="3744a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3744a-113">Origami Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="3744a-113">An Origami single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3744a-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3744a-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3744a-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="3744a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3744a-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3744a-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="3744a-118">Scenario description</span></span>
<span data-ttu-id="3744a-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3744a-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3744a-121">갤러리에서 Origami 추가</span><span class="sxs-lookup"><span data-stu-id="3744a-121">Adding Origami from the gallery</span></span>
2. <span data-ttu-id="3744a-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="3744a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-origami-from-the-gallery"></a><span data-ttu-id="3744a-123">갤러리에서 Origami 추가</span><span class="sxs-lookup"><span data-stu-id="3744a-123">Adding Origami from the gallery</span></span>
<span data-ttu-id="3744a-124">Origami의 Azure AD 통합을 구성하려면 갤러리의 Origami를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-124">To configure the integration of Origami into Azure AD, you need to add Origami from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3744a-125">**갤러리에서 Origami를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="3744a-125">**To add Origami from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3744a-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3744a-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3744a-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="3744a-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="3744a-133">검색 상자에 **Origami**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-133">In the search box, type **Origami**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-origami-tutorial/tutorial_origami_search.png)

5. <span data-ttu-id="3744a-135">결과 패널에서 **Origami**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-135">In the results panel, select **Origami**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-origami-tutorial/tutorial_origami_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3744a-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="3744a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3744a-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Origami에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-138">In this section, you configure and test Azure AD single sign-on with Origami based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3744a-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Origami 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Origami is to a user in Azure AD.</span></span> <span data-ttu-id="3744a-140">즉, Azure AD 사용자와 Origami의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-140">In other words, a link relationship between an Azure AD user and the related user in Origami needs to be established.</span></span>

<span data-ttu-id="3744a-141">Origami에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-141">In Origami, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="3744a-142">Origami에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-142">To configure and test Azure AD single sign-on with Origami, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3744a-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3744a-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3744a-145">**[Origami 테스트 사용자 만들기](#creating-an-origami-test-user)** - Britta Simon의 Azure AD 표현과 연결되는 대응 사용자를 Origami에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-145">**[Creating an Origami test user](#creating-an-origami-test-user)** - to have a counterpart of Britta Simon in Origami that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3744a-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3744a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3744a-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="3744a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3744a-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Origami 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Origami application.</span></span>

<span data-ttu-id="3744a-150">**Origami에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="3744a-150">**To configure Azure AD single sign-on with Origami, perform the following steps:**</span></span>

1. <span data-ttu-id="3744a-151">Azure Portal의 **Origami** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-151">In the Azure portal, on the **Origami** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="3744a-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-origami-tutorial/tutorial_origami_samlbase.png)

3. <span data-ttu-id="3744a-155">**Origami 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-155">On the **Origami Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-origami-tutorial/tutorial_origami_url.png)

    <span data-ttu-id="3744a-157">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://live.origamirisk.com/origami/account/login?account=<companyname>`</span><span class="sxs-lookup"><span data-stu-id="3744a-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://live.origamirisk.com/origami/account/login?account=<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3744a-158">이 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-158">The value is not real.</span></span> <span data-ttu-id="3744a-159">이 값을 실제 로그온 URL로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="3744a-160">값을 얻으려면 [Origami 클라이언트 지원 팀](https://wordpress.org/support/theme/origami)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="3744a-160">Contact [Origami Client support team](https://wordpress.org/support/theme/origami) to get the value.</span></span> 
 
4. <span data-ttu-id="3744a-161">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-origami-tutorial/tutorial_origami_certificate.png) 

5. <span data-ttu-id="3744a-163">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-163">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-origami-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3744a-165">**Origami 구성** 섹션에서 **Origami 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-165">On the **Origami Configuration** section, click **Configure Origami** to open **Configure sign-on** window.</span></span> <span data-ttu-id="3744a-166">**빠른 참조 섹션**에서 **로그아웃 URL 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-166">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-origami-tutorial/tutorial_origami_configure.png) 

7. <span data-ttu-id="3744a-168">관리자 권한이 있는 Origami 계정으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-168">Log in to the Origami account with Admin rights.</span></span>

8. <span data-ttu-id="3744a-169">위쪽의 메뉴에서 **관리자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-169">In the menu on the top, click **Admin**.</span></span>
   
    ![Single Sign-On 구성](./media/active-directory-saas-origami-tutorial/tutorial_origami_51.png)

9. <span data-ttu-id="3744a-171">Single Sign-On 설정 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-171">On the Single Sign On Setup dialog page, perform the following steps:</span></span>
   
    ![Single Sign-On 구성](./media/active-directory-saas-origami-tutorial/tutorial_origami_531.png)

    <span data-ttu-id="3744a-173">a.</span><span class="sxs-lookup"><span data-stu-id="3744a-173">a.</span></span> <span data-ttu-id="3744a-174">**Single Sign-On 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-174">Select **Enable Single Sign On**.</span></span>

    <span data-ttu-id="3744a-175">b.</span><span class="sxs-lookup"><span data-stu-id="3744a-175">b.</span></span> <span data-ttu-id="3744a-176">Azure Portal에서 복사한 **SAML Single Sign-On 서비스 URL** 값을 **ID 공급자 로그인 페이지 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-176">In the **Identity Provider's Sign-in Page URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="3744a-177">c.</span><span class="sxs-lookup"><span data-stu-id="3744a-177">c.</span></span> <span data-ttu-id="3744a-178">Azure Portal에서 복사한 **로그아웃 URL** 값을 **ID 공급자 로그아웃 페이지 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-178">In the **Identity Provider's Sign-out Page URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="3744a-179">d.</span><span class="sxs-lookup"><span data-stu-id="3744a-179">d.</span></span> <span data-ttu-id="3744a-180">**찾아보기**를 클릭하여 Azure Portal에서 다운로드한 인증서를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-180">Click **Browse** to upload the certificate you have downloaded from the Azure portal.</span></span>

    <span data-ttu-id="3744a-181">e.</span><span class="sxs-lookup"><span data-stu-id="3744a-181">e.</span></span> <span data-ttu-id="3744a-182">**변경 내용 저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-182">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="3744a-183">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-183">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3744a-184">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-184">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3744a-185">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-185">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3744a-186">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="3744a-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="3744a-187">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="3744a-189">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="3744a-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3744a-190">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-190">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-origami-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3744a-192">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-192">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-origami-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3744a-194">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-194">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-origami-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3744a-196">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-196">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-origami-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3744a-198">a.</span><span class="sxs-lookup"><span data-stu-id="3744a-198">a.</span></span> <span data-ttu-id="3744a-199">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-199">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3744a-200">b.</span><span class="sxs-lookup"><span data-stu-id="3744a-200">b.</span></span> <span data-ttu-id="3744a-201">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3744a-202">c.</span><span class="sxs-lookup"><span data-stu-id="3744a-202">c.</span></span> <span data-ttu-id="3744a-203">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-203">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="3744a-204">d.</span><span class="sxs-lookup"><span data-stu-id="3744a-204">d.</span></span> <span data-ttu-id="3744a-205">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-205">Click **Create**.</span></span>
 
### <a name="creating-an-origami-test-user"></a><span data-ttu-id="3744a-206">Origami 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="3744a-206">Creating an Origami test user</span></span>

<span data-ttu-id="3744a-207">이 섹션에서는 Origami에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-207">In this section, you create a user called Britta Simon in Origami.</span></span> 

1. <span data-ttu-id="3744a-208">관리자 권한이 있는 Origami 계정으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-208">Log in to the Origami account with Admin rights.</span></span>

2. <span data-ttu-id="3744a-209">위쪽의 메뉴에서 **관리자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-209">In the menu on the top, click **Admin**.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-origami-tutorial/tutorial_origami_51.png)

3. <span data-ttu-id="3744a-211">**사용자 및 보안** 대화 상자에서 **사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-211">On the **Users and Security** dialog, click **Users**.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-origami-tutorial/tutorial_origami_54.png)

4. <span data-ttu-id="3744a-213">**새 사용자 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-213">Click **Add New User**.</span></span>
   
    ![Single Sign-On 구성](./media/active-directory-saas-origami-tutorial/tutorial_origami_55.png)

5. <span data-ttu-id="3744a-215">새 사용자 추가 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-215">On the Add New User dialog, perform the following steps:</span></span>
   
    ![Single Sign-On 구성](./media/active-directory-saas-origami-tutorial/tutorial_origami_56.png)

    <span data-ttu-id="3744a-217">a.</span><span class="sxs-lookup"><span data-stu-id="3744a-217">a.</span></span> <span data-ttu-id="3744a-218">**사용자 이름** 텍스트 상자에 사용자의 메일(예: **brittasimon@contoso.com**)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-218">In the **User Name** textbox, enter the email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="3744a-219">b.</span><span class="sxs-lookup"><span data-stu-id="3744a-219">b.</span></span> <span data-ttu-id="3744a-220">**암호** 텍스트 상자에 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-220">In the **Password** textbox, type a password.</span></span>

    <span data-ttu-id="3744a-221">c.</span><span class="sxs-lookup"><span data-stu-id="3744a-221">c.</span></span> <span data-ttu-id="3744a-222">**암호 확인** 텍스트 상자에 암호를 다시 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-222">In the **Confirm Password** textbox, type the password again.</span></span>

    <span data-ttu-id="3744a-223">d.</span><span class="sxs-lookup"><span data-stu-id="3744a-223">d.</span></span> <span data-ttu-id="3744a-224">**이름** 텍스트 상자에 사용자의 이름(예: **Britta**)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-224">In the **First Name** textbox, enter the first name of user like **Britta**.</span></span>

    <span data-ttu-id="3744a-225">e.</span><span class="sxs-lookup"><span data-stu-id="3744a-225">e.</span></span> <span data-ttu-id="3744a-226">**성** 텍스트 상자에 사용자의 성(예: **Simon**)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-226">In the **Last Name** textbox, enter the last name of user like **Simon**.</span></span>

    <span data-ttu-id="3744a-227">f.</span><span class="sxs-lookup"><span data-stu-id="3744a-227">f.</span></span> <span data-ttu-id="3744a-228">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-228">Click **Save**.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-origami-tutorial/tutorial_origami_57.png)

6. <span data-ttu-id="3744a-230">사용자에게 **사용자 역할** 및 **클라이언트 액세스**를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-230">Assign **User Roles** and **Client Access** to the user.</span></span> 
   
    ![Single Sign-on 구성](./media/active-directory-saas-origami-tutorial/tutorial_origami_58.png)

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="3744a-232">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="3744a-232">Assigning the Azure AD test user</span></span>

<span data-ttu-id="3744a-233">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Origami에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-233">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Origami.</span></span>

![사용자 할당][200] 

<span data-ttu-id="3744a-235">**Britta Simon을 Origami에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="3744a-235">**To assign Britta Simon to Origami, perform the following steps:**</span></span>

1. <span data-ttu-id="3744a-236">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-236">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="3744a-238">응용 프로그램 목록에서 **Origami**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-238">In the applications list, select **Origami**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-origami-tutorial/tutorial_origami_app.png) 

3. <span data-ttu-id="3744a-240">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-240">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="3744a-242">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-242">Click **Add** button.</span></span> <span data-ttu-id="3744a-243">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="3744a-245">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-245">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3744a-246">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3744a-247">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3744a-248">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="3744a-248">Testing single sign-on</span></span>

<span data-ttu-id="3744a-249">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-249">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="3744a-250">액세스 패널에서 Origami 타일을 클릭하면 Origami 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="3744a-250">When you click the Origami tile in the Access Panel, you should get automatically signed-on to your Origami application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3744a-251">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="3744a-251">Additional resources</span></span>

* [<span data-ttu-id="3744a-252">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="3744a-252">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3744a-253">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="3744a-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-origami-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-origami-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-origami-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-origami-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-origami-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-origami-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-origami-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-origami-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-origami-tutorial/tutorial_general_203.png

