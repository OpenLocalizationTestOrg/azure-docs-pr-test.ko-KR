---
title: "자습서:Azure Active Directory와 Hosted Graphite 통합 | Microsoft Docs"
description: "Azure Active Directory와 Hosted Graphite 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a1ac4d7f-d079-4f3c-b6da-0f520d427ceb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: f6ed02cc67be4090402a115c30819ff6cff99c99
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hosted-graphite"></a><span data-ttu-id="f7131-103">자습서:Azure Active Directory와 Hosted Graphite 통합</span><span class="sxs-lookup"><span data-stu-id="f7131-103">Tutorial: Azure Active Directory integration with Hosted Graphite</span></span>

<span data-ttu-id="f7131-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Hosted Graphite를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-104">In this tutorial, you learn how to integrate Hosted Graphite with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f7131-105">Hosted Graphite를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-105">Integrating Hosted Graphite with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f7131-106">Hosted Graphite에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-106">You can control in Azure AD who has access to Hosted Graphite</span></span>
- <span data-ttu-id="f7131-107">사용자가 해당 Azure AD 계정으로 Hosted Graphite에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-107">You can enable your users to automatically get signed-on to Hosted Graphite (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f7131-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f7131-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f7131-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f7131-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="f7131-110">Prerequisites</span></span>

<span data-ttu-id="f7131-111">Hosted Graphite와의 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-111">To configure Azure AD integration with Hosted Graphite, you need the following items:</span></span>

- <span data-ttu-id="f7131-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="f7131-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f7131-113">Hosted Graphite Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="f7131-113">A Hosted Graphite single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f7131-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f7131-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f7131-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="f7131-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f7131-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f7131-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="f7131-118">Scenario description</span></span>
<span data-ttu-id="f7131-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f7131-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f7131-121">갤러리에서 Hosted Graphite 추가</span><span class="sxs-lookup"><span data-stu-id="f7131-121">Adding Hosted Graphite from the gallery</span></span>
2. <span data-ttu-id="f7131-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="f7131-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hosted-graphite-from-the-gallery"></a><span data-ttu-id="f7131-123">갤러리에서 Hosted Graphite 추가</span><span class="sxs-lookup"><span data-stu-id="f7131-123">Adding Hosted Graphite from the gallery</span></span>
<span data-ttu-id="f7131-124">Hosted Graphite의 Azure AD 통합을 구성하려면 갤러리의 Hosted Graphite를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-124">To configure the integration of Hosted Graphite into Azure AD, you need to add Hosted Graphite from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f7131-125">**갤러리에서 Hosted Graphite를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="f7131-125">**To add Hosted Graphite from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f7131-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f7131-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f7131-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="f7131-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="f7131-133">검색 상자에 **Hosted Graphite**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-133">In the search box, type **Hosted Graphite**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_search.png)

5. <span data-ttu-id="f7131-135">결과 패널에서 **Hosted Graphite**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-135">In the results panel, select **Hosted Graphite**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f7131-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="f7131-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f7131-138">이 섹션에서는 “Britta Simon”이라는 테스트 사용자를 기반으로 Hosted Graphite에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-138">In this section, you configure and test Azure AD single sign-on with Hosted Graphite based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f7131-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD의 사용자에 해당하는 Hosted Graphite의 사용자가 누군지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Hosted Graphite is to a user in Azure AD.</span></span> <span data-ttu-id="f7131-140">즉, Azure AD 사용자와 Hosted Graphite의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-140">In other words, a link relationship between an Azure AD user and the related user in Hosted Graphite needs to be established.</span></span>

<span data-ttu-id="f7131-141">Hosted Graphite에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-141">In Hosted Graphite, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f7131-142">Hosted Graphite에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-142">To configure and test Azure AD single sign-on with Hosted Graphite, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f7131-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f7131-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f7131-145">**[Hosted Graphite 테스트 사용자 만들기](#creating-a-hosted-graphite-test-user)** - Britta Simon의 Azure AD 사용자 표현과 연결되는 대응 사용자를 Hosted Graphite에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-145">**[Creating a Hosted Graphite test user](#creating-a-hosted-graphite-test-user)** - to have a counterpart of Britta Simon in Hosted Graphite that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f7131-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f7131-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f7131-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="f7131-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f7131-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Hosted Graphite 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Hosted Graphite application.</span></span>

<span data-ttu-id="f7131-150">**Hosted Graphite에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="f7131-150">**To configure Azure AD single sign-on with Hosted Graphite, perform the following steps:**</span></span>

1. <span data-ttu-id="f7131-151">Azure Portal의 **Hosted Graphite** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-151">In the Azure portal, on the **Hosted Graphite** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="f7131-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_samlbase.png)

