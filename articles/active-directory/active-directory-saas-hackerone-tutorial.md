---
title: "자습서: HackerOne과 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 HackerOne 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 229d1efb-b6a5-4df8-9839-5d551487db4e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 657d8d4c98b7b133698a5cda0aa675da7f68c464
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hackerone"></a><span data-ttu-id="3c8d8-103">자습서:Azure Active Directory와 HackerOne 통합</span><span class="sxs-lookup"><span data-stu-id="3c8d8-103">Tutorial: Azure Active Directory integration with HackerOne</span></span>

<span data-ttu-id="3c8d8-104">이 자습서에서는 Azure AD(Azure Active Directory)와 HackerOne을 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-104">In this tutorial, you learn how to integrate HackerOne with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3c8d8-105">HackerOne을 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-105">Integrating HackerOne with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3c8d8-106">HackerOne에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-106">You can control in Azure AD who has access to HackerOne</span></span>
- <span data-ttu-id="3c8d8-107">사용자가 해당 Azure AD 계정으로 HackerOne(Single Sign-on)에 자동으로 로그인하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-107">You can enable your users to automatically get signed-on to HackerOne (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3c8d8-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="3c8d8-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3c8d8-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="3c8d8-110">Prerequisites</span></span>

<span data-ttu-id="3c8d8-111">HackerOne과 Azure AD의 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-111">To configure Azure AD integration with HackerOne, you need the following items:</span></span>

- <span data-ttu-id="3c8d8-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="3c8d8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3c8d8-113">HackerOne Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="3c8d8-113">A HackerOne single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3c8d8-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3c8d8-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3c8d8-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3c8d8-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3c8d8-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="3c8d8-118">Scenario description</span></span>
<span data-ttu-id="3c8d8-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3c8d8-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3c8d8-121">갤러리에서 HackerOne 추가</span><span class="sxs-lookup"><span data-stu-id="3c8d8-121">Adding HackerOne from the gallery</span></span>
2. <span data-ttu-id="3c8d8-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="3c8d8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hackerone-from-the-gallery"></a><span data-ttu-id="3c8d8-123">갤러리에서 HackerOne 추가</span><span class="sxs-lookup"><span data-stu-id="3c8d8-123">Adding HackerOne from the gallery</span></span>
<span data-ttu-id="3c8d8-124">HackerOne의 Azure AD 통합을 구성하려면 갤러리의 HackerOne을 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-124">To configure the integration of HackerOne into Azure AD, you need to add HackerOne from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3c8d8-125">**갤러리에서 HackerOne을 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="3c8d8-125">**To add HackerOne from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3c8d8-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3c8d8-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3c8d8-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="3c8d8-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="3c8d8-133">검색 상자에 **HackerOne**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-133">In the search box, type **HackerOne**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_search.png)

5. <span data-ttu-id="3c8d8-135">결과 패널에서 **HackerOne**을 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-135">In the results panel, select **HackerOne**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3c8d8-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="3c8d8-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="3c8d8-138">이 섹션에서는 “Britta Simon”이라는 테스트 사용자를 기반으로 HackerOne에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-138">In this section, you configure and test Azure AD single sign-on with HackerOne based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="3c8d8-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 HackerOne 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-139">For single sign-on to work, Azure AD needs to know what the counterpart user in HackerOne is to a user in Azure AD.</span></span> <span data-ttu-id="3c8d8-140">즉, Azure AD 사용자와 HackerOne의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-140">In other words, a link relationship between an Azure AD user and the related user in HackerOne needs to be established.</span></span>

<span data-ttu-id="3c8d8-141">HackerOne에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-141">In HackerOne, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="3c8d8-142">HackerOne에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-142">To configure and test Azure AD single sign-on with HackerOne, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3c8d8-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3c8d8-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3c8d8-145">**[HackerOne 테스트 사용자 만들기](#creating-a-hackerone-test-user)** - Britta Simon의 Azure AD 표현과 연결되는 대응 사용자를 HackerOne에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-145">**[Creating a HackerOne test user](#creating-a-hackerone-test-user)** - to have a counterpart of Britta Simon in HackerOne that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3c8d8-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3c8d8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3c8d8-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="3c8d8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3c8d8-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 HackerOne 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your HackerOne application.</span></span>

<span data-ttu-id="3c8d8-150">**HackerOne에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="3c8d8-150">**To configure Azure AD single sign-on with HackerOne, perform the following steps:**</span></span>

1. <span data-ttu-id="3c8d8-151">Azure Portal의 **HackerOne** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-151">In the Azure portal, on the **HackerOne** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="3c8d8-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_samlbase.png)

