---
title: "LiquidFiles와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 LiquidFiles 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: cb517134-0b34-4a74-b40c-5a3223ca81b6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: b858c6d26b78be4641a46b3453f53d103b512356
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-liquidfiles"></a><span data-ttu-id="62ebd-103">자습서: LiquidFiles와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="62ebd-103">Tutorial: Azure Active Directory integration with LiquidFiles</span></span>

<span data-ttu-id="62ebd-104">이 자습서에서는 Azure AD(Azure Active Directory)와 LiquidFiles를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="62ebd-104">In this tutorial, you learn how to integrate LiquidFiles with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="62ebd-105">LiquidFiles를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="62ebd-105">Integrating LiquidFiles with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="62ebd-106">LiquidFiles에 액세스할 수 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62ebd-106">You can control in Azure AD who has access to LiquidFiles</span></span>
- <span data-ttu-id="62ebd-107">사용자가 자신의 Azure AD 계정으로 LiquidFiles에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62ebd-107">You can enable your users to automatically get signed-on to LiquidFiles (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="62ebd-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62ebd-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="62ebd-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="62ebd-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="62ebd-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="62ebd-110">Prerequisites</span></span>

<span data-ttu-id="62ebd-111">LiquidFiles와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="62ebd-111">To configure Azure AD integration with LiquidFiles, you need the following items:</span></span>

- <span data-ttu-id="62ebd-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="62ebd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="62ebd-113">LiquidFiles Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="62ebd-113">A LiquidFiles single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="62ebd-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="62ebd-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="62ebd-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="62ebd-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="62ebd-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="62ebd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="62ebd-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62ebd-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="62ebd-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="62ebd-118">Scenario description</span></span>
<span data-ttu-id="62ebd-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="62ebd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="62ebd-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62ebd-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="62ebd-121">갤러리에서 LiquidFiles 추가</span><span class="sxs-lookup"><span data-stu-id="62ebd-121">Adding LiquidFiles from the gallery</span></span>
2. <span data-ttu-id="62ebd-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="62ebd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-liquidfiles-from-the-gallery"></a><span data-ttu-id="62ebd-123">갤러리에서 LiquidFiles 추가</span><span class="sxs-lookup"><span data-stu-id="62ebd-123">Adding LiquidFiles from the gallery</span></span>
<span data-ttu-id="62ebd-124">LiquidFiles가 Azure AD에 통합되도록 구성하려면 갤러리의 LiquidFiles를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="62ebd-124">To configure the integration of LiquidFiles into Azure AD, you need to add LiquidFiles from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="62ebd-125">**갤러리에서 LiquidFiles를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="62ebd-125">**To add LiquidFiles from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="62ebd-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="62ebd-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="62ebd-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="62ebd-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="62ebd-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="62ebd-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="62ebd-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="62ebd-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="62ebd-133">검색 상자에서 **LiquidFiles**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="62ebd-133">In the search box, type **LiquidFiles**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_search.png)

5. <span data-ttu-id="62ebd-135">결과 패널에서 **LiquidFiles**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="62ebd-135">In the results panel, select **LiquidFiles**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="62ebd-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="62ebd-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="62ebd-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 사용하여 LiquidFiles에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="62ebd-138">In this section, you configure and test Azure AD single sign-on with LiquidFiles based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="62ebd-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 LiquidFiles 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="62ebd-139">For single sign-on to work, Azure AD needs to know what the counterpart user in LiquidFiles is to a user in Azure AD.</span></span> <span data-ttu-id="62ebd-140">즉, Azure AD 사용자와 LiquidFiles의 관련 사용자 간에 연결 관계를 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="62ebd-140">In other words, a link relationship between an Azure AD user and the related user in LiquidFiles needs to be established.</span></span>

<span data-ttu-id="62ebd-141">LiquidFiles에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 연결 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="62ebd-141">In LiquidFiles, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="62ebd-142">LiquidFiles에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="62ebd-142">To configure and test Azure AD single sign-on with LiquidFiles, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="62ebd-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="62ebd-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="62ebd-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="62ebd-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="62ebd-145">**[LiquidFiles 테스트 사용자 만들기](#creating-a-liquidfiles-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 LiquidFiles에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="62ebd-145">**[Creating a LiquidFiles test user](#creating-a-liquidfiles-test-user)** - to have a counterpart of Britta Simon in LiquidFiles that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="62ebd-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="62ebd-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="62ebd-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="62ebd-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="62ebd-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="62ebd-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="62ebd-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 LiquidFiles 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="62ebd-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LiquidFiles application.</span></span>

<span data-ttu-id="62ebd-150">**LiquidFiles에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="62ebd-150">**To configure Azure AD single sign-on with LiquidFiles, perform the following steps:**</span></span>

1. <span data-ttu-id="62ebd-151">Azure Portal의 **LiquidFiles** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="62ebd-151">In the Azure portal, on the **LiquidFiles** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="62ebd-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="62ebd-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_samlbase.png)

