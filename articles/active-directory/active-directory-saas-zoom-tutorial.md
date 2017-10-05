---
title: "자습서: Azure Active Directory와 Zoom 통합 | Microsoft Docs"
description: "Azure Active Directory와 Zoom 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0ebdab6c-83a8-4737-a86a-974f37269c31
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: aab491f162fd4d24c6ff4d8858f2edd96dda30d4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zoom"></a><span data-ttu-id="f66b5-103">자습서: Azure Active Directory와 Zoom 통합</span><span class="sxs-lookup"><span data-stu-id="f66b5-103">Tutorial: Azure Active Directory integration with Zoom</span></span>

<span data-ttu-id="f66b5-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Zoom을 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-104">In this tutorial, you learn how to integrate Zoom with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f66b5-105">Zoom을 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-105">Integrating Zoom with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f66b5-106">Zoom에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-106">You can control in Azure AD who has access to Zoom.</span></span>
- <span data-ttu-id="f66b5-107">사용자가 해당 Azure AD 계정으로 Zoom에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-107">You can enable your users to automatically get signed-on to Zoom (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="f66b5-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="f66b5-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f66b5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f66b5-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="f66b5-110">Prerequisites</span></span>

<span data-ttu-id="f66b5-111">Zoom과 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-111">To configure Azure AD integration with Zoom, you need the following items:</span></span>

- <span data-ttu-id="f66b5-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="f66b5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f66b5-113">Zoom Single Sign-on이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="f66b5-113">A Zoom single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f66b5-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f66b5-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f66b5-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="f66b5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f66b5-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f66b5-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="f66b5-118">Scenario description</span></span>
<span data-ttu-id="f66b5-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f66b5-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f66b5-121">갤러리에서 Zoom 추가</span><span class="sxs-lookup"><span data-stu-id="f66b5-121">Adding Zoom from the gallery</span></span>
2. <span data-ttu-id="f66b5-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="f66b5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zoom-from-the-gallery"></a><span data-ttu-id="f66b5-123">갤러리에서 Zoom 추가</span><span class="sxs-lookup"><span data-stu-id="f66b5-123">Adding Zoom from the gallery</span></span>
<span data-ttu-id="f66b5-124">Zoom의 Azure AD 통합을 구성하려면 갤러리의 Zoom을 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-124">To configure the integration of Zoom into Azure AD, you need to add Zoom from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f66b5-125">**갤러리에서 Zoom을 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="f66b5-125">**To add Zoom from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f66b5-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory 단추][1]

2. <span data-ttu-id="f66b5-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f66b5-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-129">Then go to **All applications**.</span></span>

    ![엔터프라이즈 응용 프로그램 블레이드][2]
    
3. <span data-ttu-id="f66b5-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![새 응용 프로그램 단추][3]

