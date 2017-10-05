---
title: "자습서: Allocadia와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory 및 Allocadia 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c415fc55-6dc1-49f2-a8a2-2fc6e3790d65
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: jeedes
ms.openlocfilehash: 8e97c365383ecdb72cc1cd449b522b75875fc1db
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-allocadia"></a><span data-ttu-id="5dad8-103">자습서: Allocadia와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="5dad8-103">Tutorial: Azure Active Directory integration with Allocadia</span></span>

<span data-ttu-id="5dad8-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Allocadia를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-104">In this tutorial, you learn how to integrate Allocadia with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5dad8-105">Allocadia를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-105">Integrating Allocadia with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5dad8-106">Allocadia에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-106">You can control in Azure AD who has access to Allocadia</span></span>
- <span data-ttu-id="5dad8-107">사용자가 해당 Azure AD 계정으로 Allocadia에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-107">You can enable your users to automatically get signed-on to Allocadia (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5dad8-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="5dad8-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5dad8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5dad8-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="5dad8-110">Prerequisites</span></span>

<span data-ttu-id="5dad8-111">Allocadia와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-111">To configure Azure AD integration with Allocadia, you need the following items:</span></span>

- <span data-ttu-id="5dad8-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="5dad8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5dad8-113">Allocadia Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="5dad8-113">An Allocadia single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5dad8-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5dad8-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5dad8-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="5dad8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5dad8-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5dad8-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="5dad8-118">Scenario description</span></span>
<span data-ttu-id="5dad8-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5dad8-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5dad8-121">갤러리에서 Allocadia 추가</span><span class="sxs-lookup"><span data-stu-id="5dad8-121">Adding Allocadia from the gallery</span></span>
2. <span data-ttu-id="5dad8-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="5dad8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-allocadia-from-the-gallery"></a><span data-ttu-id="5dad8-123">갤러리에서 Allocadia 추가</span><span class="sxs-lookup"><span data-stu-id="5dad8-123">Adding Allocadia from the gallery</span></span>
<span data-ttu-id="5dad8-124">Allocadia의 Azure AD 통합을 구성하려면 갤러리의 Allocadia를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-124">To configure the integration of Allocadia into Azure AD, you need to add Allocadia from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5dad8-125">**갤러리에서 Allocadia를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="5dad8-125">**To add Allocadia from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5dad8-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5dad8-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5dad8-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="5dad8-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="5dad8-133">검색 상자에 **Allocadia**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-133">In the search box, type **Allocadia**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_search.png)

5. <span data-ttu-id="5dad8-135">결과 패널에서 **Allocadia**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-135">In the results panel, select **Allocadia**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5dad8-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="5dad8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5dad8-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Allocadia에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-138">In this section, you configure and test Azure AD single sign-on with Allocadia based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="5dad8-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Allocadia 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Allocadia is to a user in Azure AD.</span></span> <span data-ttu-id="5dad8-140">즉, Azure AD 사용자와 Allocadia의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-140">In other words, a link relationship between an Azure AD user and the related user in Allocadia needs to be established.</span></span>

<span data-ttu-id="5dad8-141">Allocadia에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-141">In Allocadia, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="5dad8-142">Allocadia에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-142">To configure and test Azure AD single sign-on with Allocadia, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5dad8-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5dad8-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5dad8-145">**[Allocadia 테스트 사용자 만들기](#creating-an-allocadia-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 Allocadia에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-145">**[Creating an Allocadia test user](#creating-an-allocadia-test-user)** - to have a counterpart of Britta Simon in Allocadia that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5dad8-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5dad8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5dad8-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="5dad8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5dad8-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Allocadia 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Allocadia application.</span></span>

<span data-ttu-id="5dad8-150">**Allocadia에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="5dad8-150">**To configure Azure AD single sign-on with Allocadia, perform the following steps:**</span></span>

1. <span data-ttu-id="5dad8-151">Azure Portal의 **Allocadia** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-151">In the Azure portal, on the **Allocadia** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="5dad8-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_samlbase.png)

