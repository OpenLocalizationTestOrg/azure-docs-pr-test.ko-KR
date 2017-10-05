---
title: "자습서: Salesforce Sandbox와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 Salesforce Sandbox 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ee54c39e-ce20-42a4-8531-da7b5f40f57c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 90e08b9cf2feb93de4877bec9734352949896dca
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce-sandbox"></a><span data-ttu-id="b38ca-103">자습서: Salesforce Sandbox와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="b38ca-103">Tutorial: Azure Active Directory integration with Salesforce Sandbox</span></span>

<span data-ttu-id="b38ca-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Salesforce Sandbox를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-104">In this tutorial, you learn how to integrate Salesforce Sandbox with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b38ca-105">Salesforce Sandbox를 Azure AD와 통합하면 다음과 같은 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-105">Integrating Salesforce Sandbox with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b38ca-106">Salesforce Sandbox에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-106">You can control in Azure AD who has access to Salesforce Sandbox</span></span>
- <span data-ttu-id="b38ca-107">사용자가 해당 Azure AD 계정으로 Salesforce Sandbox에 자동으로 로그인(Single Sign-On)하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-107">You can enable your users to automatically get signed-on to Salesforce Sandbox (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b38ca-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b38ca-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b38ca-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b38ca-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="b38ca-110">Prerequisites</span></span>

<span data-ttu-id="b38ca-111">Salesforce Sandbox와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-111">To configure Azure AD integration with Salesforce Sandbox, you need the following items:</span></span>

- <span data-ttu-id="b38ca-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="b38ca-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b38ca-113">Salesforce Sandbox Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="b38ca-113">A Salesforce Sandbox single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b38ca-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b38ca-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b38ca-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="b38ca-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b38ca-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b38ca-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="b38ca-118">Scenario description</span></span>
<span data-ttu-id="b38ca-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b38ca-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b38ca-121">갤러리에서 Salesforce Sandbox를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-121">Adding Salesforce Sandbox from the gallery</span></span>
2. <span data-ttu-id="b38ca-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="b38ca-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-salesforce-sandbox-from-the-gallery"></a><span data-ttu-id="b38ca-123">갤러리에서 Salesforce Sandbox를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-123">Adding Salesforce Sandbox from the gallery</span></span>
<span data-ttu-id="b38ca-124">Salesforce Sandbox의 Azure AD 통합을 구성하려면 갤러리의 Salesforce Sandbox를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-124">To configure the integration of Salesforce Sandbox into Azure AD, you need to add Salesforce Sandbox from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b38ca-125">**갤러리에서 Salesforce Sandbox를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="b38ca-125">**To add Salesforce Sandbox from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b38ca-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b38ca-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b38ca-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="b38ca-131">대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-131">Click **New application** button on the top of the dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="b38ca-133">검색 상자에 **Salesforce Sandbox**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-133">In the search box, type **Salesforce Sandbox**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_search.png)

5. <span data-ttu-id="b38ca-135">결과 창에서 **Salesforce Sandbox**를 선택하고 **추가**를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-135">In the results panel, select **Salesforce Sandbox**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b38ca-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="b38ca-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b38ca-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Salesforce Sandbox에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-138">In this section, you configure and test Azure AD single sign-on with Salesforce Sandbox based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b38ca-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Salesforce Sandbox 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Salesforce Sandbox is to a user in Azure AD.</span></span> <span data-ttu-id="b38ca-140">즉, Azure AD 사용자와 Salesforce Sandbox의 관련 사용자 간에 연결 관계가 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-140">In other words, a link relationship between an Azure AD user and the related user in Salesforce Sandbox needs to be established.</span></span>

<span data-ttu-id="b38ca-141">이 연결 관계는 Azure AD의 **사용자 이름** 값을 Salesforce Sandbox의 **Username** 값으로 할당하여 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Salesforce Sandbox.</span></span>

