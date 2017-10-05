---
title: "자습서: Workplace by Facebook과 Azure Active Directory 통합 | Microsoft 문서"
description: "Azure Active Directory와 Workplace by Facebook 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 30f2ee64-95d3-44ef-b832-8a0a27e2967c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: jeedes
ms.openlocfilehash: 27e62a00832484667117d8718db9f2fc05e2f4e2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workplace-by-facebook"></a><span data-ttu-id="c88ee-103">자습서: Workplace by Facebook과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="c88ee-103">Tutorial: Azure Active Directory integration with Workplace by Facebook</span></span>

<span data-ttu-id="c88ee-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Workplace by Facebook을 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-104">In this tutorial, you learn how to integrate Workplace by Facebook with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c88ee-105">Workplace by Facebook과 Azure AD를 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-105">Integrating Workplace by Facebook with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c88ee-106">Azure AD에서는 Workplace by Facebook에 대한 액세스 권한이 있는 사용자를 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-106">You can control in Azure AD who has access to Workplace by Facebook.</span></span>
- <span data-ttu-id="c88ee-107">사용자가 Azure AD 계정으로 Workplace by Facebook에 자동으로 로그인(Single Sign-On)할 수 있도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-107">You can enable your users to automatically get signed on to Workplace by Facebook (single sign-on) with their Azure AD accounts.</span></span>
- <span data-ttu-id="c88ee-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-108">You can manage your accounts in one central location: the Azure portal.</span></span>

