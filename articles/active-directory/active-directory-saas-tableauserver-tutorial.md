---
title: "자습서: Tableau Server와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 Tableau Server 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c1917375-08aa-445c-a444-e22e23fa19e0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: 6b35609d88fbbf649e15863901d521886db2a4d6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tableau-server"></a><span data-ttu-id="87d5d-103">자습서: Tableau Server와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="87d5d-103">Tutorial: Azure Active Directory integration with Tableau Server</span></span>

<span data-ttu-id="87d5d-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Tableau Server를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-104">In this tutorial, you learn how to integrate Tableau Server with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="87d5d-105">Tableau Server를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-105">Integrating Tableau Server with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="87d5d-106">Tableau Server에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-106">You can control in Azure AD who has access to Tableau Server</span></span>
- <span data-ttu-id="87d5d-107">사용자가 해당 Azure AD 계정으로 Tableau Server에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-107">You can enable your users to automatically get signed-on to Tableau Server (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="87d5d-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="87d5d-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="87d5d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="87d5d-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="87d5d-110">Prerequisites</span></span>

<span data-ttu-id="87d5d-111">Tableau Server와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-111">To configure Azure AD integration with Tableau Server, you need the following items:</span></span>

- <span data-ttu-id="87d5d-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="87d5d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="87d5d-113">Tableau Server Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="87d5d-113">A Tableau Server single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="87d5d-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="87d5d-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="87d5d-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="87d5d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="87d5d-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="87d5d-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="87d5d-118">Scenario description</span></span>
<span data-ttu-id="87d5d-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="87d5d-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="87d5d-121">갤러리에서 Tableau Server 추가</span><span class="sxs-lookup"><span data-stu-id="87d5d-121">Adding Tableau Server from the gallery</span></span>
2. <span data-ttu-id="87d5d-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="87d5d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-tableau-server-from-the-gallery"></a><span data-ttu-id="87d5d-123">갤러리에서 Tableau Server 추가</span><span class="sxs-lookup"><span data-stu-id="87d5d-123">Adding Tableau Server from the gallery</span></span>
<span data-ttu-id="87d5d-124">Tableau Server의 Azure AD 통합을 구성하려면 갤러리의 Tableau Server를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-124">To configure the integration of Tableau Server into Azure AD, you need to add Tableau Server from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="87d5d-125">**갤러리에서 Tableau Server를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="87d5d-125">**To add Tableau Server from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="87d5d-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="87d5d-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="87d5d-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="87d5d-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="87d5d-133">검색 상자에 **Tableau Server**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-133">In the search box, type **Tableau Server**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_search.png)

5. <span data-ttu-id="87d5d-135">결과 창에서 **Tableau Server**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-135">In the results panel, select **Tableau Server**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="87d5d-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="87d5d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="87d5d-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Tableau Server에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-138">In this section, you configure and test Azure AD single sign-on with Tableau Server based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="87d5d-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Tableau Server 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Tableau Server is to a user in Azure AD.</span></span> <span data-ttu-id="87d5d-140">즉, Azure AD 사용자와 Tableau Server의 관련 사용자 간에 연결이 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-140">In other words, a link relationship between an Azure AD user and the related user in Tableau Server needs to be established.</span></span>

<span data-ttu-id="87d5d-141">Tableau Server에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 연결 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-141">In Tableau Server, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="87d5d-142">Tableau Server에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-142">To configure and test Azure AD single sign-on with Tableau Server, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="87d5d-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="87d5d-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="87d5d-145">**[Tableau Server 테스트 사용자 만들기](#creating-a-tableau-server-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 Tableau Server에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-145">**[Creating a Tableau Server test user](#creating-a-tableau-server-test-user)** - to have a counterpart of Britta Simon in Tableau Server that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="87d5d-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="87d5d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="87d5d-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="87d5d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="87d5d-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Tableau Server 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Tableau Server application.</span></span>

<span data-ttu-id="87d5d-150">**Tableau Server에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="87d5d-150">**To configure Azure AD single sign-on with Tableau Server, perform the following steps:**</span></span>

1. <span data-ttu-id="87d5d-151">Azure Portal의 **Tableau Server** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-151">In the Azure portal, on the **Tableau Server** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="87d5d-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_samlbase.png)

