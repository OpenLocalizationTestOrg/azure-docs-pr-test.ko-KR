---
title: "자습서: Lifesize Cloud와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 Lifesize Cloud 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 75fab335-fdcd-4066-b42c-cc738fcb6513
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 7542360f9c75786bf400553090ba0a891d9c2fcc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lifesize-cloud"></a><span data-ttu-id="1515c-103">자습서: Lifesize Cloud와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="1515c-103">Tutorial: Azure Active Directory integration with Lifesize Cloud</span></span>

<span data-ttu-id="1515c-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Lifesize Cloud를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-104">In this tutorial, you learn how to integrate Lifesize Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1515c-105">Lifesize Cloud를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-105">Integrating Lifesize Cloud with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1515c-106">Lifesize Cloud에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-106">You can control in Azure AD who has access to Lifesize Cloud</span></span>
- <span data-ttu-id="1515c-107">사용자가 해당 Azure AD 계정으로 Lifesize Cloud에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-107">You can enable your users to automatically get signed-on to Lifesize Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1515c-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1515c-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1515c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1515c-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="1515c-110">Prerequisites</span></span>

<span data-ttu-id="1515c-111">Lifesize Cloud와 Azure AD의 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-111">To configure Azure AD integration with Lifesize Cloud, you need the following items:</span></span>

- <span data-ttu-id="1515c-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="1515c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1515c-113">Lifesize Cloud Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="1515c-113">A Lifesize Cloud single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1515c-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1515c-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1515c-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="1515c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1515c-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1515c-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="1515c-118">Scenario description</span></span>
<span data-ttu-id="1515c-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1515c-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1515c-121">갤러리에서 Lifesize Cloud 추가</span><span class="sxs-lookup"><span data-stu-id="1515c-121">Adding Lifesize Cloud from the gallery</span></span>
2. <span data-ttu-id="1515c-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="1515c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lifesize-cloud-from-the-gallery"></a><span data-ttu-id="1515c-123">갤러리에서 Lifesize Cloud 추가</span><span class="sxs-lookup"><span data-stu-id="1515c-123">Adding Lifesize Cloud from the gallery</span></span>
<span data-ttu-id="1515c-124">Lifesize Cloud와 Azure AD의 통합을 구성하려면 갤러리의 Lifesize Cloud를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-124">To configure the integration of Lifesize Cloud into Azure AD, you need to add Lifesize Cloud from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1515c-125">**갤러리에서 Lifesize Cloud를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="1515c-125">**To add Lifesize Cloud from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1515c-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1515c-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1515c-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="1515c-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="1515c-133">검색 상자에 **Lifesize Cloud**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-133">In the search box, type **Lifesize Cloud**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_search.png)

5. <span data-ttu-id="1515c-135">결과 패널에서 **Lifesize Cloud**를 선택하고 **추가** 단추를 클릭하여 해당 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-135">In the results panel, select **Lifesize Cloud**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1515c-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="1515c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1515c-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Lifesize Cloud에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-138">In this section, you configure and test Azure AD single sign-on with Lifesize Cloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1515c-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Lifesize Cloud 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Lifesize Cloud is to a user in Azure AD.</span></span> <span data-ttu-id="1515c-140">즉, Azure AD 사용자와 Lifesize Cloud의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-140">In other words, a link relationship between an Azure AD user and the related user in Lifesize Cloud needs to be established.</span></span>

<span data-ttu-id="1515c-141">Lifesize Cloud에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-141">In Lifesize Cloud, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="1515c-142">Lifesize Cloud에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-142">To configure and test Azure AD single sign-on with Lifesize Cloud, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1515c-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1515c-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1515c-145">**[Lifesize Cloud 테스트 사용자 만들기](#creating-a-lifesize-cloud-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 Lifesize Cloud에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-145">**[Creating a Lifesize Cloud test user](#creating-a-lifesize-cloud-test-user)** - to have a counterpart of Britta Simon in Lifesize Cloud that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1515c-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1515c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1515c-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="1515c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1515c-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Lifesize Cloud 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Lifesize Cloud application.</span></span>

<span data-ttu-id="1515c-150">**Lifesize Cloud에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="1515c-150">**To configure Azure AD single sign-on with Lifesize Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="1515c-151">Azure Portal의 **Lifesize Cloud** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-151">In the Azure portal, on the **Lifesize Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="1515c-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_samlbase.png)

3. <span data-ttu-id="1515c-155">**Lifesize Cloud 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-155">On the **Lifesize Cloud Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_url.png)

    <span data-ttu-id="1515c-157">a.</span><span class="sxs-lookup"><span data-stu-id="1515c-157">a.</span></span> <span data-ttu-id="1515c-158">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://login.lifesizecloud.com/ls/?acs`</span><span class="sxs-lookup"><span data-stu-id="1515c-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://login.lifesizecloud.com/ls/?acs`</span></span>

    <span data-ttu-id="1515c-159">b.</span><span class="sxs-lookup"><span data-stu-id="1515c-159">b.</span></span> <span data-ttu-id="1515c-160">**식별자** 텍스트 상자에서 `https://login.lifesizecloud.com/<companyname>` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-160">In the **Identifier** textbox, type a URL using the following pattern: `https://login.lifesizecloud.com/<companyname>`</span></span>

     
