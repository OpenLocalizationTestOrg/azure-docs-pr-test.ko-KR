---
title: "자습서: Canvas LMS와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory 및 Canvas LMS 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bfed291c-a33e-410d-b919-5b965a631d45
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: jeedes
ms.openlocfilehash: 2212b7a81b66d1afd1aa78d1487b07b6d7b84129
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-canvas-lms"></a><span data-ttu-id="b60d0-103">자습서: Canvas LMS와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="b60d0-103">Tutorial: Azure Active Directory integration with Canvas LMS</span></span>

<span data-ttu-id="b60d0-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Canvas를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-104">In this tutorial, you learn how to integrate Canvas with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b60d0-105">Canvas를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-105">Integrating Canvas with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b60d0-106">Canvas에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-106">You can control in Azure AD who has access to Canvas</span></span>
- <span data-ttu-id="b60d0-107">사용자가 해당 Azure AD 계정으로 Canvas에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-107">You can enable your users to automatically get signed-on to Canvas (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b60d0-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b60d0-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b60d0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b60d0-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="b60d0-110">Prerequisites</span></span>

<span data-ttu-id="b60d0-111">Canvas와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-111">To configure Azure AD integration with Canvas, you need the following items:</span></span>

- <span data-ttu-id="b60d0-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="b60d0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b60d0-113">Canvas Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="b60d0-113">A Canvas single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b60d0-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b60d0-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b60d0-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="b60d0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b60d0-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b60d0-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="b60d0-118">Scenario description</span></span>
<span data-ttu-id="b60d0-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b60d0-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b60d0-121">갤러리에서 Canvas 추가</span><span class="sxs-lookup"><span data-stu-id="b60d0-121">Adding Canvas from the gallery</span></span>
2. <span data-ttu-id="b60d0-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="b60d0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-canvas-from-the-gallery"></a><span data-ttu-id="b60d0-123">갤러리에서 Canvas 추가</span><span class="sxs-lookup"><span data-stu-id="b60d0-123">Adding Canvas from the gallery</span></span>
<span data-ttu-id="b60d0-124">Azure AD와 Canvas 통합을 구성하려면 갤러리의 Canvas를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-124">To configure the integration of Canvas into Azure AD, you need to add Canvas from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b60d0-125">**갤러리에서 Canvas를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="b60d0-125">**To add Canvas from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b60d0-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b60d0-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b60d0-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="b60d0-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="b60d0-133">검색 상자에 **Canvas**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-133">In the search box, type **Canvas**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_search.png)

5. <span data-ttu-id="b60d0-135">결과 패널에서 **Canvas**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-135">In the results panel, select **Canvas**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b60d0-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="b60d0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b60d0-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Canvas에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-138">In this section, you configure and test Azure AD single sign-on with Canvas based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b60d0-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Canvas 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Canvas is to a user in Azure AD.</span></span> <span data-ttu-id="b60d0-140">즉, Azure AD 사용자와 Canvas의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-140">In other words, a link relationship between an Azure AD user and the related user in Canvas needs to be established.</span></span>

<span data-ttu-id="b60d0-141">Canvas에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-141">In Canvas, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b60d0-142">Canvas에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-142">To configure and test Azure AD single sign-on with Canvas, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b60d0-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b60d0-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b60d0-145">**[Canvas 테스트 사용자 만들기](#creating-a-canvas-test-user)** - Britta Simon의 Azure AD 사용자 표현과 연결되는 대응 사용자를 Canvas에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-145">**[Creating a Canvas test user](#creating-a-canvas-test-user)** - to have a counterpart of Britta Simon in Canvas that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b60d0-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b60d0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b60d0-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="b60d0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b60d0-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Canvas 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Canvas application.</span></span>

<span data-ttu-id="b60d0-150">**Canvas에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="b60d0-150">**To configure Azure AD single sign-on with Canvas, perform the following steps:**</span></span>

1. <span data-ttu-id="b60d0-151">Azure Portal의 **Canvas** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-151">In the Azure portal, on the **Canvas** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="b60d0-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_samlbase.png)

