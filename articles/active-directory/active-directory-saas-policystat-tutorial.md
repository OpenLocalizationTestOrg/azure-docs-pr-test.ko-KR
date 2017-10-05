---
title: "자습서: PolicyStat와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 PolicyStat 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: af5eb0f1-1c8e-4809-b0c4-8ccfb915ca42
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 704afd5515b02ce2a4fbf35da65fad74dc506271
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-policystat"></a><span data-ttu-id="5a8a7-103">자습서: PolicyStat와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="5a8a7-103">Tutorial: Azure Active Directory integration with PolicyStat</span></span>

<span data-ttu-id="5a8a7-104">이 자습서에서는 Azure AD(Azure Active Directory)와 PolicyStat를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-104">In this tutorial, you learn how to integrate PolicyStat with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5a8a7-105">PolicyStat를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-105">Integrating PolicyStat with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5a8a7-106">PolicyStat에 액세스할 수 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-106">You can control in Azure AD who has access to PolicyStat</span></span>
- <span data-ttu-id="5a8a7-107">사용자가 자신의 Azure AD 계정으로 PolicyStat에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-107">You can enable your users to automatically get signed-on to PolicyStat (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5a8a7-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="5a8a7-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5a8a7-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="5a8a7-110">Prerequisites</span></span>

<span data-ttu-id="5a8a7-111">PolicyStat와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-111">To configure Azure AD integration with PolicyStat, you need the following items:</span></span>

- <span data-ttu-id="5a8a7-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="5a8a7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5a8a7-113">PolicyStat Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="5a8a7-113">A PolicyStat single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5a8a7-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5a8a7-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5a8a7-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5a8a7-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5a8a7-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="5a8a7-118">Scenario description</span></span>
<span data-ttu-id="5a8a7-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5a8a7-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5a8a7-121">갤러리에서 PolicyStat 추가</span><span class="sxs-lookup"><span data-stu-id="5a8a7-121">Adding PolicyStat from the gallery</span></span>
2. <span data-ttu-id="5a8a7-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="5a8a7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-policystat-from-the-gallery"></a><span data-ttu-id="5a8a7-123">갤러리에서 PolicyStat 추가</span><span class="sxs-lookup"><span data-stu-id="5a8a7-123">Adding PolicyStat from the gallery</span></span>
<span data-ttu-id="5a8a7-124">PolicyStat가 Azure AD에 통합되도록 구성하려면 갤러리의 PolicyStat를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-124">To configure the integration of PolicyStat into Azure AD, you need to add PolicyStat from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5a8a7-125">**갤러리에서 PolicyStat를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="5a8a7-125">**To add PolicyStat from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5a8a7-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5a8a7-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5a8a7-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="5a8a7-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="5a8a7-133">검색 상자에 **PolicyStat**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-133">In the search box, type **PolicyStat**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_search.png)

5. <span data-ttu-id="5a8a7-135">결과 패널에서 **PolicyStat**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-135">In the results panel, select **PolicyStat**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5a8a7-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="5a8a7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5a8a7-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 사용하여 PolicyStat에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-138">In this section, you configure and test Azure AD single sign-on with PolicyStat based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5a8a7-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 PolicyStat 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-139">For single sign-on to work, Azure AD needs to know what the counterpart user in PolicyStat is to a user in Azure AD.</span></span> <span data-ttu-id="5a8a7-140">즉, Azure AD 사용자와 PolicyStat의 관련 사용자 간에 연결 관계를 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-140">In other words, a link relationship between an Azure AD user and the related user in PolicyStat needs to be established.</span></span>

<span data-ttu-id="5a8a7-141">PolicyStat에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 연결 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-141">In PolicyStat, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="5a8a7-142">PolicyStat에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-142">To configure and test Azure AD single sign-on with PolicyStat, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5a8a7-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5a8a7-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5a8a7-145">**[PolicyStat 테스트 사용자 만들기](#creating-a-policystat-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 PolicyStat에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-145">**[Creating a PolicyStat test user](#creating-a-policystat-test-user)** - to have a counterpart of Britta Simon in PolicyStat that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5a8a7-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5a8a7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5a8a7-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="5a8a7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5a8a7-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 PolicyStat 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your PolicyStat application.</span></span>

<span data-ttu-id="5a8a7-150">**PolicyStat에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="5a8a7-150">**To configure Azure AD single sign-on with PolicyStat, perform the following steps:**</span></span>

1. <span data-ttu-id="5a8a7-151">Azure Portal의 **PolicyStat** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-151">In the Azure portal, on the **PolicyStat** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="5a8a7-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_samlbase.png)

