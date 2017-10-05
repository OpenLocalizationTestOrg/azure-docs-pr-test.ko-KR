---
title: "자습서: Learningpool Act와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 Learningpool Act 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 51e8695f-31e1-4d09-8eb3-13241999d99f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 932f5f12c75299e532d3fa2c31f1805a7df30158
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-learningpool-act"></a><span data-ttu-id="d3af9-103">자습서: Learningpool Act와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="d3af9-103">Tutorial: Azure Active Directory integration with Learningpool Act</span></span>

<span data-ttu-id="d3af9-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Learningpool Act를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-104">In this tutorial, you learn how to integrate Learningpool Act with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d3af9-105">Learningpool Act를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-105">Integrating Learningpool Act with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d3af9-106">Learningpool Act에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-106">You can control in Azure AD who has access to Learningpool Act</span></span>
- <span data-ttu-id="d3af9-107">사용자가 해당 Azure AD 계정으로 Learningpool Act에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-107">You can enable your users to automatically get signed-on to Learningpool Act (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d3af9-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d3af9-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d3af9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d3af9-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d3af9-110">Prerequisites</span></span>

<span data-ttu-id="d3af9-111">Learningpool Act와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-111">To configure Azure AD integration with Learningpool Act, you need the following items:</span></span>

- <span data-ttu-id="d3af9-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="d3af9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d3af9-113">Learningpool Act Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="d3af9-113">A Learningpool Act single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d3af9-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d3af9-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d3af9-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="d3af9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d3af9-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d3af9-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="d3af9-118">Scenario description</span></span>
<span data-ttu-id="d3af9-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d3af9-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d3af9-121">갤러리에서 Learningpool Act 추가</span><span class="sxs-lookup"><span data-stu-id="d3af9-121">Adding Learningpool Act from the gallery</span></span>
2. <span data-ttu-id="d3af9-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="d3af9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-learningpool-act-from-the-gallery"></a><span data-ttu-id="d3af9-123">갤러리에서 Learningpool Act 추가</span><span class="sxs-lookup"><span data-stu-id="d3af9-123">Adding Learningpool Act from the gallery</span></span>
<span data-ttu-id="d3af9-124">Learningpool Act와 Azure AD의 통합을 구성하려면 갤러리의 Learningpool Act를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-124">To configure the integration of Learningpool Act into Azure AD, you need to add Learningpool Act from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d3af9-125">**갤러리에서 Learningpool Act를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="d3af9-125">**To add Learningpool Act from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d3af9-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d3af9-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d3af9-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="d3af9-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="d3af9-133">검색 상자에서 **Learningpool Act**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-133">In the search box, type **Learningpool Act**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_search.png)

5. <span data-ttu-id="d3af9-135">결과 패널에서 **Learningpool Act**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-135">In the results panel, select **Learningpool Act**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d3af9-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="d3af9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d3af9-138">이 섹션에서는 “Britta Simon”이라는 테스트 사용자를 기반으로 Learningpool Act에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-138">In this section, you configure and test Azure AD single sign-on with Learningpool Act based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d3af9-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Learningpool Act 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Learningpool Act is to a user in Azure AD.</span></span> <span data-ttu-id="d3af9-140">즉, Azure AD 사용자와 Learningpool Act의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-140">In other words, a link relationship between an Azure AD user and the related user in Learningpool Act needs to be established.</span></span>

<span data-ttu-id="d3af9-141">Learningpool Act에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-141">In Learningpool Act, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d3af9-142">Learningpool Act에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-142">To configure and test Azure AD single sign-on with Learningpool Act, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d3af9-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d3af9-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d3af9-145">**[Learningpool Act 테스트 사용자 만들기](#creating-a-learningpool-act-test-user)** - Britta Simon의 Azure AD 표현과 연결되는 대응 사용자를 Learningpool Act에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-145">**[Creating a Learningpool Act test user](#creating-a-learningpool-act-test-user)** - to have a counterpart of Britta Simon in Learningpool Act that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d3af9-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d3af9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d3af9-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="d3af9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d3af9-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Learningpool Act 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Learningpool Act application.</span></span>

<span data-ttu-id="d3af9-150">**Learningpool Act에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="d3af9-150">**To configure Azure AD single sign-on with Learningpool Act, perform the following steps:**</span></span>

1. <span data-ttu-id="d3af9-151">Azure Portal의 **Learningpool Act** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-151">In the Azure portal, on the **Learningpool Act** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="d3af9-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_samlbase.png)

