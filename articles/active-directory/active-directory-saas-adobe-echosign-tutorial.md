---
title: "자습서: Adobe Sign과 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory 및 Adobe Sign 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f9385723-8fe7-4340-8afb-1508dac3e92b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/24/2017
ms.author: jeedes
ms.openlocfilehash: b413772de1af1fbb128d29b81e5831cfd6a39ab4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adobe-sign"></a><span data-ttu-id="25bae-103">자습서: Adobe Sign과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="25bae-103">Tutorial: Azure Active Directory integration with Adobe Sign</span></span>

<span data-ttu-id="25bae-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Adobe Sign을 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-104">In this tutorial, you learn how to integrate Adobe Sign with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="25bae-105">Adobe Sign과 Azure AD를 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-105">Integrating Adobe Sign with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="25bae-106">Adobe Sign에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-106">You can control in Azure AD who has access to Adobe Sign</span></span>
- <span data-ttu-id="25bae-107">사용자가 해당 Azure AD 계정으로 Adobe Sign에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-107">You can enable your users to automatically get signed-on to Adobe Sign (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="25bae-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="25bae-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="25bae-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="25bae-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="25bae-110">Prerequisites</span></span>

<span data-ttu-id="25bae-111">Adobe Sign과 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-111">To configure Azure AD integration with Adobe Sign, you need the following items:</span></span>

- <span data-ttu-id="25bae-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="25bae-112">An Azure AD subscription</span></span>
- <span data-ttu-id="25bae-113">Adobe Sign Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="25bae-113">An Adobe Sign single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="25bae-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="25bae-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="25bae-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="25bae-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="25bae-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="25bae-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="25bae-118">Scenario description</span></span>
<span data-ttu-id="25bae-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="25bae-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="25bae-121">갤러리에서 Adobe Sign 추가</span><span class="sxs-lookup"><span data-stu-id="25bae-121">Adding Adobe Sign from the gallery</span></span>
2. <span data-ttu-id="25bae-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="25bae-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adobe-sign-from-the-gallery"></a><span data-ttu-id="25bae-123">갤러리에서 Adobe Sign 추가</span><span class="sxs-lookup"><span data-stu-id="25bae-123">Adding Adobe Sign from the gallery</span></span>
<span data-ttu-id="25bae-124">Adobe Sign의 Azure AD 통합을 구성하려면 갤러리의 Adobe Sign을 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-124">To configure the integration of Adobe Sign into Azure AD, you need to add Adobe Sign from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="25bae-125">**갤러리에서 Adobe Sign을 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="25bae-125">**To add Adobe Sign from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="25bae-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="25bae-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="25bae-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="25bae-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="25bae-133">검색 상자에 **Adobe Sign**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-133">In the search box, type **Adobe Sign**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_search.png)

5. <span data-ttu-id="25bae-135">결과 패널에서 **Adobe Sign**을 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-135">In the results panel, select **Adobe Sign**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="25bae-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="25bae-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="25bae-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Adobe Sign에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-138">In this section, you configure and test Azure AD single sign-on with Adobe Sign based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="25bae-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Adobe Sign 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Adobe Sign is to a user in Azure AD.</span></span> <span data-ttu-id="25bae-140">즉, Azure AD 사용자와 Adobe Sign의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-140">In other words, a link relationship between an Azure AD user and the related user in Adobe Sign needs to be established.</span></span>

<span data-ttu-id="25bae-141">Adobe Sign에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-141">In Adobe Sign, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="25bae-142">Adobe Sign에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-142">To configure and test Azure AD single sign-on with Adobe Sign, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="25bae-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="25bae-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="25bae-145">**[Adobe Sign 테스트 사용자 만들기](#creating-an-adobe-sign-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 Adobe Sign에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-145">**[Creating an Adobe Sign test user](#creating-an-adobe-sign-test-user)** - to have a counterpart of Britta Simon in Adobe Sign that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="25bae-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="25bae-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="25bae-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="25bae-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="25bae-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Adobe Sign 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Adobe Sign application.</span></span>

<span data-ttu-id="25bae-150">**Adobe Sign에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="25bae-150">**To configure Azure AD single sign-on with Adobe Sign, perform the following steps:**</span></span>

1. <span data-ttu-id="25bae-151">Azure Portal의 **Adobe Sign** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-151">In the Azure portal, on the **Adobe Sign** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="25bae-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_samlbase.png)