3. <span data-ttu-id="5dad8-155">**Allocadia 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-155">On the **Allocadia Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_url.png)

    <span data-ttu-id="5dad8-157">a.</span><span class="sxs-lookup"><span data-stu-id="5dad8-157">a.</span></span> <span data-ttu-id="5dad8-158">**식별자** 텍스트 상자에서 다음 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-158">In the **Identifier** textbox, type a URL using the following patterns:</span></span> 
       
     <span data-ttu-id="5dad8-159">테스트 환경의 경우 - `https://na2standby.allocadia.com`</span><span class="sxs-lookup"><span data-stu-id="5dad8-159">For test environment -  `https://na2standby.allocadia.com`</span></span>
    
     <span data-ttu-id="5dad8-160">프로덕션 환경의 경우 - `https://na2.allocadia.com`</span><span class="sxs-lookup"><span data-stu-id="5dad8-160">For production environment - `https://na2.allocadia.com`</span></span>

    <span data-ttu-id="5dad8-161">b.</span><span class="sxs-lookup"><span data-stu-id="5dad8-161">b.</span></span> <span data-ttu-id="5dad8-162">**회신 URL** 텍스트 상자에 다음 패턴으로 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-162">In the **Reply URL** textbox, type a URL using the following patterns:</span></span> 
    
     <span data-ttu-id="5dad8-163">테스트 환경의 경우 - `https://na2standby.allocadia.com/allocadia/saml/SSO`</span><span class="sxs-lookup"><span data-stu-id="5dad8-163">For test environment - `https://na2standby.allocadia.com/allocadia/saml/SSO`</span></span>
    
     <span data-ttu-id="5dad8-164">프로덕션 환경의 경우 - `https://na2.allocadia.com/allocadia/saml/SSO`</span><span class="sxs-lookup"><span data-stu-id="5dad8-164">For production environment - `https://na2.allocadia.com/allocadia/saml/SSO`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5dad8-165">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-165">These values are not real.</span></span> <span data-ttu-id="5dad8-166">실제 식별자 및 회신 URL로 해당 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-166">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="5dad8-167">이러한 값을 가져오려면 [Allocadia 지원팀](mailTo:support@allocadia.com)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="5dad8-167">Contact [Allocadia support team](mailTo:support@allocadia.com) to get these values.</span></span>

4. <span data-ttu-id="5dad8-168">Allocadia 응용 프로그램은 특정 형식의 SAML 어설션이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-168">Allocadia application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="5dad8-169">이 응용 프로그램에 대해 다음 클레임을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-169">Configure the following claims for this application.</span></span> <span data-ttu-id="5dad8-170">응용 프로그램 통합 페이지의 **"사용자 특성"** 섹션에서 이러한 특성의 값을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-170">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="5dad8-171">다음 스크린샷은 이 구성에 대한 예제를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-171">The following screenshot shows an example for this configuration.</span></span> 

    ![Single Sign-on 구성](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_attributes.png)
    
5. <span data-ttu-id="5dad8-173">**Single Sign-On** 대화 상자의 **사용자 특성** 섹션에서 이미지에 표시된 것과 같이 SAML 토큰 특성을 구성하고 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-173">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="5dad8-174">특성 이름</span><span class="sxs-lookup"><span data-stu-id="5dad8-174">Attribute Name</span></span> | <span data-ttu-id="5dad8-175">특성 값</span><span class="sxs-lookup"><span data-stu-id="5dad8-175">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="5dad8-176">firstname</span><span class="sxs-lookup"><span data-stu-id="5dad8-176">firstname</span></span> | <span data-ttu-id="5dad8-177">user.givenname</span><span class="sxs-lookup"><span data-stu-id="5dad8-177">user.givenname</span></span> |
    | <span data-ttu-id="5dad8-178">lastname</span><span class="sxs-lookup"><span data-stu-id="5dad8-178">lastname</span></span> | <span data-ttu-id="5dad8-179">user.surname</span><span class="sxs-lookup"><span data-stu-id="5dad8-179">user.surname</span></span> |
    | <span data-ttu-id="5dad8-180">email</span><span class="sxs-lookup"><span data-stu-id="5dad8-180">email</span></span> | <span data-ttu-id="5dad8-181">user.mail</span><span class="sxs-lookup"><span data-stu-id="5dad8-181">user.mail</span></span> |
    
    <span data-ttu-id="5dad8-182">a.</span><span class="sxs-lookup"><span data-stu-id="5dad8-182">a.</span></span> <span data-ttu-id="5dad8-183">**특성 추가**를 클릭하여 **특성 추가** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-183">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-allocadia-tutorial/tutorial_attribute_04.png)

    <span data-ttu-id="5dad8-185">b.</span><span class="sxs-lookup"><span data-stu-id="5dad8-185">b.</span></span> <span data-ttu-id="5dad8-186">**이름** 텍스트 상자에서 해당 행에 표시된 특성 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-186">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-allocadia-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="5dad8-188">c.</span><span class="sxs-lookup"><span data-stu-id="5dad8-188">c.</span></span> <span data-ttu-id="5dad8-189">**값** 목록에서 해당 행에 대해 표시된 특성을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-189">From the **Value** list, type the attribute value shown for that row.</span></span>
 
    <span data-ttu-id="5dad8-190">d.</span><span class="sxs-lookup"><span data-stu-id="5dad8-190">d.</span></span> <span data-ttu-id="5dad8-191">**Ok**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-191">Click **Ok**.</span></span>