3. <span data-ttu-id="62ebd-155">**LiquidFiles 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="62ebd-155">On the **LiquidFiles Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_url.png)

    <span data-ttu-id="62ebd-157">a.</span><span class="sxs-lookup"><span data-stu-id="62ebd-157">a.</span></span> <span data-ttu-id="62ebd-158">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<YOUR_SERVER_URL>/saml/init`</span><span class="sxs-lookup"><span data-stu-id="62ebd-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<YOUR_SERVER_URL>/saml/init`</span></span>

    <span data-ttu-id="62ebd-159">b.</span><span class="sxs-lookup"><span data-stu-id="62ebd-159">b.</span></span> <span data-ttu-id="62ebd-160">**식별자** 텍스트 상자에서 `https://<YOUR_SERVER_URL>` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="62ebd-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<YOUR_SERVER_URL>`</span></span>

    <span data-ttu-id="62ebd-161">c.</span><span class="sxs-lookup"><span data-stu-id="62ebd-161">c.</span></span> <span data-ttu-id="62ebd-162">b.</span><span class="sxs-lookup"><span data-stu-id="62ebd-162">b.</span></span> <span data-ttu-id="62ebd-163">**회신 URL** 텍스트 상자에 다음 패턴으로 URL을 입력합니다.`https://<YOUR_SERVER_URL>/saml/consume`</span><span class="sxs-lookup"><span data-stu-id="62ebd-163">In the **Reply URL** textbox, type a URL using the following pattern: `https://<YOUR_SERVER_URL>/saml/consume`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="62ebd-164">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="62ebd-164">These values are not real.</span></span> <span data-ttu-id="62ebd-165">실제 로그온 URL, 식별자 및 회신 URL로 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="62ebd-165">Update these values with the actual Sign-On URL, Identifier and, Reply URL.</span></span> <span data-ttu-id="62ebd-166">이러한 값을 얻으려면 [LiquidFiles 클라이언트 지원 팀](https://www.liquidfiles.com/support.html)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="62ebd-166">Contact [LiquidFiles Client support team](https://www.liquidfiles.com/support.html) to get these values.</span></span> 
 
4. <span data-ttu-id="62ebd-167">**SAML 서명 인증서** 섹션에서 인증서의 **지문** 값을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="62ebd-167">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_certificate.png) 

5. <span data-ttu-id="62ebd-169">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="62ebd-169">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="62ebd-171">**LiquidFiles 구성** 섹션에서 **LiquidFiles 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="62ebd-171">On the **LiquidFiles Configuration** section, click **Configure LiquidFiles** to open **Configure sign-on** window.</span></span> <span data-ttu-id="62ebd-172">**빠른 참조 섹션**에서 **로그아웃 URL 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="62ebd-172">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_configure.png)
 
7. <span data-ttu-id="62ebd-174">LiquidFiles 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="62ebd-174">Sign-on to your LiquidFiles company site as administrator.</span></span>

8. <span data-ttu-id="62ebd-175">메뉴의 **관리자 > 구성**에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="62ebd-175">Click **Single Sign-On** in the **Admin > Configuration** from the menu.</span></span>

9. <span data-ttu-id="62ebd-176">**Single Sign-On 구성** 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="62ebd-176">On the **Single Sign-On Configuration** page, perform the following steps</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-liquidfiles-tutorial/tutorial_single_01.png)

    <span data-ttu-id="62ebd-178">a.</span><span class="sxs-lookup"><span data-stu-id="62ebd-178">a.</span></span> <span data-ttu-id="62ebd-179">**Single Sign On 방법**으로 **SAML 2**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="62ebd-179">As **Single Sign On Method**, select **SAML 2**.</span></span>

    <span data-ttu-id="62ebd-180">b.</span><span class="sxs-lookup"><span data-stu-id="62ebd-180">b.</span></span> <span data-ttu-id="62ebd-181">Azure Portal에서 복사한 **SAML Single Sign-On 서비스 URL** 값을 **IDP 로그인 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="62ebd-181">In the **IDP Login URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="62ebd-182">c.</span><span class="sxs-lookup"><span data-stu-id="62ebd-182">c.</span></span> <span data-ttu-id="62ebd-183">Azure Portal에서 복사한 **로그아웃 URL** 값을 **IDP 로그아웃 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="62ebd-183">In the **IDP Logout URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="62ebd-184">d.</span><span class="sxs-lookup"><span data-stu-id="62ebd-184">d.</span></span> <span data-ttu-id="62ebd-185">Azure Portal에서 복사한 인증서의 **지문** 값을 **IDP 인증서 지문** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="62ebd-185">In the **IDP Cert Fingerprint** textbox, paste the **THUMBPRINT** value which you have copied from Azure portal..</span></span>

    <span data-ttu-id="62ebd-186">e.</span><span class="sxs-lookup"><span data-stu-id="62ebd-186">e.</span></span> <span data-ttu-id="62ebd-187">[이름 식별자 형식] 텍스트 상자에 **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress** 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="62ebd-187">In the Name Identifier Format textbox, type the value **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>

    <span data-ttu-id="62ebd-188">f.</span><span class="sxs-lookup"><span data-stu-id="62ebd-188">f.</span></span> <span data-ttu-id="62ebd-189">[Authn Context](인증 컨텍스트) 텍스트 상자에 **urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport** 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="62ebd-189">In the Authn Context textbox, type the value **urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport**.</span></span>

    <span data-ttu-id="62ebd-190">g.</span><span class="sxs-lookup"><span data-stu-id="62ebd-190">g.</span></span> <span data-ttu-id="62ebd-191">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="62ebd-191">Click **Save**.</span></span>  

