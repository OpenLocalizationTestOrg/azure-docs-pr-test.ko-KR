---
title: "자습서: Citrix ShareFile과 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory 및 Citrix ShareFile 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: e14fc310-bac4-4f09-99ef-87e5c77288b6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2017
ms.author: jeedes
ms.openlocfilehash: b85680104fe4f33638c559b2a12483a2312a4476
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-citrix-sharefile"></a><span data-ttu-id="f0318-103">자습서: Citrix ShareFile과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="f0318-103">Tutorial: Azure Active Directory integration with Citrix ShareFile</span></span>

<span data-ttu-id="f0318-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Citrix ShareFile을 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-104">In this tutorial, you learn how to integrate Citrix ShareFile with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f0318-105">Citrix ShareFile을 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-105">Integrating Citrix ShareFile with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f0318-106">Citrix ShareFile에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-106">You can control in Azure AD who has access to Citrix ShareFile.</span></span>
- <span data-ttu-id="f0318-107">사용자가 해당 Azure AD 계정으로 Citrix ShareFile에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-107">You can enable your users to automatically get signed-on to Citrix ShareFile (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="f0318-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="f0318-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f0318-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f0318-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="f0318-110">Prerequisites</span></span>

<span data-ttu-id="f0318-111">Citrix ShareFile과의 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-111">To configure Azure AD integration with Citrix ShareFile, you need the following items:</span></span>

- <span data-ttu-id="f0318-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="f0318-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f0318-113">Citrix ShareFile Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="f0318-113">A Citrix ShareFile single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f0318-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f0318-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f0318-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="f0318-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f0318-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f0318-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="f0318-118">Scenario description</span></span>
<span data-ttu-id="f0318-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f0318-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f0318-121">갤러리에서 Citrix ShareFile 추가</span><span class="sxs-lookup"><span data-stu-id="f0318-121">Add Citrix ShareFile from the gallery</span></span>
2. <span data-ttu-id="f0318-122">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="f0318-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-citrix-sharefile-from-the-gallery"></a><span data-ttu-id="f0318-123">갤러리에서 Citrix ShareFile 추가</span><span class="sxs-lookup"><span data-stu-id="f0318-123">Add Citrix ShareFile from the gallery</span></span>
<span data-ttu-id="f0318-124">Citrix ShareFile의 Azure AD 통합을 구성하려면 갤러리의 Citrix ShareFile을 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-124">To configure the integration of Citrix ShareFile into Azure AD, you need to add Citrix ShareFile from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f0318-125">**갤러리에서 Citrix ShareFile을 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="f0318-125">**To add Citrix ShareFile from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f0318-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory 단추][1]

2. <span data-ttu-id="f0318-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f0318-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-129">Then go to **All applications**.</span></span>

    ![엔터프라이즈 응용 프로그램 블레이드][2]
    
3. <span data-ttu-id="f0318-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![새 응용 프로그램 단추][3]