4. <span data-ttu-id="1515c-161">**고급 URL 설정 표시**를 확인하고, 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-161">Check **Show advanced URL settings**, perform the following step:</span></span>    
   
    ![Single Sign-on 구성](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_url1.png)

    <span data-ttu-id="1515c-163">**릴레이 상태** 텍스트 상자에서 `https://webapp.lifesizecloud.com/?ent=<identifier>` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-163">In the **Relay state** textbox, type a URL using the following pattern: `https://webapp.lifesizecloud.com/?ent=<identifier>`</span></span>
   
   > [!NOTE] 
   ><span data-ttu-id="1515c-164">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-164">Please note that these are not the real values.</span></span> <span data-ttu-id="1515c-165">실제 로그온 URL, 릴레이 상태 및 식별자로 값을 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-165">you have to update these values with the actual Sign-On URL, Relay State, and Identifier.</span></span> <span data-ttu-id="1515c-166">로그온 URL 및 식별자 값을 얻으려면 [Lifesize Cloud 클라이언트 지원 팀](https://www.lifesize.com/support)에 문의하세요. 자습서 뒷부분에서 설명하는 SSO 구성에서 릴레이 상태 값을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-166">Contact [Lifesize Cloud Client support team](https://www.lifesize.com/support) to get Sign-On URL, and Identifier values and you can get Relay State  value from SSO Configuration that is explained later in the tutorial.</span></span>

4. <span data-ttu-id="1515c-167">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-167">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_certificate.png) 

5. <span data-ttu-id="1515c-169">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-169">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1515c-171">**Lifesize Cloud 구성** 섹션에서 **Lifesize Cloud 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-171">On the **Lifesize Cloud Configuration** section, click **Configure Lifesize Cloud** to open **Configure sign-on** window.</span></span> <span data-ttu-id="1515c-172">**빠른 참조 섹션**에서 **SAML 엔터티 ID 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-172">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_configure.png) 

7. <span data-ttu-id="1515c-174">응용 프로그램에 대해 구성된 SSO를 가져오려면 관리자 권한으로 Lifesize Cloud 응용 프로그램에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-174">To get SSO configured for your application, login into the Lifesize Cloud application with Admin privileges.</span></span>

8. <span data-ttu-id="1515c-175">페이지의 오른쪽 위 모서리에 있는 사용자 이름을 클릭하고 **고급 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-175">In the top right corner click on your name and then click on the **Advance Settings**.</span></span>
   
    ![Single Sign-On 구성](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_06.png)

9. <span data-ttu-id="1515c-177">고급 설정에서 이제 **SSO 구성** 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-177">In the Advance Settings now click on the **SSO Configuration** link.</span></span> <span data-ttu-id="1515c-178">현재 인스턴스에 대한 SSO 구성 페이지가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-178">It will open the SSO Configuration page for your instance.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_07.png)

10. <span data-ttu-id="1515c-180">이제 SSO 구성 UI에서 다음 값을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-180">Now configure the following values in the SSO configuration UI.</span></span>    
   
    ![Single Sign-on 구성](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_08.png)
    
    <span data-ttu-id="1515c-182">a.</span><span class="sxs-lookup"><span data-stu-id="1515c-182">a.</span></span> <span data-ttu-id="1515c-183">Azure Portal에서 복사한 **SAML 엔터티 ID** 값을 **ID 공급자 발급자** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-183">In **Identity Provider Issuer** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="1515c-184">b.</span><span class="sxs-lookup"><span data-stu-id="1515c-184">b.</span></span>  <span data-ttu-id="1515c-185">Azure Portal에서 복사한 **SAML Single Sign-On 서비스 URL** 값을 **로그인 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-185">In **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="1515c-186">c.</span><span class="sxs-lookup"><span data-stu-id="1515c-186">c.</span></span> <span data-ttu-id="1515c-187">Azure Portal에서 다운로드한 base-64로 인코딩된 인증서를 메모장에서 열고, 콘텐츠를 클립보드에 복사한 다음, **X.509 인증서** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-187">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox.</span></span>
  
    <span data-ttu-id="1515c-188">d.</span><span class="sxs-lookup"><span data-stu-id="1515c-188">d.</span></span> <span data-ttu-id="1515c-189">이름에 대한 SAML 특성 매핑 텍스트 상자에 값을 **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**으로 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-189">In the SAML Attribute mappings for the First Name text box enter the value as **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**</span></span>
    
    <span data-ttu-id="1515c-190">e.</span><span class="sxs-lookup"><span data-stu-id="1515c-190">e.</span></span> <span data-ttu-id="1515c-191">**성**에 대한 SAML 특성 매핑 텍스트 상자에 값을 **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**으로 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-191">In the SAML Attribute mapping for the **Last Name** text box enter the value as **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**</span></span>
    
    <span data-ttu-id="1515c-192">f.</span><span class="sxs-lookup"><span data-stu-id="1515c-192">f.</span></span> <span data-ttu-id="1515c-193">**전자 메일**에 대한 SAML 특성 매핑 텍스트 상자에 값을 **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**로 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-193">In the SAML Attribute mapping for the **Email** text box enter the value as **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**</span></span>

