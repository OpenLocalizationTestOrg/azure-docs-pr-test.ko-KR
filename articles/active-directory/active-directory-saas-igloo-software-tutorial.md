---
title: "자습서: Igloo Software와 Azure Active Directory 통합| Microsoft Azure"
description: "Azure Active Directory 및 Igloo Software 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2eb625c1-d3fc-4ae1-a304-6a6733a10e6e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: ab3891e11eb33b4d233e4fc967a40c7df06e4f4e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-igloo-software"></a><span data-ttu-id="b84d2-103">자습서: Igloo Software와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="b84d2-103">Tutorial: Azure Active Directory integration with Igloo Software</span></span>

<span data-ttu-id="b84d2-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Igloo Software를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-104">In this tutorial, you learn how to integrate Igloo Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b84d2-105">Igloo Software를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-105">Integrating Igloo Software with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b84d2-106">Igloo Software에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-106">You can control in Azure AD who has access to Igloo Software</span></span>
- <span data-ttu-id="b84d2-107">사용자가 해당 Azure AD 계정으로 Igloo Software에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-107">You can enable your users to automatically get signed-on to Igloo Software (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b84d2-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b84d2-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b84d2-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b84d2-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="b84d2-110">Prerequisites</span></span>

<span data-ttu-id="b84d2-111">Igloo Software와의 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-111">To configure Azure AD integration with Igloo Software, you need the following items:</span></span>

- <span data-ttu-id="b84d2-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="b84d2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b84d2-113">Igloo Software Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="b84d2-113">An Igloo Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b84d2-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b84d2-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b84d2-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="b84d2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b84d2-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b84d2-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="b84d2-118">Scenario description</span></span>
<span data-ttu-id="b84d2-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b84d2-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b84d2-121">갤러리에서 Igloo Software 추가</span><span class="sxs-lookup"><span data-stu-id="b84d2-121">Adding Igloo Software from the gallery</span></span>
2. <span data-ttu-id="b84d2-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="b84d2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-igloo-software-from-the-gallery"></a><span data-ttu-id="b84d2-123">갤러리에서 Igloo Software 추가</span><span class="sxs-lookup"><span data-stu-id="b84d2-123">Adding Igloo Software from the gallery</span></span>
<span data-ttu-id="b84d2-124">Igloo Software의 Azure AD 통합을 구성하려면 갤러리의 Igloo Software를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-124">To configure the integration of Igloo Software into Azure AD, you need to add Igloo Software from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b84d2-125">**갤러리에서 Igloo Software를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="b84d2-125">**To add Igloo Software from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b84d2-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b84d2-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b84d2-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="b84d2-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="b84d2-133">검색 상자에 **Igloo Software**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-133">In the search box, type **Igloo Software**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_search.png)

5. <span data-ttu-id="b84d2-135">결과 패널에서 **Igloo Software**를 선택한 다음 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-135">In the results panel, select **Igloo Software**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b84d2-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="b84d2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b84d2-138">이 섹션에서는 “Britta Simon”이라는 테스트 사용자를 기반으로 Igloo Software에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-138">In this section, you configure and test Azure AD single sign-on with Igloo Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b84d2-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD의 사용자에 해당하는 Igloo Software의 사용자가 누군지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Igloo Software is to a user in Azure AD.</span></span> <span data-ttu-id="b84d2-140">즉, Azure AD 사용자와 Igloo Software의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-140">In other words, a link relationship between an Azure AD user and the related user in Igloo Software needs to be established.</span></span>

<span data-ttu-id="b84d2-141">Igloo Software에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-141">In Igloo Software, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b84d2-142">Igloo Software에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-142">To configure and test Azure AD single sign-on with Igloo Software, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b84d2-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b84d2-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b84d2-145">**[Igloo Software 테스트 사용자 만들기](#creating-an-igloo-software-test-user)** - Britta Simon의 Azure AD 사용자 표현과 연결되는 대응 사용자를 Igloo Software에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-145">**[Creating an Igloo Software test user](#creating-an-igloo-software-test-user)** - to have a counterpart of Britta Simon in Igloo Software that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b84d2-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b84d2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b84d2-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="b84d2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b84d2-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Igloo Software 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Igloo Software application.</span></span>

<span data-ttu-id="b84d2-150">**Igloo Software에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="b84d2-150">**To configure Azure AD single sign-on with Igloo Software, perform the following steps:**</span></span>

1. <span data-ttu-id="b84d2-151">Azure Portal의 **Igloo Software** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-151">In the Azure portal, on the **Igloo Software** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="b84d2-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_samlbase.png)

