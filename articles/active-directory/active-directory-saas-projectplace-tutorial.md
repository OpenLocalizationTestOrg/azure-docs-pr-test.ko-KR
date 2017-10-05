---
title: "자습서: Projectplace와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 Projectplace 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 298059ca-b652-4577-916a-c31393d53d7a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: bb9dd10c887cb0e42e544066d9b0dcfa554e10ce
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-projectplace"></a><span data-ttu-id="18a5e-103">자습서: Projectplace와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="18a5e-103">Tutorial: Azure Active Directory integration with Projectplace</span></span>

<span data-ttu-id="18a5e-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Projectplace를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="18a5e-104">In this tutorial, you learn how to integrate Projectplace with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="18a5e-105">Projectplace를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="18a5e-105">Integrating Projectplace with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="18a5e-106">Projectplace에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18a5e-106">You can control in Azure AD who has access to Projectplace</span></span>
- <span data-ttu-id="18a5e-107">사용자가 해당 Azure AD 계정으로 Projectplace에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18a5e-107">You can enable your users to automatically get signed-on to Projectplace (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="18a5e-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18a5e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="18a5e-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="18a5e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="18a5e-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="18a5e-110">Prerequisites</span></span>

<span data-ttu-id="18a5e-111">Projectplace와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="18a5e-111">To configure Azure AD integration with Projectplace, you need the following items:</span></span>

- <span data-ttu-id="18a5e-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="18a5e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="18a5e-113">Projectplace Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="18a5e-113">A Projectplace single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="18a5e-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="18a5e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="18a5e-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18a5e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="18a5e-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="18a5e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="18a5e-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18a5e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="18a5e-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="18a5e-118">Scenario description</span></span>
<span data-ttu-id="18a5e-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="18a5e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="18a5e-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18a5e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="18a5e-121">갤러리에서 Projectplace 추가</span><span class="sxs-lookup"><span data-stu-id="18a5e-121">Adding Projectplace from the gallery</span></span>
2. <span data-ttu-id="18a5e-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="18a5e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-projectplace-from-the-gallery"></a><span data-ttu-id="18a5e-123">갤러리에서 Projectplace 추가</span><span class="sxs-lookup"><span data-stu-id="18a5e-123">Adding Projectplace from the gallery</span></span>
<span data-ttu-id="18a5e-124">Projectplace의 Azure AD 통합을 구성하려면 갤러리의 Projectplace를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18a5e-124">To configure the integration of Projectplace into Azure AD, you need to add Projectplace from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="18a5e-125">**갤러리에서 Projectplace를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="18a5e-125">**To add Projectplace from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="18a5e-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="18a5e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="18a5e-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="18a5e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="18a5e-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="18a5e-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="18a5e-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="18a5e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="18a5e-133">검색 상자에 **Projectplace**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="18a5e-133">In the search box, type **Projectplace**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_search.png)

5. <span data-ttu-id="18a5e-135">결과 패널에서 **Projectplace**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="18a5e-135">In the results panel, select **Projectplace**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="18a5e-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="18a5e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="18a5e-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Projectplace에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="18a5e-138">In this section, you configure and test Azure AD single sign-on with Projectplace based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="18a5e-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Projectplace 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18a5e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Projectplace is to a user in Azure AD.</span></span> <span data-ttu-id="18a5e-140">즉, Azure AD 사용자와 Projectplace의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18a5e-140">In other words, a link relationship between an Azure AD user and the related user in Projectplace needs to be established.</span></span>

<span data-ttu-id="18a5e-141">Projectplace에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="18a5e-141">In Projectplace, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="18a5e-142">Projectplace에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18a5e-142">To configure and test Azure AD single sign-on with Projectplace, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="18a5e-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="18a5e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="18a5e-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="18a5e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="18a5e-145">**[Projectplace 테스트 사용자 만들기](#creating-a-projectplace-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 Projectplace에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="18a5e-145">**[Creating a Projectplace test user](#creating-a-projectplace-test-user)** - to have a counterpart of Britta Simon in Projectplace that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="18a5e-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="18a5e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="18a5e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="18a5e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="18a5e-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="18a5e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="18a5e-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Projectplace 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="18a5e-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Projectplace application.</span></span>

<span data-ttu-id="18a5e-150">**Projectplace에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="18a5e-150">**To configure Azure AD single sign-on with Projectplace, perform the following steps:**</span></span>

