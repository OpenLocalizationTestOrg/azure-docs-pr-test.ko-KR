---
title: "자습서: Hightail과 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 Hightail 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e15206ac-74b0-46e4-9329-892c7d242ec0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: ba55f9b62d274aa3eb91723c62b53f54de0891b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hightail"></a><span data-ttu-id="003d1-103">자습서:Azure Active Directory와 Hightail 통합</span><span class="sxs-lookup"><span data-stu-id="003d1-103">Tutorial: Azure Active Directory integration with Hightail</span></span>

<span data-ttu-id="003d1-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Hightail을 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-104">In this tutorial, you learn how to integrate Hightail with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="003d1-105">Hightail을 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-105">Integrating Hightail with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="003d1-106">Hightail에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-106">You can control in Azure AD who has access to Hightail</span></span>
- <span data-ttu-id="003d1-107">사용자가 해당 Azure AD 계정으로 Hightail에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-107">You can enable your users to automatically get signed-on to Hightail (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="003d1-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="003d1-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="003d1-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="003d1-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="003d1-110">Prerequisites</span></span>

<span data-ttu-id="003d1-111">Hightail과 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-111">To configure Azure AD integration with Hightail, you need the following items:</span></span>

- <span data-ttu-id="003d1-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="003d1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="003d1-113">Hightail Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="003d1-113">A Hightail single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="003d1-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="003d1-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="003d1-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="003d1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="003d1-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="003d1-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="003d1-118">Scenario description</span></span>
<span data-ttu-id="003d1-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="003d1-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="003d1-121">갤러리에서 Hightail 추가</span><span class="sxs-lookup"><span data-stu-id="003d1-121">Adding Hightail from the gallery</span></span>
2. <span data-ttu-id="003d1-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="003d1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hightail-from-the-gallery"></a><span data-ttu-id="003d1-123">갤러리에서 Hightail 추가</span><span class="sxs-lookup"><span data-stu-id="003d1-123">Adding Hightail from the gallery</span></span>
<span data-ttu-id="003d1-124">Hightail과 Azure AD 통합을 구성하려면 갤러리의 Hightail을 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-124">To configure the integration of Hightail into Azure AD, you need to add Hightail from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="003d1-125">**갤러리에서 Hightail을 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="003d1-125">**To add Hightail from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="003d1-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="003d1-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="003d1-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="003d1-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="003d1-133">검색 상자에 **Hightail**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-133">In the search box, type **Hightail**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_search.png)

5. <span data-ttu-id="003d1-135">결과 패널에서 **Hightail**을 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-135">In the results panel, select **Hightail**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="003d1-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="003d1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="003d1-138">이 섹션에서는 “Britta Simon”이라는 테스트 사용자를 기반으로 Hightail에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-138">In this section, you configure and test Azure AD single sign-on with Hightail based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="003d1-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Hightail 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Hightail is to a user in Azure AD.</span></span> <span data-ttu-id="003d1-140">즉, Azure AD 사용자 및 Hightail의 관련 사용자 간에 연결이 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-140">In other words, a link relationship between an Azure AD user and the related user in Hightail needs to be established.</span></span>

<span data-ttu-id="003d1-141">Hightail에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-141">In Hightail, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="003d1-142">Hightail에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-142">To configure and test Azure AD single sign-on with Hightail, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="003d1-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="003d1-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="003d1-145">**[Hightail 테스트 사용자 만들기](#creating-a-hightail-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 Hightail에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-145">**[Creating a Hightail test user](#creating-a-hightail-test-user)** - to have a counterpart of Britta Simon in Hightail that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="003d1-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="003d1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="003d1-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="003d1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="003d1-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Hightail 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Hightail application.</span></span>

<span data-ttu-id="003d1-150">**Hightail에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="003d1-150">**To configure Azure AD single sign-on with Hightail, perform the following steps:**</span></span>

1. <span data-ttu-id="003d1-151">Azure Portal의 **Hightail** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-151">In the Azure portal, on the **Hightail** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="003d1-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_samlbase.png)

3. <span data-ttu-id="003d1-155">**Hightail 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-155">On the **Hightail Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_url.png)

     <span data-ttu-id="003d1-157">**회신 URL** 텍스트 상자에서 URL `https://www.hightail.com/samlLogin?phi_action=app/samlLogin&subAction=handleSamlResponse`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-157">In the **Reply URL** textbox, type the URL as: `https://www.hightail.com/samlLogin?phi_action=app/samlLogin&subAction=handleSamlResponse`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="003d1-158">위의 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-158">The preceding value is not real value.</span></span> <span data-ttu-id="003d1-159">자습서 뒷부분에 설명된 실제 회신 URL로 값을 업데이트하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-159">You will update the value with the actual Reply URL, which is explained later in the tutorial.</span></span>
 
