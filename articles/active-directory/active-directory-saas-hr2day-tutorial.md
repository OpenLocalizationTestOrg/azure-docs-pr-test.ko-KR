---
title: "자습서: HR2day by Merces와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 HR2day by Merces 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 853d08c9-27b1-48d4-b8e7-3705140eb67f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/24/2017
ms.author: jeedes
ms.openlocfilehash: 77e2fcf9c306259286b15767f3a992510d6d79d8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hr2day-by-merces"></a><span data-ttu-id="7f819-103">자습서: HR2day by Merces와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="7f819-103">Tutorial: Azure Active Directory integration with HR2day by Merces</span></span>

<span data-ttu-id="7f819-104">이 자습서에서는 Azure AD(Azure Active Directory)와 HR2day by Merces를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-104">In this tutorial, you learn how to integrate HR2day by Merces with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7f819-105">HR2day by Merces를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-105">Integrating HR2day by Merces with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7f819-106">HR2day by Merces에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-106">You can control in Azure AD who has access to HR2day by Merces.</span></span>
- <span data-ttu-id="7f819-107">사용자가 해당 Azure AD 계정으로 HR2day by Merces에 자동으로 로그인되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-107">You can enable your users to automatically get signed in to HR2day by Merces with their Azure AD accounts.</span></span>
- <span data-ttu-id="7f819-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-108">You can manage your accounts in one central location--the Azure portal.</span></span>

<span data-ttu-id="7f819-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory를 사용한 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7f819-109">For more information about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7f819-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="7f819-110">Prerequisites</span></span>

<span data-ttu-id="7f819-111">HR2day by Merces와의 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-111">To configure Azure AD integration with HR2day by Merces, you need the following items:</span></span>

- <span data-ttu-id="7f819-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="7f819-112">An Azure AD subscription.</span></span>
- <span data-ttu-id="7f819-113">HR2day by Merces Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="7f819-113">An HR2day by Merces single sign-on enabled subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="7f819-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-114">We don't recommend using a production environment to test the steps in this tutorial.</span></span>

