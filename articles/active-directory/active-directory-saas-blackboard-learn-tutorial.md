---
title: "자습서: Blackboard Learn과 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 Blackboard Learn 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0b8ca505-61ea-487c-9a3e-fa50c936df0c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: jeedes
ms.openlocfilehash: c2b7638e99fa46ff41a7f2202bdf0e7a2b017c19
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-blackboard-learn"></a><span data-ttu-id="bae9b-103">자습서: Blackboard Learn과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="bae9b-103">Tutorial: Azure Active Directory integration with Blackboard Learn</span></span>

<span data-ttu-id="bae9b-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Blackboard Learn을 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-104">In this tutorial, you learn how to integrate Blackboard Learn with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bae9b-105">Blackboard Learn을 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-105">Integrating Blackboard Learn with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="bae9b-106">Blackboard Learn에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-106">You can control in Azure AD who has access to Blackboard Learn</span></span>
- <span data-ttu-id="bae9b-107">사용자가 해당 Azure AD 계정으로 Blackboard Learn에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-107">You can enable your users to automatically get signed-on to Blackboard Learn (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bae9b-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="bae9b-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bae9b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bae9b-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="bae9b-110">Prerequisites</span></span>

<span data-ttu-id="bae9b-111">Blackboard Learn과 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-111">To configure Azure AD integration with Blackboard Learn, you need the following items:</span></span>

- <span data-ttu-id="bae9b-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="bae9b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bae9b-113">Blackboard Learn Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="bae9b-113">A Blackboard Learn single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bae9b-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bae9b-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bae9b-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="bae9b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bae9b-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bae9b-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="bae9b-118">Scenario description</span></span>
<span data-ttu-id="bae9b-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bae9b-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bae9b-121">갤러리에서 Blackboard Learn 추가</span><span class="sxs-lookup"><span data-stu-id="bae9b-121">Adding Blackboard Learn from the gallery</span></span>
2. <span data-ttu-id="bae9b-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="bae9b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-blackboard-learn-from-the-gallery"></a><span data-ttu-id="bae9b-123">갤러리에서 Blackboard Learn 추가</span><span class="sxs-lookup"><span data-stu-id="bae9b-123">Adding Blackboard Learn from the gallery</span></span>
<span data-ttu-id="bae9b-124">Blackboard Learn의 Azure AD 통합을 구성하려면 갤러리의 Blackboard Learn을 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-124">To configure the integration of Blackboard Learn into Azure AD, you need to add Blackboard Learn from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="bae9b-125">**갤러리에서 Blackboard Learn을 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="bae9b-125">**To add Blackboard Learn from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="bae9b-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="bae9b-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="bae9b-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="bae9b-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="bae9b-133">검색 상자에 **Blackboard Learn**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-133">In the search box, type **Blackboard Learn**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_search.png)

5. <span data-ttu-id="bae9b-135">결과 패널에서 **Blackboard Learn**을 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-135">In the results panel, select **Blackboard Learn**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bae9b-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="bae9b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bae9b-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Blackboard Learn에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-138">In this section, you configure and test Azure AD single sign-on with Blackboard Learn based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="bae9b-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Blackboard Learn 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Blackboard Learn is to a user in Azure AD.</span></span> <span data-ttu-id="bae9b-140">즉, Azure AD 사용자와 Blackboard Learn의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-140">In other words, a link relationship between an Azure AD user and the related user in Blackboard Learn needs to be established.</span></span>

<span data-ttu-id="bae9b-141">이 연결 관계는 Azure AD의 **사용자 이름** 값을 Blackboard Learn의 **Username** 값으로 할당하여 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Blackboard Learn.</span></span>

<span data-ttu-id="bae9b-142">Blackboard Learn에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-142">To configure and test Azure AD single sign-on with Blackboard Learn, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="bae9b-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="bae9b-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bae9b-145">**[Blackboard Learn 테스트 사용자 만들기](#creating-a-blackboard-learn-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 Blackboard Learn에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-145">**[Creating a Blackboard Learn test user](#creating-a-blackboard-learn-test-user)** - to have a counterpart of Britta Simon in Blackboard Learn that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="bae9b-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bae9b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bae9b-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="bae9b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bae9b-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Blackboard Learn 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Blackboard Learn application.</span></span>

<span data-ttu-id="bae9b-150">**Blackboard Learn에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="bae9b-150">**To configure Azure AD single sign-on with Blackboard Learn, perform the following steps:**</span></span>

1. <span data-ttu-id="bae9b-151">Azure Portal의 **Blackboard Learn** 응용 프로그램 통합 페이지에서 **Single sign-on**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-151">In the Azure portal, on the **Blackboard Learn** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="bae9b-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_samlbase.png)