<span data-ttu-id="b38ca-142">Salesforce Sandbox에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-142">To configure and test Azure AD single sign-on with Salesforce Sandbox, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b38ca-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b38ca-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b38ca-145">**[Salesforce Sandbox 테스트 사용자 만들기](#creating-a-salesforce-sandbox-test-user)** - Britta Simon의 Azure AD 표현과 연결되는 대응 사용자를 Salesforce Sandbox에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-145">**[Creating a Salesforce Sandbox test user](#creating-a-salesforce-sandbox-test-user)** - to have a counterpart of Britta Simon in Salesforce Sandbox that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b38ca-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b38ca-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b38ca-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="b38ca-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b38ca-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Salesforce Sandbox 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Salesforce Sandbox application.</span></span>

<span data-ttu-id="b38ca-150">**Salesforce Sandbox에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="b38ca-150">**To configure Azure AD single sign-on with Salesforce Sandbox, perform the following steps:**</span></span>

1. <span data-ttu-id="b38ca-151">Azure Portal의 **Salesforce Sandbox** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-151">In the Azure portal, on the **Salesforce Sandbox** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="b38ca-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_samlbase.png)

3. <span data-ttu-id="b38ca-155">**Salesforce Sandbox 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-155">On the **Salesforce Sandbox Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_url.png)

     <span data-ttu-id="b38ca-157">**로그온 URL** 텍스트 상자에 다음 패턴으로 값을 입력합니다. `https://<subdomain>.my.salesforce.com` </span><span class="sxs-lookup"><span data-stu-id="b38ca-157">In the **Sign-on URL** textbox, type the value using the following pattern: `https://<subdomain>.my.salesforce.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b38ca-158">이 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-158">This value is not the real.</span></span> <span data-ttu-id="b38ca-159">이 값을 실제 로그온 URL로 업데이트 합니다. 이 값을 얻으려면 [Salesforce Sandbox 클라이언트 지원 팀](https://help.salesforce.com/support)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="b38ca-159">Update this value with the actual Sign-on URL.Contact [Salesforce Sandbox Client support team](https://help.salesforce.com/support) to get this value.</span></span>


4. <span data-ttu-id="b38ca-160">디렉터리의 다른 Salesforce Sandbox 인스턴스에 대한 Single Sign-On을 이미 구성한 경우 **로그온 URL**과 같은 값으로 **식별자**도 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-160">If you have already configured single sign-on for another Salesforce Sandbox instance in your directory, then you must also configure the **Identifier** to have the same value as the **Sign on URL**.</span></span> 
    
    >[!Note]
    ><span data-ttu-id="b38ca-161">대화 상자의 **앱 URL 구성** 페이지에서 **고급 설정 표시** 확인란을 선택하여 **식별자** 필드를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-161">The **Identifier** field can be found by checking the **Show advanced settings** checkbox on the **Configure App URL** page of the dialog</span></span> 


5. <span data-ttu-id="b38ca-162">**SAML 서명 인증서** 섹션에서 **인증서**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-162">On the **SAML Signing Certificate** section, click **Certificate** and then save the certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_certificate.png) 

6. <span data-ttu-id="b38ca-164">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-164">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="b38ca-166">**Salesforce Sandbox 구성** 섹션에서 **Salesforce Sandbox 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-166">On the **Salesforce Sandbox Configuration** section, click **Configure Salesforce Sandbox** to open **Configure sign-on** window.</span></span> <span data-ttu-id="b38ca-167">**빠른 참조 섹션**에서 **SAML 엔터티 ID 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-167">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    <span data-ttu-id="b38ca-168">![Single Sign-On 구성](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="b38ca-168">![Configure Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_configure.png) 
<CS></span></span>
8. <span data-ttu-id="b38ca-169">브라우저에서 새 탭을 열고 Salesforce Sandbox Administrator 계정으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-169">Open a new tab in your browser and log in to your Salesforce Sandbox administrator account.</span></span>

9. <span data-ttu-id="b38ca-170">위쪽의 메뉴에서 **설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-170">In the menu on the top, click **Setup**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-salesforcesandbox-tutorial/IC781024.png)
10. <span data-ttu-id="b38ca-172">왼쪽의 탐색 창에서 **보안 제어**를 클릭한 다음 **Single Sign-On 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-172">In the navigation pane on the left, click **Security Controls**, and then click **Single Sign-On Settings**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-salesforcesandbox-tutorial/IC781025.png)
11. <span data-ttu-id="b38ca-174">Single Sign-On 설정 섹션에서 ![Single Sign-On 구성](./media/active-directory-saas-salesforcesandbox-tutorial/IC781026.png) 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-174">On the Single Sign-On Settings section, perform the following steps:  ![Configure Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/IC781026.png)</span></span>
     
     <span data-ttu-id="b38ca-175">a.</span><span class="sxs-lookup"><span data-stu-id="b38ca-175">a.</span></span>  <span data-ttu-id="b38ca-176">**SAML 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-176">Select **SAML Enabled**.</span></span> 

     <span data-ttu-id="b38ca-177">b.</span><span class="sxs-lookup"><span data-stu-id="b38ca-177">b.</span></span>  <span data-ttu-id="b38ca-178">**새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-178">Click **New**.</span></span>

12. <span data-ttu-id="b38ca-179">SAML Single Sign-On 설정 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-179">On the SAML Single Sign-On Settings section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-salesforcesandbox-tutorial/IC781027.png)

    <span data-ttu-id="b38ca-181">a. 이름 텍스트 상자에 구성의 이름을 입력합니다(예: *SPSSOWAAD\_Test*).</span><span class="sxs-lookup"><span data-stu-id="b38ca-181">a.In the Name textbox, type the name of the configuration (e.g.: *SPSSOWAAD\_Test*).</span></span> 

    <span data-ttu-id="b38ca-182">b.</span><span class="sxs-lookup"><span data-stu-id="b38ca-182">b.</span></span> <span data-ttu-id="b38ca-183">**SMAL 엔터티 ID** 값을 **발급자** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-183">Paste **SMAL Entity ID** value into the **Issuer** textbox.</span></span>

    <span data-ttu-id="b38ca-184">c.</span><span class="sxs-lookup"><span data-stu-id="b38ca-184">c.</span></span> <span data-ttu-id="b38ca-185">디렉터리에 처음으로 추가하는 Salesforce Sandbox 인스턴스인 경우 **엔터티 Id** 텍스트 상자에 **https://test.salesforce.com**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-185">In the **Entity Id** textbox, type **https://test.salesforce.com** if it is the first Salesforce Sandbox instance that you are adding to your directory.</span></span> <span data-ttu-id="b38ca-186">Salesforce Sandbox의 인스턴스를 이미 추가한 경우에는 **엔터티 ID**에 **로그온 URL**을 입력합니다. 형식은 다음과 같아야 합니다. `http://company.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="b38ca-186">If you have already added an instance of Salesforce Sandbox, then for the **Entity ID** type in the **Sign On URL**, which should be in this format: `http://company.my.salesforce.com`</span></span>  
 
    <span data-ttu-id="b38ca-187">d.</span><span class="sxs-lookup"><span data-stu-id="b38ca-187">d.</span></span> <span data-ttu-id="b38ca-188">다운로드한 인증서를 업로드하려면 **찾아보기** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-188">Click **Browse** to upload the downloaded certificate.</span></span>  

    <span data-ttu-id="b38ca-189">e.</span><span class="sxs-lookup"><span data-stu-id="b38ca-189">e.</span></span> <span data-ttu-id="b38ca-190">**SAML ID 유형**으로 **사용자 개체에서 페더레이션 ID를 포함하는 어설션**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-190">As **SAML Identity Type**, select **Assertion contains the Federation ID from the User object**.</span></span>
 
    <span data-ttu-id="b38ca-191">f.</span><span class="sxs-lookup"><span data-stu-id="b38ca-191">f.</span></span> <span data-ttu-id="b38ca-192">**SAML ID 위치**로 **Subject 문의 NameIdentifier 요소에 ID 포함**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-192">As **SAML Identity Location**, select **Identity is in the NameIdentifier element of the Subject statement**.</span></span>

    <span data-ttu-id="b38ca-193">g.</span><span class="sxs-lookup"><span data-stu-id="b38ca-193">g.</span></span> <span data-ttu-id="b38ca-194">**Single Sign-On 서비스 URL**을 **ID 공급자 로그인 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-194">Paste **Single Sign-On Service URL** into the **Identity Provider Login URL** textbox.</span></span> 

    <span data-ttu-id="b38ca-195">h.</span><span class="sxs-lookup"><span data-stu-id="b38ca-195">h.</span></span> <span data-ttu-id="b38ca-196">SFDC는 SAML 로그아웃을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-196">SFDC does not support SAML logout.</span></span>  <span data-ttu-id="b38ca-197">해결 방법으로 **ID 공급자 로그아웃 URL** 텍스트 상자에 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0'을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-197">As a workaround, paste 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0' it into the **Identity Provider Logout URL** textbox.</span></span>

    <span data-ttu-id="b38ca-198">i.</span><span class="sxs-lookup"><span data-stu-id="b38ca-198">i.</span></span> <span data-ttu-id="b38ca-199">**서비스 공급자가 시작한 요청 바인딩**에서 **HTTP Post**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-199">As **Service Provider Initiated Request Binding**, select **HTTP POST**.</span></span> 

    <span data-ttu-id="b38ca-200">j.</span><span class="sxs-lookup"><span data-stu-id="b38ca-200">j.</span></span> <span data-ttu-id="b38ca-201">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-201">Click **Save**.</span></span>