3. <span data-ttu-id="b60d0-155">**Canvas 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-155">On the **Canvas Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_url.png)

    <span data-ttu-id="b60d0-157">a.</span><span class="sxs-lookup"><span data-stu-id="b60d0-157">a.</span></span> <span data-ttu-id="b60d0-158">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<tenant-name>.instructure.com`</span><span class="sxs-lookup"><span data-stu-id="b60d0-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.instructure.com`</span></span>

    <span data-ttu-id="b60d0-159">b.</span><span class="sxs-lookup"><span data-stu-id="b60d0-159">b.</span></span> <span data-ttu-id="b60d0-160">**식별자** 텍스트 상자에 `https://<tenant-name>.instructure.com/saml2` 패턴으로 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-160">In the **Identifier** textbox, type the value using the following pattern: `https://<tenant-name>.instructure.com/saml2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b60d0-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-161">These values are not real.</span></span> <span data-ttu-id="b60d0-162">실제 로그온 URL 및 식별자로 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="b60d0-163">이러한 값을 얻으려면 [Canvas 클라이언트 지원팀](https://community.canvaslms.com/community/help)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="b60d0-163">Contact [Canvas Client support team](https://community.canvaslms.com/community/help) to get these values.</span></span> 
 
4. <span data-ttu-id="b60d0-164">**SAML 서명 인증서** 섹션에서 인증서의 **지문** 값을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-164">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_certificate.png) 

5. <span data-ttu-id="b60d0-166">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-166">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b60d0-168">**Canvas 구성** 섹션에서 **Canvas 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-168">On the **Canvas Configuration** section, click **Configure Canvas** to open **Configure sign-on** window.</span></span> <span data-ttu-id="b60d0-169">**빠른 참조 섹션**에서 **암호 변경 URL, 로그아웃 URL, SAML 엔터티 ID 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-169">Copy the **Change Password URL, Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_configure.png) 
 
7. <span data-ttu-id="b60d0-171">다른 웹 브라우저 창에서 Canvas 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-171">In a different web browser window, log in to your Canvas company site as an administrator.</span></span>

8. <span data-ttu-id="b60d0-172">**코스 \> 관리된 계정 \> Microsoft**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-172">Go to **Courses \> Managed Accounts \> Microsoft**.</span></span>
   
    <span data-ttu-id="b60d0-173">![Canvas](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")</span><span class="sxs-lookup"><span data-stu-id="b60d0-173">![Canvas](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")</span></span>

9. <span data-ttu-id="b60d0-174">왼쪽 탐색 창에서 **인증**을 선택한 다음 **새 SAML Config 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-174">In the navigation pane on the left, select **Authentication**, and then click **Add New SAML Config**.</span></span>
   
    <span data-ttu-id="b60d0-175">![인증](./media/active-directory-saas-canvas-lms-tutorial/IC775991.png "인증")</span><span class="sxs-lookup"><span data-stu-id="b60d0-175">![Authentication](./media/active-directory-saas-canvas-lms-tutorial/IC775991.png "Authentication")</span></span>

