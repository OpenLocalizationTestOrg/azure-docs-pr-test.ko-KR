---
title: "자습서: Springer Link와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 Springer Link 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 58cdf029-bdc0-43c4-a469-b921c2a669bd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: jeedes
ms.openlocfilehash: b9aec6f8f293cdd31456a7f50e3efe792804c7c8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-springer-link"></a><span data-ttu-id="4680c-103">자습서: Springer Link와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="4680c-103">Tutorial: Azure Active Directory integration with Springer Link</span></span>

<span data-ttu-id="4680c-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Springer Link를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4680c-104">In this tutorial, you learn how to integrate Springer Link with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4680c-105">Springer Link를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="4680c-105">Integrating Springer Link with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4680c-106">Springer Link에 액세스할 수 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4680c-106">You can control in Azure AD who has access to Springer Link.</span></span>
- <span data-ttu-id="4680c-107">사용자가 Azure AD 계정으로 Springer Link에 자동으로 로그인(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4680c-107">You can enable your users to automatically get signed-on to Springer Link (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="4680c-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4680c-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="4680c-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4680c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4680c-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="4680c-110">Prerequisites</span></span>

<span data-ttu-id="4680c-111">Springer Link와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4680c-111">To configure Azure AD integration with Springer Link, you need the following items:</span></span>

- <span data-ttu-id="4680c-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="4680c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4680c-113">Springer Link Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="4680c-113">A Springer Link single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4680c-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4680c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4680c-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4680c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4680c-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="4680c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4680c-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4680c-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4680c-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="4680c-118">Scenario description</span></span>
<span data-ttu-id="4680c-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="4680c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4680c-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4680c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4680c-121">갤러리에서 Springer Link 추가</span><span class="sxs-lookup"><span data-stu-id="4680c-121">Adding Springer Link from the gallery</span></span>
2. <span data-ttu-id="4680c-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="4680c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-springer-link-from-the-gallery"></a><span data-ttu-id="4680c-123">갤러리에서 Springer Link 추가</span><span class="sxs-lookup"><span data-stu-id="4680c-123">Adding Springer Link from the gallery</span></span>
<span data-ttu-id="4680c-124">Springer Link가 Azure AD에 통합되도록 구성하려면 갤러리의 Springer Link를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4680c-124">To configure the integration of Springer Link into Azure AD, you need to add Springer Link from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4680c-125">**갤러리에서 Springer Link를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="4680c-125">**To add Springer Link from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4680c-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4680c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory 단추][1]

2. <span data-ttu-id="4680c-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="4680c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4680c-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="4680c-129">Then go to **All applications**.</span></span>

    ![엔터프라이즈 응용 프로그램 블레이드][2]
    
3. <span data-ttu-id="4680c-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4680c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![새 응용 프로그램 단추][3]

