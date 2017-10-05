---
title: "자습서: Optimizely와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 Optimizely 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28ef03e1-9aad-4301-af97-d94e853edc74
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 4d6f6da6bace09fbd6ab105530a1162653675c99
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-optimizely"></a><span data-ttu-id="60298-103">자습서: Optimizely와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="60298-103">Tutorial: Azure Active Directory integration with Optimizely</span></span>

<span data-ttu-id="60298-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Optimizely를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="60298-104">In this tutorial, you learn how to integrate Optimizely with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="60298-105">Optimizely를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="60298-105">Integrating Optimizely with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="60298-106">Optimizely 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60298-106">You can control in Azure AD who has access to Optimizely</span></span>
- <span data-ttu-id="60298-107">사용자가 해당 Azure AD 계정으로 Optimizely에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60298-107">You can enable your users to automatically get signed-on to Optimizely (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="60298-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60298-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="60298-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60298-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="60298-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="60298-110">Prerequisites</span></span>

<span data-ttu-id="60298-111">Optimizely와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="60298-111">To configure Azure AD integration with Optimizely, you need the following items:</span></span>

- <span data-ttu-id="60298-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="60298-112">An Azure AD subscription</span></span>
- <span data-ttu-id="60298-113">Optimizely Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="60298-113">An Optimizely single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="60298-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="60298-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="60298-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60298-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="60298-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="60298-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="60298-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60298-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="60298-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="60298-118">Scenario description</span></span>
<span data-ttu-id="60298-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="60298-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="60298-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60298-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="60298-121">갤러리에서 Optimizely 추가</span><span class="sxs-lookup"><span data-stu-id="60298-121">Adding Optimizely from the gallery</span></span>
2. <span data-ttu-id="60298-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="60298-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-optimizely-from-the-gallery"></a><span data-ttu-id="60298-123">갤러리에서 Optimizely 추가</span><span class="sxs-lookup"><span data-stu-id="60298-123">Adding Optimizely from the gallery</span></span>
<span data-ttu-id="60298-124">Optimizely의 Azure AD 통합을 구성하려면 갤러리의 Optimizely를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60298-124">To configure the integration of Optimizely into Azure AD, you need to add Optimizely from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="60298-125">**갤러리에서 Optimizely를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="60298-125">**To add Optimizely from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="60298-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60298-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="60298-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="60298-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="60298-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="60298-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="60298-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60298-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="60298-133">검색 상자에 **Optimizely**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="60298-133">In the search box, type **Optimizely**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_search.png)

5. <span data-ttu-id="60298-135">결과 창에서 **Optimizely**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="60298-135">In the results panel, select **Optimizely**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="60298-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="60298-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="60298-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Optimizely에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="60298-138">In this section, you configure and test Azure AD single sign-on with Optimizely based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="60298-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Optimizely 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60298-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Optimizely is to a user in Azure AD.</span></span> <span data-ttu-id="60298-140">즉, Azure AD 사용자와 Optimizely의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60298-140">In other words, a link relationship between an Azure AD user and the related user in Optimizely needs to be established.</span></span>

<span data-ttu-id="60298-141">이 연결 관계는 Azure AD의 **사용자 이름** 값을 Optimizely의 **Username** 값으로 할당하여 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="60298-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Optimizely.</span></span>

<span data-ttu-id="60298-142">Optimizely에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60298-142">To configure and test Azure AD single sign-on with Optimizely, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="60298-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="60298-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="60298-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="60298-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="60298-145">**[Optimizely 테스트 사용자 만들기](#creating-an-optimizely-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 Optimizely에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="60298-145">**[Creating an Optimizely test user](#creating-an-optimizely-test-user)** - to have a counterpart of Britta Simon in Optimizely that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="60298-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="60298-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="60298-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="60298-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="60298-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="60298-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="60298-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Optimizely 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="60298-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Optimizely application.</span></span>

<span data-ttu-id="60298-150">**Optimizely에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="60298-150">**To configure Azure AD single sign-on with Optimizely, perform the following steps:**</span></span>

1. <span data-ttu-id="60298-151">Azure Portal의 **Optimizely** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60298-151">In the Azure portal, on the **Optimizely** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="60298-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="60298-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_samlbase.png)