10. <span data-ttu-id="b60d0-176">현재 통합 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-176">On the Current Integration page, perform the following steps:</span></span>
   
    <span data-ttu-id="b60d0-177">![현재 통합](./media/active-directory-saas-canvas-lms-tutorial/IC775992.png "현재 통합")</span><span class="sxs-lookup"><span data-stu-id="b60d0-177">![Current Integration](./media/active-directory-saas-canvas-lms-tutorial/IC775992.png "Current Integration")</span></span>

    <span data-ttu-id="b60d0-178">a.</span><span class="sxs-lookup"><span data-stu-id="b60d0-178">a.</span></span> <span data-ttu-id="b60d0-179">Azure Portal에서 복사한 **SAML 엔터티 ID**를 **IdP 엔터티 ID** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-179">In **IdP Entity ID** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="b60d0-180">b.</span><span class="sxs-lookup"><span data-stu-id="b60d0-180">b.</span></span> <span data-ttu-id="b60d0-181">Azure Portal에서 복사한 **SAML Single Sign-On 서비스 URL** 값을 **로그온 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-181">In **Log On URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal .</span></span>

    <span data-ttu-id="b60d0-182">c.</span><span class="sxs-lookup"><span data-stu-id="b60d0-182">c.</span></span> <span data-ttu-id="b60d0-183">Azure Portal에서 복사한 **로그아웃 URL** 값을 **로그아웃 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-183">In **Log Out URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="b60d0-184">d.</span><span class="sxs-lookup"><span data-stu-id="b60d0-184">d.</span></span> <span data-ttu-id="b60d0-185">Azure Portal에서 복사한 **암호 변경 URL** 값을 **암호 변경 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-185">In **Change Password Link** textbox, paste the value of **Change Password URL** which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="b60d0-186">e.</span><span class="sxs-lookup"><span data-stu-id="b60d0-186">e.</span></span> <span data-ttu-id="b60d0-187">Azure Portal에서 복사한 인증서의 **지문** 값을 **인증서 지문** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-187">In **Certificate Fingerprint** textbox, paste the **Thumbprint** value of certificate which you have copied from Azure portal.</span></span>      
        
    <span data-ttu-id="b60d0-188">f.</span><span class="sxs-lookup"><span data-stu-id="b60d0-188">f.</span></span> <span data-ttu-id="b60d0-189">**로그인 특성** 목록에서 **NameID**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-189">From the **Login Attribute** list, select **NameID**.</span></span>

    <span data-ttu-id="b60d0-190">g.</span><span class="sxs-lookup"><span data-stu-id="b60d0-190">g.</span></span> <span data-ttu-id="b60d0-191">**식별자 형식** 목록에서 **emailAddress**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-191">From the **Identifier Format** list, select **emailAddress**.</span></span>

    <span data-ttu-id="b60d0-192">h.</span><span class="sxs-lookup"><span data-stu-id="b60d0-192">h.</span></span> <span data-ttu-id="b60d0-193">**인증 설정 저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-193">Click **Save Authentication Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="b60d0-194">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b60d0-195">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b60d0-196">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b60d0-197">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="b60d0-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="b60d0-198">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="b60d0-200">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="b60d0-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b60d0-201">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b60d0-203">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b60d0-205">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b60d0-207">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b60d0-209">a.</span><span class="sxs-lookup"><span data-stu-id="b60d0-209">a.</span></span> <span data-ttu-id="b60d0-210">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b60d0-211">b.</span><span class="sxs-lookup"><span data-stu-id="b60d0-211">b.</span></span> <span data-ttu-id="b60d0-212">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b60d0-213">c.</span><span class="sxs-lookup"><span data-stu-id="b60d0-213">c.</span></span> <span data-ttu-id="b60d0-214">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b60d0-215">d.</span><span class="sxs-lookup"><span data-stu-id="b60d0-215">d.</span></span> <span data-ttu-id="b60d0-216">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-216">Click **Create**.</span></span>
 
### <a name="creating-a-canvas-test-user"></a><span data-ttu-id="b60d0-217">Canvas 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="b60d0-217">Creating a Canvas test user</span></span>

<span data-ttu-id="b60d0-218">Azure AD 사용자가 Canvas에 로그인할 수 있도록 하려면 Canvas로 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-218">To enable Azure AD users to log in to Canvas, they must be provisioned into Canvas.</span></span>

<span data-ttu-id="b60d0-219">Canvas의 경우 사용자 프로비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-219">In case of Canvas, user provisioning is a manual task.</span></span>

<span data-ttu-id="b60d0-220">**사용자 계정을 프로비전하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="b60d0-220">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="b60d0-221">**Canvas** 테넌트에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-221">Log in to your **Canvas** tenant.</span></span>

2. <span data-ttu-id="b60d0-222">**코스 \> 관리된 계정 \> Microsoft**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-222">Go to **Courses \> Managed Accounts \> Microsoft**.</span></span>
   
   <span data-ttu-id="b60d0-223">![Canvas](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")</span><span class="sxs-lookup"><span data-stu-id="b60d0-223">![Canvas](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")</span></span>

3. <span data-ttu-id="b60d0-224">**사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-224">Click **Users**.</span></span>
   
   <span data-ttu-id="b60d0-225">![사용자](./media/active-directory-saas-canvas-lms-tutorial/IC775995.png "사용자")</span><span class="sxs-lookup"><span data-stu-id="b60d0-225">![Users](./media/active-directory-saas-canvas-lms-tutorial/IC775995.png "Users")</span></span>