4. <span data-ttu-id="003d1-160">**Hightail 도메인 및 URL** 섹션에서 **SP 시작 모드**로 응용 프로그램을 구성하려는 경우 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-160">On the **Hightail Domain and URLs** section, If you wish to configure the application in **SP initiated mode**, perform the following steps:</span></span>
    
    ![Single Sign-on 구성](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_url1.png)

    <span data-ttu-id="003d1-162">a.</span><span class="sxs-lookup"><span data-stu-id="003d1-162">a.</span></span> <span data-ttu-id="003d1-163">**고급 URL 설정 표시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-163">Click the **Show advanced URL settings**.</span></span>

    <span data-ttu-id="003d1-164">b.</span><span class="sxs-lookup"><span data-stu-id="003d1-164">b.</span></span> <span data-ttu-id="003d1-165">**로그온 URL** 텍스트 상자에서 URL `https://www.hightail.com/loginSSO`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-165">In the **Sign On URL** textbox, type the URL as: `https://www.hightail.com/loginSSO`</span></span>

4. <span data-ttu-id="003d1-166">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-166">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_certificate.png) 

5. <span data-ttu-id="003d1-168">Hightail 응용 프로그램은 특정 형식의 SAML 어설션이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-168">Hightail application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="003d1-169">이 응용 프로그램에 대한 다음 클레임을 구성하세요.</span><span class="sxs-lookup"><span data-stu-id="003d1-169">Please configure the following claims for this application.</span></span> <span data-ttu-id="003d1-170">응용 프로그램의 **"특성"** 탭에서 이러한 특성의 값을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-170">You can manage the values of these attributes from the **"Atrribute"** tab of the application.</span></span> <span data-ttu-id="003d1-171">다음 스크린샷은 이에 대한 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-171">The following screenshot shows an example for this.</span></span> 

    ![Single Sign-on 구성](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_attribute.png) 

6. <span data-ttu-id="003d1-173">**Single Sign-On** 대화 상자의 **사용자 특성** 섹션에서 이미지에 표시된 것과 같이 SAML 토큰 특성을 구성하고 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-173">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="003d1-174">특성 이름</span><span class="sxs-lookup"><span data-stu-id="003d1-174">Attribute Name</span></span> | <span data-ttu-id="003d1-175">특성 값</span><span class="sxs-lookup"><span data-stu-id="003d1-175">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="003d1-176">FirstName</span><span class="sxs-lookup"><span data-stu-id="003d1-176">FirstName</span></span> | <span data-ttu-id="003d1-177">user.givenname</span><span class="sxs-lookup"><span data-stu-id="003d1-177">user.givenname</span></span> |
    | <span data-ttu-id="003d1-178">LastName</span><span class="sxs-lookup"><span data-stu-id="003d1-178">LastName</span></span> | <span data-ttu-id="003d1-179">user.surname</span><span class="sxs-lookup"><span data-stu-id="003d1-179">user.surname</span></span> |
    | <span data-ttu-id="003d1-180">Email</span><span class="sxs-lookup"><span data-stu-id="003d1-180">Email</span></span> | <span data-ttu-id="003d1-181">user.mail</span><span class="sxs-lookup"><span data-stu-id="003d1-181">user.mail</span></span> |    
    | <span data-ttu-id="003d1-182">UserIdentity</span><span class="sxs-lookup"><span data-stu-id="003d1-182">UserIdentity</span></span> | <span data-ttu-id="003d1-183">user.mail</span><span class="sxs-lookup"><span data-stu-id="003d1-183">user.mail</span></span> |
    
    <span data-ttu-id="003d1-184">a.</span><span class="sxs-lookup"><span data-stu-id="003d1-184">a.</span></span> <span data-ttu-id="003d1-185">**특성 추가**를 클릭하여 **특성 추가** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-185">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-hightail-tutorial/tutorial_officespace_04.png)

    ![Single Sign-on 구성](./media/active-directory-saas-hightail-tutorial/tutorial_officespace_05.png)

    <span data-ttu-id="003d1-188">b.</span><span class="sxs-lookup"><span data-stu-id="003d1-188">b.</span></span> <span data-ttu-id="003d1-189">**이름** 텍스트 상자에서 해당 행에 표시된 특성 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-189">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="003d1-190">c.</span><span class="sxs-lookup"><span data-stu-id="003d1-190">c.</span></span> <span data-ttu-id="003d1-191">**값** 목록에서 해당 행에 대해 표시된 특성을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-191">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="003d1-192">d.</span><span class="sxs-lookup"><span data-stu-id="003d1-192">d.</span></span> <span data-ttu-id="003d1-193">**네임스페이스**를 비워 둡니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-193">Leave the **Namespace** blank.</span></span>
    
    <span data-ttu-id="003d1-194">e.</span><span class="sxs-lookup"><span data-stu-id="003d1-194">e.</span></span> <span data-ttu-id="003d1-195">**Ok**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-195">Click **Ok**.</span></span>

