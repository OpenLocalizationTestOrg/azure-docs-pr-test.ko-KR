---
title: "자습서: Intralinks와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 Intralinks 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 147f2bf9-166b-402e-adc4-4b19dd336883
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: ee7fd5b88ac806104002ffb41af11bab4fd1b2dc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-intralinks"></a><span data-ttu-id="c9d39-103">자습서: Intralinks와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="c9d39-103">Tutorial: Azure Active Directory integration with Intralinks</span></span>

<span data-ttu-id="c9d39-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Intralinks를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-104">In this tutorial, you learn how to integrate Intralinks with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c9d39-105">Intralinks를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-105">Integrating Intralinks with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c9d39-106">Intralinks에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-106">You can control in Azure AD who has access to Intralinks</span></span>
- <span data-ttu-id="c9d39-107">사용자가 해당 Azure AD 계정으로 Intralinks에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-107">You can enable your users to automatically get signed-on to Intralinks (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c9d39-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c9d39-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c9d39-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c9d39-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="c9d39-110">Prerequisites</span></span>

<span data-ttu-id="c9d39-111">Intralinks와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-111">To configure Azure AD integration with Intralinks, you need the following items:</span></span>

- <span data-ttu-id="c9d39-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="c9d39-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c9d39-113">Intralinks Single Sign-on이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="c9d39-113">An Intralinks single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c9d39-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c9d39-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c9d39-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="c9d39-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c9d39-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c9d39-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="c9d39-118">Scenario description</span></span>
<span data-ttu-id="c9d39-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c9d39-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c9d39-121">갤러리에서 Intralinks 추가</span><span class="sxs-lookup"><span data-stu-id="c9d39-121">Adding Intralinks from the gallery</span></span>
2. <span data-ttu-id="c9d39-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="c9d39-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-intralinks-from-the-gallery"></a><span data-ttu-id="c9d39-123">갤러리에서 Intralinks 추가</span><span class="sxs-lookup"><span data-stu-id="c9d39-123">Adding Intralinks from the gallery</span></span>
<span data-ttu-id="c9d39-124">Intralinks의 Azure AD 통합을 구성하려면 갤러리의 Intralinks를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-124">To configure the integration of Intralinks into Azure AD, you need to add Intralinks from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c9d39-125">**갤러리에서 Intralinks를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="c9d39-125">**To add Intralinks from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c9d39-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c9d39-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c9d39-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="c9d39-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="c9d39-133">검색 상자에 **Intralinks**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-133">In the search box, type **Intralinks**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_search.png)

5. <span data-ttu-id="c9d39-135">결과 창에서 **Intralinks**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-135">In the results panel, select **Intralinks**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c9d39-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="c9d39-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c9d39-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Intralinks에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-138">In this section, you configure and test Azure AD single sign-on with Intralinks based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c9d39-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Intralinks 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Intralinks is to a user in Azure AD.</span></span> <span data-ttu-id="c9d39-140">즉, Azure AD 사용자와 Intralinks의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-140">In other words, a link relationship between an Azure AD user and the related user in Intralinks needs to be established.</span></span>

<span data-ttu-id="c9d39-141">Intralinks에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-141">In Intralinks, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c9d39-142">Intralinks에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-142">To configure and test Azure AD single sign-on with Intralinks, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c9d39-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c9d39-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c9d39-145">**[Intralinks 테스트 사용자 만들기](#creating-an-intralinks-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 Intralinks에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-145">**[Creating an Intralinks test user](#creating-an-intralinks-test-user)** - to have a counterpart of Britta Simon in Intralinks that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c9d39-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c9d39-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c9d39-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="c9d39-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c9d39-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Intralinks 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Intralinks application.</span></span>

<span data-ttu-id="c9d39-150">**Intralinks에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="c9d39-150">**To configure Azure AD single sign-on with Intralinks, perform the following steps:**</span></span>

1. <span data-ttu-id="c9d39-151">Azure Portal의 **Intralinks** 응용 프로그램 통합 페이지에서 **Single sign-on**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-151">In the Azure portal, on the **Intralinks** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="c9d39-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_samlbase.png)