### <a name="enable-your-domain"></a><span data-ttu-id="b38ca-202">도메인 활성화</span><span class="sxs-lookup"><span data-stu-id="b38ca-202">Enable your domain</span></span>
<span data-ttu-id="b38ca-203">이 섹션에서는 이미 도메인을 만들었다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-203">This section assumes that you already have created a domain.</span></span>  <span data-ttu-id="b38ca-204">자세한 내용은 [도메인 이름 정의](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b38ca-204">For more information, see [Defining Your Domain Name](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).</span></span>

<span data-ttu-id="b38ca-205">**도메인을 사용하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="b38ca-205">**To enable your domain, perform the following steps:**</span></span>

1. <span data-ttu-id="b38ca-206">왼쪽 탐색 창에서 **도메인 관리**를 클릭한 다음 **내 도메인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-206">In the left navigation pane, click **Domain Management**, and then click **My Domain.**</span></span>
   
     ![Single Sign-on 구성](./media/active-directory-saas-salesforcesandbox-tutorial/IC781029.png)
   
   >[!NOTE]
   ><span data-ttu-id="b38ca-208">도메인이 올바르게 구성되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-208">Please make sure that your domain has been configured correctly.</span></span> 

2. <span data-ttu-id="b38ca-209">**로그인 페이지 설정** 섹션에서 **편집**을 클릭한 다음 **인증 서비스**로 이전 섹션에서 SAML Single Sign-On 설정의 이름을 선택하고 마지막으로 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-209">In the **Login Page Settings** section, click **Edit**, then, as **Authentication Service**, select the name of the SAML Single Sign-On Setting from the previous section, and finally click **Save**.</span></span>
   
   ![Single Sign-on 구성](./media/active-directory-saas-salesforcesandbox-tutorial/IC781030.png)

