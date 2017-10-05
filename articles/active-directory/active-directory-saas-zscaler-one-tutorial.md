---
title: "자습서: Azure Active Directory와 Zscaler One 통합| Microsoft Azure"
description: "Azure Active Directory와 Zscaler One 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f352e00d-68d3-4a77-bb92-717d055da56f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 7d655c482a16c991a819eec84c84556d2f288a75
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-one"></a><span data-ttu-id="fcc06-103">자습서: Azure Active Directory와 Zscaler One 통합</span><span class="sxs-lookup"><span data-stu-id="fcc06-103">Tutorial: Azure Active Directory integration with Zscaler One</span></span>

<span data-ttu-id="fcc06-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Zscaler One을 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-104">In this tutorial, you learn how to integrate Zscaler One with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fcc06-105">Zscaler One을 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-105">Integrating Zscaler One with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="fcc06-106">Zscaler One에 액세스할 수 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-106">You can control in Azure AD who has access to Zscaler One</span></span>
- <span data-ttu-id="fcc06-107">사용자가 자신의 Azure AD 계정으로 Zscaler One에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-107">You can enable your users to automatically get signed-on to Zscaler One (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="fcc06-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="fcc06-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fcc06-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fcc06-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="fcc06-110">Prerequisites</span></span>

<span data-ttu-id="fcc06-111">Zscaler One과 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-111">To configure Azure AD integration with Zscaler One, you need the following items:</span></span>

- <span data-ttu-id="fcc06-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="fcc06-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fcc06-113">ZScaler One Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="fcc06-113">A Zscaler One single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fcc06-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fcc06-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fcc06-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="fcc06-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fcc06-117">Azure AD 평가판 환경이 없으면 [평가판 제품](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fcc06-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="fcc06-118">Scenario description</span></span>
<span data-ttu-id="fcc06-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fcc06-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fcc06-121">갤러리에서 Zscaler One 추가</span><span class="sxs-lookup"><span data-stu-id="fcc06-121">Adding Zscaler One from the gallery</span></span>
2. <span data-ttu-id="fcc06-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="fcc06-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zscaler-one-from-the-gallery"></a><span data-ttu-id="fcc06-123">갤러리에서 Zscaler One 추가</span><span class="sxs-lookup"><span data-stu-id="fcc06-123">Adding Zscaler One from the gallery</span></span>
<span data-ttu-id="fcc06-124">Zscaler One이 Azure AD에 통합되도록 구성하려면 갤러리의 Zscaler One을 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-124">To configure the integration of Zscaler One into Azure AD, you need to add Zscaler One from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="fcc06-125">**갤러리에서 Zscaler One을 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="fcc06-125">**To add Zscaler One from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="fcc06-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="fcc06-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="fcc06-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="fcc06-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="fcc06-133">검색 상자에 **Zscaler One**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-133">In the search box, type **Zscaler One**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-zscaler-one-tutorial/tutorial_zscalerone_search.png)

5. <span data-ttu-id="fcc06-135">결과 패널에서 **Zscaler One**을 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-135">In the results panel, select **Zscaler One**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-zscaler-one-tutorial/tutorial_zscalerone_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="fcc06-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="fcc06-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="fcc06-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 사용하여 Zscaler One에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-138">In this section, you configure and test Azure AD single sign-on with Zscaler One based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="fcc06-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Zscaler One 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Zscaler One is to a user in Azure AD.</span></span> <span data-ttu-id="fcc06-140">즉, Azure AD 사용자와 Zscaler One의 관련 사용자 간에 연결 관계를 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-140">In other words, a link relationship between an Azure AD user and the related user in Zscaler One needs to be established.</span></span>