3. <span data-ttu-id="87d5d-155">**Tableau Server 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-155">On the **Tableau Server Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_url.png)

    <span data-ttu-id="87d5d-157">a.</span><span class="sxs-lookup"><span data-stu-id="87d5d-157">a.</span></span> <span data-ttu-id="87d5d-158">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://azure.<domain name>.link`</span><span class="sxs-lookup"><span data-stu-id="87d5d-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://azure.<domain name>.link`</span></span>
    
    <span data-ttu-id="87d5d-159">b.</span><span class="sxs-lookup"><span data-stu-id="87d5d-159">b.</span></span> <span data-ttu-id="87d5d-160">**식별자** 텍스트 상자에서 `https://azure.<domain name>.link` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-160">In the **Identifier** textbox, type a URL using the following pattern: `https://azure.<domain name>.link`</span></span>

    <span data-ttu-id="87d5d-161">c.</span><span class="sxs-lookup"><span data-stu-id="87d5d-161">c.</span></span> <span data-ttu-id="87d5d-162">**회신 URL** 텍스트 상자에 다음 패턴으로 URL을 입력합니다.`https://azure.<domain name>.link/wg/saml/SSO/index.html`</span><span class="sxs-lookup"><span data-stu-id="87d5d-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://azure.<domain name>.link/wg/saml/SSO/index.html`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="87d5d-163">위의 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-163">The preceding values are not real values.</span></span> <span data-ttu-id="87d5d-164">나중에 이 값을 Tableau Server 구성 페이지의 실제 URL과 식별자로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-164">Later, you update the values with the actual URL and identifier from the Tableau Server configuration page.</span></span> 

4. <span data-ttu-id="87d5d-165">Tableau Server 응용 프로그램은 특정 형식의 SAML 어설션이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-165">Tableau Server application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="87d5d-166">이 응용 프로그램에 대해 다음 클레임을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-166">Configure the following claims for this application.</span></span> <span data-ttu-id="87d5d-167">응용 프로그램 통합 페이지의 **"사용자 특성"** 섹션에서 이러한 특성의 값을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-167">You can manage the values of these attributes from the **"User Attributes"** section on application integration page.</span></span> <span data-ttu-id="87d5d-168">다음 스크린샷은 동일 상황에 대한 예를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-168">The following screenshot shows an example for the same.</span></span>
    
    ![Single Sign-on 구성](./media/active-directory-saas-tableauserver-tutorial/3.png)
    
5. <span data-ttu-id="87d5d-170">**Single sign-on** 대화 상자의 **사용자 특성** 섹션에서 위의 이미지에 표시된 것과 같이 SAML 토큰 특성을 구성하고 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-170">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="87d5d-171">특성 이름</span><span class="sxs-lookup"><span data-stu-id="87d5d-171">Attribute Name</span></span> | <span data-ttu-id="87d5d-172">특성 값</span><span class="sxs-lookup"><span data-stu-id="87d5d-172">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="87d5d-173">username</span><span class="sxs-lookup"><span data-stu-id="87d5d-173">username</span></span> | <span data-ttu-id="87d5d-174">*user.displayname*</span><span class="sxs-lookup"><span data-stu-id="87d5d-174">*user.displayname*</span></span> |

    <span data-ttu-id="87d5d-175">a.</span><span class="sxs-lookup"><span data-stu-id="87d5d-175">a.</span></span> <span data-ttu-id="87d5d-176">**특성 추가**를 클릭하여 **특성 추가** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-176">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-tableauserver-tutorial/tutorial_officespace_04.png)

    ![Single Sign-on 구성](./media/active-directory-saas-tableauserver-tutorial/tutorial_officespace_05.png)
    
    <span data-ttu-id="87d5d-179">b.</span><span class="sxs-lookup"><span data-stu-id="87d5d-179">b.</span></span> <span data-ttu-id="87d5d-180">**이름** 텍스트 상자에서 해당 행에 표시된 특성 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-180">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="87d5d-181">c.</span><span class="sxs-lookup"><span data-stu-id="87d5d-181">c.</span></span> <span data-ttu-id="87d5d-182">**값** 목록에서 해당 행에 대해 표시된 특성을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-182">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="87d5d-183">d.</span><span class="sxs-lookup"><span data-stu-id="87d5d-183">d.</span></span> <span data-ttu-id="87d5d-184">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-184">Click **Ok**</span></span>


6. <span data-ttu-id="87d5d-185">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 메타데이터 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-185">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_certificate.png) 

7. <span data-ttu-id="87d5d-187">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-187">Click **Save** button.</span></span>

    <span data-ttu-id="87d5d-188">![Single Sign-On 구성](./media/active-directory-saas-tableauserver-tutorial/tutorial_general_400.png)
