---
title: "자습서: Samanage와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 Samanage 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f0db4fb0-7eec-48c2-9c7a-beab1ab49bc2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: c54dbe407145a29a712acc3c0fb549a38ac26bed
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-samanage"></a><span data-ttu-id="9d831-103">자습서: Samanage와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="9d831-103">Tutorial: Azure Active Directory integration with Samanage</span></span>

<span data-ttu-id="9d831-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Samanage를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-104">In this tutorial, you learn how to integrate Samanage with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9d831-105">Samanage를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-105">Integrating Samanage with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9d831-106">Samanage에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-106">You can control in Azure AD who has access to Samanage</span></span>
- <span data-ttu-id="9d831-107">사용자가 해당 Azure AD 계정으로 Samanage(Single Sign-on)에 자동으로 로그인하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-107">You can enable your users to automatically get signed-on to Samanage (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9d831-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="9d831-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9d831-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9d831-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="9d831-110">Prerequisites</span></span>

<span data-ttu-id="9d831-111">Samanage와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-111">To configure Azure AD integration with Samanage, you need the following items:</span></span>

- <span data-ttu-id="9d831-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="9d831-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9d831-113">Samanage Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="9d831-113">A Samanage single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9d831-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9d831-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9d831-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="9d831-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9d831-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9d831-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="9d831-118">Scenario description</span></span>
<span data-ttu-id="9d831-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9d831-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9d831-121">갤러리에서 Samanage 추가</span><span class="sxs-lookup"><span data-stu-id="9d831-121">Adding Samanage from the gallery</span></span>
2. <span data-ttu-id="9d831-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="9d831-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-samanage-from-the-gallery"></a><span data-ttu-id="9d831-123">갤러리에서 Samanage 추가</span><span class="sxs-lookup"><span data-stu-id="9d831-123">Adding Samanage from the gallery</span></span>
<span data-ttu-id="9d831-124">Samanage의 Azure AD 통합을 구성하려면 갤러리의 Samanage를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-124">To configure the integration of Samanage into Azure AD, you need to add Samanage from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9d831-125">**갤러리에서 Samanage를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="9d831-125">**To add Samanage from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9d831-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9d831-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9d831-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="9d831-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="9d831-133">검색 상자에 **Samanage**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-133">In the search box, type **Samanage**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_search.png)

5. <span data-ttu-id="9d831-135">결과 패널에서 **Samanage**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-135">In the results panel, select **Samanage**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9d831-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="9d831-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9d831-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 사용하여 Samanage에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-138">In this section, you configure and test Azure AD single sign-on with Samanage based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9d831-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Samanage 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Samanage is to a user in Azure AD.</span></span> <span data-ttu-id="9d831-140">즉, Azure AD 사용자와 Samanage의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-140">In other words, a link relationship between an Azure AD user and the related user in Samanage needs to be established.</span></span>

<span data-ttu-id="9d831-141">Samanage에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 연결 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-141">In Samanage, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="9d831-142">Samanage에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-142">To configure and test Azure AD single sign-on with Samanage, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9d831-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9d831-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9d831-145">**[Samanage 테스트 사용자 만들기](#creating-a-samanage-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 Samanage에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-145">**[Creating a Samanage test user](#creating-a-samanage-test-user)** - to have a counterpart of Britta Simon in Samanage that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="9d831-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9d831-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9d831-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="9d831-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9d831-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Samanage 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Samanage application.</span></span>

<span data-ttu-id="9d831-150">**Samanage에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="9d831-150">**To configure Azure AD single sign-on with Samanage, perform the following steps:**</span></span>

1. <span data-ttu-id="9d831-151">Azure Portal의 **Samanage** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-151">In the Azure portal, on the **Samanage** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="9d831-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_samlbase.png)

3. <span data-ttu-id="9d831-155">**Samanage 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-155">On the **Samanage Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_url.png)

    <span data-ttu-id="9d831-157">a.</span><span class="sxs-lookup"><span data-stu-id="9d831-157">a.</span></span> <span data-ttu-id="9d831-158">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<Company Name>.samanage.com/saml_login/<Company Name>`</span><span class="sxs-lookup"><span data-stu-id="9d831-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<Company Name>.samanage.com/saml_login/<Company Name>`</span></span>

    <span data-ttu-id="9d831-159">b.</span><span class="sxs-lookup"><span data-stu-id="9d831-159">b.</span></span> <span data-ttu-id="9d831-160">**식별자** 텍스트 상자에서 `https://<Company Name>.samanage.com` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<Company Name>.samanage.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9d831-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-161">These values are not real.</span></span> <span data-ttu-id="9d831-162">자습서 뒷부분에 설명된 실제 로그온 URL 및 식별자로 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-162">Update these values with the actual Sign-on URL and Identifier, which is explained later in the tutorial.</span></span> <span data-ttu-id="9d831-163">자세한 내용은 [Samanage 클라이언트 지원 팀](https://www.samanage.com/support)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="9d831-163">For more details contact [Samanage Client support team](https://www.samanage.com/support).</span></span>    
 
4. <span data-ttu-id="9d831-164">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_certificate.png) 

