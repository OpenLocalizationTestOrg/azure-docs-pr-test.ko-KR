---
title: "자습서: Showpad와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 Showpad 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 48b6bee0-dbc5-4863-964d-75b25e517741
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: c8b39c9215675d8073f896f934339e7cd55334cc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-showpad"></a><span data-ttu-id="81562-103">자습서: Showpad와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="81562-103">Tutorial: Azure Active Directory integration with Showpad</span></span>

<span data-ttu-id="81562-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Showpad를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="81562-104">In this tutorial, you learn how to integrate Showpad with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="81562-105">Showpad를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="81562-105">Integrating Showpad with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="81562-106">Showpad에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81562-106">You can control in Azure AD who has access to Showpad</span></span>
- <span data-ttu-id="81562-107">사용자가 해당 Azure AD 계정으로 Showpad에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81562-107">You can enable your users to automatically get signed-on to Showpad (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="81562-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81562-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="81562-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="81562-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="81562-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="81562-110">Prerequisites</span></span>

<span data-ttu-id="81562-111">Showpad과 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-111">To configure Azure AD integration with Showpad, you need the following items:</span></span>

- <span data-ttu-id="81562-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="81562-112">An Azure AD subscription</span></span>
- <span data-ttu-id="81562-113">Showpad Single Sign-on이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="81562-113">A Showpad single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="81562-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="81562-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="81562-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="81562-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="81562-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="81562-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81562-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="81562-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="81562-118">Scenario description</span></span>
<span data-ttu-id="81562-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="81562-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81562-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="81562-121">갤러리에서 Showpad 추가</span><span class="sxs-lookup"><span data-stu-id="81562-121">Adding Showpad from the gallery</span></span>
2. <span data-ttu-id="81562-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="81562-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-showpad-from-the-gallery"></a><span data-ttu-id="81562-123">갤러리에서 Showpad 추가</span><span class="sxs-lookup"><span data-stu-id="81562-123">Adding Showpad from the gallery</span></span>

<span data-ttu-id="81562-124">Showpad의 Azure AD 통합을 구성하려면 갤러리의 Showpad를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-124">To configure the integration of Showpad into Azure AD, you need to add Showpad from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="81562-125">**갤러리에서 Showpad를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="81562-125">**To add Showpad from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="81562-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="81562-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="81562-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="81562-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="81562-133">검색 상자에 **Showpad**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-133">In the search box, type **Showpad**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_search.png)

5. <span data-ttu-id="81562-135">결과 창에서 **Showpad**을 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-135">In the results panel, select **Showpad**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="81562-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="81562-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="81562-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Showpad에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-138">In this section, you configure and test Azure AD single sign-on with Showpad based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="81562-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Showpad 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Showpad is to a user in Azure AD.</span></span> <span data-ttu-id="81562-140">즉, Azure AD 사용자와 Showpad의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-140">In other words, a link relationship between an Azure AD user and the related user in Showpad needs to be established.</span></span>

<span data-ttu-id="81562-141">Showpad에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-141">In Showpad, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="81562-142">Showpad에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-142">To configure and test Azure AD single sign-on with Showpad, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="81562-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="81562-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="81562-145">**[Showpad 테스트 사용자 만들기](#creating-a-showpad-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 Showpad에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="81562-145">**[Creating a Showpad test user](#creating-a-showpad-test-user)** - to have a counterpart of Britta Simon in Showpad that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="81562-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="81562-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="81562-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="81562-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="81562-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Showpad 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Showpad application.</span></span>

<span data-ttu-id="81562-150">**Showpad에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="81562-150">**To configure Azure AD single sign-on with Showpad, perform the following steps:**</span></span>

1. <span data-ttu-id="81562-151">Azure Portal의 **Showpad** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-151">In the Azure portal, on the **Showpad** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="81562-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_samlbase.png)