4. <span data-ttu-id="4680c-133">검색 상자에 **Springer Link** 를 입력하고 결과 패널에서 **Springer Link** 를 선택한 후 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4680c-133">In the search box, type **Springer Link**, select **Springer Link** from result panel then click **Add** button to add the application.</span></span>

    ![결과 목록의 Springer Link](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="4680c-135">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="4680c-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="4680c-136">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 사용하여 Springer Link에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="4680c-136">In this section, you configure and test Azure AD single sign-on with Springer Link based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4680c-137">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Springer Link 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4680c-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Springer Link is to a user in Azure AD.</span></span> <span data-ttu-id="4680c-138">즉, Azure AD 사용자와 Springer Link의 관련 사용자 간에 연결 관계를 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4680c-138">In other words, a link relationship between an Azure AD user and the related user in Springer Link needs to be established.</span></span>

<span data-ttu-id="4680c-139">Springer Link에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 연결 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4680c-139">In Springer Link, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="4680c-140">Springer Link에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4680c-140">To configure and test Azure AD single sign-on with Springer Link, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4680c-141">**[Azure AD Single Sign-On 구성](#configure-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="4680c-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="4680c-142">**[Azure AD 테스트 사용자 만들기](#create-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4680c-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4680c-143">**[Azure AD 테스트 사용자 할당](#assign-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="4680c-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
4. <span data-ttu-id="4680c-144">**[Single Sign-On 테스트](#test-single-sign-on)** - 구성이 작동하는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4680c-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="4680c-145">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="4680c-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="4680c-146">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Springer Link 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="4680c-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Springer Link application.</span></span>

<span data-ttu-id="4680c-147">**Springer Link에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="4680c-147">**To configure Azure AD single sign-on with Springer Link, perform the following steps:**</span></span>

1. <span data-ttu-id="4680c-148">Azure Portal의 **Springer Link** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4680c-148">In the Azure portal, on the **Springer Link** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-On 구성 링크][4]

2. <span data-ttu-id="4680c-150">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4680c-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_samlbase.png)

3. <span data-ttu-id="4680c-152">**Springer Link 도메인 및 URL** 섹션에서 **IDP** 시작 모드로 응용 프로그램을 구성하려는 경우 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4680c-152">On the **Springer Link Domain and URLs** section,  If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Springer Link 도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_url1.png)

    <span data-ttu-id="4680c-154">a.</span><span class="sxs-lookup"><span data-stu-id="4680c-154">a.</span></span> <span data-ttu-id="4680c-155">**식별자** 텍스트 상자에 URL `https://fsso.springer.com`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4680c-155">In the **Identifier** textbox, type the URL: `https://fsso.springer.com`</span></span>

    <span data-ttu-id="4680c-156">b.</span><span class="sxs-lookup"><span data-stu-id="4680c-156">b.</span></span> <span data-ttu-id="4680c-157">**회신 URL** 텍스트 상자에 URL `https://fsso-qa1.springer.com/federation/Consumer/metaAlias/SpringerServiceProvider`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4680c-157">In the **Reply URL** textbox, type the URL: `https://fsso-qa1.springer.com/federation/Consumer/metaAlias/SpringerServiceProvider`</span></span>    

4. <span data-ttu-id="4680c-158">**고급 URL 설정 표시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4680c-158">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="4680c-159">**SP** 시작 모드에서 응용 프로그램을 구성하려면:</span><span class="sxs-lookup"><span data-stu-id="4680c-159">If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Springer Link 도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_url.png)

    <span data-ttu-id="4680c-161">**로그온 URL** 텍스트 상자에 URL `https://fsso.springer.com/federation/Consumer/metaAlias/SpringerServiceProvider`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4680c-161">In the **Sign-on URL** textbox, type the URL : `https://fsso.springer.com/federation/Consumer/metaAlias/SpringerServiceProvider`</span></span>    

5. <span data-ttu-id="4680c-162">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4680c-162">Click **Save** button.</span></span>

    ![Single Sign-On 구성 저장 단추](./media/active-directory-saas-springerlink-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4680c-164">**메타데이터** URL을 생성하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4680c-164">To generate the **Metadata** url, perform the following steps:</span></span>

    <span data-ttu-id="4680c-165">a.</span><span class="sxs-lookup"><span data-stu-id="4680c-165">a.</span></span> <span data-ttu-id="4680c-166">**앱 등록**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4680c-166">Click **App registrations**.</span></span>
    
    ![Single Sign-on 구성](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_appregistrations.png)
   
    <span data-ttu-id="4680c-168">b.</span><span class="sxs-lookup"><span data-stu-id="4680c-168">b.</span></span> <span data-ttu-id="4680c-169">**끝점**을 클릭하여 **끝점** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4680c-169">Click **Endpoints** to open **Endpoints** dialog box.</span></span>  
    
    ![Single Sign-on 구성](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_endpointicon.png)

    <span data-ttu-id="4680c-171">c.</span><span class="sxs-lookup"><span data-stu-id="4680c-171">c.</span></span> <span data-ttu-id="4680c-172">복사 단추를 클릭하여 **페더레이션 메타데이터 문서** URL을 복사하여 메모장에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="4680c-172">Click the copy button to copy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Single Sign-on 구성](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_endpoint.png)
     
    <span data-ttu-id="4680c-174">d.</span><span class="sxs-lookup"><span data-stu-id="4680c-174">d.</span></span> <span data-ttu-id="4680c-175">이제 **Springer Link**의 속성 페이지로 이동하고 **복사** 단추를 사용하여 **응용 프로그램 ID**를 복사하여 메모장에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="4680c-175">Now go to the property page of **Springer Link** and copy the **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_appid.png)

    <span data-ttu-id="4680c-177">e.</span><span class="sxs-lookup"><span data-stu-id="4680c-177">e.</span></span> <span data-ttu-id="4680c-178">`<FEDERATION METADATA DOCUMENT url>?appid=<application id>` 패턴을 사용하여 **메타데이터 URL**을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="4680c-178">Generate the **Metadata URL** using the following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>

7. <span data-ttu-id="4680c-179">**Application Id** 쪽에서 Single Sign-On을 구성하려면 생성된 **메타데이터 URL**을 [Springer Link 지원 팀](mailto:identity@springernature.com)에 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4680c-179">To configure single sign-on on **Springer Link** side, you need to send the generated **Metadata URL** to [Springer Link support team](mailto:identity@springernature.com).</span></span>

> [!TIP]
> <span data-ttu-id="4680c-180">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4680c-180">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="4680c-181">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4680c-181">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="4680c-182">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4680c-182">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="4680c-183">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="4680c-183">Create an Azure AD test user</span></span>

<span data-ttu-id="4680c-184">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4680c-184">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Azure AD 테스트 사용자 만들기][100]

<span data-ttu-id="4680c-186">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="4680c-186">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4680c-187">Azure Portal의 왼쪽 창에서 **Azure Active Directory** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4680c-187">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Azure Active Directory 단추](./media/active-directory-saas-springerlink-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="4680c-189">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4680c-189">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !["사용자 및 그룹" 및 "모든 사용자" 링크](./media/active-directory-saas-springerlink-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="4680c-191">**사용자** 대화 상자를 열려면 **모든 사용자** 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4680c-191">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![추가 단추](./media/active-directory-saas-springerlink-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="4680c-193">**사용자** 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4680c-193">In the **User** dialog box, perform the following steps:</span></span>

    ![사용자 대화 상자](./media/active-directory-saas-springerlink-tutorial/create_aaduser_04.png)

    <span data-ttu-id="4680c-195">a.</span><span class="sxs-lookup"><span data-stu-id="4680c-195">a.</span></span> <span data-ttu-id="4680c-196">**이름** 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4680c-196">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4680c-197">b.</span><span class="sxs-lookup"><span data-stu-id="4680c-197">b.</span></span> <span data-ttu-id="4680c-198">**사용자 이름** 상자에 사용자인 Britta Simon의 전자 메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4680c-198">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="4680c-199">c.</span><span class="sxs-lookup"><span data-stu-id="4680c-199">c.</span></span> <span data-ttu-id="4680c-200">**암호 표시** 확인란을 선택한 다음 **암호** 상자에 표시된 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="4680c-200">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="4680c-201">d.</span><span class="sxs-lookup"><span data-stu-id="4680c-201">d.</span></span> <span data-ttu-id="4680c-202">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4680c-202">Click **Create**.</span></span>
 
### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="4680c-203">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="4680c-203">Assign the Azure AD test user</span></span>

<span data-ttu-id="4680c-204">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Springer Link에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="4680c-204">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Springer Link.</span></span>

![사용자 역할 할당][200] 

<span data-ttu-id="4680c-206">**Britta Simon을 Springer Link에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="4680c-206">**To assign Britta Simon to Springer Link, perform the following steps:**</span></span>

1. <span data-ttu-id="4680c-207">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4680c-207">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="4680c-209">응용 프로그램 목록에서 **Springer Link**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4680c-209">In the applications list, select **Springer Link**.</span></span>

    ![응용 프로그램 목록의 Springer Link 링크](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_app.png)  

3. <span data-ttu-id="4680c-211">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4680c-211">In the menu on the left, click **Users and groups**.</span></span>

    !["사용자 및 그룹" 링크][202]

4. <span data-ttu-id="4680c-213">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4680c-213">Click **Add** button.</span></span> <span data-ttu-id="4680c-214">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4680c-214">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![할당 추가 창][203]

5. <span data-ttu-id="4680c-216">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4680c-216">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="4680c-217">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4680c-217">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4680c-218">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4680c-218">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="4680c-219">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="4680c-219">Test single sign-on</span></span>

<span data-ttu-id="4680c-220">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="4680c-220">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="4680c-221">액세스 패널에서 Springer Link 타일을 클릭하면 Springer Link 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="4680c-221">When you click the Springer Link tile in the Access Panel, you should get automatically signed-on to your Springer Link application.</span></span>
<span data-ttu-id="4680c-222">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4680c-222">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4680c-223">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="4680c-223">Additional resources</span></span>

* [<span data-ttu-id="4680c-224">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="4680c-224">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4680c-225">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="4680c-225">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_203.png

