---
title: "자습서: CloudPassage와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory 및 CloudPassage 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bfe1f14e-74e4-4680-ac9e-f7355e1c94cc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 094740e20570665e975dec1a591989e411f90c16
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cloudpassage"></a><span data-ttu-id="c1471-103">자습서: CloudPassage와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="c1471-103">Tutorial: Azure Active Directory integration with CloudPassage</span></span>

<span data-ttu-id="c1471-104">이 자습서에서는 Azure AD(Azure Active Directory)와 CloudPassage를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-104">In this tutorial, you learn how to integrate CloudPassage with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c1471-105">CloudPassage를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-105">Integrating CloudPassage with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c1471-106">CloudPassage에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-106">You can control in Azure AD who has access to CloudPassage</span></span>
- <span data-ttu-id="c1471-107">사용자가 해당 Azure AD 계정으로 CloudPassage에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-107">You can enable your users to automatically get signed-on to CloudPassage (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c1471-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c1471-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c1471-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c1471-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="c1471-110">Prerequisites</span></span>

<span data-ttu-id="c1471-111">CloudPassage와의 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-111">To configure Azure AD integration with CloudPassage, you need the following items:</span></span>

- <span data-ttu-id="c1471-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="c1471-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c1471-113">CloudPassage Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="c1471-113">A CloudPassage single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c1471-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c1471-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c1471-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="c1471-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c1471-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c1471-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="c1471-118">Scenario description</span></span>
<span data-ttu-id="c1471-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c1471-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c1471-121">갤러리에서 CloudPassage 추가</span><span class="sxs-lookup"><span data-stu-id="c1471-121">Adding CloudPassage from the gallery</span></span>
2. <span data-ttu-id="c1471-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="c1471-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cloudpassage-from-the-gallery"></a><span data-ttu-id="c1471-123">갤러리에서 CloudPassage 추가</span><span class="sxs-lookup"><span data-stu-id="c1471-123">Adding CloudPassage from the gallery</span></span>
<span data-ttu-id="c1471-124">CloudPassage의 Azure AD 통합을 구성하려면 갤러리의 CloudPassage를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-124">To configure the integration of CloudPassage into Azure AD, you need to add CloudPassage from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c1471-125">**갤러리에서 CloudPassage를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="c1471-125">**To add CloudPassage from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c1471-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c1471-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c1471-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="c1471-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="c1471-133">검색 상자에 **CloudPassage**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-133">In the search box, type **CloudPassage**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_search.png)

5. <span data-ttu-id="c1471-135">결과 패널에서 **CloudPassage**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-135">In the results panel, select **CloudPassage**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c1471-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="c1471-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c1471-138">이 섹션에서는 “Britta Simon”이라는 테스트 사용자를 기반으로 CloudPassage에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-138">In this section, you configure and test Azure AD single sign-on with CloudPassage based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c1471-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 CloudPassage 사용자가 누군지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-139">For single sign-on to work, Azure AD needs to know what the counterpart user in CloudPassage is to a user in Azure AD.</span></span> <span data-ttu-id="c1471-140">즉, Azure AD 사용자와 CloudPassage의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-140">In other words, a link relationship between an Azure AD user and the related user in CloudPassage needs to be established.</span></span>

<span data-ttu-id="c1471-141">CloudPassage에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-141">In CloudPassage, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c1471-142">CloudPassage에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-142">To configure and test Azure AD single sign-on with CloudPassage, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c1471-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c1471-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c1471-145">**[CloudPassage 테스트 사용자 만들기](#creating-a-cloudpassage-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 CloudPassage에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-145">**[Creating a CloudPassage test user](#creating-a-cloudpassage-test-user)** - to have a counterpart of Britta Simon in CloudPassage that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c1471-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c1471-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c1471-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="c1471-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c1471-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 CloudPassage 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your CloudPassage application.</span></span>

<span data-ttu-id="c1471-150">**CloudPassage에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="c1471-150">**To configure Azure AD single sign-on with CloudPassage, perform the following steps:**</span></span>

1. <span data-ttu-id="c1471-151">Azure Portal의 **CloudPassage** 응용 프로그램 통합 페이지에서 **Single sign-on**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-151">In the Azure portal, on the **CloudPassage** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="c1471-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_samlbase.png)