3. <span data-ttu-id="3c8d8-155">**HackerOne Single Sign-On URL 및 식별자** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-155">On the **HackerOne Single sign-on URL and Identifier** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_url.png)

    <span data-ttu-id="3c8d8-157">a.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-157">a.</span></span> <span data-ttu-id="3c8d8-158">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://hackerone.com/<company name>/authentication`</span><span class="sxs-lookup"><span data-stu-id="3c8d8-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://hackerone.com/<company name>/authentication`</span></span>

    <span data-ttu-id="3c8d8-159">b.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-159">b.</span></span> <span data-ttu-id="3c8d8-160">**식별자** 텍스트 상자에 URL `https://hackerone.com/users/saml/metadata`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-160">In the **Identifier** textbox, type a URL as:  `https://hackerone.com/users/saml/metadata`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="3c8d8-161">이 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-161">This value is not real.</span></span> <span data-ttu-id="3c8d8-162">이 값을 실제 로그온 URL로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-162">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="3c8d8-163">이 값을 얻으려면 [HackerOne 지원 팀](mailto:support@hackerone.com)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-163">Contact [HackerOne support team](mailto:support@hackerone.com) to get this value.</span></span> 
 
4. <span data-ttu-id="3c8d8-164">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_certificate.png) 

5. <span data-ttu-id="3c8d8-166">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-166">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-hackerone-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3c8d8-168">**HackerOne 구성** 섹션에서 **HackerOne 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-168">On the **HackerOne Configuration** section, click **Configure HackerOne** to open **Configure sign-on** window.</span></span> <span data-ttu-id="3c8d8-169">**빠른 참조 섹션**에서 **SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_configure.png) 

7. <span data-ttu-id="3c8d8-171">HackerOne 테넌트에 관리자로 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-171">Sign On to your HackerOne tenant as an administrator.</span></span>

8. <span data-ttu-id="3c8d8-172">위쪽 메뉴에서 “**설정**”을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-172">In the menu on the top, click the "**Settings**."</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_001.png) 

9. <span data-ttu-id="3c8d8-174">“**인증**”으로 이동하여 “**SAML 설정 추가**”를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-174">Navigate to "**Authentication**" and click "**Add SAML settings**."</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_003.png) 

10. <span data-ttu-id="3c8d8-176">**SAML 설정** 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-176">On the **SAML Settings** dialog, perform the following steps:</span></span>
   
    ![Single Sign-On 구성](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_004.png) 

    <span data-ttu-id="3c8d8-178">a.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-178">a.</span></span> <span data-ttu-id="3c8d8-179">**전자 메일 도메인** 텍스트 상자에 등록된 도메인을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-179">In the **Email Domain** textbox, type a registered domain.</span></span>

    <span data-ttu-id="3c8d8-180">b.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-180">b.</span></span> <span data-ttu-id="3c8d8-181">Azure Portal에서 복사한 **SAML Single Sign-On 서비스 URL** 값을 **Single Sign On URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-181">In  **Single Sign On URL** textboxes, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="3c8d8-182">c.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-182">c.</span></span> <span data-ttu-id="3c8d8-183">Azure Portal에서 다운로드한 **인증서 파일**을 메모장에서 열고, 내용을 클립보드에 복사한 다음, **X509 인증서** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-183">Open your **Certificate file** in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **X509 Certificate**  textbox.</span></span>
    
    <span data-ttu-id="3c8d8-184">d.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-184">d.</span></span> <span data-ttu-id="3c8d8-185">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-185">Click **Save**.</span></span>