3. <span data-ttu-id="25bae-155">**Adobe Sign 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-155">On the **Adobe Sign Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_url.png)

    <span data-ttu-id="25bae-157">a.</span><span class="sxs-lookup"><span data-stu-id="25bae-157">a.</span></span> <span data-ttu-id="25bae-158">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<companyname>.echosign.com/`</span><span class="sxs-lookup"><span data-stu-id="25bae-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.echosign.com/`</span></span>

    <span data-ttu-id="25bae-159">b.</span><span class="sxs-lookup"><span data-stu-id="25bae-159">b.</span></span> <span data-ttu-id="25bae-160">**식별자** 텍스트 상자에서 `https://<companyname>.echosign.com` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.echosign.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="25bae-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-161">These values are not real.</span></span> <span data-ttu-id="25bae-162">실제 로그온 URL 및 식별자로 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="25bae-163">이러한 값을 얻으려면 [Adobe Sign 클라이언트 지원팀](https://helpx.adobe.com/in/contact/support.html)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="25bae-163">Contact [Adobe Sign Client support team](https://helpx.adobe.com/in/contact/support.html) to get these values.</span></span> 
 
4. <span data-ttu-id="25bae-164">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_certificate.png) 

5. <span data-ttu-id="25bae-166">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-166">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="25bae-168">**Adobe Sign 구성** 섹션에서 **Adobe Sign 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-168">On the **Adobe Sign Configuration** section, click **Configure Adobe Sign** to open **Configure sign-on** window.</span></span> <span data-ttu-id="25bae-169">**빠른 참조 섹션**에서 **로그아웃 URL, SAML 엔터티 ID 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_configure.png) 


7. <span data-ttu-id="25bae-171">다른 웹 브라우저 창에서 Adobe Sign 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-171">In a different web browser window, log in to your Adobe Sign company site as an administrator.</span></span>

8. <span data-ttu-id="25bae-172">위쪽의 메뉴에서 **계정**을 클릭한 다음 왼쪽의 탐색 창에서 **계정 설정**의 **SAML 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-172">In the menu on the top, click **Account**, and then, in the navigation pane on the left side, click **SAML Settings** under **Account Settings**.</span></span>
   
   <span data-ttu-id="25bae-173">![계정](./media/active-directory-saas-adobe-echosign-tutorial/ic789520.png "계정")</span><span class="sxs-lookup"><span data-stu-id="25bae-173">![Account](./media/active-directory-saas-adobe-echosign-tutorial/ic789520.png "Account")</span></span>

9. <span data-ttu-id="25bae-174">SAML 설정 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-174">In the SAML Settings section, perform the following steps:</span></span>
   
   <span data-ttu-id="25bae-175">![SAML 설정](./media/active-directory-saas-adobe-echosign-tutorial/ic789521.png "SAML 설정")</span><span class="sxs-lookup"><span data-stu-id="25bae-175">![SAML Settings](./media/active-directory-saas-adobe-echosign-tutorial/ic789521.png "SAML Settings")</span></span>
   
   <span data-ttu-id="25bae-176">a.</span><span class="sxs-lookup"><span data-stu-id="25bae-176">a.</span></span> <span data-ttu-id="25bae-177">**SAML 모드**로 **SAML 필수**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-177">As **SAML Mode**, select **SAML Mandatory**.</span></span>
   
   <span data-ttu-id="25bae-178">b.</span><span class="sxs-lookup"><span data-stu-id="25bae-178">b.</span></span> <span data-ttu-id="25bae-179">**EchoSign 계정 관리자가 EchoSign 자격 증명을 사용하여 로그인할 수 있게 허용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-179">Select **Allow EchoSign Account Administrators to log in using their EchoSign Credentials**.</span></span>
   
   <span data-ttu-id="25bae-180">c.</span><span class="sxs-lookup"><span data-stu-id="25bae-180">c.</span></span> <span data-ttu-id="25bae-181">**사용자 만들기**로 **SAML을 통해 인증된 사용자를 자동으로 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-181">As **User Creation**, select **Automatically add users authenticated through SAML**.</span></span>

