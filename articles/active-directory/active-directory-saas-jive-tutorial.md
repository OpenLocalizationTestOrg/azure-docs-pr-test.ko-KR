---
title: "자습서: Jive와 Azure Active Directory 통합 | Microsoft 문서"
description: "Azure Active Directory와 Jive 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9fc5659a-c116-4a1b-a601-333325a26b46
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 6d2d4b777d7afd74598d2eba4a7e3571a8a18d6f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jive"></a><span data-ttu-id="b9846-103">자습서: Jive와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="b9846-103">Tutorial: Azure Active Directory integration with Jive</span></span>

<span data-ttu-id="b9846-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Jive를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b9846-104">In this tutorial, you learn how to integrate Jive with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b9846-105">Jive를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9846-105">Integrating Jive with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b9846-106">Jive에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9846-106">You can control in Azure AD who has access to Jive</span></span>
- <span data-ttu-id="b9846-107">사용자가 해당 Azure AD 계정으로 Jive에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9846-107">You can enable your users to automatically get signed-on to Jive (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b9846-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9846-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b9846-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory를 사용한 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b9846-109">If you want to know more information about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b9846-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="b9846-110">Prerequisites</span></span>

<span data-ttu-id="b9846-111">Jive와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b9846-111">To configure Azure AD integration with Jive, you need the following items:</span></span>

- <span data-ttu-id="b9846-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="b9846-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b9846-113">Jive Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="b9846-113">A Jive single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b9846-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b9846-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b9846-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9846-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b9846-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="b9846-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b9846-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9846-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b9846-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="b9846-118">Scenario description</span></span>
<span data-ttu-id="b9846-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9846-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b9846-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9846-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b9846-121">갤러리에서 Jive 추가</span><span class="sxs-lookup"><span data-stu-id="b9846-121">Adding Jive from the gallery</span></span>
2. <span data-ttu-id="b9846-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="b9846-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jive-from-the-gallery"></a><span data-ttu-id="b9846-123">갤러리에서 Jive 추가</span><span class="sxs-lookup"><span data-stu-id="b9846-123">Adding Jive from the gallery</span></span>
<span data-ttu-id="b9846-124">Jive의 Azure AD 통합을 구성하려면 갤러리의 Jive를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9846-124">To configure the integration of Jive into Azure AD, you need to add Jive from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b9846-125">**갤러리에서 Jive를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="b9846-125">**To add Jive from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b9846-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b9846-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b9846-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b9846-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b9846-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b9846-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="b9846-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b9846-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="b9846-133">검색 상자에 **Jive**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b9846-133">In the search box, type **Jive**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-jive-tutorial/tutorial_jive_search.png)

5. <span data-ttu-id="b9846-135">결과 창에서 **Jive**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b9846-135">In the results panel, select **Jive**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-jive-tutorial/tutorial_jive_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b9846-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="b9846-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b9846-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Jive에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="b9846-138">In this section, you configure and test Azure AD single sign-on with Jive based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b9846-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Jive 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9846-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Jive is to a user in Azure AD.</span></span> <span data-ttu-id="b9846-140">즉, Azure AD 사용자와 Jive의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9846-140">In other words, a link relationship between an Azure AD user and the related user in Jive needs to be established.</span></span>

<span data-ttu-id="b9846-141">이 연결 관계는 Azure AD의 **사용자 이름** 값을 Jive의 **Username** 값으로 할당하여 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b9846-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Jive.</span></span>

<span data-ttu-id="b9846-142">Jive에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9846-142">To configure and test Azure AD single sign-on with Jive, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b9846-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9846-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b9846-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b9846-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b9846-145">**[Jive 테스트 사용자 만들기](#creating-a-jive-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 Jive에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b9846-145">**[Creating a Jive test user](#creating-a-jive-test-user)** - to have a counterpart of Britta Simon in Jive that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b9846-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9846-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b9846-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b9846-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b9846-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="b9846-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b9846-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Jive 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b9846-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Jive application.</span></span>

<span data-ttu-id="b9846-150">**Jive에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="b9846-150">**To configure Azure AD single sign-on with Jive, perform the following steps:**</span></span>

1. <span data-ttu-id="b9846-151">Azure Portal의 **Jive** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b9846-151">In the Azure portal, on the **Jive** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="b9846-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b9846-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-jive-tutorial/tutorial_jive_samlbase.png)