<CS></span><span class="sxs-lookup"><span data-stu-id="87d5d-188">![Configure Single Sign-On](./media/active-directory-saas-tableauserver-tutorial/tutorial_general_400.png)
<CS></span></span>
8. <span data-ttu-id="87d5d-189">응용 프로그램에 대해 구성된 SSO를 가져오려면 관리자 권한으로 Tableau Server 테넌트에 로그온해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-189">To get SSO configured for your application, you need to sign-on to your Tableau Server tenant as an administrator.</span></span>
   
   <span data-ttu-id="87d5d-190">a.</span><span class="sxs-lookup"><span data-stu-id="87d5d-190">a.</span></span> <span data-ttu-id="87d5d-191">Tableau Server 구성에서 **SAML** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-191">In the Tableau Server configuration, click the **SAML** tab.</span></span>
  
    ![Single Sign-On 구성](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_001.png) 
  
   <span data-ttu-id="87d5d-193">b.</span><span class="sxs-lookup"><span data-stu-id="87d5d-193">b.</span></span> <span data-ttu-id="87d5d-194">**Single Sign-On에 SAML 사용**확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-194">Select the checkbox of **Use SAML for single sign-on**.</span></span>
   
   <span data-ttu-id="87d5d-195">c.</span><span class="sxs-lookup"><span data-stu-id="87d5d-195">c.</span></span> <span data-ttu-id="87d5d-196">Tableau Server 반환 URL - Tableau Server 사용자가 액세스하는 URL예: http://tableau_server 입니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-196">Tableau Server return URL—The URL that Tableau Server users will be accessing, such as http://tableau_server.</span></span> <span data-ttu-id="87d5d-197">http://localhost 를 사용하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-197">Using http://localhost is not recommended.</span></span> <span data-ttu-id="87d5d-198">후행 슬래시가 있는 URL(예: http://tableau_server/)은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-198">Using a URL with a trailing slash (for example, http://tableau_server/) is not supported.</span></span> <span data-ttu-id="87d5d-199">**Tableau Server 반환 URL**을 복사하여 **Tableau Server 도메인 및 URL** 섹션의 Azure AD **로그온 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-199">Copy **Tableau Server return URL** and paste it to Azure AD **Sign On URL** textbox in **Tableau Server Domain and URLs** section.</span></span>
   
   <span data-ttu-id="87d5d-200">d.</span><span class="sxs-lookup"><span data-stu-id="87d5d-200">d.</span></span> <span data-ttu-id="87d5d-201">SAML 엔터티 ID - 엔터티 ID는 IdP에 대한 Tableau Server 설치를 고유하게 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-201">SAML entity ID—The entity ID uniquely identifies your Tableau Server installation to the IdP.</span></span> <span data-ttu-id="87d5d-202">원하는 경우 여기에 Tableau Server URL을 다시 입력할 수 있지만 반드시 Tableau Server URL을 입력해야 하는 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-202">You can enter your Tableau Server URL again here, if you like, but it does not have to be your Tableau Server URL.</span></span> <span data-ttu-id="87d5d-203">**SAML 엔터티 ID**를 복사하여 **Tableau Server 도메인 및 URL** 섹션의 Azure AD **식별자** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-203">Copy **SAML entity ID** and paste it to Azure AD **Identifier** textbox in **Tableau Server Domain and URLs** section.</span></span>
     
   <span data-ttu-id="87d5d-204">e.</span><span class="sxs-lookup"><span data-stu-id="87d5d-204">e.</span></span> <span data-ttu-id="87d5d-205">**메타데이터 파일 내보내기**를 클릭하여 텍스트 편집기 응용 프로그램에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-205">Click the **Export Metadata File** and open it in the text editor application.</span></span> <span data-ttu-id="87d5d-206">Http Post 및 인덱스 0이 포함된 어설션 소비자 서비스 URL을 찾아서 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-206">Locate Assertion Consumer Service URL with Http Post and Index 0 and copy the URL.</span></span> <span data-ttu-id="87d5d-207">**Tableau Server 도메인 및 URL** 섹션의 Azure AD **응답 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-207">Now paste it to Azure AD **Reply URL** textbox in **Tableau Server Domain and URLs** section.</span></span>
   
   <span data-ttu-id="87d5d-208">f.</span><span class="sxs-lookup"><span data-stu-id="87d5d-208">f.</span></span> <span data-ttu-id="87d5d-209">Azure Portal에서 다운로드한 페더레이션 메타데이터 파일을 찾은 다음 **SAML Idp 메타데이터 파일**에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-209">Locate your Federation Metadata file downloaded from Azure portal, and then upload it in the **SAML Idp metadata file**.</span></span>
   
   <span data-ttu-id="87d5d-210">g.</span><span class="sxs-lookup"><span data-stu-id="87d5d-210">g.</span></span> <span data-ttu-id="87d5d-211">Tableau Server 구성 페이지에서 **확인** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-211">Click the **OK** button in the Tableau Server Configuration page.</span></span>
   
    >[!NOTE] 
    ><span data-ttu-id="87d5d-212">고객은 Tableau Server SAML SSO 구성의 모든 인증서를 업로드해야 하며, 인증서는 SSO 흐름에서 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-212">Customer have to upload any certificate in the Tableau Server SAML SSO configuration and it will get ignored in the SSO flow.</span></span>
    ><span data-ttu-id="87d5d-213">Tableau Server에서 SAML을 구성하는 데 도움이 필요한 경우 [SAML 구성](http://onlinehelp.tableau.com/current/server/en-us/config_saml.htm) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="87d5d-213">If you need help configuring SAML on Tableau Server then please refer to this article [Configure SAML](http://onlinehelp.tableau.com/current/server/en-us/config_saml.htm).</span></span>
    >
<CE>

> [!TIP]
> <span data-ttu-id="87d5d-214">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-214">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="87d5d-215">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-215">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="87d5d-216">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-216">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="87d5d-217">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="87d5d-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="87d5d-218">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-218">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="87d5d-220">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="87d5d-220">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="87d5d-221">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-221">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="87d5d-223">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-223">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="87d5d-225">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-225">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="87d5d-227">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-227">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="87d5d-229">a.</span><span class="sxs-lookup"><span data-stu-id="87d5d-229">a.</span></span> <span data-ttu-id="87d5d-230">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-230">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="87d5d-231">b.</span><span class="sxs-lookup"><span data-stu-id="87d5d-231">b.</span></span> <span data-ttu-id="87d5d-232">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-232">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="87d5d-233">c.</span><span class="sxs-lookup"><span data-stu-id="87d5d-233">c.</span></span> <span data-ttu-id="87d5d-234">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-234">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="87d5d-235">d.</span><span class="sxs-lookup"><span data-stu-id="87d5d-235">d.</span></span> <span data-ttu-id="87d5d-236">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-236">Click **Create**.</span></span>
 
### <a name="creating-a-tableau-server-test-user"></a><span data-ttu-id="87d5d-237">Tableau Server 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="87d5d-237">Creating a Tableau Server test user</span></span>

<span data-ttu-id="87d5d-238">이 섹션은 Tableau Server에서 Britta Simon이라는 사용자를 만들기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-238">The objective of this section is to create a user called Britta Simon in Tableau Server.</span></span> <span data-ttu-id="87d5d-239">Tableau Server의 모든 사용자를 프로비전해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-239">You need to provision all the users in the Tableau server.</span></span> 

<span data-ttu-id="87d5d-240">사용자의 사용자 이름은 Azure AD에서 구성한 사용자 지정 특성 **username**의 값과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-240">That username of the user should match the value which you have configured in the Azure AD custom attribute of **username**.</span></span> <span data-ttu-id="87d5d-241">올바른 매핑을 사용해야 통합 시 [Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)이 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-241">With the correct mapping the integration should work [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span></span>

>[!NOTE]
><span data-ttu-id="87d5d-242">사용자를 수동으로 만들어야 하는 경우 조직의 Tableau Server 관리자에게 문의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-242">If you need to create a user manually, you need to contact the Tableau Server administrator in your organization.</span></span>
> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="87d5d-243">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="87d5d-243">Assigning the Azure AD test user</span></span>

<span data-ttu-id="87d5d-244">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Tableau Server에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-244">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Tableau Server.</span></span>

![사용자 할당][200] 

<span data-ttu-id="87d5d-246">**Britta Simon을 Tableau Server에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="87d5d-246">**To assign Britta Simon to Tableau Server, perform the following steps:**</span></span>

1. <span data-ttu-id="87d5d-247">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-247">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="87d5d-249">응용 프로그램 목록에서 **Tableau Server**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-249">In the applications list, select **Tableau Server**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_app.png) 

3. <span data-ttu-id="87d5d-251">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-251">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="87d5d-253">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-253">Click **Add** button.</span></span> <span data-ttu-id="87d5d-254">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="87d5d-256">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-256">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="87d5d-257">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="87d5d-258">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="87d5d-259">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="87d5d-259">Testing single sign-on</span></span>

<span data-ttu-id="87d5d-260">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-260">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="87d5d-261">액세스 패널에서 Tableau Server 타일을 클릭하면 Tableau Server 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="87d5d-261">When you click the Tableau Server tile in the Access Panel, you should get automatically signed-on to your Tableau Server application.</span></span>
<span data-ttu-id="87d5d-262">액세스 패널에 대한 자세한 내용은 [Azure 시작](https://msdn.microsoft.com/library/dn308586)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="87d5d-262">For more information about the Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="87d5d-263">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="87d5d-263">Additional resources</span></span>

* [<span data-ttu-id="87d5d-264">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="87d5d-264">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="87d5d-265">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="87d5d-265">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_203.png