10. <span data-ttu-id="25bae-182">다음 단계를 수행하기 위해 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-182">Move on, performing the following steps:</span></span>

       <span data-ttu-id="25bae-183">![SAML 설정](./media/active-directory-saas-adobe-echosign-tutorial/ic789522.png "SAML 설정")</span><span class="sxs-lookup"><span data-stu-id="25bae-183">![SAML Settings](./media/active-directory-saas-adobe-echosign-tutorial/ic789522.png "SAML Settings")</span></span>

    <span data-ttu-id="25bae-184">a.</span><span class="sxs-lookup"><span data-stu-id="25bae-184">a.</span></span> <span data-ttu-id="25bae-185">Azure Portal에서 복사한 **SAML 엔터티 ID**를 **IdP 엔터티 ID** 텍스트 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-185">Paste **SAML Entity ID**, which you have copied from Azure portal into the **IdP Entity ID** textbox.</span></span>
    
    <span data-ttu-id="25bae-186">b.</span><span class="sxs-lookup"><span data-stu-id="25bae-186">b.</span></span> <span data-ttu-id="25bae-187">Azure Portal에서 복사한 **SAML Single Sign-On 서비스 URL**을 **IdP 로그인 URL** 텍스트 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-187">Paste **SAML Single Sign-On Service URL**, which you have copied from Azure portal into the **IdP Login URL** textbox.</span></span>
   
    <span data-ttu-id="25bae-188">c.</span><span class="sxs-lookup"><span data-stu-id="25bae-188">c.</span></span> <span data-ttu-id="25bae-189">Azure Portal에서 복사한 **로그아웃 URL**을 **IdP 로그아웃 URL** 텍스트 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-189">Paste **Sign-Out URL**, which you have copied from Azure portal into the **IdP Logout URL** textbox.</span></span>

    <span data-ttu-id="25bae-190">d.</span><span class="sxs-lookup"><span data-stu-id="25bae-190">d.</span></span> <span data-ttu-id="25bae-191">다운로드된 **인증서(Base64)** 파일을 메모장에서 열고, 내용을 클립보드에 복사한 다음 전체 인증서를 **IdP 인증서** 텍스트 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-191">Open your downloaded **Certificate(Base64)** file in notepad, copy the content of it into your clipboard, and then paste it to the **IdP Certificate** textbox</span></span>

    <span data-ttu-id="25bae-192">e.</span><span class="sxs-lookup"><span data-stu-id="25bae-192">e.</span></span> <span data-ttu-id="25bae-193">**변경 내용 저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-193">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="25bae-194">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="25bae-195">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="25bae-196">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="25bae-197">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="25bae-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="25bae-198">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="25bae-200">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="25bae-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="25bae-201">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="25bae-203">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="25bae-205">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="25bae-207">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="25bae-209">a.</span><span class="sxs-lookup"><span data-stu-id="25bae-209">a.</span></span> <span data-ttu-id="25bae-210">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="25bae-211">b.</span><span class="sxs-lookup"><span data-stu-id="25bae-211">b.</span></span> <span data-ttu-id="25bae-212">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="25bae-213">c.</span><span class="sxs-lookup"><span data-stu-id="25bae-213">c.</span></span> <span data-ttu-id="25bae-214">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="25bae-215">d.</span><span class="sxs-lookup"><span data-stu-id="25bae-215">d.</span></span> <span data-ttu-id="25bae-216">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-216">Click **Create**.</span></span>
 
### <a name="creating-an-adobe-sign-test-user"></a><span data-ttu-id="25bae-217">Adobe Sign 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="25bae-217">Creating an Adobe Sign test user</span></span>

<span data-ttu-id="25bae-218">Azure AD 사용자가 Adobe Sign에 로그인할 수 있도록 하려면 Adobe Sign으로 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-218">To enable Azure AD users to log in to Adobe Sign, they must be provisioned into Adobe Sign.</span></span> <span data-ttu-id="25bae-219">Adobe Sign의 경우 프로비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-219">In the case of Adobe Sign, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="25bae-220">다른 Adobe Sign 사용자 계정 생성 도구 또는 Adobe Sign이 제공한 API를 사용하여 AAD 사용자 계정을 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-220">You can use any other Adobe Sign user account creation tools or APIs provided by Adobe Sign to provision AAD user accounts.</span></span> 

