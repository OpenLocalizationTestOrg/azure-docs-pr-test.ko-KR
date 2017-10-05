---
title: "자습서: ClickTime과 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory 및 ClickTime 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d437b5ab-4d71-4c13-96d0-79018cebbbd4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: jeedes
ms.openlocfilehash: 0e0123a40d52dfd7a2e29c29cb2239e979089ca9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clicktime"></a><span data-ttu-id="da71f-103">자습서: ClickTime과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="da71f-103">Tutorial: Azure Active Directory integration with ClickTime</span></span>

<span data-ttu-id="da71f-104">이 자습서에서는 Azure AD(Azure Active Directory)와 ClickTime을 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-104">In this tutorial, you learn how to integrate ClickTime with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="da71f-105">ClickTime을 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-105">Integrating ClickTime with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="da71f-106">ClickTime에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-106">You can control in Azure AD who has access to ClickTime</span></span>
- <span data-ttu-id="da71f-107">사용자가 해당 Azure AD 계정으로 ClickTime(Single Sign-on)에 자동으로 로그온되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-107">You can enable your users to automatically get signed-on to ClickTime (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="da71f-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="da71f-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="da71f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="da71f-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="da71f-110">Prerequisites</span></span>

<span data-ttu-id="da71f-111">ClickTime과 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-111">To configure Azure AD integration with ClickTime, you need the following items:</span></span>

- <span data-ttu-id="da71f-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="da71f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="da71f-113">ClickTime Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="da71f-113">A ClickTime single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="da71f-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="da71f-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="da71f-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="da71f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="da71f-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="da71f-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="da71f-118">Scenario description</span></span>
<span data-ttu-id="da71f-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="da71f-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="da71f-121">갤러리에서 ClickTime 추가</span><span class="sxs-lookup"><span data-stu-id="da71f-121">Adding ClickTime from the gallery</span></span>
2. <span data-ttu-id="da71f-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="da71f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-clicktime-from-the-gallery"></a><span data-ttu-id="da71f-123">갤러리에서 ClickTime 추가</span><span class="sxs-lookup"><span data-stu-id="da71f-123">Adding ClickTime from the gallery</span></span>
<span data-ttu-id="da71f-124">ClickTime의 Azure AD 통합을 구성하려면 갤러리의 ClickTime을 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-124">To configure the integration of ClickTime into Azure AD, you need to add ClickTime from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="da71f-125">**갤러리에서 ClickTime을 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="da71f-125">**To add ClickTime from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="da71f-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory 단추][1]

2. <span data-ttu-id="da71f-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="da71f-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-129">Then go to **All applications**.</span></span>

    ![엔터프라이즈 응용 프로그램 블레이드][2]
    
3. <span data-ttu-id="da71f-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![새 응용 프로그램 단추][3]

