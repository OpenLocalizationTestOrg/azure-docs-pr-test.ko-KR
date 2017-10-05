---
title: "자습서: Rightscale과 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 Rightscale 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3a8d376d-95fb-4dd7-832a-4fdd4dd7c87c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 222c4414a9f736a3589b4cdd0ed934696f6c31ef
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rightscale"></a><span data-ttu-id="d75fc-103">자습서: Rightscale과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="d75fc-103">Tutorial: Azure Active Directory integration with Rightscale</span></span>

<span data-ttu-id="d75fc-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Rightscale을 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d75fc-104">In this tutorial, you learn how to integrate Rightscale with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d75fc-105">Rightscale을 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="d75fc-105">Integrating Rightscale with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d75fc-106">RightScale에 액세스할 수 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d75fc-106">You can control in Azure AD who has access to Rightscale</span></span>
- <span data-ttu-id="d75fc-107">사용자가 자신의 Azure AD 계정으로 Rightscale에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d75fc-107">You can enable your users to automatically get signed-on to Rightscale (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d75fc-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d75fc-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d75fc-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d75fc-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d75fc-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d75fc-110">Prerequisites</span></span>

<span data-ttu-id="d75fc-111">Rightscale과 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d75fc-111">To configure Azure AD integration with Rightscale, you need the following items:</span></span>

- <span data-ttu-id="d75fc-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="d75fc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d75fc-113">Rightscale Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="d75fc-113">A Rightscale single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d75fc-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d75fc-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d75fc-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75fc-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d75fc-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="d75fc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d75fc-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d75fc-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d75fc-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="d75fc-118">Scenario description</span></span>
<span data-ttu-id="d75fc-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75fc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d75fc-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d75fc-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d75fc-121">갤러리에서 Rightscale 추가</span><span class="sxs-lookup"><span data-stu-id="d75fc-121">Adding Rightscale from the gallery</span></span>
2. <span data-ttu-id="d75fc-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="d75fc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-rightscale-from-the-gallery"></a><span data-ttu-id="d75fc-123">갤러리에서 Rightscale 추가</span><span class="sxs-lookup"><span data-stu-id="d75fc-123">Adding Rightscale from the gallery</span></span>
<span data-ttu-id="d75fc-124">Rightscale이 Azure AD에 통합되도록 구성하려면 갤러리의 Rightscale을 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75fc-124">To configure the integration of Rightscale into Azure AD, you need to add Rightscale from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d75fc-125">**갤러리에서 Rightscale을 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="d75fc-125">**To add Rightscale from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d75fc-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d75fc-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d75fc-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d75fc-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d75fc-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d75fc-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="d75fc-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d75fc-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="d75fc-133">검색 상자에 **Rightscale**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d75fc-133">In the search box, type **Rightscale**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_search.png)

5. <span data-ttu-id="d75fc-135">결과 패널에서 **Rightscale**을 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d75fc-135">In the results panel, select **Rightscale**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d75fc-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="d75fc-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d75fc-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 사용하여 Rightscale에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="d75fc-138">In this section, you configure and test Azure AD single sign-on with Rightscale based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d75fc-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Rightscale 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75fc-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Rightscale is to a user in Azure AD.</span></span> <span data-ttu-id="d75fc-140">즉, Azure AD 사용자와 Rightscale의 관련 사용자 간에 연결 관계를 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75fc-140">In other words, a link relationship between an Azure AD user and the related user in Rightscale needs to be established.</span></span>

<span data-ttu-id="d75fc-141">Rightscale에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 연결 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d75fc-141">In Rightscale, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d75fc-142">Rightscale에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75fc-142">To configure and test Azure AD single sign-on with Rightscale, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d75fc-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75fc-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d75fc-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d75fc-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d75fc-145">**[Rightscale 테스트 사용자 만들기](#creating-a-rightscale-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 Rightscale에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d75fc-145">**[Creating a Rightscale test user](#creating-a-rightscale-test-user)** - to have a counterpart of Britta Simon in Rightscale that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d75fc-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75fc-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d75fc-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d75fc-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d75fc-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="d75fc-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d75fc-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Rightscale 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d75fc-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Rightscale application.</span></span>

<span data-ttu-id="d75fc-150">**Rightscale에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="d75fc-150">**To configure Azure AD single sign-on with Rightscale, perform the following steps:**</span></span>

1. <span data-ttu-id="d75fc-151">Azure Portal의 **Rightscale** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d75fc-151">In the Azure portal, on the **Rightscale** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="d75fc-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d75fc-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_samlbase.png)