3. <span data-ttu-id="c9d39-155">**Intralinks 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-155">On the **Intralinks Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_url.png)

    <span data-ttu-id="c9d39-157">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<company name>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/<AzureADTenantID>`</span><span class="sxs-lookup"><span data-stu-id="c9d39-157">In the **Sign-on URL** textbox, type a URL using the following pattern:  `https://<company name>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/<AzureADTenantID>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c9d39-158">이 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-158">This value is not real.</span></span> <span data-ttu-id="c9d39-159">이 값을 실제 로그온 URL로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="c9d39-160">이 값을 얻으려면 [Intralinks 클라이언트 지원 팀](https://www.intralinks.com/contact-1)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="c9d39-160">Contact [Intralinks Client support team](https://www.intralinks.com/contact-1) to get this value.</span></span> 
 
4. <span data-ttu-id="c9d39-161">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 메타데이터 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_certificate.png) 

5. <span data-ttu-id="c9d39-163">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-163">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-intralinks-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c9d39-165">**Intralinks** 쪽에서 Single Sign-On을 구성하려면 다운로드한 **메타데이터 XML**을 [Intralinks 지원 팀](https://www.intralinks.com/contact-1)에 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-165">To configure single sign-on on **Intralinks** side, you need to send the downloaded **Metadata XML** [Intralinks support team](https://www.intralinks.com/contact-1).</span></span> <span data-ttu-id="c9d39-166">이렇게 설정하면 SAML SSO 연결이 양쪽에서 제대로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="c9d39-167">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c9d39-168">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c9d39-169">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c9d39-170">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="c9d39-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="c9d39-171">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="c9d39-173">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="c9d39-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c9d39-174">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-174">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-intralinks-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c9d39-176">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-176">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-intralinks-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c9d39-178">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-178">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-intralinks-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c9d39-180">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-180">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-intralinks-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c9d39-182">a.</span><span class="sxs-lookup"><span data-stu-id="c9d39-182">a.</span></span> <span data-ttu-id="c9d39-183">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-183">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c9d39-184">b.</span><span class="sxs-lookup"><span data-stu-id="c9d39-184">b.</span></span> <span data-ttu-id="c9d39-185">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c9d39-186">c.</span><span class="sxs-lookup"><span data-stu-id="c9d39-186">c.</span></span> <span data-ttu-id="c9d39-187">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-187">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c9d39-188">d.</span><span class="sxs-lookup"><span data-stu-id="c9d39-188">d.</span></span> <span data-ttu-id="c9d39-189">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-189">Click **Create**.</span></span>
 
### <a name="creating-an-intralinks-test-user"></a><span data-ttu-id="c9d39-190">Intralinks 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="c9d39-190">Creating an Intralinks test user</span></span>

<span data-ttu-id="c9d39-191">이 섹션에서는 Intralinks에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-191">In this section, you create a user called Britta Simon in Intralinks.</span></span> <span data-ttu-id="c9d39-192">Intralinks 플랫폼에 사용자를 추가하려면 [Intralinks 지원 팀](https://www.intralinks.com/contact-1)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="c9d39-192">Please work with [Intralinks support team](https://www.intralinks.com/contact-1) to add the users in the Intralinks platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c9d39-193">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="c9d39-193">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c9d39-194">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Intralinks에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-194">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Intralinks.</span></span>

![사용자 할당][200] 

<span data-ttu-id="c9d39-196">**Britta Simon을 Intralinks에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="c9d39-196">**To assign Britta Simon to Intralinks, perform the following steps:**</span></span>

1. <span data-ttu-id="c9d39-197">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-197">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="c9d39-199">응용 프로그램 목록에서 **Intralinks**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-199">In the applications list, select **Intralinks**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_app.png) 

3. <span data-ttu-id="c9d39-201">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-201">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="c9d39-203">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-203">Click **Add** button.</span></span> <span data-ttu-id="c9d39-204">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="c9d39-206">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-206">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c9d39-207">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c9d39-208">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-208">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="add-intralinks-via-or-elite-application"></a><span data-ttu-id="c9d39-209">Intralinks VIA 또는 Elite 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="c9d39-209">Add Intralinks VIA or Elite application</span></span>

<span data-ttu-id="c9d39-210">Intralinks는 Deal Nexus 응용 프로그램을 제외한 모든 다른 Intralinks 응용 프로그램에 대해 동일한 SSO ID 플랫폼을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-210">Intralinks uses the same SSO identity platform for all other Intralinks applications excluding Deal Nexus application.</span></span> <span data-ttu-id="c9d39-211">따라서 다른 Intralinks 응용 프로그램을 사용하려는 경우 먼저 위에 설명된 절차를 사용하여 하나의 주 Intralinks 응용 프로그램에 대해 SSO를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-211">So if you plan to use any other Intralinks application then first you have to configure SSO for one Primary Intralinks application using the procedure described above.</span></span>

