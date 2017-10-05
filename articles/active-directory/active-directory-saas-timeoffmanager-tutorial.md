---
title: "자습서: TimeOffManager와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory 및 TimeOffManager 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 3685912f-d5aa-4730-ab58-35a088fc1cc3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 3f944ffbf704694b293b4b1e5bdb4f2c93ae35a1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-timeoffmanager"></a><span data-ttu-id="5ef6e-103">자습서: TimeOffManager와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="5ef6e-103">Tutorial: Azure Active Directory integration with TimeOffManager</span></span>

<span data-ttu-id="5ef6e-104">이 자습서에서는 Azure AD(Azure Active Directory)와 TimeOffManager를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-104">In this tutorial, you learn how to integrate TimeOffManager with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5ef6e-105">TimeOffManager를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-105">Integrating TimeOffManager with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5ef6e-106">TimeOffManager에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-106">You can control in Azure AD who has access to TimeOffManager</span></span>
- <span data-ttu-id="5ef6e-107">사용자가 해당 Azure AD 계정으로 TimeOffManager에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-107">You can enable your users to automatically get signed-on to TimeOffManager (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5ef6e-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="5ef6e-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5ef6e-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="5ef6e-110">Prerequisites</span></span>

<span data-ttu-id="5ef6e-111">TimeOffManager와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-111">To configure Azure AD integration with TimeOffManager, you need the following items:</span></span>

