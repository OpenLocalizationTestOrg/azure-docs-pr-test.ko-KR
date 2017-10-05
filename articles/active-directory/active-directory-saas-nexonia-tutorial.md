---
title: "자습서: Nexonia와 Azure Active Directory 통합 | Microsoft 문서"
description: "Azure Active Directory 및 Nexonia 간에 Single Sign-On을 구성하는 방법을 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a93b771a-9bc3-444a-bdc0-457f8bb7e780
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/1/2017
ms.author: jeedes
ms.openlocfilehash: 1370fa64c2ddc25d3121c567ceea4828b1e50921
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-nexonia"></a><span data-ttu-id="d6b52-103">자습서: Nexonia와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="d6b52-103">Tutorial: Azure Active Directory integration with Nexonia</span></span>

<span data-ttu-id="d6b52-104">이 자습서에서는 Nexonia와 Azure AD(Azure Active Directory)를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d6b52-104">In this tutorial, you learn how to integrate Nexonia with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d6b52-105">Nexonia와 Azure AD를 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6b52-105">Integrating Nexonia with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d6b52-106">Azure AD에서는 Nexonia에 대한 액세스 권한이 있는 사용자를 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6b52-106">You can control in Azure AD who has access to Nexonia</span></span>
- <span data-ttu-id="d6b52-107">사용자가 Azure AD 계정으로 Nexonia에 자동으로 로그인(Single Sign-On)할 수 있도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6b52-107">You can enable your users to automatically get signed-on to Nexonia (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d6b52-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6b52-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d6b52-109">Azure AD와의 SaaS 앱 통합에 대한 자세한 내용은</span><span class="sxs-lookup"><span data-stu-id="d6b52-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="d6b52-110">[Azure Active Directory를 사용한 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d6b52-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d6b52-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d6b52-111">Prerequisites</span></span>

<span data-ttu-id="d6b52-112">Nexonia와 Azure AD를 통합하도록 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b52-112">To configure Azure AD integration with Nexonia, you need the following items:</span></span>

- <span data-ttu-id="d6b52-113">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="d6b52-113">An Azure AD subscription</span></span>
- <span data-ttu-id="d6b52-114">Nexonia Single Sign-On 사용이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="d6b52-114">A Nexonia single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d6b52-115">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d6b52-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d6b52-116">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b52-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d6b52-117">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="d6b52-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d6b52-118">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6b52-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d6b52-119">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="d6b52-119">Scenario description</span></span>
<span data-ttu-id="d6b52-120">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b52-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d6b52-121">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6b52-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d6b52-122">갤러리에서 Nexonia 추가</span><span class="sxs-lookup"><span data-stu-id="d6b52-122">Adding Nexonia from the gallery</span></span>
2. <span data-ttu-id="d6b52-123">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="d6b52-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-nexonia-from-the-gallery"></a><span data-ttu-id="d6b52-124">갤러리에서 Nexonia 추가</span><span class="sxs-lookup"><span data-stu-id="d6b52-124">Adding Nexonia from the gallery</span></span>
<span data-ttu-id="d6b52-125">Azure AD에 Nexonia를 통합하도록 구성하려면 갤러리의 Nexonia를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b52-125">To configure the integration of Nexonia into Azure AD, you need to add Nexonia from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d6b52-126">**갤러리에서 Nexonia를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="d6b52-126">**To add Nexonia from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d6b52-127">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b52-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d6b52-129">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b52-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d6b52-130">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b52-130">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="d6b52-132">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b52-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="d6b52-134">검색 상자에서 **Nexonia**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b52-134">In the search box, type **Nexonia**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_search.png)

5. <span data-ttu-id="d6b52-136">결과 패널에서 **Nexonia**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b52-136">In the results panel, select **Nexonia**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d6b52-138">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="d6b52-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d6b52-139">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 하여 Nexonia에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b52-139">In this section, you configure and test Azure AD single sign-on with Nexonia based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d6b52-140">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 대응하는 Nexonia 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b52-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Nexonia is to a user in Azure AD.</span></span> <span data-ttu-id="d6b52-141">즉 Azure AD 사용자와 Nexonia의 관련 사용자 간에 연결 관계가 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b52-141">In other words, a link relationship between an Azure AD user and the related user in Nexonia needs to be established.</span></span>

