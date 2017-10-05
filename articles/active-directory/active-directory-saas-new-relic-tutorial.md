---
title: "자습서: New Relic과 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 New Relic 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3186b9a8-f4d8-45e2-ad82-6275f95e7aa6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: jeedes
ms.openlocfilehash: 605e85c23a849f70fcc0237361d7a891f716ca3a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-new-relic"></a><span data-ttu-id="d47ab-103">자습서: New Relic과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="d47ab-103">Tutorial: Azure Active Directory integration with New Relic</span></span>

<span data-ttu-id="d47ab-104">이 자습서에서는 Azure AD(Azure Active Directory)와 New Relic을 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-104">In this tutorial, you learn how to integrate New Relic with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d47ab-105">New Relic을 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-105">Integrating New Relic with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d47ab-106">New Relic에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-106">You can control in Azure AD who has access to New Relic</span></span>
- <span data-ttu-id="d47ab-107">사용자가 해당 Azure AD 계정으로 New Relic에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-107">You can enable your users to automatically get signed-on to New Relic (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d47ab-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d47ab-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d47ab-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d47ab-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d47ab-110">Prerequisites</span></span>

<span data-ttu-id="d47ab-111">New Relic과 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-111">To configure Azure AD integration with New Relic, you need the following items:</span></span>

- <span data-ttu-id="d47ab-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="d47ab-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d47ab-113">New Relic Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="d47ab-113">A New Relic single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d47ab-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d47ab-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d47ab-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="d47ab-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d47ab-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d47ab-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="d47ab-118">Scenario description</span></span>
<span data-ttu-id="d47ab-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d47ab-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d47ab-121">갤러리에서 New Relic 추가</span><span class="sxs-lookup"><span data-stu-id="d47ab-121">Adding New Relic from the gallery</span></span>
2. <span data-ttu-id="d47ab-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="d47ab-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-new-relic-from-the-gallery"></a><span data-ttu-id="d47ab-123">갤러리에서 New Relic 추가</span><span class="sxs-lookup"><span data-stu-id="d47ab-123">Adding New Relic from the gallery</span></span>
<span data-ttu-id="d47ab-124">New Relic의 Azure AD 통합을 구성하려면 갤러리의 New Relic을 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-124">To configure the integration of New Relic into Azure AD, you need to add New Relic from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d47ab-125">**갤러리에서 New Relic을 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="d47ab-125">**To add New Relic from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d47ab-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d47ab-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d47ab-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="d47ab-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="d47ab-133">검색 상자에서 **New Relic**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-133">In the search box, type **New Relic**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_search.png)

5. <span data-ttu-id="d47ab-135">결과 패널에서 **New Relic**을 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-135">In the results panel, select **New Relic**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d47ab-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="d47ab-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d47ab-138">이 섹션에서는 “Britta Simon”이라는 테스트 사용자를 기반으로 New Relic에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-138">In this section, you configure and test Azure AD single sign-on with New Relic based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d47ab-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 New Relic 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-139">For single sign-on to work, Azure AD needs to know what the counterpart user in New Relic is to a user in Azure AD.</span></span> <span data-ttu-id="d47ab-140">즉, Azure AD 사용자와 New Relic의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-140">In other words, a link relationship between an Azure AD user and the related user in New Relic needs to be established.</span></span>

<span data-ttu-id="d47ab-141">New Relic에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-141">In New Relic, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d47ab-142">New Relic에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-142">To configure and test Azure AD single sign-on with New Relic, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d47ab-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d47ab-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d47ab-145">**[New Relic 테스트 사용자 만들기](#creating-a-new-relic-test-user)** - Britta Simon의 Azure AD 표현과 연결되는 대응 사용자를 New Relic에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-145">**[Creating a New Relic test user](#creating-a-new-relic-test-user)** - to have a counterpart of Britta Simon in New Relic that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d47ab-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d47ab-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d47ab-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="d47ab-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d47ab-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 New Relic 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your New Relic application.</span></span>

<span data-ttu-id="d47ab-150">**New Relic에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="d47ab-150">**To configure Azure AD single sign-on with New Relic, perform the following steps:**</span></span>

1. <span data-ttu-id="d47ab-151">Azure Portal의 **New Relic** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-151">In the Azure portal, on the **New Relic** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="d47ab-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_samlbase.png)