> [!TIP]
> <span data-ttu-id="62ebd-192">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62ebd-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="62ebd-193">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="62ebd-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="62ebd-194">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62ebd-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="62ebd-195">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="62ebd-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="62ebd-196">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="62ebd-196">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="62ebd-198">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="62ebd-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="62ebd-199">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="62ebd-199">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-liquidfiles-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="62ebd-201">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="62ebd-201">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-liquidfiles-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="62ebd-203">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="62ebd-203">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-liquidfiles-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="62ebd-205">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="62ebd-205">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-liquidfiles-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="62ebd-207">a.</span><span class="sxs-lookup"><span data-stu-id="62ebd-207">a.</span></span> <span data-ttu-id="62ebd-208">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="62ebd-208">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="62ebd-209">b.</span><span class="sxs-lookup"><span data-stu-id="62ebd-209">b.</span></span> <span data-ttu-id="62ebd-210">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="62ebd-210">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="62ebd-211">c.</span><span class="sxs-lookup"><span data-stu-id="62ebd-211">c.</span></span> <span data-ttu-id="62ebd-212">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="62ebd-212">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="62ebd-213">d.</span><span class="sxs-lookup"><span data-stu-id="62ebd-213">d.</span></span> <span data-ttu-id="62ebd-214">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="62ebd-214">Click **Create**.</span></span>
 
### <a name="creating-a-liquidfiles-test-user"></a><span data-ttu-id="62ebd-215">LiquidFiles 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="62ebd-215">Creating a LiquidFiles test user</span></span>

<span data-ttu-id="62ebd-216">이 섹션의 목적은 LiquidFiles에서 Britta Simon이라는 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="62ebd-216">The objective of this section is to create a user called Britta Simon in LiquidFiles.</span></span> <span data-ttu-id="62ebd-217">LiquidFiles 응용 프로그램에 로그인하기 전에 사용자로 추가되도록 하려면 LiquidFiles 서버 관리자에게 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="62ebd-217">Work with your LiquidFiles server administrator to get yourself added as a user before logging in to your LiquidFiles application.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="62ebd-218">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="62ebd-218">Assigning the Azure AD test user</span></span>

<span data-ttu-id="62ebd-219">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 LiquidFiles에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="62ebd-219">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LiquidFiles.</span></span>

![사용자 할당][200] 

<span data-ttu-id="62ebd-221">**Britta Simon을 LiquidFiles에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="62ebd-221">**To assign Britta Simon to LiquidFiles, perform the following steps:**</span></span>

1. <span data-ttu-id="62ebd-222">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="62ebd-222">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="62ebd-224">응용 프로그램 목록에서 **LiquidFiles**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="62ebd-224">In the applications list, select **LiquidFiles**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_app.png) 

3. <span data-ttu-id="62ebd-226">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="62ebd-226">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="62ebd-228">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="62ebd-228">Click **Add** button.</span></span> <span data-ttu-id="62ebd-229">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="62ebd-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="62ebd-231">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="62ebd-231">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="62ebd-232">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="62ebd-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="62ebd-233">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="62ebd-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="62ebd-234">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="62ebd-234">Testing single sign-on</span></span>

<span data-ttu-id="62ebd-235">이 섹션은 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="62ebd-235">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="62ebd-236">액세스 패널에서 LiquidFiles 타일을 클릭하면 LiquidFiles 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="62ebd-236">When you click the LiquidFiles tile in the Access Panel, you should get automatically signed-on to your LiquidFiles application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="62ebd-237">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="62ebd-237">Additional resources</span></span>

* [<span data-ttu-id="62ebd-238">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="62ebd-238">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="62ebd-239">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="62ebd-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_203.png