4. <span data-ttu-id="da71f-133">검색 상자에 **ClickTime**을 입력하고 결과 패널에서 **ClickTime**을 선택한 후 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-133">In the search box, type **ClickTime**, select **ClickTime** from result panel then click **Add** button to add the application.</span></span>

    ![결과 목록의 ClickTime](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="da71f-135">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="da71f-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="da71f-136">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 ClickTime에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-136">In this section, you configure and test Azure AD single sign-on with ClickTime based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="da71f-137">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 ClickTime 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-137">For single sign-on to work, Azure AD needs to know what the counterpart user in ClickTime is to a user in Azure AD.</span></span> <span data-ttu-id="da71f-138">즉, Azure AD 사용자와 ClickTime의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-138">In other words, a link relationship between an Azure AD user and the related user in ClickTime needs to be established.</span></span>

<span data-ttu-id="da71f-139">ClickTime에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-139">In ClickTime, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="da71f-140">ClickTime에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-140">To configure and test Azure AD single sign-on with ClickTime, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="da71f-141">**[Azure AD Single Sign-On 구성](#configure-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="da71f-142">**[Azure AD 테스트 사용자 만들기](#create-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="da71f-143">**[ClickTime 테스트 사용자 만들기](#create-a-clicktime-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 ClickTime에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-143">**[Create a ClickTime test user](#create-a-clicktime-test-user)** - to have a counterpart of Britta Simon in ClickTime that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="da71f-144">**[Azure AD 테스트 사용자 할당](#assign-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="da71f-145">**[Single Sign-On 테스트](#test-single-sign-on)** - 구성이 작동하는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="da71f-146">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="da71f-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="da71f-147">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 ClickTime 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ClickTime application.</span></span>

<span data-ttu-id="da71f-148">**ClickTime에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="da71f-148">**To configure Azure AD single sign-on with ClickTime, perform the following steps:**</span></span>

1. <span data-ttu-id="da71f-149">Azure Portal의 **ClickTime** 응용 프로그램 통합 페이지에서 **Single sign-on**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-149">In the Azure portal, on the **ClickTime** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-On 구성 링크][4]

2. <span data-ttu-id="da71f-151">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_samlbase.png)

3. <span data-ttu-id="da71f-153">**ClickTime 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-153">On the **ClickTime Domain and URLs** section, perform the following steps:</span></span>

    ![ClickTime 도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_url.png)

    <span data-ttu-id="da71f-155">a.</span><span class="sxs-lookup"><span data-stu-id="da71f-155">a.</span></span> <span data-ttu-id="da71f-156">**식별자** 텍스트 상자에 URL `https://app.clicktime.com/sp/`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-156">In the **Identifier** textbox, type a URL as: `https://app.clicktime.com/sp/`</span></span>
    
    <span data-ttu-id="da71f-157">b.</span><span class="sxs-lookup"><span data-stu-id="da71f-157">b.</span></span> <span data-ttu-id="da71f-158">**회신 URL** 텍스트 상자에 다음 패턴으로 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-158">In the **Reply URL** textbox, type a URL using the following patterns:</span></span> 

    | |
    |--|
    | `https://app.clicktime.com/Login/` |
    | `https://app.clicktime.com/App/Login/Consume.aspx` |

4. <span data-ttu-id="da71f-159">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-159">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![인증서 다운로드 링크](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_certificate.png) 

5. <span data-ttu-id="da71f-161">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-161">Click **Save** button.</span></span>

    ![Single Sign-On 구성 저장 단추](./media/active-directory-saas-clicktime-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="da71f-163">**ClickTime 구성** 섹션에서 **ClickTime 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-163">On the **ClickTime Configuration** section, click **Configure ClickTime** to open **Configure sign-on** window.</span></span> <span data-ttu-id="da71f-164">**빠른 참조 섹션**에서 **SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-164">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![ClickTime 구성](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_configure.png) 

7. <span data-ttu-id="da71f-166">다른 웹 브라우저 창에서 ClickTime 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-166">In a different web browser window, log into your ClickTime company site as an administrator.</span></span>

8. <span data-ttu-id="da71f-167">위쪽에 도구 모음에서 **기본 설정**을 클릭한 다음 **보안 설정** 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-167">In the toolbar on the top, click **Preferences**, and then click **Security Settings**.</span></span>

9. <span data-ttu-id="da71f-168">**Single Sign-On 선호도** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-168">In the **Single Sign-On Preferences** configuration section, perform the following steps:</span></span>
   
    <span data-ttu-id="da71f-169">![보안 설정](./media/active-directory-saas-clicktime-tutorial/tic777280.png "보안 설정")</span><span class="sxs-lookup"><span data-stu-id="da71f-169">![Security Settings](./media/active-directory-saas-clicktime-tutorial/tic777280.png "Security Settings")</span></span>
   
    <span data-ttu-id="da71f-170">a.</span><span class="sxs-lookup"><span data-stu-id="da71f-170">a.</span></span>  <span data-ttu-id="da71f-171">**Azure AD**와 SSO(Single Sign-On)를 사용하여 로그인 **허용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-171">Select **Allow** sign-in using Single Sign-On (SSO) with **Azure AD**.</span></span>
   
    <span data-ttu-id="da71f-172">b.</span><span class="sxs-lookup"><span data-stu-id="da71f-172">b.</span></span> <span data-ttu-id="da71f-173">Azure Portal에서 복사한 **SAML Single Sign-On 서비스 URL**을 **ID 공급자 끝점** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-173">In the **Identity Provider Endpoint** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="da71f-174">c.</span><span class="sxs-lookup"><span data-stu-id="da71f-174">c.</span></span>  <span data-ttu-id="da71f-175">Azure Portal에서 다운로드한 **base-64로 인코딩된 인증서**를 **메모장**에서 열고, 콘텐츠를 복사한 다음, **X.509 인증서** 텍스트 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-175">Open the **base-64 encoded certificate** downloaded from Azure portal in **Notepad**, copy the content, and then paste it into the **X.509 Certificate** textbox.</span></span>
   
    <span data-ttu-id="da71f-176">d.</span><span class="sxs-lookup"><span data-stu-id="da71f-176">d.</span></span>  <span data-ttu-id="da71f-177">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-177">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="da71f-178">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-178">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="da71f-179">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-179">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="da71f-180">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-180">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="da71f-181">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="da71f-181">Create an Azure AD test user</span></span>
<span data-ttu-id="da71f-182">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-182">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 테스트 사용자 만들기][100]

<span data-ttu-id="da71f-184">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="da71f-184">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="da71f-185">Azure Portal의 왼쪽 창에서 **Azure Active Directory** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-185">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Azure Active Directory 단추](./media/active-directory-saas-clicktime-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="da71f-187">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-187">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>
    
    !["사용자 및 그룹" 및 "모든 사용자" 링크](./media/active-directory-saas-clicktime-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="da71f-189">**사용자** 대화 상자를 열려면 **모든 사용자** 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-189">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>
 
    ![추가 단추](./media/active-directory-saas-clicktime-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="da71f-191">**사용자** 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-191">In the **User** dialog box, perform the following steps:</span></span>
 
    ![사용자 대화 상자](./media/active-directory-saas-clicktime-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="da71f-193">a.</span><span class="sxs-lookup"><span data-stu-id="da71f-193">a.</span></span> <span data-ttu-id="da71f-194">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-194">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="da71f-195">b.</span><span class="sxs-lookup"><span data-stu-id="da71f-195">b.</span></span> <span data-ttu-id="da71f-196">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-196">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="da71f-197">c.</span><span class="sxs-lookup"><span data-stu-id="da71f-197">c.</span></span> <span data-ttu-id="da71f-198">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-198">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="da71f-199">d.</span><span class="sxs-lookup"><span data-stu-id="da71f-199">d.</span></span> <span data-ttu-id="da71f-200">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-200">Click **Create**.</span></span>
 
### <a name="create-a-clicktime-test-user"></a><span data-ttu-id="da71f-201">ClickTime 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="da71f-201">Create a ClickTime test user</span></span>

<span data-ttu-id="da71f-202">Azure AD 사용자가 ClickTime에 로그인할 수 있도록 하려면 ClickTime로 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-202">In order to enable Azure AD users to log into ClickTime, they must be provisioned into ClickTime.</span></span>  
<span data-ttu-id="da71f-203">ClickTime의 경우 프로비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-203">In the case of ClickTime, provisioning is a manual task.</span></span>

> [!NOTE]
> <span data-ttu-id="da71f-204">다른 ClickTime 사용자 계정 생성 도구 또는 ClickTime이 제공한 API를 사용하여 Azure AD 사용자 계정을 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-204">You can use any other ClickTime user account creation tools or APIs provided by ClickTime to provision Azure AD user accounts.</span></span>

<span data-ttu-id="da71f-205">**사용자 계정을 프로비전하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="da71f-205">**To provision a user account, perform the following steps:**</span></span>
1. <span data-ttu-id="da71f-206">**ClickTime** 테넌트에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-206">Log in to your **ClickTime** tenant.</span></span>
2. <span data-ttu-id="da71f-207">위쪽에 도구 모음에서 **회사**를 클릭한 다음 **피플**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-207">In the toolbar on the top, click **Company**, and then click **People**.</span></span>
   
    <span data-ttu-id="da71f-208">![사람](./media/active-directory-saas-clicktime-tutorial/tic777282.png "사람")</span><span class="sxs-lookup"><span data-stu-id="da71f-208">![People](./media/active-directory-saas-clicktime-tutorial/tic777282.png "People")</span></span>
3. <span data-ttu-id="da71f-209">**사람 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-209">Click **Add Person**.</span></span>
   
    <span data-ttu-id="da71f-210">![사람 추가](./media/active-directory-saas-clicktime-tutorial/tic777283.png "사람 추가")</span><span class="sxs-lookup"><span data-stu-id="da71f-210">![Add Person](./media/active-directory-saas-clicktime-tutorial/tic777283.png "Add Person")</span></span>
4. <span data-ttu-id="da71f-211">새 사람 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-211">In the New Person section, perform the following steps:</span></span>
   
    <span data-ttu-id="da71f-212">![사람](./media/active-directory-saas-clicktime-tutorial/tic777284.png "사람")</span><span class="sxs-lookup"><span data-stu-id="da71f-212">![People](./media/active-directory-saas-clicktime-tutorial/tic777284.png "People")</span></span>
   
    <span data-ttu-id="da71f-213">a.</span><span class="sxs-lookup"><span data-stu-id="da71f-213">a.</span></span>  <span data-ttu-id="da71f-214">**전체 이름** 텍스트 상자에서 **Britta Simon**과 같은 사용자의 전체 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-214">In the **full name** textbox, type full name of user like **Britta Simon**.</span></span> 
  
    <span data-ttu-id="da71f-215">b.</span><span class="sxs-lookup"><span data-stu-id="da71f-215">b.</span></span>  <span data-ttu-id="da71f-216">**이메일 주소** 텍스트 상자에서 **brittasimon@contoso.com**과 같은 사용자의 이메일을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-216">In the **email address** textbox, type the email of user like **brittasimon@contoso.com**.</span></span>
       
    > [!NOTE]
    > <span data-ttu-id="da71f-217">원한다면 새 사람 개체의 추가 속성을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-217">If you want to, you can set additional properties of the new person object.</span></span>
   
    <span data-ttu-id="da71f-218">c.</span><span class="sxs-lookup"><span data-stu-id="da71f-218">c.</span></span>  <span data-ttu-id="da71f-219">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-219">Click **Save**.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="da71f-220">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="da71f-220">Assign the Azure AD test user</span></span>

<span data-ttu-id="da71f-221">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 ClickTime에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ClickTime.</span></span>

![사용자 역할 할당][200] 

<span data-ttu-id="da71f-223">**Britta Simon을 ClickTime에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="da71f-223">**To assign Britta Simon to ClickTime, perform the following steps:**</span></span>

1. <span data-ttu-id="da71f-224">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="da71f-226">응용 프로그램 목록에서 **ClickTime**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-226">In the applications list, select **ClickTime**.</span></span>

    ![응용 프로그램 목록의 ClickTimne 링크](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_app.png) 

3. <span data-ttu-id="da71f-228">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-228">In the menu on the left, click **Users and groups**.</span></span>

    !["사용자 및 그룹" 링크][202] 

4. <span data-ttu-id="da71f-230">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-230">Click **Add** button.</span></span> <span data-ttu-id="da71f-231">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![할당 추가 창][203]

5. <span data-ttu-id="da71f-233">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="da71f-234">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="da71f-235">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="da71f-236">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="da71f-236">Test single sign-on</span></span>

<span data-ttu-id="da71f-237">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="da71f-238">액세스 패널에서 ClickTime 타일을 클릭하면 ClickTime 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="da71f-238">When you click the ClickTime tile in the Access Panel, you should get automatically signed-on to your ClickTime application.</span></span>
<span data-ttu-id="da71f-239">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="da71f-239">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="da71f-240">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="da71f-240">Additional resources</span></span>

* [<span data-ttu-id="da71f-241">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="da71f-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="da71f-242">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="da71f-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_203.png

