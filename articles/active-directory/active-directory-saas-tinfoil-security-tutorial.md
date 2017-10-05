---
title: "자습서: TINFOIL SECURITY와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 TINFOIL SECURITY 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: da02da92-e3b0-4c09-ad6c-180882b0f9f8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 614e4de3335574f4b56c7d641af4fcfafdb17d12
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tinfoil-security"></a><span data-ttu-id="366d5-103">자습서: TINFOIL SECURITY와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="366d5-103">Tutorial: Azure Active Directory integration with TINFOIL SECURITY</span></span>

<span data-ttu-id="366d5-104">이 자습서에서는 Azure AD(Azure Active Directory)와 TINFOIL SECURITY를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-104">In this tutorial, you learn how to integrate TINFOIL SECURITY with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="366d5-105">TINFOIL SECURITY를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-105">Integrating TINFOIL SECURITY with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="366d5-106">TINFOIL SECURITY에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-106">You can control in Azure AD who has access to TINFOIL SECURITY</span></span>
- <span data-ttu-id="366d5-107">사용자의 Azure AD 계정으로 TINFOIL SECURITY에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-107">You can enable your users to automatically get signed-on to TINFOIL SECURITY (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="366d5-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="366d5-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="366d5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="366d5-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="366d5-110">Prerequisites</span></span>

<span data-ttu-id="366d5-111">TINFOIL SECURITY와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-111">To configure Azure AD integration with TINFOIL SECURITY, you need the following items:</span></span>

