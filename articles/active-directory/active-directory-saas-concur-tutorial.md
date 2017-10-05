---
title: "자습서: Concur와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 Concur 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1eee0a5d-24fa-4986-9aef-3c543cfe3296
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 0b44437b3dcf69dae3587529da7d12e7809b9f55
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-concur"></a><span data-ttu-id="3f8b5-103">자습서: Concur와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="3f8b5-103">Tutorial: Azure Active Directory integration with Concur</span></span>

<span data-ttu-id="3f8b5-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Concur를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-104">In this tutorial, you learn how to integrate Concur with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3f8b5-105">Concur를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-105">Integrating Concur with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3f8b5-106">Concur에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-106">You can control in Azure AD who has access to Concur</span></span>
- <span data-ttu-id="3f8b5-107">사용자가 해당 Azure AD 계정으로 Concur에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-107">You can enable your users to automatically get signed-on to Concur (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3f8b5-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="3f8b5-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory를 사용한 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-109">If you want to know more information about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3f8b5-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="3f8b5-110">Prerequisites</span></span>

<span data-ttu-id="3f8b5-111">Concur와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-111">To configure Azure AD integration with Concur, you need the following items:</span></span>

- <span data-ttu-id="3f8b5-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="3f8b5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3f8b5-113">Concur Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="3f8b5-113">A Concur single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3f8b5-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3f8b5-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3f8b5-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3f8b5-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3f8b5-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="3f8b5-118">Scenario description</span></span>
<span data-ttu-id="3f8b5-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3f8b5-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3f8b5-121">갤러리에서 Concur 추가</span><span class="sxs-lookup"><span data-stu-id="3f8b5-121">Adding Concur from the gallery</span></span>
2. <span data-ttu-id="3f8b5-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="3f8b5-122">Configuring and testing Azure AD single sign-on</span></span>