3. <span data-ttu-id="f7131-155">**Hosted Graphite 도메인 및 URL** 섹션에서 **IDP 시작 모드**로 응용 프로그램을 구성하려는 경우 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-155">On the **Hosted Graphite Domain and URLs** section, if you wish to configure the application in **IDP initiated mode**, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_url.png)

    <span data-ttu-id="f7131-157">a.</span><span class="sxs-lookup"><span data-stu-id="f7131-157">a.</span></span> <span data-ttu-id="f7131-158">**식별자** 텍스트 상자에서 `https://www.hostedgraphite.com/metadata/<user id>` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-158">In the **Identifier** textbox, type a URL using the following pattern: `https://www.hostedgraphite.com/metadata/<user id>`</span></span>

    <span data-ttu-id="f7131-159">b.</span><span class="sxs-lookup"><span data-stu-id="f7131-159">b.</span></span> <span data-ttu-id="f7131-160">**회신 URL** 텍스트 상자에 다음 패턴으로 URL을 입력합니다.`https://www.hostedgraphite.com/complete/saml/<user id>`</span><span class="sxs-lookup"><span data-stu-id="f7131-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://www.hostedgraphite.com/complete/saml/<user id>`</span></span>

4. <span data-ttu-id="f7131-161">**Hosted Graphite 도메인 및 URL** 섹션에서 **SP 시작 모드**로 응용 프로그램을 구성하려는 경우 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-161">On the **Hosted Graphite Domain and URLs** section, if you wish to configure the application in **SP initiated mode**, perform the following steps:</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_10.png)
  
    <span data-ttu-id="f7131-163">a.</span><span class="sxs-lookup"><span data-stu-id="f7131-163">a.</span></span> <span data-ttu-id="f7131-164">**고급 URL 설정 표시** 옵션을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-164">Click on the **Show advanced URL settings** option</span></span>

    <span data-ttu-id="f7131-165">b.</span><span class="sxs-lookup"><span data-stu-id="f7131-165">b.</span></span> <span data-ttu-id="f7131-166">**로그온 URL** 텍스트 상자에서 다음 패턴 `https://www.hostedgraphite.com/login/saml/<user id>/`을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-166">In the **Sign On URL** textbox, type a URL using the following pattern: `https://www.hostedgraphite.com/login/saml/<user id>/`</span></span>   

    > [!NOTE] 
    > <span data-ttu-id="f7131-167">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-167">Please note that these are not the real values.</span></span> <span data-ttu-id="f7131-168">실제 식별자, 회신 URL 및 로그온 URL로 이러한 값을 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-168">You have to update these values with the actual Identifier, Reply URL and Sign On URL.</span></span> <span data-ttu-id="f7131-169">이러한 값을 얻으려면 응용 프로그램 쪽에서 액세스->SAML 설정으로 이동하거나 [Hosted Graphite 지원 팀](mailto:help@hostedgraphite.com)에 문의하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-169">To get these values, you can go to Access->SAML setup on your Application side or Contact [Hosted Graphite support team](mailto:help@hostedgraphite.com).</span></span>
    >
 
5. <span data-ttu-id="f7131-170">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-170">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_certificate.png) 

6. <span data-ttu-id="f7131-172">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-172">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="f7131-174">**Hosted Graphite 구성** 섹션에서 **Hosted Graphite 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-174">On the **Hosted Graphite Configuration** section, click **Configure Hosted Graphite** to open **Configure sign-on** window.</span></span> <span data-ttu-id="f7131-175">**빠른 참조 섹션**에서 **SAML 엔터티 ID 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-175">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_configure.png) 

8. <span data-ttu-id="f7131-177">Hosted Graphite 테넌트에 관리자 권한으로 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-177">Sign-on to your Hosted Graphite tenant as an administrator.</span></span>

9. <span data-ttu-id="f7131-178">세로 막대에서 **SAML 설정 페이지**로 이동합니다(**액세스 -> SAML 설정**).</span><span class="sxs-lookup"><span data-stu-id="f7131-178">Go to the **SAML Setup page** in the sidebar (**Access -> SAML Setup**).</span></span>
   
    ![앱 쪽에서 Single Sign-On 구성](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_000.png)

10. <span data-ttu-id="f7131-180">이러한 URl가 Azure Portal의 **Hosted Graphite 도메인 및 URL** 섹션에서 수행한 구성과 일치하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-180">Confirm these URls match your configuration done on the **Hosted Graphite Domain and URLs** section of the Azure portal.</span></span>
   
    ![앱 쪽에서 Single Sign-On 구성](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_001.png)

