---
title: "자습서: Jitbit Helpdesk와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 Jitbit Helpdesk 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 15ce27d4-0621-4103-8a34-e72c98d72ec3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 6523ee3179dafd79528093b856b0ec10fafb4f7b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jitbit-helpdesk"></a><span data-ttu-id="e0ac7-103">자습서: Jitbit Helpdesk와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="e0ac7-103">Tutorial: Azure Active Directory integration with Jitbit Helpdesk</span></span>

<span data-ttu-id="e0ac7-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Jitbit Helpdesk를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-104">In this tutorial, you learn how to integrate Jitbit Helpdesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e0ac7-105">Jitbit Helpdesk와 Azure AD를 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-105">Integrating Jitbit Helpdesk with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e0ac7-106">Jitbit Helpdesk에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-106">You can control in Azure AD who has access to Jitbit Helpdesk</span></span>
- <span data-ttu-id="e0ac7-107">사용자가 해당 Azure AD 계정으로 Jitbit Helpdesk에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-107">You can enable your users to automatically get signed-on to Jitbit Helpdesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e0ac7-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e0ac7-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e0ac7-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="e0ac7-110">Prerequisites</span></span>

<span data-ttu-id="e0ac7-111">Jitbit Helpdesk와 Azure AD를 통합하도록 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-111">To configure Azure AD integration with Jitbit Helpdesk, you need the following items:</span></span>

- <span data-ttu-id="e0ac7-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="e0ac7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e0ac7-113">Jitbit Helpdesk Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="e0ac7-113">A Jitbit Helpdesk single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e0ac7-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e0ac7-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e0ac7-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e0ac7-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e0ac7-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="e0ac7-118">Scenario description</span></span>
<span data-ttu-id="e0ac7-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e0ac7-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e0ac7-121">갤러리에서 Jitbit Helpdesk 추가</span><span class="sxs-lookup"><span data-stu-id="e0ac7-121">Adding Jitbit Helpdesk from the gallery</span></span>
2. <span data-ttu-id="e0ac7-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="e0ac7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jitbit-helpdesk-from-the-gallery"></a><span data-ttu-id="e0ac7-123">갤러리에서 Jitbit Helpdesk 추가</span><span class="sxs-lookup"><span data-stu-id="e0ac7-123">Adding Jitbit Helpdesk from the gallery</span></span>
<span data-ttu-id="e0ac7-124">Jitbit Helpdesk의 Azure AD 통합을 구성하려면 갤러리의 Jitbit Helpdesk를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-124">To configure the integration of Jitbit Helpdesk into Azure AD, you need to add Jitbit Helpdesk from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e0ac7-125">**갤러리에서 Jitbit Helpdesk를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="e0ac7-125">**To add Jitbit Helpdesk from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e0ac7-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e0ac7-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e0ac7-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="e0ac7-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="e0ac7-133">검색 상자에 **Jitbit Helpdesk**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-133">In the search box, type **Jitbit Helpdesk**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_search.png)

5. <span data-ttu-id="e0ac7-135">결과 패널에서 **Jitbit Helpdesk**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-135">In the results panel, select **Jitbit Helpdesk**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e0ac7-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="e0ac7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e0ac7-138">이 섹션에서는 “Britta Simon”이라는 테스트 사용자를 기반으로 Jitbit Helpdesk에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-138">In this section, you configure and test Azure AD single sign-on with Jitbit Helpdesk based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e0ac7-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Jitbit Helpdesk 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Jitbit Helpdesk is to a user in Azure AD.</span></span> <span data-ttu-id="e0ac7-140">즉, Azure AD 사용자와 Jitbit Helpdesk의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-140">In other words, a link relationship between an Azure AD user and the related user in Jitbit Helpdesk needs to be established.</span></span>