3. <span data-ttu-id="5a8a7-155">**PolicyStat 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-155">On the **PolicyStat Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_url.png)

    <span data-ttu-id="5a8a7-157">a.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-157">a.</span></span> <span data-ttu-id="5a8a7-158">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<companyname>.policystat.com`</span><span class="sxs-lookup"><span data-stu-id="5a8a7-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.policystat.com`</span></span>

    <span data-ttu-id="5a8a7-159">b.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-159">b.</span></span> <span data-ttu-id="5a8a7-160">**식별자** 텍스트 상자에서 `https://<companyname>.policystat.com/saml2/metadata/` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.policystat.com/saml2/metadata/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5a8a7-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-161">These values are not real.</span></span> <span data-ttu-id="5a8a7-162">실제 로그온 URL 및 식별자로 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="5a8a7-163">이러한 값을 얻으려면 [PolicyStat 클라이언트 지원 팀](http://www.policystat.com/support/)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-163">Contact [PolicyStat Client support team](http://www.policystat.com/support/) to get these values.</span></span> 
 
4. <span data-ttu-id="5a8a7-164">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 메타데이터 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_certificate.png) 

5. <span data-ttu-id="5a8a7-166">이 섹션은 사용자가 SAML 프로토콜 기반 페더레이션을 사용하여 Azure AD의 계정으로 PolicyStat에 인증할 수 있게 하는 방법을 간략하게 설명하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-166">The objective of this section is to outline how to enable users to authenticate to PolicyStat with their account in Azure AD using federation based on the SAML protocol.</span></span>

    <span data-ttu-id="5a8a7-167">PolicyStat 응용 프로그램에는 특정 형식의 SAML 어설션이 필요하므로, **SAML 토큰 특성** 구성에 사용자 지정 특성 매핑을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-167">The PolicyStat application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **SAML Token Attributes** configuration.</span></span>  

     <span data-ttu-id="5a8a7-168">다음 스크린샷은 이에 대한 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-168">The following screenshot shows an example of this.</span></span>

     <span data-ttu-id="5a8a7-169">![특성](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_attribute.png "특성")</span><span class="sxs-lookup"><span data-stu-id="5a8a7-169">![Attributes](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_attribute.png "Attributes")</span></span>

6. <span data-ttu-id="5a8a7-170">필요한 특성 매핑을 추가하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-170">To add the required attribute mappings, perform the following steps:</span></span>

    | <span data-ttu-id="5a8a7-171">특성 이름</span><span class="sxs-lookup"><span data-stu-id="5a8a7-171">Attribute Name</span></span>    |   <span data-ttu-id="5a8a7-172">특성 값</span><span class="sxs-lookup"><span data-stu-id="5a8a7-172">Attribute Value</span></span> |
    |------------------- | -------------------- |
    | <span data-ttu-id="5a8a7-173">uid</span><span class="sxs-lookup"><span data-stu-id="5a8a7-173">uid</span></span> | <span data-ttu-id="5a8a7-174">ExtractMailPrefix([mail])</span><span class="sxs-lookup"><span data-stu-id="5a8a7-174">ExtractMailPrefix([mail])</span></span> |
    
    <span data-ttu-id="5a8a7-175">a.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-175">a.</span></span> <span data-ttu-id="5a8a7-176">**특성 추가**를 클릭하여 **특성 추가** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-176">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_04.png)

    ![Single Sign-on 구성](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_addatribute.png)
    
    <span data-ttu-id="5a8a7-179">b.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-179">b.</span></span> <span data-ttu-id="5a8a7-180">**특성 이름** 텍스트 상자에 **uid**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-180">In the **Attribute Name** textbox, type **uid**.</span></span>

    <span data-ttu-id="5a8a7-181">c.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-181">c.</span></span> <span data-ttu-id="5a8a7-182">**특성 값** 텍스트 상자에서 **ExtractMailPrefix()**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-182">In the **Attribute Value** textbox, select **ExtractMailPrefix()**.</span></span>    
   
    <span data-ttu-id="5a8a7-183">d.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-183">d.</span></span> <span data-ttu-id="5a8a7-184">**메일** 목록에서 **User.mail**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-184">From the **Mail** list, select **User.mail**.</span></span>
    
    <span data-ttu-id="5a8a7-185">e.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-185">e.</span></span> <span data-ttu-id="5a8a7-186">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-186">Click **Ok**</span></span>