11. <span data-ttu-id="f7131-182">Azure Portal에서 복사한 **SAML 엔터티 ID** 및 **SAML Single Sign-On 서비스 URL** 값을 **엔터티 또는 발급자 ID** 및 **SSO 로그인 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-182">In  **Entity or Issuer ID** and **SSO Login URL** textboxes, paste the value of **SAML Entity ID** and **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 
   
    ![앱 쪽에서 Single Sign-On 구성](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_002.png)
   

12. <span data-ttu-id="f7131-184">"**읽기 전용**"을 **기본 사용자 역할**로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-184">Select "**Read-only**" as **Default User Role**.</span></span>
    
    ![앱 쪽에서 Single Sign-On 구성](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_004.png)

13. <span data-ttu-id="f7131-186">Azure Portal에서 다운로드한 base-64로 인코딩된 인증서를 메모장에서 열고, 콘텐츠를 클립보드에 복사한 다음, **X.509 인증서** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-186">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox.</span></span>
    
    ![앱 쪽에서 Single Sign-On 구성](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_005.png)

14. <span data-ttu-id="f7131-188">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-188">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="f7131-189">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f7131-190">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f7131-191">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f7131-192">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="f7131-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="f7131-193">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="f7131-195">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="f7131-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f7131-196">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-hostedgraphite-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f7131-198">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-hostedgraphite-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f7131-200">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-hostedgraphite-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f7131-202">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-hostedgraphite-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f7131-204">a.</span><span class="sxs-lookup"><span data-stu-id="f7131-204">a.</span></span> <span data-ttu-id="f7131-205">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f7131-206">b.</span><span class="sxs-lookup"><span data-stu-id="f7131-206">b.</span></span> <span data-ttu-id="f7131-207">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f7131-208">c.</span><span class="sxs-lookup"><span data-stu-id="f7131-208">c.</span></span> <span data-ttu-id="f7131-209">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f7131-210">d.</span><span class="sxs-lookup"><span data-stu-id="f7131-210">d.</span></span> <span data-ttu-id="f7131-211">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-211">Click **Create**.</span></span>
 
### <a name="creating-a-hosted-graphite-test-user"></a><span data-ttu-id="f7131-212">Hosted Graphite 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="f7131-212">Creating a Hosted Graphite test user</span></span>

<span data-ttu-id="f7131-213">이 섹션은 Hosted Graphite에서 Britta Simon이라는 사용자를 만들기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-213">The objective of this section is to create a user called Britta Simon in Hosted Graphite.</span></span> <span data-ttu-id="f7131-214">Hosted Graphite는 적시에 프로비전을 지원하며 기본적으로 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-214">Hosted Graphite supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="f7131-215">이 섹션에 작업 항목이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-215">There is no action item for you in this section.</span></span> <span data-ttu-id="f7131-216">새 사용자가 아직 존재하지 않는 경우 Hosted Graphite에 액세스하는 동안 만들어질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-216">A new user will be created during an attempt to access Hosted Graphite if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="f7131-217">사용자를 수동으로 만들어야 하는 경우 <mailto:help@hostedgraphite.com>을 통해 Hosted Graphite 지원 팀에 문의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-217">If you need to create a user manually, you need to contact the Hosted Graphite support team via <mailto:help@hostedgraphite.com>.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f7131-218">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="f7131-218">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f7131-219">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Hosted Graphite에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-219">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Hosted Graphite.</span></span>

![사용자 할당][200] 

<span data-ttu-id="f7131-221">**Britta Simon을 Hosted Graphite에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="f7131-221">**To assign Britta Simon to Hosted Graphite, perform the following steps:**</span></span>

1. <span data-ttu-id="f7131-222">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-222">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="f7131-224">응용 프로그램 목록에서 **Hosted Graphite**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-224">In the applications list, select **Hosted Graphite**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_app.png) 

3. <span data-ttu-id="f7131-226">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-226">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="f7131-228">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-228">Click **Add** button.</span></span> <span data-ttu-id="f7131-229">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="f7131-231">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-231">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f7131-232">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f7131-233">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f7131-234">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="f7131-234">Testing single sign-on</span></span>

<span data-ttu-id="f7131-235">이 섹션은 액세스 패널을 사용하여 Azure AD SSO 구성을 테스트하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-235">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="f7131-236">액세스 패널에서 Hosted Graphite 타일을 클릭하면 Hosted Graphite 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7131-236">When you click the Hosted Graphite tile in the Access Panel, you should get automatically signed-on to your Hosted Graphite application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f7131-237">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="f7131-237">Additional resources</span></span>

* [<span data-ttu-id="f7131-238">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="f7131-238">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f7131-239">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="f7131-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_203.png

