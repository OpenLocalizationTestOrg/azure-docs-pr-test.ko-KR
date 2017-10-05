---
title: "자습서: Azure Active Directory와 Zendesk 통합 | Microsoft Docs"
description: "Azure Active Directory와 Zendesk 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9d7c91e5-78f5-4016-862f-0f3242b00680
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 51c06d838c5ed6286dfb99ea25faaaf33bad5f3c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zendesk"></a><span data-ttu-id="2c102-103">자습서:Azure Active Directory와 Zendesk 통합</span><span class="sxs-lookup"><span data-stu-id="2c102-103">Tutorial: Azure Active Directory integration with Zendesk</span></span>

<span data-ttu-id="2c102-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Zendesk를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-104">In this tutorial, you learn how to integrate Zendesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2c102-105">Zendesk와 Azure AD를 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-105">Integrating Zendesk with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="2c102-106">Zendesk에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-106">You can control in Azure AD who has access to Zendesk</span></span>
- <span data-ttu-id="2c102-107">사용자가 해당 Azure AD 계정으로 Zendesk에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-107">You can enable your users to automatically get signed-on to Zendesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2c102-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="2c102-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2c102-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2c102-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="2c102-110">Prerequisites</span></span>

<span data-ttu-id="2c102-111">Zendesk와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-111">To configure Azure AD integration with Zendesk, you need the following items:</span></span>

- <span data-ttu-id="2c102-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="2c102-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2c102-113">Zendesk Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="2c102-113">A Zendesk single sign-on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="2c102-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="2c102-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2c102-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="2c102-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2c102-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="2c102-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="2c102-118">Scenario description</span></span>
<span data-ttu-id="2c102-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2c102-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2c102-121">갤러리에서 Zendesk 추가</span><span class="sxs-lookup"><span data-stu-id="2c102-121">Adding Zendesk from the gallery</span></span>
2. <span data-ttu-id="2c102-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="2c102-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-zendesk-from-the-gallery"></a><span data-ttu-id="2c102-123">갤러리에서 Zendesk 추가</span><span class="sxs-lookup"><span data-stu-id="2c102-123">Adding Zendesk from the gallery</span></span>
<span data-ttu-id="2c102-124">Zendesk의 Azure AD 통합을 구성하려면 갤러리의 Zendesk를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-124">To configure the integration of Zendesk into Azure AD, you need to add Zendesk from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2c102-125">**갤러리에서 Zendesk를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="2c102-125">**To add Zendesk from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2c102-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-126">In the **[Azure Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2c102-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="2c102-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="2c102-131">대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-131">Click **New application** button on the top of the dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="2c102-133">검색 상자에 **Zendesk**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-133">In the search box, type **Zendesk**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_search.png)

5. <span data-ttu-id="2c102-135">결과 패널에서 **Zendesk**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-135">In the results panel, select **Zendesk**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2c102-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="2c102-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2c102-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Zendesk에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-138">In this section, you configure and test Azure AD single sign-on with Zendesk based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2c102-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Zendesk 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Zendesk is to a user in Azure AD.</span></span> <span data-ttu-id="2c102-140">즉, Azure AD 사용자와 Zendesk의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-140">In other words, a link relationship between an Azure AD user and the related user in Zendesk needs to be established.</span></span>

<span data-ttu-id="2c102-141">이 연결 관계는 Azure AD의 **사용자 이름** 값을 Zendesk의 **Username** 값으로 할당하여 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Zendesk.</span></span>

<span data-ttu-id="2c102-142">Zendesk에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-142">To configure and test Azure AD single sign-on with Zendesk, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2c102-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="2c102-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2c102-145">**[Zendesk 테스트 사용자 만들기](#creating-a-zendesk-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 Zendesk에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-145">**[Creating a Zendesk test user](#creating-a-zendesk-test-user)** - to have a counterpart of Britta Simon in Zendesk that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="2c102-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2c102-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2c102-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="2c102-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2c102-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Zendesk 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Zendesk application.</span></span>

<span data-ttu-id="2c102-150">**Zendesk에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="2c102-150">**To configure Azure AD single sign-on with Zendesk, perform the following steps:**</span></span>

1. <span data-ttu-id="2c102-151">Azure Portal의 **Zendesk** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-151">In the Azure portal, on the **Zendesk** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="2c102-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_samlbase.png)