<span data-ttu-id="c88ee-109">Azure AD와의 SaaS(Software as a Service) 앱 통합에 대한 자세한 내용은 [Azure Active Directory를 사용한 응용 프로그램 액세스 및 Single Sign-On](active-directory-appssoaccess-whatis.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c88ee-109">For more details about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c88ee-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="c88ee-110">Prerequisites</span></span>

<span data-ttu-id="c88ee-111">Workplace by Facebook과 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-111">To configure Azure AD integration with Workplace by Facebook, you need the following items:</span></span>

- <span data-ttu-id="c88ee-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="c88ee-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c88ee-113">Workplace by Facebook SSO(Single Sign-On)가 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="c88ee-113">A Workplace by Facebook single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="c88ee-114">이 자습서의 단계를 테스트하려면 다음 권장 사항을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-114">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="c88ee-115">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="c88ee-115">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c88ee-116">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-116">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c88ee-117">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="c88ee-117">Scenario description</span></span>
<span data-ttu-id="c88ee-118">이 자습서에서는 테스트 환경에서 Azure AD SSO를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-118">In this tutorial, you test Azure AD SSO in a test environment.</span></span> <span data-ttu-id="c88ee-119">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-119">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c88ee-120">갤러리에서 Workplace by Facebook을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-120">Add Workplace by Facebook from the gallery.</span></span>
2. <span data-ttu-id="c88ee-121">Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-121">Configure and test Azure AD single sign-on.</span></span>

## <a name="add-workplace-by-facebook-from-the-gallery"></a><span data-ttu-id="c88ee-122">갤러리에서 Workplace by Facebook 추가</span><span class="sxs-lookup"><span data-stu-id="c88ee-122">Add Workplace by Facebook from the gallery</span></span>
<span data-ttu-id="c88ee-123">Azure AD에 Workplace by Facebook을 통합하도록 구성하려면 갤러리의 Workplace by Facebook을 관리되는 SaaS 앱 목록에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-123">To configure the integration of Workplace by Facebook into Azure AD, add Workplace by Facebook from the gallery to your list of managed SaaS apps.</span></span>

1. <span data-ttu-id="c88ee-124">[Azure Portal](https://portal.azure.com)의 왼쪽 창에서 **Azure Active Directory**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-124">In the [Azure portal](https://portal.azure.com), in the left pane, select **Azure Active Directory**.</span></span> 

    ![Azure Active Directory 단추][1]

2. <span data-ttu-id="c88ee-126">**엔터프라이즈 응용 프로그램** > **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-126">Browse to **Enterprise applications** > **All applications**.</span></span>

    ![엔터프라이즈 응용 프로그램 블레이드][2]
    
3. <span data-ttu-id="c88ee-128">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-128">To add the new application, select **New application** on the top of the dialog box.</span></span>

    ![새 응용 프로그램 단추][3]

4. <span data-ttu-id="c88ee-130">검색 상자에 **Workplace by Facebook**을 선택하고 결과에서 **Workplace by Facebook**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-130">In the search box, type **Workplace by Facebook**, and select **Workplace by Facebook** from results.</span></span> <span data-ttu-id="c88ee-131">그런 후 **추가**를 선택하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-131">Then select **Add**, to add the application.</span></span>

    ![결과 목록의 Workplace by Facebook](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_search.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="c88ee-133">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="c88ee-133">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="c88ee-134">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Workplace by Facebook에서 Azure AD SSO를 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-134">In this section, you configure and test Azure AD SSO with Workplace by Facebook, based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c88ee-135">SSO가 작동하려면 Azure AD의 사용자에 해당하는 Workplace by Facebook의 사용자가 누구인지 Azure AD에서 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-135">For SSO to work, Azure AD needs to know what the counterpart user in Workplace by Facebook is to a user in Azure AD.</span></span> <span data-ttu-id="c88ee-136">즉, Azure AD 사용자와 Workplace by Facebook의 관련 사용자 간에 링크 관계가 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-136">In other words, a linked relationship between an Azure AD user and the related user in Workplace by Facebook should be established.</span></span>

<span data-ttu-id="c88ee-137">Azure AD의 **사용자 이름** 값을 Workplace by Facebook의 **Username** 값으로 할당하여 이 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-137">Establish this relationship by assigning the value of the **user name** in Azure AD as the value of the **Username** in Workplace by Facebook.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="c88ee-138">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="c88ee-138">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="c88ee-139">이 섹션에서는 Azure Portal에서 Azure AD SSO를 사용하도록 설정하고 Workplace by Facebook 응용 프로그램에서 SSO를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-139">In this section, you enable Azure AD SSO in the Azure portal, and you configure SSO in your Workplace by Facebook application.</span></span>

1. <span data-ttu-id="c88ee-140">Azure Portal의 **Workplace by Facebook** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-140">In the Azure portal, on the **Workplace by Facebook** application integration page, select **Single sign-on**.</span></span>

    ![Single Sign-On 구성 링크][4]

2. <span data-ttu-id="c88ee-142">SSO를 사용하도록 설정하려면 **Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-142">In the **Single sign-on** dialog box, select **Mode** as **SAML-based Sign-on** to enable SSO.</span></span>
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_samlbase.png)

3. <span data-ttu-id="c88ee-144">**Workplace by Facebook 도메인 및 URL** 섹션에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-144">In the **Workplace by Facebook Domain and URLs** section, do the following:</span></span>

    <span data-ttu-id="c88ee-145">a.</span><span class="sxs-lookup"><span data-stu-id="c88ee-145">a.</span></span> <span data-ttu-id="c88ee-146">**로그온 URL** 텍스트 상자에서 다음과 같은 패턴을 사용하여 URL을 입력합니다. `https://<company subdomain>.facebook.com`</span><span class="sxs-lookup"><span data-stu-id="c88ee-146">In the **Sign-on URL** text box, type a URL that uses the following pattern: `https://<company subdomain>.facebook.com`</span></span>

    <span data-ttu-id="c88ee-147">b.</span><span class="sxs-lookup"><span data-stu-id="c88ee-147">b.</span></span> <span data-ttu-id="c88ee-148">**식별자** 텍스트 상자에서 다음과 같은 패턴을 사용하여 URL을 입력합니다. `https://www.facebook.com/company/<scim company id>`</span><span class="sxs-lookup"><span data-stu-id="c88ee-148">In the **Identifier** text box, type a URL that uses the following pattern: `https://www.facebook.com/company/<scim company id>`</span></span>

    > [!NOTE]
    > <span data-ttu-id="c88ee-149">이러한 값은 예제일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-149">These values are an example only.</span></span> <span data-ttu-id="c88ee-150">실제 로그온 URL 및 식별자로 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-150">Update these values with the actual sign-on URL and identifier.</span></span> <span data-ttu-id="c88ee-151">이러한 값을 구하려면 [Workplace by Facebook 클라이언트 지원 팀](https://workplace.fb.com/faq/)에 문의합니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-151">Contact the [Workplace by Facebook Client support team](https://workplace.fb.com/faq/) to get these values.</span></span> 

4. <span data-ttu-id="c88ee-152">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 선택한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-152">In the **SAML Signing Certificate** section, select **Certificate (Base64)**, and then save the certificate file on your computer.</span></span>

    ![인증서 다운로드 링크](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_certificate.png) 

5. <span data-ttu-id="c88ee-154">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-154">Select **Save**.</span></span>

    ![Single Sign-On 구성 저장 단추](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c88ee-156">**Workplace by Facebook 구성** 섹션에서 **Workplace by Facebook 구성**을 선택하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-156">In the **Workplace by Facebook Configuration** section, select **Configure Workplace by Facebook** to open the **Configure sign-on** window.</span></span> <span data-ttu-id="c88ee-157">**빠른 참조** 섹션에서 **로그아웃 URL, SAML 엔터티 ID 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-157">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference** section.</span></span>

    ![Workplace by Facebook 구성](./media/active-directory-saas-facebook-at-work-tutorial/config.png) 

7. <span data-ttu-id="c88ee-159">다른 웹 브라우저 창에서 Workplace by Facebook 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-159">In a different web browser window, sign in to your Workplace by Facebook company site as an administrator.</span></span>
  
   > [!NOTE] 
   > <span data-ttu-id="c88ee-160">SAML 인증 프로세스의 일환으로 Workplace는 Azure AD에 매개 변수를 전달하기 위해 최대 2.5KB 크기의 쿼리 문자열을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-160">As part of the SAML authentication process, Workplace can use query strings of up to 2.5 kilobytes in size in order to pass parameters to Azure AD.</span></span>

8. <span data-ttu-id="c88ee-161">**회사 대시보드**에서 **인증** 탭으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-161">In the **Company Dashboard**, go to the **Authentication** tab.</span></span>

9. <span data-ttu-id="c88ee-162">**SAML 인증** 아래 드롭다운 목록에서 **SSO 전용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-162">Under **SAML Authentication**, select **SSO Only** from the drop-down list.</span></span>

10. <span data-ttu-id="c88ee-163">Azure Portal의 **Workplace by Facebook 구성** 섹션에서 복사한 값을 해당 필드에 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-163">Enter the values copied from the **Workplace by Facebook Configuration** section of the Azure portal into the corresponding fields:</span></span>

    *   <span data-ttu-id="c88ee-164">**SAML URL** 텍스트 상자에 Azure Portal에서 복사한 **Single Sign-On 서비스 URL** 값을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-164">In the **SAML URL** text box, paste the value of **Single Sign-On Service URL**, which you have copied from the Azure portal.</span></span>
    *   <span data-ttu-id="c88ee-165">**SAML 발급자 URL 텍스트 상자**에 Azure Portal에서 복사한 **SAML 엔터티 ID** 값을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-165">In the **SAML Issuer URL** text box, paste the value of **SAML Entity ID**, which you have copied from the Azure portal.</span></span>
    *   <span data-ttu-id="c88ee-166">**SAML 로그아웃 리디렉션**(선택 사항)에 Azure Portal에서 복사한 **로그아웃 URL**을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-166">In **SAML Logout Redirect (optional)**, paste the value of **Sign-Out URL**, which you have copied from the Azure portal.</span></span>
    *   <span data-ttu-id="c88ee-167">Azure Portal에서 다운로드한 **base-64로 인코딩된 인증서**를 메모장에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-167">Open your **base-64 encoded certificate** in Notepad, downloaded from the Azure portal.</span></span> <span data-ttu-id="c88ee-168">내용을 클립보드로 복사한 후 **SAML 인증서** 입력란에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-168">Copy the content of it into your clipboard, and then paste it to the **SAML Certificate** text box.</span></span>

11. <span data-ttu-id="c88ee-169">**SAML 구성** 섹션에 나열된 대상 그룹 URL, 받는 사람 URL 및 ACS(Assertion Consumer Service) URL을 입력해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-169">You might need to enter the audience URL, recipient URL, and ACS (Assertion Consumer Service) URL, listed under the **SAML Configuration** section.</span></span>

12. <span data-ttu-id="c88ee-170">섹션 맨 아래로 스크롤하여 **SSO 테스트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-170">Scroll to the bottom of the section, and select **Test SSO**.</span></span> <span data-ttu-id="c88ee-171">Azure AD 로그인 페이지와 팝업 창이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-171">A pop-up window appears, with the Azure AD sign-in page.</span></span> <span data-ttu-id="c88ee-172">인증을 받으려면 평소처럼 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-172">To authenticate, enter your credentials as normal.</span></span> <span data-ttu-id="c88ee-173">Azure AD에서 반환되는 전자 메일 주소가 로그인한 Workplace 계정과 동일한지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-173">Ensure the email address returned back from Azure AD is the same as the Workplace account you are logged in with.</span></span>

13. <span data-ttu-id="c88ee-174">테스트를 성공적으로 마치면 페이지의 아래쪽으로 스크롤하여 **저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-174">If the test has finished successfully, scroll to the bottom of the page and select **Save**.</span></span>

14. <span data-ttu-id="c88ee-175">Workplace를 사용하는 모든 사용자에게 이제 인증을 위한 Azure AD 로그인 페이지가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-175">Anyone using Workplace is now presented with Azure AD sign-in page for authentication.</span></span>

<span data-ttu-id="c88ee-176">Azure AD 로그아웃 페이지를 가리키는 데 사용할 수 있는 SAML 로그아웃 URL을 구성하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-176">You can choose to configure a SAML sign out URL, which can be used to point at the Azure AD sign-out page.</span></span> <span data-ttu-id="c88ee-177">이 설정을 사용하도록 설정하고 구성하면 더 이상 사용자가 Workplace 로그아웃 페이지로 이동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-177">When this setting is enabled and configured, the user is no longer directed to the Workplace sign-out page.</span></span> <span data-ttu-id="c88ee-178">대신 SAML 로그아웃 리디렉션 설정에 추가된 URL로 사용자가 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-178">Instead, the user is redirected to the URL that was added in the SAML sign-out redirect setting.</span></span>


> [!TIP]
> <span data-ttu-id="c88ee-179">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-179">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app.</span></span> <span data-ttu-id="c88ee-180">**Active Directory** > **엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 선택하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-180">After adding this app from the **Active Directory** > **Enterprise Applications** section, simply select the **Single Sign-On** tab, and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c88ee-181">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-181">You can read more about the embedded documentation feature in the [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>

### <a name="configure-reauthentication-frequency"></a><span data-ttu-id="c88ee-182">재인증 빈도 구성</span><span class="sxs-lookup"><span data-stu-id="c88ee-182">Configure reauthentication frequency</span></span>

<span data-ttu-id="c88ee-183">매일, 3일, 1주, 2주, 매달을 주기로 SAML 확인을 요청하거나 SAML 확인을 요청하지 않도록 Workplace를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-183">You can configure Workplace to prompt for a SAML check every day, three days, one week, two weeks, one month, or never.</span></span>

> [!NOTE] 
><span data-ttu-id="c88ee-184">모바일 응용 프로그램에서 SAML 확인에 대한 최소값은 일주일로 설정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-184">The minimum value for the SAML check on mobile applications is set to one week.</span></span>

<span data-ttu-id="c88ee-185">모든 사용자에 대해 강제로 SAML 재설정을 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-185">You can also force a SAML reset for all users.</span></span> <span data-ttu-id="c88ee-186">이를 위해서는 **현재 모든 사용자에 대해 SAML 인증 필요** 단추를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-186">To do this, use the **Require SAML authentication for all users now** button.</span></span>


### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="c88ee-187">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="c88ee-187">Create an Azure AD test user</span></span>
<span data-ttu-id="c88ee-188">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

1. <span data-ttu-id="c88ee-190">**Azure Portal**의 왼쪽 창에서 **Azure Active Directory**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-190">In the **Azure portal**, in the left pane, select **Azure Active Directory**.</span></span>

    ![Azure Active Directory 단추](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c88ee-192">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-192">To display the list of users, go to **Users and groups**, and select **All users**.</span></span>
    
    !["사용자 및 그룹" 및 "모든 사용자" 링크](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c88ee-194">**사용자** 대화 상자를 열려면 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-194">To open the **User** dialog box, select **Add**.</span></span>
 
    ![추가 단추](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c88ee-196">**사용자** 대화 상자에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-196">In the **User** dialog box, do the following:</span></span>
 
    ![사용자 대화 상자](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c88ee-198">a.</span><span class="sxs-lookup"><span data-stu-id="c88ee-198">a.</span></span> <span data-ttu-id="c88ee-199">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-199">In the **Name** text box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c88ee-200">b.</span><span class="sxs-lookup"><span data-stu-id="c88ee-200">b.</span></span> <span data-ttu-id="c88ee-201">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-201">In the **User name** text box, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c88ee-202">c.</span><span class="sxs-lookup"><span data-stu-id="c88ee-202">c.</span></span> <span data-ttu-id="c88ee-203">**암호 표시**를 선택하고 암호를 적어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-203">Select **Show Password**, and write it down.</span></span>

    <span data-ttu-id="c88ee-204">d.</span><span class="sxs-lookup"><span data-stu-id="c88ee-204">d.</span></span> <span data-ttu-id="c88ee-205">**만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-205">Select **Create**.</span></span>
 
### <a name="create-a-workplace-by-facebook-test-user"></a><span data-ttu-id="c88ee-206">Workplace by Facebook 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="c88ee-206">Create a Workplace by Facebook test user</span></span>

<span data-ttu-id="c88ee-207">이 섹션에서는 Workplace by Facebook에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-207">In this section, a user called Britta Simon is created in Workplace by Facebook.</span></span> <span data-ttu-id="c88ee-208">Workplace by Facebook은 기본적으로 사용하도록 설정된 Just-In-Time 프로비전을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-208">Workplace by Facebook supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="c88ee-209">이 섹션에는 사용자의 작업이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-209">There is no action for you in this section.</span></span> <span data-ttu-id="c88ee-210">Workplace by Facebook에 사용자가 없는 경우 Workplace by Facebook에 액세스하려고 하면 새 사용자가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-210">If a user doesn't exist in Workplace by Facebook, a new one is created when you attempt to access Workplace by Facebook.</span></span>

>[!Note]
><span data-ttu-id="c88ee-211">사용자를 수동으로 만들어야 하는 경우 [Workplace by Facebook 클라이언트 지원 팀](https://workplace.fb.com/faq/)에 문의합니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-211">If you need to create a user manually, contact the [Workplace by Facebook Client support team](https://workplace.fb.com/faq/).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="c88ee-212">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="c88ee-212">Assign the Azure AD test user</span></span>

<span data-ttu-id="c88ee-213">이 섹션에서는 Britta Simon이 Azure SSO를 사용할 수 있도록 Workplace by Facebook에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-213">In this section, you enable Britta Simon to use Azure SSO by granting access to Workplace by Facebook.</span></span>

![사용자 할당][200] 

1. <span data-ttu-id="c88ee-215">Azure Portal에서 응용 프로그램 보기를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-215">In the Azure portal, open the applications view.</span></span> <span data-ttu-id="c88ee-216">디렉터리 보기로 가서 **엔터프라이즈 응용 프로그램**으로 이동한 다음 **모든 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-216">Go to the directory view, go to **Enterprise applications**, and then select **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="c88ee-218">응용 프로그램 목록에서 **Workplace by Facebook**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-218">In the applications list, select **Workplace by Facebook**.</span></span>

    ![응용 프로그램 목록의 Workplace by Facebook 링크](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_app.png) 

3. <span data-ttu-id="c88ee-220">왼쪽 메뉴에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-220">In the menu on the left, select **Users and groups**.</span></span>

    !["사용자 및 그룹" 링크][202] 

4. <span data-ttu-id="c88ee-222">**추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-222">Select **Add**.</span></span> <span data-ttu-id="c88ee-223">그런 후 **할당 추가** 창에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-223">Then, in the **Add Assignment** pane, select **Users and groups**.</span></span>

    ![할당 추가 창][203]

5. <span data-ttu-id="c88ee-225">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-225">In the **Users and groups** dialog box, select **Britta Simon** in the users list.</span></span>

6. <span data-ttu-id="c88ee-226">**사용자 및 그룹** 대화 상자에서 **선택**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-226">In the **Users and groups** dialog box, select **Select**.</span></span>

7. <span data-ttu-id="c88ee-227">**할당 추가** 대화 상자에서 **할당**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-227">In the **Add Assignment** dialog box, select **Assign**.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="c88ee-228">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="c88ee-228">Test single sign-on</span></span>

<span data-ttu-id="c88ee-229">SSO 설정을 테스트하려면 액세스 패널을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c88ee-229">If you want to test your SSO settings, open the Access Panel.</span></span>
<span data-ttu-id="c88ee-230">자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c88ee-230">For more information, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="c88ee-231">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c88ee-231">Next steps</span></span>

* <span data-ttu-id="c88ee-232">[Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록](active-directory-saas-tutorial-list.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c88ee-232">See the [list of tutorials on how to integrate SaaS Apps with Azure Active Directory](active-directory-saas-tutorial-list.md).</span></span>
* <span data-ttu-id="c88ee-233">[Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)를 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="c88ee-233">Read [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>
* <span data-ttu-id="c88ee-234">[사용자 프로비저닝 구성](active-directory-saas-facebook-at-work-provisioning-tutorial.md) 방법을 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="c88ee-234">Learn more about how to [configure user provisioning](active-directory-saas-facebook-at-work-provisioning-tutorial.md).</span></span>



<!--Image references-->

[1]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_203.png