3. <span data-ttu-id="b84d2-155">**Igloo Software 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-155">On the **Igloo Software Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_url.png)
    
    <span data-ttu-id="b84d2-157">a.</span><span class="sxs-lookup"><span data-stu-id="b84d2-157">a.</span></span> <span data-ttu-id="b84d2-158">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<company name>.igloocommmunities.com`</span><span class="sxs-lookup"><span data-stu-id="b84d2-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.igloocommmunities.com`</span></span>

    <span data-ttu-id="b84d2-159">b.</span><span class="sxs-lookup"><span data-stu-id="b84d2-159">b.</span></span> <span data-ttu-id="b84d2-160">**식별자** 텍스트 상자에서 `https://<company name>.igloocommmunities.com/saml.digest` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.igloocommmunities.com/saml.digest`</span></span>

    <span data-ttu-id="b84d2-161">c.</span><span class="sxs-lookup"><span data-stu-id="b84d2-161">c.</span></span> <span data-ttu-id="b84d2-162">**회신 URL** 텍스트 상자에 다음 패턴으로 URL을 입력합니다.`https://<company name>.igloocommmunities.com/saml.digest`</span><span class="sxs-lookup"><span data-stu-id="b84d2-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.igloocommmunities.com/saml.digest`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b84d2-163">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-163">These values are not real.</span></span> <span data-ttu-id="b84d2-164">이러한 값을 실제 식별자, 회신 URL 및 로그온 URL로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-164">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="b84d2-165">이러한 값을 얻으려면 [Igloo Software 클라이언트 지원 팀](https://www.igloosoftware.com/services/support)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="b84d2-165">Contact [Igloo Software Client support team](https://www.igloosoftware.com/services/support) to get these values.</span></span> 

4. <span data-ttu-id="b84d2-166">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-166">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_certificate.png) 

5. <span data-ttu-id="b84d2-168">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-168">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-igloo-software-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="b84d2-170">**Igloo Software 구성** 섹션에서 **Igloo Software 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-170">On the **Igloo Software Configuration** section, click **Configure Igloo Software** to open **Configure sign-on** window.</span></span> <span data-ttu-id="b84d2-171">**빠른 참조 섹션**에서 **로그아웃 URL 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-171">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_configure.png) 

7. <span data-ttu-id="b84d2-173">다른 웹 브라우저 창에서 Igloo Software 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-173">In a different web browser window, log in to your Igloo Software company site as an administrator.</span></span>

8. <span data-ttu-id="b84d2-174">**제어판**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-174">Go to the **Control Panel**.</span></span>
   
     <span data-ttu-id="b84d2-175">![제어판](./media/active-directory-saas-igloo-software-tutorial/ic799949.png "제어판")</span><span class="sxs-lookup"><span data-stu-id="b84d2-175">![Control Panel](./media/active-directory-saas-igloo-software-tutorial/ic799949.png "Control Panel")</span></span>

9. <span data-ttu-id="b84d2-176">**멤버 자격** 탭을 클릭하고 **로그인 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-176">In the **Membership** tab, click **Sign In Settings**.</span></span>
   
    <span data-ttu-id="b84d2-177">![로그인 설정](./media/active-directory-saas-igloo-software-tutorial/ic783968.png "로그인 설정")</span><span class="sxs-lookup"><span data-stu-id="b84d2-177">![Sign in Settings](./media/active-directory-saas-igloo-software-tutorial/ic783968.png "Sign in Settings")</span></span>

10. <span data-ttu-id="b84d2-178">SAML 구성 섹션에서 **SAML 인증 구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-178">In the SAML Configuration section, click **Configure SAML Authentication**.</span></span>
   
    <span data-ttu-id="b84d2-179">![SAML 구성](./media/active-directory-saas-igloo-software-tutorial/ic783969.png "SAML 구성")</span><span class="sxs-lookup"><span data-stu-id="b84d2-179">![SAML Configuration](./media/active-directory-saas-igloo-software-tutorial/ic783969.png "SAML Configuration")</span></span>
   