<span data-ttu-id="b38ca-211">도메인이 구성되면 바로 사용자가 Salesforce 샌드박스에 로그인하는 도메인 URL을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-211">As soon as you have a domain configured, your users should use the domain URL to login to the Salesforce sandbox.</span></span>  

<span data-ttu-id="b38ca-212">URL의 값을 가져오려면 이전 섹션에서 만든 SSO 프로필을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-212">To get the value of the URL, click the SSO profile you have created in the previous section.</span></span>    

> [!TIP]
> <span data-ttu-id="b38ca-213">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-213">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b38ca-214">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-214">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b38ca-215">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-215">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b38ca-216">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="b38ca-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="b38ca-217">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-217">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="b38ca-219">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="b38ca-219">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b38ca-220">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-220">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b38ca-222">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-222">to display the list of users go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b38ca-224">대화 상자 위쪽에서 **추가**를 클릭하여 **사용자** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-224">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b38ca-226">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-226">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b38ca-228">a.</span><span class="sxs-lookup"><span data-stu-id="b38ca-228">a.</span></span> <span data-ttu-id="b38ca-229">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-229">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b38ca-230">b.</span><span class="sxs-lookup"><span data-stu-id="b38ca-230">b.</span></span> <span data-ttu-id="b38ca-231">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-231">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b38ca-232">c.</span><span class="sxs-lookup"><span data-stu-id="b38ca-232">c.</span></span> <span data-ttu-id="b38ca-233">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-233">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b38ca-234">d.</span><span class="sxs-lookup"><span data-stu-id="b38ca-234">d.</span></span> <span data-ttu-id="b38ca-235">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-235">Click **Create**.</span></span>
 