7. <span data-ttu-id="5a8a7-187">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-187">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-policystat-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="5a8a7-189">다른 웹 브라우저 창에서 PolicyStat 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-189">In a different web browser window, log into your PolicyStat company site as an administrator.</span></span>

9. <span data-ttu-id="5a8a7-190">**관리** 탭을 클릭한 다음 왼쪽 탐색 창에서 **Single Sign-On 구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-190">Click the **Admin** tab, and then click **Single Sign-On Configuration** in left navigation pane.</span></span>
   
    <span data-ttu-id="5a8a7-191">![관리자 메뉴](./media/active-directory-saas-policystat-tutorial/ic808633.png "관리자 메뉴")</span><span class="sxs-lookup"><span data-stu-id="5a8a7-191">![Administrator Menu](./media/active-directory-saas-policystat-tutorial/ic808633.png "Administrator Menu")</span></span>

10. <span data-ttu-id="5a8a7-192">**설정** 섹션에서 **Single Sign-On 통합 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-192">In the **Setup** section, select **Enable Single Sign-on Integration**.</span></span>
   
    <span data-ttu-id="5a8a7-193">![Single Sign-on 구성](./media/active-directory-saas-policystat-tutorial/ic808634.png "Single Sign-on 구성")</span><span class="sxs-lookup"><span data-stu-id="5a8a7-193">![Single Sign-On Configuration](./media/active-directory-saas-policystat-tutorial/ic808634.png "Single Sign-On Configuration")</span></span>

11. <span data-ttu-id="5a8a7-194">**특성 구성**을 클릭한 다음 **특성 구성** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-194">Click **Configure Attributes**, and then, in the **Configure Attributes** section, perform the following steps:</span></span>
   
    <span data-ttu-id="5a8a7-195">![Single Sign-on 구성](./media/active-directory-saas-policystat-tutorial/ic808635.png "Single Sign-on 구성")</span><span class="sxs-lookup"><span data-stu-id="5a8a7-195">![Single Sign-On Configuration](./media/active-directory-saas-policystat-tutorial/ic808635.png "Single Sign-On Configuration")</span></span>
   
    <span data-ttu-id="5a8a7-196">a.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-196">a.</span></span> <span data-ttu-id="5a8a7-197">**사용자 이름 특성** 텍스트 상자에 **uid**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-197">In the **Username Attribute** textbox, type **uid**.</span></span>

    <span data-ttu-id="5a8a7-198">b.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-198">b.</span></span> <span data-ttu-id="5a8a7-199">**First Name Attribute**(이름 특성) 텍스트 상자에 사용자의 **이름**을 **Britta**로 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-199">In the **First Name Attribute** textbox, type **firstname** of user **Britta**.</span></span>

    <span data-ttu-id="5a8a7-200">c.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-200">c.</span></span> <span data-ttu-id="5a8a7-201">**Last Name Attribute**(성 특성) 텍스트 상자에 사용자의 **성**을 **Simon**으로 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-201">In the **Last Name Attribute** textbox, type **lastname** of user **Simon**.</span></span>

    <span data-ttu-id="5a8a7-202">d.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-202">d.</span></span> <span data-ttu-id="5a8a7-203">**Email Attribute**(메일 특성) 텍스트 상자에 사용자의 **메일 주소**를 **BrittaSimon@contoso.com**으로 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-203">In the **Email Attribute** textbox, type **emailaddress** of user **BrittaSimon@contoso.com**.</span></span>

    <span data-ttu-id="5a8a7-204">e.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-204">e.</span></span> <span data-ttu-id="5a8a7-205">**변경 내용 저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-205">Click **Save Changes**.</span></span>