3. <span data-ttu-id="60298-155">**Optimizely 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="60298-155">On the **Optimizely Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_url.png)

    <span data-ttu-id="60298-157">a.</span><span class="sxs-lookup"><span data-stu-id="60298-157">a.</span></span> <span data-ttu-id="60298-158">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://app.optimizely.net/<instance name>`</span><span class="sxs-lookup"><span data-stu-id="60298-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://app.optimizely.net/<instance name>`</span></span>

    <span data-ttu-id="60298-159">b.</span><span class="sxs-lookup"><span data-stu-id="60298-159">b.</span></span> <span data-ttu-id="60298-160">**식별자** 텍스트 상자에 `urn:auth0:optimizely:contoso` 패턴으로 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="60298-160">In the **Identifier** textbox, type a URL using the following pattern:  `urn:auth0:optimizely:contoso`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="60298-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="60298-161">These values are not the real.</span></span> <span data-ttu-id="60298-162">자습서 뒷부분에 설명된 실제 로그온 URL 및 식별자로 값을 업데이트하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="60298-162">You will update the value with the actual Sign-on URL and Identifier, which is explained later in the tutorial.</span></span> 

4. <span data-ttu-id="60298-163">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="60298-163">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_certificate.png) 

5. <span data-ttu-id="60298-165">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60298-165">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-optimizely-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="60298-167">**Optimizely 구성** 섹션에서 **Optimizely 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="60298-167">On the **Optimizely Configuration** section, click **Configure Optimizely** to open **Configure sign-on** window.</span></span> <span data-ttu-id="60298-168">**빠른 참조 섹션**에서 **SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="60298-168">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_configure.png) 

7. <span data-ttu-id="60298-170">**Optimizely** 쪽에서 Single Sign-On을 구성하려면 Optimizely 계정 관리자에게 문의하여 다운로드한 **인증서(Base64)** 및 **SAML Single Sign-On 서비스 URL**을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="60298-170">To configure single sign-on on **Optimizely** side, contact your Optimizely Account Manager and provide the downloaded **Certificate (Base64)**, and **SAML Single Sign-On Service URL**.</span></span> 

8. <span data-ttu-id="60298-171">전자 메일에 대한 응답으로 Optimizely는 로그온 URL(SP에서 시작한 SSO) 및 식별자(서비스 공급자 엔터티 ID) 값을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="60298-171">In response to your email, Optimizely provides you with the Sign On URL (SP-initiated SSO) and the Identifier (Service Provider Entity ID) values.</span></span>

    <span data-ttu-id="60298-172">a.</span><span class="sxs-lookup"><span data-stu-id="60298-172">a.</span></span> <span data-ttu-id="60298-173">Optimizely에서 제공한 **SP 시작 SSO URL**을 복사하여 Azure Portal **Optimizely 도메인 및 URL** 섹션의 **로그온 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="60298-173">Copy the **SP-initiated SSO URL** provided by Optimizely, and paste into the **Sign On URL** textbox in **Optimizely Domain and URLs** section on Azure portal</span></span> 

    <span data-ttu-id="60298-174">b.</span><span class="sxs-lookup"><span data-stu-id="60298-174">b.</span></span> <span data-ttu-id="60298-175">Optimizely에서 제공한 **서비스 공급자 엔터티 ID**를 복사하여 Azure Portal **Optimizely 도메인 및 URL** 섹션의 **식별자** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="60298-175">Copy the **Service Provider Entity ID** provided by Optimizely, and paste into the **Identifier** textbox in **Optimizely Domain and URLs** section on Azure portal</span></span> 

9. <span data-ttu-id="60298-176">다른 브라우저 창에서 Optimizely 응용 프로그램에 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="60298-176">In a different browser window, sign-on to your Optimizely application.</span></span>

10. <span data-ttu-id="60298-177">오른쪽 위 구석에 있는 계정 이름을 클릭하고 **계정 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60298-177">Click you account name in the top right corner and then **Account Settings**.</span></span>
   
    ![Azure AD Single Sign-On](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_09.png)

11. <span data-ttu-id="60298-179">계정 탭에서 **개요** 섹션의 Single Sign-On 아래에 있는 **SSO 사용** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="60298-179">In the Account tab, check the box **Enable SSO** under Single Sign On in the **Overview** section.</span></span>
   
    ![Azure AD Single Sign-On](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_10.png)
    