>[!NOTE]
><span data-ttu-id="3f8b5-123">SAML을 통해 페더레이션된 SSO에 대한 Concur 구독의 구성은 별도 작업이며 수행하려면 [Concur 클라이언트 지원 팀](https://www.concur.co.in/contact)에 문의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-123">The configuration of your Concur subscription for federated SSO via SAML is a separate task, which you must contact [Concur Client support team](https://www.concur.co.in/contact) to perform.</span></span> 

## <a name="adding-concur-from-the-gallery"></a><span data-ttu-id="3f8b5-124">갤러리에서 Concur 추가</span><span class="sxs-lookup"><span data-stu-id="3f8b5-124">Adding Concur from the gallery</span></span>
<span data-ttu-id="3f8b5-125">Concur의 Azure AD 통합을 구성하려면 갤러리의 Concur를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-125">To configure the integration of Concur into Azure AD, you need to add Concur from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3f8b5-126">**갤러리에서 Concur를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="3f8b5-126">**To add Concur from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3f8b5-127">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3f8b5-129">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3f8b5-130">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-130">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="3f8b5-132">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="3f8b5-134">검색 상자에 **Concur**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-134">In the search box, type **Concur**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-concur-tutorial/tutorial_concur_search.png)

5. <span data-ttu-id="3f8b5-136">결과 패널에서 **Concur**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-136">In the results panel, select **Concur**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-concur-tutorial/tutorial_concur_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3f8b5-138">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="3f8b5-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3f8b5-139">이 섹션에서는 “Britta Simon”이라는 테스트 사용자를 기반으로 Concur에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-139">In this section, you configure and test Azure AD single sign-on with Concur based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="3f8b5-140">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Concur 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Concur is to a user in Azure AD.</span></span> <span data-ttu-id="3f8b5-141">즉, Azure AD 사용자와 Concur의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-141">In other words, a link relationship between an Azure AD user and the related user in Concur needs to be established.</span></span>

<span data-ttu-id="3f8b5-142">이 연결 관계는 Azure AD의 **사용자 이름** 값을 Concur의 **Username** 값으로 할당하여 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Concur.</span></span>

<span data-ttu-id="3f8b5-143">Concur에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-143">To configure and test Azure AD single sign-on with Concur, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3f8b5-144">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3f8b5-145">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3f8b5-146">**[Concur 테스트 사용자 만들기](#creating-a-concur-test-user)** - Britta Simon의 Azure AD 표현과 연결되는 대응 사용자를 Concur에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-146">**[Creating a Concur test user](#creating-a-concur-test-user)** - to have a counterpart of Britta Simon in Concur that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3f8b5-147">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3f8b5-148">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3f8b5-149">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="3f8b5-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3f8b5-150">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Concur 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Concur application.</span></span>

<span data-ttu-id="3f8b5-151">**Concur에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="3f8b5-151">**To configure Azure AD single sign-on with Concur, perform the following steps:**</span></span>

1. <span data-ttu-id="3f8b5-152">Azure Portal의 **Concur** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-152">In the Azure portal, on the **Concur** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="3f8b5-154">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-concur-tutorial/tutorial_concur_samlbase.png)

3. <span data-ttu-id="3f8b5-156">**Concur 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-156">On the **Concur Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-concur-tutorial/tutorial_concur_url.png)

    <span data-ttu-id="3f8b5-158">a.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-158">a.</span></span> <span data-ttu-id="3f8b5-159">**로그온 URL** 텍스트 상자에서 `https://www.concursolutions.com/UI/SSO/<OrganizationId>` 패턴을 사용하여 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-159">In the **Sign on URL** textbox, type the value using the following pattern: `https://www.concursolutions.com/UI/SSO/<OrganizationId>`</span></span>

    <span data-ttu-id="3f8b5-160">b.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-160">b.</span></span> <span data-ttu-id="3f8b5-161">**식별자** 텍스트 상자에서 `https://<customer-domain>.concursolutions.com` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-161">In the **Identifier** textbox, type a URL using the following pattern: `https://<customer-domain>.concursolutions.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3f8b5-162">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-162">These values are not the real.</span></span> <span data-ttu-id="3f8b5-163">실제 로그온 URL 및 식별자로 이러한 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-163">Update these values with the actual Sign on URL and Identifier.</span></span> <span data-ttu-id="3f8b5-164">이러한 값을 얻으려면 [Concur 클라이언트 지원 팀](https://www.concur.co.in/contact)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-164">Contact [Concur Client support team](https://www.concur.co.in/contact) to get these values.</span></span> 

4. <span data-ttu-id="3f8b5-165">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 XML 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-concur-tutorial/tutorial_concur_certificate.png) 

5. <span data-ttu-id="3f8b5-167">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-167">Click **Save** button.</span></span>

    <span data-ttu-id="3f8b5-168">![Single Sign-On 구성](./media/active-directory-saas-concur-tutorial/tutorial_general_400.png)
<CS></span><span class="sxs-lookup"><span data-stu-id="3f8b5-168">![Configure Single Sign-On](./media/active-directory-saas-concur-tutorial/tutorial_general_400.png)
<CS></span></span>

6. <span data-ttu-id="3f8b5-169">**Concur** 쪽에서 Single Sign-On을 구성하려면 다운로드한 **메타데이터 XML**을 Concur 지원에 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-169">To configure single sign-on on **Concur** side, you need to send the downloaded **Metadata XML** to Concur support.</span></span> <span data-ttu-id="3f8b5-170">이렇게 설정하면 SAML SSO 연결이 양쪽에서 제대로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-170">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

  >[!NOTE]
  ><span data-ttu-id="3f8b5-171">SAML을 통해 페더레이션된 SSO에 대한 Concur 구독의 구성은 별도 작업이며 수행하려면 [Concur 클라이언트 지원 팀](https://www.concur.co.in/contact)에 문의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-171">The configuration of your Concur subscription for federated SSO via SAML is a separate task, which you must contact [Concur Client support team](https://www.concur.co.in/contact) to perform.</span></span> 
  
<CE>

> [!TIP]
> <span data-ttu-id="3f8b5-172">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3f8b5-173">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3f8b5-174">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3f8b5-175">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="3f8b5-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="3f8b5-176">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="3f8b5-178">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="3f8b5-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3f8b5-179">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-concur-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3f8b5-181">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-concur-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3f8b5-183">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-concur-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3f8b5-185">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-concur-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3f8b5-187">a.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-187">a.</span></span> <span data-ttu-id="3f8b5-188">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3f8b5-189">b.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-189">b.</span></span> <span data-ttu-id="3f8b5-190">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3f8b5-191">c.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-191">c.</span></span> <span data-ttu-id="3f8b5-192">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="3f8b5-193">d.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-193">d.</span></span> <span data-ttu-id="3f8b5-194">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-194">Click **Create**.</span></span>
 
### <a name="creating-a-concur-test-user"></a><span data-ttu-id="3f8b5-195">Concur 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="3f8b5-195">Creating a Concur test user</span></span>

<span data-ttu-id="3f8b5-196">응용 프로그램이 Just-In-Time 사용자 프로비전을 지원하며 인증 후에는 응용 프로그램에서 자동으로 사용자가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-196">Application supports the Just in time user provisioning and after authentication users are created in the application automatically.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="3f8b5-197">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="3f8b5-197">Assigning the Azure AD test user</span></span>

<span data-ttu-id="3f8b5-198">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Concur에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Concur.</span></span>

![사용자 할당][200] 

<span data-ttu-id="3f8b5-200">**Britta Simon을 Concur에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="3f8b5-200">**To assign Britta Simon to Concur, perform the following steps:**</span></span>

1. <span data-ttu-id="3f8b5-201">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="3f8b5-203">응용 프로그램 목록에서 **Concur**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-203">In the applications list, select **Concur**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-concur-tutorial/tutorial_concur_app.png) 

3. <span data-ttu-id="3f8b5-205">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-205">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="3f8b5-207">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-207">Click **Add** button.</span></span> <span data-ttu-id="3f8b5-208">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="3f8b5-210">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3f8b5-211">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3f8b5-212">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3f8b5-213">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="3f8b5-213">Testing single sign-on</span></span>

<span data-ttu-id="3f8b5-214">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="3f8b5-215">액세스 패널에서 Concur 타일을 클릭하면 Concur 응용 프로그램의 로그인 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-215">When you click the Concur tile in the Access Panel, you should get login page of Concur application.</span></span>
<span data-ttu-id="3f8b5-216">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3f8b5-216">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="3f8b5-217">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="3f8b5-217">Additional resources</span></span>

* [<span data-ttu-id="3f8b5-218">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="3f8b5-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3f8b5-219">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="3f8b5-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="3f8b5-220">사용자 프로비저닝 구성</span><span class="sxs-lookup"><span data-stu-id="3f8b5-220">Configure User Provisioning</span></span>](active-directory-saas-concur-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-concur-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-concur-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-concur-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-concur-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-concur-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-concur-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-concur-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-concur-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-concur-tutorial/tutorial_general_203.png

