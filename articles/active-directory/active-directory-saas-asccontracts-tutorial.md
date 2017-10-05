---
title: "자습서: ASC Contracts와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory 및 ASC Contracts 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f7f54202-1581-4e55-a97e-02633ff9382d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/21/2017
ms.author: jeedes
ms.openlocfilehash: 87ea3cc55f9683e7d5b9912a87d675575cea0347
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-asc-contracts"></a><span data-ttu-id="67d5e-103">자습서: ASC Contracts와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="67d5e-103">Tutorial: Azure Active Directory integration with ASC Contracts</span></span>

<span data-ttu-id="67d5e-104">이 자습서에서는 Azure AD(Azure Active Directory)와 ASC Contracts를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="67d5e-104">In this tutorial, you learn how to integrate ASC Contracts with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="67d5e-105">ASC Contracts와 Azure AD를 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="67d5e-105">Integrating ASC Contracts with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="67d5e-106">ASC Contracts에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67d5e-106">You can control in Azure AD who has access to ASC Contracts</span></span>
- <span data-ttu-id="67d5e-107">사용자가 해당 Azure AD 계정으로 ASC Contracts에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67d5e-107">You can enable your users to automatically get signed-on to ASC Contracts (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="67d5e-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67d5e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="67d5e-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="67d5e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="67d5e-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="67d5e-110">Prerequisites</span></span>

<span data-ttu-id="67d5e-111">ASC Contracts와 Azure AD를 통합하도록 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="67d5e-111">To configure Azure AD integration with ASC Contracts, you need the following items:</span></span>

- <span data-ttu-id="67d5e-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="67d5e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="67d5e-113">ASC Contracts Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="67d5e-113">An ASC Contracts single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="67d5e-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="67d5e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="67d5e-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67d5e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="67d5e-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="67d5e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="67d5e-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67d5e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="67d5e-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="67d5e-118">Scenario description</span></span>
<span data-ttu-id="67d5e-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="67d5e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="67d5e-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67d5e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="67d5e-121">갤러리에서 ASC Contracts 추가</span><span class="sxs-lookup"><span data-stu-id="67d5e-121">Adding ASC Contracts from the gallery</span></span>
2. <span data-ttu-id="67d5e-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="67d5e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-asc-contracts-from-the-gallery"></a><span data-ttu-id="67d5e-123">갤러리에서 ASC Contracts 추가</span><span class="sxs-lookup"><span data-stu-id="67d5e-123">Adding ASC Contracts from the gallery</span></span>
<span data-ttu-id="67d5e-124">Azure AD에 ASC Contracts를 통합하도록 구성하려면 갤러리에서 관리되는 SaaS 앱 목록으로 ASC Contracts를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67d5e-124">To configure the integration of ASC Contracts into Azure AD, you need to add ASC Contracts from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="67d5e-125">**갤러리에서 ASC Contracts를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="67d5e-125">**To add ASC Contracts from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="67d5e-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="67d5e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="67d5e-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="67d5e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="67d5e-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="67d5e-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="67d5e-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="67d5e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="67d5e-133">검색 상자에서 **ASC Contracts**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="67d5e-133">In the search box, type **ASC Contracts**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_search.png)

5. <span data-ttu-id="67d5e-135">결과 창에서 **ASC Contracts**를 선택한 다음 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="67d5e-135">In the results panel, select **ASC Contracts**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="67d5e-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="67d5e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="67d5e-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 하여 ASC Contracts에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="67d5e-138">In this section, you configure and test Azure AD single sign-on with ASC Contracts based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="67d5e-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 ASC Contracts 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67d5e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ASC Contracts is to a user in Azure AD.</span></span> <span data-ttu-id="67d5e-140">즉 Azure AD 사용자와 ASC Contracts의 관련 사용자 간의 링크 관계가 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67d5e-140">In other words, a link relationship between an Azure AD user and the related user in ASC Contracts needs to be established.</span></span>

<span data-ttu-id="67d5e-141">이 링크 관계는 Azure AD의 **사용자 이름** 값을 ASC Contracts의 **Username** 값으로 할당하여 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="67d5e-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ASC Contracts.</span></span>

<span data-ttu-id="67d5e-142">ASC Contracts에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67d5e-142">To configure and test Azure AD single sign-on with ASC Contracts, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="67d5e-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="67d5e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="67d5e-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="67d5e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="67d5e-145">**[ASC Contracts 테스트 사용자 만들기](#creating-an-asc-contracts-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 ASC Contracts에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="67d5e-145">**[Creating an ASC Contracts test user](#creating-an-asc-contracts-test-user)** - to have a counterpart of Britta Simon in ASC Contracts that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="67d5e-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="67d5e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="67d5e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="67d5e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="67d5e-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="67d5e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="67d5e-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 ASC Contracts 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="67d5e-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ASC Contracts application.</span></span>

<span data-ttu-id="67d5e-150">**ASC Contracts에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="67d5e-150">**To configure Azure AD single sign-on with ASC Contracts, perform the following steps:**</span></span>

1. <span data-ttu-id="67d5e-151">Azure Portal의 **ASC Contracts** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="67d5e-151">In the Azure portal, on the **ASC Contracts** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="67d5e-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="67d5e-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_samlbase.png)

