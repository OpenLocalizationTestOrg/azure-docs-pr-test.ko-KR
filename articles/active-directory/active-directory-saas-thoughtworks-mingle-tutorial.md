---
title: "자습서: Thoughtworks Mingle과 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 Thoughtworks Mingle 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 69d859d9-b7f7-4c42-bc8c-8036138be586
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 268ae5affb88a718f68c08daa94fe7aba4a99c11
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-thoughtworks-mingle"></a><span data-ttu-id="1c257-103">자습서: Thoughtworks Mingle과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="1c257-103">Tutorial: Azure Active Directory integration with Thoughtworks Mingle</span></span>

<span data-ttu-id="1c257-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Thoughtworks Mingle을 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-104">In this tutorial, you learn how to integrate Thoughtworks Mingle with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1c257-105">Thoughtworks Mingle을 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-105">Integrating Thoughtworks Mingle with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1c257-106">Thoughtworks Mingle에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-106">You can control in Azure AD who has access to Thoughtworks Mingle</span></span>
- <span data-ttu-id="1c257-107">사용자가 해당 Azure AD 계정으로 Thoughtworks Mingle에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-107">You can enable your users to automatically get signed-on to Thoughtworks Mingle (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1c257-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1c257-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1c257-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1c257-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="1c257-110">Prerequisites</span></span>

<span data-ttu-id="1c257-111">Thoughtworks Mingle과 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-111">To configure Azure AD integration with Thoughtworks Mingle, you need the following items:</span></span>

- <span data-ttu-id="1c257-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="1c257-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1c257-113">Thoughtworks Mingle Single Sign-on이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="1c257-113">A Thoughtworks Mingle single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1c257-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1c257-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1c257-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="1c257-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1c257-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1c257-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="1c257-118">Scenario description</span></span>
<span data-ttu-id="1c257-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1c257-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1c257-121">갤러리에서 Thoughtworks Mingle 추가</span><span class="sxs-lookup"><span data-stu-id="1c257-121">Adding Thoughtworks Mingle from the gallery</span></span>
2. <span data-ttu-id="1c257-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="1c257-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-thoughtworks-mingle-from-the-gallery"></a><span data-ttu-id="1c257-123">갤러리에서 Thoughtworks Mingle 추가</span><span class="sxs-lookup"><span data-stu-id="1c257-123">Adding Thoughtworks Mingle from the gallery</span></span>
<span data-ttu-id="1c257-124">Thoughtworks Mingle의 Azure AD 통합을 구성하려면 갤러리의 Thoughtworks Mingle을 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-124">To configure the integration of Thoughtworks Mingle into Azure AD, you need to add Thoughtworks Mingle from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1c257-125">**갤러리에서 Thoughtworks Mingle을 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="1c257-125">**To add Thoughtworks Mingle from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1c257-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory 단추][1]

2. <span data-ttu-id="1c257-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1c257-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-129">Then go to **All applications**.</span></span>

    ![엔터프라이즈 응용 프로그램 블레이드][2]
    
3. <span data-ttu-id="1c257-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![새 응용 프로그램 단추][3]

