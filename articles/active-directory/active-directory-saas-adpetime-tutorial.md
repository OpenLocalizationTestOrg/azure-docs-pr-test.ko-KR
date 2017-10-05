---
title: "자습서: ADP eTime과 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 ADP eTime 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a3e9f0be-19ed-4b99-a180-619e7624fc26
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: 31fed307a32e629d00aab7cc9d5167ee16d83936
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adp-etime"></a><span data-ttu-id="f6008-103">자습서: ADP eTime과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="f6008-103">Tutorial: Azure Active Directory integration with ADP eTime</span></span>

<span data-ttu-id="f6008-104">이 자습서에서는 Azure AD(Azure Active Directory)와 ADP eTime을 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-104">In this tutorial, you learn how to integrate ADP eTime with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f6008-105">ADP eTime을 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-105">Integrating ADP eTime with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f6008-106">ADP eTime에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-106">You can control in Azure AD who has access to ADP eTime</span></span>
- <span data-ttu-id="f6008-107">사용자가 해당 Azure AD 계정으로 ADP eTime에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-107">You can enable your users to automatically get signed-on to ADP eTime (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f6008-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f6008-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f6008-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f6008-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="f6008-110">Prerequisites</span></span>

<span data-ttu-id="f6008-111">ADP eTime과의 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-111">To configure Azure AD integration with ADP eTime, you need the following items:</span></span>

- <span data-ttu-id="f6008-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="f6008-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f6008-113">ADP eTime Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="f6008-113">An ADP eTime single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f6008-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f6008-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f6008-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="f6008-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f6008-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f6008-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="f6008-118">Scenario description</span></span>
<span data-ttu-id="f6008-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f6008-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f6008-121">갤러리에서 ADP eTime 추가</span><span class="sxs-lookup"><span data-stu-id="f6008-121">Adding ADP eTime from the gallery</span></span>
2. <span data-ttu-id="f6008-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="f6008-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adp-etime-from-the-gallery"></a><span data-ttu-id="f6008-123">갤러리에서 ADP eTime 추가</span><span class="sxs-lookup"><span data-stu-id="f6008-123">Adding ADP eTime from the gallery</span></span>
<span data-ttu-id="f6008-124">ADP eTime의 Azure AD 통합을 구성하려면 갤러리의 ADP eTime을 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-124">To configure the integration of ADP eTime into Azure AD, you need to add ADP eTime from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f6008-125">**갤러리에서 ADP eTime을 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="f6008-125">**To add ADP eTime from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f6008-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f6008-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f6008-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="f6008-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="f6008-133">검색 상자에 **ADP eTime**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-133">In the search box, type **ADP eTime**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_search.png)

5. <span data-ttu-id="f6008-135">결과 패널에서 **ADP eTime**을 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-135">In the results panel, select **ADP eTime**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f6008-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="f6008-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f6008-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 ADP eTime에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-138">In this section, you configure and test Azure AD single sign-on with ADP eTime based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f6008-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 ADP eTime 사용자가 누군지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ADP eTime is to a user in Azure AD.</span></span> <span data-ttu-id="f6008-140">즉, Azure AD 사용자와 ADP eTime의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-140">In other words, a link relationship between an Azure AD user and the related user in ADP eTime needs to be established.</span></span>

<span data-ttu-id="f6008-141">이 연결 관계는 Azure AD의 **사용자 이름** 값을 ADP eTime의 **Username** 값으로 할당하여 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ADP eTime.</span></span>

<span data-ttu-id="f6008-142">ADP eTime에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-142">To configure and test Azure AD single sign-on with ADP eTime, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f6008-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f6008-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f6008-145">**[ADP eTime 테스트 사용자 만들기](#creating-an-adp-etime-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 ADP eTime에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-145">**[Creating an ADP eTime test user](#creating-an-adp-etime-test-user)** - to have a counterpart of Britta Simon in ADP eTime that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f6008-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f6008-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f6008-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="f6008-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f6008-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 ADP eTime 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ADP eTime application.</span></span>

<span data-ttu-id="f6008-150">**ADP eTime에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="f6008-150">**To configure Azure AD single sign-on with ADP eTime, perform the following steps:**</span></span>

1. <span data-ttu-id="f6008-151">Azure Portal의 **ADP eTime** 응용 프로그램 통합 페이지에서 **Single sign-on**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-151">In the Azure portal, on the **ADP eTime** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="f6008-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_samlbase.png)