3. <span data-ttu-id="2c102-155">**Zendesk 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-155">On the **Zendesk Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_url.png)

    <span data-ttu-id="2c102-157">a.</span><span class="sxs-lookup"><span data-stu-id="2c102-157">a.</span></span> <span data-ttu-id="2c102-158">**로그온 URL** 텍스트 상자에 다음 패턴으로 값을 입력합니다. `https://<subdomain>.zendesk.com` </span><span class="sxs-lookup"><span data-stu-id="2c102-158">In the **Sign-on URL** textbox, type the value using the following pattern: `https://<subdomain>.zendesk.com`</span></span>

    <span data-ttu-id="2c102-159">b.</span><span class="sxs-lookup"><span data-stu-id="2c102-159">b.</span></span> <span data-ttu-id="2c102-160">**식별자** 텍스트 상자에 `https://<subdomain>.zendesk.com` 패턴으로 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-160">In the **Identifier** textbox, type the value using the following pattern: `https://<subdomain>.zendesk.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2c102-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-161">These values are not real.</span></span> <span data-ttu-id="2c102-162">실제 로그온 URL 및 식별자 URL로 이러한 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-162">Update these values with the actual Sign-on URL and Identifier URL.</span></span> <span data-ttu-id="2c102-163">이러한 값을 얻으려면 [Zendesk 지원 팀](https://support.zendesk.com/hc/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="2c102-163">Contact [Zendesk support team](https://support.zendesk.com/hc/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise) to get these values.</span></span> 

4. <span data-ttu-id="2c102-164">Zendesk에는 특정 형식의 SAML 어설션이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-164">Zendesk expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="2c102-165">필수 SAML 특성은 없지만 필요에 따라 다음 단계를 수행하여 **사용자 특성** 섹션에서 특성을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-165">There are no mandatory SAML attributes but optionally you can add an attribute from **User Attributes** section by following the below steps:</span></span> 

     ![Single Sign-on 구성](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_attributes1.png)

    <span data-ttu-id="2c102-167">a.</span><span class="sxs-lookup"><span data-stu-id="2c102-167">a.</span></span> <span data-ttu-id="2c102-168">**기타 모든 사용자 특성 보기 및 편집** 확인란을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-168">Click the **View and edit all the other attributes** check box.</span></span>
     
    ![Single Sign-on 구성](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_attributes2.png)
   
    <span data-ttu-id="2c102-170">b.</span><span class="sxs-lookup"><span data-stu-id="2c102-170">b.</span></span> <span data-ttu-id="2c102-171">**특성 추가**를 클릭하여 **특성 추가** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-171">Click the **Add Attribute** to open **Add attribute** dialog.</span></span>
    
    ![Single Sign-on 구성](./media/active-directory-saas-zendesk-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="2c102-173">c.</span><span class="sxs-lookup"><span data-stu-id="2c102-173">c.</span></span> <span data-ttu-id="2c102-174">**이름** 텍스트 상자에 특성 이름(예: **emailaddress**)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-174">In the **Name** textbox, type the attribute name (for example **emailaddress**).</span></span>
    
    <span data-ttu-id="2c102-175">d.</span><span class="sxs-lookup"><span data-stu-id="2c102-175">d.</span></span> <span data-ttu-id="2c102-176">**값** 목록에서 특성 값을 **user.mail**로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-176">From the **Value** list, select the attribute value (as **user.mail**).</span></span>
    
    <span data-ttu-id="2c102-177">e.</span><span class="sxs-lookup"><span data-stu-id="2c102-177">e.</span></span> <span data-ttu-id="2c102-178">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-178">Click **Ok**</span></span>
 
    > [!NOTE] 
    > <span data-ttu-id="2c102-179">기본적으로 Azure AD에 없는 특성을 추가하려면 확장 특성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-179">You use extension attributes to add attributes that are not in Azure AD by default.</span></span> <span data-ttu-id="2c102-180">**Zendesk**에서 허용하는 전체 SAML 특성 목록을 가져오려면 [User attributes that can be set in SAML](https://support.zendesk.com/hc/en-us/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise-)(SAML에서 설정할 수 있는 사용자 특성)을 클릭하세요.</span><span class="sxs-lookup"><span data-stu-id="2c102-180">Click [User attributes that can be set in SAML](https://support.zendesk.com/hc/en-us/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise-) to get the complete list of SAML attributes that **Zendesk** accepts.</span></span> 

5. <span data-ttu-id="2c102-181">**SAML 서명 인증서** 섹션에서 인증서의 **지문** 값을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-181">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_certificate.png) 

6. <span data-ttu-id="2c102-183">**Zendesk 구성** 섹션에서 **Zendesk 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-183">On the **Zendesk Configuration** section, click **Configure Zendesk** to open **Configure sign-on** window.</span></span> <span data-ttu-id="2c102-184">**빠른 참조 섹션**에서 **로그아웃 URL 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-184">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_configure.png) 