<span data-ttu-id="e0ac7-141">Jitbit Helpdesk에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-141">In Jitbit Helpdesk, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e0ac7-142">Jitbit Helpdesk에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-142">To configure and test Azure AD single sign-on with Jitbit Helpdesk, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e0ac7-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e0ac7-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e0ac7-145">**[Jitbit Helpdesk 테스트 사용자 만들기](#creating-a-jitbit-helpdesk-test-user)** - Britta Simon의 Azure AD 표현과 연결되는 대응 사용자를 Jitbit Helpdesk에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-145">**[Creating a Jitbit Helpdesk test user](#creating-a-jitbit-helpdesk-test-user)** - to have a counterpart of Britta Simon in Jitbit Helpdesk that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e0ac7-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e0ac7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e0ac7-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="e0ac7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e0ac7-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Jitbit Helpdesk 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Jitbit Helpdesk application.</span></span>

<span data-ttu-id="e0ac7-150">**Jitbit Helpdesk에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="e0ac7-150">**To configure Azure AD single sign-on with Jitbit Helpdesk, perform the following steps:**</span></span>

1. <span data-ttu-id="e0ac7-151">Azure Portal의 **Jitbit Helpdesk** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-151">In the Azure portal, on the **Jitbit Helpdesk** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="e0ac7-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_samlbase.png)

3. <span data-ttu-id="e0ac7-155">**Jitbit Helpdesk 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-155">On the **Jitbit Helpdesk Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_url.png)

    <span data-ttu-id="e0ac7-157">a.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-157">a.</span></span> <span data-ttu-id="e0ac7-158">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-158">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span> 
    | |     
    | ----------------------------------------|
    | `https://<hostname>/helpdesk/User/Login`|
    | `https://<tenant-name>.Jitbit.com`|
    | |
    
    > [!NOTE] 
    > <span data-ttu-id="e0ac7-159">이 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-159">This value is not real.</span></span> <span data-ttu-id="e0ac7-160">이 값을 실제 로그온 URL로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-160">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="e0ac7-161">이 값을 얻으려면 [Jitbit Helpdesk 클라이언트 지원 팀](https://www.jitbit.com/support/)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-161">Contact [Jitbit Helpdesk Client support team](https://www.jitbit.com/support/) to get this value.</span></span> 
    
    <span data-ttu-id="e0ac7-162">b.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-162">b.</span></span>  <span data-ttu-id="e0ac7-163">**식별자** 텍스트 상자에 URL `https://www.jitbit.com/web-helpdesk/`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-163">In the **Identifier** textbox, type a URL as following: `https://www.jitbit.com/web-helpdesk/`</span></span>

    
 


4. <span data-ttu-id="e0ac7-164">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_certificate.png) 

5. <span data-ttu-id="e0ac7-166">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-166">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e0ac7-168">**Jitbit Helpdesk 구성** 섹션에서 **Jitbit Helpdesk 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-168">On the **Jitbit Helpdesk Configuration** section, click **Configure Jitbit Helpdesk** to open **Configure sign-on** window.</span></span> <span data-ttu-id="e0ac7-169">**빠른 참조 섹션**에서 **SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_configure.png) 

7. <span data-ttu-id="e0ac7-171">다른 웹 브라우저 창에서 Jitbit Helpdesk 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-171">In a different web browser window, log into your Jitbit Helpdesk company site as an administrator.</span></span>

8. <span data-ttu-id="e0ac7-172">위쪽의 도구 모음에서 **관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-172">In the toolbar on the top, click **Administration**.</span></span>
   
    <span data-ttu-id="e0ac7-173">![관리](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "관리")</span><span class="sxs-lookup"><span data-stu-id="e0ac7-173">![Administration](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "Administration")</span></span>

9. <span data-ttu-id="e0ac7-174">**일반 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-174">Click **General settings**.</span></span>
   
    <span data-ttu-id="e0ac7-175">![사용자, 회사 및 권한](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777680.png "사용자, 회사 및 권한")</span><span class="sxs-lookup"><span data-stu-id="e0ac7-175">![Users, companies, and permissions](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777680.png "Users, companies, and permissions")</span></span>