5. <span data-ttu-id="9d831-166">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-166">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-samanage-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9d831-168">**Samanage 구성** 섹션에서 **Samanage 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-168">On the **Samanage Configuration** section, click **Configure Samanage** to open **Configure sign-on** window.</span></span> <span data-ttu-id="9d831-169">**빠른 참조** 섹션에서 **로그아웃 URL 및 SAML 엔터티 ID**를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-169">Copy the **Sign-Out URL, and SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_configure.png) 

7. <span data-ttu-id="9d831-171">다른 웹 브라우저 창에서 Samanage 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-171">In a different web browser window, log into your Samanage company site as an administrator.</span></span>

8. <span data-ttu-id="9d831-172">**대시보드**를 클릭하고 왼쪽 창에서 **설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-172">Click **Dashboard** and select **Setup** in left navigation pane.</span></span>
   
    <span data-ttu-id="9d831-173">![대시보드](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "대시보드")</span><span class="sxs-lookup"><span data-stu-id="9d831-173">![Dashboard](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Dashboard")</span></span>

9. <span data-ttu-id="9d831-174">**Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-174">Click **Single Sign-On**.</span></span>
   
    <span data-ttu-id="9d831-175">![Single Sign-On](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_002.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="9d831-175">![Single Sign-On](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_002.png "Single Sign-On")</span></span>

10. <span data-ttu-id="9d831-176">**SAML을 사용하여 로그인** 섹션으로 이동하고 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-176">Navigate to **Login using SAML** section, perform the following steps:</span></span>
   
    <span data-ttu-id="9d831-177">![SAML을 사용하여 로그인](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_003.png "SAML을 사용하여 로그인")</span><span class="sxs-lookup"><span data-stu-id="9d831-177">![Login using SAML](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_003.png "Login using SAML")</span></span>
 
    <span data-ttu-id="9d831-178">a.</span><span class="sxs-lookup"><span data-stu-id="9d831-178">a.</span></span> <span data-ttu-id="9d831-179">**SAML로 Single Sign-On 사용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-179">Click **Enable Single Sign-On with SAML**.</span></span>  
 
    <span data-ttu-id="9d831-180">b.</span><span class="sxs-lookup"><span data-stu-id="9d831-180">b.</span></span> <span data-ttu-id="9d831-181">Azure Portal에서 복사한 **SAML 엔터티 ID** 값을 **Identity Provider URL**(ID 공급자 URL) 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-181">In the **Identity Provider URL** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>    
 
    <span data-ttu-id="9d831-182">c.</span><span class="sxs-lookup"><span data-stu-id="9d831-182">c.</span></span> <span data-ttu-id="9d831-183">**로그인 URL**이 Azure Portal **Samanage 도메인 및 URL**의 **로그온 URL**과 일치하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-183">Confirm the **Login URL** matches the **Sign On URL** of **Samanage Domain and URLs** section in Azure portal.</span></span>
 
    <span data-ttu-id="9d831-184">d.</span><span class="sxs-lookup"><span data-stu-id="9d831-184">d.</span></span> <span data-ttu-id="9d831-185">Azure Portal에서 복사한 **로그아웃 URL** 값을 **로그아웃 URL** 텍스트 상자에 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-185">In the **Logout URL** textbox, enter the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
 
    <span data-ttu-id="9d831-186">e.</span><span class="sxs-lookup"><span data-stu-id="9d831-186">e.</span></span> <span data-ttu-id="9d831-187">**SAML Issuer**(SAML 발급자) 텍스트 상자에 ID 공급자에서 설정한 앱 ID URI를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-187">In the **SAML Issuer** textbox, type the app id URI set in your identity provider.</span></span>
 
    <span data-ttu-id="9d831-188">f.</span><span class="sxs-lookup"><span data-stu-id="9d831-188">f.</span></span> <span data-ttu-id="9d831-189">Azure Portal에서 다운로드한 Base-64로 인코딩된 인증서를 메모장에서 열고, 내용을 클립보드에 복사한 다음 **Paste your Identity Provider x.509 Certificate below**(아래 ID 공급자 x.509 인증서 붙여넣기) 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-189">Open your base-64 encoded certificate downloaded from Azure portal in notepad, copy the content of it into your clipboard, and then paste it to the **Paste your Identity Provider x.509 Certificate below** textbox.</span></span>
 
    <span data-ttu-id="9d831-190">g.</span><span class="sxs-lookup"><span data-stu-id="9d831-190">g.</span></span> <span data-ttu-id="9d831-191">**Samanage에 없는 경우 사용자 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-191">Click **Create users if they do not exist in Samanage**.</span></span>
 
    <span data-ttu-id="9d831-192">h.</span><span class="sxs-lookup"><span data-stu-id="9d831-192">h.</span></span> <span data-ttu-id="9d831-193">**업데이트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-193">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="9d831-194">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9d831-195">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9d831-196">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9d831-197">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="9d831-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="9d831-198">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="9d831-200">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="9d831-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9d831-201">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-samanage-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9d831-203">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-samanage-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9d831-205">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-samanage-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9d831-207">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-samanage-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9d831-209">a.</span><span class="sxs-lookup"><span data-stu-id="9d831-209">a.</span></span> <span data-ttu-id="9d831-210">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9d831-211">b.</span><span class="sxs-lookup"><span data-stu-id="9d831-211">b.</span></span> <span data-ttu-id="9d831-212">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9d831-213">c.</span><span class="sxs-lookup"><span data-stu-id="9d831-213">c.</span></span> <span data-ttu-id="9d831-214">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9d831-215">d.</span><span class="sxs-lookup"><span data-stu-id="9d831-215">d.</span></span> <span data-ttu-id="9d831-216">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-216">Click **Create**.</span></span>
 
### <a name="creating-a-samanage-test-user"></a><span data-ttu-id="9d831-217">Samanage 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="9d831-217">Creating a Samanage test user</span></span>

<span data-ttu-id="9d831-218">Azure AD 사용자가 Samanage에 로그인할 수 있도록 하려면 Samanage로 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-218">To enable Azure AD users to log in to Samanage, they must be provisioned into Samanage.</span></span>  
<span data-ttu-id="9d831-219">Samanage의 경우 프로비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-219">In the case of Samanage, provisioning is a manual task.</span></span>

<span data-ttu-id="9d831-220">**사용자 계정을 프로비전하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="9d831-220">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="9d831-221">Samanage 회사 사이트에 관리자 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-221">Log into your Samanage company site as an administrator.</span></span>

2. <span data-ttu-id="9d831-222">**대시보드**를 클릭하고 왼쪽 창에서 **설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-222">Click **Dashboard** and select **Setup** in left navigation pan.</span></span>
   
    <span data-ttu-id="9d831-223">![설치](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "설치")</span><span class="sxs-lookup"><span data-stu-id="9d831-223">![Setup](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Setup")</span></span>

3. <span data-ttu-id="9d831-224">**사용자** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-224">Click the **Users** tab</span></span>
   
    <span data-ttu-id="9d831-225">![사용자](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_006.png "사용자")</span><span class="sxs-lookup"><span data-stu-id="9d831-225">![Users](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_006.png "Users")</span></span>

4. <span data-ttu-id="9d831-226">**새 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-226">Click **New User**.</span></span>
   
    <span data-ttu-id="9d831-227">![새 사용자](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_007.png "새 사용자")</span><span class="sxs-lookup"><span data-stu-id="9d831-227">![New User](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_007.png "New User")</span></span>

5. <span data-ttu-id="9d831-228">프로비전할 Azure Active Directory 계정의 **이름**과 **메일 주소**를 입력하고 **사용자 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-228">Type the **Name** and the **Email Address** of an Azure Active Directory account you want to provision and click **Create user**.</span></span>
   
    <span data-ttu-id="9d831-229">![사용자 만들기](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_008.png "사용자 만들기")</span><span class="sxs-lookup"><span data-stu-id="9d831-229">![Create User](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_008.png "Create User")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="9d831-230">Azure Active Directory 계정 보유자는 활성화되기 전에 전자 메일을 받고 링크를 따라 계정을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-230">The Azure Active Directory account holder will receive an email and follow a link to confirm their account before it becomes active.</span></span> <span data-ttu-id="9d831-231">Samanage에서 제공하는 다른 Samanage 사용자 계정 만들기 도구 또는 API를 사용하여 Azure Active Directory 사용자 계정을 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-231">You can use any other Samanage user account creation tools or APIs provided by Samanage to provision Azure Active Directory user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="9d831-232">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="9d831-232">Assigning the Azure AD test user</span></span>

<span data-ttu-id="9d831-233">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Samanage에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-233">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Samanage.</span></span>

![사용자 할당][200] 

<span data-ttu-id="9d831-235">**Britta Simon을 Samanage에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="9d831-235">**To assign Britta Simon to Samanage, perform the following steps:**</span></span>

1. <span data-ttu-id="9d831-236">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-236">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="9d831-238">응용 프로그램 목록에서 **Samanage**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-238">In the applications list, select **Samanage**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_app.png) 

3. <span data-ttu-id="9d831-240">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-240">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="9d831-242">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-242">Click **Add** button.</span></span> <span data-ttu-id="9d831-243">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="9d831-245">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-245">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9d831-246">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9d831-247">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9d831-248">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="9d831-248">Testing single sign-on</span></span>

<span data-ttu-id="9d831-249">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-249">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="9d831-250">액세스 패널에서 Samanage 타일을 클릭하면 Samanage 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="9d831-250">When you click the Samanage tile in the Access Panel, you should get automatically signed-on to your Samanage application.</span></span>
<span data-ttu-id="9d831-251">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9d831-251">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9d831-252">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="9d831-252">Additional resources</span></span>

* [<span data-ttu-id="9d831-253">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="9d831-253">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9d831-254">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="9d831-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_203.png