4. <span data-ttu-id="f0318-133">검색 상자에 **Citrix ShareFile**을 입력하고 결과 패널에서 **Citrix ShareFile**을 선택한 후 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-133">In the search box, type **Citrix ShareFile**, select **Citrix ShareFile** from result panel then click **Add** button to add the application.</span></span>

    ![결과 목록에서 Citrix ShareFile](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="f0318-135">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="f0318-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="f0318-136">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Citrix ShareFile에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-136">In this section, you configure and test Azure AD single sign-on with Citrix ShareFile based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f0318-137">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Citrix ShareFile 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Citrix ShareFile is to a user in Azure AD.</span></span> <span data-ttu-id="f0318-138">즉, Azure AD 사용자와 Citrix ShareFile의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-138">In other words, a link relationship between an Azure AD user and the related user in Citrix ShareFile needs to be established.</span></span>

<span data-ttu-id="f0318-139">Citrix ShareFile에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-139">In Citrix ShareFile, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f0318-140">Citrix ShareFile에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-140">To configure and test Azure AD single sign-on with Citrix ShareFile, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f0318-141">**[Azure AD Single Sign-On 구성](#configure-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f0318-142">**[Azure AD 테스트 사용자 만들기](#create-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f0318-143">**[Citrix ShareFile 테스트 사용자 만들기](#create-a-citrix-sharefile-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 Citrix ShareFile에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-143">**[Create a Citrix ShareFile test user](#create-a-citrix-sharefile-test-user)** - to have a counterpart of Britta Simon in Citrix ShareFile that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f0318-144">**[Azure AD 테스트 사용자 할당](#assign-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f0318-145">**[Single Sign-On 테스트](#test-single-sign-on)** - 구성이 작동하는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="f0318-146">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="f0318-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="f0318-147">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Citrix ShareFile 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Citrix ShareFile application.</span></span>

<span data-ttu-id="f0318-148">**Citrix ShareFile에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="f0318-148">**To configure Azure AD single sign-on with Citrix ShareFile, perform the following steps:**</span></span>

1. <span data-ttu-id="f0318-149">Azure Portal의 **Citrix ShareFile** 응용 프로그램 통합 페이지에서 **Single sign-on**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-149">In the Azure portal, on the **Citrix ShareFile** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-On 구성 링크][4]

2. <span data-ttu-id="f0318-151">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_samlbase.png)

3. <span data-ttu-id="f0318-153">**Citrix ShareFile 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-153">On the **Citrix ShareFile Domain and URLs** section, perform the following steps:</span></span>

    ![Citrix ShareFile 도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_url.png)
    
    <span data-ttu-id="f0318-155">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<tenant-name>.sharefile.com/saml/login`</span><span class="sxs-lookup"><span data-stu-id="f0318-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.sharefile.com/saml/login`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f0318-156">이 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-156">This value is not real.</span></span> <span data-ttu-id="f0318-157">이 값을 실제 로그온 URL로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-157">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="f0318-158">이 값을 얻으려면 [Citrix ShareFile 클라이언트 지원 팀](https://www.citrix.co.in/products/sharefile/support.html)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="f0318-158">Contact [Citrix ShareFile Client support team](https://www.citrix.co.in/products/sharefile/support.html) to get this value.</span></span> 

4. <span data-ttu-id="f0318-159">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-159">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![인증서 다운로드 링크](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_certificate.png) 

5. <span data-ttu-id="f0318-161">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-161">Click **Save** button.</span></span>

    ![Single Sign-On 구성 저장 단추](./media/active-directory-saas-sharefile-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f0318-163">**Citrix ShareFile 구성** 섹션에서 **Citrix ShareFile 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-163">On the **Citrix ShareFile Configuration** section, click **Configure Citrix ShareFile** to open **Configure sign-on** window.</span></span> <span data-ttu-id="f0318-164">**빠른 참조 섹션**에서 **로그아웃 URL, SAML 엔터티 ID 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-164">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Citrix ShareFile 구성](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_configure.png) 

7. <span data-ttu-id="f0318-166">다른 웹 브라우저 창에서 **Citrix ShareFile** 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-166">In a different web browser window, log into your **Citrix ShareFile** company site as an administrator.</span></span>

8. <span data-ttu-id="f0318-167">위쪽에 도구 모음에서 **관리자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-167">In the toolbar on the top, click **Admin**.</span></span>

9. <span data-ttu-id="f0318-168">왼쪽 탐색 창에서 **Single Sign-On 구성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-168">In the left navigation pane, select **Configure Single Sign-On**.</span></span>
   
    <span data-ttu-id="f0318-169">![계정 관리](./media/active-directory-saas-sharefile-tutorial/ic773627.png "계정 관리")</span><span class="sxs-lookup"><span data-stu-id="f0318-169">![Account Administration](./media/active-directory-saas-sharefile-tutorial/ic773627.png "Account Administration")</span></span>

10. <span data-ttu-id="f0318-170">**기본 설정**의 **Single Sign-on/SAML 2.0 구성** 대화 상자 페이지에서 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-170">On the **Single Sign-On/ SAML 2.0 Configuration** dialog page under **Basic Settings**, perform the following steps:</span></span>
   
    <span data-ttu-id="f0318-171">![Single Sign-On](./media/active-directory-saas-sharefile-tutorial/ic773628.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="f0318-171">![Single sign-on](./media/active-directory-saas-sharefile-tutorial/ic773628.png "Single sign-on")</span></span>
   
    <span data-ttu-id="f0318-172">a.</span><span class="sxs-lookup"><span data-stu-id="f0318-172">a.</span></span> <span data-ttu-id="f0318-173">**SAML 사용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-173">Click **Enable SAML**.</span></span>
    
    <span data-ttu-id="f0318-174">b.</span><span class="sxs-lookup"><span data-stu-id="f0318-174">b.</span></span> <span data-ttu-id="f0318-175">Azure Portal에서 복사한 **SAML 엔터티 ID** 값을 **IDP 발급자/엔터티 ID** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-175">In **Your IDP Issuer/ Entity ID** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="f0318-176">c.</span><span class="sxs-lookup"><span data-stu-id="f0318-176">c.</span></span> <span data-ttu-id="f0318-177">**X.509 인증서** 필드 옆의 **변경**을 클릭한 다음 Azure Portal에서 다운로드한 인증서를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-177">Click **Change** next to the **X.509 Certificate** field and then upload the certificate you downloaded from the Azure portal.</span></span>
    
    <span data-ttu-id="f0318-178">d.</span><span class="sxs-lookup"><span data-stu-id="f0318-178">d.</span></span> <span data-ttu-id="f0318-179">Azure Portal에서 복사한 **SAML Single Sign-On 서비스 URL** 값을 **로그인 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-179">In **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="f0318-180">e.</span><span class="sxs-lookup"><span data-stu-id="f0318-180">e.</span></span> <span data-ttu-id="f0318-181">Azure Portal에서 복사한 **로그아웃 URL** 값을 **로그아웃 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-181">In **Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

11. <span data-ttu-id="f0318-182">Citrix ShareFile 관리 포털에서 **저장** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-182">Click **Save** on the Citrix ShareFile management portal.</span></span>

> [!TIP]
> <span data-ttu-id="f0318-183">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-183">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f0318-184">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-184">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f0318-185">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-185">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="f0318-186">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="f0318-186">Create an Azure AD test user</span></span>

<span data-ttu-id="f0318-187">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Azure AD 테스트 사용자 만들기][100]

<span data-ttu-id="f0318-189">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="f0318-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f0318-190">Azure Portal의 왼쪽 창에서 **Azure Active Directory** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-190">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Azure Active Directory 단추](./media/active-directory-saas-sharefile-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="f0318-192">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-192">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !["사용자 및 그룹" 및 "모든 사용자" 링크](./media/active-directory-saas-sharefile-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="f0318-194">**사용자** 대화 상자를 열려면 **모든 사용자** 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-194">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![추가 단추](./media/active-directory-saas-sharefile-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="f0318-196">**사용자** 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-196">In the **User** dialog box, perform the following steps:</span></span>

    ![사용자 대화 상자](./media/active-directory-saas-sharefile-tutorial/create_aaduser_04.png)

    <span data-ttu-id="f0318-198">a.</span><span class="sxs-lookup"><span data-stu-id="f0318-198">a.</span></span> <span data-ttu-id="f0318-199">**이름** 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-199">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f0318-200">b.</span><span class="sxs-lookup"><span data-stu-id="f0318-200">b.</span></span> <span data-ttu-id="f0318-201">**사용자 이름** 상자에 사용자인 Britta Simon의 전자 메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-201">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="f0318-202">c.</span><span class="sxs-lookup"><span data-stu-id="f0318-202">c.</span></span> <span data-ttu-id="f0318-203">**암호 표시** 확인란을 선택한 다음 **암호** 상자에 표시된 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-203">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="f0318-204">d.</span><span class="sxs-lookup"><span data-stu-id="f0318-204">d.</span></span> <span data-ttu-id="f0318-205">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-205">Click **Create**.</span></span>
 
### <a name="create-a-citrix-sharefile-test-user"></a><span data-ttu-id="f0318-206">Citrix ShareFile 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="f0318-206">Create a Citrix ShareFile test user</span></span>

<span data-ttu-id="f0318-207">Azure AD 사용자가 Citrix ShareFile에 로그인할 수 있도록 하려면 Citrix ShareFile로 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-207">In order to enable Azure AD users to log into Citrix ShareFile, they must be provisioned into Citrix ShareFile.</span></span> <span data-ttu-id="f0318-208">Citrix ShareFile의 경우 프로비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-208">In the case of Citrix ShareFile, provisioning is a manual task.</span></span>

<span data-ttu-id="f0318-209">**사용자 계정을 프로비전하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="f0318-209">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="f0318-210">**Citrix ShareFile** 테넌트에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-210">Log in to your **Citrix ShareFile** tenant.</span></span>

2. <span data-ttu-id="f0318-211">**사용자 관리 \> 사용자 홈 관리 \> + 직원 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-211">Click **Manage Users \> Manage Users Home \> + Create Employee**.</span></span>
   
   <span data-ttu-id="f0318-212">![직원 만들기](./media/active-directory-saas-sharefile-tutorial/IC781050.png "직원 만들기")</span><span class="sxs-lookup"><span data-stu-id="f0318-212">![Create Employee](./media/active-directory-saas-sharefile-tutorial/IC781050.png "Create Employee")</span></span>

3. <span data-ttu-id="f0318-213">**기본 정보** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-213">On the **Basic Information** section, perform below steps:</span></span>
   
   <span data-ttu-id="f0318-214">![기본 정보](./media/active-directory-saas-sharefile-tutorial/IC799951.png "기본 정보")</span><span class="sxs-lookup"><span data-stu-id="f0318-214">![Basic Information](./media/active-directory-saas-sharefile-tutorial/IC799951.png "Basic Information")</span></span>
   
   <span data-ttu-id="f0318-215">a.</span><span class="sxs-lookup"><span data-stu-id="f0318-215">a.</span></span> <span data-ttu-id="f0318-216">**이메일 주소** 텍스트 상자에 Britta Simon의 전자 메일 주소를 **brittasimon@contoso.com**으로 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-216">In the **Email Address** textbox, type the email address of Britta Simon as **brittasimon@contoso.com**.</span></span>
   
   <span data-ttu-id="f0318-217">b.</span><span class="sxs-lookup"><span data-stu-id="f0318-217">b.</span></span> <span data-ttu-id="f0318-218">**이름** 텍스트 상자에 사용자의 **이름**을 **Britta**로 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-218">In the **First Name** textbox, type **first name** of user as **Britta**.</span></span>
   
   <span data-ttu-id="f0318-219">c.</span><span class="sxs-lookup"><span data-stu-id="f0318-219">c.</span></span> <span data-ttu-id="f0318-220">**성** 텍스트 상자에 사용자의 **성**을 **Simon**으로 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-220">In the **Last Name** textbox, type **last name** of user as **Simon**.</span></span>

4. <span data-ttu-id="f0318-221">**사용자 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-221">Click **Add User**.</span></span>
  
   >[!NOTE]
   ><span data-ttu-id="f0318-222">Azure AD 계정 보유자에게 이메일이 발송되며 여기에 포함된 링크를 클릭하여 계정을 확인하면 계정이 활성화됩니다. 다른 Citrix ShareFile 사용자 계정 생성 도구 또는 Citrix ShareFile에서 제공한 API를 사용하여 Azure AD 사용자 계정을 프로비전할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-222">The Azure AD account holder will receive an email and follow a link to confirm their account before it becomes active.You can use any other Citrix ShareFile user account creation tools or APIs provided by Citrix ShareFile to provision Azure AD user accounts.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="f0318-223">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="f0318-223">Assign the Azure AD test user</span></span>

<span data-ttu-id="f0318-224">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Citrix ShareFile에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-224">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Citrix ShareFile.</span></span>

![사용자 역할 할당][200] 

<span data-ttu-id="f0318-226">**Citrix ShareFile에 Britta Simon을 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="f0318-226">**To assign Britta Simon to Citrix ShareFile, perform the following steps:**</span></span>

1. <span data-ttu-id="f0318-227">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-227">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="f0318-229">응용 프로그램 목록에서 **Citrix ShareFile**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-229">In the applications list, select **Citrix ShareFile**.</span></span>

    ![응용 프로그램 목록의 Citrix ShareFile 링크](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_app.png)  

3. <span data-ttu-id="f0318-231">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-231">In the menu on the left, click **Users and groups**.</span></span>

    !["사용자 및 그룹" 링크][202]

4. <span data-ttu-id="f0318-233">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-233">Click **Add** button.</span></span> <span data-ttu-id="f0318-234">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![할당 추가 창][203]

5. <span data-ttu-id="f0318-236">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-236">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f0318-237">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f0318-238">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="f0318-239">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="f0318-239">Test single sign-on</span></span>

<span data-ttu-id="f0318-240">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-240">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f0318-241">액세스 패널에서 Citrix ShareFile 타일을 클릭하면 Citrix ShareFile 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0318-241">When you click the Citrix ShareFile tile in the Access Panel, you should get automatically signed-on to your Citrix ShareFile application.</span></span>
<span data-ttu-id="f0318-242">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f0318-242">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="f0318-243">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="f0318-243">Additional resources</span></span>

* [<span data-ttu-id="f0318-244">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="f0318-244">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f0318-245">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="f0318-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_203.png