3. <span data-ttu-id="d3af9-155">**Learningpool Act 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-155">On the **Learningpool Act Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_url.png)

    <span data-ttu-id="d3af9-157">a.</span><span class="sxs-lookup"><span data-stu-id="d3af9-157">a.</span></span> <span data-ttu-id="d3af9-158">**로그온 URL** 텍스트 상자에서 URL `https://parliament.preview.Learningpool.com/auth/shibboleth/index.php`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-158">In the **Sign-on URL** textbox, type the URL: `https://parliament.preview.Learningpool.com/auth/shibboleth/index.php`</span></span>

    <span data-ttu-id="d3af9-159">b.</span><span class="sxs-lookup"><span data-stu-id="d3af9-159">b.</span></span> <span data-ttu-id="d3af9-160">**식별자** 텍스트 상자에서 다음 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<subdomain>.Learningpool.com/shibboleth` |
    | `https://<subdomain>.preview.Learningpool.com/shibboleth` |

    > [!NOTE] 
    > <span data-ttu-id="d3af9-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-161">These values are not real.</span></span> <span data-ttu-id="d3af9-162">실제 로그온 URL 및 식별자로 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="d3af9-163">이러한 값을 얻으려면 [Learningpool Act 클라이언트 지원 팀](https://www.Learningpool.com/support)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="d3af9-163">Contact [Learningpool Act Client support team](https://www.Learningpool.com/support) to get these values.</span></span> 
 
4. <span data-ttu-id="d3af9-164">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 메타데이터 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_certificate.png) 

5. <span data-ttu-id="d3af9-166">Learningpool Act 응용 프로그램에는 특정 형식의 SAML 어설션이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-166">Learningpool Act application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="d3af9-167">이 응용 프로그램에 대한 다음 클레임을 구성하세요.</span><span class="sxs-lookup"><span data-stu-id="d3af9-167">Please configure the following claims for this application.</span></span> <span data-ttu-id="d3af9-168">응용 프로그램의 **"특성"** 탭에서 이러한 특성의 값을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-168">You can manage the values of these attributes from the **"Atrribute"** tab of the application.</span></span> <span data-ttu-id="d3af9-169">다음 스크린샷은 이에 대한 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-169">The following screenshot shows an example for this.</span></span> 

    ![Single Sign-on 구성](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_attribute.png) 