4. <span data-ttu-id="1c257-133">검색 상자에 **Thoughtworks Mingle**을 입력하고 결과 패널에서 **Thoughtworks Mingle**을 선택한 후 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-133">In the search box, type **Thoughtworks Mingle**, select **Thoughtworks Mingle** from result panel then click **Add** button to add the application.</span></span>

    ![결과 목록의 Thoughtworks Mingle](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="1c257-135">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="1c257-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="1c257-136">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Thoughtworks Mingle에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-136">In this section, you configure and test Azure AD single sign-on with Thoughtworks Mingle based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1c257-137">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Thoughtworks Mingle 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Thoughtworks Mingle is to a user in Azure AD.</span></span> <span data-ttu-id="1c257-138">즉, Azure AD 사용자와 Thoughtworks Mingle의 관련 사용자 간에 연결 관계가 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-138">In other words, a link relationship between an Azure AD user and the related user in Thoughtworks Mingle needs to be established.</span></span>

<span data-ttu-id="1c257-139">Thoughtworks Mingle에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 연결 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-139">In Thoughtworks Mingle, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="1c257-140">Thoughtworks Mingle에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-140">To configure and test Azure AD single sign-on with Thoughtworks Mingle, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1c257-141">**[Azure AD Single Sign-On 구성](#configure-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1c257-142">**[Azure AD 테스트 사용자 만들기](#create-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1c257-143">**[Thoughtworks Mingle 테스트 사용자 만들기](#create-a-thoughtworks-mingle-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 Thoughtworks Mingle에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-143">**[Create a Thoughtworks Mingle test user](#create-a-thoughtworks-mingle-test-user)** - to have a counterpart of Britta Simon in Thoughtworks Mingle that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1c257-144">**[Azure AD 테스트 사용자 할당](#assign-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1c257-145">**[Single Sign-on 테스트](#test-single-sign-on)** - 구성이 작동하는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="1c257-146">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="1c257-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="1c257-147">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Thoughtworks Mingle 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Thoughtworks Mingle application.</span></span>

<span data-ttu-id="1c257-148">**Thoughtworks Mingle에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="1c257-148">**To configure Azure AD single sign-on with Thoughtworks Mingle, perform the following steps:**</span></span>

1. <span data-ttu-id="1c257-149">Azure Portal의 **Thoughtworks Mingle** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-149">In the Azure portal, on the **Thoughtworks Mingle** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="1c257-151">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_samlbase.png)

3. <span data-ttu-id="1c257-153">**Thoughtworks Mingle 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-153">On the **Thoughtworks Mingle Domain and URLs** section, perform the following steps:</span></span>

    ![Thoughtworks Mingle 도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_url.png)

    <span data-ttu-id="1c257-155">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<companyname>.mingle.thoughtworks.com`</span><span class="sxs-lookup"><span data-stu-id="1c257-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.mingle.thoughtworks.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1c257-156">이 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-156">The value is not real.</span></span> <span data-ttu-id="1c257-157">이 값을 실제 로그온 URL로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-157">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="1c257-158">값을 얻으려면 [Thoughtworks Mingle 클라이언트 지원 팀](https://support.thoughtworks.com/hc/categories/201743486-Mingle-Community-Support)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="1c257-158">Contact [Thoughtworks Mingle Client support team](https://support.thoughtworks.com/hc/categories/201743486-Mingle-Community-Support) to get the value.</span></span> 
 
4. <span data-ttu-id="1c257-159">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 메타데이터 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-159">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![인증서 다운로드 링크](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_certificate.png) 

5. <span data-ttu-id="1c257-161">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-161">Click **Save** button.</span></span>

    ![Single Sign-On 구성 저장 단추](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1c257-163">**Thoughtworks Mingle** 회사 사이트에 관리자 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-163">Log in to your **Thoughtworks Mingle** company site as administrator.</span></span>

7. <span data-ttu-id="1c257-164">**관리자** 탭을 클릭하고 **SSO 구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-164">Click the **Admin** tab, and then, click **SSO Config**.</span></span>
   
    <span data-ttu-id="1c257-165">![관리 탭](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785157.png "SSO 구성")</span><span class="sxs-lookup"><span data-stu-id="1c257-165">![Admin tab](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785157.png "SSO Config")</span></span>

8. <span data-ttu-id="1c257-166">**SSO 구성** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-166">In the **SSO Config** section, perform the following steps:</span></span>
   
    <span data-ttu-id="1c257-167">![SSO 구성](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785158.png "SSO 구성")</span><span class="sxs-lookup"><span data-stu-id="1c257-167">![SSO Config](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785158.png "SSO Config")</span></span>
    
    <span data-ttu-id="1c257-168">a.</span><span class="sxs-lookup"><span data-stu-id="1c257-168">a.</span></span> <span data-ttu-id="1c257-169">메타데이터 파일을 업로드하려면 **파일 선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-169">To upload the metadata file, click **Choose file**.</span></span> 

    <span data-ttu-id="1c257-170">b.</span><span class="sxs-lookup"><span data-stu-id="1c257-170">b.</span></span> <span data-ttu-id="1c257-171">**변경 내용 저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-171">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="1c257-172">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1c257-173">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1c257-174">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="1c257-175">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="1c257-175">Create an Azure AD test user</span></span>
<span data-ttu-id="1c257-176">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 테스트 사용자 만들기][100]

<span data-ttu-id="1c257-178">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="1c257-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1c257-179">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure Active Directory 단추](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1c257-181">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    !["사용자 및 그룹" 및 "모든 사용자" 링크](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1c257-183">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![추가 단추](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1c257-185">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![사용자 대화 상자](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1c257-187">a.</span><span class="sxs-lookup"><span data-stu-id="1c257-187">a.</span></span> <span data-ttu-id="1c257-188">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1c257-189">b.</span><span class="sxs-lookup"><span data-stu-id="1c257-189">b.</span></span> <span data-ttu-id="1c257-190">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1c257-191">c.</span><span class="sxs-lookup"><span data-stu-id="1c257-191">c.</span></span> <span data-ttu-id="1c257-192">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1c257-193">d.</span><span class="sxs-lookup"><span data-stu-id="1c257-193">d.</span></span> <span data-ttu-id="1c257-194">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-194">Click **Create**.</span></span>
 
### <a name="create-a-thoughtworks-mingle-test-user"></a><span data-ttu-id="1c257-195">Thoughtworks Mingle 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="1c257-195">Create a Thoughtworks Mingle test user</span></span>

<span data-ttu-id="1c257-196">Azure AD 사용자가 로그인 할 수 있도록 Azure Active Directory 사용자 이름을 사용하여 Thoughtworks Mingle 응용 프로그램에 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-196">For Azure AD users to be able to sign in, they must be provisioned to the Thoughtworks Mingle application using their Azure Active Directory user names.</span></span> <span data-ttu-id="1c257-197">Thoughtworks Mingle의 경우 프로비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-197">In the case of Thoughtworks Mingle, provisioning is a manual task.</span></span>

<span data-ttu-id="1c257-198">**사용자 프로비전을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="1c257-198">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="1c257-199">Thoughtworks Mingle 회사 사이트에 관리자 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-199">Log in to your Thoughtworks Mingle company site as administrator.</span></span>

2. <span data-ttu-id="1c257-200">**프로필**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-200">Click **Profile**.</span></span>
   
    <span data-ttu-id="1c257-201">![첫 번째 프로젝트](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785160.png "첫 번째 프로젝트")</span><span class="sxs-lookup"><span data-stu-id="1c257-201">![Your First Project](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785160.png "Your First Project")</span></span>

3. <span data-ttu-id="1c257-202">**관리자** 탭을 클릭하고 **사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-202">Click the **Admin** tab, and then click **Users**.</span></span>
   
    <span data-ttu-id="1c257-203">![사용자](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785161.png "사용자")</span><span class="sxs-lookup"><span data-stu-id="1c257-203">![Users](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785161.png "Users")</span></span>

4. <span data-ttu-id="1c257-204">**새 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-204">Click **New User**.</span></span>
   
    <span data-ttu-id="1c257-205">![새 사용자](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785162.png "새 사용자")</span><span class="sxs-lookup"><span data-stu-id="1c257-205">![New User](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785162.png "New User")</span></span>

5. <span data-ttu-id="1c257-206">**새 사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-206">On the **New User** dialog page, perform the following steps:</span></span>
   
    <span data-ttu-id="1c257-207">![새 사용자 대화 상자](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785163.png "새 사용자")</span><span class="sxs-lookup"><span data-stu-id="1c257-207">![New User dialog](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785163.png "New User")</span></span>  
 
    <span data-ttu-id="1c257-208">a.</span><span class="sxs-lookup"><span data-stu-id="1c257-208">a.</span></span> <span data-ttu-id="1c257-209">관련된 텍스트 상자에 프로비전할 유효한 Azure AD 계정의 **로그인 이름**, **표시 이름**, **암호 선택**, **암호 확인**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-209">Type the **Sign-in name**, **Display name**, **Choose password**, **Confirm password** of a valid Azure AD account you want to provision into the related textboxes.</span></span> 

    <span data-ttu-id="1c257-210">b.</span><span class="sxs-lookup"><span data-stu-id="1c257-210">b.</span></span> <span data-ttu-id="1c257-211">**사용자 유형**으로 **전체 사용자**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-211">As **User type**, select **Full user**.</span></span>

    <span data-ttu-id="1c257-212">c.</span><span class="sxs-lookup"><span data-stu-id="1c257-212">c.</span></span> <span data-ttu-id="1c257-213">**이 프로필 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-213">Click **Create This Profile**.</span></span>

>[!NOTE]
><span data-ttu-id="1c257-214">다른 Thoughtworks Mingle 사용자 계정 생성 도구 또는 Thoughtworks Mingle이 제공한 API를 사용하여 AAD 사용자 계정을 프로비전할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-214">You can use any other Thoughtworks Mingle user account creation tools or APIs provided by Thoughtworks Mingle to provision AAD user accounts.</span></span>
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="1c257-215">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="1c257-215">Assign the Azure AD test user</span></span>

<span data-ttu-id="1c257-216">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Thoughtworks Mingle에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-216">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Thoughtworks Mingle.</span></span>

![사용자 역할 할당][200] 

<span data-ttu-id="1c257-218">**Thoughtworks Mingle에 Britta Simon을 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="1c257-218">**To assign Britta Simon to Thoughtworks Mingle, perform the following steps:**</span></span>

1. <span data-ttu-id="1c257-219">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-219">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="1c257-221">응용 프로그램 목록에서 **Thoughtworks Mingle**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-221">In the applications list, select **Thoughtworks Mingle**.</span></span>

    ![응용 프로그램 목록의 Thoughtworks Mingle 연결](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_app.png) 

3. <span data-ttu-id="1c257-223">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-223">In the menu on the left, click **Users and groups**.</span></span>

    !["사용자 및 그룹" 링크][202] 

4. <span data-ttu-id="1c257-225">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-225">Click **Add** button.</span></span> <span data-ttu-id="1c257-226">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![할당 추가 창][203]

5. <span data-ttu-id="1c257-228">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-228">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1c257-229">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1c257-230">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="1c257-231">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="1c257-231">Test single sign-on</span></span>

<span data-ttu-id="1c257-232">이 섹션은 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-232">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="1c257-233">액세스 패널에서 Thoughtworks Mingle 타일을 클릭하면 Thoughtworks Mingle 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-233">When you click the Thoughtworks Mingle tile in the Access Panel, you should get automatically signed-on to your Thoughtworks Mingle application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1c257-234">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="1c257-234">Additional resources</span></span>

* [<span data-ttu-id="1c257-235">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="1c257-235">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1c257-236">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="1c257-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_203.png

