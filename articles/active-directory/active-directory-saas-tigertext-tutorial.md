---
title: "자습서: TigerText Secure Messenger와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 TigerText Secure Messenger 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 03f1e128-5bcb-4e49-b6a3-fe22eedc6d5e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: jeedes
ms.openlocfilehash: e101e5fc84b032b66dd0636bab8bff128791f77c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tigertext-secure-messenger"></a><span data-ttu-id="79082-103">자습서: TigerText Secure Messenger와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="79082-103">Tutorial: Azure Active Directory integration with TigerText Secure Messenger</span></span>

<span data-ttu-id="79082-104">이 자습서에서는 Azure AD(Azure Active Directory)와 TigerText Secure Messenger를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="79082-104">In this tutorial, you learn how to integrate TigerText Secure Messenger with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="79082-105">TigerText Secure Messenger를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="79082-105">Integrating TigerText Secure Messenger with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="79082-106">TigerText Secure Messenger에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79082-106">You can control in Azure AD who has access to TigerText Secure Messenger</span></span>
- <span data-ttu-id="79082-107">사용자가 해당 Azure AD 계정으로 TigerText Secure Messenger에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79082-107">You can enable your users to automatically get signed-on to TigerText Secure Messenger (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="79082-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79082-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="79082-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="79082-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="79082-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="79082-110">Prerequisites</span></span>

<span data-ttu-id="79082-111">TigerText Secure Messenger와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="79082-111">To configure Azure AD integration with TigerText Secure Messenger, you need the following items:</span></span>

