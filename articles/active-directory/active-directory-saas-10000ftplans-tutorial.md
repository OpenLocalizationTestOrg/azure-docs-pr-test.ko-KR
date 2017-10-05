---
title: "자습서: Azure Active Directory와 10,000ft Plans 통합 | Microsoft Docs"
description: "Azure Active Directory 및 10,000ft Plans 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b60c955e-8fa3-4872-a897-c4e81fd7beac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: c81a6adb3abad58af149bbef6f5dff736c142f51
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-10000ft-plans"></a><span data-ttu-id="67534-103">자습서: Azure Active Directory와 10,000ft Plans 통합</span><span class="sxs-lookup"><span data-stu-id="67534-103">Tutorial: Azure Active Directory integration with 10,000ft Plans</span></span>

<span data-ttu-id="67534-104">이 자습서에서는 Azure AD(Azure Active Directory)와 10,000ft Plans를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="67534-104">In this tutorial, you learn how to integrate 10,000ft Plans with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="67534-105">10,000ft Plans를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="67534-105">Integrating 10,000ft Plans with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="67534-106">10,000ft Plans에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67534-106">You can control in Azure AD who has access to 10,000ft Plans</span></span>
- <span data-ttu-id="67534-107">사용자가 해당 Azure AD 계정으로 10,000ft Plans에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67534-107">You can enable your users to automatically get signed-on to 10,000ft Plans (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="67534-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67534-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="67534-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="67534-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="67534-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="67534-110">Prerequisites</span></span>

<span data-ttu-id="67534-111">10,000ft Plans와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="67534-111">To configure Azure AD integration with 10,000ft Plans, you need the following items:</span></span>

- <span data-ttu-id="67534-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="67534-112">An Azure AD subscription</span></span>
- <span data-ttu-id="67534-113">10,000ft Plans Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="67534-113">A 10,000ft Plans single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="67534-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="67534-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="67534-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67534-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="67534-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="67534-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="67534-117">Azure AD 평가판 환경이 없으면 [평가판 제품](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67534-117">If you don't have an Azure AD trial environment, you can get a one-month trial here [trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="67534-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="67534-118">Scenario description</span></span>
<span data-ttu-id="67534-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="67534-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="67534-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67534-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="67534-121">갤러리에서 10,000ft Plans 추가</span><span class="sxs-lookup"><span data-stu-id="67534-121">Adding 10,000ft Plans from the gallery</span></span>
2. <span data-ttu-id="67534-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="67534-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-10000ft-plans-from-the-gallery"></a><span data-ttu-id="67534-123">갤러리에서 10,000ft Plans 추가</span><span class="sxs-lookup"><span data-stu-id="67534-123">Adding 10,000ft Plans from the gallery</span></span>
<span data-ttu-id="67534-124">10,000ft Plans의 Azure AD 통합을 구성하려면 갤러리의 10,000ft Plans를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67534-124">To configure the integration of 10,000ft Plans into Azure AD, you need to add 10,000ft Plans from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="67534-125">**갤러리에서 10,000ft Plans를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="67534-125">**To add 10,000ft Plans from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="67534-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="67534-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="67534-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="67534-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="67534-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="67534-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="67534-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="67534-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="67534-133">검색 상자에 **10,000ft Plans**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="67534-133">In the search box, type **10,000ft Plans**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_search.png)

5. <span data-ttu-id="67534-135">결과 창에서 **10,000ft Plans**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="67534-135">In the results panel, select **10,000ft Plans**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="67534-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="67534-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="67534-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 10,000ft Plans에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="67534-138">In this section, you configure and test Azure AD single sign-on with 10,000ft Plans based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="67534-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 10,000ft Plans 사용자가 누군지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67534-139">For single sign-on to work, Azure AD needs to know what the counterpart user in 10,000ft Plans is to a user in Azure AD.</span></span> <span data-ttu-id="67534-140">즉, Azure AD 사용자와 10,000ft Plans의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67534-140">In other words, a link relationship between an Azure AD user and the related user in 10,000ft Plans needs to be established.</span></span>