7. <span data-ttu-id="003d1-196">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-196">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-hightail-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="003d1-198">**Hightail 구성** 섹션에서 **Hightail 구성**을 클릭하여 **로그인 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-198">On the **Hightail Configuration** section, click **Configure Hightail** to open **Configure sign-on** window.</span></span> <span data-ttu-id="003d1-199">**빠른 참조 섹션**에서 **SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-199">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_configure.png) 

    >[!NOTE] 
    ><span data-ttu-id="003d1-201">Hightail 앱에서 Single Sign On을 구성하기 전에 이 도메인을 사용하는 모든 사용자가 Single Sign On 기능을 활용할 수 있도록 Hightail 팀을 통해 전자 메일 도메인을 허용 목록에 포함시키세요.</span><span class="sxs-lookup"><span data-stu-id="003d1-201">Before configuring the Single Sign On at Hightail app, please white list your email domain with Hightail team so that all the users who are using this domain can use Single Sign On functionality.</span></span>


9. <span data-ttu-id="003d1-202">응용 프로그램에 대해 구성된 SSO를 가져오려면 관리자 권한으로 Hightail 테넌트에 로그온해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-202">To get SSO configured for your application, you need to sign-on to your Hightail tenant as an administrator.</span></span>
   
    <span data-ttu-id="003d1-203">a.</span><span class="sxs-lookup"><span data-stu-id="003d1-203">a.</span></span> <span data-ttu-id="003d1-204">위쪽 메뉴에서 **계정** 탭을 클릭하고 **SAML 구성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-204">In the menu on the top, click the **Account** tab and select **Configure SAML**.</span></span>
 
    ![Single Sign-On 구성](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_001.png) 

    <span data-ttu-id="003d1-206">b.</span><span class="sxs-lookup"><span data-stu-id="003d1-206">b.</span></span> <span data-ttu-id="003d1-207">**SAML 인증 사용**확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-207">Select the checkbox of **Enable SAML Authentication**.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_002.png) 

    <span data-ttu-id="003d1-209">c.</span><span class="sxs-lookup"><span data-stu-id="003d1-209">c.</span></span> <span data-ttu-id="003d1-210">Azure Portal에서 다운로드한 base-64로 인코딩된 인증서를 메모장에서 열고, 콘텐츠를 클립보드에 복사한 다음, **SAML 토큰 서명 인증서** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-210">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **SAML Token Signing Certificate** textbox.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_003.png) 

    <span data-ttu-id="003d1-212">d.</span><span class="sxs-lookup"><span data-stu-id="003d1-212">d.</span></span> <span data-ttu-id="003d1-213">Azure Portal에서 복사한 **SAML Single Sign-On 서비스 URL** 값을 **SAML 인증 기관(ID 공급자)** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-213">In the **SAML Authority (Identity Provider)** textbox, paste the value of **SAML Single Sign-On Service URL** copied from Azure portal.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_004.png)

    <span data-ttu-id="003d1-215">e.</span><span class="sxs-lookup"><span data-stu-id="003d1-215">e.</span></span> <span data-ttu-id="003d1-216">**IDP 시작 모드**로 응용 프로그램을 구성하려는 경우 **"IdP(ID 공급자) 시작 로그인"**을 선택하고,</span><span class="sxs-lookup"><span data-stu-id="003d1-216">If you wish to configure the application in **IDP initiated mode** select **"Identity Provider (IdP) initiated log in"**.</span></span> <span data-ttu-id="003d1-217">**SP 시작 모드**로 응용 프로그램을 구성하려는 경우 **"SP(서비스 공급자) 시작 로그인"**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-217">If **SP initiated mode** select **"Service Provider (SP) initiated log in"**.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_006.png)

    <span data-ttu-id="003d1-219">f.</span><span class="sxs-lookup"><span data-stu-id="003d1-219">f.</span></span> <span data-ttu-id="003d1-220">인스턴스에 대한 SAML 소비자 URL을 복사하여 Azure Portal의 **Hightail 도메인 및 URL**에서 **회신 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-220">Copy the SAML consumer URL for your instance and paste it in **Reply URL** textbox in **Hightail Domain and URLs** section on Azure portal.</span></span>
    
    <span data-ttu-id="003d1-221">g.</span><span class="sxs-lookup"><span data-stu-id="003d1-221">g.</span></span> <span data-ttu-id="003d1-222">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-222">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="003d1-223">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-223">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="003d1-224">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-224">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="003d1-225">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-225">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="003d1-226">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="003d1-226">Creating an Azure AD test user</span></span>