3. <span data-ttu-id="d75fc-155">**Rightscale 도메인 및 URL** 섹션에서 **IDP initiated mode**(IDP 시작 모드)로 응용 프로그램을 구성하려는 경우에는 앱이 이미 Azure와 사전 통합되어 있으므로 수행해야 하는 단계가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d75fc-155">On the **Rightscale Domain and URLs** section, if you wish to configure the application in **IDP initiated mode** you do not have to perform any steps as the app is already pre-integrated with Azure.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_url.png)

4. <span data-ttu-id="d75fc-157">**Rightscale 도메인 및 URL** 섹션에서 **SP initiated mode**(SP 시작 모드)로 응용 프로그램을 구성하려는 경우 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d75fc-157">On the **Rightscale Domain and URLs** section, if you wish to configure the application in **SP initiated mode**, perform the following steps:</span></span>
    
    ![Single Sign-on 구성](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_url1.png)

    <span data-ttu-id="d75fc-159">a.</span><span class="sxs-lookup"><span data-stu-id="d75fc-159">a.</span></span> <span data-ttu-id="d75fc-160">**고급 URL 설정 표시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d75fc-160">Click on the **Show advanced URL settings**.</span></span>

    <span data-ttu-id="d75fc-161">b.</span><span class="sxs-lookup"><span data-stu-id="d75fc-161">b.</span></span> <span data-ttu-id="d75fc-162">**로그온 URL** 텍스트 상자에 URL `https://login.rightscale.com/`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d75fc-162">In the **Sign On URL** textbox, type the URL: `https://login.rightscale.com/`</span></span>

5. <span data-ttu-id="d75fc-163">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="d75fc-163">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_certificate.png) 

6. <span data-ttu-id="d75fc-165">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d75fc-165">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-rightscale-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="d75fc-167">**Rightscale 구성** 섹션에서 **Rightscale 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d75fc-167">On the **Rightscale Configuration** section, click **Configure Rightscale** to open **Configure sign-on** window.</span></span> <span data-ttu-id="d75fc-168">**빠른 참조** 섹션에서 **SAML 엔터티 ID 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="d75fc-168">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    <span data-ttu-id="d75fc-169">![Single Sign-On 구성](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="d75fc-169">![Configure Single Sign-On](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_configure.png) 
<CS></span></span>
8. <span data-ttu-id="d75fc-170">응용 프로그램에 대해 구성된 SSO를 가져오려면 관리자 권한으로 RightScale 테넌트에 로그온해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75fc-170">To get SSO configured for your application, you need to sign-on to your RightScale tenant as an administrator.</span></span>

    <span data-ttu-id="d75fc-171">a.</span><span class="sxs-lookup"><span data-stu-id="d75fc-171">a.</span></span> <span data-ttu-id="d75fc-172">위쪽 메뉴에서 **설정** 탭을 클릭하고 **Single Sign-On**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d75fc-172">In the menu on the top, click the **Settings** tab and select **Single Sign-On**.</span></span>
   
    ![Single Sign-On 구성](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_001.png) 

    <span data-ttu-id="d75fc-174">b.</span><span class="sxs-lookup"><span data-stu-id="d75fc-174">b.</span></span> <span data-ttu-id="d75fc-175">"**새로 만들기**" 단추를 클릭하여 **SAML ID 공급자**를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d75fc-175">Click the "**new**" button to add **Your SAML Identity Providers**.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_002.png) 
 
    <span data-ttu-id="d75fc-177">c.</span><span class="sxs-lookup"><span data-stu-id="d75fc-177">c.</span></span> <span data-ttu-id="d75fc-178">**표시 이름**의 텍스트 상자에 회사 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d75fc-178">In the textbox of **Display Name**, input your company name.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_003.png)
 
    <span data-ttu-id="d75fc-180">d.</span><span class="sxs-lookup"><span data-stu-id="d75fc-180">d.</span></span> <span data-ttu-id="d75fc-181">**검색 힌트를 사용하여 RightScale에서 시작한 SSO 허용**을 선택하고 아래 텍스트 상자에 **도메인 이름**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d75fc-181">Select **Allow RightScale-initiated SSO using a discovery hint** and input your **domain name** in the below textbox.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_004.png)

    <span data-ttu-id="d75fc-183">e.</span><span class="sxs-lookup"><span data-stu-id="d75fc-183">e.</span></span> <span data-ttu-id="d75fc-184">Azure Portal에서 복사한 **SAML Single Sign-On 서비스 URL** 값을 RightScale의 **SAML SSO Endpoint**(SAML SSO 끝점)에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="d75fc-184">Paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal into **SAML SSO Endpoint** in RightScale.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_006.png)

    <span data-ttu-id="d75fc-186">f.</span><span class="sxs-lookup"><span data-stu-id="d75fc-186">f.</span></span> <span data-ttu-id="d75fc-187">Azure Portal에서 복사한 **SAML 엔터티 ID**를 RightScale의 **SAML 엔터티 ID**에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="d75fc-187">Paste the value of **SAML Entity ID** which you have copied from Azure portal into **SAML EntityID** in RightScale.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_008.png)

    <span data-ttu-id="d75fc-189">g.</span><span class="sxs-lookup"><span data-stu-id="d75fc-189">g.</span></span> <span data-ttu-id="d75fc-190">**브라우저** 단추를 클릭하여 Azure Portal에서 다운로드한 인증서를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="d75fc-190">Click **Browser** button to upload the certificate which you downloaded from Azure portal.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_009.png)

    <span data-ttu-id="d75fc-192">h.</span><span class="sxs-lookup"><span data-stu-id="d75fc-192">h.</span></span> <span data-ttu-id="d75fc-193">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d75fc-193">Click **Save**.</span></span>