1. <span data-ttu-id="18a5e-151">Azure Portal의 **Projectplace** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="18a5e-151">In the Azure portal, on the **Projectplace** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="18a5e-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="18a5e-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_samlbase.png)

3. <span data-ttu-id="18a5e-155">**Projectplace 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="18a5e-155">On the **Projectplace Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_url.png)

    <span data-ttu-id="18a5e-157">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<company>.projectplace.com`</span><span class="sxs-lookup"><span data-stu-id="18a5e-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company>.projectplace.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="18a5e-158">이 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="18a5e-158">This value is not real.</span></span> <span data-ttu-id="18a5e-159">이 값을 실제 로그온 URL로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="18a5e-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="18a5e-160">이 값을 얻으려면 [Projectplace 클라이언트 지원 팀](https://success.planview.com/Projectplace/Support)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="18a5e-160">Contact [Projectplace Client support team](https://success.planview.com/Projectplace/Support) to get this value.</span></span> 
 
4. <span data-ttu-id="18a5e-161">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 메타데이터 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="18a5e-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_certificate.png) 

5. <span data-ttu-id="18a5e-163">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="18a5e-163">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-projectplace-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="18a5e-165">**Projectplace** 쪽에서 Single Sign-On을 구성하려면 다운로드한 **메타데이터 XML**을 [Projectplace 지원 팀](https://success.planview.com/Projectplace/Support)에 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18a5e-165">To configure single sign-on on **Projectplace** side, you need to send the downloaded **Metadata XML** to [Projectplace support team](https://success.planview.com/Projectplace/Support).</span></span> <span data-ttu-id="18a5e-166">이렇게 설정하면 SAML SSO 연결이 양쪽에서 제대로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="18a5e-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

>[!NOTE]
><span data-ttu-id="18a5e-167">Single Sign-On 구성을 [Projectplace 지원 팀](https://success.planview.com/Projectplace/Support)에서 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18a5e-167">The single sign-on configuration has to be performed by the [Projectplace support team](https://success.planview.com/Projectplace/Support).</span></span> <span data-ttu-id="18a5e-168">구성이 완료되는 즉시 알림을 받아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18a5e-168">You will get a notification as soon as the configuration has been completed.</span></span>

> [!TIP]
> <span data-ttu-id="18a5e-169">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18a5e-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="18a5e-170">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18a5e-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="18a5e-171">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18a5e-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="18a5e-172">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="18a5e-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="18a5e-173">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="18a5e-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="18a5e-175">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="18a5e-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="18a5e-176">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="18a5e-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-projectplace-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="18a5e-178">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="18a5e-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-projectplace-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="18a5e-180">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="18a5e-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-projectplace-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="18a5e-182">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="18a5e-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-projectplace-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="18a5e-184">a.</span><span class="sxs-lookup"><span data-stu-id="18a5e-184">a.</span></span> <span data-ttu-id="18a5e-185">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="18a5e-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="18a5e-186">b.</span><span class="sxs-lookup"><span data-stu-id="18a5e-186">b.</span></span> <span data-ttu-id="18a5e-187">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="18a5e-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="18a5e-188">c.</span><span class="sxs-lookup"><span data-stu-id="18a5e-188">c.</span></span> <span data-ttu-id="18a5e-189">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="18a5e-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="18a5e-190">d.</span><span class="sxs-lookup"><span data-stu-id="18a5e-190">d.</span></span> <span data-ttu-id="18a5e-191">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="18a5e-191">Click **Create**.</span></span>
 
### <a name="creating-a-projectplace-test-user"></a><span data-ttu-id="18a5e-192">Projectplace 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="18a5e-192">Creating a Projectplace test user</span></span>

<span data-ttu-id="18a5e-193">Azure AD 사용자가 Projectplace에 로그인할 수 있도록 하려면 Projectplace로 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18a5e-193">In order to enable Azure AD users to log into Projectplace, they must be provisioned into Projectplace.</span></span> <span data-ttu-id="18a5e-194">Projectplace의 경우 프로비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="18a5e-194">In the case of Projectplace, provisioning is a manual task.</span></span>

<span data-ttu-id="18a5e-195">**사용자 계정을 프로비전하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="18a5e-195">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="18a5e-196">**Projectplace** 회사 사이트에 관리자 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="18a5e-196">Log in to your **Projectplace** company site as an administrator.</span></span>

2. <span data-ttu-id="18a5e-197">**사람**으로 이동한 다음 **멤버**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="18a5e-197">Go to **People**, and then click **Members**.</span></span>
   
    <span data-ttu-id="18a5e-198">![사람](./media/active-directory-saas-projectplace-tutorial/ic790228.png "사람")</span><span class="sxs-lookup"><span data-stu-id="18a5e-198">![People](./media/active-directory-saas-projectplace-tutorial/ic790228.png "People")</span></span>

3. <span data-ttu-id="18a5e-199">**멤버 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="18a5e-199">Click **Add Member**.</span></span>
   
    <span data-ttu-id="18a5e-200">![멤버 추가](./media/active-directory-saas-projectplace-tutorial/ic790232.png "멤버 추가")</span><span class="sxs-lookup"><span data-stu-id="18a5e-200">![Add Members](./media/active-directory-saas-projectplace-tutorial/ic790232.png "Add Members")</span></span>

4. <span data-ttu-id="18a5e-201">**멤버 추가** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="18a5e-201">In the **Add Member** section, perform the following steps:</span></span>
   
    <span data-ttu-id="18a5e-202">![새 멤버](./media/active-directory-saas-projectplace-tutorial/ic790233.png "새 멤버")</span><span class="sxs-lookup"><span data-stu-id="18a5e-202">![New Members](./media/active-directory-saas-projectplace-tutorial/ic790233.png "New Members")</span></span>
   
    <span data-ttu-id="18a5e-203">a.</span><span class="sxs-lookup"><span data-stu-id="18a5e-203">a.</span></span> <span data-ttu-id="18a5e-204">**새 멤버** 텍스트 상자에서 프로비전할 유효한 AAD 계정의 이메일 주소를 관련 텍스트 상자에 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="18a5e-204">In the **New Members** textbox, type the email address of a valid AAD account you want to provision into the related textboxes.</span></span>
   
    <span data-ttu-id="18a5e-205">b.</span><span class="sxs-lookup"><span data-stu-id="18a5e-205">b.</span></span> <span data-ttu-id="18a5e-206">**보내기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="18a5e-206">Click **Send**.</span></span>

   <span data-ttu-id="18a5e-207">활성화되기 전에 계정을 확인하기 위한 링크를 포함한 이메일이 Azure Active Directory 계정 보유자에게 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="18a5e-207">An email including a link to confirm the account before it becomes active is sent to the Azure Active Directory account holder.</span></span>

>[!NOTE]
><span data-ttu-id="18a5e-208">다른 Projectplace 사용자 계정 생성 도구 또는 Projectplace가 제공한 API를 사용하여 AAD 사용자 계정을 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18a5e-208">You can use any other Projectplace user account creation tools or APIs provided by Projectplace to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="18a5e-209">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="18a5e-209">Assigning the Azure AD test user</span></span>

<span data-ttu-id="18a5e-210">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Projectplace에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="18a5e-210">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Projectplace.</span></span>

![사용자 할당][200] 

<span data-ttu-id="18a5e-212">**Britta Simon을 Projectplace에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="18a5e-212">**To assign Britta Simon to Projectplace, perform the following steps:**</span></span>

1. <span data-ttu-id="18a5e-213">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="18a5e-213">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="18a5e-215">응용 프로그램 목록에서 **Projectplace**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="18a5e-215">In the applications list, select **Projectplace**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_app.png) 

3. <span data-ttu-id="18a5e-217">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="18a5e-217">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="18a5e-219">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="18a5e-219">Click **Add** button.</span></span> <span data-ttu-id="18a5e-220">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="18a5e-220">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="18a5e-222">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="18a5e-222">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="18a5e-223">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="18a5e-223">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="18a5e-224">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="18a5e-224">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="18a5e-225">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="18a5e-225">Testing single sign-on</span></span>

<span data-ttu-id="18a5e-226">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="18a5e-226">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="18a5e-227">액세스 패널에서 Projectplace 타일을 클릭하면 Projectplace 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="18a5e-227">When you click the Projectplace tile in the Access Panel, you should get automatically signed-on to your Projectplace application.</span></span>
<span data-ttu-id="18a5e-228">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="18a5e-228">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="18a5e-229">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="18a5e-229">Additional resources</span></span>

* [<span data-ttu-id="18a5e-230">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="18a5e-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="18a5e-231">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="18a5e-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_203.png

