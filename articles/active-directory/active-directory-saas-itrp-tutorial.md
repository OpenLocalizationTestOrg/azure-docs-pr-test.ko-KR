---
title: "자습서: ITRP와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 ITRP 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e09716a3-4200-4853-9414-2390e6c10d98
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: fae1c7b6b0e04c1e23123d3aee7913cb3131e645
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-itrp"></a><span data-ttu-id="db701-103">자습서: ITRP와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="db701-103">Tutorial: Azure Active Directory integration with ITRP</span></span>

<span data-ttu-id="db701-104">이 자습서에서는 Azure AD(Azure Active Directory)와 ITRP를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="db701-104">In this tutorial, you learn how to integrate ITRP with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="db701-105">ITRP를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="db701-105">Integrating ITRP with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="db701-106">ITRP에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db701-106">You can control in Azure AD who has access to ITRP</span></span>
- <span data-ttu-id="db701-107">사용자가 해당 Azure AD 계정으로 ITRP에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db701-107">You can enable your users to automatically get signed-on to ITRP (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="db701-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db701-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="db701-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="db701-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="db701-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="db701-110">Prerequisites</span></span>

<span data-ttu-id="db701-111">ITRP와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="db701-111">To configure Azure AD integration with ITRP, you need the following items:</span></span>

- <span data-ttu-id="db701-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="db701-112">An Azure AD subscription</span></span>
- <span data-ttu-id="db701-113">ITRP Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="db701-113">An ITRP single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="db701-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="db701-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="db701-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db701-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="db701-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="db701-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="db701-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db701-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="db701-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="db701-118">Scenario description</span></span>
<span data-ttu-id="db701-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="db701-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="db701-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db701-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="db701-121">갤러리에서 ITRP 추가</span><span class="sxs-lookup"><span data-stu-id="db701-121">Adding ITRP from the gallery</span></span>
2. <span data-ttu-id="db701-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="db701-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-itrp-from-the-gallery"></a><span data-ttu-id="db701-123">갤러리에서 ITRP 추가</span><span class="sxs-lookup"><span data-stu-id="db701-123">Adding ITRP from the gallery</span></span>
<span data-ttu-id="db701-124">ITRP의 Azure AD 통합을 구성하려면 갤러리의 ITRP를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db701-124">To configure the integration of ITRP in to Azure AD, you need to add ITRP from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="db701-125">**갤러리에서 ITRP를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="db701-125">**To add ITRP from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="db701-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db701-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="db701-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="db701-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="db701-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="db701-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="db701-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db701-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="db701-133">검색 상자에 **ITRP**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="db701-133">In the search box, type **ITRP**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_search.png)

5. <span data-ttu-id="db701-135">결과 패널에서 **ITRP**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="db701-135">In the results panel, select **ITRP**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="db701-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="db701-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="db701-138">이 섹션에서는 “Britta Simon”이라는 테스트 사용자를 기반으로 ITRP에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="db701-138">In this section, you configure and test Azure AD single sign-on with ITRP based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="db701-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 ITRP 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db701-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ITRP is to a user in Azure AD.</span></span> <span data-ttu-id="db701-140">즉, Azure AD 사용자와 ITRP의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db701-140">In other words, a link relationship between an Azure AD user and the related user in ITRP needs to be established.</span></span>

<span data-ttu-id="db701-141">ITRP에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="db701-141">In ITRP, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="db701-142">ITRP에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db701-142">To configure and test Azure AD single sign-on with ITRP, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="db701-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="db701-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="db701-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="db701-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="db701-145">**[ITRP 테스트 사용자 만들기](#creating-an-itrp-test-user)** - Britta Simon의 Azure AD 표현과 연결되는 대응 사용자를 ITRP에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="db701-145">**[Creating an ITRP test user](#creating-an-itrp-test-user)** - to have a counterpart of Britta Simon in ITRP that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="db701-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="db701-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="db701-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="db701-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="db701-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="db701-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="db701-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 ITRP 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="db701-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ITRP application.</span></span>

<span data-ttu-id="db701-150">**ITRP에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="db701-150">**To configure Azure AD single sign-on with ITRP, perform the following steps:**</span></span>

1. <span data-ttu-id="db701-151">Azure Portal의 **ITRP** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db701-151">In the Azure portal, on the **ITRP** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="db701-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="db701-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_samlbase.png)

3. <span data-ttu-id="db701-155">**ITRP 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="db701-155">On the **ITRP Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_url.png)

    <span data-ttu-id="db701-157">a.</span><span class="sxs-lookup"><span data-stu-id="db701-157">a.</span></span> <span data-ttu-id="db701-158">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<tenant-name>.itrp.com`</span><span class="sxs-lookup"><span data-stu-id="db701-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.itrp.com`</span></span>

    <span data-ttu-id="db701-159">b.</span><span class="sxs-lookup"><span data-stu-id="db701-159">b.</span></span> <span data-ttu-id="db701-160">**식별자** 텍스트 상자에서 `https://<tenant-name>.itrp.com` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="db701-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenant-name>.itrp.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="db701-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="db701-161">These values are not real.</span></span> <span data-ttu-id="db701-162">실제 로그온 URL 및 식별자로 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="db701-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="db701-163">이러한 값을 얻으려면 [ITRP 클라이언트 지원 팀](https://www.itrp.com/support)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="db701-163">Contact [ITRP Client support team](https://www.itrp.com/support) to get these values.</span></span> 
 