3. <span data-ttu-id="81562-155">**Showpad 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-155">On the **Showpad Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_url.png)

    <span data-ttu-id="81562-157">a.</span><span class="sxs-lookup"><span data-stu-id="81562-157">a.</span></span> <span data-ttu-id="81562-158">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<comapany-name>.showpad.biz/login`</span><span class="sxs-lookup"><span data-stu-id="81562-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<comapany-name>.showpad.biz/login`</span></span>

    <span data-ttu-id="81562-159">b.</span><span class="sxs-lookup"><span data-stu-id="81562-159">b.</span></span> <span data-ttu-id="81562-160">**식별자** 텍스트 상자에서 `https://<company-name>.showpad.biz` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<company-name>.showpad.biz`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="81562-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="81562-161">These values are not real.</span></span> <span data-ttu-id="81562-162">실제 로그온 URL 및 식별자로 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="81562-163">이러한 값을 얻으려면 [Showpad 지원 팀](https://help.showpad.com)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="81562-163">Contact [Showpad support team](https://help.showpad.com) to get these values.</span></span> 
 


4. <span data-ttu-id="81562-164">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 메타데이터 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_certificate.png) 

5. <span data-ttu-id="81562-166">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-166">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-showpad-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="81562-168">Showpad 테넌트에 관리자 권한으로 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-168">Sign-on to your Showpad tenant as an administrator.</span></span>

7. <span data-ttu-id="81562-169">위쪽 메뉴에서 **설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-169">In the menu on the top, click the **Settings**.</span></span>
   
    ![앱 쪽에서 Single Sign-On 구성](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_001.png) 

8. <span data-ttu-id="81562-171">"**Single Sign-On**"으로 이동하고 "**사용**"을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-171">Navigate to "**Single Sign-On**" and click "**Enable**."</span></span>
   
    ![앱 쪽에서 Single Sign-On 구성](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_002.png)

9. <span data-ttu-id="81562-173">**SAML 2.0 서비스 추가** 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-173">On the **Add a SAML 2.0 Service** dialog, perform the following steps:</span></span>
   
    ![앱 쪽에서 Single Sign-On 구성](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_003.png) 
   
    <span data-ttu-id="81562-175">a.</span><span class="sxs-lookup"><span data-stu-id="81562-175">a.</span></span> <span data-ttu-id="81562-176">**이름** 텍스트 상자에 식별자 공급자의 이름(예: 회사 이름)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-176">In the **Name** textbox, type the name of Identifier Provider (for example: your company name).</span></span>
   
    <span data-ttu-id="81562-177">b.</span><span class="sxs-lookup"><span data-stu-id="81562-177">b.</span></span> <span data-ttu-id="81562-178">**메타데이터 소스**로 **XML**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-178">As **Metadata Source**, select **XML**.</span></span>
   
    <span data-ttu-id="81562-179">c.</span><span class="sxs-lookup"><span data-stu-id="81562-179">c.</span></span> <span data-ttu-id="81562-180">Azure Portal에서 다운로드한 메타데이터 XML 파일의 내용을 복사한 다음 **메타데이터 XML** 텍스트 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="81562-180">Copy the content of metadata XML file, which you have downloaded from the Azure portal, and then paste it into the **Metadata XML** textbox.</span></span>
   
    <span data-ttu-id="81562-181">d.</span><span class="sxs-lookup"><span data-stu-id="81562-181">d.</span></span> <span data-ttu-id="81562-182">**로그인할 때 새 사용자에 대한 계정 자동 프로비전**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-182">Select **Auto-provision accounts for new users when they log in**.</span></span>
   
    <span data-ttu-id="81562-183">e.</span><span class="sxs-lookup"><span data-stu-id="81562-183">e.</span></span> <span data-ttu-id="81562-184">**제출**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-184">Click **Submit**.</span></span>

> [!TIP]
> <span data-ttu-id="81562-185">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81562-185">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="81562-186">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="81562-186">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="81562-187">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81562-187">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="81562-188">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="81562-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="81562-189">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="81562-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="81562-191">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="81562-191">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="81562-192">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-192">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-showpad-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="81562-194">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-194">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-showpad-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="81562-196">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-196">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-showpad-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="81562-198">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-198">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-showpad-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="81562-200">a.</span><span class="sxs-lookup"><span data-stu-id="81562-200">a.</span></span> <span data-ttu-id="81562-201">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-201">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="81562-202">b.</span><span class="sxs-lookup"><span data-stu-id="81562-202">b.</span></span> <span data-ttu-id="81562-203">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-203">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="81562-204">c.</span><span class="sxs-lookup"><span data-stu-id="81562-204">c.</span></span> <span data-ttu-id="81562-205">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="81562-205">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="81562-206">d.</span><span class="sxs-lookup"><span data-stu-id="81562-206">d.</span></span> <span data-ttu-id="81562-207">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-207">Click **Create**.</span></span>
 
### <a name="creating-a-showpad-test-user"></a><span data-ttu-id="81562-208">Showpad 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="81562-208">Creating a Showpad test user</span></span>

<span data-ttu-id="81562-209">이 섹션은 Showpad에서 Britta Simon이라는 사용자를 만들기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="81562-209">The objective of this section is to create a user called Britta Simon in Showpad.</span></span> 

<span data-ttu-id="81562-210">Showpad는 Just-In-Time 프로비전을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-210">Showpad supports just-in-time provisioning.</span></span> <span data-ttu-id="81562-211">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)**을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="81562-211">You have enabled provisioning in **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**.</span></span> 

<span data-ttu-id="81562-212">이 섹션에 작업 항목이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="81562-212">There is no action item for you in this section.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="81562-213">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="81562-213">Assigning the Azure AD test user</span></span>

<span data-ttu-id="81562-214">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Showpad에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-214">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Showpad.</span></span>

![사용자 할당][200] 

<span data-ttu-id="81562-216">**Britta Simon을 Showpad에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="81562-216">**To assign Britta Simon to Showpad, perform the following steps:**</span></span>

1. <span data-ttu-id="81562-217">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-217">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="81562-219">응용 프로그램 목록에서 **Showpad**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-219">In the applications list, select **Showpad**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_app.png) 

3. <span data-ttu-id="81562-221">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-221">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="81562-223">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-223">Click **Add** button.</span></span> <span data-ttu-id="81562-224">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="81562-226">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-226">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="81562-227">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="81562-228">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="81562-229">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="81562-229">Testing single sign-on</span></span>

<span data-ttu-id="81562-230">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-230">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="81562-231">액세스 패널에서 Showpad 타일을 클릭하면 Showpad 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="81562-231">When you click the Showpad tile in the Access Panel, you should get automatically signed-on to Showpad application.</span></span>
<span data-ttu-id="81562-232">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="81562-232">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="81562-233">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="81562-233">Additional resources</span></span>

* [<span data-ttu-id="81562-234">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="81562-234">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="81562-235">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="81562-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_203.png