<span data-ttu-id="fcc06-141">Zscaler One에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 연결 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-141">In Zscaler One, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="fcc06-142">Zscaler One에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-142">To configure and test Azure AD single sign-on with Zscaler One, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="fcc06-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="fcc06-144">**[프록시 설정 구성](#configuring-proxy-settings)** - Internet Explorer에서 프록시 설정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-144">**[Configuring proxy settings](#configuring-proxy-settings)** - to configure the proxy settings in Internet Explorer</span></span>
3. <span data-ttu-id="fcc06-145">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="fcc06-146">**[Zscaler One 테스트 사용자 만들기](#creating-a-zscaler-one-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 Zscaler One에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-146">**[Creating a Zscaler One test user](#creating-a-zscaler-one-test-user)** - to have a counterpart of Britta Simon in Zscaler One that is linked to the Azure AD representation of user.</span></span>
5. <span data-ttu-id="fcc06-147">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
6. <span data-ttu-id="fcc06-148">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="fcc06-149">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="fcc06-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="fcc06-150">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Zscaler One 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Zscaler One application.</span></span>

<span data-ttu-id="fcc06-151">**Zscaler One에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="fcc06-151">**To configure Azure AD single sign-on with Zscaler One, perform the following steps:**</span></span>

1. <span data-ttu-id="fcc06-152">Azure Portal의 **Zscaler One** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-152">In the Azure portal, on the **Zscaler One** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="fcc06-154">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-zscaler-one-tutorial/tutorial_zscalerone_samlbase.png)

3. <span data-ttu-id="fcc06-156">**Zscaler One 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-156">On the **Zscaler One Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-zscaler-one-tutorial/tutorial_zscalerone_url.png)

    <span data-ttu-id="fcc06-158">[로그온 URL] 텍스트 상자에 사용자가 Zscaler One 응용 프로그램에 로그인하는 데 사용하는 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-158">In the Sign-on URL textbox, type the URL used by your users to sign-on to your Zscaler One application.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="fcc06-159">이 값은 실제 로그온 URL로 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-159">You have to update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="fcc06-160">이러한 값을 얻으려면 [Zscaler One 클라이언트 지원 팀](https://www.zscaler.com/company/contact)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="fcc06-160">Contact [Zscaler One Client support team](https://www.zscaler.com/company/contact) to get these values.</span></span>

4. <span data-ttu-id="fcc06-161">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-zscaler-one-tutorial/tutorial_zscalerone_certificate.png) 

5. <span data-ttu-id="fcc06-163">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-163">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="fcc06-165">**Zscaler One 구성** 섹션에서 **Zscaler One 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-165">On the **Zscaler One Configuration** section, click **Configure Zscaler One** to open **Configure sign-on** window.</span></span> <span data-ttu-id="fcc06-166">**빠른 참조 섹션**에서 **SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-166">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-zscaler-one-tutorial/tutorial_zscalerone_configure.png) 

7. <span data-ttu-id="fcc06-168">다른 웹 브라우저 창에서 관리자 권한으로 Zscaler One 회사 사이트에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-168">In a different web browser window, log in to your Zscaler One company site as an administrator.</span></span>

8. <span data-ttu-id="fcc06-169">위쪽의 메뉴에서 **관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-169">In the menu on the top, click **Administration**.</span></span>
   
    <span data-ttu-id="fcc06-170">![관리](./media/active-directory-saas-zscaler-one-tutorial/ic800206.png "관리")</span><span class="sxs-lookup"><span data-stu-id="fcc06-170">![Administration](./media/active-directory-saas-zscaler-one-tutorial/ic800206.png "Administration")</span></span>

9. <span data-ttu-id="fcc06-171">**관리자 & 역할 관리**에서 **사용자 및 인증 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-171">Under **Manage Administrators & Roles**, click **Manage Users & Authentication**.</span></span>   
            
    <span data-ttu-id="fcc06-172">![사용자 및 인증 관리](./media/active-directory-saas-zscaler-one-tutorial/ic800207.png "사용자 및 인증 관리")</span><span class="sxs-lookup"><span data-stu-id="fcc06-172">![Manage Users & Authentication](./media/active-directory-saas-zscaler-one-tutorial/ic800207.png "Manage Users & Authentication")</span></span>

10. <span data-ttu-id="fcc06-173">**구성에 대한 인증 옵션 선택** 섹션에서, 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-173">In the **Choose Authentication Options for your Organization** section, perform the following steps:</span></span>   
                
    <span data-ttu-id="fcc06-174">![인증](./media/active-directory-saas-zscaler-one-tutorial/ic800208.png "인증")</span><span class="sxs-lookup"><span data-stu-id="fcc06-174">![Authentication](./media/active-directory-saas-zscaler-one-tutorial/ic800208.png "Authentication")</span></span>
   
    <span data-ttu-id="fcc06-175">a.</span><span class="sxs-lookup"><span data-stu-id="fcc06-175">a.</span></span> <span data-ttu-id="fcc06-176">**SAML Single Sign-On을 사용하여 인증**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-176">Select **Authenticate using SAML Single Sign-On**.</span></span>

    <span data-ttu-id="fcc06-177">b.</span><span class="sxs-lookup"><span data-stu-id="fcc06-177">b.</span></span> <span data-ttu-id="fcc06-178">**SAML Single Sign-On 매개 변수 구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-178">Click **Configure SAML Single Sign-On Parameters**.</span></span>

11. <span data-ttu-id="fcc06-179">**SAML Single Sign-On 매개 변수 구성** 대화 상자 페이지에서 다음 단계를 수행하고 **완료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-179">On the **Configure SAML Single Sign-On Parameters** dialog page, perform the following steps, and then click **Done**</span></span>

    <span data-ttu-id="fcc06-180">![Single Sign-On](./media/active-directory-saas-zscaler-one-tutorial/ic800209.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="fcc06-180">![Single Sign-On](./media/active-directory-saas-zscaler-one-tutorial/ic800209.png "Single Sign-On")</span></span>
    
    <span data-ttu-id="fcc06-181">a.</span><span class="sxs-lookup"><span data-stu-id="fcc06-181">a.</span></span> <span data-ttu-id="fcc06-182">Azure Portal에서 복사한 **SAML Single Sign-On 서비스 URL** 값을 **URL of the SAML Portal to which users are sent for authentication**(인증할 사용자가 전송되는 SAML 포털의 URL) 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-182">Paste the **SAML Single Sign-On Service URL** value, which you have copied from the Azure portal into the **URL of the SAML Portal to which users are sent for authentication** textbox.</span></span>
    
    <span data-ttu-id="fcc06-183">b.</span><span class="sxs-lookup"><span data-stu-id="fcc06-183">b.</span></span> <span data-ttu-id="fcc06-184">**로그인 이름을 포함한 특성** 텍스트 상자에 **NameID**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-184">In the **Attribute containing Login Name** textbox, type **NameID**.</span></span>
    
    <span data-ttu-id="fcc06-185">c.</span><span class="sxs-lookup"><span data-stu-id="fcc06-185">c.</span></span> <span data-ttu-id="fcc06-186">**Zscaler pem**을 클릭하여 다운로드한 인증서를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-186">To upload your downloaded certificate, click **Zscaler pem**.</span></span>
    
    <span data-ttu-id="fcc06-187">d.</span><span class="sxs-lookup"><span data-stu-id="fcc06-187">d.</span></span> <span data-ttu-id="fcc06-188">**SAML 자동 프로비전 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-188">Select **Enable SAML Auto-Provisioning**.</span></span>

12. <span data-ttu-id="fcc06-189">**사용자 인증 구성** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-189">On the **Configure User Authentication** dialog page, perform the following steps:</span></span>

    <span data-ttu-id="fcc06-190">![관리](./media/active-directory-saas-zscaler-one-tutorial/ic800210.png "관리")</span><span class="sxs-lookup"><span data-stu-id="fcc06-190">![Administration](./media/active-directory-saas-zscaler-one-tutorial/ic800210.png "Administration")</span></span>
    
    <span data-ttu-id="fcc06-191">a.</span><span class="sxs-lookup"><span data-stu-id="fcc06-191">a.</span></span> <span data-ttu-id="fcc06-192">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-192">Click **Save**.</span></span>

    <span data-ttu-id="fcc06-193">b.</span><span class="sxs-lookup"><span data-stu-id="fcc06-193">b.</span></span> <span data-ttu-id="fcc06-194">**지금 활성화**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-194">Click **Activate Now**.</span></span>

## <a name="configuring-proxy-settings"></a><span data-ttu-id="fcc06-195">프록시 설정 구성</span><span class="sxs-lookup"><span data-stu-id="fcc06-195">Configuring proxy settings</span></span>
### <a name="to-configure-the-proxy-settings-in-internet-explorer"></a><span data-ttu-id="fcc06-196">Internet Explorer에서 프록시 설정을 구성하려면</span><span class="sxs-lookup"><span data-stu-id="fcc06-196">To configure the proxy settings in Internet Explorer</span></span>

1. <span data-ttu-id="fcc06-197">**Internet Explorer**를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-197">Start **Internet Explorer**.</span></span>

2. <span data-ttu-id="fcc06-198">**도구** 메뉴에서 **인터넷 옵션**을 선택하여 **인터넷 옵션** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-198">Select **Internet options** from the **Tools** menu for open the **Internet Options** dialog.</span></span>   
    
     <span data-ttu-id="fcc06-199">![인터넷 옵션](./media/active-directory-saas-zscaler-one-tutorial/ic769492.png "인터넷 옵션")</span><span class="sxs-lookup"><span data-stu-id="fcc06-199">![Internet Options](./media/active-directory-saas-zscaler-one-tutorial/ic769492.png "Internet Options")</span></span>

3. <span data-ttu-id="fcc06-200">**연결** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-200">Click the **Connections** tab.</span></span>   
  
     <span data-ttu-id="fcc06-201">![연결](./media/active-directory-saas-zscaler-one-tutorial/ic769493.png "연결")</span><span class="sxs-lookup"><span data-stu-id="fcc06-201">![Connections](./media/active-directory-saas-zscaler-one-tutorial/ic769493.png "Connections")</span></span>

4. <span data-ttu-id="fcc06-202">**LAN 설정**을 클릭하여 **LAN 설정** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-202">Click **LAN settings** to open the **LAN Settings** dialog.</span></span>

5. <span data-ttu-id="fcc06-203">프록시 서버 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-203">In the Proxy server section, perform the following steps:</span></span>   
   
    <span data-ttu-id="fcc06-204">![프록시 서버](./media/active-directory-saas-zscaler-one-tutorial/ic769494.png "프록시 서버")</span><span class="sxs-lookup"><span data-stu-id="fcc06-204">![Proxy server](./media/active-directory-saas-zscaler-one-tutorial/ic769494.png "Proxy server")</span></span>

    <span data-ttu-id="fcc06-205">a.</span><span class="sxs-lookup"><span data-stu-id="fcc06-205">a.</span></span> <span data-ttu-id="fcc06-206">**사용자 LAN의 프록시 서버 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-206">Select **Use a proxy server for your LAN**.</span></span>

    <span data-ttu-id="fcc06-207">b.</span><span class="sxs-lookup"><span data-stu-id="fcc06-207">b.</span></span> <span data-ttu-id="fcc06-208">주소 텍스트 상자에 **gateway.zscalerone.net**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-208">In the Address textbox, type **gateway.zscalerone.net**.</span></span>

    <span data-ttu-id="fcc06-209">c.</span><span class="sxs-lookup"><span data-stu-id="fcc06-209">c.</span></span> <span data-ttu-id="fcc06-210">포트 텍스트 상자에 **80**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-210">In the Port textbox, type **80**.</span></span>

    <span data-ttu-id="fcc06-211">d.</span><span class="sxs-lookup"><span data-stu-id="fcc06-211">d.</span></span> <span data-ttu-id="fcc06-212">**로컬 주소의 바이패스 프록시 서버**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-212">Select **Bypass proxy server for local addresses**.</span></span>

    <span data-ttu-id="fcc06-213">e.</span><span class="sxs-lookup"><span data-stu-id="fcc06-213">e.</span></span> <span data-ttu-id="fcc06-214">**확인**을 클릭하여 **LAN(Local Area Network) 설정** 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-214">Click **OK** to close the **Local Area Network (LAN) Settings** dialog.</span></span>

6. <span data-ttu-id="fcc06-215">**확인**을 클릭하여 **인터넷 옵션** 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-215">Click **OK** to close the **Internet Options** dialog.</span></span>

> [!TIP]
> <span data-ttu-id="fcc06-216">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-216">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="fcc06-217">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-217">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="fcc06-218">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-218">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="fcc06-219">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="fcc06-219">Creating an Azure AD test user</span></span>
<span data-ttu-id="fcc06-220">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-220">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="fcc06-222">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="fcc06-222">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="fcc06-223">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-223">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-zscaler-one-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="fcc06-225">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-225">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-zscaler-one-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="fcc06-227">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-227">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-zscaler-one-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="fcc06-229">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-229">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-zscaler-one-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="fcc06-231">a.</span><span class="sxs-lookup"><span data-stu-id="fcc06-231">a.</span></span> <span data-ttu-id="fcc06-232">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-232">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fcc06-233">b.</span><span class="sxs-lookup"><span data-stu-id="fcc06-233">b.</span></span> <span data-ttu-id="fcc06-234">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-234">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="fcc06-235">c.</span><span class="sxs-lookup"><span data-stu-id="fcc06-235">c.</span></span> <span data-ttu-id="fcc06-236">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-236">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="fcc06-237">d.</span><span class="sxs-lookup"><span data-stu-id="fcc06-237">d.</span></span> <span data-ttu-id="fcc06-238">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-238">Click **Create**.</span></span>
 
### <a name="creating-a-zscaler-one-test-user"></a><span data-ttu-id="fcc06-239">Zscaler One 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="fcc06-239">Creating a Zscaler One test user</span></span>

<span data-ttu-id="fcc06-240">Azure AD 사용자가 Zscaler One에 로그인할 수 있도록 하려면 사용자 계정이 Zscaler Onedmfh 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-240">To enable Azure AD users to log in to Zscaler One, they must be provisioned to Zscaler One.</span></span> <span data-ttu-id="fcc06-241">Zscaler One의 경우, 수동으로 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-241">In the case of Zscaler One, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="fcc06-242">사용자 프로비저닝을 구성하려면</span><span class="sxs-lookup"><span data-stu-id="fcc06-242">To configure user provisioning, perform the following steps:</span></span>

1. <span data-ttu-id="fcc06-243">**Zscaler One** 테넌트에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-243">Log in to your **Zscaler One** tenant.</span></span>

2. <span data-ttu-id="fcc06-244">**관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-244">Click **Administration**.</span></span>   
   
    <span data-ttu-id="fcc06-245">![관리](./media/active-directory-saas-zscaler-one-tutorial/ic781035.png "관리")</span><span class="sxs-lookup"><span data-stu-id="fcc06-245">![Administration](./media/active-directory-saas-zscaler-one-tutorial/ic781035.png "Administration")</span></span>

3. <span data-ttu-id="fcc06-246">**사용자 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-246">Click **User Management**.</span></span>   
        
     <span data-ttu-id="fcc06-247">![추가](./media/active-directory-saas-zscaler-one-tutorial/ic781036.png "추가")</span><span class="sxs-lookup"><span data-stu-id="fcc06-247">![Add](./media/active-directory-saas-zscaler-one-tutorial/ic781036.png "Add")</span></span>

4. <span data-ttu-id="fcc06-248">**사용자** 탭에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-248">In the **Users** tab, click **Add**.</span></span>
      
    <span data-ttu-id="fcc06-249">![추가](./media/active-directory-saas-zscaler-one-tutorial/ic781037.png "추가")</span><span class="sxs-lookup"><span data-stu-id="fcc06-249">![Add](./media/active-directory-saas-zscaler-one-tutorial/ic781037.png "Add")</span></span>

5. <span data-ttu-id="fcc06-250">사용자 추가 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-250">In the Add User section, perform the following steps:</span></span>
        
    <span data-ttu-id="fcc06-251">![사용자 추가](./media/active-directory-saas-zscaler-one-tutorial/ic781038.png "사용자 추가")</span><span class="sxs-lookup"><span data-stu-id="fcc06-251">![Add User](./media/active-directory-saas-zscaler-one-tutorial/ic781038.png "Add User")</span></span>
   
    <span data-ttu-id="fcc06-252">a.</span><span class="sxs-lookup"><span data-stu-id="fcc06-252">a.</span></span> <span data-ttu-id="fcc06-253">**사용자ID**, **사용자 표시 이름**, **암호**, **암호 확인**을 입력하고, 프로비전할 유효한 Azure AD 계정의 **그룹** 및 **부서**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-253">Type the **UserID**, **User Display Name**, **Password**, **Confirm Password**, and then select **Groups** and the **Department** of a valid Azure AD account you want to provision.</span></span>

    <span data-ttu-id="fcc06-254">b.</span><span class="sxs-lookup"><span data-stu-id="fcc06-254">b.</span></span> <span data-ttu-id="fcc06-255">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-255">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="fcc06-256">다른 Zscaler One 사용자 계정 생성 도구 또는 Zscaler One에서 제공하는 API를 사용하여 Azure AD 사용자 계정을 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-256">You can use any other Zscaler One user account creation tools or APIs provided by Zscaler One to provision Azure AD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="fcc06-257">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="fcc06-257">Assigning the Azure AD test user</span></span>

<span data-ttu-id="fcc06-258">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Zscaler One에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-258">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Zscaler One.</span></span>

![사용자 할당][200] 

<span data-ttu-id="fcc06-260">**Zscaler One에 Britta Simon을 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="fcc06-260">**To assign Britta Simon to Zscaler One, perform the following steps:**</span></span>

1. <span data-ttu-id="fcc06-261">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-261">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="fcc06-263">응용 프로그램 목록에서 **Zscaler One**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-263">In the applications list, select **Zscaler One**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-zscaler-one-tutorial/tutorial_zscalerone_app.png) 

3. <span data-ttu-id="fcc06-265">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-265">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="fcc06-267">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-267">Click **Add** button.</span></span> <span data-ttu-id="fcc06-268">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-268">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="fcc06-270">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-270">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="fcc06-271">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-271">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fcc06-272">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-272">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="fcc06-273">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="fcc06-273">Testing single sign-on</span></span>

<span data-ttu-id="fcc06-274">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-274">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="fcc06-275">액세스 패널에서 Zscaler One 타일을 클릭하면 Zscaler One 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="fcc06-275">When you click the Zscaler One tile in the Access Panel, you should get automatically signed-on to your Zscaler One application.</span></span>
<span data-ttu-id="fcc06-276">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fcc06-276">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fcc06-277">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="fcc06-277">Additional resources</span></span>

* [<span data-ttu-id="fcc06-278">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="fcc06-278">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fcc06-279">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="fcc06-279">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_203.png