- <span data-ttu-id="79082-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="79082-112">An Azure AD subscription</span></span>
- <span data-ttu-id="79082-113">TigerText Secure Messenger Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="79082-113">A TigerText Secure Messenger single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="79082-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="79082-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="79082-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="79082-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="79082-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="79082-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="79082-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79082-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="79082-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="79082-118">Scenario description</span></span>
<span data-ttu-id="79082-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="79082-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="79082-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79082-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="79082-121">갤러리에서 TigerText Secure Messenger 추가</span><span class="sxs-lookup"><span data-stu-id="79082-121">Add TigerText Secure Messenger from the gallery</span></span>
2. <span data-ttu-id="79082-122">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="79082-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-tigertext-secure-messenger-from-the-gallery"></a><span data-ttu-id="79082-123">갤러리에서 TigerText Secure Messenger 추가</span><span class="sxs-lookup"><span data-stu-id="79082-123">Add TigerText Secure Messenger from the gallery</span></span>
<span data-ttu-id="79082-124">TigerText Secure Messenger의 Azure AD 통합을 구성하려면 갤러리의 TigerText Secure Messenger를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="79082-124">To configure the integration of TigerText Secure Messenger into Azure AD, you need to add TigerText Secure Messenger from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="79082-125">**갤러리에서 TigerText Secure Messenger를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="79082-125">**To add TigerText Secure Messenger from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="79082-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="79082-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="79082-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="79082-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="79082-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="79082-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="79082-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="79082-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="79082-133">검색 상자에서 **TigerText Secure Messenger**를 입력하고, 결과 패널에서 **TigerText Secure Messenger**를 선택한 다음, **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="79082-133">In the search box, type **TigerText Secure Messenger**, select **TigerText Secure Messenger** from result panel then click **Add** button to add the application.</span></span>

    ![갤러리에서 추가](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="79082-135">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="79082-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="79082-136">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 하여 TigerText Secure Messenger에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="79082-136">In this section, you configure and test Azure AD single sign-on with TigerText Secure Messenger based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="79082-137">Single Sign-On이 작동하려면 Azure AD 사용자에 해당하는 TigerText Secure Messenger 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="79082-137">For single sign-on to work, Azure AD needs to know what the counterpart user in TigerText Secure Messenger is to a user in Azure AD.</span></span> <span data-ttu-id="79082-138">즉, Azure AD 사용자와 TigerText Secure Messenger의 관련 사용자 간에 링크 관계가 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="79082-138">In other words, a link relationship between an Azure AD user and the related user in TigerText Secure Messenger needs to be established.</span></span>

<span data-ttu-id="79082-139">TigerText Secure Messenger에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="79082-139">In TigerText Secure Messenger, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="79082-140">TigerText Secure Messenger에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="79082-140">To configure and test Azure AD single sign-on with TigerText Secure Messenger, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="79082-141">**[Azure AD Single Sign-On 구성](#configure-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="79082-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="79082-142">**[Azure AD 테스트 사용자 만들기](#create-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="79082-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="79082-143">**[TigerText Secure Messenger 테스트 사용자 만들기](#create-a-tigertext-secure-messenger-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 TigerText Secure Messenger에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="79082-143">**[Create a TigerText Secure Messenger test user](#create-a-tigertext-secure-messenger-test-user)** - to have a counterpart of Britta Simon in TigerText Secure Messenger that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="79082-144">**[Azure AD 테스트 사용자 할당](#assign-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="79082-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="79082-145">**[Single Sign-on 테스트](#test-single-sign-on)** - 구성이 작동하는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="79082-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="79082-146">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="79082-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="79082-147">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 TigerText Secure Messenger 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="79082-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TigerText Secure Messenger application.</span></span>

<span data-ttu-id="79082-148">**TigerText Secure Messenger에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="79082-148">**To configure Azure AD single sign-on with TigerText Secure Messenger, perform the following steps:**</span></span>

1. <span data-ttu-id="79082-149">Azure Portal의 **TigerText Secure Messenger** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="79082-149">In the Azure portal, on the **TigerText Secure Messenger** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="79082-151">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="79082-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![SAML 기반 로그온](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_samlbase.png)

3. <span data-ttu-id="79082-153">**TigerText Secure Messenger 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="79082-153">On the **TigerText Secure Messenger Domain and URLs** section, perform the following steps:</span></span>

    ![TigerText Secure Messenger 도메인 및 URL 섹션](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_url.png)

    <span data-ttu-id="79082-155">a.</span><span class="sxs-lookup"><span data-stu-id="79082-155">a.</span></span> <span data-ttu-id="79082-156">**로그온 URL** 텍스트 상자에서 URL을 입력합니다(예: `https://home.tigertext.com`).</span><span class="sxs-lookup"><span data-stu-id="79082-156">In the **Sign-on URL** textbox, type URL as: `https://home.tigertext.com`</span></span>

    <span data-ttu-id="79082-157">b.</span><span class="sxs-lookup"><span data-stu-id="79082-157">b.</span></span> <span data-ttu-id="79082-158">**식별자** 텍스트 상자에서 `https://saml-lb.tigertext.me/v1/organization/<instance Id>` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="79082-158">In the **Identifier** textbox, type a URL using the following pattern: `https://saml-lb.tigertext.me/v1/organization/<instance Id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="79082-159">이 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="79082-159">This value is not real.</span></span> <span data-ttu-id="79082-160">실제 식별자로 이 값을 업데이트하세요.</span><span class="sxs-lookup"><span data-stu-id="79082-160">Update this value with the actual Identifier.</span></span> <span data-ttu-id="79082-161">이 값을 얻으려면 [TigerText Secure Messenger 클라이언트 지원 팀](mailTo:prosupport@tigertext.com)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="79082-161">Contact [TigerText Secure Messenger Client support team](mailTo:prosupport@tigertext.com) to get this value.</span></span> 
 
4. <span data-ttu-id="79082-162">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 메타데이터 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="79082-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![SAML 서명 인증서 섹션](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_certificate.png) 

5. <span data-ttu-id="79082-164">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="79082-164">Click **Save** button.</span></span>

    ![저장 단추](./media/active-directory-saas-tigertext-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="79082-166">응용 프로그램에 대해 Single Sign-On을 구성하려면 [TigerText Secure Messenger 지원 팀](mailTo:prosupport@tigertext.com)에 문의하고 **다운로드한 메타데이터**를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="79082-166">To get single sign-on configured for your application, contact [TigerText Secure Messenger support team](mailTo:prosupport@tigertext.com) and provide them the **Downloaded metadata**.</span></span>

> [!TIP]
> <span data-ttu-id="79082-167">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79082-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="79082-168">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="79082-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="79082-169">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79082-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="79082-170">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="79082-170">Create an Azure AD test user</span></span>
<span data-ttu-id="79082-171">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="79082-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="79082-173">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="79082-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="79082-174">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="79082-174">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-tigertext-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="79082-176">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="79082-176">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![사용자 및 그룹 -> 모든 사용자](./media/active-directory-saas-tigertext-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="79082-178">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="79082-178">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![추가 단추](./media/active-directory-saas-tigertext-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="79082-180">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="79082-180">On the **User** dialog page, perform the following steps:</span></span>
 
    ![사용자 대화 상자](./media/active-directory-saas-tigertext-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="79082-182">a.</span><span class="sxs-lookup"><span data-stu-id="79082-182">a.</span></span> <span data-ttu-id="79082-183">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="79082-183">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="79082-184">b.</span><span class="sxs-lookup"><span data-stu-id="79082-184">b.</span></span> <span data-ttu-id="79082-185">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="79082-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="79082-186">c.</span><span class="sxs-lookup"><span data-stu-id="79082-186">c.</span></span> <span data-ttu-id="79082-187">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="79082-187">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="79082-188">d.</span><span class="sxs-lookup"><span data-stu-id="79082-188">d.</span></span> <span data-ttu-id="79082-189">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="79082-189">Click **Create**.</span></span>
 
### <a name="create-a-tigertext-secure-messenger-test-user"></a><span data-ttu-id="79082-190">TigerText Secure Messenger 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="79082-190">Create a TigerText Secure Messenger test user</span></span>

<span data-ttu-id="79082-191">이 섹션에서는 TigerText에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="79082-191">In this section, you create a user called Britta Simon in TigerText.</span></span> <span data-ttu-id="79082-192">[TigerText Secure Messenger 클라이언트 지원 팀](mailTo:prosupport@tigertext.com)에 문의하여 TigerText 플랫폼에 사용자를 추가하세요.</span><span class="sxs-lookup"><span data-stu-id="79082-192">Please reach out to [TigerText Secure Messenger Client support team](mailTo:prosupport@tigertext.com) to add the users in the TigerText platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="79082-193">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="79082-193">Assign the Azure AD test user</span></span>

<span data-ttu-id="79082-194">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 TigerText Secure Messenger에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="79082-194">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TigerText Secure Messenger.</span></span>

![사용자 할당][200] 

<span data-ttu-id="79082-196">**Britta Simon을 TigerText Secure Messenger에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="79082-196">**To assign Britta Simon to TigerText Secure Messenger, perform the following steps:**</span></span>

1. <span data-ttu-id="79082-197">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="79082-197">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="79082-199">응용 프로그램 목록에서 **TigerText Secure Messenger**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="79082-199">In the applications list, select **TigerText Secure Messenger**.</span></span>

    ![응용 프로그램 목록의 TigerText Secure Messenger](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_app.png) 

3. <span data-ttu-id="79082-201">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="79082-201">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="79082-203">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="79082-203">Click **Add** button.</span></span> <span data-ttu-id="79082-204">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="79082-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="79082-206">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="79082-206">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="79082-207">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="79082-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="79082-208">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="79082-208">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="79082-209">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="79082-209">Test single sign-on</span></span>

<span data-ttu-id="79082-210">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="79082-210">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="79082-211">액세스 패널에서 TigerText 타일을 클릭하면 TigerText 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="79082-211">When you click the TigerText tile in the Access Panel, you should get automatically signed-on to your TigerText application.</span></span> <span data-ttu-id="79082-212">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="79082-212">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="79082-213">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="79082-213">Additional resources</span></span>

* [<span data-ttu-id="79082-214">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="79082-214">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="79082-215">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="79082-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_203.png

