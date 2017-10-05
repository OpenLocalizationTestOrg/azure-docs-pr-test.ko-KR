---
title: "자습서: Moxtra와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 Moxtra 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2aed2d4b-1dcd-4839-8fed-9419d107c61c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: db2f041a44b6771b0a4f734e58d899298ef0847b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-moxtra"></a><span data-ttu-id="e760f-103">자습서: Moxtra와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="e760f-103">Tutorial: Azure Active Directory integration with Moxtra</span></span>

<span data-ttu-id="e760f-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Moxtra를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-104">In this tutorial, you learn how to integrate Moxtra with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e760f-105">Moxtra를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-105">Integrating Moxtra with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e760f-106">Moxtra에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-106">You can control in Azure AD who has access to Moxtra</span></span>
- <span data-ttu-id="e760f-107">사용자가 해당 Azure AD 계정으로 Moxtra에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-107">You can enable your users to automatically get signed-on to Moxtra (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e760f-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e760f-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e760f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e760f-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="e760f-110">Prerequisites</span></span>

<span data-ttu-id="e760f-111">Moxtra와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-111">To configure Azure AD integration with Moxtra, you need the following items:</span></span>

- <span data-ttu-id="e760f-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="e760f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e760f-113">Moxtra Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="e760f-113">A Moxtra single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e760f-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e760f-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e760f-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="e760f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e760f-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e760f-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="e760f-118">Scenario description</span></span>
<span data-ttu-id="e760f-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e760f-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e760f-121">갤러리에서 Moxtra 추가</span><span class="sxs-lookup"><span data-stu-id="e760f-121">Adding Moxtra from the gallery</span></span>
2. <span data-ttu-id="e760f-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="e760f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-moxtra-from-the-gallery"></a><span data-ttu-id="e760f-123">갤러리에서 Moxtra 추가</span><span class="sxs-lookup"><span data-stu-id="e760f-123">Adding Moxtra from the gallery</span></span>
<span data-ttu-id="e760f-124">Moxtra의 Azure AD 통합을 구성하려면 갤러리의 Moxtra를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-124">To configure the integration of Moxtra into Azure AD, you need to add Moxtra from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e760f-125">**갤러리에서 Moxtra를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="e760f-125">**To add Moxtra from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e760f-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e760f-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e760f-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="e760f-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="e760f-133">검색 상자에 **Moxtra**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-133">In the search box, type **Moxtra**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_search.png)

5. <span data-ttu-id="e760f-135">결과 패널에서 **Moxtra**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-135">In the results panel, select **Moxtra**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e760f-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="e760f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e760f-138">이 섹션에서는 “Britta Simon”이라는 테스트 사용자를 기반으로 Moxtra에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-138">In this section, you configure and test Azure AD single sign-on with Moxtra based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e760f-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Moxtra 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Moxtra is to a user in Azure AD.</span></span> <span data-ttu-id="e760f-140">즉, Azure AD 사용자와 Moxtra의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-140">In other words, a link relationship between an Azure AD user and the related user in Moxtra needs to be established.</span></span>

<span data-ttu-id="e760f-141">Moxtra에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-141">In Moxtra, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e760f-142">Moxtra에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-142">To configure and test Azure AD single sign-on with Moxtra, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e760f-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e760f-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e760f-145">**[Moxtra 테스트 사용자 만들기](#creating-a-moxtra-test-user)** - Britta Simon의 Azure AD 표현과 연결되는 대응 사용자를 Moxtra에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-145">**[Creating a Moxtra test user](#creating-a-moxtra-test-user)** - to have a counterpart of Britta Simon in Moxtra that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e760f-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e760f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e760f-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="e760f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e760f-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Moxtra 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Moxtra application.</span></span>

<span data-ttu-id="e760f-150">**Moxtra에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="e760f-150">**To configure Azure AD single sign-on with Moxtra, perform the following steps:**</span></span>

1. <span data-ttu-id="e760f-151">Azure Portal의 **Moxtra** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-151">In the Azure portal, on the **Moxtra** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="e760f-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_samlbase.png)

3. <span data-ttu-id="e760f-155">**Moxtra 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-155">On the **Moxtra Domain and URLs** section, perform the following step:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_url.png)

    <span data-ttu-id="e760f-157">**로그온 URL** 텍스트 상자에 URL을 입력합니다. `https://www.moxtra.com/service/#login`</span><span class="sxs-lookup"><span data-stu-id="e760f-157">In the **Sign-on URL** textbox, type a URL as: `https://www.moxtra.com/service/#login`</span></span>