11. <span data-ttu-id="b84d2-180">**일반 구성** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-180">In the **General Configuration** section, perform the following steps:</span></span>
   
    <span data-ttu-id="b84d2-181">![일반 구성](./media/active-directory-saas-igloo-software-tutorial/ic783970.png "일반 구성")</span><span class="sxs-lookup"><span data-stu-id="b84d2-181">![General Configuration](./media/active-directory-saas-igloo-software-tutorial/ic783970.png "General Configuration")</span></span>

    <span data-ttu-id="b84d2-182">a.</span><span class="sxs-lookup"><span data-stu-id="b84d2-182">a.</span></span> <span data-ttu-id="b84d2-183">**연결 이름** 텍스트 상자에 구성의 사용자 지정 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-183">In the **Connection Name** textbox, type a custom name for your configuration.</span></span>
   
    <span data-ttu-id="b84d2-184">b.</span><span class="sxs-lookup"><span data-stu-id="b84d2-184">b.</span></span> <span data-ttu-id="b84d2-185">Azure Portal에서 복사한 **SAML Single Sign-On 서비스 URL** 값을 **IdP 로그인 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-185">In the **IdP Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="b84d2-186">c.</span><span class="sxs-lookup"><span data-stu-id="b84d2-186">c.</span></span> <span data-ttu-id="b84d2-187">Azure Portal에서 복사한 **로그아웃 URL** 값을 **IdP 로그아웃 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-187">In the **IdP Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="b84d2-188">d.</span><span class="sxs-lookup"><span data-stu-id="b84d2-188">d.</span></span> <span data-ttu-id="b84d2-189">**로그아웃 응답 및 요청 HTTP 형식**을 **POST**로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-189">Select **Logout Response and Request HTTP Type** as **POST**.</span></span>
   
    <span data-ttu-id="b84d2-190">e.</span><span class="sxs-lookup"><span data-stu-id="b84d2-190">e.</span></span> <span data-ttu-id="b84d2-191">Azure Portal에서 다운로드한 **base-64**로 인코딩된 인증서를 메모장에서 열고, 콘텐츠를 클립보드에 복사한 다음, **공용 인증서** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-191">Open your **base-64** encoded certificate in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **Public Certificate** textbox.</span></span>
    
12. <span data-ttu-id="b84d2-192">**응답 및 인증 구성**에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-192">In the **Response and Authentication Configuration**, perform the following steps:</span></span>
    
    <span data-ttu-id="b84d2-193">![응답 및 인증 구성](./media/active-directory-saas-igloo-software-tutorial/IC783971.png "응답 및 인증 구성")</span><span class="sxs-lookup"><span data-stu-id="b84d2-193">![Response and Authentication Configuration](./media/active-directory-saas-igloo-software-tutorial/IC783971.png "Response and Authentication Configuration")</span></span>
  
      <span data-ttu-id="b84d2-194">a.</span><span class="sxs-lookup"><span data-stu-id="b84d2-194">a.</span></span> <span data-ttu-id="b84d2-195">**ID 공급자**로 **Microsoft ADFS**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-195">As **Identity Provider**, select **Microsoft ADFS**.</span></span>
      
      <span data-ttu-id="b84d2-196">b.</span><span class="sxs-lookup"><span data-stu-id="b84d2-196">b.</span></span> <span data-ttu-id="b84d2-197">**ID 형식**으로 **전자 메일 주소**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-197">As **Identifier Type**, select **Email Address**.</span></span> 

      <span data-ttu-id="b84d2-198">c.</span><span class="sxs-lookup"><span data-stu-id="b84d2-198">c.</span></span> <span data-ttu-id="b84d2-199">**이메일 특성** 텍스트 상자에 **emailaddress**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-199">In the **Email Attribute** textbox, type **emailaddress**.</span></span>

      <span data-ttu-id="b84d2-200">d.</span><span class="sxs-lookup"><span data-stu-id="b84d2-200">d.</span></span> <span data-ttu-id="b84d2-201">**이름 특성** 텍스트 상자에 **givenname**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-201">In the **First Name Attribute** textbox, type **givenname**.</span></span>

      <span data-ttu-id="b84d2-202">e.</span><span class="sxs-lookup"><span data-stu-id="b84d2-202">e.</span></span> <span data-ttu-id="b84d2-203">**성 특성** 텍스트 상자에 **surname**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-203">In the **Last Name Attribute** textbox, type **surname**.</span></span>