7. <span data-ttu-id="2c102-186">다른 웹 브라우저 창에서 관리자 권한으로 Zendesk 회사 사이트에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-186">In a different web browser window, log into your Zendesk company site as an administrator.</span></span>

8. <span data-ttu-id="2c102-187">**Admin**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-187">Click **Admin**.</span></span>

9. <span data-ttu-id="2c102-188">**설정**을 클릭하고 왼쪽 탐색 창에서 **보안**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-188">In the left navigation pane, click **Settings**, and then click **Security**.</span></span>

10. <span data-ttu-id="2c102-189">**보안** 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-189">On the **Security** page, perform the following steps:</span></span> 
   
     <span data-ttu-id="2c102-190">![보안](./media/active-directory-saas-zendesk-tutorial/ic773089.png "보안")</span><span class="sxs-lookup"><span data-stu-id="2c102-190">![Security](./media/active-directory-saas-zendesk-tutorial/ic773089.png "Security")</span></span>

    <span data-ttu-id="2c102-191">![Single Sign-On](./media/active-directory-saas-zendesk-tutorial/ic773090.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="2c102-191">![Single sign-on](./media/active-directory-saas-zendesk-tutorial/ic773090.png "Single sign-on")</span></span>

     <span data-ttu-id="2c102-192">a.</span><span class="sxs-lookup"><span data-stu-id="2c102-192">a.</span></span> <span data-ttu-id="2c102-193">**관리자 및 에이전트** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-193">Click the **Admin & Agents** tab.</span></span>

     <span data-ttu-id="2c102-194">b.</span><span class="sxs-lookup"><span data-stu-id="2c102-194">b.</span></span> <span data-ttu-id="2c102-195">**SSO(Single Sign-On) 및 SAML**을 선택하고**SAML**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-195">Select **Single sign-on (SSO) and SAML**, and then select **SAML**.</span></span>

     <span data-ttu-id="2c102-196">c.</span><span class="sxs-lookup"><span data-stu-id="2c102-196">c.</span></span> <span data-ttu-id="2c102-197">Azure Portal에서 복사한 **SAML Single Sign-On 서비스 URL** 값을 **SAML SSO URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-197">In **SAML SSO URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 

     <span data-ttu-id="2c102-198">d.</span><span class="sxs-lookup"><span data-stu-id="2c102-198">d.</span></span> <span data-ttu-id="2c102-199">Azure Portal에서 복사한 **로그아웃 URL** 값을 **원격 로그아웃 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-199">In **Remote Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
        
     <span data-ttu-id="2c102-200">e.</span><span class="sxs-lookup"><span data-stu-id="2c102-200">e.</span></span> <span data-ttu-id="2c102-201">Azure Portal에서 복사한 인증서의 **지문** 값을 **인증서 지문** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-201">In **Certificate Fingerprint** textbox, paste the **Thumbprint** value of certificate which you have copied from Azure portal.</span></span>
     
     <span data-ttu-id="2c102-202">f.</span><span class="sxs-lookup"><span data-stu-id="2c102-202">f.</span></span> <span data-ttu-id="2c102-203">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-203">Click **Save**.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2c102-204">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="2c102-204">Creating an Azure AD test user</span></span>
<span data-ttu-id="2c102-205">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-205">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="2c102-207">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="2c102-207">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2c102-208">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-208">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-zendesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2c102-210">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-210">To display the list of users go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-zendesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2c102-212">대화 상자 위쪽에서 **추가**를 클릭하여 **사용자** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-212">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-zendesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2c102-214">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-214">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-zendesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2c102-216">a.</span><span class="sxs-lookup"><span data-stu-id="2c102-216">a.</span></span> <span data-ttu-id="2c102-217">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-217">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2c102-218">b.</span><span class="sxs-lookup"><span data-stu-id="2c102-218">b.</span></span> <span data-ttu-id="2c102-219">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-219">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2c102-220">c.</span><span class="sxs-lookup"><span data-stu-id="2c102-220">c.</span></span> <span data-ttu-id="2c102-221">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-221">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="2c102-222">d.</span><span class="sxs-lookup"><span data-stu-id="2c102-222">d.</span></span> <span data-ttu-id="2c102-223">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-223">Click **Create**.</span></span> 

### <a name="creating-a-zendesk-test-user"></a><span data-ttu-id="2c102-224">Zendesk 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="2c102-224">Creating a Zendesk test user</span></span>

<span data-ttu-id="2c102-225">Azure AD 사용자가 **Zendesk**에 로그인할 수 있도록 하려면 **Zendesk**로 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-225">To enable Azure AD users to log into **Zendesk**, they must be provisioned into **Zendesk**.</span></span>  
<span data-ttu-id="2c102-226">앱에서 할당된 역할에 따라 예상된 동작입니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-226">Depending on the role assigned in the apps, it's the expected behavior:</span></span>

 1. <span data-ttu-id="2c102-227">**최종 사용자** 계정은 로그인할 때 자동으로 프로비전됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-227">**End-user** accounts are automatically provisioned when signing in.</span></span>
 2. <span data-ttu-id="2c102-228">**에이전트** 및 **관리자** 계정은 로그인하기 전에 **Zendesk**에서 수동으로 프로비전해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-228">**Agent** and **Admin** accounts need to be manually provisioned in **Zendesk** before signing in.</span></span>
 
<span data-ttu-id="2c102-229">**사용자 계정을 프로비전하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="2c102-229">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="2c102-230">**Zendesk** 테넌트에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-230">Log in to your **Zendesk** tenant.</span></span>

2. <span data-ttu-id="2c102-231">**고객 목록** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-231">Select the **Customer List** tab.</span></span>

3. <span data-ttu-id="2c102-232">**사용자** 탭을 선택하고 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-232">Select the **User** tab, and click **Add**.</span></span>
   
    <span data-ttu-id="2c102-233">![사용자 추가](./media/active-directory-saas-zendesk-tutorial/ic773632.png "사용자 추가")</span><span class="sxs-lookup"><span data-stu-id="2c102-233">![Add user](./media/active-directory-saas-zendesk-tutorial/ic773632.png "Add user")</span></span>
4. <span data-ttu-id="2c102-234">프로비전 하려는 기존 Azure AD 계정의 이메일 주소를 입력하고, **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-234">Type the email address of an existing Azure AD account you want to provision, and then click **Save**.</span></span>
   
    <span data-ttu-id="2c102-235">![새 사용자](./media/active-directory-saas-zendesk-tutorial/ic773633.png "새 사용자")</span><span class="sxs-lookup"><span data-stu-id="2c102-235">![New user](./media/active-directory-saas-zendesk-tutorial/ic773633.png "New user")</span></span>

> [!NOTE]
> <span data-ttu-id="2c102-236">다른 Zendesk 사용자 계정 생성 도구 또는 Zendesk에서 제공하는 APIs를 사용하여 AAD 사용자 계정을 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-236">You can use any other Zendesk user account creation tools or APIs provided by Zendesk to provision AAD user accounts.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="2c102-237">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="2c102-237">Assigning the Azure AD test user</span></span>

<span data-ttu-id="2c102-238">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Zendesk에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-238">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Zendesk.</span></span>

![사용자 할당][200] 

<span data-ttu-id="2c102-240">**Britta Simon을 Zendesk에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="2c102-240">**To assign Britta Simon to Zendesk, perform the following steps:**</span></span>

1. <span data-ttu-id="2c102-241">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-241">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="2c102-243">응용 프로그램 목록에서 **Zendesk**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-243">In the applications list, select **Zendesk**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_app.png) 

3. <span data-ttu-id="2c102-245">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-245">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="2c102-247">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-247">Click **Add** button.</span></span> <span data-ttu-id="2c102-248">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="2c102-250">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-250">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="2c102-251">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2c102-252">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2c102-253">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="2c102-253">Testing single sign-on</span></span>

<span data-ttu-id="2c102-254">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-254">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="2c102-255">액세스 패널에서 Zendesk 타일을 클릭하면 Zendesk 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c102-255">When you click the Zendesk tile in the Access Panel, you should get automatically signed-on to your Zendesk application.</span></span>
<span data-ttu-id="2c102-256">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2c102-256">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2c102-257">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="2c102-257">Additional resources</span></span>

* [<span data-ttu-id="2c102-258">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="2c102-258">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2c102-259">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="2c102-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_203.png