### <a name="creating-a-salesforce-sandbox-test-user"></a><span data-ttu-id="b38ca-236">Salesforce Sandbox 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="b38ca-236">Creating a Salesforce Sandbox test user</span></span>

<span data-ttu-id="b38ca-237">이 섹션에서는 Salesforce Sandbox에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-237">In this section, a user called Britta Simon is created in Salesforce Sandbox.</span></span> <span data-ttu-id="b38ca-238">Salesforce Sandbox는 기본적으로 설정되는 Just-In-Time 프로비전을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-238">Salesforce Sandbox supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="b38ca-239">이 섹션에 작업 항목이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-239">There is no action item for you in this section.</span></span> <span data-ttu-id="b38ca-240">Salesforce Sandbox에 사용자가 없는 경우 Salesforce Sandbox에 액세스하려고 시도하면 새 사용자가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-240">If a user doesn't already exist in Salesforce Sandbox, a new one is created when you attempt to access Salesforce Sandbox.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b38ca-241">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="b38ca-241">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b38ca-242">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Salesforce Sandbox에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-242">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Salesforce Sandbox.</span></span>

![사용자 할당][200] 

<span data-ttu-id="b38ca-244">**Salesforce Sandbox에 사용자를 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="b38ca-244">**To assign Britta Simon to Salesforce Sandbox, perform the following steps:**</span></span>

1. <span data-ttu-id="b38ca-245">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-245">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="b38ca-247">응용 프로그램 목록에서 **Salesforce Sandbox**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-247">In the applications list, select **Salesforce Sandbox**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_app.png) 

3. <span data-ttu-id="b38ca-249">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-249">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="b38ca-251">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-251">Click **Add** button.</span></span> <span data-ttu-id="b38ca-252">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="b38ca-254">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-254">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b38ca-255">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b38ca-256">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b38ca-257">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="b38ca-257">Testing single sign-on</span></span>

<span data-ttu-id="b38ca-258">SSO 설정을 테스트하려면 액세스 패널을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b38ca-258">If you want to test your SSO settings, open the Access Panel.</span></span> <span data-ttu-id="b38ca-259">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b38ca-259">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b38ca-260">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="b38ca-260">Additional resources</span></span>

* [<span data-ttu-id="b38ca-261">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="b38ca-261">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b38ca-262">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="b38ca-262">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="b38ca-263">사용자 프로비저닝 구성</span><span class="sxs-lookup"><span data-stu-id="b38ca-263">Configure User Provisioning</span></span>](active-directory-saas-salesforce-sandbox-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_203.png