<span data-ttu-id="d6b52-142">Nexonia에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b52-142">In Nexonia, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d6b52-143">Nexonia에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b52-143">To configure and test Azure AD single sign-on with Nexonia, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d6b52-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b52-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d6b52-145">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b52-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d6b52-146">**[Nexonia 테스트 사용자 만들기](#creating-a-nexonia-test-user)** - Britta Simon의 Azure AD 표현과 연결되는 대응 사용자를 Nexonia에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d6b52-146">**[Creating a Nexonia test user](#creating-a-nexonia-test-user)** - to have a counterpart of Britta Simon in Nexonia that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d6b52-147">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b52-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d6b52-148">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b52-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d6b52-149">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="d6b52-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d6b52-150">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Nexonia 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b52-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Nexonia application.</span></span>

>[!Note]
><span data-ttu-id="d6b52-151">통합에 문제가 있는 경우 문제 해결 가이드에 대한 이 [링크](https://docs.microsoft.com/azure/active-directory/application-sign-in-problem-federated-sso-gallery?WT.mc_id=UI_AAD_Enterprise_Apps_SupportOrTroubleshooting)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d6b52-151">If you have issues in the integration then refer this [link](https://docs.microsoft.com/azure/active-directory/application-sign-in-problem-federated-sso-gallery?WT.mc_id=UI_AAD_Enterprise_Apps_SupportOrTroubleshooting) for troubleshooting guide.</span></span> <span data-ttu-id="d6b52-152">그래도 해결 방법을 찾지 못하면 Azure Portal에서 지원 요청을 제기하세요.</span><span class="sxs-lookup"><span data-stu-id="d6b52-152">If you still have not found the solution, then raise the support request from Azure portal.</span></span>

<span data-ttu-id="d6b52-153">**Nexonia에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="d6b52-153">**To configure Azure AD single sign-on with Nexonia, perform the following steps:**</span></span>

1. <span data-ttu-id="d6b52-154">Azure Portal의 **Nexonia** 응용 프로그램 통합 페이지에서 **Single sign-on**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b52-154">In the Azure portal, on the **Nexonia** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="d6b52-156">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b52-156">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_samlbase.png)

3. <span data-ttu-id="d6b52-158">**Nexonia 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b52-158">On the **Nexonia Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_url.png)

    <span data-ttu-id="d6b52-160">**회신 URL** 텍스트 상자에 다음 패턴으로 URL을 입력합니다.`https://system.nexonia.com/assistant/saml.do?orgCode=<organizationcode>`</span><span class="sxs-lookup"><span data-stu-id="d6b52-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://system.nexonia.com/assistant/saml.do?orgCode=<organizationcode>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d6b52-161">이 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="d6b52-161">This value is not real.</span></span> <span data-ttu-id="d6b52-162">실제 회신 URL로 이 값을 업데이트하세요.</span><span class="sxs-lookup"><span data-stu-id="d6b52-162">Update this value with the actual Reply URL.</span></span> <span data-ttu-id="d6b52-163">이 값을 가져오려면 [Nexonia 지원 팀](https://nexonia.zendesk.com/hc/requests/new)에 문의합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b52-163">Contact [Nexonia support team](https://nexonia.zendesk.com/hc/requests/new) to get this value.</span></span> 


4. <span data-ttu-id="d6b52-164">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b52-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_certificate.png) 

5. <span data-ttu-id="d6b52-166">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b52-166">Click **Save** button.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-nexonia-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d6b52-168">**Nexonia 구성** 섹션에서 **Nexonia 구성**을 클릭하여 **로그인 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d6b52-168">On the **Nexonia Configuration** section, click **Configure Nexonia** to open **Configure sign-on** window.</span></span> <span data-ttu-id="d6b52-169">**빠른 참조 섹션**에서 **로그아웃 URL, SAML 엔터티 ID 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b52-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_configure.png) 

7. <span data-ttu-id="d6b52-171">응용 프로그램에 SSO를 구성하려면 [Nexonia 지원 팀](https://nexonia.zendesk.com/hc/requests/new)에 문의하고 다음을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b52-171">To get SSO configured for your application, contact [Nexonia support team](https://nexonia.zendesk.com/hc/requests/new) and provide them with the following:</span></span>

    <span data-ttu-id="d6b52-172">• 다운로드한 **인증서**</span><span class="sxs-lookup"><span data-stu-id="d6b52-172">• The downloaded **certificate**</span></span>

    <span data-ttu-id="d6b52-173">• **SAML 엔터티 ID**</span><span class="sxs-lookup"><span data-stu-id="d6b52-173">• The **SAML Entity ID**</span></span>

    <span data-ttu-id="d6b52-174">• **SAML Single Sign-On 서비스 URL**</span><span class="sxs-lookup"><span data-stu-id="d6b52-174">• The **SAML Single Sign-On Service URL**</span></span>

    <span data-ttu-id="d6b52-175">• **로그아웃 URL**</span><span class="sxs-lookup"><span data-stu-id="d6b52-175">• The **Sign-Out URL**</span></span>

> [!TIP]
> <span data-ttu-id="d6b52-176">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6b52-176">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d6b52-177">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6b52-177">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d6b52-178">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6b52-178">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d6b52-179">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="d6b52-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="d6b52-180">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d6b52-180">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="d6b52-182">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="d6b52-182">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d6b52-183">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b52-183">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-nexonia-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d6b52-185">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b52-185">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-nexonia-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d6b52-187">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b52-187">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-nexonia-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d6b52-189">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b52-189">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-nexonia-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d6b52-191">a.</span><span class="sxs-lookup"><span data-stu-id="d6b52-191">a.</span></span> <span data-ttu-id="d6b52-192">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b52-192">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d6b52-193">b.</span><span class="sxs-lookup"><span data-stu-id="d6b52-193">b.</span></span> <span data-ttu-id="d6b52-194">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b52-194">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d6b52-195">c.</span><span class="sxs-lookup"><span data-stu-id="d6b52-195">c.</span></span> <span data-ttu-id="d6b52-196">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="d6b52-196">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d6b52-197">d.</span><span class="sxs-lookup"><span data-stu-id="d6b52-197">d.</span></span> <span data-ttu-id="d6b52-198">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b52-198">Click **Create**.</span></span>
 
### <a name="creating-a-nexonia-test-user"></a><span data-ttu-id="d6b52-199">Nexonia 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="d6b52-199">Creating a Nexonia test user</span></span>

<span data-ttu-id="d6b52-200">이 섹션에서는 Nexonia에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d6b52-200">In this section, you create a user called Britta Simon in Nexonia.</span></span> <span data-ttu-id="d6b52-201">[Nexonia 지원 팀](https://nexonia.zendesk.com/hc/requests/new)에 문의하여 Nexonia 플랫폼에 사용자를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b52-201">Work with [Nexonia support team](https://nexonia.zendesk.com/hc/requests/new) to add the users in the Nexonia platform.</span></span> <span data-ttu-id="d6b52-202">Single Sign-On을 사용하려면 먼저 사용자를 만들고 활성화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b52-202">Users must be created and activated before you use single sign-on.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d6b52-203">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="d6b52-203">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d6b52-204">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Nexonia에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b52-204">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Nexonia.</span></span>

![사용자 할당][200] 

<span data-ttu-id="d6b52-206">**Britta Simon을 Nexonia에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="d6b52-206">**To assign Britta Simon to Nexonia, perform the following steps:**</span></span>

1. <span data-ttu-id="d6b52-207">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b52-207">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="d6b52-209">응용 프로그램 목록에서 **Nexonia**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b52-209">In the applications list, select **Nexonia**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_app.png) 

3. <span data-ttu-id="d6b52-211">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b52-211">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="d6b52-213">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b52-213">Click **Add** button.</span></span> <span data-ttu-id="d6b52-214">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b52-214">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="d6b52-216">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b52-216">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d6b52-217">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b52-217">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d6b52-218">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b52-218">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d6b52-219">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="d6b52-219">Testing single sign-on</span></span>

<span data-ttu-id="d6b52-220">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b52-220">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d6b52-221">[액세스 패널]에서 [Nexonia] 타일을 클릭하면 Nexonia 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6b52-221">When you click the Nexonia tile in the Access Panel, you should get automatically signed-on to your Nexonia application.</span></span>
<span data-ttu-id="d6b52-222">액세스 패널에 대한 자세한 내용은 [Azure 시작](https://msdn.microsoft.com/library/dn308586)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d6b52-222">For more information about the Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d6b52-223">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="d6b52-223">Additional resources</span></span>

* [<span data-ttu-id="d6b52-224">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="d6b52-224">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d6b52-225">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="d6b52-225">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_203.png

