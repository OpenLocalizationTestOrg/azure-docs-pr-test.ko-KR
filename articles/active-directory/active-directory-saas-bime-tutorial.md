---
title: "자습서: Bime와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 Bime 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bdcf0729-c880-4c95-b739-0f6345b17dd8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: 8f46ff1265d302ab114747b4b45227e58718166b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bime"></a><span data-ttu-id="201c4-103">자습서: Bime와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="201c4-103">Tutorial: Azure Active Directory integration with Bime</span></span>

<span data-ttu-id="201c4-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Bime를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-104">In this tutorial, you learn how to integrate Bime with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="201c4-105">Bime를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-105">Integrating Bime with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="201c4-106">Bime에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-106">You can control in Azure AD who has access to Bime</span></span>
- <span data-ttu-id="201c4-107">사용자가 해당 Azure AD 계정으로 Bime에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-107">You can enable your users to automatically get signed-on to Bime (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="201c4-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="201c4-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="201c4-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="201c4-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="201c4-110">Prerequisites</span></span>

<span data-ttu-id="201c4-111">Bime와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-111">To configure Azure AD integration with Bime, you need the following items:</span></span>

- <span data-ttu-id="201c4-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="201c4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="201c4-113">Bime Single Sign-on이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="201c4-113">A Bime single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="201c4-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="201c4-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="201c4-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="201c4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="201c4-117">Azure AD 평가판 환경이 없으면 [평가판 제품](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="201c4-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="201c4-118">Scenario description</span></span>
<span data-ttu-id="201c4-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="201c4-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="201c4-121">갤러리에서 Bime 추가</span><span class="sxs-lookup"><span data-stu-id="201c4-121">Adding Bime from the gallery</span></span>
2. <span data-ttu-id="201c4-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="201c4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bime-from-the-gallery"></a><span data-ttu-id="201c4-123">갤러리에서 Bime 추가</span><span class="sxs-lookup"><span data-stu-id="201c4-123">Adding Bime from the gallery</span></span>
<span data-ttu-id="201c4-124">Bime의 Azure AD 통합을 구성하려면 갤러리의 Bime를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-124">To configure the integration of Bime into Azure AD, you need to add Bime from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="201c4-125">**갤러리에서 Bime를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="201c4-125">**To add Bime from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="201c4-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="201c4-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="201c4-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="201c4-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="201c4-133">검색 상자 **Bime**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-133">In the search box, type **Bime**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-bime-tutorial/tutorial_bime_search.png)

5. <span data-ttu-id="201c4-135">결과 패널에서 **Bime**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-135">In the results panel, select **Bime**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-bime-tutorial/tutorial_bime_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="201c4-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="201c4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="201c4-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Bime에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-138">In this section, you configure and test Azure AD single sign-on with Bime based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="201c4-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Bime 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Bime is to a user in Azure AD.</span></span> <span data-ttu-id="201c4-140">즉, Azure AD 사용자와 Bime의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-140">In other words, a link relationship between an Azure AD user and the related user in Bime needs to be established.</span></span>

<span data-ttu-id="201c4-141">Bime에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-141">In Bime, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="201c4-142">Bime에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-142">To configure and test Azure AD single sign-on with Bime, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="201c4-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="201c4-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="201c4-145">**[Bime 테스트 사용자 만들기](#creating-a-bime-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 Bime에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-145">**[Creating a Bime test user](#creating-a-bime-test-user)** - to have a counterpart of Britta Simon in Bime that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="201c4-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="201c4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="201c4-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="201c4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="201c4-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Bime 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Bime application.</span></span>

<span data-ttu-id="201c4-150">**Bime에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="201c4-150">**To configure Azure AD single sign-on with Bime, perform the following steps:**</span></span>

1. <span data-ttu-id="201c4-151">Azure Portal의 **Bime** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-151">In the Azure portal, on the **Bime** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="201c4-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-bime-tutorial/tutorial_bime_samlbase.png)

