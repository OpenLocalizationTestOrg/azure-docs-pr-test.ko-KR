---
title: "자습서: Abintegro와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory 및 Abintegro 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 99287e1f-4189-494a-97c8-e1c03d047fd3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: a2a3c1a7a338ee1cb35dd08176ad3bb5f3cdc319
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-abintegro"></a><span data-ttu-id="79ad0-103">자습서: Abintegro와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="79ad0-103">Tutorial: Azure Active Directory integration with Abintegro</span></span>

<span data-ttu-id="79ad0-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Abintegro를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="79ad0-104">In this tutorial, you learn how to integrate Abintegro with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="79ad0-105">Abintegro를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="79ad0-105">Integrating Abintegro with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="79ad0-106">Abintegro에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79ad0-106">You can control in Azure AD who has access to Abintegro</span></span>
- <span data-ttu-id="79ad0-107">사용자가 해당 Azure AD 계정으로 Abintegro에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79ad0-107">You can enable your users to automatically get signed-on to Abintegro (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="79ad0-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79ad0-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="79ad0-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="79ad0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="79ad0-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="79ad0-110">Prerequisites</span></span>

<span data-ttu-id="79ad0-111">Abintegro와의 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="79ad0-111">To configure Azure AD integration with Abintegro, you need the following items:</span></span>

- <span data-ttu-id="79ad0-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="79ad0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="79ad0-113">Abintegro Single Sign-on이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="79ad0-113">An Abintegro single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="79ad0-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="79ad0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="79ad0-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="79ad0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="79ad0-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="79ad0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="79ad0-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79ad0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="79ad0-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="79ad0-118">Scenario description</span></span>
<span data-ttu-id="79ad0-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="79ad0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="79ad0-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79ad0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="79ad0-121">갤러리에서 Abintegro 추가</span><span class="sxs-lookup"><span data-stu-id="79ad0-121">Adding Abintegro from the gallery</span></span>
2. <span data-ttu-id="79ad0-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="79ad0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-abintegro-from-the-gallery"></a><span data-ttu-id="79ad0-123">갤러리에서 Abintegro 추가</span><span class="sxs-lookup"><span data-stu-id="79ad0-123">Adding Abintegro from the gallery</span></span>
<span data-ttu-id="79ad0-124">Abintegro의 Azure AD 통합을 구성하려면 갤러리의 Abintegro를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="79ad0-124">To configure the integration of Abintegro into Azure AD, you need to add Abintegro from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="79ad0-125">**갤러리에서 Abintegro를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="79ad0-125">**To add Abintegro from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="79ad0-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="79ad0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="79ad0-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="79ad0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="79ad0-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="79ad0-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="79ad0-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="79ad0-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="79ad0-133">검색 상자에 **Abintegro**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="79ad0-133">In the search box, type **Abintegro**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-abintegro-tutorial/tutorial_abintegro_search.png)

5. <span data-ttu-id="79ad0-135">결과 패널에서 **Abintegro**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="79ad0-135">In the results panel, select **Abintegro**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-abintegro-tutorial/tutorial_abintegro_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="79ad0-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="79ad0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="79ad0-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Abintegro에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="79ad0-138">In this section, you configure and test Azure AD single sign-on with Abintegro based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="79ad0-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Abintegro 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="79ad0-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Abintegro is to a user in Azure AD.</span></span> <span data-ttu-id="79ad0-140">즉, Azure AD 사용자와 Abintegro의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="79ad0-140">In other words, a link relationship between an Azure AD user and the related user in Abintegro needs to be established.</span></span>

<span data-ttu-id="79ad0-141">Abintegro에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="79ad0-141">In Abintegro, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="79ad0-142">Abintegro에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="79ad0-142">To configure and test Azure AD single sign-on with Abintegro, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="79ad0-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="79ad0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="79ad0-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="79ad0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="79ad0-145">**[Abintegro 테스트 사용자 만들기](#creating-an-abintegro-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 Abintegro에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="79ad0-145">**[Creating an Abintegro test user](#creating-an-abintegro-test-user)** - to have a counterpart of Britta Simon in Abintegro that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="79ad0-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="79ad0-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="79ad0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="79ad0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="79ad0-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="79ad0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="79ad0-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Abintegro 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="79ad0-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Abintegro application.</span></span>

<span data-ttu-id="79ad0-150">**Abintegro에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="79ad0-150">**To configure Azure AD single sign-on with Abintegro, perform the following steps:**</span></span>

1. <span data-ttu-id="79ad0-151">Azure Portal의 **Abintegro** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="79ad0-151">In the Azure portal, on the **Abintegro** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="79ad0-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="79ad0-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-abintegro-tutorial/tutorial_abintegro_samlbase.png)