6. <span data-ttu-id="d3af9-171">**Single Sign-On** 대화 상자의 **사용자 특성** 섹션에서 이미지에 표시된 것과 같이 SAML 토큰 특성을 구성하고 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-171">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="d3af9-172">특성 이름</span><span class="sxs-lookup"><span data-stu-id="d3af9-172">Attribute Name</span></span> | <span data-ttu-id="d3af9-173">특성 값</span><span class="sxs-lookup"><span data-stu-id="d3af9-173">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="d3af9-174">urn:oid:1.2.840.113556.1.4.221</span><span class="sxs-lookup"><span data-stu-id="d3af9-174">urn:oid:1.2.840.113556.1.4.221</span></span> | <span data-ttu-id="d3af9-175">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="d3af9-175">user.userprincipalname</span></span> |
    | <span data-ttu-id="d3af9-176">urn:oid:2.5.4.42</span><span class="sxs-lookup"><span data-stu-id="d3af9-176">urn:oid:2.5.4.42</span></span> | <span data-ttu-id="d3af9-177">user.givenname</span><span class="sxs-lookup"><span data-stu-id="d3af9-177">user.givenname</span></span> |
    | <span data-ttu-id="d3af9-178">urn:oid:0.9.2342.19200300.100.1.3</span><span class="sxs-lookup"><span data-stu-id="d3af9-178">urn:oid:0.9.2342.19200300.100.1.3</span></span> | <span data-ttu-id="d3af9-179">user.mail</span><span class="sxs-lookup"><span data-stu-id="d3af9-179">user.mail</span></span> |    
    | <span data-ttu-id="d3af9-180">urn:oid:2.5.4.4</span><span class="sxs-lookup"><span data-stu-id="d3af9-180">urn:oid:2.5.4.4</span></span> | <span data-ttu-id="d3af9-181">user.surname</span><span class="sxs-lookup"><span data-stu-id="d3af9-181">user.surname</span></span> |
    
    <span data-ttu-id="d3af9-182">a.</span><span class="sxs-lookup"><span data-stu-id="d3af9-182">a.</span></span> <span data-ttu-id="d3af9-183">**특성 추가**를 클릭하여 **특성 추가** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-183">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-Learningpool-tutorial/tutorial_attribute_04.png)

    ![Single Sign-on 구성](./media/active-directory-saas-Learningpool-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="d3af9-186">b.</span><span class="sxs-lookup"><span data-stu-id="d3af9-186">b.</span></span> <span data-ttu-id="d3af9-187">**이름** 텍스트 상자에서 해당 행에 표시된 특성 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-187">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="d3af9-188">c.</span><span class="sxs-lookup"><span data-stu-id="d3af9-188">c.</span></span> <span data-ttu-id="d3af9-189">**값** 목록에서 해당 행에 대해 표시된 특성을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-189">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="d3af9-190">d.</span><span class="sxs-lookup"><span data-stu-id="d3af9-190">d.</span></span> <span data-ttu-id="d3af9-191">**네임스페이스**를 비워 둡니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-191">Leave the **Namespace** blank.</span></span>
    
    <span data-ttu-id="d3af9-192">e.</span><span class="sxs-lookup"><span data-stu-id="d3af9-192">e.</span></span> <span data-ttu-id="d3af9-193">**Ok**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-193">Click **Ok**.</span></span>

7. <span data-ttu-id="d3af9-194">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-194">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-Learningpool-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="d3af9-196">**Learningpool Act** 쪽에서 Single Sign-On을 구성하려면 다운로드한 **메타데이터 XML**을 [Learningpool Act 지원 팀](https://www.Learningpool.com/support)에 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-196">To configure single sign-on on **Learningpool Act** side, you need to send the downloaded **Metadata XML** to [Learningpool Act support team](https://www.Learningpool.com/support).</span></span> <span data-ttu-id="d3af9-197">이렇게 설정하면 SAML SSO 연결이 양쪽에서 제대로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-197">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="d3af9-198">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-198">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d3af9-199">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-199">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d3af9-200">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-200">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d3af9-201">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="d3af9-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="d3af9-202">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-202">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="d3af9-204">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="d3af9-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d3af9-205">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-205">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-Learningpool-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d3af9-207">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-207">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-Learningpool-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d3af9-209">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-209">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-Learningpool-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d3af9-211">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-211">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-Learningpool-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d3af9-213">a.</span><span class="sxs-lookup"><span data-stu-id="d3af9-213">a.</span></span> <span data-ttu-id="d3af9-214">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-214">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d3af9-215">b.</span><span class="sxs-lookup"><span data-stu-id="d3af9-215">b.</span></span> <span data-ttu-id="d3af9-216">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-216">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d3af9-217">c.</span><span class="sxs-lookup"><span data-stu-id="d3af9-217">c.</span></span> <span data-ttu-id="d3af9-218">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-218">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d3af9-219">d.</span><span class="sxs-lookup"><span data-stu-id="d3af9-219">d.</span></span> <span data-ttu-id="d3af9-220">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-220">Click **Create**.</span></span>
 
### <a name="creating-a-learningpool-act-test-user"></a><span data-ttu-id="d3af9-221">Learningpool Act 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="d3af9-221">Creating a Learningpool Act test user</span></span>

<span data-ttu-id="d3af9-222">Learningpool Act에 프로비전된 Azure AD 사용자만이 Learningpool Act에 로그인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-222">To enable Azure AD users to log in to Learningpool Act, they must be provisioned into Learningpool Act.</span></span>

<span data-ttu-id="d3af9-223">Learningpool Act에 대한 사용자 프로비저닝을 구성할 작업 항목이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-223">There is no action item for you to configure user provisioning to Learningpool Act.</span></span>  
<span data-ttu-id="d3af9-224">[Learningpool Act 지원 팀](https://www.Learningpool.com/support)에서 사용자를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-224">Users need to be created by your [Learningpool Act support team](https://www.Learningpool.com/support).</span></span>

>[!NOTE]
><span data-ttu-id="d3af9-225">다른 Learningpool Act 사용자 계정 생성 도구 또는 Learningpool Act가 제공한 API를 사용하여 AAD 사용자 계정을 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-225">You can use any other Learningpool Act user account creation tools or APIs provided by Learningpool Act to provision AAD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d3af9-226">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="d3af9-226">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d3af9-227">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Learningpool Act에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-227">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Learningpool Act.</span></span>

![사용자 할당][200] 

<span data-ttu-id="d3af9-229">**Britta Simon을 Learningpool Act에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="d3af9-229">**To assign Britta Simon to Learningpool Act, perform the following steps:**</span></span>

1. <span data-ttu-id="d3af9-230">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="d3af9-232">응용 프로그램 목록에서 **Learningpool Act**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-232">In the applications list, select **Learningpool Act**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_app.png) 

3. <span data-ttu-id="d3af9-234">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-234">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="d3af9-236">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-236">Click **Add** button.</span></span> <span data-ttu-id="d3af9-237">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="d3af9-239">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d3af9-240">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d3af9-241">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d3af9-242">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="d3af9-242">Testing single sign-on</span></span>

<span data-ttu-id="d3af9-243">이 섹션은 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-243">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d3af9-244">액세스 패널에서 Learningpool Act 타일을 클릭하면 Learningpool Act 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3af9-244">When you click the Learningpool Act tile in the Access Panel, you should get automatically signed-on to your Learningpool Act application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d3af9-245">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="d3af9-245">Additional resources</span></span>

* [<span data-ttu-id="d3af9-246">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="d3af9-246">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d3af9-247">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="d3af9-247">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_203.png

