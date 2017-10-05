---
title: "자습서: PagerDuty와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory 및 PagerDuty 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0410456a-76f7-42a7-9bb5-f767de75a0e0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: bf5263ce4d8fbc231029c101f167f4b55a921e60
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pagerduty"></a><span data-ttu-id="16e94-103">자습서: PagerDuty와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="16e94-103">Tutorial: Azure Active Directory integration with PagerDuty</span></span>

<span data-ttu-id="16e94-104">이 자습서에서는 Azure AD(Azure Active Directory)와 PagerDuty를 통합하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-104">In this tutorial, you learn how to integrate PagerDuty with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="16e94-105">PagerDuty를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-105">Integrating PagerDuty with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="16e94-106">PagerDuty에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-106">You can control in Azure AD who has access to PagerDuty</span></span>
- <span data-ttu-id="16e94-107">사용자가 해당 Azure AD 계정으로 PagerDuty에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-107">You can enable your users to automatically get signed-on to PagerDuty (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="16e94-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="16e94-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="16e94-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="16e94-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="16e94-110">Prerequisites</span></span>

<span data-ttu-id="16e94-111">PagerDuty와 Azure AD의 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-111">To configure Azure AD integration with PagerDuty, you need the following items:</span></span>

- <span data-ttu-id="16e94-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="16e94-112">An Azure AD subscription</span></span>
- <span data-ttu-id="16e94-113">PagerDuty Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="16e94-113">A PagerDuty single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="16e94-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="16e94-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="16e94-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="16e94-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="16e94-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="16e94-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="16e94-118">Scenario description</span></span>
<span data-ttu-id="16e94-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="16e94-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="16e94-121">갤러리에서 PagerDuty 추가</span><span class="sxs-lookup"><span data-stu-id="16e94-121">Adding PagerDuty from the gallery</span></span>
2. <span data-ttu-id="16e94-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="16e94-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pagerduty-from-the-gallery"></a><span data-ttu-id="16e94-123">갤러리에서 PagerDuty 추가</span><span class="sxs-lookup"><span data-stu-id="16e94-123">Adding PagerDuty from the gallery</span></span>
<span data-ttu-id="16e94-124">PagerDuty가 Azure AD에 통합되도록 구성하려면 갤러리의 PagerDuty를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-124">To configure the integration of PagerDuty into Azure AD, you need to add PagerDuty from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="16e94-125">**갤러리에서 PagerDuty를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="16e94-125">**To add PagerDuty from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="16e94-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory 단추][1]

2. <span data-ttu-id="16e94-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="16e94-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-129">Then go to **All applications**.</span></span>

    ![엔터프라이즈 응용 프로그램 블레이드][2]
    
3. <span data-ttu-id="16e94-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![새 응용 프로그램 단추][3]

4. <span data-ttu-id="16e94-133">검색 상자에서 **PagerDuty**를 입력하고, 결과 패널에서 **PagerDuty**를 선택한 다음, **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-133">In the search box, type **PagerDuty**, select  **PagerDuty**  from result panel then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="16e94-135">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="16e94-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="16e94-136">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 하여 PagerDuty에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-136">In this section, you configure and test Azure AD single sign-on with PagerDuty based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="16e94-137">Single Sign-On이 작동하려면 Azure AD 사용자에 해당하는 PagerDuty 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-137">For single sign-on to work, Azure AD needs to know what the counterpart user in PagerDuty is to a user in Azure AD.</span></span> <span data-ttu-id="16e94-138">즉, Azure AD 사용자와 PagerDuty의 관련 사용자 간에 링크 관계가 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-138">In other words, a link relationship between an Azure AD user and the related user in PagerDuty needs to be established.</span></span>

