---
title: "자습서: Fuse와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 Fuse 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 5ef34f58-863a-4b37-875c-e8efa3e18bb3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 9a91e22faced9e126043bebefd85c307dbdf933d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-fuse"></a><span data-ttu-id="23f33-103">자습서: Fuse와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="23f33-103">Tutorial: Azure Active Directory integration with Fuse</span></span>

<span data-ttu-id="23f33-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Fuse를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="23f33-104">In this tutorial, you learn how to integrate Fuse with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="23f33-105">Fuse를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="23f33-105">Integrating Fuse with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="23f33-106">Fuse에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23f33-106">You can control in Azure AD who has access to Fuse.</span></span>
- <span data-ttu-id="23f33-107">사용자가 해당 Azure AD 계정으로 Fuse에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23f33-107">You can enable your users to automatically get signed-on to Fuse (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="23f33-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23f33-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="23f33-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="23f33-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="23f33-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="23f33-110">Prerequisites</span></span>

<span data-ttu-id="23f33-111">Fuse와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="23f33-111">To configure Azure AD integration with Fuse, you need the following items:</span></span>

- <span data-ttu-id="23f33-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="23f33-112">An Azure AD subscription</span></span>
- <span data-ttu-id="23f33-113">Fuse Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="23f33-113">A Fuse single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="23f33-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="23f33-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="23f33-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="23f33-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="23f33-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="23f33-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="23f33-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23f33-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="23f33-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="23f33-118">Scenario description</span></span>
<span data-ttu-id="23f33-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="23f33-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="23f33-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23f33-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="23f33-121">갤러리에서 Fuse 추가</span><span class="sxs-lookup"><span data-stu-id="23f33-121">Add Fuse from the gallery</span></span>
2. <span data-ttu-id="23f33-122">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="23f33-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-fuse-from-the-gallery"></a><span data-ttu-id="23f33-123">갤러리에서 Fuse 추가</span><span class="sxs-lookup"><span data-stu-id="23f33-123">Add Fuse from the gallery</span></span>
<span data-ttu-id="23f33-124">Fuse의 Azure AD 통합을 구성하려면 갤러리의 Fuse를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="23f33-124">To configure the integration of Fuse into Azure AD, you need to add Fuse from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="23f33-125">**갤러리에서 Fuse를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="23f33-125">**To add Fuse from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="23f33-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="23f33-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory 단추][1]

2. <span data-ttu-id="23f33-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="23f33-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="23f33-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="23f33-129">Then go to **All applications**.</span></span>

    ![엔터프라이즈 응용 프로그램 블레이드][2]
    
3. <span data-ttu-id="23f33-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="23f33-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![새 응용 프로그램 단추][3]