3. <span data-ttu-id="bae9b-155">**Blackboard Learn 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-155">On the **Blackboard Learn Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_url.png)

    <span data-ttu-id="bae9b-157">a.</span><span class="sxs-lookup"><span data-stu-id="bae9b-157">a.</span></span> <span data-ttu-id="bae9b-158">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<subdomain>.blackboard.com/`</span><span class="sxs-lookup"><span data-stu-id="bae9b-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.blackboard.com/`</span></span>

    <span data-ttu-id="bae9b-159">b.</span><span class="sxs-lookup"><span data-stu-id="bae9b-159">b.</span></span> <span data-ttu-id="bae9b-160">**식별자** 텍스트 상자에서 `https://<subdomain>.blackboard.com/auth-saml/saml/SSO/entity-id/SAML_AD` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.blackboard.com/auth-saml/saml/SSO/entity-id/SAML_AD`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="bae9b-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-161">These values are not real.</span></span> <span data-ttu-id="bae9b-162">실제 로그온 URL 및 식별자로 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="bae9b-163">이러한 값을 얻으려면 [Blackboard Learn 클라이언트 지원팀](https://www.blackboard.com/support/index.aspx)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="bae9b-163">Contact [Blackboard Learn Client support team](https://www.blackboard.com/support/index.aspx) to get these values.</span></span> 

4. <span data-ttu-id="bae9b-164">Blackboard Learn 응용 프로그램은 특정 형식의 SAML 어설션이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-164">Blackboard Learn application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="bae9b-165">이 응용 프로그램에 대해 다음 클레임을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-165">Configure the following claims for this application.</span></span> <span data-ttu-id="bae9b-166">응용 프로그램 통합 페이지의 **사용자 특성** 섹션에서 이러한 특성의 값을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-166">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span></span>
 <span data-ttu-id="bae9b-167">다음 스크린샷에서는 이에 대한 예제를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-167">The following screenshot shows an example about it.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_attribute.png)

5. <span data-ttu-id="bae9b-169">**Single Sign-On** 대화 상자의 **사용자 특성** 섹션에서 이미지에 표시된 것과 같이 SAML 토큰 특성을 구성하고 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-169">In the **User Attributes** section on **Single sign-on** dialog, configure SAML token attributes as shown in the image and perform the following steps.</span></span> <span data-ttu-id="bae9b-170">여기서는 Userprincipalname을 고유한 사용자 특성으로 매핑했지만 조직의 사용자를 고유하게 식별하고 Blackboard Learn 사용자 이름 필드에 매핑하는 적합한 값에 매핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-170">We have mapped the Userprincipalname as the unique user attribute here but you can map it to the appropriate value, which uniquely distinguishes the user in the organization and that maps to Blackboard Learn username field.</span></span>
           
    | <span data-ttu-id="bae9b-171">특성 이름</span><span class="sxs-lookup"><span data-stu-id="bae9b-171">Attribute Name</span></span> | <span data-ttu-id="bae9b-172">특성 값</span><span class="sxs-lookup"><span data-stu-id="bae9b-172">Attribute Value</span></span> |   
    | ---------------| ----------------|
    | <span data-ttu-id="bae9b-173">urn:oid:1.3.6.1.4.1.5923.1.1.1.6</span><span class="sxs-lookup"><span data-stu-id="bae9b-173">urn:oid:1.3.6.1.4.1.5923.1.1.1.6</span></span> |<span data-ttu-id="bae9b-174">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="bae9b-174">user.userprincipalname</span></span> |

    <span data-ttu-id="bae9b-175">a.</span><span class="sxs-lookup"><span data-stu-id="bae9b-175">a.</span></span> <span data-ttu-id="bae9b-176">**특성 추가**를 클릭하여 **특성 추가** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-176">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_attribute_04.png)
    
    ![Single Sign-on 구성](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="bae9b-179">b.</span><span class="sxs-lookup"><span data-stu-id="bae9b-179">b.</span></span> <span data-ttu-id="bae9b-180">**이름** 텍스트 상자에서 해당 행에 표시된 특성 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-180">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="bae9b-181">c.</span><span class="sxs-lookup"><span data-stu-id="bae9b-181">c.</span></span> <span data-ttu-id="bae9b-182">**값** 목록에서 해당 행에 대해 표시된 특성을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-182">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="bae9b-183">d.</span><span class="sxs-lookup"><span data-stu-id="bae9b-183">d.</span></span> <span data-ttu-id="bae9b-184">**Ok**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-184">Click **Ok**.</span></span>

4. <span data-ttu-id="bae9b-185">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 XML 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-185">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_certificate.png)

7. <span data-ttu-id="bae9b-187">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-187">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="bae9b-189">**Blackboard Learn 구성** 섹션에서 **Blackboard Learn 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-189">On the **Blackboard Learn Configuration** section, click **Configure Blackboard Learn** to open **Configure sign-on** window.</span></span> <span data-ttu-id="bae9b-190">**빠른 참조 섹션**에서 **SAML 엔터티 ID**를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-190">Copy the **SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_configure.png) 

9. <span data-ttu-id="bae9b-192">**Blackboard Learn** 쪽에서 Single Sign-On을 구성하려면 다운로드한 **메타데이터 XML** 및, **SAML 엔터티 ID**를 [Blackboard Learn 지원](https://www.blackboard.com/support/index.aspx)으로 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-192">To configure single sign-on on **Blackboard Learn** side, you need to send the downloaded **Metadata XML** and **SAML Entity ID** to [Blackboard Learn support](https://www.blackboard.com/support/index.aspx).</span></span>

> [!TIP]
> <span data-ttu-id="bae9b-193">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-193">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="bae9b-194">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-194">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="bae9b-195">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-195">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bae9b-196">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="bae9b-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="bae9b-197">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-197">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="bae9b-199">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="bae9b-199">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="bae9b-200">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-200">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bae9b-202">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-202">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bae9b-204">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-204">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bae9b-206">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-206">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bae9b-208">a.</span><span class="sxs-lookup"><span data-stu-id="bae9b-208">a.</span></span> <span data-ttu-id="bae9b-209">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-209">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bae9b-210">b.</span><span class="sxs-lookup"><span data-stu-id="bae9b-210">b.</span></span> <span data-ttu-id="bae9b-211">**사용자 이름** 텍스트 상자에 Britta Simon의 **메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-211">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="bae9b-212">c.</span><span class="sxs-lookup"><span data-stu-id="bae9b-212">c.</span></span> <span data-ttu-id="bae9b-213">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-213">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="bae9b-214">d.</span><span class="sxs-lookup"><span data-stu-id="bae9b-214">d.</span></span> <span data-ttu-id="bae9b-215">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-215">Click **Create**.</span></span>
 
### <a name="creating-a-blackboard-learn-test-user"></a><span data-ttu-id="bae9b-216">Blackboard Learn 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="bae9b-216">Creating a Blackboard Learn test user</span></span>
<span data-ttu-id="bae9b-217">이 섹션에서는 Blackboard Learn에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-217">In this section, you create a user called Britta Simon in Blackboard Learn.</span></span> 

<span data-ttu-id="bae9b-218">Blackboard Learn 응용 프로그램은 적절한 사용자 프로비전을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-218">Blackboard Learn application support just in time user provisioning.</span></span> <span data-ttu-id="bae9b-219">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** 섹션에서 설명한 대로 클레임을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-219">Make sure that you have configured the claims as described in the section **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**</span></span>
### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="bae9b-220">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="bae9b-220">Assigning the Azure AD test user</span></span>

<span data-ttu-id="bae9b-221">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Blackboard Learn에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Blackboard Learn.</span></span>

![사용자 할당][200] 

<span data-ttu-id="bae9b-223">**Britta Simon을 Blackboard Learn에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="bae9b-223">**To assign Britta Simon to Blackboard Learn, perform the following steps:**</span></span>

1. <span data-ttu-id="bae9b-224">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="bae9b-226">응용 프로그램 목록에서 **Blackboard Learn**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-226">In the applications list, select **Blackboard Learn**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_app.png) 

3. <span data-ttu-id="bae9b-228">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-228">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="bae9b-230">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-230">Click **Add** button.</span></span> <span data-ttu-id="bae9b-231">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="bae9b-233">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="bae9b-234">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bae9b-235">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bae9b-236">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="bae9b-236">Testing single sign-on</span></span>

<span data-ttu-id="bae9b-237">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="bae9b-238">액세스 패널에서 Blackboard Learn 타일을 클릭하면 Blackboard Learn 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="bae9b-238">When you click the Blackboard Learn tile in the Access Panel, you should get automatically signed-on to your Blackboard Learn application.</span></span> <span data-ttu-id="bae9b-239">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bae9b-239">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="bae9b-240">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="bae9b-240">Additional resources</span></span>

* [<span data-ttu-id="bae9b-241">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="bae9b-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bae9b-242">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="bae9b-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_203.png

