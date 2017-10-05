---
title: "자습서: Bonusly와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory 및 Bonusly 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 29fea32a-fa20-47b2-9e24-26feb47b0ae6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 29a88b2efdb9f0f33f7933bc654a5a0fdf589c5a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bonusly"></a><span data-ttu-id="6ead6-103">자습서: Bonusly와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="6ead6-103">Tutorial: Azure Active Directory integration with Bonusly</span></span>

<span data-ttu-id="6ead6-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Bonusly를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-104">In this tutorial, you learn how to integrate Bonusly with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6ead6-105">Bonusly를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-105">Integrating Bonusly with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6ead6-106">Bonusly에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-106">You can control in Azure AD who has access to Bonusly</span></span>
- <span data-ttu-id="6ead6-107">사용자가 해당 Azure AD 계정으로 Bonusly SSO(Single Sign-On)에 자동으로 로그온되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-107">You can enable your users to automatically get signed-on to Bonusly (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6ead6-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="6ead6-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6ead6-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6ead6-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="6ead6-110">Prerequisites</span></span>

<span data-ttu-id="6ead6-111">Bonusly와 Azure AD의 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-111">To configure Azure AD integration with Bonusly, you need the following items:</span></span>

- <span data-ttu-id="6ead6-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="6ead6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6ead6-113">Bonusly Single Sign-on이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="6ead6-113">A Bonusly single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6ead6-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6ead6-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6ead6-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="6ead6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6ead6-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6ead6-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="6ead6-118">Scenario description</span></span>
<span data-ttu-id="6ead6-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6ead6-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6ead6-121">갤러리에서 Bonusly 추가</span><span class="sxs-lookup"><span data-stu-id="6ead6-121">Adding Bonusly from the gallery</span></span>
2. <span data-ttu-id="6ead6-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="6ead6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bonusly-from-the-gallery"></a><span data-ttu-id="6ead6-123">갤러리에서 Bonusly 추가</span><span class="sxs-lookup"><span data-stu-id="6ead6-123">Adding Bonusly from the gallery</span></span>
<span data-ttu-id="6ead6-124">Bonusly의 Azure AD 통합을 구성하려면 갤러리의 Bonusly를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-124">To configure the integration of Bonusly into Azure AD, you need to add Bonusly from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6ead6-125">**갤러리에서 Bonusly를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="6ead6-125">**To add Bonusly from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6ead6-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory 단추][1]

2. <span data-ttu-id="6ead6-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6ead6-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-129">Then go to **All applications**.</span></span>

    ![엔터프라이즈 응용 프로그램 블레이드][2]
    
3. <span data-ttu-id="6ead6-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![새 응용 프로그램 단추][3]

