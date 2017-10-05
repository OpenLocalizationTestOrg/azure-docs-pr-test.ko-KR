---
title: "자습서: Panorama9와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 Panorama9 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5e28d7fa-03be-49f3-96c8-b567f1257d44
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 934c0743464fd32398071aa3d07f7af76fdf7e3b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-panorama9"></a><span data-ttu-id="a5ba3-103">자습서: Panorama9와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="a5ba3-103">Tutorial: Azure Active Directory integration with Panorama9</span></span>

<span data-ttu-id="a5ba3-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Panorama9를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-104">In this tutorial, you learn how to integrate Panorama9 with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a5ba3-105">Panorama9를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-105">Integrating Panorama9 with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a5ba3-106">Panorama9에 액세스할 수 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-106">You can control in Azure AD who has access to Panorama9</span></span>
- <span data-ttu-id="a5ba3-107">사용자가 자신의 Azure AD 계정으로 Panorama9에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-107">You can enable your users to automatically get signed-on to Panorama9 (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a5ba3-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a5ba3-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a5ba3-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="a5ba3-110">Prerequisites</span></span>

<span data-ttu-id="a5ba3-111">Panorama9와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-111">To configure Azure AD integration with Panorama9, you need the following items:</span></span>

- <span data-ttu-id="a5ba3-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="a5ba3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a5ba3-113">Panorama9 Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="a5ba3-113">A Panorama9 single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a5ba3-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a5ba3-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a5ba3-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a5ba3-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a5ba3-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="a5ba3-118">Scenario description</span></span>
<span data-ttu-id="a5ba3-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a5ba3-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a5ba3-121">갤러리에서 Panorama9 추가</span><span class="sxs-lookup"><span data-stu-id="a5ba3-121">Adding Panorama9 from the gallery</span></span>
2. <span data-ttu-id="a5ba3-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="a5ba3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-panorama9-from-the-gallery"></a><span data-ttu-id="a5ba3-123">갤러리에서 Panorama9 추가</span><span class="sxs-lookup"><span data-stu-id="a5ba3-123">Adding Panorama9 from the gallery</span></span>
<span data-ttu-id="a5ba3-124">Panorama9가 Azure AD에 통합되도록 구성하려면 갤러리의 Panorama9를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-124">To configure the integration of Panorama9 into Azure AD, you need to add Panorama9 from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a5ba3-125">**갤러리에서 Panorama9를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="a5ba3-125">**To add Panorama9 from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a5ba3-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a5ba3-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a5ba3-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="a5ba3-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="a5ba3-133">검색 상자에 **Panorama9**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-133">In the search box, type **Panorama9**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_search.png)

5. <span data-ttu-id="a5ba3-135">결과 패널에서 **Panorama9**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-135">In the results panel, select **Panorama9**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a5ba3-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="a5ba3-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="a5ba3-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 사용하여 Panorama9에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-138">In this section, you configure and test Azure AD single sign-on with Panorama9 based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a5ba3-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Panorama9 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Panorama9 is to a user in Azure AD.</span></span> <span data-ttu-id="a5ba3-140">즉, Azure AD 사용자와 Panorama9의 관련 사용자 간에 연결 관계를 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-140">In other words, a link relationship between an Azure AD user and the related user in Panorama9 needs to be established.</span></span>

<span data-ttu-id="a5ba3-141">Panorama9에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 연결 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-141">In Panorama9, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a5ba3-142">Panorama9에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-142">To configure and test Azure AD single sign-on with Panorama9, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a5ba3-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a5ba3-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a5ba3-145">**[Panorama9 테스트 사용자 만들기](#creating-a-panorama9-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 Panorama9에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-145">**[Creating a Panorama9 test user](#creating-a-panorama9-test-user)** - to have a counterpart of Britta Simon in Panorama9 that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a5ba3-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a5ba3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a5ba3-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="a5ba3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a5ba3-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Panorama9 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Panorama9 application.</span></span>

<span data-ttu-id="a5ba3-150">**Panorama9에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="a5ba3-150">**To configure Azure AD single sign-on with Panorama9, perform the following steps:**</span></span>

1. <span data-ttu-id="a5ba3-151">Azure Portal의 **Panorama9** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-151">In the Azure portal, on the **Panorama9** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="a5ba3-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_samlbase.png)