4. <span data-ttu-id="f66b5-133">검색 상자에 **Zoom**을 입력하고 결과 패널에서 **Zoom**을 선택한 후 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-133">In the search box, type **Zoom**, select **Zoom** from result panel then click **Add** button to add the application.</span></span>

    ![결과 목록의 Zoom in](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="f66b5-135">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="f66b5-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="f66b5-136">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Zoom에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-136">In this section, you configure and test Azure AD single sign-on with Zoom based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f66b5-137">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Zoom 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Zoom is to a user in Azure AD.</span></span> <span data-ttu-id="f66b5-138">즉, Azure AD 사용자와 Zoom의 관련 사용자 간에 연결 관계가 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-138">In other words, a link relationship between an Azure AD user and the related user in Zoom needs to be established.</span></span>

<span data-ttu-id="f66b5-139">Zoom에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 연결 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-139">In Zoom, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f66b5-140">Zoom에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-140">To configure and test Azure AD single sign-on with Zoom, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f66b5-141">**[Azure AD Single Sign-On 구성](#configure-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f66b5-142">**[Azure AD 테스트 사용자 만들기](#create-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f66b5-143">**[Zoom 테스트 사용자 만들기](#create-a-zoom-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 Zoom에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-143">**[Create a Zoom test user](#create-a-zoom-test-user)** - to have a counterpart of Britta Simon in Zoom that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f66b5-144">**[Azure AD 테스트 사용자 할당](#assign-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f66b5-145">**[Single Sign-On 테스트](#test-single-sign-on)** - 구성이 작동하는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="f66b5-146">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="f66b5-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="f66b5-147">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Zoom 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Zoom application.</span></span>

<span data-ttu-id="f66b5-148">**Zoom에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="f66b5-148">**To configure Azure AD single sign-on with Zoom, perform the following steps:**</span></span>

1. <span data-ttu-id="f66b5-149">Azure Portal의 **Zoom** 응용 프로그램 통합 페이지에서 **Single sign-on**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-149">In the Azure portal, on the **Zoom** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-On 구성 링크][4]

2. <span data-ttu-id="f66b5-151">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_samlbase.png)

3. <span data-ttu-id="f66b5-153">**Zoom 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-153">On the **Zoom Domain and URLs** section, perform the following steps:</span></span>

    ![Zoom 도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_url.png)

    <span data-ttu-id="f66b5-155">a.</span><span class="sxs-lookup"><span data-stu-id="f66b5-155">a.</span></span> <span data-ttu-id="f66b5-156">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<companyname>.zoom.us`</span><span class="sxs-lookup"><span data-stu-id="f66b5-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.zoom.us`</span></span>

    <span data-ttu-id="f66b5-157">b.</span><span class="sxs-lookup"><span data-stu-id="f66b5-157">b.</span></span> <span data-ttu-id="f66b5-158">**식별자** 텍스트 상자에서 `https://<companyname>.zoom.us` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.zoom.us`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f66b5-159">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-159">These values are not real.</span></span> <span data-ttu-id="f66b5-160">실제 로그온 URL 및 식별자로 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="f66b5-161">이러한 값을 얻으려면 [Zoom 클라이언트 지원팀](https://support.zoom.us/hc)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="f66b5-161">Contact [Zoom Client support team](https://support.zoom.us/hc) to get these values.</span></span> 
 
4. <span data-ttu-id="f66b5-162">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-162">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![인증서 다운로드 링크](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_certificate.png) 

5. <span data-ttu-id="f66b5-164">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-164">Click **Save** button.</span></span>

    ![Single Sign-On 구성 저장 단추](./media/active-directory-saas-zoom-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f66b5-166">**Zoom 구성** 섹션에서 **Zoom 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-166">On the **Zoom Configuration** section, click **Configure Zoom** to open **Configure sign-on** window.</span></span> <span data-ttu-id="f66b5-167">**빠른 참조 섹션**에서 **로그아웃 URL, SAML 엔터티 ID 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-167">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Zoom 구성](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_configure.png) 

7. <span data-ttu-id="f66b5-169">다른 웹 브라우저 창에서 관리자 권한으로 Zoom 회사 사이트에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-169">In a different web browser window, log in to your Zoom company site as an administrator.</span></span>

8. <span data-ttu-id="f66b5-170">**Single Sign-On** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-170">Click the **Single Sign-On** tab.</span></span>
   
    <span data-ttu-id="f66b5-171">![Single Sign-On 탭](./media/active-directory-saas-zoom-tutorial/IC784700.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="f66b5-171">![Single sign-on tab](./media/active-directory-saas-zoom-tutorial/IC784700.png "Single sign-on")</span></span>

9. <span data-ttu-id="f66b5-172">**보안 제어**를 클릭하고, **Single Sign-On** 설정으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-172">Click the **Security Control** tab, and then go to the **Single Sign-On** settings.</span></span>

10. <span data-ttu-id="f66b5-173">Single Sign-On 섹션에서 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-173">In the Single Sign-On section, perform the following steps:</span></span>
   
    <span data-ttu-id="f66b5-174">![Single Sign-On 섹션](./media/active-directory-saas-zoom-tutorial/IC784701.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="f66b5-174">![Single sign-on section](./media/active-directory-saas-zoom-tutorial/IC784701.png "Single sign-on")</span></span>
   
    <span data-ttu-id="f66b5-175">a.</span><span class="sxs-lookup"><span data-stu-id="f66b5-175">a.</span></span> <span data-ttu-id="f66b5-176">Azure Portal에서 복사한 **SAML Single Sign-On 서비스 URL** 값을 **로그인 페이지 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-176">In the **Sign-in page URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="f66b5-177">b.</span><span class="sxs-lookup"><span data-stu-id="f66b5-177">b.</span></span> <span data-ttu-id="f66b5-178">Azure Portal에서 복사한 **로그아웃 URL** 값을 **로그아웃 페이지 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-178">In the **Sign-out page URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>
     
    <span data-ttu-id="f66b5-179">c.</span><span class="sxs-lookup"><span data-stu-id="f66b5-179">c.</span></span> <span data-ttu-id="f66b5-180">Base 64로 인코딩된 인증서를 메모장에서 열고, 내용을 클립보드에 복사한 다음 **ID 공급자 인증서** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-180">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **Identity provider certificate** textbox.</span></span>

    <span data-ttu-id="f66b5-181">d.</span><span class="sxs-lookup"><span data-stu-id="f66b5-181">d.</span></span> <span data-ttu-id="f66b5-182">Azure Portal에서 복사한 **SAML 엔터티 ID** 값을 **발급자** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-182">In the **Issuer** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="f66b5-183">e.</span><span class="sxs-lookup"><span data-stu-id="f66b5-183">e.</span></span> <span data-ttu-id="f66b5-184">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-184">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="f66b5-185">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-185">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f66b5-186">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-186">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f66b5-187">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-187">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="f66b5-188">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="f66b5-188">Create an Azure AD test user</span></span>

<span data-ttu-id="f66b5-189">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Azure AD 테스트 사용자 만들기][100]

<span data-ttu-id="f66b5-191">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="f66b5-191">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f66b5-192">Azure Portal의 왼쪽 창에서 **Azure Active Directory** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-192">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Azure Active Directory 단추](./media/active-directory-saas-zoom-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="f66b5-194">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-194">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !["사용자 및 그룹" 및 "모든 사용자" 링크](./media/active-directory-saas-zoom-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="f66b5-196">**사용자** 대화 상자를 열려면 **모든 사용자** 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-196">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![추가 단추](./media/active-directory-saas-zoom-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="f66b5-198">**사용자** 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-198">In the **User** dialog box, perform the following steps:</span></span>

    ![사용자 대화 상자](./media/active-directory-saas-zoom-tutorial/create_aaduser_04.png)

    <span data-ttu-id="f66b5-200">a.</span><span class="sxs-lookup"><span data-stu-id="f66b5-200">a.</span></span> <span data-ttu-id="f66b5-201">**이름** 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-201">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f66b5-202">b.</span><span class="sxs-lookup"><span data-stu-id="f66b5-202">b.</span></span> <span data-ttu-id="f66b5-203">**사용자 이름** 상자에 사용자인 Britta Simon의 전자 메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-203">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="f66b5-204">c.</span><span class="sxs-lookup"><span data-stu-id="f66b5-204">c.</span></span> <span data-ttu-id="f66b5-205">**암호 표시** 확인란을 선택한 다음 **암호** 상자에 표시된 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-205">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="f66b5-206">d.</span><span class="sxs-lookup"><span data-stu-id="f66b5-206">d.</span></span> <span data-ttu-id="f66b5-207">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-207">Click **Create**.</span></span>
 
### <a name="create-a-zoom-test-user"></a><span data-ttu-id="f66b5-208">Zoom 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="f66b5-208">Create a Zoom test user</span></span>

<span data-ttu-id="f66b5-209">Azure AD 사용자가 Zoom에 로그인할 수 있도록 하려면 사용자 계정이 Zoom으로 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-209">In order to enable Azure AD users to log in to Zoom, they must be provisioned into Zoom.</span></span> <span data-ttu-id="f66b5-210">Zoom의 경우, 수동으로 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-210">In the case of Zoom, provisioning is a manual task.</span></span>

### <a name="to-provision-a-user-account-perform-the-following-steps"></a><span data-ttu-id="f66b5-211">사용자 계정을 프로비저닝하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-211">To provision a user account, perform the following steps:</span></span>

1. <span data-ttu-id="f66b5-212">관리자 권한으로 **Zoom** 회사 사이트로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-212">Log in to your **Zoom** company site as an administrator.</span></span>
 
2. <span data-ttu-id="f66b5-213">**계정 관리** 탭을 클릭한 후 **사용자 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-213">Click the **Account Management** tab, and then click **User Management**.</span></span>

3. <span data-ttu-id="f66b5-214">사용자 관리 섹션에서 **사용자 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-214">In the User Management section, click **Add users**.</span></span>
   
    <span data-ttu-id="f66b5-215">![사용자 관리](./media/active-directory-saas-zoom-tutorial/IC784703.png "사용자 관리")</span><span class="sxs-lookup"><span data-stu-id="f66b5-215">![User management](./media/active-directory-saas-zoom-tutorial/IC784703.png "User management")</span></span>

4. <span data-ttu-id="f66b5-216">**사용자 추가** 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-216">On the **Add users** page, perform the following steps:</span></span>
   
    <span data-ttu-id="f66b5-217">![사용자 추가](./media/active-directory-saas-zoom-tutorial/IC784704.png "사용자 추가")</span><span class="sxs-lookup"><span data-stu-id="f66b5-217">![Add users](./media/active-directory-saas-zoom-tutorial/IC784704.png "Add users")</span></span>
   
    <span data-ttu-id="f66b5-218">a.</span><span class="sxs-lookup"><span data-stu-id="f66b5-218">a.</span></span> <span data-ttu-id="f66b5-219">**사용자 유형**으로 **기본**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-219">As **User Type**, select **Basic**.</span></span>

    <span data-ttu-id="f66b5-220">b.</span><span class="sxs-lookup"><span data-stu-id="f66b5-220">b.</span></span> <span data-ttu-id="f66b5-221">**이메일** 텍스트 상자에 프로비전하려는 유효한 Azure AD 계정의 이메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-221">In the **Emails** textbox, type the email address of a valid Azure AD account you want to provision.</span></span>

    <span data-ttu-id="f66b5-222">c.</span><span class="sxs-lookup"><span data-stu-id="f66b5-222">c.</span></span> <span data-ttu-id="f66b5-223">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-223">Click **Add**.</span></span>

> [!NOTE]
> <span data-ttu-id="f66b5-224">Zoom에서 제공하는 다른 Zoom 사용자 계정 만들기 도구 또는 API를 사용하여 Azure Active Directory 사용자 계정을 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-224">You can use any other Zoom user account creation tools or APIs provided by Zoom to provision Azure Active Directory user accounts.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="f66b5-225">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="f66b5-225">Assign the Azure AD test user</span></span>

<span data-ttu-id="f66b5-226">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Zoom에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Zoom.</span></span>

![사용자 역할 할당][200] 

<span data-ttu-id="f66b5-228">**Britta Simon을 Zoom에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="f66b5-228">**To assign Britta Simon to Zoom, perform the following steps:**</span></span>

1. <span data-ttu-id="f66b5-229">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-229">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="f66b5-231">응용 프로그램 목록에서 **Zoom**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-231">In the applications list, select **Zoom**.</span></span>

    ![응용 프로그램 목록의 Zoom 연결](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_app.png)  

3. <span data-ttu-id="f66b5-233">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-233">In the menu on the left, click **Users and groups**.</span></span>

    !["사용자 및 그룹" 링크][202]

4. <span data-ttu-id="f66b5-235">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-235">Click **Add** button.</span></span> <span data-ttu-id="f66b5-236">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![할당 추가 창][203]

5. <span data-ttu-id="f66b5-238">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f66b5-239">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f66b5-240">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="f66b5-241">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="f66b5-241">Test single sign-on</span></span>

<span data-ttu-id="f66b5-242">이 섹션은 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-242">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f66b5-243">액세스 패널에서 Zoom 타일을 클릭하면 Zoom 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="f66b5-243">When you click the Zoom tile in the Access Panel, you should get automatically signed-on to your Zoom application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f66b5-244">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="f66b5-244">Additional resources</span></span>

* [<span data-ttu-id="f66b5-245">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="f66b5-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f66b5-246">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="f66b5-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_203.png