3. <span data-ttu-id="b9846-155">**Jive 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b9846-155">On the **Jive Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-jive-tutorial/tutorial_jive_url.png)

    <span data-ttu-id="b9846-157">a.</span><span class="sxs-lookup"><span data-stu-id="b9846-157">a.</span></span> <span data-ttu-id="b9846-158">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<instance name>.jivecustom.com`</span><span class="sxs-lookup"><span data-stu-id="b9846-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<instance name>.jivecustom.com`</span></span>

    <span data-ttu-id="b9846-159">b.</span><span class="sxs-lookup"><span data-stu-id="b9846-159">b.</span></span> <span data-ttu-id="b9846-160">**식별자** 텍스트 상자에서 `https://<instance name>.jiveon.com` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b9846-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<instance name>.jiveon.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b9846-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="b9846-161">These values are not the real.</span></span> <span data-ttu-id="b9846-162">실제 로그온 URL 및 식별자로 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="b9846-162">Update these values with the actual Sign-on URL and Identifier.</span></span> <span data-ttu-id="b9846-163">이러한 값을 얻으려면 [Jive 클라이언트 지원 팀](https://www.jivesoftware.com/services-support/)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="b9846-163">Contact [Jive Client support team](https://www.jivesoftware.com/services-support/) to get these values.</span></span> 
 
4. <span data-ttu-id="b9846-164">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 XML 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b9846-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-jive-tutorial/tutorial_jive_certificate.png) 

5. <span data-ttu-id="b9846-166">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b9846-166">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-jive-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b9846-168">**Jive** 쪽에서 Single Sign-On을 구성하려면 Jive 테넌트에 관리자 권한으로 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="b9846-168">To configure single sign-on on **Jive** side, sign-on to your Jive tenant as an administrator.</span></span>

7. <span data-ttu-id="b9846-169">메뉴 위쪽에서 "**SAML**"을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b9846-169">In the menu on the top, Click "**Saml**."</span></span>

    ![앱 쪽에서 Single Sign-On 구성](./media/active-directory-saas-jive-tutorial/tutorial_jive_002.png)

    <span data-ttu-id="b9846-171">a.</span><span class="sxs-lookup"><span data-stu-id="b9846-171">a.</span></span> <span data-ttu-id="b9846-172">**일반** 탭에서 **사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b9846-172">Select **Enabled** under the **General** tab.</span></span>   
    <span data-ttu-id="b9846-173">b.</span><span class="sxs-lookup"><span data-stu-id="b9846-173">b.</span></span> <span data-ttu-id="b9846-174">"**모든 SAML 설정 저장**" 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b9846-174">Click the "**Save all saml settings**" button.</span></span>

8. <span data-ttu-id="b9846-175">"**IdP 메타데이터**" 탭으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b9846-175">Navigate to the "**Idp Metadata**" tab.</span></span>
   
    ![앱 쪽에서 Single Sign-On 구성](./media/active-directory-saas-jive-tutorial/tutorial_jive_003.png)
   
    <span data-ttu-id="b9846-177">a.</span><span class="sxs-lookup"><span data-stu-id="b9846-177">a.</span></span> <span data-ttu-id="b9846-178">다운로드한 메타데이터 XML 파일의 내용을 복사한 다음 **IDP(ID 공급자) 메타데이터** 텍스트 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="b9846-178">Copy the content of the downloaded metadata XML file, and then paste it into the **Identity Provider (IDP) Metadata** textbox.</span></span>
    
    <span data-ttu-id="b9846-179">b.</span><span class="sxs-lookup"><span data-stu-id="b9846-179">b.</span></span> <span data-ttu-id="b9846-180">"**모든 SAML 설정 저장**" 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b9846-180">Click the "**Save all saml settings**" button.</span></span> 