- <span data-ttu-id="366d5-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="366d5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="366d5-113">TINFOIL SECURITY Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="366d5-113">A TINFOIL SECURITY single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="366d5-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="366d5-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="366d5-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="366d5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="366d5-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="366d5-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="366d5-118">Scenario description</span></span>
<span data-ttu-id="366d5-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="366d5-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="366d5-121">갤러리에서 TINFOIL SECURITY 추가</span><span class="sxs-lookup"><span data-stu-id="366d5-121">Add TINFOIL SECURITY from the gallery</span></span>
2. <span data-ttu-id="366d5-122">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="366d5-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-tinfoil-security-from-the-gallery"></a><span data-ttu-id="366d5-123">갤러리에서 TINFOIL SECURITY 추가</span><span class="sxs-lookup"><span data-stu-id="366d5-123">Add TINFOIL SECURITY from the gallery</span></span>
<span data-ttu-id="366d5-124">TINFOIL SECURITY가 Azure AD로 통합되도록 구성하려면 갤러리에서 TINFOIL SECURITY를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-124">To configure the integration of TINFOIL SECURITY into Azure AD, you need to add TINFOIL SECURITY from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="366d5-125">**갤러리에서 TINFOIL SECURITY를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="366d5-125">**To add TINFOIL SECURITY from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="366d5-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="366d5-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="366d5-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="366d5-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="366d5-133">검색 상자에 **TINFOIL SECURITY**를 입력하고 결과 창에서 **TINFOIL SECURITY**를 선택한 후 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-133">In the search box, type **TINFOIL SECURITY**, select  **TINFOIL SECURITY** from result panel then click **Add** button to add the application.</span></span>

    ![갤러리의 TINFOIL SECURITY](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="366d5-135">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="366d5-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="366d5-136">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 TINFOIL SECURITY에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-136">In this section, you configure and test Azure AD single sign-on with TINFOIL SECURITY based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="366d5-137">Single Sign-On이 작동하려면 Azure AD 사용자에 대응하는 TINFOIL SECURITY 사용자가 누구인지 Azure AD에서 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-137">For single sign-on to work, Azure AD needs to know what the counterpart user in TINFOIL SECURITY is to a user in Azure AD.</span></span> <span data-ttu-id="366d5-138">즉, Azure AD 사용자와 TINFOIL SECURITY의 관련 사용자 간에 링크 관계가 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-138">In other words, a link relationship between an Azure AD user and the related user in TINFOIL SECURITY needs to be established.</span></span>

<span data-ttu-id="366d5-139">TINFOIL SECURITY에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-139">In TINFOIL SECURITY, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="366d5-140">TINFOIL SECURITY에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-140">To configure and test Azure AD single sign-on with TINFOIL SECURITY, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="366d5-141">**[Azure AD Single Sign-On 구성](#configure-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="366d5-142">**[Azure AD 테스트 사용자 만들기](#create-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="366d5-143">**[TINFOIL SECURITY 테스트 사용자 만들기](#create-a-tinfoil-security-test-user)** - Britta Simon의 Azure AD 표현과 연결되는 대응 사용자를 TINFOIL SECURITY에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-143">**[Create a TINFOIL SECURITY test user](#create-a-tinfoil-security-test-user)** - to have a counterpart of Britta Simon in TINFOIL SECURITY that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="366d5-144">**[Azure AD 테스트 사용자 할당](#assign-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="366d5-145">**[Single Sign-on 테스트](#test-single-sign-on)** - 구성이 작동하는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="366d5-146">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="366d5-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="366d5-147">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 TINFOIL SECURITY 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TINFOIL SECURITY application.</span></span>

<span data-ttu-id="366d5-148">**TINFOIL SECURITY에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="366d5-148">**To configure Azure AD single sign-on with TINFOIL SECURITY, perform the following steps:**</span></span>

1. <span data-ttu-id="366d5-149">Azure Portal의 **TINFOIL SECURITY** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-149">In the Azure portal, on the **TINFOIL SECURITY** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="366d5-151">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![SAML 기반 로그온](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_samlbase.png)

3. <span data-ttu-id="366d5-153">앱이 Azure와 이미 사전 통합되었으므로 **TINFOIL SECURITY 도메인 및 URL** 섹션에서 사용자는 아무 단계도 수행할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-153">On the **TINFOIL SECURITY Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_url.png)


4. <span data-ttu-id="366d5-155">**SAML 서명 인증서** 섹션에서 인증서의 **지문** 값을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-155">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value.</span></span>

    ![SAML 서명 인증서 섹션](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_certificate.png) 

5. <span data-ttu-id="366d5-157">필요한 특성 매핑을 추가하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-157">To add the required attribute mappings, perform the following steps:</span></span>
    
    <span data-ttu-id="366d5-158">![특성](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute1.png "특성")</span><span class="sxs-lookup"><span data-stu-id="366d5-158">![Attributes](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute1.png "Attributes")</span></span>
    
    | <span data-ttu-id="366d5-159">특성 이름</span><span class="sxs-lookup"><span data-stu-id="366d5-159">Attribute Name</span></span>    |   <span data-ttu-id="366d5-160">특성 값</span><span class="sxs-lookup"><span data-stu-id="366d5-160">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="366d5-161">accountid</span><span class="sxs-lookup"><span data-stu-id="366d5-161">accountid</span></span> | <span data-ttu-id="366d5-162">UXXXXXXXXXXXXX</span><span class="sxs-lookup"><span data-stu-id="366d5-162">UXXXXXXXXXXXXX</span></span> |
    
    <span data-ttu-id="366d5-163">a.</span><span class="sxs-lookup"><span data-stu-id="366d5-163">a.</span></span> <span data-ttu-id="366d5-164">**사용자 특성 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-164">Click **add user attribute**.</span></span>
    
    <span data-ttu-id="366d5-165">![특성 추가](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute.png "특성")</span><span class="sxs-lookup"><span data-stu-id="366d5-165">![ADD Attribute](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute.png "Attributes")</span></span>
    
    <span data-ttu-id="366d5-166">![특성 추가](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_addatt.png "특성")</span><span class="sxs-lookup"><span data-stu-id="366d5-166">![ADD Attribute](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_addatt.png "Attributes")</span></span>
    
    <span data-ttu-id="366d5-167">b.</span><span class="sxs-lookup"><span data-stu-id="366d5-167">b.</span></span> <span data-ttu-id="366d5-168">**특성 이름** 텍스트 상자에 **accountid**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-168">In the **Attribute Name** textbox, type **accountid**.</span></span>
    
    <span data-ttu-id="366d5-169">c.</span><span class="sxs-lookup"><span data-stu-id="366d5-169">c.</span></span> <span data-ttu-id="366d5-170">**특성 값** 텍스트 상자에 나중에 이 자습서에서 얻을 계정 ID 값을 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-170">In the **Attribute Value** textbox, paste the account ID value which you will get later on the tutorial.</span></span>
    
    <span data-ttu-id="366d5-171">d.</span><span class="sxs-lookup"><span data-stu-id="366d5-171">d.</span></span> <span data-ttu-id="366d5-172">**Ok**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-172">Click **Ok**.</span></span>    

6. <span data-ttu-id="366d5-173">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-173">Click **Save** button.</span></span>

    ![저장 단추](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="366d5-175">**TINFOIL SECURITY 구성** 섹션에서 **TINFOIL SECURITY 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-175">On the **TINFOIL SECURITY Configuration** section, click **Configure TINFOIL SECURITY** to open **Configure sign-on** window.</span></span> <span data-ttu-id="366d5-176">**빠른 참조 섹션**에서 **SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-176">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![TINFOIL SECURITY 구성](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_configure.png) 

8. <span data-ttu-id="366d5-178">다른 웹 브라우저 창에서 TINFOIL SECURITY 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-178">In a different web browser window, log into your TINFOIL SECURITY company site as an administrator.</span></span>

9. <span data-ttu-id="366d5-179">위쪽에 도구 모음에서 **내 계정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-179">In the toolbar on the top, click **My Account**.</span></span>
   
    <span data-ttu-id="366d5-180">![대시보드](./media/active-directory-saas-tinfoil-security-tutorial/ic798971.png "대시보드")</span><span class="sxs-lookup"><span data-stu-id="366d5-180">![Dashboard](./media/active-directory-saas-tinfoil-security-tutorial/ic798971.png "Dashboard")</span></span>

10. <span data-ttu-id="366d5-181">**보안**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-181">Click **Security**.</span></span>
   
    <span data-ttu-id="366d5-182">![보안](./media/active-directory-saas-tinfoil-security-tutorial/ic798972.png "보안")</span><span class="sxs-lookup"><span data-stu-id="366d5-182">![Security](./media/active-directory-saas-tinfoil-security-tutorial/ic798972.png "Security")</span></span>

11. <span data-ttu-id="366d5-183">**Single Sign-On** 구성 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-183">On the **Single Sign-On** configuration page, perform the following steps:</span></span>
   
    <span data-ttu-id="366d5-184">![Single Sign-On](./media/active-directory-saas-tinfoil-security-tutorial/ic798973.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="366d5-184">![Single Sign-On](./media/active-directory-saas-tinfoil-security-tutorial/ic798973.png "Single Sign-On")</span></span>
   
    <span data-ttu-id="366d5-185">a.</span><span class="sxs-lookup"><span data-stu-id="366d5-185">a.</span></span> <span data-ttu-id="366d5-186">**SAML 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-186">Select **Enable SAML**.</span></span>
   
    <span data-ttu-id="366d5-187">b.</span><span class="sxs-lookup"><span data-stu-id="366d5-187">b.</span></span> <span data-ttu-id="366d5-188">**수동 구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-188">Click **Manual Configuration**.</span></span>
   
    <span data-ttu-id="366d5-189">c.</span><span class="sxs-lookup"><span data-stu-id="366d5-189">c.</span></span> <span data-ttu-id="366d5-190">**SAML Post URL** 텍스트 상자에 Azure Portal에서 복사한 **SAML Single Sign-On 서비스 URL** 값을 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-190">In **SAML Post URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal</span></span>
   
    <span data-ttu-id="366d5-191">d.</span><span class="sxs-lookup"><span data-stu-id="366d5-191">d.</span></span> <span data-ttu-id="366d5-192">**SAML Certificate Fingerprint**(SAML 인증서 지문) 텍스트 상자에 **SAML 서명 인증서** 섹션에서 복사한 **지문** 값을 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-192">In **SAML Certificate Fingerprint** textbox, paste the value of **Thumbprint** which you have copied from **SAML Signing Certificate** section.</span></span>
  
    <span data-ttu-id="366d5-193">e.</span><span class="sxs-lookup"><span data-stu-id="366d5-193">e.</span></span> <span data-ttu-id="366d5-194">**Your Account ID**(사용자의 계정 ID) 값을 복사하여 Azure Portal에서 **특성 추가** 섹션의 **특성 값** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-194">Copy **Your Account ID** value and paste the value in **Attribute Value** textbox under **Add Attribute** section in Azure portal.</span></span>
   
    <span data-ttu-id="366d5-195">f.</span><span class="sxs-lookup"><span data-stu-id="366d5-195">f.</span></span> <span data-ttu-id="366d5-196">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-196">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="366d5-197">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-197">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="366d5-198">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-198">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="366d5-199">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-199">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="366d5-200">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="366d5-200">Create an Azure AD test user</span></span>
<span data-ttu-id="366d5-201">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-201">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="366d5-203">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="366d5-203">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="366d5-204">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-204">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="366d5-206">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-206">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![<span data-ttu-id="366d5-207">사용자 및 그룹 -> 모든 사용자</span><span class="sxs-lookup"><span data-stu-id="366d5-207">Users and groups -> All users</span></span> ](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="366d5-208">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-208">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![사용자](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="366d5-210">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-210">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="366d5-212">a.</span><span class="sxs-lookup"><span data-stu-id="366d5-212">a.</span></span> <span data-ttu-id="366d5-213">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-213">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="366d5-214">b.</span><span class="sxs-lookup"><span data-stu-id="366d5-214">b.</span></span> <span data-ttu-id="366d5-215">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-215">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="366d5-216">c.</span><span class="sxs-lookup"><span data-stu-id="366d5-216">c.</span></span> <span data-ttu-id="366d5-217">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-217">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="366d5-218">d.</span><span class="sxs-lookup"><span data-stu-id="366d5-218">d.</span></span> <span data-ttu-id="366d5-219">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-219">Click **Create**.</span></span>
 
### <a name="create-a-tinfoil-security-test-user"></a><span data-ttu-id="366d5-220">TINFOIL SECURITY 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="366d5-220">Create a TINFOIL SECURITY test user</span></span>

<span data-ttu-id="366d5-221">Azure AD 사용자가 TINFOIL SECURITY에 로그인할 수 있게 하려면 TINFOIL SECURITY로 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-221">In order to enable Azure AD users to log into TINFOIL SECURITY, they must be provisioned into TINFOIL SECURITY.</span></span> <span data-ttu-id="366d5-222">TINFOIL SECURITY의 경우 프로비전이 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-222">In the case of TINFOIL SECURITY, provisioning is a manual task.</span></span>

<span data-ttu-id="366d5-223">**사용자를 프로비전하려면 다음 단계를 따르십시오.**</span><span class="sxs-lookup"><span data-stu-id="366d5-223">**To get a user provisioned, perform the following steps:**</span></span>

1. <span data-ttu-id="366d5-224">사용자가 엔터프라이즈 계정의 일부라면 [TINFOIL SECURITY 지원 팀에 문의](https://www.tinfoilsecurity.com/contact)하여 사용자 계정을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-224">If the user is a part of an Enterprise account, you need to [contact the TINFOIL SECURITY support team](https://www.tinfoilsecurity.com/contact) to get the user account created.</span></span>

2. <span data-ttu-id="366d5-225">사용자가 일반적인 TINFOIL SECURITY SaaS 사용자라면 사용자는 원하는 사용자 사이트에 협력자를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-225">If the user is a regular TINFOIL SECURITY SaaS user, then the user can add a collaborator to any of the user’s sites.</span></span> <span data-ttu-id="366d5-226">그러면 지정된 이메일로 초대장을 보내는 프로세스가 트리거되고 새로운 TINFOIL SECURITY 사용자 계정이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-226">This triggers a process to send an invitation to the specified email to create a new TINFOIL SECURITY user account.</span></span>

> [!NOTE]
> <span data-ttu-id="366d5-227">다른 TINFOIL SECURITY 사용자 계정 생성 도구 또는 TINFOIL SECURITY가 제공한 API를 사용하여 Azure AD 사용자 계정을 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-227">You can use any other TINFOIL SECURITY user account creation tools or APIs provided by TINFOIL SECURITY to provision Azure AD user accounts.</span></span>
> 
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="366d5-228">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="366d5-228">Assign the Azure AD test user</span></span>

<span data-ttu-id="366d5-229">이 섹션에서는 Britta Simon이 Azure Single Sign-On을 사용할 수 있도록 TINFOIL SECURITY에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-229">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TINFOIL SECURITY.</span></span>

![사용자 할당][200] 

<span data-ttu-id="366d5-231">**Britta Simon을 TINFOIL SECURITY에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="366d5-231">**To assign Britta Simon to TINFOIL SECURITY, perform the following steps:**</span></span>

1. <span data-ttu-id="366d5-232">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-232">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="366d5-234">응용 프로그램 목록에서 **TINFOIL SECURITY**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-234">In the applications list, select **TINFOIL SECURITY**.</span></span>

    ![TINFOIL SECURITY 선택](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_app.png) 

3. <span data-ttu-id="366d5-236">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-236">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="366d5-238">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-238">Click **Add** button.</span></span> <span data-ttu-id="366d5-239">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="366d5-241">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-241">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="366d5-242">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="366d5-243">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="366d5-244">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="366d5-244">Test single sign-on</span></span>

<span data-ttu-id="366d5-245">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-245">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="366d5-246">액세스 패널에서 TINFOIL SECURITY 타일을 클릭하면 TINFOIL SECURITY 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-246">When you click the TINFOIL SECURITY tile in the Access Panel, you should get automatically signed-on to your TINFOIL SECURITY application.</span></span> <span data-ttu-id="366d5-247">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="366d5-247">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="366d5-248">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="366d5-248">Additional resources</span></span>

* [<span data-ttu-id="366d5-249">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="366d5-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="366d5-250">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="366d5-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_203.png