<span data-ttu-id="25bae-221">**사용자 계정을 프로비전하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="25bae-221">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="25bae-222">**Adobe Sign** 회사 사이트에 관리자 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-222">Log in to your **Adobe Sign** company site as administrator.</span></span>

2. <span data-ttu-id="25bae-223">위쪽의 메뉴에서 **계정**을 클릭한 다음 왼쪽의 탐색 창에서 **사용자 및 그룹**과 **새 사용자 만들기**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-223">In the menu on the top, click **Account**, and then, in the navigation pane on the left side, click **Users & Groups**, and then, click **Create a new user**.</span></span>
   
   <span data-ttu-id="25bae-224">![계정](./media/active-directory-saas-adobe-echosign-tutorial/ic789524.png "계정")</span><span class="sxs-lookup"><span data-stu-id="25bae-224">![Account](./media/active-directory-saas-adobe-echosign-tutorial/ic789524.png "Account")</span></span>
   
3. <span data-ttu-id="25bae-225">**새 사용자 만들기** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-225">In the **Create New User** section, perform the following steps:</span></span>
   
   <span data-ttu-id="25bae-226">![사용자 만들기](./media/active-directory-saas-adobe-echosign-tutorial/ic789525.png "사용자 만들기")</span><span class="sxs-lookup"><span data-stu-id="25bae-226">![Create User](./media/active-directory-saas-adobe-echosign-tutorial/ic789525.png "Create User")</span></span>
   
   <span data-ttu-id="25bae-227">a.</span><span class="sxs-lookup"><span data-stu-id="25bae-227">a.</span></span> <span data-ttu-id="25bae-228">관련된 텍스트 상자에 프로비전할 유효한 AAD 계정의 **전자 메일 주소**, **이름** 및 **성**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-228">Type the **Email Address**, **First Name**, and **Last Name** of a valid AAD account you want to provision into the related textboxes.</span></span>
   
   <span data-ttu-id="25bae-229">b.</span><span class="sxs-lookup"><span data-stu-id="25bae-229">b.</span></span> <span data-ttu-id="25bae-230">**사용자 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-230">Click **Create User**.</span></span>

>[!NOTE]
><span data-ttu-id="25bae-231">Azure Active Directory 계정 보유자는 활성화되기 전에 계정을 확인하기 위한 링크를 포함한 이메일을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-231">The Azure Active Directory account holder receives an email that includes a link to confirm the account before it becomes active.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="25bae-232">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="25bae-232">Assigning the Azure AD test user</span></span>

<span data-ttu-id="25bae-233">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Adobe Sign에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-233">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Adobe Sign.</span></span>

![사용자 할당][200] 

<span data-ttu-id="25bae-235">**Britta Simon을 Adobe Sign에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="25bae-235">**To assign Britta Simon to Adobe Sign, perform the following steps:**</span></span>

1. <span data-ttu-id="25bae-236">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-236">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="25bae-238">응용 프로그램 목록에서 **Adobe Sign**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-238">In the applications list, select **Adobe Sign**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_app.png) 

3. <span data-ttu-id="25bae-240">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-240">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="25bae-242">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-242">Click **Add** button.</span></span> <span data-ttu-id="25bae-243">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="25bae-245">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-245">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="25bae-246">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="25bae-247">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="25bae-248">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="25bae-248">Testing single sign-on</span></span>

<span data-ttu-id="25bae-249">액세스 패널에서 Adobe Sign 타일을 클릭하면 Adobe Sign 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="25bae-249">When you click the Adobe Sign tile in the Access Panel, you should get automatically signed-on to your Adobe Sign application.</span></span>
<span data-ttu-id="25bae-250">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="25bae-250">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="25bae-251">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="25bae-251">Additional resources</span></span>

* [<span data-ttu-id="25bae-252">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="25bae-252">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="25bae-253">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="25bae-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_203.png