<span data-ttu-id="16e94-139">PagerDuty에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-139">In PagerDuty, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="16e94-140">PagerDuty에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-140">To configure and test Azure AD single sign-on with PagerDuty, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="16e94-141">**[Azure AD Single Sign-On 구성](#configure-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="16e94-142">**[Azure AD 테스트 사용자 만들기](#create-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="16e94-143">**[PagerDuty 테스트 사용자 만들기](#create-a-pagerduty-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 PagerDuty에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-143">**[Create a PagerDuty test user](#create-a-pagerduty-test-user)** - to have a counterpart of Britta Simon in PagerDuty that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="16e94-144">**[Azure AD 테스트 사용자 할당](#assign-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="16e94-145">**[Single Sign-on 테스트](#test-single-sign-on)** - 구성이 작동하는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="16e94-146">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="16e94-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="16e94-147">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 PagerDuty 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your PagerDuty application.</span></span>

<span data-ttu-id="16e94-148">**PagerDuty에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="16e94-148">**To configure Azure AD single sign-on with PagerDuty, perform the following steps:**</span></span>

1. <span data-ttu-id="16e94-149">Azure Portal의 **PagerDuty** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-149">In the Azure portal, on the **PagerDuty** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-On 구성 링크][4]

2. <span data-ttu-id="16e94-151">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_samlbase.png)

3. <span data-ttu-id="16e94-153">**PagerDuty 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-153">On the **PagerDuty Domain and URLs** section, perform the following steps:</span></span>

    ![PagerDuty 도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_url.png)

    <span data-ttu-id="16e94-155">a.</span><span class="sxs-lookup"><span data-stu-id="16e94-155">a.</span></span> <span data-ttu-id="16e94-156">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<tenant-name>.pagerduty.com`</span><span class="sxs-lookup"><span data-stu-id="16e94-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.pagerduty.com`</span></span>

    <span data-ttu-id="16e94-157">b.</span><span class="sxs-lookup"><span data-stu-id="16e94-157">b.</span></span> <span data-ttu-id="16e94-158">**식별자** 텍스트 상자에서 `https://<tenant-name>.pagerduty.com` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenant-name>.pagerduty.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="16e94-159">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-159">These values are not real.</span></span> <span data-ttu-id="16e94-160">실제 로그온 URL 및 식별자로 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="16e94-161">이러한 값을 얻으려면 [PagerDuty 클라이언트 지원 팀](https://www.pagerduty.com/support/)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="16e94-161">Contact [PagerDuty Client support team](https://www.pagerduty.com/support/) to get these values.</span></span> 

4. <span data-ttu-id="16e94-162">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-162">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![인증서 다운로드 링크](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_certificate.png) 