4. <span data-ttu-id="db701-164">**SAML 서명 인증서** 섹션에서 인증서의 **지문** 값을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="db701-164">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_certificate.png) 

5. <span data-ttu-id="db701-166">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db701-166">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-itrp-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="db701-168">**ITRP 구성** 섹션에서 **ITRP 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="db701-168">On the **ITRP Configuration** section, click **Configure ITRP** to open **Configure sign-on** window.</span></span> <span data-ttu-id="db701-169">**빠른 참조 섹션**에서 **SAML Single Sign-On 서비스 URL 및 로그아웃 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="db701-169">Copy the **SAML Single Sign-On Service URL and Sign-Out URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_configure.png) 

7. <span data-ttu-id="db701-171">다른 웹 브라우저 창에서 ITRP 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="db701-171">In a different web browser window, log in to your ITRP company site as an administrator.</span></span>

8. <span data-ttu-id="db701-172">위쪽에 도구 모음에서 **설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db701-172">In the toolbar on the top, click **Settings**.</span></span>
   
    <span data-ttu-id="db701-173">![ITRP](./media/active-directory-saas-itrp-tutorial/ic775570.png "ITRP")</span><span class="sxs-lookup"><span data-stu-id="db701-173">![ITRP](./media/active-directory-saas-itrp-tutorial/ic775570.png "ITRP")</span></span>