3. <span data-ttu-id="79ad0-155">**Abintegro 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="79ad0-155">On the **Abintegro Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-abintegro-tutorial/tutorial_abintegro_url.png)

    <span data-ttu-id="79ad0-157">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://dev.abintegro.com/Shibboleth.sso/Login?entityID=<Issuer>&target=https://dev.abintegro.com/secure/`</span><span class="sxs-lookup"><span data-stu-id="79ad0-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://dev.abintegro.com/Shibboleth.sso/Login?entityID=<Issuer>&target=https://dev.abintegro.com/secure/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="79ad0-158">이 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="79ad0-158">This value is not real.</span></span> <span data-ttu-id="79ad0-159">이 값을 실제 로그온 URL로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="79ad0-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="79ad0-160">이 값을 얻으려면 [Abintegro Client 지원 팀](mailto:support@abintegro.com)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="79ad0-160">Contact [Abintegro Client support team](mailto:support@abintegro.com) to get this value.</span></span> 
 
4. <span data-ttu-id="79ad0-161">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 메타데이터 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="79ad0-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-abintegro-tutorial/tutorial_abintegro_certificate.png) 

5. <span data-ttu-id="79ad0-163">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="79ad0-163">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-abintegro-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="79ad0-165">**Abintegro** 쪽에서 Single Sign-On을 구성하려면 다운로드한 **메타데이터 XML**을 [Abintegro 지원 팀](mailto:support@abintegro.com)에 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="79ad0-165">To configure single sign-on on **Abintegro** side, you need to send the downloaded **Metadata XML** to [Abintegro support team](mailto:support@abintegro.com).</span></span> <span data-ttu-id="79ad0-166">이렇게 설정하면 SAML SSO 연결이 양쪽에서 제대로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="79ad0-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="79ad0-167">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79ad0-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="79ad0-168">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="79ad0-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="79ad0-169">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79ad0-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="79ad0-170">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="79ad0-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="79ad0-171">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="79ad0-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="79ad0-173">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="79ad0-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="79ad0-174">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="79ad0-174">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-abintegro-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="79ad0-176">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="79ad0-176">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-abintegro-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="79ad0-178">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="79ad0-178">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-abintegro-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="79ad0-180">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="79ad0-180">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-abintegro-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="79ad0-182">a.</span><span class="sxs-lookup"><span data-stu-id="79ad0-182">a.</span></span> <span data-ttu-id="79ad0-183">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="79ad0-183">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="79ad0-184">b.</span><span class="sxs-lookup"><span data-stu-id="79ad0-184">b.</span></span> <span data-ttu-id="79ad0-185">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="79ad0-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="79ad0-186">c.</span><span class="sxs-lookup"><span data-stu-id="79ad0-186">c.</span></span> <span data-ttu-id="79ad0-187">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="79ad0-187">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="79ad0-188">d.</span><span class="sxs-lookup"><span data-stu-id="79ad0-188">d.</span></span> <span data-ttu-id="79ad0-189">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="79ad0-189">Click **Create**.</span></span>
 
### <a name="creating-an-abintegro-test-user"></a><span data-ttu-id="79ad0-190">Abintegro 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="79ad0-190">Creating an Abintegro test user</span></span>

<span data-ttu-id="79ad0-191">Abintegro를 프로비전하는 사용자를 구성할 작업 항목이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="79ad0-191">There is no action item for you to configure user provisioning to Abintegro.</span></span> <span data-ttu-id="79ad0-192">할당된 사용자가 액세스 패널을 사용하여 Abintegro에 로그인하려는 경우 Abintegro는 사용자가 존재하는지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="79ad0-192">When an assigned user tries to log into Abintegro using the access panel, Abintegro checks whether the user exists.</span></span>
  
<span data-ttu-id="79ad0-193">사용할 수 있는 사용자 계정이 없으면 자동으로 Abintegro에 의해 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="79ad0-193">If there is no user account available yet, it is automatically created by Abintegro.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="79ad0-194">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="79ad0-194">Assigning the Azure AD test user</span></span>

<span data-ttu-id="79ad0-195">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Abintegro에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="79ad0-195">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Abintegro.</span></span>

![사용자 할당][200] 

<span data-ttu-id="79ad0-197">**Britta Simon을 Abintegro에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="79ad0-197">**To assign Britta Simon to Abintegro, perform the following steps:**</span></span>

1. <span data-ttu-id="79ad0-198">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="79ad0-198">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="79ad0-200">응용 프로그램 목록에서 **Abintegro**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="79ad0-200">In the applications list, select **Abintegro**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-abintegro-tutorial/tutorial_abintegro_app.png) 

3. <span data-ttu-id="79ad0-202">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="79ad0-202">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="79ad0-204">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="79ad0-204">Click **Add** button.</span></span> <span data-ttu-id="79ad0-205">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="79ad0-205">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="79ad0-207">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="79ad0-207">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="79ad0-208">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="79ad0-208">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="79ad0-209">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="79ad0-209">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="79ad0-210">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="79ad0-210">Testing single sign-on</span></span>

<span data-ttu-id="79ad0-211">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="79ad0-211">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="79ad0-212">액세스 패널에서 Abintegro 타일을 클릭할 때 Abintegro 응용 프로그램의 로그인 페이지를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="79ad0-212">When you click the Abintegro tile in the Access Panel, you should get login page of Abintegro application.</span></span>
<span data-ttu-id="79ad0-213">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="79ad0-213">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="79ad0-214">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="79ad0-214">Additional resources</span></span>

* [<span data-ttu-id="79ad0-215">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="79ad0-215">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="79ad0-216">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="79ad0-216">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_203.png