4. <span data-ttu-id="e760f-158">Moxtra 응용 프로그램에는 특정 형식의 SAML 어설션이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-158">Moxtra application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="e760f-159">이 응용 프로그램에 대해 다음 클레임을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-159">Configure the following claims for this application.</span></span> <span data-ttu-id="e760f-160">응용 프로그램 통합 페이지의 **"사용자 특성"** 섹션에서 이러한 특성의 값을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-160">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="e760f-161">다음 스크린샷은 이 구성에 대한 예제를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-161">The following screenshot shows an example for this configuration.</span></span> 

    ![Single Sign-on 구성](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_attributes.png)
    
5. <span data-ttu-id="e760f-163">**Single Sign-On** 대화 상자의 **사용자 특성** 섹션에서 이미지에 표시된 것과 같이 SAML 토큰 특성을 구성하고 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-163">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="e760f-164">특성 이름</span><span class="sxs-lookup"><span data-stu-id="e760f-164">Attribute Name</span></span> | <span data-ttu-id="e760f-165">특성 값</span><span class="sxs-lookup"><span data-stu-id="e760f-165">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="e760f-166">firstname</span><span class="sxs-lookup"><span data-stu-id="e760f-166">firstname</span></span> | <span data-ttu-id="e760f-167">user.givenname</span><span class="sxs-lookup"><span data-stu-id="e760f-167">user.givenname</span></span> |
    | <span data-ttu-id="e760f-168">lastname</span><span class="sxs-lookup"><span data-stu-id="e760f-168">lastname</span></span> | <span data-ttu-id="e760f-169">user.surname</span><span class="sxs-lookup"><span data-stu-id="e760f-169">user.surname</span></span> |
    | <span data-ttu-id="e760f-170">idpid</span><span class="sxs-lookup"><span data-stu-id="e760f-170">idpid</span></span>    | <span data-ttu-id="e760f-171">< SAML 엔터티 ID ></span><span class="sxs-lookup"><span data-stu-id="e760f-171">< SAML Entity ID ></span></span> 

    > [!Note]
    > <span data-ttu-id="e760f-172">**idpid** 특성 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-172">The value of **idpid** attribute is not real.</span></span> <span data-ttu-id="e760f-173">**Moxtra 구성** 아래 **빠른 참조** 섹션에서 실제 값을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-173">You can get the actual value from **Quick reference** section under **Moxtra Configuration**.</span></span>
    
    <span data-ttu-id="e760f-174">a.</span><span class="sxs-lookup"><span data-stu-id="e760f-174">a.</span></span> <span data-ttu-id="e760f-175">**특성 추가**를 클릭하여 **특성 추가** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-175">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-moxtra-tutorial/tutorial_attribute_04.png)

    <span data-ttu-id="e760f-177">b.</span><span class="sxs-lookup"><span data-stu-id="e760f-177">b.</span></span> <span data-ttu-id="e760f-178">**이름** 텍스트 상자에서 해당 행에 표시된 특성 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-178">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-moxtra-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="e760f-180">c.</span><span class="sxs-lookup"><span data-stu-id="e760f-180">c.</span></span> <span data-ttu-id="e760f-181">**값** 목록에서 해당 행에 대해 표시된 특성을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-181">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="e760f-182">d.</span><span class="sxs-lookup"><span data-stu-id="e760f-182">d.</span></span> <span data-ttu-id="e760f-183">**Ok**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-183">Click **Ok**.</span></span>
    
5. <span data-ttu-id="e760f-184">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-184">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_certificate.png) 

6. <span data-ttu-id="e760f-186">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-186">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-moxtra-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="e760f-188">**Moxtra 구성** 섹션에서 **Moxtra 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-188">On the **Moxtra Configuration** section, click **Configure Moxtra** to open **Configure sign-on** window.</span></span> <span data-ttu-id="e760f-189">**빠른 참조 섹션**에서 **SAML 엔터티 ID 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-189">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_configure.png) 

8. <span data-ttu-id="e760f-191">다른 웹 브라우저 창에서 Moxtra 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-191">In another browser window, sign on to your Moxtra company site as an administrator.</span></span>

9. <span data-ttu-id="e760f-192">왼쪽의 도구 모음에서 **관리 콘솔 > SAML Single Sign-On**을 클릭하고 나서 **새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-192">In the toolbar on the left, click **Admin Console > SAML Single Sign-on**, and then click **New**.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_06.png) 