<span data-ttu-id="67534-141">10,000ft Plans에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 연결 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="67534-141">In 10,000ft Plans, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="67534-142">10,000ft Plans에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67534-142">To configure and test Azure AD single sign-on with 10,000ft Plans, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="67534-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="67534-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="67534-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="67534-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="67534-145">**[10,000ft Plans 테스트 사용자 만들기](#creating-a-10000ft-plans-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 10,000ft Plans에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="67534-145">**[Creating a 10,000ft Plans test user](#creating-a-10000ft-plans-test-user)** - to have a counterpart of Britta Simon in 10,000ft Plans that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="67534-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="67534-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="67534-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="67534-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="67534-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="67534-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="67534-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 10,000ft Plans 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="67534-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your 10,000ft Plans application.</span></span>

<span data-ttu-id="67534-150">**10,000ft Plans에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="67534-150">**To configure Azure AD single sign-on with 10,000ft Plans, perform the following steps:**</span></span>

1. <span data-ttu-id="67534-151">Azure Portal의 **10,000ft Plans** 응용 프로그램 통합 페이지에서 **Single sign-on**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="67534-151">In the Azure portal, on the **10,000ft Plans** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="67534-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="67534-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_samlbase.png)

3. <span data-ttu-id="67534-155">**10,000ft Plans 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="67534-155">On the **10,000ft Plans Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_url.png)

    <span data-ttu-id="67534-157">a.</span><span class="sxs-lookup"><span data-stu-id="67534-157">a.</span></span> <span data-ttu-id="67534-158">**로그온 URL** 텍스트 상자에서 URL `https://app.10000ft.com`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="67534-158">In the **Sign-on URL** textbox, type the URL: `https://app.10000ft.com`</span></span>

    <span data-ttu-id="67534-159">b.</span><span class="sxs-lookup"><span data-stu-id="67534-159">b.</span></span> <span data-ttu-id="67534-160">**식별자** 텍스트 상자에 URL `https://app.10000ft.com/saml/metadata`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="67534-160">In the **Identifier** textbox, type the URL: `https://app.10000ft.com/saml/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="67534-161">사용자 지정 도메인이 있는 경우 **식별자** 값이 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="67534-161">The value for **Identifier** is different if you have a custom domain.</span></span> <span data-ttu-id="67534-162">이 값을 얻으려면 [10,000ft Plans 지원 팀](https://www.10000ft.com/plans/support)에 문의합니다.</span><span class="sxs-lookup"><span data-stu-id="67534-162">Contact [10,000ft Plans support team](https://www.10000ft.com/plans/support) to get this value.</span></span> 
 
4. <span data-ttu-id="67534-163">**SAML 서명 인증서** 섹션에서 **인증서(원시)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="67534-163">On the **SAML Signing Certificate** section, click **Certificate(Raw)** and then save the certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_certificate.png) 

5. <span data-ttu-id="67534-165">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="67534-165">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="67534-167">**10,000ft Plans 구성** 섹션에서 **10,000ft Plans 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="67534-167">On the **10,000ft Plans Configuration** section, click **Configure 10,000ft Plans** to open **Configure sign-on** window.</span></span> <span data-ttu-id="67534-168">**빠른 참조 섹션**에서 **로그아웃 URL, SAML 엔터티 ID 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="67534-168">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_configure.png) 

7. <span data-ttu-id="67534-170">**10,000ft Plans** 쪽에서 Single Sign-On을 구성하려면 다운로드한 **인증서(원시), 로그아웃 URL, SAML 엔터티 ID 및 SAML Single Sign-On 서비스 URL**을 [10,000ft Plans 지원 팀](https://www.10000ft.com/plans/support)에 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67534-170">To configure single sign-on on **10,000ft Plans** side, you need to send the downloaded **Certificate(Raw), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [10,000ft Plans support team](https://www.10000ft.com/plans/support).</span></span>

> [!TIP]
> <span data-ttu-id="67534-171">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67534-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="67534-172">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67534-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="67534-173">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67534-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="67534-174">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="67534-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="67534-175">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="67534-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="67534-177">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="67534-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="67534-178">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="67534-178">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-10000ftplans-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="67534-180">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="67534-180">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-10000ftplans-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="67534-182">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="67534-182">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-10000ftplans-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="67534-184">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="67534-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-10000ftplans-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="67534-186">a.</span><span class="sxs-lookup"><span data-stu-id="67534-186">a.</span></span> <span data-ttu-id="67534-187">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="67534-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="67534-188">b.</span><span class="sxs-lookup"><span data-stu-id="67534-188">b.</span></span> <span data-ttu-id="67534-189">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="67534-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="67534-190">c.</span><span class="sxs-lookup"><span data-stu-id="67534-190">c.</span></span> <span data-ttu-id="67534-191">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="67534-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="67534-192">d.</span><span class="sxs-lookup"><span data-stu-id="67534-192">d.</span></span> <span data-ttu-id="67534-193">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="67534-193">Click **Create**.</span></span>
 
### <a name="creating-a-10000ft-plans-test-user"></a><span data-ttu-id="67534-194">10,000ft Plans 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="67534-194">Creating a 10,000ft Plans test user</span></span>

<span data-ttu-id="67534-195">이 섹션은 10,000ft Plans에서 Britta Simon이라는 사용자를 만들기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="67534-195">The objective of this section is to create a user called Britta Simon in 10,000ft Plans.</span></span> <span data-ttu-id="67534-196">10,000ft Plans는 적시에 프로비전을 지원하며 기본적으로 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="67534-196">10,000ft Plans supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="67534-197">이 섹션에 작업 항목이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="67534-197">There is no action item for you in this section.</span></span> <span data-ttu-id="67534-198">새 사용자가 아직 존재하지 않는 경우 10,000ft Plans에 액세스하는 동안 만들어질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67534-198">A new user is created during an attempt to access 10,000ft Plans if it doesn't exist yet.</span></span> 

> [!NOTE]
> <span data-ttu-id="67534-199">사용자를 수동으로 만들어야 하는 경우 [10,000ft Plans 지원 팀](https://www.10000ft.com/plans/support)에 문의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67534-199">If you need to create a user manually, you need to contact the [10,000ft Plans support team](https://www.10000ft.com/plans/support).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="67534-200">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="67534-200">Assigning the Azure AD test user</span></span>

<span data-ttu-id="67534-201">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 10,000ft Plans에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="67534-201">In this section, you enable Britta Simon to use Azure single sign-on by granting access to 10,000ft Plans.</span></span>

![사용자 할당][200] 

<span data-ttu-id="67534-203">**Britta Simon을 10,000ft Plans에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="67534-203">**To assign Britta Simon to 10,000ft Plans, perform the following steps:**</span></span>

1. <span data-ttu-id="67534-204">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="67534-204">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="67534-206">응용 프로그램 목록에서 **10,000ft Plans**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="67534-206">In the applications list, select **10,000ft Plans**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_app.png) 

3. <span data-ttu-id="67534-208">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="67534-208">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="67534-210">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="67534-210">Click **Add** button.</span></span> <span data-ttu-id="67534-211">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="67534-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="67534-213">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="67534-213">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="67534-214">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="67534-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="67534-215">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="67534-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="67534-216">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="67534-216">Testing single sign-on</span></span>

<span data-ttu-id="67534-217">이 섹션은 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="67534-217">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="67534-218">액세스 패널에서 10,000ft Plans 타일을 클릭하면 10,000ft Plans 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="67534-218">When you click the 10,000ft Plans tile in the Access Panel, you should get automatically signed-on to your 10,000ft Plans application.</span></span>
 
## <a name="additional-resources"></a><span data-ttu-id="67534-219">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="67534-219">Additional resources</span></span>

* [<span data-ttu-id="67534-220">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="67534-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="67534-221">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="67534-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_203.png