8. <span data-ttu-id="db701-174">왼쪽 탐색 창에서 **Single Sign-On**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="db701-174">In the left navigation pane, select **Single Sign-On**.</span></span>
   
    <span data-ttu-id="db701-175">![Single Sign-On](./media/active-directory-saas-itrp-tutorial/ic775571.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="db701-175">![Single Sign-On](./media/active-directory-saas-itrp-tutorial/ic775571.png "Single Sign-On")</span></span>

9. <span data-ttu-id="db701-176">Single Sign-On 구성 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="db701-176">In the Single Sign-On configuration section, perform the following steps:</span></span>
   
    <span data-ttu-id="db701-177">![Single Sign-On](./media/active-directory-saas-itrp-tutorial/ic775572.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="db701-177">![Single Sign-On](./media/active-directory-saas-itrp-tutorial/ic775572.png "Single Sign-On")</span></span>
    
    <span data-ttu-id="db701-178">![Single Sign-On](./media/active-directory-saas-itrp-tutorial/ic775573.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="db701-178">![Single Sign-On](./media/active-directory-saas-itrp-tutorial/ic775573.png "Single Sign-On")</span></span>   

    <span data-ttu-id="db701-179">a.</span><span class="sxs-lookup"><span data-stu-id="db701-179">a.</span></span> <span data-ttu-id="db701-180">**사용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db701-180">Click **Enable**.</span></span>

    <span data-ttu-id="db701-181">b.</span><span class="sxs-lookup"><span data-stu-id="db701-181">b.</span></span> <span data-ttu-id="db701-182">Azure Portal에서 복사한 **로그아웃 URL** 값을 **원격 로그아웃 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="db701-182">In **Remote Log Out URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="db701-183">c.</span><span class="sxs-lookup"><span data-stu-id="db701-183">c.</span></span> <span data-ttu-id="db701-184">Azure Portal에서 복사한 **SAML Single Sign-On 서비스 URL** 값을 **SAML SSO URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="db701-184">In **SAML SSO URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="db701-185">Azure Portal에서 복사한 인증서의 **지문** 값을 **인증서 지문** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="db701-185">d.In **Certificate Fingerprint** textbox, paste the **Thumbprint** value of certificate, which you have copied from Azure portal.</span></span> 
      
10. <span data-ttu-id="db701-186">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db701-186">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="db701-187">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db701-187">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="db701-188">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="db701-188">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="db701-189">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db701-189">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="db701-190">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="db701-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="db701-191">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="db701-191">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="db701-193">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="db701-193">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="db701-194">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db701-194">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-itrp-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="db701-196">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db701-196">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-itrp-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="db701-198">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db701-198">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-itrp-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="db701-200">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="db701-200">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-itrp-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="db701-202">a.</span><span class="sxs-lookup"><span data-stu-id="db701-202">a.</span></span> <span data-ttu-id="db701-203">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="db701-203">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="db701-204">b.</span><span class="sxs-lookup"><span data-stu-id="db701-204">b.</span></span> <span data-ttu-id="db701-205">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="db701-205">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="db701-206">c.</span><span class="sxs-lookup"><span data-stu-id="db701-206">c.</span></span> <span data-ttu-id="db701-207">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="db701-207">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="db701-208">d.</span><span class="sxs-lookup"><span data-stu-id="db701-208">d.</span></span> <span data-ttu-id="db701-209">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db701-209">Click **Create**.</span></span>
 
### <a name="creating-an-itrp-test-user"></a><span data-ttu-id="db701-210">ITRP 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="db701-210">Creating an ITRP test user</span></span>

<span data-ttu-id="db701-211">ITRP로 프로비전된 Azure AD 사용자만이 ITRP에 로그인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db701-211">To enable Azure AD users to log in to ITRP, they must be provisioned in to ITRP.</span></span>  

<span data-ttu-id="db701-212">ITRP의 경우 프로비저닝 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="db701-212">In the case of ITRP, provisioning is a manual task.</span></span>

<span data-ttu-id="db701-213">**사용자 계정을 프로비전하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="db701-213">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="db701-214">**ITRP** 테넌트에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="db701-214">Log in to your **ITRP** tenant.</span></span>

2. <span data-ttu-id="db701-215">위쪽의 도구 모음에서 **레코드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db701-215">In the toolbar on the top, click **Records**.</span></span>
   
    <span data-ttu-id="db701-216">![관리자](./media/active-directory-saas-itrp-tutorial/ic775575.png "관리자")</span><span class="sxs-lookup"><span data-stu-id="db701-216">![Admin](./media/active-directory-saas-itrp-tutorial/ic775575.png "Admin")</span></span>

3. <span data-ttu-id="db701-217">팝업 메뉴에서 **사람**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="db701-217">From the popup menu, select **People**.</span></span>
   
    <span data-ttu-id="db701-218">![사람](./media/active-directory-saas-itrp-tutorial/ic775587.png "사람")</span><span class="sxs-lookup"><span data-stu-id="db701-218">![People](./media/active-directory-saas-itrp-tutorial/ic775587.png "People")</span></span>

4. <span data-ttu-id="db701-219">**새 사람 추가** (“+”)를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db701-219">Click **Add New Person** (“+”).</span></span>
   
    <span data-ttu-id="db701-220">![관리자](./media/active-directory-saas-itrp-tutorial/ic775576.png "관리자")</span><span class="sxs-lookup"><span data-stu-id="db701-220">![Admin](./media/active-directory-saas-itrp-tutorial/ic775576.png "Admin")</span></span>

5. <span data-ttu-id="db701-221">새 사람 추가 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="db701-221">On the Add New Person dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="db701-222">![사용자](./media/active-directory-saas-itrp-tutorial/ic775577.png "사용자")</span><span class="sxs-lookup"><span data-stu-id="db701-222">![User](./media/active-directory-saas-itrp-tutorial/ic775577.png "User")</span></span> 
      
    <span data-ttu-id="db701-223">a.</span><span class="sxs-lookup"><span data-stu-id="db701-223">a.</span></span> <span data-ttu-id="db701-224">프로비전할 유효한 AAD 계정의 **이름**과 **전자 메일**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="db701-224">Type the **Name**, **Email** of a valid AAD account you want to provision.</span></span>

    <span data-ttu-id="db701-225">b.</span><span class="sxs-lookup"><span data-stu-id="db701-225">b.</span></span> <span data-ttu-id="db701-226">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db701-226">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="db701-227">다른 ITRP 사용자 계정 생성 도구 또는 ITRP가 제공한 API를 사용하여 AAD 사용자 계정을 프로비저닝할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db701-227">You can use any other ITRP user account creation tools or APIs provided by ITRP to provision AAD user accounts.</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="db701-228">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="db701-228">Assigning the Azure AD test user</span></span>

<span data-ttu-id="db701-229">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 ITRP에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="db701-229">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ITRP.</span></span>

![사용자 할당][200] 

<span data-ttu-id="db701-231">**Britta Simon을 ITRP에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="db701-231">**To assign Britta Simon to ITRP, perform the following steps:**</span></span>

1. <span data-ttu-id="db701-232">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db701-232">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="db701-234">응용 프로그램 목록에서 **ITRP**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="db701-234">In the applications list, select **ITRP**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_app.png) 

3. <span data-ttu-id="db701-236">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db701-236">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="db701-238">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db701-238">Click **Add** button.</span></span> <span data-ttu-id="db701-239">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="db701-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="db701-241">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="db701-241">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="db701-242">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db701-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="db701-243">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db701-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="db701-244">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="db701-244">Testing single sign-on</span></span>

<span data-ttu-id="db701-245">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="db701-245">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="db701-246">액세스 패널에서 ITRP 타일을 클릭하면 ITRP 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="db701-246">When you click the ITRP tile in the Access Panel, you should get automatically signed-on to your ITRP application.</span></span>
<span data-ttu-id="db701-247">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="db701-247">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="db701-248">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="db701-248">Additional resources</span></span>

* [<span data-ttu-id="db701-249">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="db701-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="db701-250">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="db701-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_203.png