3. <span data-ttu-id="c1471-155">**CloudPassage 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-155">On the **CloudPassage Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_url.png)

    <span data-ttu-id="c1471-157">a.</span><span class="sxs-lookup"><span data-stu-id="c1471-157">a.</span></span> <span data-ttu-id="c1471-158">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://portal.cloudpassage.com/saml/init/accountid`</span><span class="sxs-lookup"><span data-stu-id="c1471-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://portal.cloudpassage.com/saml/init/accountid`</span></span>

    <span data-ttu-id="c1471-159">b.</span><span class="sxs-lookup"><span data-stu-id="c1471-159">b.</span></span> <span data-ttu-id="c1471-160">**회신 URL** 텍스트 상자에 `https://portal.cloudpassage.com/saml/consume/accountid` 패턴으로 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://portal.cloudpassage.com/saml/consume/accountid`.</span></span> <span data-ttu-id="c1471-161">CloudPassage 포털의 **Single Sign-On 설정** 섹션에서 **SSO 설치 설명서**를 클릭하여 이 특성의 값을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-161">You can get your value for this attribute by clicking **SSO Setup documentation** in the **Single Sign-on Settings** section of your CloudPassage portal.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_05.png)
     
    > [!NOTE] 
    > <span data-ttu-id="c1471-163">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-163">These values are not real.</span></span> <span data-ttu-id="c1471-164">실제 회신 URL 및 로그온 URL을 사용하여 이러한 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-164">Update these values with the actual Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="c1471-165">이러한 값을 얻으려면 [CloudPassage 클라이언트 지원 팀](https://www.cloudpassage.com/company/contact/)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="c1471-165">Contact [CloudPassage Client support team](https://www.cloudpassage.com/company/contact/) to get these values.</span></span> 

4. <span data-ttu-id="c1471-166">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-166">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_certificate.png) 

5. <span data-ttu-id="c1471-168">CloudPassage 응용 프로그램은 특정 서식에서 SAML 어설션을 예상하며 이는 SAML 토큰 특성 구성에 사용자 지정 특성 매핑을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-168">Your CloudPassage application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="c1471-169">다음 스크린샷은 이에 대한 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-169">The following screenshot shows an example for this.</span></span>
   
   ![Single Sign-on 구성](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_25.png) 

6. <span data-ttu-id="c1471-171">**Single sign-on** 대화 상자의 **사용자 특성** 섹션에서 위의 이미지에 표시된 것과 같이 SAML 토큰 특성을 구성하고 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-171">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>

    | <span data-ttu-id="c1471-172">특성 이름</span><span class="sxs-lookup"><span data-stu-id="c1471-172">Attribute Name</span></span> | <span data-ttu-id="c1471-173">특성 값</span><span class="sxs-lookup"><span data-stu-id="c1471-173">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="c1471-174">firstname</span><span class="sxs-lookup"><span data-stu-id="c1471-174">firstname</span></span> |<span data-ttu-id="c1471-175">user.givenname</span><span class="sxs-lookup"><span data-stu-id="c1471-175">user.givenname</span></span> |
    | <span data-ttu-id="c1471-176">lastname</span><span class="sxs-lookup"><span data-stu-id="c1471-176">lastname</span></span> |<span data-ttu-id="c1471-177">user.surname</span><span class="sxs-lookup"><span data-stu-id="c1471-177">user.surname</span></span> |
    | <span data-ttu-id="c1471-178">email</span><span class="sxs-lookup"><span data-stu-id="c1471-178">email</span></span> |<span data-ttu-id="c1471-179">user.mail</span><span class="sxs-lookup"><span data-stu-id="c1471-179">user.mail</span></span> |
    
    <span data-ttu-id="c1471-180">a.</span><span class="sxs-lookup"><span data-stu-id="c1471-180">a.</span></span> <span data-ttu-id="c1471-181">**특성 추가**를 클릭하여 **특성 추가** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-181">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-cloudpassage-tutorial/tutorial_attribute_04.png)
    
    ![Single Sign-on 구성](./media/active-directory-saas-cloudpassage-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="c1471-184">b.</span><span class="sxs-lookup"><span data-stu-id="c1471-184">b.</span></span> <span data-ttu-id="c1471-185">**이름** 텍스트 상자에서 해당 행에 표시된 특성 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-185">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="c1471-186">c.</span><span class="sxs-lookup"><span data-stu-id="c1471-186">c.</span></span> <span data-ttu-id="c1471-187">**값** 목록에서 해당 행에 대해 표시된 특성을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-187">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="c1471-188">d.</span><span class="sxs-lookup"><span data-stu-id="c1471-188">d.</span></span> <span data-ttu-id="c1471-189">**Ok**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-189">Click **Ok**.</span></span>

7. <span data-ttu-id="c1471-190">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-190">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_400.png)
    
8. <span data-ttu-id="c1471-192">**CloudPassage 구성** 섹션에서 **CloudPassage 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-192">On the **CloudPassage Configuration** section, click **Configure CloudPassage** to open **Configure sign-on** window.</span></span> <span data-ttu-id="c1471-193">**빠른 참조 섹션**에서 **로그아웃 URL, SAML 엔터티 ID 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-193">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_configure.png) 

9. <span data-ttu-id="c1471-195">다른 브라우저 창에서 CloudPassage 회사 사이트에 관리자 권한으로 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-195">In a different browser window, sign-on to your CloudPassage company site as administrator.</span></span>

10. <span data-ttu-id="c1471-196">위쪽 메뉴에서 **설정**을 클릭한 다음 **사이트 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-196">In the menu on the top, click **Settings**, and then click **Site Administration**.</span></span> 
   
    ![Single Sign-on 구성][12]

11. <span data-ttu-id="c1471-198">**인증 설정** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-198">Click the **Authentication Settings** tab.</span></span> 
   
    ![Single Sign-On 구성][13]

12. <span data-ttu-id="c1471-200">**Single Sign-On 설정** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-200">In the **Single Sign-on Settings** section, perform the following steps:</span></span> 
   
    ![Single Sign-On 구성][14]

    <span data-ttu-id="c1471-202">a.</span><span class="sxs-lookup"><span data-stu-id="c1471-202">a.</span></span> <span data-ttu-id="c1471-203">**SSO(Single Sign-On) 사용(SSO 설치 설명서)** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-203">Select **Enable Single sign-on(SSO)(SSO Setup Documentation)** checkbox.</span></span>
    
    <span data-ttu-id="c1471-204">b.</span><span class="sxs-lookup"><span data-stu-id="c1471-204">b.</span></span> <span data-ttu-id="c1471-205">**SAML 엔터티 ID**를 **SAML 발급자 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-205">Paste **SAML Entity ID** into the **SAML issuer URL** textbox.</span></span>
  
    <span data-ttu-id="c1471-206">c.</span><span class="sxs-lookup"><span data-stu-id="c1471-206">c.</span></span> <span data-ttu-id="c1471-207">**SAML Single Sign-On 서비스 URL**을 **SAML 끝점 URL** 텍스트 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-207">Paste **SAML Single Sign-On Service URL** into the **SAML endpoint URL** textbox.</span></span>
  
    <span data-ttu-id="c1471-208">d.</span><span class="sxs-lookup"><span data-stu-id="c1471-208">d.</span></span> <span data-ttu-id="c1471-209">**로그아웃 URL**을 **로그아웃 방문 페이지** 텍스트 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-209">Paste **Sign-Out URL** into the **Logout landing page** textbox.</span></span>
  
    <span data-ttu-id="c1471-210">e.</span><span class="sxs-lookup"><span data-stu-id="c1471-210">e.</span></span> <span data-ttu-id="c1471-211">다운로드한 인증서를 메모장에서 열고, 다운로드한 인증서의 내용을 클립보드에 복사한 다음, **x 509 인증서** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-211">Open your downloaded certificate in notepad, copy the content of downloaded certificate into your clipboard, and then paste it into the **x 509 certificate** textbox.</span></span>
  
    <span data-ttu-id="c1471-212">f.</span><span class="sxs-lookup"><span data-stu-id="c1471-212">f.</span></span> <span data-ttu-id="c1471-213">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-213">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="c1471-214">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-214">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c1471-215">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-215">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c1471-216">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-216">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c1471-217">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="c1471-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="c1471-218">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-218">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="c1471-220">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="c1471-220">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c1471-221">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-221">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c1471-223">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-223">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c1471-225">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-225">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c1471-227">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-227">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c1471-229">a.</span><span class="sxs-lookup"><span data-stu-id="c1471-229">a.</span></span> <span data-ttu-id="c1471-230">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-230">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c1471-231">b.</span><span class="sxs-lookup"><span data-stu-id="c1471-231">b.</span></span> <span data-ttu-id="c1471-232">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-232">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c1471-233">c.</span><span class="sxs-lookup"><span data-stu-id="c1471-233">c.</span></span> <span data-ttu-id="c1471-234">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-234">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c1471-235">d.</span><span class="sxs-lookup"><span data-stu-id="c1471-235">d.</span></span> <span data-ttu-id="c1471-236">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-236">Click **Create**.</span></span>
 
### <a name="creating-a-cloudpassage-test-user"></a><span data-ttu-id="c1471-237">CloudPassage 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="c1471-237">Creating a CloudPassage test user</span></span>

<span data-ttu-id="c1471-238">이 섹션은 CloudPassage에서 Britta Simon이라는 사용자를 만들기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-238">The objective of this section is to create a user called Britta Simon in CloudPassage.</span></span>

<span data-ttu-id="c1471-239">**CloudPassage에서 Britta Simon이라는 사용자를 만들려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="c1471-239">**To create a user called Britta Simon in CloudPassage, perform the following steps:**</span></span>

1. <span data-ttu-id="c1471-240">**CloudPassage** 회사 사이트에 관리자 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-240">Sign-on to your **CloudPassage** company site as an administrator.</span></span> 

2. <span data-ttu-id="c1471-241">위쪽 도구 모음에서 **설정**을 클릭한 다음 **사이트 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-241">In the toolbar on the top, click **Settings**, and then click **Site Administration**.</span></span> 
   
   ![CloudPassage 테스트 사용자 만들기][22] 

3. <span data-ttu-id="c1471-243">**사용자** 탭을 클릭한 다음 **새 사용자 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-243">Click the **Users** tab, and then click **Add New User**.</span></span> 
   
   ![CloudPassage 테스트 사용자 만들기][23]

4. <span data-ttu-id="c1471-245">**새 사용자 추가** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-245">In the **Add New User** section, perform the following steps:</span></span> 
   
   ![CloudPassage 테스트 사용자 만들기][24]
    
    <span data-ttu-id="c1471-247">a.</span><span class="sxs-lookup"><span data-stu-id="c1471-247">a.</span></span> <span data-ttu-id="c1471-248">**이름** 텍스트 상자에 Britta를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-248">In the **First Name** textbox, type Britta.</span></span> 
  
    <span data-ttu-id="c1471-249">b.</span><span class="sxs-lookup"><span data-stu-id="c1471-249">b.</span></span> <span data-ttu-id="c1471-250">**성** 텍스트 상자에 Simon을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-250">In the **Last Name** textbox, type Simon.</span></span>
  
    <span data-ttu-id="c1471-251">c.</span><span class="sxs-lookup"><span data-stu-id="c1471-251">c.</span></span> <span data-ttu-id="c1471-252">**사용자 이름** 텍스트 상자, **전자 메일** 텍스트 상자 및 **전자 메일 다시 입력** 텍스트 상자에 Azure AD의 Britta 사용자 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-252">In the **Username** textbox, the **Email** textbox and the **Retype Email** textbox, type Britta's user name in Azure AD.</span></span>
  
    <span data-ttu-id="c1471-253">d.</span><span class="sxs-lookup"><span data-stu-id="c1471-253">d.</span></span> <span data-ttu-id="c1471-254">**액세스 유형**으로 **Halo 포털 액세스 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-254">As **Access Type**, select **Enable Halo Portal Access**.</span></span>
  
    <span data-ttu-id="c1471-255">e.</span><span class="sxs-lookup"><span data-stu-id="c1471-255">e.</span></span> <span data-ttu-id="c1471-256">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-256">Click **Add**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c1471-257">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="c1471-257">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c1471-258">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 CloudPassage에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-258">In this section, you enable Britta Simon to use Azure single sign-on by granting access to CloudPassage.</span></span>

![사용자 할당][200] 

<span data-ttu-id="c1471-260">**Britta Simon을 CloudPassage에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="c1471-260">**To assign Britta Simon to CloudPassage, perform the following steps:**</span></span>

1. <span data-ttu-id="c1471-261">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-261">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="c1471-263">응용 프로그램 목록에서 **CloudPassage**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-263">In the applications list, select **CloudPassage**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_app.png) 

3. <span data-ttu-id="c1471-265">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-265">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="c1471-267">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-267">Click **Add** button.</span></span> <span data-ttu-id="c1471-268">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-268">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="c1471-270">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-270">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c1471-271">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-271">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c1471-272">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-272">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c1471-273">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="c1471-273">Testing single sign-on</span></span>

<span data-ttu-id="c1471-274">이 섹션은 액세스 패널을 사용하여 Azure AD SSO 구성을 테스트하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-274">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="c1471-275">액세스 패널에서 CloudPassage 타일을 클릭하면 CloudPassage 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="c1471-275">When you click the CloudPassage tile in the Access Panel, you should get automatically signed-on to your CloudPassage application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c1471-276">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="c1471-276">Additional resources</span></span>

* [<span data-ttu-id="c1471-277">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="c1471-277">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c1471-278">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="c1471-278">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_04.png
[12]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_07.png
[13]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_08.png
[14]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_09.png
[15]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_10.png
[22]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_15.png
[23]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_16.png
[24]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_17.png

[100]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_203.png