<span data-ttu-id="003d1-227">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-227">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="003d1-229">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="003d1-229">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="003d1-230">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-230">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-hightail-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="003d1-232">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-232">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-hightail-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="003d1-234">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-234">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-hightail-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="003d1-236">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-236">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-hightail-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="003d1-238">a.</span><span class="sxs-lookup"><span data-stu-id="003d1-238">a.</span></span> <span data-ttu-id="003d1-239">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-239">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="003d1-240">b.</span><span class="sxs-lookup"><span data-stu-id="003d1-240">b.</span></span> <span data-ttu-id="003d1-241">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-241">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="003d1-242">c.</span><span class="sxs-lookup"><span data-stu-id="003d1-242">c.</span></span> <span data-ttu-id="003d1-243">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-243">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="003d1-244">d.</span><span class="sxs-lookup"><span data-stu-id="003d1-244">d.</span></span> <span data-ttu-id="003d1-245">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-245">Click **Create**.</span></span>
 
### <a name="creating-a-hightail-test-user"></a><span data-ttu-id="003d1-246">Hightail 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="003d1-246">Creating a Hightail test user</span></span>

<span data-ttu-id="003d1-247">이 섹션은 Hightail에서 Britta Simon이라는 사용자를 만들기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-247">The objective of this section is to create a user called Britta Simon in Hightail.</span></span> 

<span data-ttu-id="003d1-248">이 섹션에 작업 항목이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-248">There is no action item for you in this section.</span></span> <span data-ttu-id="003d1-249">Hightail은 사용자 지정 클레임을 기반으로 하는 Just-In-Time 사용자 프로비전을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-249">Hightail supports just-in-time user provisioning based on the custom claims.</span></span> <span data-ttu-id="003d1-250">위의 **[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** 섹션에 나와 있는 것처럼 사용자 지정 클레임을 구성한 경우 사용자가 없으면 응용 프로그램에 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-250">If you have configured the custom claims as shown in the section **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** above, a user is automatically created in the application it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="003d1-251">사용자를 수동으로 만들어야 하는 경우 [Hightail 지원 팀](mailto:support@hightail.com)에 문의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-251">If you need to create a user manually, you need to contact the [Hightail support team](mailto:support@hightail.com).</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="003d1-252">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="003d1-252">Assigning the Azure AD test user</span></span>

<span data-ttu-id="003d1-253">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Hightail에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-253">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Hightail.</span></span>

![사용자 할당][200] 

<span data-ttu-id="003d1-255">**Britta Simon을 Hightail에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="003d1-255">**To assign Britta Simon to Hightail, perform the following steps:**</span></span>

1. <span data-ttu-id="003d1-256">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-256">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="003d1-258">응용 프로그램 목록에서 **Hightail**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-258">In the applications list, select **Hightail**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_app.png) 

3. <span data-ttu-id="003d1-260">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-260">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="003d1-262">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-262">Click **Add** button.</span></span> <span data-ttu-id="003d1-263">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-263">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="003d1-265">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-265">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="003d1-266">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-266">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="003d1-267">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-267">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="003d1-268">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="003d1-268">Testing single sign-on</span></span>

<span data-ttu-id="003d1-269">이 섹션은 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-269">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="003d1-270">액세스 패널에서 Hightail 타일을 클릭하면 Hightail 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="003d1-270">When you click the Hightail tile in the Access Panel, you should get automatically signed-on to your Hightail application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="003d1-271">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="003d1-271">Additional resources</span></span>

* [<span data-ttu-id="003d1-272">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="003d1-272">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="003d1-273">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="003d1-273">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_203.png