13. <span data-ttu-id="b84d2-204">다음 단계를 수행하여 구성을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-204">Perform the following steps to complete the configuration:</span></span>
    
    <span data-ttu-id="b84d2-205">![로그인할 때 사용자 만들기](./media/active-directory-saas-igloo-software-tutorial/IC783972.png "로그인할 때 사용자 만들기")</span><span class="sxs-lookup"><span data-stu-id="b84d2-205">![User creation on Sign in](./media/active-directory-saas-igloo-software-tutorial/IC783972.png "User creation on Sign in")</span></span> 

     <span data-ttu-id="b84d2-206">a.</span><span class="sxs-lookup"><span data-stu-id="b84d2-206">a.</span></span> <span data-ttu-id="b84d2-207">**로그인할 때 사용자 만들기**에서 **로그인할 때 사이트에 새 사용자 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-207">As **User creation on Sign in**, select **Create a new user in your site when they sign in**.</span></span>

     <span data-ttu-id="b84d2-208">b.</span><span class="sxs-lookup"><span data-stu-id="b84d2-208">b.</span></span> <span data-ttu-id="b84d2-209">**로그인 설정**에서 **"로그인" 화면에서 SAML 단추 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-209">As **Sign in Settings**, select **Use SAML button on “Sign in” screen**.</span></span>

     <span data-ttu-id="b84d2-210">c.</span><span class="sxs-lookup"><span data-stu-id="b84d2-210">c.</span></span> <span data-ttu-id="b84d2-211">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-211">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="b84d2-212">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-212">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b84d2-213">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-213">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b84d2-214">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-214">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b84d2-215">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="b84d2-215">Creating an Azure AD test user</span></span>
<span data-ttu-id="b84d2-216">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-216">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="b84d2-218">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="b84d2-218">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b84d2-219">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-219">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b84d2-221">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-221">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b84d2-223">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-223">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b84d2-225">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-225">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b84d2-227">a.</span><span class="sxs-lookup"><span data-stu-id="b84d2-227">a.</span></span> <span data-ttu-id="b84d2-228">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-228">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b84d2-229">b.</span><span class="sxs-lookup"><span data-stu-id="b84d2-229">b.</span></span> <span data-ttu-id="b84d2-230">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-230">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b84d2-231">c.</span><span class="sxs-lookup"><span data-stu-id="b84d2-231">c.</span></span> <span data-ttu-id="b84d2-232">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-232">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b84d2-233">d.</span><span class="sxs-lookup"><span data-stu-id="b84d2-233">d.</span></span> <span data-ttu-id="b84d2-234">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-234">Click **Create**.</span></span>
 
### <a name="creating-an-igloo-software-test-user"></a><span data-ttu-id="b84d2-235">Igloo Software 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="b84d2-235">Creating an Igloo Software test user</span></span>

<span data-ttu-id="b84d2-236">Igloo Software를 프로비저닝하는 사용자를 구성할 작업 항목이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-236">There is no action item for you to configure user provisioning to Igloo Software.</span></span>  

<span data-ttu-id="b84d2-237">할당된 사용자가 액세스 패널을 사용하여 Igloo Software에 로그인을 시도하면 Igloo Software는 사용자가 존재하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-237">When an assigned user tries to log in to Igloo Software using the access panel, Igloo Software checks whether the user exists.</span></span>  <span data-ttu-id="b84d2-238">사용할 수 있는 사용자 계정이 없으면 자동으로 Igloo Software에서 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-238">If there is no user account available yet, it is automatically created by Igloo Software.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b84d2-239">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="b84d2-239">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b84d2-240">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Igloo Software에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-240">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Igloo Software.</span></span>

![사용자 할당][200] 

<span data-ttu-id="b84d2-242">**Britta Simon을 Igloo Software에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="b84d2-242">**To assign Britta Simon to Igloo Software, perform the following steps:**</span></span>

1. <span data-ttu-id="b84d2-243">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-243">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="b84d2-245">응용 프로그램 목록에서 **Igloo Software**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-245">In the applications list, select **Igloo Software**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_app.png) 

3. <span data-ttu-id="b84d2-247">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-247">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="b84d2-249">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-249">Click **Add** button.</span></span> <span data-ttu-id="b84d2-250">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="b84d2-252">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-252">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b84d2-253">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b84d2-254">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b84d2-255">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="b84d2-255">Testing single sign-on</span></span>

<span data-ttu-id="b84d2-256">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-256">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b84d2-257">액세스 패널에서 Igloo Software 타일을 클릭하면 Igloo Software 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="b84d2-257">When you click the Igloo Software tile in the Access Panel, you should get automatically signed-on to your Igloo Software application.</span></span>
<span data-ttu-id="b84d2-258">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b84d2-258">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="b84d2-259">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="b84d2-259">Additional resources</span></span>

* [<span data-ttu-id="b84d2-260">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="b84d2-260">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b84d2-261">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="b84d2-261">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_203.png