<CE>
> [!TIP]
> <span data-ttu-id="d75fc-194">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d75fc-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d75fc-195">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d75fc-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d75fc-196">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d75fc-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d75fc-197">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="d75fc-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="d75fc-198">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d75fc-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="d75fc-200">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="d75fc-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d75fc-201">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d75fc-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-rightscale-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d75fc-203">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d75fc-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-rightscale-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d75fc-205">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d75fc-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-rightscale-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d75fc-207">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d75fc-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-rightscale-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d75fc-209">a.</span><span class="sxs-lookup"><span data-stu-id="d75fc-209">a.</span></span> <span data-ttu-id="d75fc-210">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d75fc-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d75fc-211">b.</span><span class="sxs-lookup"><span data-stu-id="d75fc-211">b.</span></span> <span data-ttu-id="d75fc-212">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d75fc-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d75fc-213">c.</span><span class="sxs-lookup"><span data-stu-id="d75fc-213">c.</span></span> <span data-ttu-id="d75fc-214">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="d75fc-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d75fc-215">d.</span><span class="sxs-lookup"><span data-stu-id="d75fc-215">d.</span></span> <span data-ttu-id="d75fc-216">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d75fc-216">Click **Create**.</span></span>
 
### <a name="creating-a-rightscale-test-user"></a><span data-ttu-id="d75fc-217">Rightscale 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="d75fc-217">Creating a Rightscale test user</span></span>

<span data-ttu-id="d75fc-218">이 섹션에서는 RightScale에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d75fc-218">In this section, you create a user called Britta Simon in RightScale.</span></span> <span data-ttu-id="d75fc-219">RightScale 플랫폼에서 사용자를 추가하려면 [Rightscale 클라이언트 지원 팀](mailto:support@rightscale.com)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="d75fc-219">Work with [Rightscale Client support team](mailto:support@rightscale.com) to add the users in the RightScale platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d75fc-220">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="d75fc-220">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d75fc-221">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Rightscale에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="d75fc-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Rightscale.</span></span>

![사용자 할당][200] 

<span data-ttu-id="d75fc-223">**Britta Simon을 Rightscale에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="d75fc-223">**To assign Britta Simon to Rightscale, perform the following steps:**</span></span>

1. <span data-ttu-id="d75fc-224">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d75fc-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="d75fc-226">응용 프로그램 목록에서 **Rightscale**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d75fc-226">In the applications list, select **Rightscale**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_app.png) 

3. <span data-ttu-id="d75fc-228">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d75fc-228">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="d75fc-230">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d75fc-230">Click **Add** button.</span></span> <span data-ttu-id="d75fc-231">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d75fc-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="d75fc-233">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d75fc-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d75fc-234">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d75fc-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d75fc-235">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d75fc-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d75fc-236">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="d75fc-236">Testing single sign-on</span></span>

<span data-ttu-id="d75fc-237">이 섹션은 액세스 패널을 사용하여 Azure AD SSO 구성을 테스트하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d75fc-237">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="d75fc-238">액세스 패널에서 RightScale 타일을 클릭하면 RightScale 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="d75fc-238">When you click the RightScale tile in the Access Panel, you should get automatically signed-on to your RightScale application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d75fc-239">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="d75fc-239">Additional resources</span></span>

* [<span data-ttu-id="d75fc-240">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="d75fc-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d75fc-241">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="d75fc-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_203.png