3. <span data-ttu-id="a5ba3-155">**Panorama9 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-155">On the **Panorama9 Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_url.png)

    <span data-ttu-id="a5ba3-157">a.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-157">a.</span></span> <span data-ttu-id="a5ba3-158">**로그온 URL** 텍스트 상자에 URL을 입력합니다. `https://dashboard.panorama9.com/saml/access/3262`</span><span class="sxs-lookup"><span data-stu-id="a5ba3-158">In the **Sign-on URL** textbox, type a URL as: `https://dashboard.panorama9.com/saml/access/3262`</span></span>

    <span data-ttu-id="a5ba3-159">b.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-159">b.</span></span> <span data-ttu-id="a5ba3-160">**식별자** 텍스트 상자에서 `http://www.panorama9.com/saml20/<tenant-name>` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-160">In the **Identifier** textbox, type a URL using the following pattern: `http://www.panorama9.com/saml20/<tenant-name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a5ba3-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-161">These values are not real.</span></span> <span data-ttu-id="a5ba3-162">실제 로그온 URL 및 식별자로 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="a5ba3-163">이러한 값을 얻으려면 [Panorama9 클라이언트 지원 팀](https://support.panorama9.com)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-163">Contact [Panorama9 Client support team](https://support.panorama9.com) to get these values.</span></span> 
 
4. <span data-ttu-id="a5ba3-164">**SAML 서명 인증서** 섹션에서 인증서의 **지문** 값을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-164">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_certificate.png) 

5. <span data-ttu-id="a5ba3-166">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-166">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-panorama9-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a5ba3-168">**Panorama9 구성** 섹션에서 **Panorama9 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-168">On the **Panorama9 Configuration** section, click **Configure Panorama9** to open **Configure sign-on** window.</span></span> <span data-ttu-id="a5ba3-169">**빠른 참조 섹션**에서 **SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_configure.png) 

5. <span data-ttu-id="a5ba3-171">다른 웹 브라우저 창에서 Panorama9 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-171">In a different web browser window, log into your Panorama9 company site as an administrator.</span></span>

6. <span data-ttu-id="a5ba3-172">위쪽의 도구 모음에서 **관리**를 클릭한 다음 **확장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-172">In the toolbar on the top, click **Manage**, and then click **Extensions**.</span></span>
   
   <span data-ttu-id="a5ba3-173">![확장](./media/active-directory-saas-panorama9-tutorial/ic790023.png "확장")</span><span class="sxs-lookup"><span data-stu-id="a5ba3-173">![Extensions](./media/active-directory-saas-panorama9-tutorial/ic790023.png "Extensions")</span></span>
7. <span data-ttu-id="a5ba3-174">**확장** 대화 상자에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-174">On the **Extensions** dialog, click **Single Sign-On**.</span></span>
   
   <span data-ttu-id="a5ba3-175">![Single Sign-On](./media/active-directory-saas-panorama9-tutorial/ic790024.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="a5ba3-175">![Single Sign-On](./media/active-directory-saas-panorama9-tutorial/ic790024.png "Single Sign-On")</span></span>
8. <span data-ttu-id="a5ba3-176">**설정** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-176">In the **Settings** section, perform the following steps:</span></span>
   
   <span data-ttu-id="a5ba3-177">![설정](./media/active-directory-saas-panorama9-tutorial/ic790025.png "설정")</span><span class="sxs-lookup"><span data-stu-id="a5ba3-177">![Settings](./media/active-directory-saas-panorama9-tutorial/ic790025.png "Settings")</span></span>
   
    <span data-ttu-id="a5ba3-178">a.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-178">a.</span></span> <span data-ttu-id="a5ba3-179">Azure Portal에서 복사한 **Single Sign-On 서비스 URL** 값을 **Identity provider URL**(ID 공급자 URL) 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-179">In **Identity provider URL** textbox, paste the value of **Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="a5ba3-180">b.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-180">b.</span></span> <span data-ttu-id="a5ba3-181">Azure Portal에서 복사한 인증서의 **지문** 값을 **Certificate fingerprint**(인증서 지문) 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-181">In **Certificate fingerprint** textbox, paste the **Thumbprint** value of certificate, which you have copied from Azure portal.</span></span>    
         
9. <span data-ttu-id="a5ba3-182">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-182">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="a5ba3-183">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-183">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a5ba3-184">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-184">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a5ba3-185">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-185">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a5ba3-186">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="a5ba3-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="a5ba3-187">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="a5ba3-189">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="a5ba3-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a5ba3-190">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-190">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-panorama9-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a5ba3-192">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-192">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-panorama9-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a5ba3-194">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-194">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-panorama9-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a5ba3-196">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-196">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-panorama9-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a5ba3-198">a.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-198">a.</span></span> <span data-ttu-id="a5ba3-199">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-199">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a5ba3-200">b.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-200">b.</span></span> <span data-ttu-id="a5ba3-201">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a5ba3-202">c.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-202">c.</span></span> <span data-ttu-id="a5ba3-203">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-203">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a5ba3-204">d.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-204">d.</span></span> <span data-ttu-id="a5ba3-205">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-205">Click **Create**.</span></span>
 
### <a name="creating-a-panorama9-test-user"></a><span data-ttu-id="a5ba3-206">Panorama9 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="a5ba3-206">Creating a Panorama9 test user</span></span>

<span data-ttu-id="a5ba3-207">Azure AD 사용자가 Panorama9에 로그인할 수 있도록 하려면 Panorama9로 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-207">In order to enable Azure AD users to log into Panorama9, they must be provisioned into Panorama9.</span></span>  

<span data-ttu-id="a5ba3-208">Panorama9의 경우 프로비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-208">In the case of Panorama9, provisioning is a manual task.</span></span>

<span data-ttu-id="a5ba3-209">**사용자 프로비전을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="a5ba3-209">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="a5ba3-210">**Panorama9** 회사 사이트에 관리자 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-210">Log in to your **Panorama9** company site as an administrator.</span></span>

2. <span data-ttu-id="a5ba3-211">위쪽 메뉴에서 **관리**를 클릭한 다음 **사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-211">In the menu on the top, click **Manage**, and then click **Users**.</span></span>
   
  <span data-ttu-id="a5ba3-212">![사용자](./media/active-directory-saas-panorama9-tutorial/ic790027.png "사용자")</span><span class="sxs-lookup"><span data-stu-id="a5ba3-212">![Users](./media/active-directory-saas-panorama9-tutorial/ic790027.png "Users")</span></span>

3. <span data-ttu-id="a5ba3-213">[사용자] 섹션에서 **+**를 클릭하여 새 사용자를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-213">In the Users section, Click **+** to add new user.</span></span>

 <span data-ttu-id="a5ba3-214">![사용자](./media/active-directory-saas-panorama9-tutorial/ic790028.png "사용자")</span><span class="sxs-lookup"><span data-stu-id="a5ba3-214">![Users](./media/active-directory-saas-panorama9-tutorial/ic790028.png "Users")</span></span>

4. <span data-ttu-id="a5ba3-215">[사용자 데이터] 섹션으로 이동하고 프로비전할 유효한 Azure Active Directory 사용자의 메일 주소를 **메일** 텍스트 상자에 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-215">Go to the User data section, type the email address of a valid Azure Active Directory user you want to provision into the **Email** textbox.</span></span>

5. <span data-ttu-id="a5ba3-216">[사용자] 섹션으로 이동하여 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-216">Come to the Users section, Click **Save**.</span></span>
   
> [!NOTE]
    > <span data-ttu-id="a5ba3-217">Azure Active Directory 계정 보유자는 활성화되기 전에 메일을 받고 링크를 따라 계정을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-217">The Azure Active Directory account holder receives an email and follows a link to confirm their account before it becomes active.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a5ba3-218">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="a5ba3-218">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a5ba3-219">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Panorama9에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-219">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Panorama9.</span></span>

![사용자 할당][200] 

<span data-ttu-id="a5ba3-221">**Britta Simon을 Panorama9에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="a5ba3-221">**To assign Britta Simon to Panorama9, perform the following steps:**</span></span>

1. <span data-ttu-id="a5ba3-222">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-222">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="a5ba3-224">응용 프로그램 목록에서 **Panorama9**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-224">In the applications list, select **Panorama9**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_app.png) 

3. <span data-ttu-id="a5ba3-226">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-226">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="a5ba3-228">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-228">Click **Add** button.</span></span> <span data-ttu-id="a5ba3-229">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="a5ba3-231">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-231">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a5ba3-232">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a5ba3-233">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a5ba3-234">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="a5ba3-234">Testing single sign-on</span></span>

<span data-ttu-id="a5ba3-235">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-235">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a5ba3-236">액세스 패널에서 Panorama9 타일을 클릭하면 Panorama9 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-236">When you click the Panorama9 tile in the Access Panel, you should get automatically signed-on to Panorama9 application.</span></span>
<span data-ttu-id="a5ba3-237">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a5ba3-237">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a5ba3-238">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="a5ba3-238">Additional resources</span></span>

* [<span data-ttu-id="a5ba3-239">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="a5ba3-239">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a5ba3-240">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="a5ba3-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_203.png