11. <span data-ttu-id="1515c-194">구성을 확인하려면 **테스트** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-194">To check the configuration you can click on the **Test** button.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="1515c-195">테스트에 성공하려면 Azure AD에서 구성 마법사를 완료하고 테스트를 수행할 수 있는 사용자 또는 그룹에 대한 액세스를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-195">For successful testing you need to complete the configuration wizard in Azure AD and also provide access to users or groups who can perform the test.</span></span>

12. <span data-ttu-id="1515c-196">**SSO 사용** 단추를 선택하여 SSO를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-196">Enable the SSO by checking on the **Enable SSO** button.</span></span>

13. <span data-ttu-id="1515c-197">이제 모든 설정을 저장할 수 있도록 **업데이트** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-197">Now click on the **Update** button so that all the settings are saved.</span></span> <span data-ttu-id="1515c-198">그러면 RelayState 값이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-198">This will generate the RelayState value.</span></span> <span data-ttu-id="1515c-199">텍스트 상자에 생성된 RelayState 값을 복사하여 **Lifesize Cloud 도메인 및 URL** 섹션의 **릴레이 상태** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-199">Copy the RelayState value, which is generated in the text box, paste it in the **Relay State** textbox under **Lifesize Cloud Domain and URLs** section.</span></span> 

> [!TIP]
> <span data-ttu-id="1515c-200">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-200">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1515c-201">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-201">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1515c-202">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-202">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1515c-203">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="1515c-203">Creating an Azure AD test user</span></span>

<span data-ttu-id="1515c-204">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-204">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="1515c-206">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="1515c-206">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1515c-207">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-207">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1515c-209">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-209">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1515c-211">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-211">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1515c-213">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-213">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1515c-215">a.</span><span class="sxs-lookup"><span data-stu-id="1515c-215">a.</span></span> <span data-ttu-id="1515c-216">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-216">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1515c-217">b.</span><span class="sxs-lookup"><span data-stu-id="1515c-217">b.</span></span> <span data-ttu-id="1515c-218">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-218">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1515c-219">c.</span><span class="sxs-lookup"><span data-stu-id="1515c-219">c.</span></span> <span data-ttu-id="1515c-220">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-220">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1515c-221">d.</span><span class="sxs-lookup"><span data-stu-id="1515c-221">d.</span></span> <span data-ttu-id="1515c-222">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-222">Click **Create**.</span></span>
 
### <a name="creating-a-lifesize-cloud-test-user"></a><span data-ttu-id="1515c-223">Lifesize Cloud 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="1515c-223">Creating a Lifesize Cloud test user</span></span>

<span data-ttu-id="1515c-224">이 섹션에서는 Lifesize Cloud에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-224">In this section, you create a user called Britta Simon in Lifesize Cloud.</span></span> <span data-ttu-id="1515c-225">Lifesize Cloud는 자동 사용자 프로비전을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-225">Lifesize cloud does support automatic user provisioning.</span></span> <span data-ttu-id="1515c-226">Azure AD에서 인증에 성공한 사용자는 응용 프로그램에서 자동으로 프로비전됩니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-226">After successful authentication at Azure AD, the user will be automatically provisioned in the application.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1515c-227">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="1515c-227">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1515c-228">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Lifesize Cloud에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-228">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Lifesize Cloud.</span></span>

![사용자 할당][200] 

<span data-ttu-id="1515c-230">**Britta Simon을 Lifesize Cloud에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="1515c-230">**To assign Britta Simon to Lifesize Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="1515c-231">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-231">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="1515c-233">응용 프로그램 목록에서 **Lifesize Cloud**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-233">In the applications list, select **Lifesize Cloud**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_app.png) 

3. <span data-ttu-id="1515c-235">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-235">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="1515c-237">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-237">Click **Add** button.</span></span> <span data-ttu-id="1515c-238">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="1515c-240">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-240">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1515c-241">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1515c-242">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1515c-243">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="1515c-243">Testing single sign-on</span></span>

<span data-ttu-id="1515c-244">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-244">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="1515c-245">액세스 패널에서 Lifesize Cloud 타일을 클릭하면 Lifesize Cloud 응용 프로그램의 로그인 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1515c-245">When you click the Lifesize Cloud tile in the Access Panel, you should get login page of Lifesize Cloud application.</span></span>
<span data-ttu-id="1515c-246">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1515c-246">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1515c-247">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="1515c-247">Additional resources</span></span>

* [<span data-ttu-id="1515c-248">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="1515c-248">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1515c-249">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="1515c-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_203.png