12. <span data-ttu-id="60298-181">페이지 맨 아래에 있는 **저장**</span><span class="sxs-lookup"><span data-stu-id="60298-181">Click **Save**</span></span>

> [!TIP]
> <span data-ttu-id="60298-182">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60298-182">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="60298-183">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="60298-183">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="60298-184">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60298-184">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="60298-185">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="60298-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="60298-186">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="60298-186">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="60298-188">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="60298-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="60298-189">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60298-189">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-optimizely-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="60298-191">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60298-191">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-optimizely-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="60298-193">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60298-193">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-optimizely-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="60298-195">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="60298-195">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-optimizely-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="60298-197">a.</span><span class="sxs-lookup"><span data-stu-id="60298-197">a.</span></span> <span data-ttu-id="60298-198">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="60298-198">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="60298-199">b.</span><span class="sxs-lookup"><span data-stu-id="60298-199">b.</span></span> <span data-ttu-id="60298-200">**사용자 이름** 텍스트 상자에 Britta Simon의 **메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="60298-200">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="60298-201">c.</span><span class="sxs-lookup"><span data-stu-id="60298-201">c.</span></span> <span data-ttu-id="60298-202">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="60298-202">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="60298-203">d.</span><span class="sxs-lookup"><span data-stu-id="60298-203">d.</span></span> <span data-ttu-id="60298-204">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60298-204">Click **Create**.</span></span>
 
### <a name="creating-an-optimizely-test-user"></a><span data-ttu-id="60298-205">Optimizely 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="60298-205">Creating an Optimizely test user</span></span>

<span data-ttu-id="60298-206">이 섹션에서는 Optimizely에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="60298-206">In this section, you create a user called Britta Simon in Optimizely.</span></span>

1. <span data-ttu-id="60298-207">홈페이지에서 **Collaborators** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="60298-207">On the home page, select **Collaborators** tab.</span></span>

2. <span data-ttu-id="60298-208">프로젝트에 새 공동 작업자를 추가하려면 **New Collaborator** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60298-208">To add new collaborator to the project, click **New Collaborator**.</span></span>
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-optimizely-tutorial/create_aaduser_10.png)

3. <span data-ttu-id="60298-210">전자 메일 주소를 입력하고 역할을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="60298-210">Fill in the email address and assign them a role.</span></span> <span data-ttu-id="60298-211">**초대**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60298-211">Click **Invite**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-optimizely-tutorial/create_aaduser_11.png)

4. <span data-ttu-id="60298-213">테스트 사용자는 이메일 초대를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="60298-213">They receive an email invite.</span></span> <span data-ttu-id="60298-214">테스트 사용자는 이메일 주소를 사용하여 Optimizely에 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60298-214">Using the email address, they have to log in to Optimizely.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="60298-215">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="60298-215">Assigning the Azure AD test user</span></span>

<span data-ttu-id="60298-216">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Optimizely에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="60298-216">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Optimizely.</span></span>

![사용자 할당][200] 

<span data-ttu-id="60298-218">**Britta Simon을 Optimizely에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="60298-218">**To assign Britta Simon to Optimizely, perform the following steps:**</span></span>

1. <span data-ttu-id="60298-219">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60298-219">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="60298-221">응용 프로그램 목록에서 **Optimizely**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="60298-221">In the applications list, select **Optimizely**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_app.png) 

3. <span data-ttu-id="60298-223">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60298-223">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="60298-225">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60298-225">Click **Add** button.</span></span> <span data-ttu-id="60298-226">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="60298-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="60298-228">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="60298-228">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="60298-229">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60298-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="60298-230">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60298-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="60298-231">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="60298-231">Testing single sign-on</span></span>

<span data-ttu-id="60298-232">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="60298-232">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="60298-233">액세스 패널에서 Optimizely 타일을 클릭하면 Optimizely 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="60298-233">When you click the Optimizely tile in the Access Panel, you should get automatically signed-on to your Optimizely application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="60298-234">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="60298-234">Additional resources</span></span>

* [<span data-ttu-id="60298-235">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="60298-235">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="60298-236">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="60298-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_203.png

