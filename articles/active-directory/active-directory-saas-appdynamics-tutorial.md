---
title: "자습서: AppDynamics와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory 및 AppDynamics 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 25fd1df0-411c-4f55-8be3-4273b543100f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 634e68bdb937eba68b27b824dc62fe2677e24ffe
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-appdynamics"></a><span data-ttu-id="3e582-103">자습서: AppDynamics와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="3e582-103">Tutorial: Azure Active Directory integration with AppDynamics</span></span>

<span data-ttu-id="3e582-104">이 자습서에서는 Azure AD(Azure Active Directory)와 AppDynamics를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-104">In this tutorial, you learn how to integrate AppDynamics with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3e582-105">AppDynamics를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-105">Integrating AppDynamics with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3e582-106">AppDynamics에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-106">You can control in Azure AD who has access to AppDynamics</span></span>
- <span data-ttu-id="3e582-107">사용자가 해당 Azure AD 계정으로 AppDynamics에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-107">You can enable your users to automatically get signed-on to AppDynamics (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3e582-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="3e582-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3e582-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3e582-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="3e582-110">Prerequisites</span></span>

<span data-ttu-id="3e582-111">AppDynamics와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-111">To configure Azure AD integration with AppDynamics, you need the following items:</span></span>

- <span data-ttu-id="3e582-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="3e582-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3e582-113">AppDynamics Single Sign-on이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="3e582-113">An AppDynamics single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3e582-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3e582-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3e582-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="3e582-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3e582-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3e582-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="3e582-118">Scenario description</span></span>
<span data-ttu-id="3e582-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3e582-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3e582-121">갤러리에서 AppDynamics 추가</span><span class="sxs-lookup"><span data-stu-id="3e582-121">Adding AppDynamics from the gallery</span></span>
2. <span data-ttu-id="3e582-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="3e582-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-appdynamics-from-the-gallery"></a><span data-ttu-id="3e582-123">갤러리에서 AppDynamics 추가</span><span class="sxs-lookup"><span data-stu-id="3e582-123">Adding AppDynamics from the gallery</span></span>
<span data-ttu-id="3e582-124">Azure AD와 AppDynamics 통합을 구성하려면 갤러리의 AppDynamics를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-124">To configure the integration of AppDynamics into Azure AD, you need to add AppDynamics from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3e582-125">**갤러리에서 AppDynamics를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="3e582-125">**To add AppDynamics from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3e582-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3e582-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3e582-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="3e582-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="3e582-133">검색 상자에 **AppDynamics**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-133">In the search box, type **AppDynamics**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_search.png)

5. <span data-ttu-id="3e582-135">결과 패널에서 **AppDynamics**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-135">In the results panel, select **AppDynamics**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3e582-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="3e582-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3e582-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 AppDynamics에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-138">In this section, you configure and test Azure AD single sign-on with AppDynamics based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="3e582-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 AppDynamics 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-139">For single sign-on to work, Azure AD needs to know what the counterpart user in AppDynamics is to a user in Azure AD.</span></span> <span data-ttu-id="3e582-140">즉, Azure AD 사용자와 AppDynamics의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-140">In other words, a link relationship between an Azure AD user and the related user in AppDynamics needs to be established.</span></span>

<span data-ttu-id="3e582-141">AppDynamics에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-141">In AppDynamics, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="3e582-142">AppDynamics에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-142">To configure and test Azure AD single sign-on with AppDynamics, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3e582-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3e582-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3e582-145">**[AppDynamics 테스트 사용자 만들기](#creating-an-appdynamics-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 AppDynamics에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-145">**[Creating an AppDynamics test user](#creating-an-appdynamics-test-user)** - to have a counterpart of Britta Simon in AppDynamics that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3e582-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3e582-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3e582-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="3e582-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3e582-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 AppDynamics 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your AppDynamics application.</span></span>

<span data-ttu-id="3e582-150">**AppDynamics에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="3e582-150">**To configure Azure AD single sign-on with AppDynamics, perform the following steps:**</span></span>

1. <span data-ttu-id="3e582-151">Azure Portal의 **AppDynamics** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-151">In the Azure portal, on the **AppDynamics** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="3e582-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_samlbase.png)