10. <span data-ttu-id="e760f-194">**SAML** 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-194">On the **SAML** page, perform the following steps:</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_08.png)   
 
    <span data-ttu-id="e760f-196">a.</span><span class="sxs-lookup"><span data-stu-id="e760f-196">a.</span></span> <span data-ttu-id="e760f-197">**이름** 텍스트 상자에서 구성할 이름을 입력합니다(예: *SAML*).</span><span class="sxs-lookup"><span data-stu-id="e760f-197">In the **Name** textbox, type a name for your configuration (e.g.: *SAML*).</span></span> 
  
    <span data-ttu-id="e760f-198">b.</span><span class="sxs-lookup"><span data-stu-id="e760f-198">b.</span></span> <span data-ttu-id="e760f-199">Azure Portal에서 복사한 **SAML 엔터티 ID** 값을 **IDP 엔터티 ID** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-199">In the **IdP Entity ID** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span> 
 
    <span data-ttu-id="e760f-200">c.</span><span class="sxs-lookup"><span data-stu-id="e760f-200">c.</span></span> <span data-ttu-id="e760f-201">Azure Portal에서 복사한 **SAML Single Sign-On 서비스 URL** 값을 **로그인 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-201">In **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 
 
    <span data-ttu-id="e760f-202">d.</span><span class="sxs-lookup"><span data-stu-id="e760f-202">d.</span></span> <span data-ttu-id="e760f-203">**AuthnContextClassRef** 텍스트 상자에 **urn:oasis:names:tc:SAML:2.0:ac:classes:Password**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-203">In the **AuthnContextClassRef** textbox, type **urn:oasis:names:tc:SAML:2.0:ac:classes:Password**.</span></span> 
 
    <span data-ttu-id="e760f-204">e.</span><span class="sxs-lookup"><span data-stu-id="e760f-204">e.</span></span> <span data-ttu-id="e760f-205">**NameID 형식** 텍스트 상자에 **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-205">In the **NameID Format** textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span> 
 
    <span data-ttu-id="e760f-206">f.</span><span class="sxs-lookup"><span data-stu-id="e760f-206">f.</span></span> <span data-ttu-id="e760f-207">Azure Portal에서 다운로드한 인증서를 메모장에서 열고, 내용을 복사한 다음, **인증서** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-207">Open certificate which you have downloaded from Azure portal in notepad, copy the content, and then paste it into the **Certificate** textbox.</span></span>    
 
    <span data-ttu-id="e760f-208">g.</span><span class="sxs-lookup"><span data-stu-id="e760f-208">g.</span></span> <span data-ttu-id="e760f-209">SAML 전자 메일 도메인 텍스트 상자에 SAML 전자 메일 도메인을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-209">In the SAML email domain textbox, type your SAML email domain.</span></span>    
  
    >[!NOTE]
    ><span data-ttu-id="e760f-210">도메인을 확인하는 단계를 보려면 아래 "**i**"를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-210">To see the steps to verify the domain, click the "**i**" below.</span></span>

    <span data-ttu-id="e760f-211">h.</span><span class="sxs-lookup"><span data-stu-id="e760f-211">h.</span></span> <span data-ttu-id="e760f-212">**업데이트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-212">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="e760f-213">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-213">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e760f-214">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-214">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e760f-215">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-215">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e760f-216">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="e760f-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="e760f-217">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-217">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="e760f-219">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="e760f-219">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e760f-220">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-220">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-moxtra-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e760f-222">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-222">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-moxtra-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e760f-224">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-224">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-moxtra-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e760f-226">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-226">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-moxtra-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e760f-228">a.</span><span class="sxs-lookup"><span data-stu-id="e760f-228">a.</span></span> <span data-ttu-id="e760f-229">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-229">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e760f-230">b.</span><span class="sxs-lookup"><span data-stu-id="e760f-230">b.</span></span> <span data-ttu-id="e760f-231">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-231">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e760f-232">c.</span><span class="sxs-lookup"><span data-stu-id="e760f-232">c.</span></span> <span data-ttu-id="e760f-233">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-233">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e760f-234">d.</span><span class="sxs-lookup"><span data-stu-id="e760f-234">d.</span></span> <span data-ttu-id="e760f-235">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-235">Click **Create**.</span></span>
 
