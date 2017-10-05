---
title: "자습서: WORKS MOBILE과 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory 및 WORKS MOBILE 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 725f32fd-d0ad-49c7-b137-1cc246bf85d7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 139a1968a59424eae278de3e7fa227ad340a1eb8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-works-mobile"></a><span data-ttu-id="f15d2-103">자습서: WORKS MOBILE과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="f15d2-103">Tutorial: Azure Active Directory integration with WORKS MOBILE</span></span>

<span data-ttu-id="f15d2-104">이 자습서에서는 Azure AD(Azure Active Directory)와 WORKS MOBILE을 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f15d2-104">In this tutorial, you learn how to integrate WORKS MOBILE with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f15d2-105">WORKS MOBILE을 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="f15d2-105">Integrating WORKS MOBILE with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f15d2-106">WORKS MOBILE에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f15d2-106">You can control in Azure AD who has access to WORKS MOBILE</span></span>
- <span data-ttu-id="f15d2-107">사용자가 해당 Azure AD 계정으로 WORKS MOBILE에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f15d2-107">You can enable your users to automatically get signed-on to WORKS MOBILE (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f15d2-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f15d2-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f15d2-109">Azure AD와의 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory를 사용한 응용 프로그램 액세스 및 Single Sign-On](active-directory-appssoaccess-whatis.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f15d2-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f15d2-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="f15d2-110">Prerequisites</span></span>

<span data-ttu-id="f15d2-111">WORKS MOBILE과의 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f15d2-111">To configure Azure AD integration with WORKS MOBILE, you need the following items:</span></span>

- <span data-ttu-id="f15d2-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="f15d2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f15d2-113">WORKS MOBILE Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="f15d2-113">A WORKS MOBILE single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f15d2-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f15d2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f15d2-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f15d2-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f15d2-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="f15d2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f15d2-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f15d2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f15d2-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="f15d2-118">Scenario description</span></span>
<span data-ttu-id="f15d2-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="f15d2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f15d2-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f15d2-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f15d2-121">갤러리에서 WORKS MOBILE 추가</span><span class="sxs-lookup"><span data-stu-id="f15d2-121">Adding WORKS MOBILE from the gallery</span></span>
2. <span data-ttu-id="f15d2-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="f15d2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-works-mobile-from-the-gallery"></a><span data-ttu-id="f15d2-123">갤러리에서 WORKS MOBILE 추가</span><span class="sxs-lookup"><span data-stu-id="f15d2-123">Adding WORKS MOBILE from the gallery</span></span>
<span data-ttu-id="f15d2-124">WORKS MOBILE의 Azure AD 통합을 구성하려면 갤러리의 WORKS MOBILE을 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f15d2-124">To configure the integration of WORKS MOBILE into Azure AD, you need to add WORKS MOBILE from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f15d2-125">**갤러리에서 WORKS MOBILE을 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="f15d2-125">**To add WORKS MOBILE from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f15d2-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f15d2-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f15d2-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f15d2-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f15d2-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f15d2-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="f15d2-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f15d2-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="f15d2-133">검색 상자에 **WORKS MOBILE**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f15d2-133">In the search box, type **WORKS MOBILE**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_search.png)

5. <span data-ttu-id="f15d2-135">결과 창에서 **WORKS MOBILE**을 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f15d2-135">In the results panel, select **WORKS MOBILE**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f15d2-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="f15d2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f15d2-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 WORKS MOBILE에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="f15d2-138">In this section, you configure and test Azure AD single sign-on with WORKS MOBILE based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f15d2-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 WORKS MOBILE 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f15d2-139">For single sign-on to work, Azure AD needs to know what the counterpart user in WORKS MOBILE is to a user in Azure AD.</span></span> <span data-ttu-id="f15d2-140">즉, Azure AD 사용자와 WORKS MOBILE의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f15d2-140">In other words, a link relationship between an Azure AD user and the related user in WORKS MOBILE needs to be established.</span></span>

<span data-ttu-id="f15d2-141">이 연결 관계는 Azure AD의 **사용자 이름** 값을 WORKS MOBILE의 **Username** 값으로 할당하여 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f15d2-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in WORKS MOBILE.</span></span>