5. <span data-ttu-id="16e94-164">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-164">Click **Save** button.</span></span>

    ![Single Sign-On 구성 저장 단추](./media/active-directory-saas-pagerduty-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="16e94-166">**PagerDuty 구성** 섹션에서 **PagerDuty 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-166">On the **PagerDuty Configuration** section, click **Configure PagerDuty** to open **Configure sign-on** window.</span></span> <span data-ttu-id="16e94-167">**빠른 참조 섹션**에서 **로그아웃 URL 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-167">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![PagerDuty 구성](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_configure.png) 

7. <span data-ttu-id="16e94-169">다른 웹 브라우저 창에서 Pagerduty 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-169">In a different web browser window, log into your Pagerduty company site as an administrator.</span></span>

8. <span data-ttu-id="16e94-170">위쪽의 메뉴에서 **계정 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-170">In the menu on the top, click **Account Settings**.</span></span>
   
    <span data-ttu-id="16e94-171">![계정 설정](./media/active-directory-saas-pagerduty-tutorial/ic778535.png "계정 설정")</span><span class="sxs-lookup"><span data-stu-id="16e94-171">![Account Settings](./media/active-directory-saas-pagerduty-tutorial/ic778535.png "Account Settings")</span></span>

9. <span data-ttu-id="16e94-172">**Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-172">Click **Single Sign-on**.</span></span>
   
    <span data-ttu-id="16e94-173">![Single Sign-On](./media/active-directory-saas-pagerduty-tutorial/ic778536.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="16e94-173">![Single sign-on](./media/active-directory-saas-pagerduty-tutorial/ic778536.png "Single sign-on")</span></span>

10. <span data-ttu-id="16e94-174">**SSO(Single Sign-On) 사용** 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-174">On the **Enable Single Sign-on (SSO)** page, perform the following steps:</span></span>
   
    <span data-ttu-id="16e94-175">![Single Sign-On 사용](./media/active-directory-saas-pagerduty-tutorial/ic778537.png "Single Sign-On 사용")</span><span class="sxs-lookup"><span data-stu-id="16e94-175">![Enable single sign-on](./media/active-directory-saas-pagerduty-tutorial/ic778537.png "Enable single sign-on")</span></span>
   
    <span data-ttu-id="16e94-176">a.</span><span class="sxs-lookup"><span data-stu-id="16e94-176">a.</span></span> <span data-ttu-id="16e94-177">Azure Portal에서 다운로드한 Base 64로 인코딩된 인증서를 메모장에서 열고, 콘텐츠를 클립보드에 복사한 다음, **X.509 인증서** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-177">Open your base-64 encoded certificate downloaded from Azure portal in notepad, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox</span></span>
  
    <span data-ttu-id="16e94-178">b.</span><span class="sxs-lookup"><span data-stu-id="16e94-178">b.</span></span> <span data-ttu-id="16e94-179">**로그인 URL** 텍스트 상자에서 Azure Portal에서 복사한 **SAML Single Sign-On 서비스 URL**을 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-179">In the **Login URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="16e94-180">c.</span><span class="sxs-lookup"><span data-stu-id="16e94-180">c.</span></span> <span data-ttu-id="16e94-181">**로그아웃 URL** 텍스트 상자에서 Azure Portal에서 복사한 **로그아웃 URL**을 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-181">In the **Logout URL** textbox, paste **Sign-Out URL** which you have copied from Azure portal.</span></span>
 
    <span data-ttu-id="16e94-182">d.</span><span class="sxs-lookup"><span data-stu-id="16e94-182">d.</span></span> <span data-ttu-id="16e94-183">**Single Sign-On 켜기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-183">Select **Turn on Single Sign-on**.</span></span>
 
    <span data-ttu-id="16e94-184">e.</span><span class="sxs-lookup"><span data-stu-id="16e94-184">e.</span></span> <span data-ttu-id="16e94-185">**변경 내용 저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-185">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="16e94-186">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-186">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="16e94-187">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-187">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="16e94-188">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-188">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="16e94-189">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="16e94-189">Create an Azure AD test user</span></span>

<span data-ttu-id="16e94-190">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-190">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 테스트 사용자 만들기][100]

<span data-ttu-id="16e94-192">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="16e94-192">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="16e94-193">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-193">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure Active Directory 단추](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="16e94-195">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-195">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    !["사용자 및 그룹" 및 "모든 사용자" 링크](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="16e94-197">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-197">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![추가 단추](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="16e94-199">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-199">On the **User** dialog page, perform the following steps:</span></span>
 
    ![사용자 대화 상자](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="16e94-201">a.</span><span class="sxs-lookup"><span data-stu-id="16e94-201">a.</span></span> <span data-ttu-id="16e94-202">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-202">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="16e94-203">b.</span><span class="sxs-lookup"><span data-stu-id="16e94-203">b.</span></span> <span data-ttu-id="16e94-204">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-204">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="16e94-205">c.</span><span class="sxs-lookup"><span data-stu-id="16e94-205">c.</span></span> <span data-ttu-id="16e94-206">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-206">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="16e94-207">d.</span><span class="sxs-lookup"><span data-stu-id="16e94-207">d.</span></span> <span data-ttu-id="16e94-208">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-208">Click **Create**.</span></span>
 
### <a name="create-a-pagerduty-test-user"></a><span data-ttu-id="16e94-209">PagerDuty 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="16e94-209">Create a PagerDuty test user</span></span>

<span data-ttu-id="16e94-210">Azure AD 사용자가 PagerDuty에 로그인할 수 있도록 하려면 이 사용자를 PagerDuty로 프로비전해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-210">To enable Azure AD users to log in to PagerDuty, they must be provisioned into PagerDuty.</span></span>  
<span data-ttu-id="16e94-211">PagerDuty의 경우 프로비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-211">In the case of PagerDuty, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="16e94-212">다른 PagerDuty 사용자 계정 생성 도구 또는 PagerDuty에서 제공하는 API를 사용하여 Azure Active Directory 사용자 계정을 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-212">You can use any other Pagerduty user account creation tools or APIs provided by Pagerduty to provision Azure Active Directory user accounts.</span></span>

<span data-ttu-id="16e94-213">**사용자 계정을 프로비전하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="16e94-213">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="16e94-214">**Pagerduty** 테넌트에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-214">Log in to your **Pagerduty** tenant.</span></span>

2. <span data-ttu-id="16e94-215">위쪽의 메뉴에서 **사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-215">In the menu on the top, click **Users**.</span></span>

3. <span data-ttu-id="16e94-216">**사용자 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-216">Click **Add Users**.</span></span>
   
    <span data-ttu-id="16e94-217">![사용자 추가](./media/active-directory-saas-pagerduty-tutorial/ic778539.png "사용자 추가")</span><span class="sxs-lookup"><span data-stu-id="16e94-217">![Add Users](./media/active-directory-saas-pagerduty-tutorial/ic778539.png "Add Users")</span></span>

4.  <span data-ttu-id="16e94-218">**팀 초대** 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-218">On the **Invite your team** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="16e94-219">![팀 초대](./media/active-directory-saas-pagerduty-tutorial/ic778540.png "팀 초대")</span><span class="sxs-lookup"><span data-stu-id="16e94-219">![Invite your team](./media/active-directory-saas-pagerduty-tutorial/ic778540.png "Invite your team")</span></span>

    <span data-ttu-id="16e94-220">a.</span><span class="sxs-lookup"><span data-stu-id="16e94-220">a.</span></span> <span data-ttu-id="16e94-221">사용자의 **성과 이름**을 입력합니다(예: **Britta Simon**).</span><span class="sxs-lookup"><span data-stu-id="16e94-221">Type the **First and Last Name** of user like **Britta Simon**.</span></span> 
   
    <span data-ttu-id="16e94-222">b.</span><span class="sxs-lookup"><span data-stu-id="16e94-222">b.</span></span> <span data-ttu-id="16e94-223">사용자의 **이메일** 주소를 입력합니다(예: **brittasimon@contoso.com**).</span><span class="sxs-lookup"><span data-stu-id="16e94-223">Enter **Email** address of user like **brittasimon@contoso.com**.</span></span>
   
    <span data-ttu-id="16e94-224">c.</span><span class="sxs-lookup"><span data-stu-id="16e94-224">c.</span></span> <span data-ttu-id="16e94-225">**추가**를 클릭한 다음 **초대장 보내기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-225">Click **Add**, and then click **Send Invites**.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="16e94-226">추가된 모든 사용자는 PagerDuty 계정을 만들도록 초대를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-226">All added users will receive an invite to create a PagerDuty account.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="16e94-227">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="16e94-227">Assign the Azure AD test user</span></span>

<span data-ttu-id="16e94-228">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 PagerDuty에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-228">In this section, you enable Britta Simon to use Azure single sign-on by granting access to PagerDuty.</span></span>

![사용자 역할 할당][200]

<span data-ttu-id="16e94-230">**Britta Simon을 PagerDuty에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="16e94-230">**To assign Britta Simon to PagerDuty, perform the following steps:**</span></span>

1. <span data-ttu-id="16e94-231">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-231">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="16e94-233">응용 프로그램 목록에서 **PagerDuty**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-233">In the applications list, select **PagerDuty**.</span></span>

    ![응용 프로그램 목록의 PagerDuty 링크](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_app.png) 

3. <span data-ttu-id="16e94-235">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-235">In the menu on the left, click **Users and groups**.</span></span>

    !["사용자 및 그룹" 링크][202]

4. <span data-ttu-id="16e94-237">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-237">Click **Add** button.</span></span> <span data-ttu-id="16e94-238">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![할당 추가 창][203]

5. <span data-ttu-id="16e94-240">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-240">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="16e94-241">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="16e94-242">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="16e94-243">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="16e94-243">Test single sign-on</span></span>

<span data-ttu-id="16e94-244">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-244">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="16e94-245">액세스 패널에서 PagerDuty 타일을 클릭하면 PagerDuty 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="16e94-245">When you click the PagerDuty tile in the Access Panelyou should get automatically signed-on to your PagerDuty application.</span></span>

<span data-ttu-id="16e94-246">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="16e94-246">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="16e94-247">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="16e94-247">Additional resources</span></span>

* [<span data-ttu-id="16e94-248">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="16e94-248">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="16e94-249">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="16e94-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_203.png

