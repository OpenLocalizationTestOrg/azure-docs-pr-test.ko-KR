---
title: "자습서: Klue와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 Klue 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 08341008-980b-4111-adb2-97bbabbf1e47
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: c64417c136340b3ffa5d67c618c6fe037d2992b5
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-klue"></a><span data-ttu-id="ee7f4-103">자습서: Klue와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="ee7f4-103">Tutorial: Azure Active Directory integration with Klue</span></span>

<span data-ttu-id="ee7f4-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Klue를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-104">In this tutorial, you learn how to integrate Klue with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ee7f4-105">Klue를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-105">Integrating Klue with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ee7f4-106">Klue에 액세스할 수 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-106">You can control in Azure AD who has access to Klue</span></span>
- <span data-ttu-id="ee7f4-107">사용자가 자신의 Azure AD 계정으로 Klue에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-107">You can enable your users to automatically get signed-on to Klue (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ee7f4-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ee7f4-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ee7f4-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="ee7f4-110">Prerequisites</span></span>

<span data-ttu-id="ee7f4-111">Klue와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-111">To configure Azure AD integration with Klue, you need the following items:</span></span>

- <span data-ttu-id="ee7f4-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="ee7f4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ee7f4-113">Klue Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="ee7f4-113">A Klue single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ee7f4-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ee7f4-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ee7f4-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ee7f4-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ee7f4-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="ee7f4-118">Scenario description</span></span>
<span data-ttu-id="ee7f4-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ee7f4-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ee7f4-121">갤러리에서 Klue 추가</span><span class="sxs-lookup"><span data-stu-id="ee7f4-121">Adding Klue from the gallery</span></span>
2. <span data-ttu-id="ee7f4-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="ee7f4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-klue-from-the-gallery"></a><span data-ttu-id="ee7f4-123">갤러리에서 Klue 추가</span><span class="sxs-lookup"><span data-stu-id="ee7f4-123">Adding Klue from the gallery</span></span>
<span data-ttu-id="ee7f4-124">Klue가 Azure AD에 통합되도록 구성하려면 갤러리의 Klue를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-124">To configure the integration of Klue into Azure AD, you need to add Klue from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ee7f4-125">**갤러리에서 Klue를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="ee7f4-125">**To add Klue from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ee7f4-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ee7f4-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ee7f4-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="ee7f4-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="ee7f4-133">검색 상자에 **Klue**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-133">In the search box, type **Klue**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-klue-tutorial/tutorial_klue_search.png)

5. <span data-ttu-id="ee7f4-135">결과 패널에서 **Klue**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-135">In the results panel, select **Klue**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-klue-tutorial/tutorial_klue_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ee7f4-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="ee7f4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ee7f4-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 사용하여 Klue에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-138">In this section, you configure and test Azure AD single sign-on with Klue based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ee7f4-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Klue 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Klue is to a user in Azure AD.</span></span> <span data-ttu-id="ee7f4-140">즉, Azure AD 사용자와 Klue의 관련 사용자 간에 연결 관계를 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-140">In other words, a link relationship between an Azure AD user and the related user in Klue needs to be established.</span></span>

<span data-ttu-id="ee7f4-141">Klue에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 연결 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-141">In Klue, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ee7f4-142">Klue에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-142">To configure and test Azure AD single sign-on with Klue, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ee7f4-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ee7f4-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ee7f4-145">**[Klue 테스트 사용자 만들기](#creating-a-klue-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 Klue에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-145">**[Creating a Klue test user](#creating-a-klue-test-user)** - to have a counterpart of Britta Simon in Klue that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ee7f4-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ee7f4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ee7f4-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="ee7f4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ee7f4-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Klue 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Klue application.</span></span>

<span data-ttu-id="ee7f4-150">**Klue에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="ee7f4-150">**To configure Azure AD single sign-on with Klue, perform the following steps:**</span></span>

1. <span data-ttu-id="ee7f4-151">Azure Portal의 **Klue** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-151">In the Azure portal, on the **Klue** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="ee7f4-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-klue-tutorial/tutorial_klue_samlbase.png)

3. <span data-ttu-id="ee7f4-155">**Klue 도메인 및 URL** 섹션에서 **IDP** 시작 모드로 응용 프로그램을 구성하려는 경우 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-155">On the **Klue Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-klue-tutorial/tutorial_klue_url1.png)

    <span data-ttu-id="ee7f4-157">a.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-157">a.</span></span> <span data-ttu-id="ee7f4-158">**식별자** 텍스트 상자에서 `urn:klue:<Customer ID>` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-158">In the **Identifier** textbox, type a URL using the following pattern: `urn:klue:<Customer ID>`</span></span>

    <span data-ttu-id="ee7f4-159">b.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-159">b.</span></span> <span data-ttu-id="ee7f4-160">**회신 URL** 텍스트 상자에 다음 패턴으로 URL을 입력합니다.`https://app.klue.com/account/auth/saml/<Customer UUID>/callback`</span><span class="sxs-lookup"><span data-stu-id="ee7f4-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://app.klue.com/account/auth/saml/<Customer UUID>/callback`</span></span>