3. <span data-ttu-id="d47ab-155">**New Relic 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-155">On the **New Relic Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_url.png)

    <span data-ttu-id="d47ab-157">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<subdomain>.newrelic.com`</span><span class="sxs-lookup"><span data-stu-id="d47ab-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.newrelic.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d47ab-158">이 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-158">The value is not real.</span></span> <span data-ttu-id="d47ab-159">이 값을 실제 로그온 URL로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="d47ab-160">값을 얻으려면 [New Relic 클라이언트 지원 팀](https://support.newrelic.com/)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="d47ab-160">Contact [New Relic Client support team](https://support.newrelic.com/) to get the value.</span></span> 
 
4. <span data-ttu-id="d47ab-161">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_certificate.png) 

5. <span data-ttu-id="d47ab-163">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-163">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-new-relic-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d47ab-165">**New Relic 구성** 섹션에서 **New Relic 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-165">On the **New Relic Configuration** section, click **Configure New Relic** to open **Configure sign-on** window.</span></span> <span data-ttu-id="d47ab-166">**빠른 참조 섹션**에서 **로그아웃 URL 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-166">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_configure.png) 

7. <span data-ttu-id="d47ab-168">다른 웹 브라우저 창에서 **New Relic** 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-168">In a different web browser window, sign on to your **New Relic** company site as administrator.</span></span>

8. <span data-ttu-id="d47ab-169">위쪽의 메뉴에서 **계정 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-169">In the menu on the top, click **Account Settings**.</span></span>
   
    <span data-ttu-id="d47ab-170">![계정 설정](./media/active-directory-saas-new-relic-tutorial/ic797036.png "계정 설정")</span><span class="sxs-lookup"><span data-stu-id="d47ab-170">![Account Settings](./media/active-directory-saas-new-relic-tutorial/ic797036.png "Account Settings")</span></span>

9. <span data-ttu-id="d47ab-171">**보안 및 인증** 탭을 클릭한 후 **Single sign on** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-171">Click the **Security and authentication** tab, and then click the **Single sign on** tab.</span></span>
   
    <span data-ttu-id="d47ab-172">![Single Sign-On](./media/active-directory-saas-new-relic-tutorial/ic797037.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="d47ab-172">![Single Sign-On](./media/active-directory-saas-new-relic-tutorial/ic797037.png "Single Sign-On")</span></span>

10. <span data-ttu-id="d47ab-173">SAML 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-173">On the SAML dialog page, perform the following steps:</span></span>
   
    <span data-ttu-id="d47ab-174">![SAML](./media/active-directory-saas-new-relic-tutorial/ic797038.png "SAML")</span><span class="sxs-lookup"><span data-stu-id="d47ab-174">![SAML](./media/active-directory-saas-new-relic-tutorial/ic797038.png "SAML")</span></span>
   
   <span data-ttu-id="d47ab-175">a.</span><span class="sxs-lookup"><span data-stu-id="d47ab-175">a.</span></span> <span data-ttu-id="d47ab-176">**파일 선택** 을 클릭하여 다운로드한 Azure Active Directory 인증서를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-176">Click **Choose File** to upload your downloaded Azure Active Directory certificate.</span></span>

   <span data-ttu-id="d47ab-177">b.</span><span class="sxs-lookup"><span data-stu-id="d47ab-177">b.</span></span> <span data-ttu-id="d47ab-178">Azure Portal에서 복사한 **SAML Single Sign-On 서비스 URL** 값을 **원격 로그인 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-178">In the **Remote login URL** textbox,  paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="d47ab-179">c.</span><span class="sxs-lookup"><span data-stu-id="d47ab-179">c.</span></span> <span data-ttu-id="d47ab-180">Azure Portal에서 복사한 **로그아웃 URL** 값을 **Logout landing URL**(로그아웃 방문 URL) 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-180">In the **Logout landing URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

   <span data-ttu-id="d47ab-181">d.</span><span class="sxs-lookup"><span data-stu-id="d47ab-181">d.</span></span> <span data-ttu-id="d47ab-182">**내 변경 내용 저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-182">Click **Save my changes**.</span></span>

> [!TIP]
> <span data-ttu-id="d47ab-183">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-183">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d47ab-184">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-184">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d47ab-185">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-185">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d47ab-186">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="d47ab-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="d47ab-187">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="d47ab-189">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="d47ab-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d47ab-190">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-190">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-new-relic-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d47ab-192">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-192">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-new-relic-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d47ab-194">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-194">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-new-relic-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d47ab-196">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-196">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-new-relic-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d47ab-198">a.</span><span class="sxs-lookup"><span data-stu-id="d47ab-198">a.</span></span> <span data-ttu-id="d47ab-199">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-199">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d47ab-200">b.</span><span class="sxs-lookup"><span data-stu-id="d47ab-200">b.</span></span> <span data-ttu-id="d47ab-201">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d47ab-202">c.</span><span class="sxs-lookup"><span data-stu-id="d47ab-202">c.</span></span> <span data-ttu-id="d47ab-203">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-203">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d47ab-204">d.</span><span class="sxs-lookup"><span data-stu-id="d47ab-204">d.</span></span> <span data-ttu-id="d47ab-205">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-205">Click **Create**.</span></span>
 
### <a name="creating-a-new-relic-test-user"></a><span data-ttu-id="d47ab-206">New Relic 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="d47ab-206">Creating a New Relic test user</span></span>

<span data-ttu-id="d47ab-207">Azure Active Directory 사용자가 New Relic에 로그인할 수 있도록 하려면 New Relic으로 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-207">In order to enable Azure Active Directory users to log in to New Relic, they must be provisioned into New Relic.</span></span> <span data-ttu-id="d47ab-208">New Relic의 경우 프로비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-208">In the case of New Relic, provisioning is a manual task.</span></span>

<span data-ttu-id="d47ab-209">**사용자 계정을 New Relic에 프로비전하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="d47ab-209">**To provision a user account to New Relic, perform the following steps:**</span></span>

1. <span data-ttu-id="d47ab-210">**New Relic** 회사 사이트에 관리자 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-210">Log in to your **New Relic** company site as administrator.</span></span>

2. <span data-ttu-id="d47ab-211">위쪽의 메뉴에서 **계정 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-211">In the menu on the top, click **Account Settings**.</span></span>
   
    <span data-ttu-id="d47ab-212">![계정 설정](./media/active-directory-saas-new-relic-tutorial/ic797040.png "계정 설정")</span><span class="sxs-lookup"><span data-stu-id="d47ab-212">![Account Settings](./media/active-directory-saas-new-relic-tutorial/ic797040.png "Account Settings")</span></span>

3. <span data-ttu-id="d47ab-213">왼쪽의 **계정** 창에서 **요약**을 클릭한 다음 **사용자 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-213">In the **Account** pane on the left side, click **Summary**, and then click **Add user**.</span></span>
   
    <span data-ttu-id="d47ab-214">![계정 설정](./media/active-directory-saas-new-relic-tutorial/ic797041.png "계정 설정")</span><span class="sxs-lookup"><span data-stu-id="d47ab-214">![Account Settings](./media/active-directory-saas-new-relic-tutorial/ic797041.png "Account Settings")</span></span>

4. <span data-ttu-id="d47ab-215">**활성 사용자** 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-215">On the **Active users** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="d47ab-216">![활성 사용자](./media/active-directory-saas-new-relic-tutorial/ic797042.png "활성 사용자")</span><span class="sxs-lookup"><span data-stu-id="d47ab-216">![Active Users](./media/active-directory-saas-new-relic-tutorial/ic797042.png "Active Users")</span></span>
   
    <span data-ttu-id="d47ab-217">a.</span><span class="sxs-lookup"><span data-stu-id="d47ab-217">a.</span></span> <span data-ttu-id="d47ab-218">**이메일** 텍스트 상자에 프로비전하려는 유효한 Azure Active Directory 사용자의 이메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-218">In the **Email** textbox, type the email address of a valid Azure Active Directory user you want to provision.</span></span>

    <span data-ttu-id="d47ab-219">b.</span><span class="sxs-lookup"><span data-stu-id="d47ab-219">b.</span></span> <span data-ttu-id="d47ab-220">**역할**로 **사용자**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-220">As **Role** select **User**.</span></span>

    <span data-ttu-id="d47ab-221">c.</span><span class="sxs-lookup"><span data-stu-id="d47ab-221">c.</span></span> <span data-ttu-id="d47ab-222">**이 사용자 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-222">Click **Add this user**.</span></span>

>[!NOTE]
><span data-ttu-id="d47ab-223">다른 New Relic 사용자 계정 생성 도구 또는 New Relic이 제공한 API를 사용하여 AAD 사용자 계정을 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-223">You can use any other New Relic user account creation tools or APIs provided by New Relic to provision AAD user accounts.</span></span>
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d47ab-224">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="d47ab-224">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d47ab-225">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 New Relic에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-225">In this section, you enable Britta Simon to use Azure single sign-on by granting access to New Relic.</span></span>

![사용자 할당][200] 

<span data-ttu-id="d47ab-227">**Britta Simon을 New Relic에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="d47ab-227">**To assign Britta Simon to New Relic, perform the following steps:**</span></span>

1. <span data-ttu-id="d47ab-228">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-228">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="d47ab-230">응용 프로그램 목록에서 **New Relic**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-230">In the applications list, select **New Relic**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_app.png) 

3. <span data-ttu-id="d47ab-232">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-232">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="d47ab-234">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-234">Click **Add** button.</span></span> <span data-ttu-id="d47ab-235">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="d47ab-237">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-237">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d47ab-238">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d47ab-239">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d47ab-240">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="d47ab-240">Testing single sign-on</span></span>

<span data-ttu-id="d47ab-241">이 섹션은 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-241">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d47ab-242">액세스 패널에서 New Relic 타일을 클릭하면 New Relic 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="d47ab-242">When you click the New Relic tile in the Access Panel, you should get automatically signed-on to your New Relic application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d47ab-243">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="d47ab-243">Additional resources</span></span>

* [<span data-ttu-id="d47ab-244">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="d47ab-244">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d47ab-245">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="d47ab-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_203.png