3. <span data-ttu-id="f6008-155">**ADP eTime 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-155">On the **ADP eTime Domain and URLs** section, perform the following step:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_url.png)

    <span data-ttu-id="f6008-157">a.</span><span class="sxs-lookup"><span data-stu-id="f6008-157">a.</span></span> <span data-ttu-id="f6008-158">**식별자** 텍스트 상자에서 `https://<servername>.adp.com` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<servername>.adp.com`</span></span>

    <span data-ttu-id="f6008-159">b.</span><span class="sxs-lookup"><span data-stu-id="f6008-159">b.</span></span> <span data-ttu-id="f6008-160">**회신 URL** 텍스트 상자에 다음 패턴으로 URL을 입력합니다.`https://<servername>.adp.com/affwebservices/public/saml2assertionconsumer`</span><span class="sxs-lookup"><span data-stu-id="f6008-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<servername>.adp.com/affwebservices/public/saml2assertionconsumer`</span></span> 
 
    > [!NOTE] 
    > <span data-ttu-id="f6008-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-161">These values are not the real.</span></span> <span data-ttu-id="f6008-162">회신 URL 및 식별자로 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-162">Update these values with the actual Reply URL and Identifier.</span></span> <span data-ttu-id="f6008-163">이러한 값을 가져오려면 [ADP eTime 지원팀](https://www.adp.com/contact-us/overview.aspx)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="f6008-163">Contact [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) to get these values.</span></span>

4. <span data-ttu-id="f6008-164">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 XML 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_certificate.png) 

5. <span data-ttu-id="f6008-166">ADP eTime 응용 프로그램은 특정 서식에서 SAML 어설션을 예상하며 이는 SAML 토큰 특성 구성에 사용자 지정 특성 매핑을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-166">The ADP eTime application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="f6008-167">다음 스크린샷은 이에 대한 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-167">The following screenshot shows an example for this.</span></span> <span data-ttu-id="f6008-168">클레임 이름은 항상 **"PersonImmutableID"** 및 사용자의 EmployeeID를 포함하는 ExtensionAttribute2에 매핑한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-168">The claim name will always be **"PersonImmutableID"** and the value of which we have mapped to ExtensionAttribute2 which contains the EmployeeID of the user.</span></span> 

    <span data-ttu-id="f6008-169">여기에서는 Azure AD에서 ADP eTime으로 매핑되는 사용자가 EmployeeID에서 수행되지만 응용 프로그램 설정에 따라 다른 값에 이를 매핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-169">Here the user mapping from Azure AD to ADP eTime will be done on the EmployeeID but you can map this to a different value also based on your application settings.</span></span> <span data-ttu-id="f6008-170">따라서 사용자의 올바른 식별자를 사용하고 해당 값을 **"PersonImmutableID"** 클레임으로 매핑하려면 [ADP eTime 지원팀](https://www.adp.com/contact-us/overview.aspx)과 먼저 작업해 보세요.</span><span class="sxs-lookup"><span data-stu-id="f6008-170">So please work with [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) first to use the correct identifier of a user and map that value with the **"PersonImmutableID"** claim.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_attribute.png)