3. <span data-ttu-id="201c4-155">**Bime 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-155">On the **Bime Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-bime-tutorial/tutorial_bime_url.png)

    <span data-ttu-id="201c4-157">a.</span><span class="sxs-lookup"><span data-stu-id="201c4-157">a.</span></span> <span data-ttu-id="201c4-158">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<tenant-name>.Bimeapp.com`</span><span class="sxs-lookup"><span data-stu-id="201c4-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.Bimeapp.com`</span></span>

    <span data-ttu-id="201c4-159">b.</span><span class="sxs-lookup"><span data-stu-id="201c4-159">b.</span></span> <span data-ttu-id="201c4-160">**식별자** 텍스트 상자에서 `https://<tenant-name>.Bimeapp.com` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenant-name>.Bimeapp.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="201c4-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-161">These values are not real.</span></span> <span data-ttu-id="201c4-162">실제 로그온 URL 및 식별자로 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="201c4-163">이러한 값을 얻으려면 [Bime 클라이언트 지원 팀](https://bime.zendesk.com/hc/categories/202604307-Support-tech-notes-and-tips-)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="201c4-163">Contact [Bime Client support team](https://bime.zendesk.com/hc/categories/202604307-Support-tech-notes-and-tips-) to get these values.</span></span> 
 
4. <span data-ttu-id="201c4-164">**SAML 서명 인증서** 섹션에서 인증서의 **지문** 값을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-164">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value from the certificate.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-bime-tutorial/tutorial_bime_certificate.png) 

5. <span data-ttu-id="201c4-166">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-166">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-bime-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="201c4-168">**Bime 구성** 섹션에서 **Bime 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-168">On the **Bime Configuration** section, click **Configure Bime** to open **Configure sign-on** window.</span></span> <span data-ttu-id="201c4-169">**빠른 참조 섹션**에서 **SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-bime-tutorial/tutorial_bime_configure.png) 

7. <span data-ttu-id="201c4-171">다른 웹 브라우저 창에서 Bime 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-171">In a different web browser window, log into your Bime company site as an administrator.</span></span>

8. <span data-ttu-id="201c4-172">도구 모음에서 **Admin**과 **계정**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-172">In the toolbar, click **Admin**, and then **Account**.</span></span>
   
    <span data-ttu-id="201c4-173">![관리자](./media/active-directory-saas-bime-tutorial/ic775558.png "관리자")</span><span class="sxs-lookup"><span data-stu-id="201c4-173">![Admin](./media/active-directory-saas-bime-tutorial/ic775558.png "Admin")</span></span>