9. <span data-ttu-id="b9846-181">"**사용자 특성 매핑**" 탭으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b9846-181">Go to the "**User Attribute Mapping**" tab.</span></span>
   
    ![앱 쪽에서 Single Sign-On 구성](./media/active-directory-saas-jive-tutorial/tutorial_jive_004.png)
   
    <span data-ttu-id="b9846-183">a.</span><span class="sxs-lookup"><span data-stu-id="b9846-183">a.</span></span> <span data-ttu-id="b9846-184">**전자 메일** 텍스트 상자에서 **mail** 값의 특성 이름을 복사한 후 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="b9846-184">In the **Email** textbox, copy and paste the attribute name of **mail** value.</span></span>
   
    <span data-ttu-id="b9846-185">b.</span><span class="sxs-lookup"><span data-stu-id="b9846-185">b.</span></span> <span data-ttu-id="b9846-186">**이름** 텍스트 상자에서 **givenname** 값의 특성 이름을 복사한 후 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="b9846-186">In the **First Name** textbox, copy and paste the attribute name of **givenname** value.</span></span>
   
    <span data-ttu-id="b9846-187">c.</span><span class="sxs-lookup"><span data-stu-id="b9846-187">c.</span></span> <span data-ttu-id="b9846-188">**성** 텍스트 상자에서 **surname** 값의 특성 이름을 복사한 후 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="b9846-188">In the **Last Name** textbox, copy and paste the attribute name of **surname** value.</span></span>

> [!TIP]
> <span data-ttu-id="b9846-189">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9846-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b9846-190">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9846-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b9846-191">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9846-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b9846-192">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="b9846-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="b9846-193">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b9846-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="b9846-195">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="b9846-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b9846-196">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b9846-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-jive-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b9846-198">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b9846-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-jive-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b9846-200">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b9846-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-jive-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b9846-202">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b9846-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-jive-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b9846-204">a.</span><span class="sxs-lookup"><span data-stu-id="b9846-204">a.</span></span> <span data-ttu-id="b9846-205">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b9846-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b9846-206">b.</span><span class="sxs-lookup"><span data-stu-id="b9846-206">b.</span></span> <span data-ttu-id="b9846-207">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b9846-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b9846-208">c.</span><span class="sxs-lookup"><span data-stu-id="b9846-208">c.</span></span> <span data-ttu-id="b9846-209">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="b9846-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b9846-210">d.</span><span class="sxs-lookup"><span data-stu-id="b9846-210">d.</span></span> <span data-ttu-id="b9846-211">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b9846-211">Click **Create**.</span></span>
 
### <a name="creating-a-jive-test-user"></a><span data-ttu-id="b9846-212">Jive 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="b9846-212">Creating a Jive test user</span></span>

<span data-ttu-id="b9846-213">Jive 플랫폼에서 사용자를 추가하려면 [Jive 클라이언트 지원 팀](https://www.jivesoftware.com/services-support/)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="b9846-213">Work with [Jive Client support team](https://www.jivesoftware.com/services-support/) to add the users in the Jive platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b9846-214">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="b9846-214">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b9846-215">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Jive에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="b9846-215">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Jive.</span></span>

![사용자 할당][200] 

<span data-ttu-id="b9846-217">**Britta Simon을 Jive에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="b9846-217">**To assign Britta Simon to Jive, perform the following steps:**</span></span>

1. <span data-ttu-id="b9846-218">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b9846-218">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="b9846-220">응용 프로그램 목록에서 **Jive**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b9846-220">In the applications list, select **Jive**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-jive-tutorial/tutorial_jive_app.png) 

3. <span data-ttu-id="b9846-222">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b9846-222">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="b9846-224">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b9846-224">Click **Add** button.</span></span> <span data-ttu-id="b9846-225">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b9846-225">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="b9846-227">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b9846-227">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b9846-228">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b9846-228">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b9846-229">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b9846-229">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b9846-230">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="b9846-230">Testing single sign-on</span></span>

<span data-ttu-id="b9846-231">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="b9846-231">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b9846-232">액세스 패널에서 Jive 타일을 클릭하면 Jive 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9846-232">When you click the Jive tile in the Access Panel, you should get automatically signed-on to your Jive application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b9846-233">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="b9846-233">Additional resources</span></span>

* [<span data-ttu-id="b9846-234">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="b9846-234">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b9846-235">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="b9846-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="b9846-236">사용자 프로비저닝 구성</span><span class="sxs-lookup"><span data-stu-id="b9846-236">Configure User Provisioning</span></span>](active-directory-saas-jive-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-jive-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jive-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jive-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jive-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jive-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jive-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jive-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jive-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jive-tutorial/tutorial_general_203.png