<span data-ttu-id="7f819-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-115">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="7f819-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="7f819-116">Don't use your production environment unless it's necessary.</span></span>
- <span data-ttu-id="7f819-117">아직 없는 경우 [Azure AD의 1개월 평가판](https://azure.microsoft.com/pricing/free-trial/)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-117">Get a [one-month free trial of Azure AD](https://azure.microsoft.com/pricing/free-trial/) if you don't already have it.</span></span>  

## <a name="scenario-description"></a><span data-ttu-id="7f819-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="7f819-118">Scenario description</span></span>
<span data-ttu-id="7f819-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7f819-120">여기에서 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-120">The scenario that's outlined here consists of two main building blocks:</span></span>

1. <span data-ttu-id="7f819-121">갤러리에서 HR2day by Merces 추가</span><span class="sxs-lookup"><span data-stu-id="7f819-121">Adding HR2day by Merces from the gallery.</span></span>
2. <span data-ttu-id="7f819-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="7f819-122">Configuring and testing Azure AD single sign-on.</span></span>

## <a name="add-hr2day-by-merces-from-the-gallery"></a><span data-ttu-id="7f819-123">갤러리에서 HR2day by Merces 추가</span><span class="sxs-lookup"><span data-stu-id="7f819-123">Add HR2day by Merces from the gallery</span></span>
<span data-ttu-id="7f819-124">HR2day by Merces와의 Azure AD 통합을 구성하려면 갤러리의 HR2day by Merces를 관리되는 SaaS 앱 목록에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-124">To configure the integration of HR2day by Merces into Azure AD, add HR2day by Merces from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7f819-125">**갤러리에서 HR2day by Merces를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="7f819-125">**To add HR2day by Merces from the gallery, take the following steps:**</span></span>

1. <span data-ttu-id="7f819-126">[Azure Portal](https://portal.azure.com)의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-126">In the [Azure portal](https://portal.azure.com), on the left navigation pane, select the **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7f819-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-128">Go to **Enterprise applications**.</span></span> <span data-ttu-id="7f819-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="7f819-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-131">To add a new application, select the **New application** button on the top of the dialog box.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="7f819-133">검색 상자에 **HR2day by Merces**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-133">In the search box, type **HR2day by Merces**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_search.png)

5. <span data-ttu-id="7f819-135">결과 패널에서 **HR2day by Merces**를 선택하고 **추가** 단추를 선택하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-135">In the results panel, select **HR2day by Merces**, and then select the **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="7f819-137">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="7f819-137">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="7f819-138">이 섹션에서는 “Britta Simon”이라는 테스트 사용자를 기반으로 HR2day by Merces에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-138">In this section, you configure and test Azure AD single sign-on with HR2day by Merces based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="7f819-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 HR2day by Merces 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-139">For single sign-on to work, Azure AD needs to know who the counterpart user in HR2day by Merces is to a user in Azure AD.</span></span> <span data-ttu-id="7f819-140">즉, Azure AD 사용자와 HR2day by Merces의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-140">In other words, you need to establish a link between an Azure AD user and the related user in HR2day by Merces.</span></span>

<span data-ttu-id="7f819-141">HR2day by Merces에서 Azure AD의 **사용자 이름**을 **Username**으로 할당하여 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-141">In HR2day by Merces, assign the **user name** in Azure AD to  **Username** to establish the relationship.</span></span>

<span data-ttu-id="7f819-142">HR2day by Merces에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-142">To configure and test Azure AD single sign-on with HR2day by Merces, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7f819-143">[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on): 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-143">[Configure Azure AD single sign-on](#configuring-azure-ad-single-sign-on): Enable your users to use this feature.</span></span>
2. <span data-ttu-id="7f819-144">[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user): Britta Simon으로 Azure AD Single Sign-On을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-144">[Create an Azure AD test user](#creating-an-azure-ad-test-user): Test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7f819-145">[HR2day by Merces 테스트 사용자 만들기](#creating-an-hr2day-by-merces-test-user): Britta Simon의 Azure AD 표현과 연결되는 대응 사용자를 HR2day by Merces에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-145">[Create an HR2day by Merces test user](#creating-an-hr2day-by-merces-test-user): Create a counterpart of Britta Simon in HR2day by Merces that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="7f819-146">[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user): Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-146">[Assign the Azure AD test user](#assigning-the-azure-ad-test-user): Enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7f819-147">[Single Sign-on 테스트](#testing-single-sign-on): 구성이 작동하는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-147">[Test single sign-on](#testing-single-sign-on): Verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="7f819-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="7f819-148">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="7f819-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 HR2day by Merces 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your HR2day by Merces application.</span></span>

<span data-ttu-id="7f819-150">**HR2day by Merces에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="7f819-150">**To configure Azure AD single sign-on with HR2day by Merces, take the following steps:**</span></span>

1. <span data-ttu-id="7f819-151">Azure Portal의 **HR2day by Merces** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-151">In the Azure portal, on the **HR2day by Merces** application integration page, select **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="7f819-153">Single Sign-On을 사용하도록 설정하려면 **Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-153">To enable single sign-on, in the **Single sign-on** dialog box, select **Mode** as **SAML-based Sign-on**.</span></span>
 
    ![Single Sign-On 구성](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_samlbase.png)

3. <span data-ttu-id="7f819-155">**HR2day by Merces 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-155">In the **HR2day by Merces Domain and URLs** section, take the following steps:</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_url.png)

    <span data-ttu-id="7f819-157">a.</span><span class="sxs-lookup"><span data-stu-id="7f819-157">a.</span></span> <span data-ttu-id="7f819-158">**로그온 URL** 텍스트 상자에서 다음과 같은 패턴을 사용하여 URL을 입력합니다. `https://<tenantname>.force.com/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="7f819-158">In the **Sign-on URL** box, type a URL by using the following pattern: `https://<tenantname>.force.com/<instancename>`.</span></span>

    <span data-ttu-id="7f819-159">b.</span><span class="sxs-lookup"><span data-stu-id="7f819-159">b.</span></span> <span data-ttu-id="7f819-160">**식별자** 텍스트 상자에서 다음과 같은 패턴을 사용하여 URL을 입력합니다. `https://hr2day.force.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="7f819-160">In the **Identifier** box, type a URL by using the following pattern: `https://hr2day.force.com/<companyname>`.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7f819-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-161">These values are not real.</span></span> <span data-ttu-id="7f819-162">실제 로그온 URL 및 식별자로 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-162">Update these values with the actual sign-on URL and identifier.</span></span> <span data-ttu-id="7f819-163">이러한 값을 얻으려면 [HR2day by Merces 클라이언트 지원 팀](mailto:servicedesk@merces.nl)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="7f819-163">Contact the [HR2day by Merces client support team](mailto:servicedesk@merces.nl) to get these values.</span></span> 
 


4. <span data-ttu-id="7f819-164">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 선택한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-164">On the **SAML Signing Certificate** section, select **Certificate(Base64)**, and then save the certificate file on your computer.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_certificate.png) 

5. <span data-ttu-id="7f819-166">이 섹션에서는 사용자가 Azure AD의 계정으로 HR2day by Merces에 인증할 수 있게 하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-166">This section describes how to enable users to authenticate to HR2day by Merces with their account in Azure AD.</span></span> <span data-ttu-id="7f819-167">SAML 프로토콜을 기반으로 하는 페더레이션을 사용하여 이를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-167">They do this by using federation that's based on the SAML protocol.</span></span>

    <span data-ttu-id="7f819-168">HR2day by Merces 응용 프로그램은 특정 서식에서 SAML 어설션을 예상하며 이는 SAML 토큰에 사용자 지정 특성 매핑을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-168">Your HR2day by Merces application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token.</span></span> <span data-ttu-id="7f819-169">다음 스크린샷은 이에 대한 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-169">The following screenshot shows an example of this.</span></span> 

    ![Single Sign-On 구성](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2day_00.png)
    
    > [!NOTE] 
    <span data-ttu-id="7f819-171">SAML 어설션을 구성하기 전에 [HR2day by Merces 클라이언트 지원 팀](mailto:servicedesk@merces.nl)에 문의하여 테넌트에 대한 고유 식별자 특성 값을 요청하세요.</span><span class="sxs-lookup"><span data-stu-id="7f819-171">Before you can configure the SAML assertion, you must contact the [HR2day by Merces Client support team](mailto:servicedesk@merces.nl) and request the value of the unique identifier attribute for your tenant.</span></span> <span data-ttu-id="7f819-172">다음 섹션의 단계를 완료하려면 이 값이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-172">You need this value to complete the steps in the next section.</span></span> 

6. <span data-ttu-id="7f819-173">**Single Sign-On** 대화 상자의 **사용자 특성** 섹션에서 다음 이미지에 표시된 것과 같이 SAML 토큰 특성을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-173">In the **Single sign-on** dialog box, in the **User Attributes** section, configure the SAML token attribute as shown in the following image.</span></span> <span data-ttu-id="7f819-174">다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-174">Then take the following steps.</span></span>
    
      | <span data-ttu-id="7f819-175">특성 이름</span><span class="sxs-lookup"><span data-stu-id="7f819-175">Attribute name</span></span>    |   <span data-ttu-id="7f819-176">특성 값</span><span class="sxs-lookup"><span data-stu-id="7f819-176">Attribute value</span></span> |  
    | ------------------- | -------------------- |    
    | <span data-ttu-id="7f819-177">ATTR_LOGINCLAIM</span><span class="sxs-lookup"><span data-stu-id="7f819-177">ATTR_LOGINCLAIM</span></span> | <span data-ttu-id="7f819-178">join([mail],"102938475Z","@"</span><span class="sxs-lookup"><span data-stu-id="7f819-178">join([mail],"102938475Z","@"</span></span> |
    
      <span data-ttu-id="7f819-179">a.</span><span class="sxs-lookup"><span data-stu-id="7f819-179">a.</span></span> <span data-ttu-id="7f819-180">**특성 추가** 대화 상자를 열려면 **특성 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-180">To open the **Add Attribute** dialog, select **Add attribute**.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-hr2day-tutorial/tutorial_attribute_04.png)

    ![Single Sign-on 구성](./media/active-directory-saas-hr2day-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="7f819-183">b.</span><span class="sxs-lookup"><span data-stu-id="7f819-183">b.</span></span> <span data-ttu-id="7f819-184">**이름** 상자에 **ATTR_LOGINCLAIM**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-184">In the **Name** box, type **ATTR_LOGINCLAIM**.</span></span>

    <span data-ttu-id="7f819-185">c.</span><span class="sxs-lookup"><span data-stu-id="7f819-185">c.</span></span> <span data-ttu-id="7f819-186">**값** 목록에서 **Join()**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-186">From the **Value** list, select **Join()**.</span></span>

    <span data-ttu-id="7f819-187">d.</span><span class="sxs-lookup"><span data-stu-id="7f819-187">d.</span></span> <span data-ttu-id="7f819-188">**String1** 목록에서 **user.mail**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-188">From the **String1** list, select **user.mail**.</span></span>

    <span data-ttu-id="7f819-189">e.</span><span class="sxs-lookup"><span data-stu-id="7f819-189">e.</span></span> <span data-ttu-id="7f819-190">**String2**의 경우 HR2day 팀에서 제공하는 고유 식별자를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-190">For **String2**, type the unique identifier that's provided by your HR2day team.</span></span>

    <span data-ttu-id="7f819-191">f.</span><span class="sxs-lookup"><span data-stu-id="7f819-191">f.</span></span> <span data-ttu-id="7f819-192">**구분 기호** 상자에 **@**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-192">In the **Separator** box, type **@**.</span></span>
    
    <span data-ttu-id="7f819-193">g.</span><span class="sxs-lookup"><span data-stu-id="7f819-193">g.</span></span> <span data-ttu-id="7f819-194">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-194">Select **Ok**.</span></span>

7. <span data-ttu-id="7f819-195">**저장** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-195">Select the **Save** button.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-hr2day-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="7f819-197">**HR2day by Merces 구성** 섹션에서 **HR2day by Merces 구성**을 선택하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-197">In the **HR2day by Merces Configuration** section, select **Configure HR2day by Merces** to open the **Configure sign-on** window.</span></span> <span data-ttu-id="7f819-198">**빠른 참조** 섹션에서 **로그아웃 URL**, **SAML 엔터티 ID** 및 **SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-198">Copy the **Sign-Out URL**, **SAML Entity ID**, and **SAML Single Sign-On Service URL** from the **Quick Reference** section.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_configure.png) 

9. <span data-ttu-id="7f819-200">응용 프로그램에 대한 SSO를 구성하려면 [HR2day by Merces 클라이언트 지원 팀](mailTo:servicedesk@merces.nl)에 문의합니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-200">To configure SSO  for your application, contact the [HR2day by Merces client support team](mailTo:servicedesk@merces.nl).</span></span> <span data-ttu-id="7f819-201">다운로드한 **인증서(Base64)** 파일을 사용자의 이메일에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-201">Attach the downloaded **Certificate(Base64)** file to your email.</span></span> <span data-ttu-id="7f819-202">또한 SSO 통합을 위해 구성할 수 있도록 **로그아웃 URL**, **SAML 엔터티 ID** 및 **SAML Single Sign-On 서비스 URL**을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-202">Also provide the **Sign-Out URL**, **SAML Entity ID**, and **SAML Single Sign-On Service URL** so that they can be configured for SSO integration.</span></span>

    > [!NOTE]
    ><span data-ttu-id="7f819-203">이 통합에는 이 패턴 **https://hr2day.force.com/INSTANCENAME**을 사용하여 설정되는 엔터티 ID가 필요하다고 Merces 팀에 알립니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-203">Mention to the Merces team that this integration needs the Entity ID to be set with the pattern **https://hr2day.force.com/INSTANCENAME**.</span></span>

    > [!TIP]
    ><span data-ttu-id="7f819-204">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-204">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7f819-205">**Active Directory** > **엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후 **Single Sign-On** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-205">After you add this app from the **Active Directory** > **Enterprise Applications** section, select the **Single Sign-On** tab.</span></span> <span data-ttu-id="7f819-206">그런 다음 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-206">Then access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7f819-207">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-207">You can read more about the embedded documentation feature in the [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="7f819-208">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="7f819-208">Create an Azure AD test user</span></span>
<span data-ttu-id="7f819-209">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-209">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="7f819-211">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="7f819-211">**To create a test user in Azure AD, take the following steps:**</span></span>

1. <span data-ttu-id="7f819-212">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-212">In the **Azure portal**, on the left navigation pane, select the **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-hr2day-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7f819-214">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-214">To display the list of users, go to **Users and groups**, and then select **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-hr2day-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7f819-216">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-216">To open the **User** dialog box, select **Add** on the top of the dialog box.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-hr2day-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7f819-218">**사용자** 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-218">In the **User** dialog box, take the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-hr2day-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7f819-220">a.</span><span class="sxs-lookup"><span data-stu-id="7f819-220">a.</span></span> <span data-ttu-id="7f819-221">**이름** 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-221">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7f819-222">b.</span><span class="sxs-lookup"><span data-stu-id="7f819-222">b.</span></span> <span data-ttu-id="7f819-223">**사용자 이름** 상자에 BrittaSimon의 **이메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-223">In the **User name** box, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7f819-224">c.</span><span class="sxs-lookup"><span data-stu-id="7f819-224">c.</span></span> <span data-ttu-id="7f819-225">**암호 표시**를 선택한 다음 암호를 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-225">Select **Show Password**, and then write down the password.</span></span>

    <span data-ttu-id="7f819-226">d.</span><span class="sxs-lookup"><span data-stu-id="7f819-226">d.</span></span> <span data-ttu-id="7f819-227">**만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-227">Select **Create**.</span></span>
 
### <a name="create-an-hr2day-by-merces-test-user"></a><span data-ttu-id="7f819-228">HR2day by Merces 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="7f819-228">Create an HR2day by Merces test user</span></span>

<span data-ttu-id="7f819-229">이 섹션의 목적은 HR2day by Merces에서 Britta Simon이라는 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-229">The objective of this section is to create a user called Britta Simon in HR2day by Merces.</span></span> <span data-ttu-id="7f819-230">HR2day 계정에 사용자를 추가하려면 [HR2day by Merces 클라이언트 지원 팀](mailto:servicedesk@merces.nl)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="7f819-230">To add the users in the HR2day account, work with the [HR2day by Merces client support team](mailto:servicedesk@merces.nl).</span></span> 

> [!NOTE]
> <span data-ttu-id="7f819-231">사용자를 수동으로 생성해야 하는 경우 [HR2day by Merces 클라이언트 지원 팀](mailto:servicedesk@merces.nl)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="7f819-231">If you need to create a user manually, contact the [HR2day by Merces client support team](mailto:servicedesk@merces.nl).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="7f819-232">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="7f819-232">Assign the Azure AD test user</span></span>

<span data-ttu-id="7f819-233">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 HR2day by Merces에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-233">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to HR2day by Merces.</span></span>

![사용자 할당][200] 

<span data-ttu-id="7f819-235">**Britta Simon을 HR2day by Merces에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="7f819-235">**To assign Britta Simon to HR2day by Merces, take the following steps:**</span></span>

1. <span data-ttu-id="7f819-236">Azure Portal에서 응용 프로그램 보기를 열고 디렉터리 보기로 이동한 다음 **엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-236">In the Azure portal, open the applications view, go to the directory view, and then go to **Enterprise applications**.</span></span> <span data-ttu-id="7f819-237">다음으로 **모든 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-237">Next, select **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="7f819-239">응용 프로그램 목록에서 **HR2day by Merces**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-239">In the applications list, select **HR2day by Merces**.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_app.png) 

3. <span data-ttu-id="7f819-241">왼쪽 메뉴에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-241">In the menu on the left, select **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="7f819-243">**추가** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-243">Select the **Add** button.</span></span> <span data-ttu-id="7f819-244">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-244">Then, in the **Add Assignment** dialog box, select **Users and groups**.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="7f819-246">**사용자 및 그룹** 대화 상자의 **사용자 목록**에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-246">In the **Users and groups** dialog box, in the **Users** list, select **Britta Simon**.</span></span>

6. <span data-ttu-id="7f819-247">**선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-247">Click the **Select** button.</span></span>

7. <span data-ttu-id="7f819-248">**할당 추가** 대화 상자에서 **할당**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-248">In the **Add Assignment** dialog box, select **Assign**.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="7f819-249">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="7f819-249">Test single sign-on</span></span>

<span data-ttu-id="7f819-250">이 섹션은 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-250">The objective of this section is to test your Azure AD single sign-on configuration by using the Access Panel.</span></span>  

<span data-ttu-id="7f819-251">액세스 패널에서 HR2day by Merces 타일을 선택하면 HR2day by Merces 응용 프로그램에 자동으로 로그인됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f819-251">When you select the HR2day by Merces tile in the Access Panel, you automatically get signed in  to your HR2day by Merces application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7f819-252">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="7f819-252">Additional resources</span></span>

* [<span data-ttu-id="7f819-253">Azure Active Directory와 SaaS 앱을 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="7f819-253">List of tutorials about how to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7f819-254">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="7f819-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_203.png