### <a name="creating-a-moxtra-test-user"></a><span data-ttu-id="e760f-236">Moxtra 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="e760f-236">Creating a Moxtra test user</span></span>

<span data-ttu-id="e760f-237">이 섹션은 Moxtra에서 Britta Simon이라는 사용자를 만들기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-237">The objective of this section is to create a user called Britta Simon in Moxtra.</span></span>

<span data-ttu-id="e760f-238">**Moxtra에서 Britta Simon이라는 사용자를 만들려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="e760f-238">**To create a user called Britta Simon in Moxtra, perform the following steps:**</span></span>

1. <span data-ttu-id="e760f-239">Moxtra 회사 사이트에 관리자로 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-239">Sign on to your Moxtra company site as an administrator.</span></span>

2. <span data-ttu-id="e760f-240">왼쪽의 도구 모음에서 **관리 콘솔 > 사용자 관리**, **사용자 추가**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-240">In the toolbar on the left, click **Admin Console > User Management**, and then **Add User**.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_10.png) 

3. <span data-ttu-id="e760f-242">**사용자 추가** 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-242">On the **Add User** dialog, perform the following steps:</span></span>
  
    <span data-ttu-id="e760f-243">a.</span><span class="sxs-lookup"><span data-stu-id="e760f-243">a.</span></span> <span data-ttu-id="e760f-244">**이름** 텍스트 상자에 **Britta**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-244">In the **First Name** textbox, type **Britta**.</span></span>
  
    <span data-ttu-id="e760f-245">b.</span><span class="sxs-lookup"><span data-stu-id="e760f-245">b.</span></span> <span data-ttu-id="e760f-246">**성** 텍스트 상자에 **Simon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-246">In the **Last Name** textbox, type **Simon**.</span></span>
  
    <span data-ttu-id="e760f-247">c.</span><span class="sxs-lookup"><span data-stu-id="e760f-247">c.</span></span> <span data-ttu-id="e760f-248">**메일** 텍스트 상자에 Azure Portal과 같은 Britta의 메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-248">In the **Email** textbox, type Britta's email address same as on Azure portal.</span></span>
  
    <span data-ttu-id="e760f-249">d.</span><span class="sxs-lookup"><span data-stu-id="e760f-249">d.</span></span> <span data-ttu-id="e760f-250">**사업부** 텍스트 상자에 **Dev**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-250">In the **Division** textbox, type **Dev**.</span></span>
  
    <span data-ttu-id="e760f-251">e.</span><span class="sxs-lookup"><span data-stu-id="e760f-251">e.</span></span> <span data-ttu-id="e760f-252">**부서** 텍스트 상자에 **IT**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-252">In the **Department** textbox, type **IT**.</span></span>
  
    <span data-ttu-id="e760f-253">f.</span><span class="sxs-lookup"><span data-stu-id="e760f-253">f.</span></span> <span data-ttu-id="e760f-254">**관리자**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-254">Select **Administrator**.</span></span>
  
    <span data-ttu-id="e760f-255">g.</span><span class="sxs-lookup"><span data-stu-id="e760f-255">g.</span></span> <span data-ttu-id="e760f-256">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-256">Click **Add**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e760f-257">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="e760f-257">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e760f-258">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Moxtra에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-258">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Moxtra.</span></span>

![사용자 할당][200] 

<span data-ttu-id="e760f-260">**Britta Simon을 Moxtra에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="e760f-260">**To assign Britta Simon to Moxtra, perform the following steps:**</span></span>

1. <span data-ttu-id="e760f-261">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-261">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="e760f-263">응용 프로그램 목록에서 **Moxtra**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-263">In the applications list, select **Moxtra**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_app.png) 

3. <span data-ttu-id="e760f-265">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-265">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="e760f-267">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-267">Click **Add** button.</span></span> <span data-ttu-id="e760f-268">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-268">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="e760f-270">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-270">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e760f-271">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-271">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e760f-272">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-272">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e760f-273">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="e760f-273">Testing single sign-on</span></span>

<span data-ttu-id="e760f-274">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-274">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e760f-275">액세스 패널에서 Moxtra 타일을 클릭하면 Moxtra 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="e760f-275">When you click the Moxtra tile in the Access Panel, you should get automatically signed-on to your Moxtra application.</span></span>
<span data-ttu-id="e760f-276">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e760f-276">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e760f-277">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="e760f-277">Additional resources</span></span>

* [<span data-ttu-id="e760f-278">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="e760f-278">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e760f-279">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="e760f-279">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_203.png

