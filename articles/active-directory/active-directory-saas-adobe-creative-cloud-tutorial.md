---
title: "자습서: Adobe Creative Cloud와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 Adobe Creative Cloud 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9ba1171e-56b1-4475-b308-58637d35e5a7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 3d13608612c77236346b0e98551d7fc427d602e1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adobe-creative-cloud"></a><span data-ttu-id="002c5-103">자습서: Adobe Creative Cloud와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="002c5-103">Tutorial: Azure Active Directory integration with Adobe Creative Cloud</span></span>

<span data-ttu-id="002c5-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Adobe Creative Cloud를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-104">In this tutorial, you learn how to integrate Adobe Creative Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="002c5-105">Adobe Creative Cloud를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-105">Integrating Adobe Creative Cloud with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="002c5-106">Adobe Creative Cloud에 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-106">You can control in Azure AD who has access to Adobe Creative Cloud</span></span>
- <span data-ttu-id="002c5-107">사용자의 Azure AD 계정으로 Adobe Creative Cloud에 자동 로그인(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-107">You can enable your users to automatically get signed-on to Adobe Creative Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="002c5-108">단일 중앙 위치인 Azure 관리 포털에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="002c5-109">Azure AD와의 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory를 사용한 응용 프로그램 액세스 및 Single Sign-On](active-directory-appssoaccess-whatis.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="002c5-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="002c5-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="002c5-110">Prerequisites</span></span>

<span data-ttu-id="002c5-111">Adobe Creative Cloud와 Azure AD의 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-111">To configure Azure AD integration with Adobe Creative Cloud, you need the following items:</span></span>

- <span data-ttu-id="002c5-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="002c5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="002c5-113">Adobe Creative Cloud Single Sign-On을 사용하도록 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="002c5-113">A Adobe Creative Cloud single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="002c5-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="002c5-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="002c5-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="002c5-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="002c5-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="002c5-118">Scenario description</span></span>
<span data-ttu-id="002c5-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="002c5-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="002c5-121">갤러리에서 Adobe Creative Cloud 추가</span><span class="sxs-lookup"><span data-stu-id="002c5-121">Adding Adobe Creative Cloud from the gallery</span></span>
2. <span data-ttu-id="002c5-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="002c5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adobe-creative-cloud-from-the-gallery"></a><span data-ttu-id="002c5-123">갤러리에서 Adobe Creative Cloud 추가</span><span class="sxs-lookup"><span data-stu-id="002c5-123">Adding Adobe Creative Cloud from the gallery</span></span>
<span data-ttu-id="002c5-124">Adobe Creative Cloud가 Azure AD에 통합되도록 구성하려면 Adobe Creative Cloud를 갤러리에서 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-124">To configure the integration of Adobe Creative Cloud into Azure AD, you need to add Adobe Creative Cloud from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="002c5-125">**갤러리에서 Adobe Creative Cloud를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="002c5-125">**To add Adobe Creative Cloud from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="002c5-126">**[Azure 관리 포털](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="002c5-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="002c5-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="002c5-131">대화 상자 위쪽에 있는 **추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-131">Click **Add** button on the top of the dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="002c5-133">검색 상자에 **Adobe Creative Cloud**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-133">In the search box, type **Adobe Creative Cloud**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_000.png)

5. <span data-ttu-id="002c5-135">결과 창에서 **Adobe Creative Cloud**를 선택하고 **추가** 단추를 클릭하여 해당 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-135">In the results panel, select **Adobe Creative Cloud**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_0001.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="002c5-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="002c5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="002c5-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Adobe Creative Cloud에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-138">In this section, you configure and test Azure AD single sign-on with Adobe Creative Cloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="002c5-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Adobe Creative Cloud 사용자가 누구인지 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Adobe Creative Cloud is to a user in Azure AD.</span></span> <span data-ttu-id="002c5-140">즉, Azure AD 사용자와 Adobe Creative Cloud의 관련 사용자 간에 연결 관계가 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-140">In other words, a link relationship between an Azure AD user and the related user in Adobe Creative Cloud needs to be established.</span></span>

<span data-ttu-id="002c5-141">이 연결 관계는 Azure AD의 **사용자 이름** 값을 Adobe Creative Cloud의 **Username** 값으로 할당하여 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Adobe Creative Cloud.</span></span>

<span data-ttu-id="002c5-142">Adobe Creative Cloud에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-142">To configure and test Azure AD single sign-on with Adobe Creative Cloud, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="002c5-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="002c5-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="002c5-145">**[Adobe Creative Cloud 테스트 사용자 만들기](#creating-an-adobe-creative-cloud-test-user)** - Britta Simon의 Azure AD 표현과 연결되는 대응 사용자를 Adobe Creative Cloud에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-145">**[Creating an Adobe Creative Cloud test user](#creating-an-adobe-creative-cloud-test-user)** - to have a counterpart of Britta Simon in Adobe Creative Cloud that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="002c5-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="002c5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="002c5-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="002c5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="002c5-149">이 섹션에서는 Azure 관리 포털에서 Azure AD Single Sign-On을 사용하도록 설정하고 Adobe Creative Cloud 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Adobe Creative Cloud application.</span></span>

<span data-ttu-id="002c5-150">**Adobe Creative Cloud에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="002c5-150">**To configure Azure AD single sign-on with Adobe Creative Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="002c5-151">Azure 관리 포털의 **Adobe Creative Cloud** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-151">In the Azure Management portal, on the **Adobe Creative Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="002c5-153">**Single sign on** 대화 상자에서 **모드**로 **SAML 기반 로그온**을 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_01.png)

3. <span data-ttu-id="002c5-155">**Adobe Creative Cloud 도메인 및 URL** 섹션에서 **IDP** 시작 모드로 응용 프로그램을 구성하려는 경우 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-155">On the **Adobe Creative Cloud Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_url1.png)

    <span data-ttu-id="002c5-157">a.</span><span class="sxs-lookup"><span data-stu-id="002c5-157">a.</span></span> <span data-ttu-id="002c5-158">**식별자** 텍스트 상자에 해당 값으로 `https://www.okta.com/saml2/service-provider/<token>`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-158">In the **Identifier** textbox, type the value as: `https://www.okta.com/saml2/service-provider/<token>`</span></span>

    <span data-ttu-id="002c5-159">b.</span><span class="sxs-lookup"><span data-stu-id="002c5-159">b.</span></span> <span data-ttu-id="002c5-160">**회신 URL** 텍스트 상자에 다음 패턴으로 URL을 입력합니다.`https://<company name>.okta.com/auth/saml20/accauthlinktest`</span><span class="sxs-lookup"><span data-stu-id="002c5-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.okta.com/auth/saml20/accauthlinktest`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="002c5-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-161">Please note that these are not the real values.</span></span> <span data-ttu-id="002c5-162">실제 식별자 및 회신 URL로 해당 값을 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-162">You have to update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="002c5-163">식별자에는 고유한 문자열 값을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-163">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="002c5-164">사용자를 수동으로 만들어야 하는 경우 Adobe Creative Cloud 지원 팀에 문의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-164">If you need to create an user manually, you need to contact the Adobe Creative Cloud support team.</span></span>

4. <span data-ttu-id="002c5-165">**Adobe Creative Cloud 도메인 및 URL** 섹션에서 **SP** 시작 모드로 응용 프로그램을 구성하려는 경우 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-165">On the **Adobe Creative Cloud Domain and URLs** section, perform the following steps if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_url2.png)

    <span data-ttu-id="002c5-167">a.</span><span class="sxs-lookup"><span data-stu-id="002c5-167">a.</span></span> <span data-ttu-id="002c5-168">**고급 URL 설정 표시** 옵션을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-168">Click on the **Show advanced URL settings** option</span></span>

    <span data-ttu-id="002c5-169">b.</span><span class="sxs-lookup"><span data-stu-id="002c5-169">b.</span></span> <span data-ttu-id="002c5-170">**로그인 URL** 텍스트 상자에서 값으로 `https://adobe.com`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-170">In the **Sign-on URL** textbox, type the value as: `https://adobe.com`</span></span>

5. <span data-ttu-id="002c5-171">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-171">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_05.png) 

6. <span data-ttu-id="002c5-173">**Adobe Creative Cloud 구성** 섹션에서 **Adobe Creative Cloud 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-173">On the **Adobe Creative Cloud Configuration** section, click **Configure Adobe Creative Cloud** to open **Configure sign-on** window.</span></span> <span data-ttu-id="002c5-174">빠른 참조 섹션에서 **SAML 엔터티 ID** 및 **SAML SSO 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-174">Please copy the **SAML Entity Id** and **SAML SSO Service URL** from Quick Reference section.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_06.png) 

7. <span data-ttu-id="002c5-176">다른 웹 브라우저 창에서 Adobe Creative Cloud 테넌트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-176">In a different web browser window, sign-on to your Adobe Creative Cloud tenant as an administrator.</span></span>

8.  <span data-ttu-id="002c5-177">탐색 창에서 **ID**로 이동하여 도메인을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-177">Go to **Identity** on the left navigation pane and click your domain.</span></span> <span data-ttu-id="002c5-178">그런 다음 **Single Sign On 구성 필요** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-178">Then perform the following steps on **Single Sign On Configuration Required** section.</span></span>

    <span data-ttu-id="002c5-179">![설정](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_001.png "설정")</span><span class="sxs-lookup"><span data-stu-id="002c5-179">![Settings](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_001.png "Settings")</span></span>

9. <span data-ttu-id="002c5-180">**찾아보기**를 클릭하여 Azure AD에서 다운로드한 인증서를 **IDP 인증서**에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-180">Click **Browse** to upload the downloaded certificate from Azure AD to **IDP Certificate**.</span></span>

10. <span data-ttu-id="002c5-181">**IDP 발급자** 텍스트 상자에 Azure Portal의 **로그온 구성** 섹션에서 복사한 **SAML 엔터티 ID**의 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-181">In the **IDP issuer** textbox, put the value of **SAML Entity Id** which you copied from **Configure sign-on** section in Azure portal.</span></span>

11. <span data-ttu-id="002c5-182">**IDP 로그인 URL** 텍스트 상자에 Azure Portal의 **로그온 구성** 섹션에서 복사한 **SAML SSO 서비스 URL**의 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-182">In the **IDP Login URL** textbox, put the value of **SAML SSO Service URL** which you copied from **Configure sign-on** section in Azure portal.</span></span>

12. <span data-ttu-id="002c5-183">**HTTP - 리디렉션**을 **IDP 바인딩**으로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-183">Select **HTTP - Redirect** as **IDP Binding**.</span></span>

13. <span data-ttu-id="002c5-184">**전자 메일 주소**를 **사용자 로그인 설정**으로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-184">Select **Email Address** as **User Login Setting**.</span></span>
 
14. <span data-ttu-id="002c5-185">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-185">Click **Save** button.</span></span>

15. <span data-ttu-id="002c5-186">이제 대시보드에 XML **"메타데이터 다운로드"** 파일이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-186">The dashboard will now present the XML **"Download Metadata"** file.</span></span> <span data-ttu-id="002c5-187">여기에는 Adobe의 EntityDescriptor URL과 AssertionConsumerService URL이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-187">It contains Adobe’s EntityDescriptor URL and AssertionConsumerService URL.</span></span> <span data-ttu-id="002c5-188">Azure AD 응용 프로그램에서 파일을 열어서 구성하십시오.</span><span class="sxs-lookup"><span data-stu-id="002c5-188">Please open the file and configure them in the Azure AD application.</span></span>

    ![앱 쪽에서 Single Sign-On 구성](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_002.png)

    ![앱 쪽에서 Single Sign-On 구성](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_003.png)

    <span data-ttu-id="002c5-191">a.</span><span class="sxs-lookup"><span data-stu-id="002c5-191">a.</span></span> <span data-ttu-id="002c5-192">**앱 설정 구성** 대화 상자에서 **식별자**에 대해 Adobe가 제공한 EntityDescriptor 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-192">Use the EntityDescriptor value Adobe provided you for **Identifier** on the **Configure App Settings** dialog.</span></span>

    <span data-ttu-id="002c5-193">b.</span><span class="sxs-lookup"><span data-stu-id="002c5-193">b.</span></span> <span data-ttu-id="002c5-194">**앱 설정 구성** 대화 상자에서 **회신 URL**에 대해 Adobe가 제공한 AssertionConsumerService 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-194">Use the AssertionConsumerService value Adobe provided you for **Reply URL** on the **Configure App Settings** dialog.</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="002c5-195">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="002c5-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="002c5-196">이 섹션의 목적은 Azure 관리 포털에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-196">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="002c5-198">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="002c5-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="002c5-199">**Azure 관리 포털**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-199">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="002c5-201">**사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭하여 사용자 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-201">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="002c5-203">대화 상자 위쪽에서 **추가**를 클릭하여 **사용자** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-203">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="002c5-205">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-205">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="002c5-207">a.</span><span class="sxs-lookup"><span data-stu-id="002c5-207">a.</span></span> <span data-ttu-id="002c5-208">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-208">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="002c5-209">b.</span><span class="sxs-lookup"><span data-stu-id="002c5-209">b.</span></span> <span data-ttu-id="002c5-210">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-210">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="002c5-211">c.</span><span class="sxs-lookup"><span data-stu-id="002c5-211">c.</span></span> <span data-ttu-id="002c5-212">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-212">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="002c5-213">d.</span><span class="sxs-lookup"><span data-stu-id="002c5-213">d.</span></span> <span data-ttu-id="002c5-214">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-214">Click **Create**.</span></span> 

### <a name="creating-an-adobe-creative-cloud-test-user"></a><span data-ttu-id="002c5-215">Adobe Creative Cloud 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="002c5-215">Creating an Adobe Creative Cloud test user</span></span>

<span data-ttu-id="002c5-216">Azure AD 사용자가 Adobe Creative Cloud에 로그인할 수 있도록 하려면 Adobe Creative Cloud에 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-216">In order to enable Azure AD users to log into Adobe Creative Cloud, they must be provisioned into Adobe Creative Cloud.</span></span>  
<span data-ttu-id="002c5-217">Adobe Creative Cloud의 경우 프로비전이 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-217">In the case of Adobe Creative Cloud, provisioning is a manual task.</span></span>

<span data-ttu-id="002c5-218">**사용자 계정을 프로비전하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="002c5-218">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="002c5-219">Adobe Creative Cloud 회사 사이트에 관리자 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-219">Log in to your Adobe Creative Cloud company site as an administrator.</span></span>

2. <span data-ttu-id="002c5-220">**피플**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-220">Click **People**.</span></span>

    <span data-ttu-id="002c5-221">![사람](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_001.png "사람")</span><span class="sxs-lookup"><span data-stu-id="002c5-221">![People](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_001.png "People")</span></span>

3. <span data-ttu-id="002c5-222">**사용자 초대**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-222">Click **Invite User**.</span></span>

    <span data-ttu-id="002c5-223">![사용자 초대](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_002.png "사용자 초대")</span><span class="sxs-lookup"><span data-stu-id="002c5-223">![Invite Users](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_002.png "Invite Users")</span></span>

4. <span data-ttu-id="002c5-224">**피플 초대** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-224">On the **Invite People** dialog page, perform the following steps:</span></span>

    <span data-ttu-id="002c5-225">![피플 초대](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_003.png "피플 초대")</span><span class="sxs-lookup"><span data-stu-id="002c5-225">![Invite People](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_003.png "Invite People")</span></span>

    <span data-ttu-id="002c5-226">a.</span><span class="sxs-lookup"><span data-stu-id="002c5-226">a.</span></span> <span data-ttu-id="002c5-227">**전자 메일** 텍스트 상자에 Britta Simon 계정의 전자 메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-227">In the **Email** textbox, type the email address of Britta Simon account.</span></span>
    
    <span data-ttu-id="002c5-228">b.</span><span class="sxs-lookup"><span data-stu-id="002c5-228">b.</span></span> <span data-ttu-id="002c5-229">**초대**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-229">Click **Invite**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="002c5-230">Azure Active Directory 계정 보유자는 활성화되기 전에 전자 메일을 받고 링크를 따라 계정을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-230">The Azure Active Directory account holder will receive an email and follow a link to confirm their account before it becomes active.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="002c5-231">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="002c5-231">Assigning the Azure AD test user</span></span>

<span data-ttu-id="002c5-232">이 섹션에서는 Britta Simon이 Azure Single Sign-On을 사용할 수 있도록 그녀에게 Adobe Creative Cloud에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-232">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Adobe Creative Cloud.</span></span>

![사용자 할당][200] 

<span data-ttu-id="002c5-234">**Britta Simon을 Adobe Creative Cloud에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="002c5-234">**To assign Britta Simon to Adobe Creative Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="002c5-235">Azure 관리 포털에서 응용 프로그램 보기를 열고 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-235">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="002c5-237">응용 프로그램 목록에서 **Adobe Creative Cloud**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-237">In the applications list, select **Adobe Creative Cloud**.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_50.png) 

3. <span data-ttu-id="002c5-239">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-239">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="002c5-241">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-241">Click **Add** button.</span></span> <span data-ttu-id="002c5-242">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="002c5-244">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="002c5-245">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="002c5-246">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="002c5-247">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="002c5-247">Testing single sign-on</span></span>

<span data-ttu-id="002c5-248">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-248">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="002c5-249">액세스 패널에서 Adobe Creative Cloud 타일을 클릭하면 Adobe Creative Cloud 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="002c5-249">When you click the Adobe Creative Cloud tile in the Access Panel, you should get automatically signed-on to your Adobe Creative Cloud application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="002c5-250">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="002c5-250">Additional resources</span></span>

* [<span data-ttu-id="002c5-251">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="002c5-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="002c5-252">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="002c5-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_203.png