10. <span data-ttu-id="e0ac7-176">**인증 설정** 구성 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-176">In the **Authentication settings** configuration section, perform the following steps:</span></span>
   
    <span data-ttu-id="e0ac7-177">![인증 설정](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777683.png "인증 설정")</span><span class="sxs-lookup"><span data-stu-id="e0ac7-177">![Authentication settings](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777683.png "Authentication settings")</span></span>
    
    <span data-ttu-id="e0ac7-178">a.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-178">a.</span></span> <span data-ttu-id="e0ac7-179">**OneLogin**과 함께 SSO(Single Sign-On)를 사용하여 로그인하려면 **SAML 2.0 Single Sign On 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-179">Select **Enable SAML 2.0 single sign on**, to sign in using Single Sign-On (SSO), with **OneLogin**.</span></span>

    <span data-ttu-id="e0ac7-180">b.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-180">b.</span></span> <span data-ttu-id="e0ac7-181">Azure Portal에서 복사한 **SAML Single Sign-On 서비스 URL** 값을 **끝점 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-181">In the **EndPoint URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="e0ac7-182">c.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-182">c.</span></span> <span data-ttu-id="e0ac7-183">**Base-64**로 인코딩된 인증서를 메모장에서 열고, 내용을 클립보드에 복사한 다음, **X.509 인증서** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-183">Open your **base-64** encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox</span></span>

    <span data-ttu-id="e0ac7-184">d.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-184">d.</span></span> <span data-ttu-id="e0ac7-185">**변경 내용 저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-185">Click **Save changes**.</span></span>

> [!TIP]
> <span data-ttu-id="e0ac7-186">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-186">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e0ac7-187">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-187">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e0ac7-188">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-188">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e0ac7-189">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="e0ac7-189">Creating an Azure AD test user</span></span>
<span data-ttu-id="e0ac7-190">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-190">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="e0ac7-192">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="e0ac7-192">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e0ac7-193">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-193">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e0ac7-195">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-195">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e0ac7-197">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-197">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e0ac7-199">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-199">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e0ac7-201">a.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-201">a.</span></span> <span data-ttu-id="e0ac7-202">**이름** 텍스트 상자에 이름을 **BrittaSimon**으로 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-202">In the **Name** textbox, type name as **BrittaSimon**.</span></span>

    <span data-ttu-id="e0ac7-203">b.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-203">b.</span></span> <span data-ttu-id="e0ac7-204">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-204">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e0ac7-205">c.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-205">c.</span></span> <span data-ttu-id="e0ac7-206">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-206">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e0ac7-207">d.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-207">d.</span></span> <span data-ttu-id="e0ac7-208">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-208">Click **Create**.</span></span>
 
### <a name="creating-a-jitbit-helpdesk-test-user"></a><span data-ttu-id="e0ac7-209">Jitbit Helpdesk 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="e0ac7-209">Creating a Jitbit Helpdesk test user</span></span>

<span data-ttu-id="e0ac7-210">Azure AD 사용자가 Jitbit Helpdesk에 로그인할 수 있도록 하려면 Jitbit Helpdesk로 프로비저닝되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-210">In order to enable Azure AD users to log into Jitbit Helpdesk, they must be provisioned into Jitbit Helpdesk.</span></span>  <span data-ttu-id="e0ac7-211">Jitbit Helpdesk의 경우 프로비저닝은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-211">In the case of Jitbit Helpdesk, provisioning is a manual task.</span></span>

<span data-ttu-id="e0ac7-212">**사용자 계정을 프로비전하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="e0ac7-212">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="e0ac7-213">**Jitbit Helpdesk** 테넌트에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-213">Log in to your **Jitbit Helpdesk** tenant.</span></span>

2. <span data-ttu-id="e0ac7-214">위쪽의 메뉴에서 **관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-214">In the menu on the top, click **Administration**.</span></span>
   
    <span data-ttu-id="e0ac7-215">![관리](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "관리")</span><span class="sxs-lookup"><span data-stu-id="e0ac7-215">![Administration](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "Administration")</span></span>

3. <span data-ttu-id="e0ac7-216">**사용자, 회사 및 사용 권한**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-216">Click **Users, companies and permissions**.</span></span>
   
    <span data-ttu-id="e0ac7-217">![사용자, 회사 및 권한](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777682.png "사용자, 회사 및 권한")</span><span class="sxs-lookup"><span data-stu-id="e0ac7-217">![Users, companies, and permissions](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777682.png "Users, companies, and permissions")</span></span>