11. <span data-ttu-id="3c8d8-186">인증 설정 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-186">On the Authentication Settings dialog, perform the following steps:</span></span>
   
    ![Single Sign-On 구성](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_005.png) 

    <span data-ttu-id="3c8d8-188">a.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-188">a.</span></span> <span data-ttu-id="3c8d8-189">**테스트 실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-189">Click **Run test**.</span></span>

    <span data-ttu-id="3c8d8-190">b.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-190">b.</span></span> <span data-ttu-id="3c8d8-191">**상태** 필드 값이 **마지막 테스트 상태: 생성됨**인 경우 [HackerOne 지원 팀](mailto:support@hackerone.com)에 문의하여 구성 검토를 요청하세요.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-191">If the value of the **Status** field equals **Last test status: created**, contact your [HackerOne support team](mailto:support@hackerone.com) to request a review of your configuration.</span></span>

> [!TIP]
> <span data-ttu-id="3c8d8-192">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3c8d8-193">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3c8d8-194">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3c8d8-195">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="3c8d8-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="3c8d8-196">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-196">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="3c8d8-198">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="3c8d8-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3c8d8-199">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-199">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-hackerone-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3c8d8-201">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-201">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-hackerone-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3c8d8-203">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-203">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-hackerone-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3c8d8-205">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-205">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-hackerone-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3c8d8-207">a.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-207">a.</span></span> <span data-ttu-id="3c8d8-208">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-208">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3c8d8-209">b.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-209">b.</span></span> <span data-ttu-id="3c8d8-210">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-210">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3c8d8-211">c.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-211">c.</span></span> <span data-ttu-id="3c8d8-212">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-212">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="3c8d8-213">d.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-213">d.</span></span> <span data-ttu-id="3c8d8-214">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-214">Click **Create**.</span></span>
 
### <a name="creating-a-hackerone-test-user"></a><span data-ttu-id="3c8d8-215">HackerOne 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="3c8d8-215">Creating a HackerOne test user</span></span>

<span data-ttu-id="3c8d8-216">다음으로, HackerOne에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-216">Next, you create a user called Britta Simon in HackerOne.</span></span> <span data-ttu-id="3c8d8-217">HackerOne은 기본적으로 사용하도록 설정된 Just-In-Time 프로비전을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-217">HackerOne supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="3c8d8-218">이 섹션에 작업 항목이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-218">There is no action item for you in this section.</span></span> <span data-ttu-id="3c8d8-219">HackerOne에 액세스하면 사용자가 존재하지 않는 경우 새 사용자가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-219">When you access HackerOne, a new user is created if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="3c8d8-220">사용자를 수동으로 만들어야 하는 경우 Certify 지원 팀에 문의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-220">If you need to create a user manually, you need to contact the Certify support team.</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="3c8d8-221">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="3c8d8-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="3c8d8-222">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 HackerOne에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-222">In this section, you enable Britta Simon to use Azure single sign-on by granting access to HackerOne.</span></span>

![사용자 할당][200] 

<span data-ttu-id="3c8d8-224">**Britta Simon을 HackerOne에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="3c8d8-224">**To assign Britta Simon to HackerOne, perform the following steps:**</span></span>

1. <span data-ttu-id="3c8d8-225">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-225">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="3c8d8-227">응용 프로그램 목록에서 **HackerOne**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-227">In the applications list, select **HackerOne**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_app.png) 

3. <span data-ttu-id="3c8d8-229">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-229">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="3c8d8-231">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-231">Click **Add** button.</span></span> <span data-ttu-id="3c8d8-232">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="3c8d8-234">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3c8d8-235">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3c8d8-236">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3c8d8-237">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="3c8d8-237">Testing single sign-on</span></span>

<span data-ttu-id="3c8d8-238">마지막으로, 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-238">Finally, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>  

<span data-ttu-id="3c8d8-239">액세스 패널에서 HackerOne 타일을 클릭하면 HackerOne 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c8d8-239">When you click the HackerOne tile in the Access Panel, you should get automatically signed-on to your HackerOne application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3c8d8-240">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="3c8d8-240">Additional resources</span></span>

* [<span data-ttu-id="3c8d8-241">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="3c8d8-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3c8d8-242">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="3c8d8-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_203.png