- <span data-ttu-id="5ef6e-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="5ef6e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5ef6e-113">TimeOffManager Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="5ef6e-113">A TimeOffManager single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5ef6e-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5ef6e-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5ef6e-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5ef6e-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5ef6e-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="5ef6e-118">Scenario description</span></span>
<span data-ttu-id="5ef6e-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5ef6e-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5ef6e-121">갤러리에서 TimeOffManager 추가</span><span class="sxs-lookup"><span data-stu-id="5ef6e-121">Add TimeOffManager from the gallery</span></span>
2. <span data-ttu-id="5ef6e-122">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="5ef6e-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-timeoffmanager-from-the-gallery"></a><span data-ttu-id="5ef6e-123">갤러리에서 TimeOffManager 추가</span><span class="sxs-lookup"><span data-stu-id="5ef6e-123">Add TimeOffManager from the gallery</span></span>
<span data-ttu-id="5ef6e-124">TimeOffManager의 Azure AD 통합을 구성하려면 갤러리의 TimeOffManager를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-124">To configure the integration of TimeOffManager into Azure AD, you need to add TimeOffManager from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5ef6e-125">**갤러리에서 TimeOffManager를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="5ef6e-125">**To add TimeOffManager from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5ef6e-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5ef6e-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5ef6e-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="5ef6e-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="5ef6e-133">검색 상자에 **TimeOffManager**를 입력하고 결과 패널에서 **TimeOffManager**를 선택한 후 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-133">In the search box, type **TimeOffManager**, select **TimeOffManager** from result panel and then click **Add** button to add the application.</span></span>

    ![갤러리에서 추가](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="5ef6e-135">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="5ef6e-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="5ef6e-136">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 TimeOffManager에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-136">In this section, you configure and test Azure AD single sign-on with TimeOffManager based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5ef6e-137">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 TimeOffManager 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-137">For single sign-on to work, Azure AD needs to know what the counterpart user in TimeOffManager is to a user in Azure AD.</span></span> <span data-ttu-id="5ef6e-138">즉, Azure AD 사용자와 TimeOffManager의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-138">In other words, a link relationship between an Azure AD user and the related user in TimeOffManager needs to be established.</span></span>

<span data-ttu-id="5ef6e-139">TimeOffManager에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 연결 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-139">In TimeOffManager, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="5ef6e-140">TimeOffManager에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-140">To configure and test Azure AD single sign-on with TimeOffManager, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5ef6e-141">**[Azure AD Single Sign-On 구성](#configure-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5ef6e-142">**[Azure AD 테스트 사용자 만들기](#create-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5ef6e-143">**[TimeOffManager 테스트 사용자 만들기](#create-a-timeoffmanager-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 TimeOffManager에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-143">**[Create a TimeOffManager test user](#create-a-timeoffmanager-test-user)** - to have a counterpart of Britta Simon in TimeOffManager that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5ef6e-144">**[Azure AD 테스트 사용자 할당](#assign-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5ef6e-145">**[Single Sign-on 테스트](#test-single-sign-on)** - 구성이 작동하는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="5ef6e-146">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="5ef6e-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="5ef6e-147">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 TimeOffManager 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TimeOffManager application.</span></span>

<span data-ttu-id="5ef6e-148">**TimeOffManager에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="5ef6e-148">**To configure Azure AD single sign-on with TimeOffManager, perform the following steps:**</span></span>

1. <span data-ttu-id="5ef6e-149">Azure Portal의 **TimeOffManager** 응용 프로그램 통합 페이지에서 **Single sign-on**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-149">In the Azure portal, on the **TimeOffManager** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="5ef6e-151">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![SAML 기반 로그온](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_samlbase.png)

3. <span data-ttu-id="5ef6e-153">**TimeOffManager 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-153">On the **TimeOffManager Domain and URLs** section, perform the following:</span></span>

     ![TimeOffManager 도메인 및 URL 섹션](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_url.png)

    <span data-ttu-id="5ef6e-155">**회신 URL** 텍스트 상자에 다음 패턴으로 URL을 입력합니다.`https://www.timeoffmanager.com/cpanel/sso/consume.aspx?company_id=<companyid>`</span><span class="sxs-lookup"><span data-stu-id="5ef6e-155">In the **Reply URL** textbox, type a URL using the following pattern: `https://www.timeoffmanager.com/cpanel/sso/consume.aspx?company_id=<companyid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5ef6e-156">이 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-156">This value is not real.</span></span> <span data-ttu-id="5ef6e-157">실제 회신 URL로 이 값을 업데이트하세요.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-157">Update this value with the actual Reply URL.</span></span> <span data-ttu-id="5ef6e-158">자습서의 뒷부분에 설명되어 있는 **Single Sign-On 설정 페이지**에서 이 값을 얻거나 [TimeOffManager 지원 팀](http://www.timeoffmanager.com/contact-us.aspx)에 문의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-158">You can get this value from **Single Sign on settings page** which is explained later in the tutorial or Contact [TimeOffManager support team](http://www.timeoffmanager.com/contact-us.aspx).</span></span>
 
4. <span data-ttu-id="5ef6e-159">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-159">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![SAML 서명 인증서 섹션](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_certificate.png) 

5. <span data-ttu-id="5ef6e-161">이 섹션은 사용자가 SAML 프로토콜 기반 페더레이션을 사용하여 Azure AD의 계정으로 TimeOffManager에 인증할 수 있게 하는 방법을 간략하게 설명하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-161">The objective of this section is to outline how to enable users to authenticate to TimeOffManger with their account in Azure AD using federation based on the SAML protocol.</span></span>
    
    <span data-ttu-id="5ef6e-162">TimeOffManager 응용 프로그램은 특정 서식에서 SAML 어설션을 예상하며, SAML 토큰 특성 구성에 사용자 지정 특성 매핑을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-162">Your TimeOffManger application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="5ef6e-163">다음 스크린샷은 이에 대한 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-163">The following screenshot shows an example for this.</span></span>

    <span data-ttu-id="5ef6e-164">![SAML 토큰 특성](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_attrb.png "SAML 토큰 특성")</span><span class="sxs-lookup"><span data-stu-id="5ef6e-164">![saml token attributes](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_attrb.png "saml token attributes")</span></span>
    
    | <span data-ttu-id="5ef6e-165">특성 이름</span><span class="sxs-lookup"><span data-stu-id="5ef6e-165">Attribute Name</span></span> | <span data-ttu-id="5ef6e-166">특성 값</span><span class="sxs-lookup"><span data-stu-id="5ef6e-166">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="5ef6e-167">firstname</span><span class="sxs-lookup"><span data-stu-id="5ef6e-167">Firstname</span></span> |<span data-ttu-id="5ef6e-168">User.givenname</span><span class="sxs-lookup"><span data-stu-id="5ef6e-168">User.givenname</span></span> |
    | <span data-ttu-id="5ef6e-169">Lastname</span><span class="sxs-lookup"><span data-stu-id="5ef6e-169">Lastname</span></span> |<span data-ttu-id="5ef6e-170">User.surname</span><span class="sxs-lookup"><span data-stu-id="5ef6e-170">User.surname</span></span> |
    | <span data-ttu-id="5ef6e-171">Email</span><span class="sxs-lookup"><span data-stu-id="5ef6e-171">Email</span></span> |<span data-ttu-id="5ef6e-172">User.mail</span><span class="sxs-lookup"><span data-stu-id="5ef6e-172">User.mail</span></span> |
    
    <span data-ttu-id="5ef6e-173">a.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-173">a.</span></span>  <span data-ttu-id="5ef6e-174">위의 테이블의 각 데이터 행에서 **사용자 특성 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-174">For each data row in the table above, click **add user attribute**.</span></span>
    
    <span data-ttu-id="5ef6e-175">![SAML 토큰 특성](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb.png "SAML 토큰 특성")</span><span class="sxs-lookup"><span data-stu-id="5ef6e-175">![saml token attributes](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb.png "saml token attributes")</span></span>
    
    <span data-ttu-id="5ef6e-176">![SAML 토큰 특성](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb1.png "SAML 토큰 특성")</span><span class="sxs-lookup"><span data-stu-id="5ef6e-176">![saml token attributes](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb1.png "saml token attributes")</span></span>
    
    <span data-ttu-id="5ef6e-177">b.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-177">b.</span></span>  <span data-ttu-id="5ef6e-178">**특성 이름** 텍스트 상자에서 해당 행에 표시된 특성 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-178">In the **Attribute Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="5ef6e-179">c.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-179">c.</span></span>  <span data-ttu-id="5ef6e-180">**특성 값** 텍스트 상자에서 해당 행에 표시된 특성 값을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-180">In the **Attribute Value** textbox, select the attribute  value shown for that row.</span></span>
    
    <span data-ttu-id="5ef6e-181">d.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-181">d.</span></span>  <span data-ttu-id="5ef6e-182">**Ok**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-182">Click **Ok**.</span></span>
    
6. <span data-ttu-id="5ef6e-183">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-183">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="5ef6e-185">**TimeOffManager 구성** 섹션에서 **TimeOffManager 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-185">On the **TimeOffManager Configuration** section, click **Configure TimeOffManager** to open **Configure sign-on** window.</span></span> <span data-ttu-id="5ef6e-186">**빠른 참조 섹션**에서 **로그아웃 URL, SAML 엔터티 ID 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-186">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![TimeOffManager 구성 섹션](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_configure.png) 

8. <span data-ttu-id="5ef6e-188">다른 웹 브라우저 창에서 TimeOffManager 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-188">In a different web browser window, log into your TimeOffManager company site as an administrator.</span></span>

9. <span data-ttu-id="5ef6e-189">**계정 \> 계정 옵션 \>Single Sign-On 설정**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-189">Go to **Account \> Account Options \> Single Sign-On Settings**.</span></span>
   
   <span data-ttu-id="5ef6e-190">![Single Sign-On 설정](./media/active-directory-saas-timeoffmanager-tutorial/ic795917.png "Single Sign-On 설정")</span><span class="sxs-lookup"><span data-stu-id="5ef6e-190">![Single Sign-On Settings](./media/active-directory-saas-timeoffmanager-tutorial/ic795917.png "Single Sign-On Settings")</span></span>
7. <span data-ttu-id="5ef6e-191">**Single Sign-On 설정** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-191">In the **Single Sign-On Settings** section, perform the following steps:</span></span>
   
   <span data-ttu-id="5ef6e-192">![Single Sign-On 설정](./media/active-directory-saas-timeoffmanager-tutorial/ic795918.png "Single Sign-On 설정")</span><span class="sxs-lookup"><span data-stu-id="5ef6e-192">![Single Sign-On Settings](./media/active-directory-saas-timeoffmanager-tutorial/ic795918.png "Single Sign-On Settings")</span></span>
   
   <span data-ttu-id="5ef6e-193">a.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-193">a.</span></span> <span data-ttu-id="5ef6e-194">Base 64로 인코딩된 인증서를 메모장에서 열고, 내용을 클립보드에 복사한 다음 전체 인증서를 **X.509 인증서** 텍스트 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-194">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste the entire Certificate into **X.509 Certificate** textbox.</span></span>
   
   <span data-ttu-id="5ef6e-195">b.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-195">b.</span></span> <span data-ttu-id="5ef6e-196">Azure Portal에서 복사한 **SAML 엔터티 ID** 값을 **IdP 발급자** 텍스트 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-196">In **Idp Issuer** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="5ef6e-197">c.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-197">c.</span></span> <span data-ttu-id="5ef6e-198">Azure Portal에서 복사한 **SAML Single Sign-On 서비스 URL** 값을 **IdP 끝점 URL** 텍스트 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-198">In **IdP Endpoint URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="5ef6e-199">d.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-199">d.</span></span> <span data-ttu-id="5ef6e-200">**SAML 적용**에서는 **아니요**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-200">As **Enforce SAML**, select **No**.</span></span>
   
   <span data-ttu-id="5ef6e-201">e.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-201">e.</span></span> <span data-ttu-id="5ef6e-202">**사용자 자동 생성**의 경우 **예**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-202">As **Auto-Create Users**, select **Yes**.</span></span>
   
   <span data-ttu-id="5ef6e-203">f.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-203">f.</span></span> <span data-ttu-id="5ef6e-204">Azure Portal에서 복사한 **로그아웃 URL** 값을 **로그아웃 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-204">In **Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="5ef6e-205">g.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-205">g.</span></span> <span data-ttu-id="5ef6e-206">**변경 내용 저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-206">click **Save Changes**.</span></span>

11. <span data-ttu-id="5ef6e-207">**Single Sign-On 설정** 페이지에서 **Assertion Consumer Service URL** 값을 복사하고 Azure Portal의 **TimeOffManager 도메인 및 URL** 섹션 아래의 **회신 URL** 텍스트 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-207">In **Single Sign on settings** page, copy the value of **Assertion Consumer Service URL** and paste it in the **Reply URL** text box under **TimeOffManager Domain and URLs** section in Azure portal.</span></span> 

      <span data-ttu-id="5ef6e-208">![Single Sign-On 설정](./media/active-directory-saas-timeoffmanager-tutorial/ic795915.png "Single Sign-On 설정")</span><span class="sxs-lookup"><span data-stu-id="5ef6e-208">![Single Sign-On Settings](./media/active-directory-saas-timeoffmanager-tutorial/ic795915.png "Single Sign-On Settings")</span></span>

> [!TIP]
> <span data-ttu-id="5ef6e-209">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-209">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5ef6e-210">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-210">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5ef6e-211">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-211">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="5ef6e-212">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="5ef6e-212">Create an Azure AD test user</span></span>
<span data-ttu-id="5ef6e-213">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-213">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="5ef6e-215">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="5ef6e-215">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5ef6e-216">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-216">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5ef6e-218">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-218">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![사용자 및 그룹 --> 모든 사용자](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5ef6e-220">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-220">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![추가 단추](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5ef6e-222">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-222">On the **User** dialog page, perform the following steps:</span></span>
 
    ![사용자 대화 상자 페이지](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5ef6e-224">a.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-224">a.</span></span> <span data-ttu-id="5ef6e-225">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-225">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5ef6e-226">b.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-226">b.</span></span> <span data-ttu-id="5ef6e-227">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-227">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5ef6e-228">c.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-228">c.</span></span> <span data-ttu-id="5ef6e-229">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-229">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="5ef6e-230">d.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-230">d.</span></span> <span data-ttu-id="5ef6e-231">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-231">Click **Create**.</span></span>
 
### <a name="create-a-timeoffmanager-test-user"></a><span data-ttu-id="5ef6e-232">TimeOffManager 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="5ef6e-232">Create a TimeOffManager test user</span></span>

<span data-ttu-id="5ef6e-233">Azure AD 사용자가 TimeOffManager에 로그인할 수 있도록 하려면 TimeOffManager로 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-233">In order to enable Azure AD users to log into TimeOffManager, they must be provisioned to TimeOffManager.</span></span>  

<span data-ttu-id="5ef6e-234">TimeOffManager는 사용자 프로비전 시간에만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-234">TimeOffManager supports just in time user provisioning.</span></span> <span data-ttu-id="5ef6e-235">작업 항목이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-235">There is no action item for you.</span></span>  

<span data-ttu-id="5ef6e-236">처음으로 Single Sign On을 사용하여 로그인할 때 사용자가 자동으로 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-236">The users are added automatically during the first login using single sign on.</span></span>

>[!NOTE]
><span data-ttu-id="5ef6e-237">다른 TimeOffManager 사용자 계정 생성 도구 또는 TimeOffManager가 제공한 API를 사용하여 Azure AD 사용자 계정을 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-237">You can use any other TimeOffManager user account creation tools or APIs provided by TimeOffManager to provision Azure AD user accounts.</span></span>
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="5ef6e-238">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="5ef6e-238">Assign the Azure AD test user</span></span>

<span data-ttu-id="5ef6e-239">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 TimeOffManager에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-239">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TimeOffManager.</span></span>

![사용자 할당][200] 

<span data-ttu-id="5ef6e-241">**Britta Simon을 TimeOffManager에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="5ef6e-241">**To assign Britta Simon to TimeOffManager, perform the following steps:**</span></span>

1. <span data-ttu-id="5ef6e-242">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-242">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="5ef6e-244">응용 프로그램 목록에서 **TimeOffManager**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-244">In the applications list, select **TimeOffManager**.</span></span>

    ![앱 목록의 TimeOffManager](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_app.png) 

3. <span data-ttu-id="5ef6e-246">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-246">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="5ef6e-248">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-248">Click **Add** button.</span></span> <span data-ttu-id="5ef6e-249">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="5ef6e-251">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-251">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5ef6e-252">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5ef6e-253">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-253">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="5ef6e-254">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="5ef6e-254">Test single sign-on</span></span>

<span data-ttu-id="5ef6e-255">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-255">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="5ef6e-256">액세스 패널에서 TimeOffManager 타일을 클릭하면 TimeOffManager 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-256">When you click the TimeOffManager tile in the Access Panel, you should get automatically signed-on to your TimeOffManager application.</span></span> <span data-ttu-id="5ef6e-257">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5ef6e-257">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5ef6e-258">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="5ef6e-258">Additional resources</span></span>

* [<span data-ttu-id="5ef6e-259">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="5ef6e-259">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5ef6e-260">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="5ef6e-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_203.png