4. <span data-ttu-id="ee7f4-161">**고급 URL 설정 표시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="ee7f4-162">**SP** 시작 모드에서 응용 프로그램을 구성하려면:</span><span class="sxs-lookup"><span data-stu-id="ee7f4-162">If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-klue-tutorial/tutorial_klue_url2.png)

    <span data-ttu-id="ee7f4-164">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://app.klue.com/account/auth/saml/<Customer UUID>/`</span><span class="sxs-lookup"><span data-stu-id="ee7f4-164">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://app.klue.com/account/auth/saml/<Customer UUID>/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="ee7f4-165">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-165">These values are not real.</span></span> <span data-ttu-id="ee7f4-166">실제 회신 URL, 식별자 및 로그온 URL로 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-166">Update these values with the actual Reply URL, Identifier, and Sign-On URL.</span></span> <span data-ttu-id="ee7f4-167">이러한 값을 얻으려면 [Klue 클라이언트 지원 팀](mailto:support@klue.com)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-167">Contact [Klue Client support team](mailto:support@klue.com) to get these values.</span></span>

5. <span data-ttu-id="ee7f4-168">Klue 응용 프로그램에는 특정 형식의 SAML 어설션이 필요하므로, SAML 토큰 특성 구성에 사용자 지정 특성 매핑을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-168">The Klue application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="ee7f4-169">응용 프로그램 통합 페이지의 **"사용자 특성"** 섹션에서 이러한 특성의 값을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-169">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> 

    ![Single Sign-on 구성](./media/active-directory-saas-klue-tutorial/attribute.png)

6. <span data-ttu-id="ee7f4-171">**Single Sign-On** 대화 상자의 **사용자 특성** 섹션에서 이전의 이미지에 표시된 것과 같이 SAML 토큰 특성을 구성하고 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-171">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the preceding image and perform the following steps:</span></span>
    
    | <span data-ttu-id="ee7f4-172">특성 이름</span><span class="sxs-lookup"><span data-stu-id="ee7f4-172">Attribute Name</span></span>      | <span data-ttu-id="ee7f4-173">특성 값</span><span class="sxs-lookup"><span data-stu-id="ee7f4-173">Attribute Value</span></span>      |
    | ------------------- | -------------------- |
    | <span data-ttu-id="ee7f4-174">first_name</span><span class="sxs-lookup"><span data-stu-id="ee7f4-174">first_name</span></span>          | <span data-ttu-id="ee7f4-175">user.givenname</span><span class="sxs-lookup"><span data-stu-id="ee7f4-175">user.givenname</span></span> |
    | <span data-ttu-id="ee7f4-176">last_name</span><span class="sxs-lookup"><span data-stu-id="ee7f4-176">last_name</span></span>           | <span data-ttu-id="ee7f4-177">user.surname</span><span class="sxs-lookup"><span data-stu-id="ee7f4-177">user.surname</span></span> |
    | <span data-ttu-id="ee7f4-178">email</span><span class="sxs-lookup"><span data-stu-id="ee7f4-178">email</span></span>               | <span data-ttu-id="ee7f4-179">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="ee7f4-179">user.userprincipalname</span></span>|
    
    <span data-ttu-id="ee7f4-180">a.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-180">a.</span></span> <span data-ttu-id="ee7f4-181">**특성 추가**를 클릭하여 **특성 추가** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-181">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-klue-tutorial/tutorial_attribute_04.png)

    ![Single Sign-on 구성](./media/active-directory-saas-klue-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="ee7f4-184">b.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-184">b.</span></span> <span data-ttu-id="ee7f4-185">**이름** 텍스트 상자에서 해당 행에 표시된 특성 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-185">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="ee7f4-186">c.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-186">c.</span></span> <span data-ttu-id="ee7f4-187">**값** 목록에서 해당 행에 대해 표시된 특성을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-187">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="ee7f4-188">d.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-188">d.</span></span> <span data-ttu-id="ee7f4-189">**Ok**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-189">Click **Ok**.</span></span>

7. <span data-ttu-id="ee7f4-190">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-190">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-klue-tutorial/tutorial_klue_certificate.png) 

8. <span data-ttu-id="ee7f4-192">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-192">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-klue-tutorial/tutorial_general_400.png)
    
9. <span data-ttu-id="ee7f4-194">**Klue 구성** 섹션에서 **Klue 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-194">On the **Klue Configuration** section, click **Configure Klue** to open **Configure sign-on** window.</span></span> <span data-ttu-id="ee7f4-195">**빠른 참조 섹션**에서 **SAML 엔터티 ID 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-195">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-klue-tutorial/tutorial_klue_configure.png) 