4. <span data-ttu-id="6ead6-133">검색 상자에 **Bonusly**를 입력하고 결과 패널에서 **Bonusly**를 선택한 후 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-133">In the search box, type **Bonusly**, select **Bonusly** from result panel then click **Add** button to add the application.</span></span>

    ![결과 목록의 Bonusly](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="6ead6-135">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="6ead6-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="6ead6-136">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Bonusly에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-136">In this section, you configure and test Azure AD single sign-on with Bonusly based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6ead6-137">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Bonusly 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Bonusly is to a user in Azure AD.</span></span> <span data-ttu-id="6ead6-138">즉, Azure AD 사용자와 Bonusly의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-138">In other words, a link relationship between an Azure AD user and the related user in Bonusly needs to be established.</span></span>

<span data-ttu-id="6ead6-139">Bonusly에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-139">In Bonusly, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="6ead6-140">Bonusly에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-140">To configure and test Azure AD single sign-on with Bonusly, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6ead6-141">**[Azure AD Single Sign-On 구성](#configure-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6ead6-142">**[Azure AD 테스트 사용자 만들기](#create-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6ead6-143">**[Bonusly 테스트 사용자 만들기](#create-a-bonusly-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 Bonusly에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-143">**[Create a Bonusly test user](#create-a-bonusly-test-user)** - to have a counterpart of Britta Simon in Bonusly that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="6ead6-144">**[Azure AD 테스트 사용자 할당](#assign-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6ead6-145">**[Single Sign-on 테스트](#test-single-sign-on)** - 구성이 작동하는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="6ead6-146">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="6ead6-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="6ead6-147">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Bonusly 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Bonusly application.</span></span>

<span data-ttu-id="6ead6-148">**Bonusly에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="6ead6-148">**To configure Azure AD single sign-on with Bonusly, perform the following steps:**</span></span>

1. <span data-ttu-id="6ead6-149">Azure Portal의 **Bonusly** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-149">In the Azure portal, on the **Bonusly** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="6ead6-151">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_samlbase.png)

3. <span data-ttu-id="6ead6-153">**Bonusly 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-153">On the **Bonusly Domain and URLs** section, perform the following steps:</span></span>

    ![Bonusly 도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_url.png)

    <span data-ttu-id="6ead6-155">**회신 URL** 텍스트 상자에 다음 패턴으로 URL을 입력합니다.`https://Bonus.ly/saml/<tenant-name>`</span><span class="sxs-lookup"><span data-stu-id="6ead6-155">In the **Reply URL** textbox, type a URL using the following pattern: `https://Bonus.ly/saml/<tenant-name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6ead6-156">이 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-156">The value is not real.</span></span> <span data-ttu-id="6ead6-157">실제 회신 URL로 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-157">Update the value with the actual Reply URL.</span></span> <span data-ttu-id="6ead6-158">값을 얻으려면 [Bonusly 지원 팀](https://Bonusly/contact)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="6ead6-158">Contact [Bonusly support team](https://Bonusly/contact) to get the value.</span></span>
 
4. <span data-ttu-id="6ead6-159">**SAML 서명 인증서** 섹션에서 인증서의 **지문** 값을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-159">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value from the certificate.</span></span>

    ![인증서 다운로드 링크](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_certificate.png) 

5. <span data-ttu-id="6ead6-161">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-161">Click **Save** button.</span></span>

    ![Single Sign-On 구성 저장 단추](./media/active-directory-saas-bonus-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6ead6-163">**Bonusly 구성** 섹션에서 **Bonusly 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-163">On the **Bonusly Configuration** section, click **Configure Bonusly** to open **Configure sign-on** window.</span></span> <span data-ttu-id="6ead6-164">**빠른 참조 섹션**에서 **SAML 엔터티 ID 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-164">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Bonusly 구성](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_configure.png) 

7. <span data-ttu-id="6ead6-166">다른 브라우저 창에서 **Bonusly** 테넌트에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-166">In a different browser window, log in to your **Bonusly** tenant.</span></span>

8. <span data-ttu-id="6ead6-167">위쪽에 도구 모음에서 **설정**을 클릭하고 **통합 및 앱**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-167">In the toolbar on the top, click **Settings**, and then select **Integrations and apps**.</span></span>
   
    <span data-ttu-id="6ead6-168">![Bonusly 소셜 섹션](./media/active-directory-saas-bonus-tutorial/ic773686.png "Bonusly")</span><span class="sxs-lookup"><span data-stu-id="6ead6-168">![Bonusly Social Section](./media/active-directory-saas-bonus-tutorial/ic773686.png "Bonusly")</span></span>
9. <span data-ttu-id="6ead6-169">**Single Sign-On**에서 **SAML**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-169">Under **Single Sign-On**, select **SAML**.</span></span>

10. <span data-ttu-id="6ead6-170">**SAML** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-170">On the **SAML** dialog page, perform the following steps:</span></span>
   
    <span data-ttu-id="6ead6-171">![Bonusly Saml 대화 상자 페이지](./media/active-directory-saas-bonus-tutorial/ic773687.png "Bonusly")</span><span class="sxs-lookup"><span data-stu-id="6ead6-171">![Bonusly Saml Dialog page](./media/active-directory-saas-bonus-tutorial/ic773687.png "Bonusly")</span></span>
   
    <span data-ttu-id="6ead6-172">a.</span><span class="sxs-lookup"><span data-stu-id="6ead6-172">a.</span></span> <span data-ttu-id="6ead6-173">Azure Portal에서 복사한 **SAML Single Sign-On 서비스 URL** 값을 **IdP SSO 대상 URL** 텍스트 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-173">In the **IdP SSO target URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="6ead6-174">b.</span><span class="sxs-lookup"><span data-stu-id="6ead6-174">b.</span></span> <span data-ttu-id="6ead6-175">Azure Portal에서 복사한 **SAML 엔터티 ID** 값을 **IdP 발급자** 텍스트 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-175">In the **IdP Issuer** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="6ead6-176">c.</span><span class="sxs-lookup"><span data-stu-id="6ead6-176">c.</span></span> <span data-ttu-id="6ead6-177">Azure Portal에서 복사한 **SAML Single Sign-On 서비스 URL** 값을 **IdP 로그인 URL** 텍스트 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-177">In the **IdP Login URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="6ead6-178">d.</span><span class="sxs-lookup"><span data-stu-id="6ead6-178">d.</span></span> <span data-ttu-id="6ead6-179">Azure Portal에서 복사한 **지문** 값을 **인증서 지문** 텍스트 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-179">Paste the **Thumbprint** value copied from Azure portal into the **Cert Fingerprint** textbox.</span></span>
   
11. <span data-ttu-id="6ead6-180">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-180">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="6ead6-181">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-181">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="6ead6-182">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-182">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="6ead6-183">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-183">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="6ead6-184">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="6ead6-184">Create an Azure AD test user</span></span>
<span data-ttu-id="6ead6-185">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-185">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 테스트 사용자 만들기][100]

<span data-ttu-id="6ead6-187">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="6ead6-187">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6ead6-188">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-188">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure Active Directory 단추](./media/active-directory-saas-bonus-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6ead6-190">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-190">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    !["사용자 및 그룹" 및 "모든 사용자" 링크](./media/active-directory-saas-bonus-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6ead6-192">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-192">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![추가 단추](./media/active-directory-saas-bonus-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6ead6-194">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-194">On the **User** dialog page, perform the following steps:</span></span>
 
    ![사용자 대화 상자](./media/active-directory-saas-bonus-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6ead6-196">a.</span><span class="sxs-lookup"><span data-stu-id="6ead6-196">a.</span></span> <span data-ttu-id="6ead6-197">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-197">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6ead6-198">b.</span><span class="sxs-lookup"><span data-stu-id="6ead6-198">b.</span></span> <span data-ttu-id="6ead6-199">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-199">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6ead6-200">c.</span><span class="sxs-lookup"><span data-stu-id="6ead6-200">c.</span></span> <span data-ttu-id="6ead6-201">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-201">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="6ead6-202">d.</span><span class="sxs-lookup"><span data-stu-id="6ead6-202">d.</span></span> <span data-ttu-id="6ead6-203">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-203">Click **Create**.</span></span>
 
### <a name="create-a-bonusly-test-user"></a><span data-ttu-id="6ead6-204">Bonusly 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="6ead6-204">Create a Bonusly test user</span></span>

<span data-ttu-id="6ead6-205">Azure AD 사용자가 Bonusly에 로그인할 수 있도록 하려면 Bonusly로 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-205">In order to enable Azure AD users to log in to Bonusly, they must be provisioned into Bonusly.</span></span> <span data-ttu-id="6ead6-206">Bonusly의 경우 프로비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-206">In the case of Bonusly, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="6ead6-207">다른 Bonusly 사용자 계정 생성 도구 또는 Bonusly가 제공한 API를 사용하여 AAD 사용자 계정을 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-207">You can use any other Bonusly user account creation tools or APIs provided by Bonusly to provision AAD user accounts.</span></span>
>  

<span data-ttu-id="6ead6-208">**사용자 프로비전을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="6ead6-208">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="6ead6-209">브라우저 창에서 Bonusly 테넌트에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-209">In a web browser window, log in to your Bonusly tenant.</span></span>

2. <span data-ttu-id="6ead6-210">**설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-210">Click **Settings**.</span></span>
 
    <span data-ttu-id="6ead6-211">![설정](./media/active-directory-saas-bonus-tutorial/ic781041.png "설정")</span><span class="sxs-lookup"><span data-stu-id="6ead6-211">![Settings](./media/active-directory-saas-bonus-tutorial/ic781041.png "Settings")</span></span>

3. <span data-ttu-id="6ead6-212">**사용자 및 보너스** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-212">Click the **Users and bonuses** tab.</span></span>
   
    <span data-ttu-id="6ead6-213">![사용자 및 보너스](./media/active-directory-saas-bonus-tutorial/ic781042.png "사용자 및 보너스")</span><span class="sxs-lookup"><span data-stu-id="6ead6-213">![Users and bonuses](./media/active-directory-saas-bonus-tutorial/ic781042.png "Users and bonuses")</span></span>

4. <span data-ttu-id="6ead6-214">**사용자 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-214">Click **Manage Users**.</span></span>
   
    <span data-ttu-id="6ead6-215">![사용자 관리](./media/active-directory-saas-bonus-tutorial/ic781043.png "사용자 관리")</span><span class="sxs-lookup"><span data-stu-id="6ead6-215">![Manage Users](./media/active-directory-saas-bonus-tutorial/ic781043.png "Manage Users")</span></span>

5. <span data-ttu-id="6ead6-216">**사용자 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-216">Click **Add User**.</span></span>
   
    <span data-ttu-id="6ead6-217">![사용자 추가](./media/active-directory-saas-bonus-tutorial/ic781044.png "사용자 추가")</span><span class="sxs-lookup"><span data-stu-id="6ead6-217">![Add User](./media/active-directory-saas-bonus-tutorial/ic781044.png "Add User")</span></span>

6. <span data-ttu-id="6ead6-218">**사용자 추가** 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-218">On the **Add User** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="6ead6-219">![사용자 추가](./media/active-directory-saas-bonus-tutorial/ic781045.png "사용자 추가")</span><span class="sxs-lookup"><span data-stu-id="6ead6-219">![Add User](./media/active-directory-saas-bonus-tutorial/ic781045.png "Add User")</span></span>  

    <span data-ttu-id="6ead6-220">a.</span><span class="sxs-lookup"><span data-stu-id="6ead6-220">a.</span></span> <span data-ttu-id="6ead6-221">**이름** 텍스트 상자에 사용자의 이름(예: **Britta**)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-221">In the **First name** textbox, enter the first name of user like **Britta**.</span></span>

    <span data-ttu-id="6ead6-222">b.</span><span class="sxs-lookup"><span data-stu-id="6ead6-222">b.</span></span> <span data-ttu-id="6ead6-223">**성** 텍스트 상자에 사용자의 성(예: **Simon**)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-223">In the **Last name** textbox, enter the last name of user like **Simon**.</span></span>
 
    <span data-ttu-id="6ead6-224">c.</span><span class="sxs-lookup"><span data-stu-id="6ead6-224">c.</span></span> <span data-ttu-id="6ead6-225">**메일** 텍스트 상자에 **brittasimon@contoso.com**과 같은 사용자의 메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-225">In the **Email** textbox, enter the email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="6ead6-226">d.</span><span class="sxs-lookup"><span data-stu-id="6ead6-226">d.</span></span> <span data-ttu-id="6ead6-227">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-227">Click **Save**.</span></span>
   
     >[!NOTE]
     ><span data-ttu-id="6ead6-228">Azure AD 계정 보유자는 활성화되기 전에 계정을 확인하기 위한 링크를 포함하는 전자 메일을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-228">The Azure AD account holder receives an email that includes a link to confirm the account before it becomes active.</span></span>
     >  

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="6ead6-229">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="6ead6-229">Assign the Azure AD test user</span></span>

<span data-ttu-id="6ead6-230">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Bonusly에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-230">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Bonusly.</span></span>

![사용자 역할 할당][200] 

<span data-ttu-id="6ead6-232">**Britta Simon을 Bonusly에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="6ead6-232">**To assign Britta Simon to Bonusly, perform the following steps:**</span></span>

1. <span data-ttu-id="6ead6-233">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-233">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="6ead6-235">응용 프로그램 목록에서 **Bonusly**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-235">In the applications list, select **Bonusly**.</span></span>

    ![응용 프로그램 목록의 Bonusly 링크](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_app.png) 

3. <span data-ttu-id="6ead6-237">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-237">In the menu on the left, click **Users and groups**.</span></span>

    !["사용자 및 그룹" 링크][202] 

4. <span data-ttu-id="6ead6-239">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-239">Click **Add** button.</span></span> <span data-ttu-id="6ead6-240">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-240">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![할당 추가 창][203]

5. <span data-ttu-id="6ead6-242">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-242">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="6ead6-243">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-243">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6ead6-244">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-244">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="6ead6-245">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="6ead6-245">Test single sign-on</span></span>

<span data-ttu-id="6ead6-246">이 섹션은 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-246">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="6ead6-247">액세스 패널에서 Bonusly 타일을 클릭하면 Bonusly 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ead6-247">When you click the Bonusly tile in the Access Panel, you should get automatically signed-on to your Bonusly application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6ead6-248">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="6ead6-248">Additional resources</span></span>

* [<span data-ttu-id="6ead6-249">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="6ead6-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6ead6-250">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="6ead6-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_203.png