9. <span data-ttu-id="201c4-174">계정 구성 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-174">On the account configuration page, perform the following steps:</span></span>
   
    <span data-ttu-id="201c4-175">![Single Sign-On 구성](./media/active-directory-saas-bime-tutorial/ic775559.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="201c4-175">![Configure Single Sign-On](./media/active-directory-saas-bime-tutorial/ic775559.png "Configure Single Sign-On")</span></span>
   
    <span data-ttu-id="201c4-176">a.</span><span class="sxs-lookup"><span data-stu-id="201c4-176">a.</span></span> <span data-ttu-id="201c4-177">**SAML 인증 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-177">Select **Enable SAML authentication**.</span></span>

    <span data-ttu-id="201c4-178">b.</span><span class="sxs-lookup"><span data-stu-id="201c4-178">b.</span></span> <span data-ttu-id="201c4-179">Azure Portal에서 복사한 **SAML Single Sign-On 서비스 URL** 값을 **원격 로그인 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-179">In the **Remote Login URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="201c4-180">c.</span><span class="sxs-lookup"><span data-stu-id="201c4-180">c.</span></span>  <span data-ttu-id="201c4-181">Azure Portal의 **지문** 값을 **Certificate Fingerprint**(인증서 지문) 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-181">Paste the **Thumbprint** value from Azure portal into the **Certificate Fingerprint** textbox.</span></span>       
   
    <span data-ttu-id="201c4-182">d.</span><span class="sxs-lookup"><span data-stu-id="201c4-182">d.</span></span> <span data-ttu-id="201c4-183">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-183">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="201c4-184">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-184">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="201c4-185">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-185">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="201c4-186">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-186">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="201c4-187">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="201c4-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="201c4-188">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="201c4-190">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="201c4-190">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="201c4-191">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-191">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-bime-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="201c4-193">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-193">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-bime-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="201c4-195">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-195">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-bime-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="201c4-197">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-197">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-bime-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="201c4-199">a.</span><span class="sxs-lookup"><span data-stu-id="201c4-199">a.</span></span> <span data-ttu-id="201c4-200">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-200">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="201c4-201">b.</span><span class="sxs-lookup"><span data-stu-id="201c4-201">b.</span></span> <span data-ttu-id="201c4-202">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-202">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="201c4-203">c.</span><span class="sxs-lookup"><span data-stu-id="201c4-203">c.</span></span> <span data-ttu-id="201c4-204">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-204">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="201c4-205">d.</span><span class="sxs-lookup"><span data-stu-id="201c4-205">d.</span></span> <span data-ttu-id="201c4-206">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-206">Click **Create**.</span></span>
 
### <a name="creating-a-bime-test-user"></a><span data-ttu-id="201c4-207">Bime 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="201c4-207">Creating a Bime test user</span></span>

<span data-ttu-id="201c4-208">Azure AD 사용자가 Bime에 로그인할 수 있도록 하려면 Bime로 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-208">In order to enable Azure AD users to log in to Bime, they must be provisioned into Bime.</span></span> <span data-ttu-id="201c4-209">Bime의 경우 프로비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-209">In the case of Bime, provisioning is a manual task.</span></span>

<span data-ttu-id="201c4-210">**사용자 프로비전을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="201c4-210">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="201c4-211">**Bime** 테넌트에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-211">Log in to your **Bime** tenant.</span></span>

2. <span data-ttu-id="201c4-212">도구 모음에서 **관리자**와 **사용자**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-212">In the toolbar, click **Admin**, and then **Users**.</span></span>
   
    <span data-ttu-id="201c4-213">![관리자](./media/active-directory-saas-bime-tutorial/ic775561.png "관리자")</span><span class="sxs-lookup"><span data-stu-id="201c4-213">![Admin](./media/active-directory-saas-bime-tutorial/ic775561.png "Admin")</span></span>

3. <span data-ttu-id="201c4-214">**사용자 목록**에서 **새 사용자 추가**("+")를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-214">In the **Users List**, click **Add New User** (“+”).</span></span>
   
    <span data-ttu-id="201c4-215">![사용자](./media/active-directory-saas-bime-tutorial/ic775562.png "사용자")</span><span class="sxs-lookup"><span data-stu-id="201c4-215">![Users](./media/active-directory-saas-bime-tutorial/ic775562.png "Users")</span></span>

4. <span data-ttu-id="201c4-216">**사용자 세부 정보** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-216">On the **User Details** dialog page, perform the following steps:</span></span>
   
    <span data-ttu-id="201c4-217">![사용자 세부 정보](./media/active-directory-saas-bime-tutorial/ic775563.png "사용자 세부 정보")</span><span class="sxs-lookup"><span data-stu-id="201c4-217">![User Details](./media/active-directory-saas-bime-tutorial/ic775563.png "User Details")</span></span>
   
    <span data-ttu-id="201c4-218">a.</span><span class="sxs-lookup"><span data-stu-id="201c4-218">a.</span></span> <span data-ttu-id="201c4-219">**이름** 텍스트 상자에 사용자의 이름(예: **Britta**)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-219">In the **First name** textbox, enter the first name of user like **Britta**.</span></span>

    <span data-ttu-id="201c4-220">b.</span><span class="sxs-lookup"><span data-stu-id="201c4-220">b.</span></span> <span data-ttu-id="201c4-221">**성** 텍스트 상자에 사용자의 성(예: **Simon**)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-221">In the **Last name** textbox, enter the last name of user like **Simon**.</span></span>
 
    <span data-ttu-id="201c4-222">c.</span><span class="sxs-lookup"><span data-stu-id="201c4-222">c.</span></span> <span data-ttu-id="201c4-223">**메일** 텍스트 상자에 **brittasimon@contoso.com**과 같은 사용자의 메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-223">In the **Email** textbox, enter the email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="201c4-224">d.</span><span class="sxs-lookup"><span data-stu-id="201c4-224">d.</span></span> <span data-ttu-id="201c4-225">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-225">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="201c4-226">다른 Bime 사용자 계정 생성 도구 또는 Bime이 제공한 API를 사용하여 AAD 사용자 계정을 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-226">You can use any other Bime user account creation tools or APIs provided by Bime to provision AAD user accounts.</span></span>
>  

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="201c4-227">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="201c4-227">Assigning the Azure AD test user</span></span>

<span data-ttu-id="201c4-228">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Bime에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-228">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Bime.</span></span>

![사용자 할당][200] 

<span data-ttu-id="201c4-230">**Britta Simon을 Bime에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="201c4-230">**To assign Britta Simon to Bime, perform the following steps:**</span></span>

1. <span data-ttu-id="201c4-231">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-231">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="201c4-233">응용 프로그램 목록에서 **Bime**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-233">In the applications list, select **Bime**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-bime-tutorial/tutorial_bime_app.png) 

3. <span data-ttu-id="201c4-235">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-235">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="201c4-237">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-237">Click **Add** button.</span></span> <span data-ttu-id="201c4-238">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="201c4-240">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-240">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="201c4-241">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="201c4-242">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="201c4-243">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="201c4-243">Testing single sign-on</span></span>

<span data-ttu-id="201c4-244">이 섹션은 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-244">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="201c4-245">액세스 패널에서 Bime 타일을 클릭하면 Bime 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="201c4-245">When you click the Bime tile in the Access Panel, you should get automatically signed-on to your Bime application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="201c4-246">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="201c4-246">Additional resources</span></span>

* [<span data-ttu-id="201c4-247">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="201c4-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="201c4-248">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="201c4-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bime-tutorial/tutorial_general_203.png