<span data-ttu-id="f15d2-142">WORKS MOBILE에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f15d2-142">To configure and test Azure AD single sign-on with WORKS MOBILE, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f15d2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f15d2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f15d2-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f15d2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f15d2-145">**[WORKS MOBILE 테스트 사용자 만들기](#creating-a-works-mobile-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 WORKS MOBILE에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f15d2-145">**[Creating a WORKS MOBILE test user](#creating-a-works-mobile-test-user)** - to have a counterpart of Britta Simon in WORKS MOBILE that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f15d2-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f15d2-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f15d2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f15d2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f15d2-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="f15d2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f15d2-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 WORKS MOBILE 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f15d2-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your WORKS MOBILE application.</span></span>

<span data-ttu-id="f15d2-150">**에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="f15d2-150">**To configure Azure AD single sign-on with WORKS MOBILE, perform the following steps:**</span></span>

1. <span data-ttu-id="f15d2-151">Azure Portal의 **WORKS MOBILE** 응용 프로그램 통합 페이지에서 **Single sign-on**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f15d2-151">In the Azure portal, on the **WORKS MOBILE** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="f15d2-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f15d2-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_samlbase.png)

3. <span data-ttu-id="f15d2-155">**WORKS MOBILE 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f15d2-155">On the **WORKS MOBILE Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_url.png)

    <span data-ttu-id="f15d2-157">a.</span><span class="sxs-lookup"><span data-stu-id="f15d2-157">a.</span></span> <span data-ttu-id="f15d2-158">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<subdomain>.worksmobile.com/jp/myservice`</span><span class="sxs-lookup"><span data-stu-id="f15d2-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.worksmobile.com/jp/myservice`</span></span>

    <span data-ttu-id="f15d2-159">b.</span><span class="sxs-lookup"><span data-stu-id="f15d2-159">b.</span></span> <span data-ttu-id="f15d2-160">**식별자** 텍스트 상자에 해당 값으로 `worksmobile.com`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f15d2-160">In the **Identifier** textbox, type the value as `worksmobile.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f15d2-161">이 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="f15d2-161">This value is not real.</span></span> <span data-ttu-id="f15d2-162">이 값을 실제 로그온 URL로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="f15d2-162">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="f15d2-163">이 값을 얻으려면 [WORKS MOBILE 클라이언트 지원 팀](mailto:dl_ssoinfo@worksmobile.com)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="f15d2-163">Contact [WORKS MOBILE Client support team](mailto:dl_ssoinfo@worksmobile.com) to get this value.</span></span> 
 
4. <span data-ttu-id="f15d2-164">**SAML 서명 인증서** 섹션에서 **인증서(원시)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f15d2-164">On the **SAML Signing Certificate** section, click **Certificate(Raw)** and then save the certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_certificate.png) 

5. <span data-ttu-id="f15d2-166">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f15d2-166">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-worksmobile-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f15d2-168">**WORKS MOBILE 구성** 섹션에서 **WORKS MOBILE 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f15d2-168">On the **WORKS MOBILE Configuration** section, click **Configure WORKS MOBILE** to open **Configure sign-on** window.</span></span> <span data-ttu-id="f15d2-169">**빠른 참조 섹션**에서 **로그아웃 URL, SAML 엔터티 ID 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="f15d2-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_configure.png) 

7. <span data-ttu-id="f15d2-171">응용 프로그램에 대해 구성된 SSO를 얻으려면 [WORKS MOBILE 지원 팀](mailto:dl_ssoinfo@worksmobile.com)에 연락하여 다음 정보를 제공하세요.</span><span class="sxs-lookup"><span data-stu-id="f15d2-171">To get SSO configured for your application, contact [WORKS MOBILE support team](mailto:dl_ssoinfo@worksmobile.com) and provide them with the following information:</span></span> 

    <span data-ttu-id="f15d2-172">• 다운로드한 **인증서 파일**</span><span class="sxs-lookup"><span data-stu-id="f15d2-172">• The downloaded **Certificate file**</span></span>

    <span data-ttu-id="f15d2-173">• **SAML Single Sign-On 서비스 URL**</span><span class="sxs-lookup"><span data-stu-id="f15d2-173">• The **SAML Single Sign-On Service URL**</span></span>

    <span data-ttu-id="f15d2-174">• **SAML 엔터티 ID**</span><span class="sxs-lookup"><span data-stu-id="f15d2-174">• The **SAML Entity ID**</span></span>

    <span data-ttu-id="f15d2-175">• **로그아웃 URL**</span><span class="sxs-lookup"><span data-stu-id="f15d2-175">• The **Sign-Out URL**</span></span>