3. <span data-ttu-id="3e582-155">**AppDynamics 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-155">On the **AppDynamics Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_url.png)

    <span data-ttu-id="3e582-157">a.</span><span class="sxs-lookup"><span data-stu-id="3e582-157">a.</span></span> <span data-ttu-id="3e582-158">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<companyname>.saas.appdynamics.com`</span><span class="sxs-lookup"><span data-stu-id="3e582-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.saas.appdynamics.com`</span></span>

    <span data-ttu-id="3e582-159">b.</span><span class="sxs-lookup"><span data-stu-id="3e582-159">b.</span></span> <span data-ttu-id="3e582-160">**식별자** 텍스트 상자에서 `https://<companyname>.saas.appdynamics.com/controller` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.saas.appdynamics.com/controller`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3e582-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-161">These values are not real.</span></span> <span data-ttu-id="3e582-162">실제 로그온 URL 및 식별자로 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="3e582-163">이러한 값을 얻으려면 [AppDynamics 클라이언트 지원팀](https://www.appdynamics.com/support/)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="3e582-163">Contact [AppDynamics Client support team](https://www.appdynamics.com/support/) to get these values.</span></span> 
 
4. <span data-ttu-id="3e582-164">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_certificate.png) 

5. <span data-ttu-id="3e582-166">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-166">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-appdynamics-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3e582-168">**AppDynamics 구성** 섹션에서 **AppDynamics 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-168">On the **AppDynamics Configuration** section, click **Configure AppDynamics** to open **Configure sign-on** window.</span></span> <span data-ttu-id="3e582-169">**빠른 참조 섹션**에서 **로그아웃 URL 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-169">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_configure.png) 

7. <span data-ttu-id="3e582-171">다른 웹 브라우저 창에서 AppDynamics 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-171">In a different web browser window, log in to your AppDynamics company site as an administrator.</span></span>

8. <span data-ttu-id="3e582-172">위쪽의 도구 모음에서 **설정**을 클릭한 다음 **관리자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-172">In the toolbar on the top, click **Settings**, and then click **Administration**.</span></span>
   
    <span data-ttu-id="3e582-173">![관리](./media/active-directory-saas-appdynamics-tutorial/ic790216.png "관리")</span><span class="sxs-lookup"><span data-stu-id="3e582-173">![Administration](./media/active-directory-saas-appdynamics-tutorial/ic790216.png "Administration")</span></span>

9. <span data-ttu-id="3e582-174">**인증 공급자** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-174">Click the **Authentication Provider** tab.</span></span>
   
    <span data-ttu-id="3e582-175">![인증 공급자](./media/active-directory-saas-appdynamics-tutorial/ic790224.png "인증 공급자")</span><span class="sxs-lookup"><span data-stu-id="3e582-175">![Authentication Provider](./media/active-directory-saas-appdynamics-tutorial/ic790224.png "Authentication Provider")</span></span>

10. <span data-ttu-id="3e582-176">**인증 공급자** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-176">In the **Authentication Provider** section, perform the following steps:</span></span>
   
    <span data-ttu-id="3e582-177">![SAML 구성](./media/active-directory-saas-appdynamics-tutorial/ic790225.png "SAML 구성")</span><span class="sxs-lookup"><span data-stu-id="3e582-177">![SAML Configuration](./media/active-directory-saas-appdynamics-tutorial/ic790225.png "SAML Configuration")</span></span>   

    <span data-ttu-id="3e582-178">a.</span><span class="sxs-lookup"><span data-stu-id="3e582-178">a.</span></span> <span data-ttu-id="3e582-179">**인증 공급자**로 **SAML**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-179">As **Authentication Provider**, select **SAML**.</span></span>

    <span data-ttu-id="3e582-180">b.</span><span class="sxs-lookup"><span data-stu-id="3e582-180">b.</span></span> <span data-ttu-id="3e582-181">Azure Portal에서 복사한 **SAML Single Sign-On 서비스 URL** 값을 **로그인 URL** 텍스트 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-181">In the **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="3e582-182">c.</span><span class="sxs-lookup"><span data-stu-id="3e582-182">c.</span></span> <span data-ttu-id="3e582-183">Azure Portal에서 복사한 **로그아웃 URL** 값을 **로그아웃 URL** 텍스트 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-183">In the **Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
       
    <span data-ttu-id="3e582-184">d.</span><span class="sxs-lookup"><span data-stu-id="3e582-184">d.</span></span> <span data-ttu-id="3e582-185">Base 64로 인코딩된 인증서를 메모장에서 열고, 내용을 클립보드에 복사한 다음 전체 인증서를 **인증서** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-185">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **Certificate** textbox</span></span>

    <span data-ttu-id="3e582-186">e.</span><span class="sxs-lookup"><span data-stu-id="3e582-186">e.</span></span> <span data-ttu-id="3e582-187">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-187">Click **Save**.</span></span>

     <span data-ttu-id="3e582-188">![저장](./media/active-directory-saas-appdynamics-tutorial/ic777673.png "저장")</span><span class="sxs-lookup"><span data-stu-id="3e582-188">![Save](./media/active-directory-saas-appdynamics-tutorial/ic777673.png "Save")</span></span>

> [!TIP]
> <span data-ttu-id="3e582-189">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3e582-190">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3e582-191">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3e582-192">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="3e582-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="3e582-193">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="3e582-195">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="3e582-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3e582-196">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3e582-198">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3e582-200">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3e582-202">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3e582-204">a.</span><span class="sxs-lookup"><span data-stu-id="3e582-204">a.</span></span> <span data-ttu-id="3e582-205">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3e582-206">b.</span><span class="sxs-lookup"><span data-stu-id="3e582-206">b.</span></span> <span data-ttu-id="3e582-207">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3e582-208">c.</span><span class="sxs-lookup"><span data-stu-id="3e582-208">c.</span></span> <span data-ttu-id="3e582-209">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="3e582-210">d.</span><span class="sxs-lookup"><span data-stu-id="3e582-210">d.</span></span> <span data-ttu-id="3e582-211">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-211">Click **Create**.</span></span>
 
### <a name="creating-an-appdynamics-test-user"></a><span data-ttu-id="3e582-212">AppDynamics 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="3e582-212">Creating an AppDynamics test user</span></span>

<span data-ttu-id="3e582-213">Azure AD 사용자가 AppDynamics에 로그인할 수 있도록 하려면 AppDynamics로 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-213">To enable Azure AD users to log in to AppDynamics, they must be provisioned into AppDynamics.</span></span> <span data-ttu-id="3e582-214">AppDynamics의 경우 프로비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-214">In the case of AppDynamics, provisioning is a manual task.</span></span>

<span data-ttu-id="3e582-215">**사용자 프로비전을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="3e582-215">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="3e582-216">AppDynamics 회사 사이트에 관리자 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-216">Log in to your AppDynamics company site as an administrator.</span></span>

2. <span data-ttu-id="3e582-217">**사용자**로 이동한 다음 **+**를 클릭하여 **사용자 만들기** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-217">Go to **Users**, and then click **+** to open the **Create User** dialog.</span></span>
   
    <span data-ttu-id="3e582-218">![사용자](./media/active-directory-saas-appdynamics-tutorial/ic790229.png "사용자")</span><span class="sxs-lookup"><span data-stu-id="3e582-218">![Users](./media/active-directory-saas-appdynamics-tutorial/ic790229.png "Users")</span></span>

3. <span data-ttu-id="3e582-219">**사용자 만들기** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-219">In the **Create User** section, perform the following steps:</span></span>
   
    <span data-ttu-id="3e582-220">![사용자 만들기](./media/active-directory-saas-appdynamics-tutorial/ic790230.png "사용자 만들기")</span><span class="sxs-lookup"><span data-stu-id="3e582-220">![Create User](./media/active-directory-saas-appdynamics-tutorial/ic790230.png "Create User")</span></span>
   
    <span data-ttu-id="3e582-221">a.</span><span class="sxs-lookup"><span data-stu-id="3e582-221">a.</span></span> <span data-ttu-id="3e582-222">관련된 텍스트 상자에 프로비전할 유효한 AAD 계정의 **사용자 이름**, **이름**, **전자 메일**, **새 암호**, **새 암호 반복**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-222">Type the **Username**, **Name**, **Email**, **New Password**, **Repeat New Password** of a valid AAD account you want to provision into the related textboxes.</span></span>

    <span data-ttu-id="3e582-223">b.</span><span class="sxs-lookup"><span data-stu-id="3e582-223">b.</span></span> <span data-ttu-id="3e582-224">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-224">Click **Save**.</span></span>

    >[!NOTE]
    ><span data-ttu-id="3e582-225">다른 AppDynamics 사용자 계정 생성 도구 또는 AppDynamics가 제공한 API를 사용하여 Azure AD 사용자 계정을 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-225">You can use any other AppDynamics user account creation tools or APIs provided by AppDynamics to provision Azure AD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="3e582-226">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="3e582-226">Assigning the Azure AD test user</span></span>

<span data-ttu-id="3e582-227">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 AppDynamics에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-227">In this section, you enable Britta Simon to use Azure single sign-on by granting access to AppDynamics.</span></span>

![사용자 할당][200] 

<span data-ttu-id="3e582-229">**Britta Simon을 AppDynamics에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="3e582-229">**To assign Britta Simon to AppDynamics, perform the following steps:**</span></span>

1. <span data-ttu-id="3e582-230">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="3e582-232">응용 프로그램 목록에서 **AppDynamics**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-232">In the applications list, select **AppDynamics**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_app.png) 

3. <span data-ttu-id="3e582-234">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-234">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="3e582-236">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-236">Click **Add** button.</span></span> <span data-ttu-id="3e582-237">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="3e582-239">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3e582-240">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3e582-241">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3e582-242">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="3e582-242">Testing single sign-on</span></span>

<span data-ttu-id="3e582-243">이 섹션은 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-243">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="3e582-244">액세스 패널에서 AppDynamics 타일을 클릭하면 AppDynamics 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e582-244">When you click the AppDynamics tile in the Access Panel, you should get automatically signed-on to your AppDynamics application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3e582-245">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="3e582-245">Additional resources</span></span>

* [<span data-ttu-id="3e582-246">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="3e582-246">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3e582-247">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="3e582-247">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_203.png