3. <span data-ttu-id="67d5e-155">**ASC Contracts 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="67d5e-155">On the **ASC Contracts Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_url.png)

    <span data-ttu-id="67d5e-157">a.</span><span class="sxs-lookup"><span data-stu-id="67d5e-157">a.</span></span> <span data-ttu-id="67d5e-158">**식별자** 텍스트 상자에서 `https://<subdomain>.asccontracts.com/shibboleth` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="67d5e-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.asccontracts.com/shibboleth`</span></span>

    <span data-ttu-id="67d5e-159">b.</span><span class="sxs-lookup"><span data-stu-id="67d5e-159">b.</span></span> <span data-ttu-id="67d5e-160">**회신 URL** 텍스트 상자에 다음 패턴으로 URL을 입력합니다.`https://<subdomain>.asccontracts.com/shibboleth.sso/login`</span><span class="sxs-lookup"><span data-stu-id="67d5e-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.asccontracts.com/shibboleth.sso/login`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="67d5e-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="67d5e-161">These values are not real.</span></span> <span data-ttu-id="67d5e-162">실제 식별자 및 회신 URL로 해당 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="67d5e-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="67d5e-163">이러한 값을 얻으려면 **613.599.6178**로 ASC(ASC Networks Inc.) 팀에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="67d5e-163">Contact ASC Networks Inc. (ASC) team at **613.599.6178** to get these values.</span></span>

4. <span data-ttu-id="67d5e-164">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 메타데이터 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="67d5e-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_certificate.png) 

5. <span data-ttu-id="67d5e-166">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="67d5e-166">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-asccontracts-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="67d5e-168">**ASC Contracts** 쪽에서 Single Sign-On을 구성하려면 **613.599.6178**로 ASC(ASC Networks Inc.) 지원을 호출하여 다운로드한 **메타데이터 XML**을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="67d5e-168">To configure single sign-on on **ASC Contracts** side, call ASC Networks Inc. (ASC) support at **613.599.6178** and provide them with the downloaded **Metadata XML**.</span></span> <span data-ttu-id="67d5e-169">그러면 이 응용 프로그램에서 SAML SSO 연결이 양쪽에 제대로 설정되도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="67d5e-169">They set this application up to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="67d5e-170">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67d5e-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="67d5e-171">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67d5e-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="67d5e-172">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67d5e-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="67d5e-173">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="67d5e-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="67d5e-174">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="67d5e-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="67d5e-176">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="67d5e-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="67d5e-177">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="67d5e-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-asccontracts-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="67d5e-179">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="67d5e-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-asccontracts-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="67d5e-181">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="67d5e-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-asccontracts-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="67d5e-183">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="67d5e-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-asccontracts-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="67d5e-185">a.</span><span class="sxs-lookup"><span data-stu-id="67d5e-185">a.</span></span> <span data-ttu-id="67d5e-186">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="67d5e-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="67d5e-187">b.</span><span class="sxs-lookup"><span data-stu-id="67d5e-187">b.</span></span> <span data-ttu-id="67d5e-188">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="67d5e-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="67d5e-189">c.</span><span class="sxs-lookup"><span data-stu-id="67d5e-189">c.</span></span> <span data-ttu-id="67d5e-190">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="67d5e-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="67d5e-191">d.</span><span class="sxs-lookup"><span data-stu-id="67d5e-191">d.</span></span> <span data-ttu-id="67d5e-192">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="67d5e-192">Click **Create**.</span></span>
 
### <a name="creating-an-asc-contracts-test-user"></a><span data-ttu-id="67d5e-193">ASC Contracts 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="67d5e-193">Creating an ASC Contracts test user</span></span>

<span data-ttu-id="67d5e-194">**613.599.6178**의 ASC(ASC Networks Inc.) 지원 팀과 협력하여 ASC Contracts 플랫폼에 추가된 사용자를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="67d5e-194">Work with ASC Networks Inc. (ASC) support team at **613.599.6178** to get the users added in the ASC Contracts platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="67d5e-195">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="67d5e-195">Assigning the Azure AD test user</span></span>

<span data-ttu-id="67d5e-196">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 ASC Contracts에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="67d5e-196">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ASC Contracts.</span></span>

![사용자 할당][200] 

<span data-ttu-id="67d5e-198">**Britta Simon을 ASC Contracts에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="67d5e-198">**To assign Britta Simon to ASC Contracts, perform the following steps:**</span></span>

1. <span data-ttu-id="67d5e-199">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="67d5e-199">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="67d5e-201">응용 프로그램 목록에서 **ASC Contracts**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="67d5e-201">In the applications list, select **ASC Contracts**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_app.png) 

3. <span data-ttu-id="67d5e-203">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="67d5e-203">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="67d5e-205">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="67d5e-205">Click **Add** button.</span></span> <span data-ttu-id="67d5e-206">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="67d5e-206">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="67d5e-208">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="67d5e-208">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="67d5e-209">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="67d5e-209">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="67d5e-210">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="67d5e-210">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="67d5e-211">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="67d5e-211">Testing single sign-on</span></span>

<span data-ttu-id="67d5e-212">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="67d5e-212">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="67d5e-213">[액세스 패널]에서 [ASC Contracts] 타일을 클릭하면 ASC Contracts 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="67d5e-213">When you click the ASC Contracts tile in the Access Panel, you should get automatically signed-on to your ASC Contracts application.</span></span> <span data-ttu-id="67d5e-214">액세스 패널에 대한 자세한 내용은</span><span class="sxs-lookup"><span data-stu-id="67d5e-214">For more information about the Access Panel, see.</span></span> <span data-ttu-id="67d5e-215">[Azure 시작](https://msdn.microsoft.com/library/dn308586)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="67d5e-215">[Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="67d5e-216">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="67d5e-216">Additional resources</span></span>

* [<span data-ttu-id="67d5e-217">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="67d5e-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="67d5e-218">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="67d5e-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_203.png