> [!TIP]
> <span data-ttu-id="f15d2-176">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f15d2-176">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f15d2-177">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f15d2-177">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f15d2-178">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f15d2-178">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f15d2-179">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="f15d2-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="f15d2-180">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f15d2-180">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="f15d2-182">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="f15d2-182">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f15d2-183">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f15d2-183">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-worksmobile-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f15d2-185">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f15d2-185">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-worksmobile-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f15d2-187">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f15d2-187">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-worksmobile-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f15d2-189">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f15d2-189">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-worksmobile-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f15d2-191">a.</span><span class="sxs-lookup"><span data-stu-id="f15d2-191">a.</span></span> <span data-ttu-id="f15d2-192">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f15d2-192">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f15d2-193">b.</span><span class="sxs-lookup"><span data-stu-id="f15d2-193">b.</span></span> <span data-ttu-id="f15d2-194">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f15d2-194">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f15d2-195">c.</span><span class="sxs-lookup"><span data-stu-id="f15d2-195">c.</span></span> <span data-ttu-id="f15d2-196">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="f15d2-196">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f15d2-197">d.</span><span class="sxs-lookup"><span data-stu-id="f15d2-197">d.</span></span> <span data-ttu-id="f15d2-198">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f15d2-198">Click **Create**.</span></span>
 
### <a name="creating-a-works-mobile-test-user"></a><span data-ttu-id="f15d2-199">WORKS MOBILE 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="f15d2-199">Creating a WORKS MOBILE test user</span></span>

 <span data-ttu-id="f15d2-200">이 섹션에서는 WORKS MOBILE에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f15d2-200">In this section, you create a user called Britta Simon in WORKS MOBILE.</span></span> <span data-ttu-id="f15d2-201">WORKS MOBILE 플랫폼에서 사용자를 추가하려면 [WORKS MOBILE 지원 팀](mailto:dl_ssoinfo@worksmobile.com)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="f15d2-201">Please work with [WORKS MOBILE support team](mailto:dl_ssoinfo@worksmobile.com) to add the users in the WORKS MOBILE platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f15d2-202">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="f15d2-202">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f15d2-203">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 WORKS MOBILE에 대한 액세스를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="f15d2-203">In this section, you enable Britta Simon to use Azure single sign-on by granting access to WORKS MOBILE.</span></span>

![사용자 할당][200] 

<span data-ttu-id="f15d2-205">**Britta Simon을 WORKS MOBILE에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="f15d2-205">**To assign Britta Simon to WORKS MOBILE, perform the following steps:**</span></span>

1. <span data-ttu-id="f15d2-206">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f15d2-206">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="f15d2-208">응용 프로그램 목록에서 **WORKS MOBILE**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f15d2-208">In the applications list, select **WORKS MOBILE**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_app.png) 

3. <span data-ttu-id="f15d2-210">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f15d2-210">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="f15d2-212">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f15d2-212">Click **Add** button.</span></span> <span data-ttu-id="f15d2-213">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f15d2-213">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="f15d2-215">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f15d2-215">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f15d2-216">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f15d2-216">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f15d2-217">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f15d2-217">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f15d2-218">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="f15d2-218">Testing single sign-on</span></span>

<span data-ttu-id="f15d2-219">이 섹션에서는 액세스 패널을 사용하여 Azure AD SSO 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="f15d2-219">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="f15d2-220">액세스 패널에서 WORKS MOBILE 타일을 클릭하면 WORKS MOBILE 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="f15d2-220">When you click the WORKS MOBILE tile in the Access Panel, you should get automatically signed-on to your WORKS MOBILE application.</span></span>
<span data-ttu-id="f15d2-221">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f15d2-221">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="f15d2-222">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="f15d2-222">Additional resources</span></span>

* [<span data-ttu-id="f15d2-223">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="f15d2-223">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f15d2-224">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="f15d2-224">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_203.png