4. <span data-ttu-id="e0ac7-218">**사용자 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-218">Click **Add user**.</span></span>
   
    <span data-ttu-id="e0ac7-219">![사용자 추가](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777685.png "사용자 추가")</span><span class="sxs-lookup"><span data-stu-id="e0ac7-219">![Add user](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777685.png "Add user")</span></span>
   
5. <span data-ttu-id="e0ac7-220">만들기 섹션에 프로비전하려는 Azure AD 계정의 데이터를 다음과 같이 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-220">In the Create section, type the data of the Azure AD account you want to provision as follows:</span></span>

    <span data-ttu-id="e0ac7-221">![만들기](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777686.png "만들기")</span><span class="sxs-lookup"><span data-stu-id="e0ac7-221">![Create](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777686.png "Create")</span></span>
   
   <span data-ttu-id="e0ac7-222">a.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-222">a.</span></span> <span data-ttu-id="e0ac7-223">**사용자 이름** 텍스트 상자에 Azure Portal 사용자 이름으로 **Britta Simon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-223">In the **Username** textbox, type **BrittaSimon**, the user name as in the Azure portal.</span></span>

   <span data-ttu-id="e0ac7-224">b.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-224">b.</span></span> <span data-ttu-id="e0ac7-225">**메일** 텍스트 상자에 사용자의 메일 주소(예: **BrittaSimon@contoso.com**)를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-225">In the **Email** textbox, type email of the user like **BrittaSimon@contoso.com**.</span></span>

   <span data-ttu-id="e0ac7-226">c.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-226">c.</span></span> <span data-ttu-id="e0ac7-227">**이름** 텍스트 상자에 사용자의 이름(예: **Britta**)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-227">In the **First Name** textbox, type first name of the user like **Britta**.</span></span>

   <span data-ttu-id="e0ac7-228">d.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-228">d.</span></span> <span data-ttu-id="e0ac7-229">**성** 텍스트 상자에 사용자의 성(예: **Simon**)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-229">In the **Last Name** textbox, type last name of the user like **Simon**.</span></span>
   
   <span data-ttu-id="e0ac7-230">e.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-230">e.</span></span> <span data-ttu-id="e0ac7-231">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-231">Click **Create**.</span></span>

>[!NOTE]
><span data-ttu-id="e0ac7-232">다른 Jitbit Helpdesk 사용자 계정 생성 도구 또는 Jitbit Helpdesk가 제공한 API를 사용하여 Azure AD 사용자 계정을 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-232">You can use any other Jitbit Helpdesk user account creation tools or APIs provided by Jitbit Helpdesk to provision Azure AD user accounts.</span></span>
> 
        

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e0ac7-233">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="e0ac7-233">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e0ac7-234">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Jitbit Helpdesk에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-234">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Jitbit Helpdesk.</span></span>

![사용자 할당][200] 

<span data-ttu-id="e0ac7-236">**Britta Simon을 Jitbit Helpdesk에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="e0ac7-236">**To assign Britta Simon to Jitbit Helpdesk, perform the following steps:**</span></span>

1. <span data-ttu-id="e0ac7-237">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-237">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="e0ac7-239">응용 프로그램 목록에서 **Jitbit Helpdesk**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-239">In the applications list, select **Jitbit Helpdesk**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_app.png) 

3. <span data-ttu-id="e0ac7-241">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-241">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="e0ac7-243">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-243">Click **Add** button.</span></span> <span data-ttu-id="e0ac7-244">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="e0ac7-246">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-246">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e0ac7-247">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e0ac7-248">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e0ac7-249">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="e0ac7-249">Testing single sign-on</span></span>

<span data-ttu-id="e0ac7-250">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-250">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e0ac7-251">액세스 패널에서 Jitbit Helpdesk 타일을 클릭하면 Jitbit Helpdesk 응용 프로그램의 로그인 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-251">When you click the Jitbit Helpdesk tile in the Access Panel, you should get login page of Jitbit Helpdesk application.</span></span>
<span data-ttu-id="e0ac7-252">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e0ac7-252">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e0ac7-253">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="e0ac7-253">Additional resources</span></span>

* [<span data-ttu-id="e0ac7-254">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="e0ac7-254">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e0ac7-255">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="e0ac7-255">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_203.png

