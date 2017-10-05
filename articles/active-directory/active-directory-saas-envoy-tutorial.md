---
title: "자습서: Envoy와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 Envoy 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 71f7afcc-1033-4098-9b7e-4f9f2b26f734
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: jeedes
ms.openlocfilehash: 49211b35ab3e28e0df914061e7fa623907935638
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-envoy"></a><span data-ttu-id="40161-103">자습서: Envoy와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="40161-103">Tutorial: Azure Active Directory integration with Envoy</span></span>

<span data-ttu-id="40161-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Envoy를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="40161-104">In this tutorial, you learn how to integrate Envoy with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="40161-105">Envoy를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="40161-105">Integrating Envoy with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="40161-106">Envoy에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40161-106">You can control in Azure AD who has access to Envoy.</span></span>
- <span data-ttu-id="40161-107">사용자가 해당 Azure AD 계정으로 Envoy에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40161-107">You can enable your users to automatically get signed-on to Envoy (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="40161-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40161-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="40161-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="40161-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="40161-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="40161-110">Prerequisites</span></span>

<span data-ttu-id="40161-111">Envoy와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="40161-111">To configure Azure AD integration with Envoy, you need the following items:</span></span>

- <span data-ttu-id="40161-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="40161-112">An Azure AD subscription</span></span>
- <span data-ttu-id="40161-113">Envoy Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="40161-113">An Envoy single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="40161-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="40161-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="40161-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40161-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="40161-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="40161-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="40161-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40161-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="40161-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="40161-118">Scenario description</span></span>
<span data-ttu-id="40161-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="40161-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="40161-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40161-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="40161-121">갤러리에서 Envoy 추가</span><span class="sxs-lookup"><span data-stu-id="40161-121">Adding Envoy from the gallery</span></span>
2. <span data-ttu-id="40161-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="40161-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-envoy-from-the-gallery"></a><span data-ttu-id="40161-123">갤러리에서 Envoy 추가</span><span class="sxs-lookup"><span data-stu-id="40161-123">Adding Envoy from the gallery</span></span>
<span data-ttu-id="40161-124">Envoy의 Azure AD 통합을 구성하려면 갤러리의 Envoy를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40161-124">To configure the integration of Envoy into Azure AD, you need to add Envoy from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="40161-125">**갤러리에서 Envoy를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="40161-125">**To add Envoy from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="40161-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="40161-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory 단추][1]

2. <span data-ttu-id="40161-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="40161-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="40161-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="40161-129">Then go to **All applications**.</span></span>

    ![엔터프라이즈 응용 프로그램 블레이드][2]
    
3. <span data-ttu-id="40161-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="40161-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![새 응용 프로그램 단추][3]