6. <span data-ttu-id="f6008-172">**Single Sign-On** 대화 상자의 **사용자 특성** 섹션에서 이미지에 표시된 것과 같이 SAML 토큰 특성을 구성하고 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-172">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="f6008-173">특성 이름</span><span class="sxs-lookup"><span data-stu-id="f6008-173">Attribute Name</span></span> | <span data-ttu-id="f6008-174">특성 값</span><span class="sxs-lookup"><span data-stu-id="f6008-174">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="f6008-175">PersonImmutableID</span><span class="sxs-lookup"><span data-stu-id="f6008-175">PersonImmutableID</span></span> | <span data-ttu-id="f6008-176">user.extensionattribute2</span><span class="sxs-lookup"><span data-stu-id="f6008-176">user.extensionattribute2</span></span> |
    
    <span data-ttu-id="f6008-177">a.</span><span class="sxs-lookup"><span data-stu-id="f6008-177">a.</span></span> <span data-ttu-id="f6008-178">**특성 추가**를 클릭하여 **특성 추가** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-178">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-adpetime-tutorial/tutorial_attribute_04.png)

    ![Single Sign-on 구성](./media/active-directory-saas-adpetime-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="f6008-181">b.</span><span class="sxs-lookup"><span data-stu-id="f6008-181">b.</span></span> <span data-ttu-id="f6008-182">**이름** 텍스트 상자에서 해당 행에 표시된 특성 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-182">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="f6008-183">c.</span><span class="sxs-lookup"><span data-stu-id="f6008-183">c.</span></span> <span data-ttu-id="f6008-184">**값** 목록에서 해당 행에 대해 표시된 특성을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-184">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="f6008-185">d.</span><span class="sxs-lookup"><span data-stu-id="f6008-185">d.</span></span> <span data-ttu-id="f6008-186">**Ok**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-186">Click **Ok**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f6008-187">SAML 어설션을 구성하기 전에 [ADP eTime 지원팀](https://www.adp.com/contact-us/overview.aspx)에 문의하고 테넌트에 대한 고유 식별자 특성 값을 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-187">Before you can configure the SAML assertion, you need to contact your [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) and request the value of the unique identifier attribute for your tenant.</span></span> <span data-ttu-id="f6008-188">응용 프로그램에 대한 사용자 지정 클레임을 구성하려면 이 값이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-188">You need this value to configure the custom claim for your application.</span></span> 

7. <span data-ttu-id="f6008-189">**ADP eTime 구성** 섹션에서 **ADP eTime 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-189">On the **ADP eTime Configuration** section, click **Configure ADP eTime** to open **Configure sign-on** window.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_configure.png) 

8. <span data-ttu-id="f6008-191">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-191">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-adpetime-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="f6008-193">**ADP eTime** 쪽에서 Single Sign-On을 구성하려면 다운로드한 **메타데이터 XML**을 [ADP eTime 지원팀](https://www.adp.com/contact-us/overview.aspx)에 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-193">To configure single sign-on on **ADP eTime** side, you need to send the downloaded **Metadata XML** to [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx).</span></span> 

> [!TIP]
> <span data-ttu-id="f6008-194">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f6008-195">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f6008-196">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f6008-197">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="f6008-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="f6008-198">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="f6008-200">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="f6008-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f6008-201">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-adpetime-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f6008-203">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-adpetime-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f6008-205">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-adpetime-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f6008-207">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-adpetime-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f6008-209">a.</span><span class="sxs-lookup"><span data-stu-id="f6008-209">a.</span></span> <span data-ttu-id="f6008-210">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f6008-211">b.</span><span class="sxs-lookup"><span data-stu-id="f6008-211">b.</span></span> <span data-ttu-id="f6008-212">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f6008-213">c.</span><span class="sxs-lookup"><span data-stu-id="f6008-213">c.</span></span> <span data-ttu-id="f6008-214">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f6008-215">d.</span><span class="sxs-lookup"><span data-stu-id="f6008-215">d.</span></span> <span data-ttu-id="f6008-216">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-216">Click **Create**.</span></span>
 
### <a name="creating-an-adp-etime-test-user"></a><span data-ttu-id="f6008-217">ADP eTime 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="f6008-217">Creating an ADP eTime test user</span></span>

<span data-ttu-id="f6008-218">이 섹션은 ADP eTime에서 Britta Simon이라는 사용자를 만들기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-218">The objective of this section is to create a user called Britta Simon in ADP eTime.</span></span> <span data-ttu-id="f6008-219">ADP eTime 계정에 사용자를 추가하려면 [ADP eTime 지원팀](https://www.adp.com/contact-us/overview.aspx)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="f6008-219">Work with [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) to add the users in the ADP eTime account.</span></span> 
   
### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f6008-220">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="f6008-220">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f6008-221">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 ADP eTime에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ADP eTime.</span></span>

![사용자 할당][200] 

<span data-ttu-id="f6008-223">**Britta Simon을 ADP eTime에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="f6008-223">**To assign Britta Simon to ADP eTime, perform the following steps:**</span></span>

1. <span data-ttu-id="f6008-224">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="f6008-226">응용 프로그램 목록에서 **ADP eTime**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-226">In the applications list, select **ADP eTime**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_app.png) 

3. <span data-ttu-id="f6008-228">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-228">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="f6008-230">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-230">Click **Add** button.</span></span> <span data-ttu-id="f6008-231">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="f6008-233">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f6008-234">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f6008-235">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f6008-236">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="f6008-236">Testing single sign-on</span></span>

<span data-ttu-id="f6008-237">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f6008-238">액세스 패널에서 ADP eTime 타일을 클릭하면 ADP eTime 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6008-238">When you click the ADP eTime tile in the Access Panel, you should get automatically signed-on to your ADP eTime application.</span></span>
<span data-ttu-id="f6008-239">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f6008-239">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="f6008-240">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="f6008-240">Additional resources</span></span>

* [<span data-ttu-id="f6008-241">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="f6008-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f6008-242">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="f6008-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_203.png