<span data-ttu-id="c9d39-212">그 후 아래 절차에 따라 SSO에 이 주 응용 프로그램을 활용할 수 있는 테넌트에 다른 Intralinks 응용 프로그램을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-212">After that you can follow the below procedure to add another Intralinks application in your tenant which can leverage this primary application for SSO.</span></span> 

>[!NOTE]
><span data-ttu-id="c9d39-213">이 기능은 Azure AD 프리미엄 SKU 고객만 사용할 수 있으며 무료 또는 기본 SKU 고객은 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-213">This feature is available only to Azure AD Premium SKU Customers and not available for Free or Basic SKU customers.</span></span>

1. <span data-ttu-id="c9d39-214">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-214">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]


2. <span data-ttu-id="c9d39-216">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-216">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c9d39-217">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-217">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="c9d39-219">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-219">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="c9d39-221">검색 상자에 **Intralinks**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-221">In the search box, type **Intralinks**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_search.png)

5. <span data-ttu-id="c9d39-223">**Intralinks 앱 추가**에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-223">On **Intralinks Add app** perform the following steps:</span></span>

    ![Intralinks VIA 또는 Elite 응용 프로그램 추가](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_addapp.png)

    <span data-ttu-id="c9d39-225">a.</span><span class="sxs-lookup"><span data-stu-id="c9d39-225">a.</span></span> <span data-ttu-id="c9d39-226">**이름** 텍스트 상자에 응용 프로그램의 적절한 이름(예: **Intralinks Elite**)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-226">In **Name** textbox, enter appropriate name of the application e.g. **Intralinks Elite**.</span></span>

    <span data-ttu-id="c9d39-227">b.</span><span class="sxs-lookup"><span data-stu-id="c9d39-227">b.</span></span> <span data-ttu-id="c9d39-228">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-228">Click **Add** button.</span></span>

6.  <span data-ttu-id="c9d39-229">Azure Portal의 **Intralinks** 응용 프로그램 통합 페이지에서 **Single sign-on**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-229">In the Azure portal, on the **Intralinks** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

7. <span data-ttu-id="c9d39-231">**Single Sign-On** 대화 상자에서 **모드**로 **연결된 로그온**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-231">On the **Single sign-on** dialog, select **Mode** as **Linked Sign-on**.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_linkedsignon.png)

8. <span data-ttu-id="c9d39-233">[Intralinks 팀](https://www.intralinks.com/contact-1)에서 다른 Intralinks 응용 프로그램에 대한 SP 시작 SSO URL을 가져오고 아래 표시된 대로 **로그온 URL 구성**에 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-233">Get the the SP Initiated SSO URL from [Intralinks team](https://www.intralinks.com/contact-1) for the other Intralinks application and enter it in **Configure Sign-on URL** as shown below.</span></span> 
    
     ![Single Sign-on 구성](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_customappurl.png)
    
     <span data-ttu-id="c9d39-235">로그온 URL 텍스트 상자에 다음 패턴을 사용하여 사용자가 Intralinks 응용 프로그램에 로그온하는 데 사용할 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-235">In the Sign On URL textbox, type the URL used by your users to sign-on to your Intralinks application using the following pattern:</span></span>
   
    `https://<company name>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/<AzureADTenantID>`

9. <span data-ttu-id="c9d39-236">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-236">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-intralinks-tutorial/tutorial_general_400.png)

10. <span data-ttu-id="c9d39-238">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** 섹션에 나와 있는 것처럼 응용 프로그램을 사용자 또는 그룹에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-238">Assign the application to user or groups as shown in the section **[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)**.</span></span>

### <a name="testing-single-sign-on"></a><span data-ttu-id="c9d39-239">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="c9d39-239">Testing single sign-on</span></span>

<span data-ttu-id="c9d39-240">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-240">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c9d39-241">액세스 패널에서 Intralinks 타일을 클릭하면 Intralinks 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9d39-241">When you click the Intralinks tile in the Access Panel, you should get automatically signed-on to your Intralinks application.</span></span>
<span data-ttu-id="c9d39-242">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c9d39-242">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c9d39-243">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="c9d39-243">Additional resources</span></span>

* [<span data-ttu-id="c9d39-244">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="c9d39-244">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c9d39-245">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="c9d39-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_203.png