12. <span data-ttu-id="5a8a7-206">**IDP 메타데이터**를 클릭한 다음, **IDP 메타데이터** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-206">Click **Your IDP Metadata**, and then, in the **Your IDP Metadata** section, perform the following steps:</span></span>
   
    <span data-ttu-id="5a8a7-207">![Single Sign-on 구성](./media/active-directory-saas-policystat-tutorial/ic808636.png "Single Sign-on 구성")</span><span class="sxs-lookup"><span data-stu-id="5a8a7-207">![Single Sign-On Configuration](./media/active-directory-saas-policystat-tutorial/ic808636.png "Single Sign-On Configuration")</span></span>
   
    <span data-ttu-id="5a8a7-208">a.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-208">a.</span></span> <span data-ttu-id="5a8a7-209">다운로드한 메타데이터 파일을 열고 내용을 복사한 다음 **Your Identity Provider Metadata**(ID 공급자 메타데이터) 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-209">Open your downloaded metadata file, copy the content, and  then paste it into the **Your Identity Provider Metadata** textbox.</span></span>

    <span data-ttu-id="5a8a7-210">b.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-210">b.</span></span> <span data-ttu-id="5a8a7-211">**변경 내용 저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-211">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="5a8a7-212">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-212">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5a8a7-213">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-213">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5a8a7-214">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-214">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5a8a7-215">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="5a8a7-215">Creating an Azure AD test user</span></span>
<span data-ttu-id="5a8a7-216">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-216">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="5a8a7-218">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="5a8a7-218">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5a8a7-219">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-219">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-policystat-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5a8a7-221">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-221">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-policystat-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5a8a7-223">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-223">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-policystat-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5a8a7-225">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-225">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-policystat-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5a8a7-227">a.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-227">a.</span></span> <span data-ttu-id="5a8a7-228">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-228">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5a8a7-229">b.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-229">b.</span></span> <span data-ttu-id="5a8a7-230">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-230">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5a8a7-231">c.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-231">c.</span></span> <span data-ttu-id="5a8a7-232">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-232">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="5a8a7-233">d.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-233">d.</span></span> <span data-ttu-id="5a8a7-234">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-234">Click **Create**.</span></span>
 
### <a name="creating-a-policystat-test-user"></a><span data-ttu-id="5a8a7-235">PolicyStat 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="5a8a7-235">Creating a PolicyStat test user</span></span>

<span data-ttu-id="5a8a7-236">Azure AD 사용자가 PolicyStat에 로그인할 수 있도록 하려면 PolicyStat로 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-236">In order to enable Azure AD users to log into PolicyStat, they must be provisioned into PolicyStat.</span></span>  

<span data-ttu-id="5a8a7-237">PolicyStat는 사용자 프로비전 시간에만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-237">PolicyStat supports just in time user provisioning.</span></span> <span data-ttu-id="5a8a7-238">즉, PolicyStat에 사용자를 수동으로 추가하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-238">This means, you do not need to add the users manually to PolicyStat.</span></span> <span data-ttu-id="5a8a7-239">SSO를 통해 첫 번째 로그인 시 사용자가 자동으로 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-239">The users will get added automatically on their first login through SSO.</span></span>

>[!NOTE]
><span data-ttu-id="5a8a7-240">다른 PolicyStat 사용자 계정 생성 도구 또는 PolicyStat가 제공한 API를 사용하여 Azure AD 사용자 계정을 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-240">You can use any other PolicyStat user account creation tools or APIs provided by PolicyStat to provision Azure AD user accounts.</span></span>
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="5a8a7-241">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="5a8a7-241">Assigning the Azure AD test user</span></span>

<span data-ttu-id="5a8a7-242">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 PolicyStat에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-242">In this section, you enable Britta Simon to use Azure single sign-on by granting access to PolicyStat.</span></span>

![사용자 할당][200] 

<span data-ttu-id="5a8a7-244">**Britta Simon을 PolicyStat에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="5a8a7-244">**To assign Britta Simon to PolicyStat, perform the following steps:**</span></span>

1. <span data-ttu-id="5a8a7-245">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-245">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="5a8a7-247">응용 프로그램 목록에서 **PolicyStat**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-247">In the applications list, select **PolicyStat**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_app.png) 

3. <span data-ttu-id="5a8a7-249">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-249">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="5a8a7-251">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-251">Click **Add** button.</span></span> <span data-ttu-id="5a8a7-252">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="5a8a7-254">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-254">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5a8a7-255">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5a8a7-256">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5a8a7-257">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="5a8a7-257">Testing single sign-on</span></span>

<span data-ttu-id="5a8a7-258">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-258">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="5a8a7-259">액세스 패널에서 PolicyStat 타일을 클릭하면 PolicyStat 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-259">When you click the PolicyStat tile in the Access Panel, you should get automatically signed-on to your PolicyStat application.</span></span>
<span data-ttu-id="5a8a7-260">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5a8a7-260">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5a8a7-261">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="5a8a7-261">Additional resources</span></span>

* [<span data-ttu-id="5a8a7-262">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="5a8a7-262">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5a8a7-263">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="5a8a7-263">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_203.png

