---
title: "자습서: FreshDesk와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory 및 FreshDesk 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2a3e5aa-7b5a-4fe4-9285-45dbe6e8efcc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: f4b47e345a40b64f69ad8a4618564662b4a6c879
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-freshdesk"></a><span data-ttu-id="1f15b-103">자습서: FreshDesk와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="1f15b-103">Tutorial: Azure Active Directory integration with FreshDesk</span></span>

<span data-ttu-id="1f15b-104">이 자습서에서는 Azure AD(Azure Active Directory)와 FreshDesk를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-104">In this tutorial, you learn how to integrate FreshDesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1f15b-105">FreshDesk를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-105">Integrating FreshDesk with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1f15b-106">FreshDesk에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-106">You can control in Azure AD who has access to FreshDesk</span></span>
- <span data-ttu-id="1f15b-107">사용자가 해당 Azure AD 계정으로 FreshDesk에 자동으로 SSO(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-107">You can enable your users to automatically get signed-on to FreshDesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1f15b-108">단일 중앙 위치인 Azure 관리 포털에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="1f15b-109">Azure AD와의 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory를 사용한 응용 프로그램 액세스 및 Single Sign-On](active-directory-appssoaccess-whatis.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1f15b-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1f15b-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="1f15b-110">Prerequisites</span></span>

<span data-ttu-id="1f15b-111">FreshDesk와 Azure AD를 통합하도록 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-111">To configure Azure AD integration with FreshDesk, you need the following items:</span></span>

- <span data-ttu-id="1f15b-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="1f15b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1f15b-113">FreshDesk Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="1f15b-113">A FreshDesk single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1f15b-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1f15b-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1f15b-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="1f15b-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1f15b-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="1f15b-118">Scenario description</span></span>
<span data-ttu-id="1f15b-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1f15b-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1f15b-121">갤러리에서 FreshDesk 추가</span><span class="sxs-lookup"><span data-stu-id="1f15b-121">Adding FreshDesk from the gallery</span></span>
2. <span data-ttu-id="1f15b-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="1f15b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-freshdesk-from-the-gallery"></a><span data-ttu-id="1f15b-123">갤러리에서 FreshDesk 추가</span><span class="sxs-lookup"><span data-stu-id="1f15b-123">Adding FreshDesk from the gallery</span></span>
<span data-ttu-id="1f15b-124">FreshDesk의 Azure AD 통합을 구성하려면 갤러리의 FreshDesk를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-124">To configure the integration of FreshDesk into Azure AD, you need to add FreshDesk from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1f15b-125">**갤러리에서 FreshDesk를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="1f15b-125">**To add FreshDesk from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1f15b-126">**[Azure 관리 포털](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1f15b-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1f15b-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="1f15b-131">대화 상자 위쪽에 있는 **추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-131">Click **Add** button on the top of the dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="1f15b-133">검색 상자에 **Freshdesk**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-133">In the search box, type **FreshDesk**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_search.png)

5. <span data-ttu-id="1f15b-135">결과 창에서 **FreshDesk**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-135">In the results panel, select **FreshDesk**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1f15b-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="1f15b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1f15b-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 FreshDesk에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-138">In this section, you configure and test Azure AD single sign-on with FreshDesk based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1f15b-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 FreshDesk 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-139">For single sign-on to work, Azure AD needs to know what the counterpart user in FreshDesk is to a user in Azure AD.</span></span> <span data-ttu-id="1f15b-140">즉, Azure AD 사용자와 FreshDesk의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-140">In other words, a link relationship between an Azure AD user and the related user in FreshDesk needs to be established.</span></span>

<span data-ttu-id="1f15b-141">이 연결 관계는 Azure AD의 **사용자 이름** 값을 FreshDesk의 **Username** 값으로 할당하여 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in FreshDesk.</span></span>

<span data-ttu-id="1f15b-142">FreshDesk에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-142">To configure and test Azure AD single sign-on with FreshDesk, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1f15b-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1f15b-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1f15b-145">**[FreshDesk 테스트 사용자 만들기](#creating-a-freshdesk-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 FreshDesk에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-145">**[Creating a FreshDesk test user](#creating-a-freshdesk-test-user)** - to have a counterpart of Britta Simon in FreshDesk that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="1f15b-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1f15b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1f15b-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="1f15b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1f15b-149">이 섹션에서는 Azure 관리 포털에서 Azure AD Single Sign-On을 사용하도록 설정하고 FreshDesk 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your FreshDesk application.</span></span>

<span data-ttu-id="1f15b-150">**FreshDesk에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="1f15b-150">**To configure Azure AD single sign-on with FreshDesk, perform the following steps:**</span></span>

1. <span data-ttu-id="1f15b-151">Azure 관리 포털의 **FreshDesk** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-151">In the Azure Management portal, on the **FreshDesk** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="1f15b-153">**Single sign on** 대화 상자에서 **모드**로 **SAML 기반 로그온**을 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_samlbase.png)

3. <span data-ttu-id="1f15b-155">**FreshDesk 도메인 및 URL** 섹션에서 **로그온 URL**을 `https://<tenant-name>.freshdesk.com` 또는 Freshdesk에서 제안한 다른 값으로 입력하세요.</span><span class="sxs-lookup"><span data-stu-id="1f15b-155">On the **FreshDesk Domain and URLs** section, please enter the **Sign-on URL** as: `https://<tenant-name>.freshdesk.com` or any other value Freshdesk has suggested.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_url.png)

    > [!NOTE] 
    > <span data-ttu-id="1f15b-157">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-157">Please note that this is not the real value.</span></span> <span data-ttu-id="1f15b-158">이러한 값은 실제 로그온 URL로 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-158">You have to update the value with the actual Sign-on URL.</span></span> <span data-ttu-id="1f15b-159">이 값을 얻으려면 [FreshDesk Client 지원 팀](https://freshdesk.com/helpdesk-software?utm_source=Google-AdWords&utm_medium=Search-IND-Brand&utm_campaign=Search-IND-Brand&utm_term=freshdesk&device=c&gclid=COSH2_LH7NICFVUDvAodBPgBZg)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="1f15b-159">Contact [FreshDesk Client support team](https://freshdesk.com/helpdesk-software?utm_source=Google-AdWords&utm_medium=Search-IND-Brand&utm_campaign=Search-IND-Brand&utm_term=freshdesk&device=c&gclid=COSH2_LH7NICFVUDvAodBPgBZg) to get this value.</span></span>  

4. <span data-ttu-id="1f15b-160">**SAML 서명 인증서** 섹션에서 **인증서**를 클릭한 후 컴퓨터에 인증서를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-160">On the **SAML Signing Certificate** section, click **Certificate** and then save the certificate on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_certificate.png) 

5. <span data-ttu-id="1f15b-162">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-162">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-freshdesk-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1f15b-164">**FreshDesk 구성** 섹션에서 **FreshDesk 구성**을 클릭하여 로그온 구성 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-164">On the **FreshDesk Configuration** section, click **Configure FreshDesk** to open Configure sign-on window.</span></span> <span data-ttu-id="1f15b-165">**빠른 참조** 섹션에서 SAML Single Sign-On 서비스 URL 및 로그아웃 URL을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-165">Copy the SAML Single Sign-On Service URL and Sign-Out URL from the **Quick Reference** section.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_configure.png)

7. <span data-ttu-id="1f15b-167">다른 웹 브라우저 창에서 Freshdesk 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-167">In a different web browser window, log into your Freshdesk company site as an administrator.</span></span>

8. <span data-ttu-id="1f15b-168">위쪽의 메뉴에서 **관리자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-168">In the menu on the top, click **Admin**.</span></span>
   
   <span data-ttu-id="1f15b-169">![관리자](./media/active-directory-saas-freshdesk-tutorial/IC776768.png "관리자")</span><span class="sxs-lookup"><span data-stu-id="1f15b-169">![Admin](./media/active-directory-saas-freshdesk-tutorial/IC776768.png "Admin")</span></span>

9. <span data-ttu-id="1f15b-170">**일반 설정** 탭에서 **보안**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-170">In the **General Settings** tab, click **Security**.</span></span>
   
   <span data-ttu-id="1f15b-171">![보안](./media/active-directory-saas-freshdesk-tutorial/IC776769.png "보안")</span><span class="sxs-lookup"><span data-stu-id="1f15b-171">![Security](./media/active-directory-saas-freshdesk-tutorial/IC776769.png "Security")</span></span>

10. <span data-ttu-id="1f15b-172">**보안** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-172">In the **Security** section, perform the following steps:</span></span>
   
    <span data-ttu-id="1f15b-173">![Single Sign On](./media/active-directory-saas-freshdesk-tutorial/IC776770.png "Single Sign On")</span><span class="sxs-lookup"><span data-stu-id="1f15b-173">![Single Sign On](./media/active-directory-saas-freshdesk-tutorial/IC776770.png "Single Sign On")</span></span>
   
    <span data-ttu-id="1f15b-174">a.</span><span class="sxs-lookup"><span data-stu-id="1f15b-174">a.</span></span> <span data-ttu-id="1f15b-175">**SSO(Single Sign On)**의 경우 **On**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-175">For **Single Sign On (SSO)**, select **On**.</span></span>

    <span data-ttu-id="1f15b-176">b.</span><span class="sxs-lookup"><span data-stu-id="1f15b-176">b.</span></span> <span data-ttu-id="1f15b-177">**SAML SSO**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-177">Select **SAML SSO**.</span></span>

    <span data-ttu-id="1f15b-178">c.</span><span class="sxs-lookup"><span data-stu-id="1f15b-178">c.</span></span> <span data-ttu-id="1f15b-179">Azure Portal에서 복사한 **SAML Single Sign-On 서비스 URL**을 **SAML 로그인 URL** 텍스트 상자에 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-179">Type the **SAML Single Sign-On Service URL** you copied from Azure portal into the **SAML Login URL** textbox.</span></span>

    <span data-ttu-id="1f15b-180">d.</span><span class="sxs-lookup"><span data-stu-id="1f15b-180">d.</span></span> <span data-ttu-id="1f15b-181">Azure Portal에서 복사한 **로그아웃 URL**을 **로그아웃 URL** 텍스트 상자에 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-181">Type the **Sign-Out URL**  you copied from Azure portal into the **Logout URL** textbox.</span></span>

    <span data-ttu-id="1f15b-182">e.</span><span class="sxs-lookup"><span data-stu-id="1f15b-182">e.</span></span> <span data-ttu-id="1f15b-183">Azure Portal에서 다운로드한 인증서의 **지문** 값을 복사해서 **보안 인증서 지문** 텍스트 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-183">Copy the **Thumbprint** value from the downloaded certificate from Azure portal and paste it into the **Security Certificate Fingerprint** textbox.</span></span>  
 
    >[!TIP]
    ><span data-ttu-id="1f15b-184">자세한 내용은 [인증서의 지문 값을 검색하는 방법](http://youtu.be/YKQF266SAxI)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1f15b-184">For more details, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span></span> 
    
    <span data-ttu-id="1f15b-185">f.</span><span class="sxs-lookup"><span data-stu-id="1f15b-185">f.</span></span> <span data-ttu-id="1f15b-186">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-186">Click **Save**.</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1f15b-187">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="1f15b-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="1f15b-188">이 섹션의 목적은 Azure 관리 포털에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-188">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="1f15b-190">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="1f15b-190">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1f15b-191">**Azure 관리 포털**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-191">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1f15b-193">**사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭하여 사용자 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-193">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1f15b-195">대화 상자 위쪽에서 **추가**를 클릭하여 **사용자** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-195">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1f15b-197">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-197">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1f15b-199">a.</span><span class="sxs-lookup"><span data-stu-id="1f15b-199">a.</span></span> <span data-ttu-id="1f15b-200">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-200">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1f15b-201">b.</span><span class="sxs-lookup"><span data-stu-id="1f15b-201">b.</span></span> <span data-ttu-id="1f15b-202">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-202">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1f15b-203">c.</span><span class="sxs-lookup"><span data-stu-id="1f15b-203">c.</span></span> <span data-ttu-id="1f15b-204">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-204">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1f15b-205">d.</span><span class="sxs-lookup"><span data-stu-id="1f15b-205">d.</span></span> <span data-ttu-id="1f15b-206">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-206">Click **Create**.</span></span>
 
### <a name="creating-a-freshdesk-test-user"></a><span data-ttu-id="1f15b-207">FreshDesk 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="1f15b-207">Creating a FreshDesk test user</span></span>

<span data-ttu-id="1f15b-208">Azure AD 사용자가 FreshDesk에 로그인할 수 있도록 하려면 FreshDesk로 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-208">In order to enable Azure AD users to log into FreshDesk, they must be provisioned into FreshDesk.</span></span>  
<span data-ttu-id="1f15b-209">FreshDesk의 경우 프로비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-209">In the case of FreshDesk, provisioning is a manual task.</span></span>

<span data-ttu-id="1f15b-210">**사용자 계정을 프로비전하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="1f15b-210">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="1f15b-211">**Freshdesk** 테넌트에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-211">Log in to your **Freshdesk** tenant.</span></span>
2. <span data-ttu-id="1f15b-212">위쪽의 메뉴에서 **관리자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-212">In the menu on the top, click **Admin**.</span></span>
   
   <span data-ttu-id="1f15b-213">![관리자](./media/active-directory-saas-freshdesk-tutorial/IC776772.png "관리자")</span><span class="sxs-lookup"><span data-stu-id="1f15b-213">![Admin](./media/active-directory-saas-freshdesk-tutorial/IC776772.png "Admin")</span></span>

3. <span data-ttu-id="1f15b-214">**일반 설정** 탭에서 **에이전트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-214">In the **General Settings** tab, click **Agents**.</span></span>
   
   <span data-ttu-id="1f15b-215">![에이전트](./media/active-directory-saas-freshdesk-tutorial/IC776773.png "에이전트")</span><span class="sxs-lookup"><span data-stu-id="1f15b-215">![Agents](./media/active-directory-saas-freshdesk-tutorial/IC776773.png "Agents")</span></span>

4. <span data-ttu-id="1f15b-216">**새 에이전트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-216">Click **New Agent**.</span></span>
   
    <span data-ttu-id="1f15b-217">![새 에이전트](./media/active-directory-saas-freshdesk-tutorial/IC776774.png "새 에이전트")</span><span class="sxs-lookup"><span data-stu-id="1f15b-217">![New Agent](./media/active-directory-saas-freshdesk-tutorial/IC776774.png "New Agent")</span></span>

5. <span data-ttu-id="1f15b-218">에이전트 정보 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-218">On the Agent Information dialog, perform the following steps:</span></span>
   
   <span data-ttu-id="1f15b-219">![에이전트 정보](./media/active-directory-saas-freshdesk-tutorial/IC776775.png "에이전트 정보")</span><span class="sxs-lookup"><span data-stu-id="1f15b-219">![Agent Information](./media/active-directory-saas-freshdesk-tutorial/IC776775.png "Agent Information")</span></span>
   
   <span data-ttu-id="1f15b-220">a.</span><span class="sxs-lookup"><span data-stu-id="1f15b-220">a.</span></span> <span data-ttu-id="1f15b-221">**전체 이름** 텍스트 상자에 프로비전하려는 Azure AD 계정의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-221">In the **Full Name** textbox, type the name of the Azure AD account you want to provision.</span></span>

   <span data-ttu-id="1f15b-222">b.</span><span class="sxs-lookup"><span data-stu-id="1f15b-222">b.</span></span> <span data-ttu-id="1f15b-223">**전자 메일** 텍스트 상자에 프로비전하려는 Azure AD 계정의 Azure AD 전자 메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-223">In the **Email** textbox, type the Azure AD email address of the Azure AD account you want to provision.</span></span>

   <span data-ttu-id="1f15b-224">c.</span><span class="sxs-lookup"><span data-stu-id="1f15b-224">c.</span></span> <span data-ttu-id="1f15b-225">**제목** 텍스트 상자에 프로비전하려는 Azure AD 계정의 제목을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-225">In the **Title** textbox, type the title of the Azure AD account you want to provision.</span></span>

   <span data-ttu-id="1f15b-226">d.</span><span class="sxs-lookup"><span data-stu-id="1f15b-226">d.</span></span> <span data-ttu-id="1f15b-227">**에이전트 역할**을 선택한 다음 **할당**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-227">Select **Agents role**, and then click **Assign**.</span></span>
       
   <span data-ttu-id="1f15b-228">e.</span><span class="sxs-lookup"><span data-stu-id="1f15b-228">e.</span></span> <span data-ttu-id="1f15b-229">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-229">Click **Save**.</span></span>     
   
    >[!NOTE]
    ><span data-ttu-id="1f15b-230">Azure AD 계정 보유자는 활성화되기 전에 계정을 확인하기 위한 링크를 포함한 전자 메일을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-230">The Azure AD account holder will get an email that includes a link to confirm the account before it is activated.</span></span> 
    > 
    
    >[!NOTE]
    ><span data-ttu-id="1f15b-231">다른 Freshdesk 사용자 계정 생성 도구 또는 Freshdesk가 제공한 API를 사용하여 AAD 사용자 계정을 </span><span class="sxs-lookup"><span data-stu-id="1f15b-231">You can use any other Freshdesk user account creation tools or APIs provided by Freshdesk to provision AAD user accounts.</span></span> <span data-ttu-id="1f15b-232">Freshdesk에 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-232">to FreshDesk.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1f15b-233">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="1f15b-233">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1f15b-234">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Box에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-234">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Box.</span></span>

![사용자 할당][200] 

<span data-ttu-id="1f15b-236">**Britta Simon을 FreshDesk에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="1f15b-236">**To assign Britta Simon to FreshDesk, perform the following steps:**</span></span>

1. <span data-ttu-id="1f15b-237">Azure 관리 포털에서 응용 프로그램 보기를 열고 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-237">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="1f15b-239">응용 프로그램 목록에서 **FreshDesk**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-239">In the applications list, select **FreshDesk**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_app.png) 

3. <span data-ttu-id="1f15b-241">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-241">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="1f15b-243">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-243">Click **Add** button.</span></span> <span data-ttu-id="1f15b-244">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="1f15b-246">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-246">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1f15b-247">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1f15b-248">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1f15b-249">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="1f15b-249">Testing single sign-on</span></span>

<span data-ttu-id="1f15b-250">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-250">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="1f15b-251">[액세스 패널]에서 [FreshDesk] 타일을 클릭하면 로그인 페이지가 나타나서 FreshDesk 응용 프로그램에 로그온할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f15b-251">When you click the FreshDesk tile in the Access Panel, you should get login page to get signed-on to your FreshDesk application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1f15b-252">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="1f15b-252">Additional resources</span></span>

* [<span data-ttu-id="1f15b-253">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="1f15b-253">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1f15b-254">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="1f15b-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_203.png