4. <span data-ttu-id="23f33-133">검색 상자에 **Fuse**를 입력하고 결과 패널에서 **Fuse**를 선택한 후 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="23f33-133">In the search box, type **Fuse**, select **Fuse** from result panel then click **Add** button to add the application.</span></span>

    ![결과 목록의 Fuse](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="23f33-135">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="23f33-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="23f33-136">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Fuse에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="23f33-136">In this section, you configure and test Azure AD single sign-on with Fuse based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="23f33-137">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Fuse 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="23f33-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Fuse is to a user in Azure AD.</span></span> <span data-ttu-id="23f33-138">즉, Azure AD 사용자와 Fuse의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="23f33-138">In other words, a link relationship between an Azure AD user and the related user in Fuse needs to be established.</span></span>

<span data-ttu-id="23f33-139">Fuse에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="23f33-139">In Fuse, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="23f33-140">Fuse에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="23f33-140">To configure and test Azure AD single sign-on with Fuse, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="23f33-141">**[Azure AD Single Sign-On 구성](#configure-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="23f33-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="23f33-142">**[Azure AD 테스트 사용자 만들기](#create-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="23f33-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="23f33-143">**[Fuse 테스트 사용자 만들기](#create-a-fuse-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 Fuse에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="23f33-143">**[Create a Fuse test user](#create-a-fuse-test-user)** - to have a counterpart of Britta Simon in Fuse that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="23f33-144">**[Azure AD 테스트 사용자 할당](#assign-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="23f33-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="23f33-145">**[Single Sign-On 테스트](#test-single-sign-on)** - 구성이 작동하는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="23f33-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="23f33-146">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="23f33-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="23f33-147">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Fuse 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="23f33-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Fuse application.</span></span>

<span data-ttu-id="23f33-148">**Fuse에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="23f33-148">**To configure Azure AD single sign-on with Fuse, perform the following steps:**</span></span>

1. <span data-ttu-id="23f33-149">Azure Portal의 **Fuse** 응용 프로그램 통합 페이지에서 **Single sign-on**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="23f33-149">In the Azure portal, on the **Fuse** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-On 구성 링크][4]

2. <span data-ttu-id="23f33-151">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="23f33-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_samlbase.png)

3. <span data-ttu-id="23f33-153">**Fuse 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="23f33-153">On the **Fuse Domain and URLs** section, perform the following steps:</span></span>

    ![Fuse 도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_url.png)
    
    <span data-ttu-id="23f33-155">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<tenant name>.fusion-universal.com/`</span><span class="sxs-lookup"><span data-stu-id="23f33-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant name>.fusion-universal.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="23f33-156">이 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="23f33-156">This value is not real.</span></span> <span data-ttu-id="23f33-157">이 값을 실제 로그온 URL로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="23f33-157">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="23f33-158">이 값을 얻으려면 [Fuse 클라이언트 지원 팀](mailto:support@fusion-universal.com)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="23f33-158">Contact [Fuse Client support team](mailto:support@fusion-universal.com) to get this value.</span></span> 
 
4. <span data-ttu-id="23f33-159">**SAML 서명 인증서** 섹션에서 **인증서(원시)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="23f33-159">On the **SAML Signing Certificate** section, click **Certificate (Raw)** and then save the certificate file on your computer.</span></span>

    ![인증서 다운로드 링크](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_certificate.png) 

5. <span data-ttu-id="23f33-161">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="23f33-161">Click **Save** button.</span></span>

    ![Single Sign-On 구성 저장 단추](./media/active-directory-saas-fuse-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="23f33-163">**Fuse 구성** 섹션에서 **Fuse 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="23f33-163">On the **Fuse Configuration** section, click **Configure Fuse** to open **Configure sign-on** window.</span></span> <span data-ttu-id="23f33-164">**빠른 참조 섹션**에서 **로그아웃 URL, SAML 엔터티 ID 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="23f33-164">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Fuse 구성](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_configure.png) 

7. <span data-ttu-id="23f33-166">응용 프로그램에 대해 구성된 SSO를 얻으려면 [Fuse 지원 팀](mailto:support@fusion-universal.com)에 문의하고 다음을 제공하세요.</span><span class="sxs-lookup"><span data-stu-id="23f33-166">To get SSO configured for your application, contact [Fuse support team](mailto:support@fusion-universal.com) and provide them with the following:</span></span>

    * <span data-ttu-id="23f33-167">다운로드한 **인증서(원시) 파일**</span><span class="sxs-lookup"><span data-stu-id="23f33-167">The downloaded **Certificate (Raw) file**</span></span>
    * <span data-ttu-id="23f33-168">**SAML Single Sign-On 서비스 URL**</span><span class="sxs-lookup"><span data-stu-id="23f33-168">The **SAML Single Sign-On Service URL**</span></span>
    * <span data-ttu-id="23f33-169">**SAML 엔터티 ID**</span><span class="sxs-lookup"><span data-stu-id="23f33-169">The **SAML Entity ID**</span></span>
    * <span data-ttu-id="23f33-170">**로그아웃 URL**</span><span class="sxs-lookup"><span data-stu-id="23f33-170">The **Sign-Out URL**</span></span>

> [!TIP]
> <span data-ttu-id="23f33-171">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23f33-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="23f33-172">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="23f33-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="23f33-173">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23f33-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="23f33-174">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="23f33-174">Create an Azure AD test user</span></span>

<span data-ttu-id="23f33-175">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="23f33-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Azure AD 테스트 사용자 만들기][100]

<span data-ttu-id="23f33-177">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="23f33-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="23f33-178">Azure Portal의 왼쪽 창에서 **Azure Active Directory** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="23f33-178">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Azure Active Directory 단추](./media/active-directory-saas-fuse-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="23f33-180">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="23f33-180">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !["사용자 및 그룹" 및 "모든 사용자" 링크](./media/active-directory-saas-fuse-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="23f33-182">**사용자** 대화 상자를 열려면 **모든 사용자** 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="23f33-182">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![추가 단추](./media/active-directory-saas-fuse-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="23f33-184">**사용자** 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="23f33-184">In the **User** dialog box, perform the following steps:</span></span>

    ![사용자 대화 상자](./media/active-directory-saas-fuse-tutorial/create_aaduser_04.png)

    <span data-ttu-id="23f33-186">a.</span><span class="sxs-lookup"><span data-stu-id="23f33-186">a.</span></span> <span data-ttu-id="23f33-187">**이름** 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="23f33-187">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="23f33-188">b.</span><span class="sxs-lookup"><span data-stu-id="23f33-188">b.</span></span> <span data-ttu-id="23f33-189">**사용자 이름** 상자에 사용자인 Britta Simon의 전자 메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="23f33-189">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="23f33-190">c.</span><span class="sxs-lookup"><span data-stu-id="23f33-190">c.</span></span> <span data-ttu-id="23f33-191">**암호 표시** 확인란을 선택한 다음 **암호** 상자에 표시된 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="23f33-191">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="23f33-192">d.</span><span class="sxs-lookup"><span data-stu-id="23f33-192">d.</span></span> <span data-ttu-id="23f33-193">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="23f33-193">Click **Create**.</span></span>
 
### <a name="create-a-fuse-test-user"></a><span data-ttu-id="23f33-194">Fuse 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="23f33-194">Create a Fuse test user</span></span>

<span data-ttu-id="23f33-195">이 섹션에서는 Fuse에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="23f33-195">In this section, you create a user called Britta Simon in Fuse.</span></span> <span data-ttu-id="23f33-196">Fuse 플랫폼에서 사용자를 추가하려면 [Fuse 지원 팀](mailto:support@fusion-universal.com)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="23f33-196">Please work with [Fuse support team](mailto:support@fusion-universal.com) to add the users in the Fuse platform.</span></span>


### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="23f33-197">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="23f33-197">Assign the Azure AD test user</span></span>

<span data-ttu-id="23f33-198">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Fuse에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="23f33-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Fuse.</span></span>

![사용자 역할 할당][200] 

<span data-ttu-id="23f33-200">**Britta Simon을 Fuse에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="23f33-200">**To assign Britta Simon to Fuse, perform the following steps:**</span></span>

1. <span data-ttu-id="23f33-201">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="23f33-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="23f33-203">응용 프로그램 목록에서 **Fuse**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="23f33-203">In the applications list, select **Fuse**.</span></span>

    ![응용 프로그램 목록의 Fuse 링크](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_app.png)  

3. <span data-ttu-id="23f33-205">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="23f33-205">In the menu on the left, click **Users and groups**.</span></span>

    !["사용자 및 그룹" 링크][202]

4. <span data-ttu-id="23f33-207">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="23f33-207">Click **Add** button.</span></span> <span data-ttu-id="23f33-208">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="23f33-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![할당 추가 창][203]

5. <span data-ttu-id="23f33-210">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="23f33-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="23f33-211">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="23f33-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="23f33-212">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="23f33-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="23f33-213">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="23f33-213">Test single sign-on</span></span>

<span data-ttu-id="23f33-214">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="23f33-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="23f33-215">액세스 패널에서 Fuse 타일을 클릭하면 Fuse 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="23f33-215">When you click the Fuse tile in the Access Panel, you should get automatically signed-on to your Fuse application.</span></span>
<span data-ttu-id="23f33-216">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="23f33-216">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="23f33-217">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="23f33-217">Additional resources</span></span>

* [<span data-ttu-id="23f33-218">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="23f33-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="23f33-219">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="23f33-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_203.png