6. <span data-ttu-id="5dad8-192">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 메타데이터 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-192">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_certificate.png) 


7. <span data-ttu-id="5dad8-194">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-194">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-allocadia-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="5dad8-196">**Allocadia** 쪽에서 Single Sign-On을 구성하려면 다운로드한 **메타데이터 XML**을 [Allocadia 지원팀](mailTo:support@allocadia.com)에 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-196">To configure single sign-on on **Allocadia** side, you need to send the downloaded **Metadata XML** to [Allocadia support team](mailTo:support@allocadia.com).</span></span> <span data-ttu-id="5dad8-197">이렇게 설정하면 SAML SSO 연결이 양쪽에서 제대로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-197">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="5dad8-198">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-198">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5dad8-199">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-199">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5dad8-200">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-200">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5dad8-201">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="5dad8-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="5dad8-202">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-202">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="5dad8-204">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="5dad8-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5dad8-205">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-205">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-allocadia-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5dad8-207">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-207">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-allocadia-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5dad8-209">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-209">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-allocadia-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5dad8-211">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-211">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-allocadia-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5dad8-213">a.</span><span class="sxs-lookup"><span data-stu-id="5dad8-213">a.</span></span> <span data-ttu-id="5dad8-214">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-214">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5dad8-215">b.</span><span class="sxs-lookup"><span data-stu-id="5dad8-215">b.</span></span> <span data-ttu-id="5dad8-216">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-216">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5dad8-217">c.</span><span class="sxs-lookup"><span data-stu-id="5dad8-217">c.</span></span> <span data-ttu-id="5dad8-218">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-218">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="5dad8-219">d.</span><span class="sxs-lookup"><span data-stu-id="5dad8-219">d.</span></span> <span data-ttu-id="5dad8-220">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-220">Click **Create**.</span></span>
 
### <a name="creating-an-allocadia-test-user"></a><span data-ttu-id="5dad8-221">Allocadia 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="5dad8-221">Creating an Allocadia test user</span></span>

<span data-ttu-id="5dad8-222">응용 프로그램은 Just-In-Time 사용자 프로비전만을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-222">Application supports Just in time user provisioning.</span></span> <span data-ttu-id="5dad8-223">인증 후 사용자가 응용 프로그램에서 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-223">After authentication users are created in the application automatically.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="5dad8-224">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="5dad8-224">Assigning the Azure AD test user</span></span>

<span data-ttu-id="5dad8-225">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Allocadia에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-225">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Allocadia.</span></span>

![사용자 할당][200] 

<span data-ttu-id="5dad8-227">**Britta Simon을 Allocadia에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="5dad8-227">**To assign Britta Simon to Allocadia, perform the following steps:**</span></span>

1. <span data-ttu-id="5dad8-228">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-228">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="5dad8-230">응용 프로그램 목록에서 **Allocadia**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-230">In the applications list, select **Allocadia**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_app.png) 

3. <span data-ttu-id="5dad8-232">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-232">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="5dad8-234">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-234">Click **Add** button.</span></span> <span data-ttu-id="5dad8-235">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="5dad8-237">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-237">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5dad8-238">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5dad8-239">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5dad8-240">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="5dad8-240">Testing single sign-on</span></span>

<span data-ttu-id="5dad8-241">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-241">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="5dad8-242">액세스 패널에서 Allocadia 타일을 클릭하면 Allocadia 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="5dad8-242">When you click the Allocadia tile in the Access Panel, you should get automatically signed-on to your Allocadia application.</span></span>
<span data-ttu-id="5dad8-243">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5dad8-243">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md)</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5dad8-244">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="5dad8-244">Additional resources</span></span>

* [<span data-ttu-id="5dad8-245">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="5dad8-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5dad8-246">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="5dad8-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_203.png