4. <span data-ttu-id="40161-133">검색 상자에 **Envoy**를 입력하고 결과 패널에서 **Envoy**를 선택한 후 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="40161-133">In the search box, type **Envoy**, select **Envoy** from result panel then click **Add** button to add the application.</span></span>

    ![결과 목록의 Envoy](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="40161-135">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="40161-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="40161-136">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Envoy에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="40161-136">In this section, you configure and test Azure AD single sign-on with Envoy based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="40161-137">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Envoy 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40161-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Envoy is to a user in Azure AD.</span></span> <span data-ttu-id="40161-138">즉, Azure AD 사용자와 Envoy의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40161-138">In other words, a link relationship between an Azure AD user and the related user in Envoy needs to be established.</span></span>

<span data-ttu-id="40161-139">Envoy에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="40161-139">In Envoy, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="40161-140">Envoy에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40161-140">To configure and test Azure AD single sign-on with Envoy, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="40161-141">**[Azure AD Single Sign-On 구성](#configure-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="40161-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="40161-142">**[Azure AD 테스트 사용자 만들기](#create-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="40161-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="40161-143">**[Envoy 테스트 사용자 만들기](#create-an-envoy-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 Envoy에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="40161-143">**[Create an Envoy test user](#create-an-envoy-test-user)** - to have a counterpart of Britta Simon in Envoy that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="40161-144">**[Azure AD 테스트 사용자 할당](#assign-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="40161-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="40161-145">**[Single Sign-On 테스트](#test-single-sign-on)** - 구성이 작동하는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="40161-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="40161-146">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="40161-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="40161-147">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Envoy 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="40161-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Envoy application.</span></span>

<span data-ttu-id="40161-148">**Envoy에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="40161-148">**To configure Azure AD single sign-on with Envoy, perform the following steps:**</span></span>

1. <span data-ttu-id="40161-149">Azure Portal의 **Envoy** 응용 프로그램 통합 페이지에서 **Single sign-on**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="40161-149">In the Azure portal, on the **Envoy** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-On 구성 링크][4]

2. <span data-ttu-id="40161-151">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="40161-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_samlbase.png)

3. <span data-ttu-id="40161-153">**Envoy 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="40161-153">On the **Envoy Domain and URLs** section, perform the following steps:</span></span>

    ![Envoy 도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_url.png)

    <span data-ttu-id="40161-155">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<tenant-name>.Envoy.com`</span><span class="sxs-lookup"><span data-stu-id="40161-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.Envoy.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="40161-156">이 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="40161-156">This value is not real.</span></span> <span data-ttu-id="40161-157">이 값을 실제 로그온 URL로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="40161-157">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="40161-158">이 값을 얻으려면 [Envoy 클라이언트 지원 팀](https://envoy.com/contact/)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="40161-158">Contact [Envoy Client support team](https://envoy.com/contact/) to get this value.</span></span>

4. <span data-ttu-id="40161-159">**SAML 서명 인증서** 섹션에서 인증서의 **지문** 값을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="40161-159">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate..</span></span>

    ![인증서 다운로드 링크](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_certificate.png) 

5. <span data-ttu-id="40161-161">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="40161-161">Click **Save** button.</span></span>

    ![Single Sign-On 구성 저장 단추](./media/active-directory-saas-envoy-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="40161-163">**Envoy 구성** 섹션에서 **Envoy 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="40161-163">On the **Envoy Configuration** section, click **Configure Envoy** to open **Configure sign-on** window.</span></span> <span data-ttu-id="40161-164">**빠른 참조 섹션**에서 **SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="40161-164">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Envoy 구성](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_configure.png)

7. <span data-ttu-id="40161-166">다른 웹 브라우저 창에서 Envoy 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="40161-166">In a different web browser window, log into your Envoy company site as an administrator.</span></span>

8. <span data-ttu-id="40161-167">위쪽에 도구 모음에서 **설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="40161-167">In the toolbar on the top, click **Settings**.</span></span>

    <span data-ttu-id="40161-168">![Envoy](./media/active-directory-saas-envoy-tutorial/ic776782.png "Envoy")</span><span class="sxs-lookup"><span data-stu-id="40161-168">![Envoy](./media/active-directory-saas-envoy-tutorial/ic776782.png "Envoy")</span></span>

9. <span data-ttu-id="40161-169">**회사**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="40161-169">Click **Company**.</span></span>

    <span data-ttu-id="40161-170">![회사](./media/active-directory-saas-envoy-tutorial/ic776783.png "회사")</span><span class="sxs-lookup"><span data-stu-id="40161-170">![Company](./media/active-directory-saas-envoy-tutorial/ic776783.png "Company")</span></span>

10. <span data-ttu-id="40161-171">**SAML**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="40161-171">Click **SAML**.</span></span>

    <span data-ttu-id="40161-172">![SAML](./media/active-directory-saas-envoy-tutorial/ic776784.png "SAML")</span><span class="sxs-lookup"><span data-stu-id="40161-172">![SAML](./media/active-directory-saas-envoy-tutorial/ic776784.png "SAML")</span></span>

11. <span data-ttu-id="40161-173">**SAML 인증** 구성 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="40161-173">In the **SAML Authentication** configuration section, perform the following steps:</span></span>

    <span data-ttu-id="40161-174">![SAML 인증](./media/active-directory-saas-envoy-tutorial/ic776785.png "SAML 인증")</span><span class="sxs-lookup"><span data-stu-id="40161-174">![SAML authentication](./media/active-directory-saas-envoy-tutorial/ic776785.png "SAML authentication")</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="40161-175">HQ 위치 ID에 대한 값은 응용 프로그램에서 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="40161-175">The value for the HQ location ID is auto generated by the application.</span></span>
    
    <span data-ttu-id="40161-176">a.</span><span class="sxs-lookup"><span data-stu-id="40161-176">a.</span></span> <span data-ttu-id="40161-177">Azure Portal에서 복사한 인증서의 **지문** 값을 **지문** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="40161-177">In **Fingerprint** textbox, paste the **Thumbprint** value of certificate, which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="40161-178">b.</span><span class="sxs-lookup"><span data-stu-id="40161-178">b.</span></span> <span data-ttu-id="40161-179">Azure Portal에서 복사한 **SAML Single Sign-On 서비스 URL** 값을 **ID 공급자 HTTP SAML URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="40161-179">Paste **SAML Single Sign-On Service URL** value, which you have copied form the Azure portal into the **IDENTITY PROVIDER HTTP SAML URL** textbox.</span></span>
    
    <span data-ttu-id="40161-180">c.</span><span class="sxs-lookup"><span data-stu-id="40161-180">c.</span></span> <span data-ttu-id="40161-181">**변경 내용 저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="40161-181">Click **Save changes**.</span></span>

> [!TIP]
> <span data-ttu-id="40161-182">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40161-182">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="40161-183">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="40161-183">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="40161-184">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40161-184">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="40161-185">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="40161-185">Create an Azure AD test user</span></span>

<span data-ttu-id="40161-186">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="40161-186">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Azure AD 테스트 사용자 만들기][100]

<span data-ttu-id="40161-188">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="40161-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="40161-189">Azure Portal의 왼쪽 창에서 **Azure Active Directory** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="40161-189">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Azure Active Directory 단추](./media/active-directory-saas-envoy-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="40161-191">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="40161-191">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !["사용자 및 그룹" 및 "모든 사용자" 링크](./media/active-directory-saas-envoy-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="40161-193">**사용자** 대화 상자를 열려면 **모든 사용자** 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="40161-193">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![추가 단추](./media/active-directory-saas-envoy-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="40161-195">**사용자** 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="40161-195">In the **User** dialog box, perform the following steps:</span></span>

    ![사용자 대화 상자](./media/active-directory-saas-envoy-tutorial/create_aaduser_04.png)

    <span data-ttu-id="40161-197">a.</span><span class="sxs-lookup"><span data-stu-id="40161-197">a.</span></span> <span data-ttu-id="40161-198">**이름** 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="40161-198">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="40161-199">b.</span><span class="sxs-lookup"><span data-stu-id="40161-199">b.</span></span> <span data-ttu-id="40161-200">**사용자 이름** 상자에 사용자인 Britta Simon의 전자 메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="40161-200">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="40161-201">c.</span><span class="sxs-lookup"><span data-stu-id="40161-201">c.</span></span> <span data-ttu-id="40161-202">**암호 표시** 확인란을 선택한 다음 **암호** 상자에 표시된 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="40161-202">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="40161-203">d.</span><span class="sxs-lookup"><span data-stu-id="40161-203">d.</span></span> <span data-ttu-id="40161-204">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="40161-204">Click **Create**.</span></span>
 
### <a name="create-an-envoy-test-user"></a><span data-ttu-id="40161-205">Envoy 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="40161-205">Create an Envoy test user</span></span>

<span data-ttu-id="40161-206">Envoy를 프로비전하는 사용자를 구성할 작업 항목이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="40161-206">There is no action item for you to configure user provisioning to Envoy.</span></span> <span data-ttu-id="40161-207">할당된 사용자가 액세스 패널을 사용하여 Envoy에 로그인하려는 경우 Envoy는 사용자가 존재하는지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="40161-207">When an assigned user tries to log into Envoy using the access panel, Envoy checks whether the user exists.</span></span> <span data-ttu-id="40161-208">사용할 수 있는 사용자 계정이 없으면 자동으로 Envoy에 의해 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="40161-208">If there is no user account available yet, it is automatically created by Envoy.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="40161-209">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="40161-209">Assign the Azure AD test user</span></span>

<span data-ttu-id="40161-210">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Envoy에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="40161-210">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Envoy.</span></span>

![사용자 역할 할당][200] 

<span data-ttu-id="40161-212">**Britta Simon을 Envoy에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="40161-212">**To assign Britta Simon to Envoy, perform the following steps:**</span></span>

1. <span data-ttu-id="40161-213">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="40161-213">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="40161-215">응용 프로그램 목록에서 **Envoy**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="40161-215">In the applications list, select **Envoy**.</span></span>

    ![응용 프로그램 목록의 Envoy 링크](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_app.png)  

3. <span data-ttu-id="40161-217">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="40161-217">In the menu on the left, click **Users and groups**.</span></span>

    !["사용자 및 그룹" 링크][202]

4. <span data-ttu-id="40161-219">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="40161-219">Click **Add** button.</span></span> <span data-ttu-id="40161-220">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="40161-220">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![할당 추가 창][203]

5. <span data-ttu-id="40161-222">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="40161-222">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="40161-223">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="40161-223">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="40161-224">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="40161-224">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="40161-225">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="40161-225">Test single sign-on</span></span>

<span data-ttu-id="40161-226">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="40161-226">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="40161-227">액세스 패널에서 Envoy 타일을 클릭하면 Envoy 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="40161-227">When you click the Envoy tile in the Access Panel, you should get automatically signed-on to your Envoy application.</span></span>
<span data-ttu-id="40161-228">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="40161-228">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="40161-229">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="40161-229">Additional resources</span></span>

* [<span data-ttu-id="40161-230">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="40161-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="40161-231">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="40161-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_203.png