4. <span data-ttu-id="b60d0-226">**새 사용자 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-226">Click **Add New User**.</span></span>
   
   <span data-ttu-id="b60d0-227">![사용자](./media/active-directory-saas-canvas-lms-tutorial/IC775996.png "사용자")</span><span class="sxs-lookup"><span data-stu-id="b60d0-227">![Users](./media/active-directory-saas-canvas-lms-tutorial/IC775996.png "Users")</span></span>

5. <span data-ttu-id="b60d0-228">새 사용자 추가 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-228">On the Add a New User dialog page, perform the following steps:</span></span>
   
   <span data-ttu-id="b60d0-229">![사용자 추가](./media/active-directory-saas-canvas-lms-tutorial/IC775997.png "사용자 추가")</span><span class="sxs-lookup"><span data-stu-id="b60d0-229">![Add User](./media/active-directory-saas-canvas-lms-tutorial/IC775997.png "Add User")</span></span>
   
   <span data-ttu-id="b60d0-230">a.</span><span class="sxs-lookup"><span data-stu-id="b60d0-230">a.</span></span> <span data-ttu-id="b60d0-231">**전체 이름** 텍스트 상자에 **BrittaSimon**과 같은 사용자의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-231">In the **Full Name** textbox, enter the name of user like **BrittaSimon**.</span></span>

   <span data-ttu-id="b60d0-232">b.</span><span class="sxs-lookup"><span data-stu-id="b60d0-232">b.</span></span> <span data-ttu-id="b60d0-233">**전자 메일** 텍스트 상자에 **brittasimon@contoso.com**과 같은 사용자의 전자 메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-233">In the **Email** textbox, enter the email of user like **brittasimon@contoso.com**.</span></span>

   <span data-ttu-id="b60d0-234">c.</span><span class="sxs-lookup"><span data-stu-id="b60d0-234">c.</span></span> <span data-ttu-id="b60d0-235">**로그인** 텍스트 상자에 **brittasimon@contoso.com**과 같은 사용자의 Azure AD 전자 메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-235">In the **Login** textbox, enter the user’s Azure AD email address like **brittasimon@contoso.com**.</span></span>

   <span data-ttu-id="b60d0-236">d.</span><span class="sxs-lookup"><span data-stu-id="b60d0-236">d.</span></span> <span data-ttu-id="b60d0-237">**이 계정 만들기에 대해 사용자에 게 전자 메일**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-237">Select **Email the user about this account creation**.</span></span>

   <span data-ttu-id="b60d0-238">e.</span><span class="sxs-lookup"><span data-stu-id="b60d0-238">e.</span></span> <span data-ttu-id="b60d0-239">**사용자 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-239">Click **Add User**.</span></span>

>[!NOTE]
><span data-ttu-id="b60d0-240">다른 Canvas 사용자 계정 생성 도구 또는 Canvas가 제공한 API를 사용하여 AAD 사용자 계정을 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-240">You can use any other Canvas user account creation tools or APIs provided by Canvas to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b60d0-241">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="b60d0-241">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b60d0-242">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Canvas에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-242">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Canvas.</span></span>

![사용자 할당][200] 

<span data-ttu-id="b60d0-244">**Britta Simon을 Canvas에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="b60d0-244">**To assign Britta Simon to Canvas, perform the following steps:**</span></span>

1. <span data-ttu-id="b60d0-245">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-245">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="b60d0-247">응용 프로그램 목록에서 **Canvas**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-247">In the applications list, select **Canvas**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_app.png) 

3. <span data-ttu-id="b60d0-249">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-249">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="b60d0-251">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-251">Click **Add** button.</span></span> <span data-ttu-id="b60d0-252">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="b60d0-254">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-254">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b60d0-255">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b60d0-256">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b60d0-257">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="b60d0-257">Testing single sign-on</span></span>

<span data-ttu-id="b60d0-258">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-258">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b60d0-259">액세스 패널에서 Canvas 타일을 클릭하면 Canvas 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="b60d0-259">When you click the Canvas tile in the Access Panel, you should get automatically signed-on to your Canvas application.</span></span>
<span data-ttu-id="b60d0-260">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b60d0-260">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b60d0-261">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="b60d0-261">Additional resources</span></span>

* [<span data-ttu-id="b60d0-262">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="b60d0-262">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b60d0-263">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="b60d0-263">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_203.png