10. <span data-ttu-id="ee7f4-197">**Klue** 쪽에서 Single Sign-On을 구성하려면 다운로드한 **인증서(Base64), SAML Single Sign-On 서비스 URL 및 SAML 엔터티 ID**를 [Klue 지원 팀](mailto:support@klue.com)에 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-197">To configure single sign-on on **Klue** side, you need to send the downloaded **Certificate(Base64), SAML Single Sign-On Service URL, and SAML Entity ID** to [Klue support team](mailto:support@klue.com).</span></span>

> [!TIP]
> <span data-ttu-id="ee7f4-198">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-198">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ee7f4-199">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-199">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ee7f4-200">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-200">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ee7f4-201">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="ee7f4-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="ee7f4-202">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-202">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="ee7f4-204">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="ee7f4-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ee7f4-205">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-205">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-klue-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ee7f4-207">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-207">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-klue-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ee7f4-209">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-209">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-klue-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ee7f4-211">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-211">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-klue-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ee7f4-213">a.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-213">a.</span></span> <span data-ttu-id="ee7f4-214">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-214">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ee7f4-215">b.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-215">b.</span></span> <span data-ttu-id="ee7f4-216">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-216">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ee7f4-217">c.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-217">c.</span></span> <span data-ttu-id="ee7f4-218">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-218">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ee7f4-219">d.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-219">d.</span></span> <span data-ttu-id="ee7f4-220">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-220">Click **Create**.</span></span>
 
### <a name="creating-a-klue-test-user"></a><span data-ttu-id="ee7f4-221">Klue 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="ee7f4-221">Creating a Klue test user</span></span>

<span data-ttu-id="ee7f4-222">이 섹션은 Klue에서 Britta Simon이라는 사용자를 만들기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-222">The objective of this section is to create a user called Britta Simon in Klue.</span></span> <span data-ttu-id="ee7f4-223">Klue는 적시에 프로비전을 지원하며 기본적으로 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-223">Klue supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="ee7f4-224">이 섹션에 작업 항목이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-224">There is no action item for you in this section.</span></span> <span data-ttu-id="ee7f4-225">새 사용자가 아직 존재하지 않는 경우 Klue에 액세스하는 동안 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-225">A new user is created during an attempt to access Klue if it doesn't exist yet.</span></span>

>[!Note]
><span data-ttu-id="ee7f4-226">사용자를 수동으로 만들어야 하는 경우 [Klue 지원 팀](mailto:support@klue.com)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-226">If you need to create a user manually, Contact [Klue support team](mailto:support@klue.com).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ee7f4-227">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="ee7f4-227">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ee7f4-228">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Klue에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-228">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Klue.</span></span>

![사용자 할당][200] 

<span data-ttu-id="ee7f4-230">**Britta Simon을 Klue에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="ee7f4-230">**To assign Britta Simon to Klue, perform the following steps:**</span></span>

1. <span data-ttu-id="ee7f4-231">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-231">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="ee7f4-233">응용 프로그램 목록에서 **Klue**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-233">In the applications list, select **Klue**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-klue-tutorial/tutorial_klue_app.png) 

3. <span data-ttu-id="ee7f4-235">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-235">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="ee7f4-237">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-237">Click **Add** button.</span></span> <span data-ttu-id="ee7f4-238">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="ee7f4-240">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-240">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ee7f4-241">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ee7f4-242">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ee7f4-243">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="ee7f4-243">Testing single sign-on</span></span>

<span data-ttu-id="ee7f4-244">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-244">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ee7f4-245">액세스 패널에서 Klue 타일을 클릭하면 Klue 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-245">When you click the Klue tile in the Access Panel, you should get automatically signed-on to your Klue application.</span></span>
<span data-ttu-id="ee7f4-246">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-246">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="ee7f4-247">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="ee7f4-247">Additional resources</span></span>

* [<span data-ttu-id="ee7f4-248">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="ee7f4-248">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ee7f4-249">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="ee7f4-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-klue-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-klue-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-klue-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-klue-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-klue-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-klue-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-klue-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-klue-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-klue-tutorial/tutorial_general_203.png

