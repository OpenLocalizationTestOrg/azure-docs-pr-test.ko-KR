---
title: "자습서: LinkedIn Learning과 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 LinkedIn Learning 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d5857070-bf79-4bd3-9a2a-4c1919a74946
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: jeedes
ms.openlocfilehash: 6ad28cb3adaa63ddc3d3769a650d26ca6a7e2695
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-learning"></a><span data-ttu-id="6ff2b-103">자습서: LinkedIn Learning과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="6ff2b-103">Tutorial: Azure Active Directory integration with LinkedIn Learning</span></span>

<span data-ttu-id="6ff2b-104">이 자습서에서는 LinkedIn Learning을 Azure AD(Azure Active Directory)와 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-104">In this tutorial, you learn how to integrate LinkedIn Learning with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6ff2b-105">LinkedIn Learning을 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-105">Integrating LinkedIn Learning with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6ff2b-106">LinkedIn Learning에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-106">You can control in Azure AD who has access to LinkedIn Learning</span></span>
- <span data-ttu-id="6ff2b-107">사용자의 Azure AD 계정으로 LinkedIn Learning에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-107">You can enable your users to automatically get signed-on to LinkedIn Learning (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6ff2b-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="6ff2b-109">Azure AD와의 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory를 사용한 응용 프로그램 액세스 및 Single Sign-On](active-directory-appssoaccess-whatis.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6ff2b-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="6ff2b-110">Prerequisites</span></span>

<span data-ttu-id="6ff2b-111">LinkedIn Learning과 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-111">To configure Azure AD integration with LinkedIn Learning, you need the following items:</span></span>

- <span data-ttu-id="6ff2b-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="6ff2b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6ff2b-113">LinkedIn Learning Single Sign-On을 사용하도록 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="6ff2b-113">A LinkedIn Learning single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6ff2b-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6ff2b-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6ff2b-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6ff2b-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6ff2b-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="6ff2b-118">Scenario description</span></span>
<span data-ttu-id="6ff2b-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6ff2b-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6ff2b-121">갤러리에서 LinkedIn Learning 추가</span><span class="sxs-lookup"><span data-stu-id="6ff2b-121">Adding LinkedIn Learning from the gallery</span></span>
2. <span data-ttu-id="6ff2b-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="6ff2b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-learning-from-the-gallery"></a><span data-ttu-id="6ff2b-123">갤러리에서 LinkedIn Learning 추가</span><span class="sxs-lookup"><span data-stu-id="6ff2b-123">Adding LinkedIn Learning from the gallery</span></span>
<span data-ttu-id="6ff2b-124">LinkedIn Learning이 Azure AD에 통합되도록 구성하려면 LinkedIn Learning을 갤러리에서 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-124">To configure the integration of LinkedIn Learning into Azure AD, you need to add LinkedIn Learning from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6ff2b-125">**갤러리에서 LinkedIn Learning을 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="6ff2b-125">**To add LinkedIn Learning from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6ff2b-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6ff2b-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6ff2b-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="6ff2b-131">대화 상자 위쪽에 있는 **추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-131">Click **Add** button on the top of the dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="6ff2b-133">검색 상자에서 **LinkedIn Learning**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-133">In the search box, type **LinkedIn Learning**.</span></span> <span data-ttu-id="6ff2b-134">결과 패널에서 **LinkedIn Learning**을 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-134">From results panel, click **LinkedIn Learning** to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_000.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6ff2b-136">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="6ff2b-136">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6ff2b-137">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 LinkedIn Learning에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-137">In this section, you configure and test Azure AD single sign-on with LinkedIn Learning based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6ff2b-138">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 LinkedIn Learning 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-138">For single sign-on to work, Azure AD needs to know what the counterpart user in LinkedIn Learning is to a user in Azure AD.</span></span> <span data-ttu-id="6ff2b-139">즉, Azure AD 사용자와 LinkedIn Learning의 관련 사용자 간에 연결 관계가 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-139">In other words, a link relationship between an Azure AD user and the related user in LinkedIn Learning needs to be established.</span></span>

<span data-ttu-id="6ff2b-140">이 연결 관계는 Azure AD의 **사용자 이름** 값을 LinkedIn Learning의 **Username** 값으로 할당하여 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-140">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in LinkedIn Learning.</span></span>

<span data-ttu-id="6ff2b-141">LinkedIn Learning에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-141">To configure and test Azure AD single sign-on with LinkedIn Learning, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6ff2b-142">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6ff2b-143">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6ff2b-144">**[LinkedIn Learning 테스트 사용자 만들기](#creating-a-linkedin-learning-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-144">**[Creating a LinkedIn Learning test user](#creating-a-linkedin-learning-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="6ff2b-145">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-145">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6ff2b-146">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-146">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6ff2b-147">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="6ff2b-147">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6ff2b-148">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 LinkedIn Learning 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-148">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LinkedIn Learning application.</span></span>

<span data-ttu-id="6ff2b-149">**LinkedIn Learning에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="6ff2b-149">**To configure Azure AD single sign-on with LinkedIn Learning, perform the following steps:**</span></span>

1. <span data-ttu-id="6ff2b-150">Azure Portal의 **LinkedIn Learning** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-150">In the Azure portal, on the **LinkedIn Learning** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="6ff2b-152">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-152">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedin_01.png)

3. <span data-ttu-id="6ff2b-154">다른 웹 브라우저 창에서 LinkedIn Learning 테넌트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-154">In a different web browser window, sign-on to your LinkedIn Learning tenant as an administrator.</span></span>

4. <span data-ttu-id="6ff2b-155">**계정 센터**의 **설정** 아래에서 **전역 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-155">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="6ff2b-156">또한 드롭다운 목록에서 **학습 - 기본**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-156">Also, select **Learning - Default** from the dropdown list.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_01.png)

5. <span data-ttu-id="6ff2b-158">**OR Click Here to load and copy individual fields from the form(또는 폼에서 개별 필드를 로드하여 복사하려면 여기를 클릭)**을 클릭하고 **엔터티 ID** 및 **ACS(Assertion Consumer Access) URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-158">Click **OR Click Here to load and copy individual fields from the form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_03.png)

6. <span data-ttu-id="6ff2b-160">**IdP 시작** 모드에서 SSO를 구성하려면 Azure Portal의 **LinkedIn Learning 도메인 및 URL**에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-160">On Azure portal, under **LinkedIn Learning Domain and URLs**, perform the following steps if you want to configure SSO in **IdP Initiated** mode</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_signon_01.png)

    <span data-ttu-id="6ff2b-162">a.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-162">a.</span></span> <span data-ttu-id="6ff2b-163">**식별자** 텍스트 상자에 LinkedIn 포털에서 복사한 **엔티티 ID**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-163">In the **Identifier** textbox, enter the **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="6ff2b-164">b.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-164">b.</span></span> <span data-ttu-id="6ff2b-165">**회신 URL** 텍스트 상자에 LinkedIn 포털에서 복사한 **ACS(Assertion Consumer Access) URL**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-165">In the **Reply URL** textbox, enter the **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

7. <span data-ttu-id="6ff2b-166">**SP 시작**에서 SSO를 구성하려면 구성 섹션에서 고급 URL 설정 표시 옵션을 클릭하고 다음 패턴으로 로그온 URL을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-166">If you want to configure SSO in **SP Initiated**, then click Show Advanced URL setting option in the configuration section and configure the sign-on URL with the following pattern:</span></span>

    `https://www.linkedin.com/checkpoint/enterprise/login/<AccountId>?application=learning&applicationInstanceId=<InstanceId>`

    ![Single Sign-on 구성](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_signon_02.png)   
    
8. <span data-ttu-id="6ff2b-168">LinkedIn Learning 응용 프로그램은 특정 형식의 SAML 어설션이 필요하기 때문에 SAML 토큰 특성 구성에 사용자 지정 특성 매핑을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-168">Your LinkedIn Learning application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="6ff2b-169">다음 스크린샷은 이에 대한 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-169">The following screenshot shows an example for this.</span></span> <span data-ttu-id="6ff2b-170">**사용자 ID**의 기본값은 **user.userprincipalname**이지만 LinkedIn Learning에는 이것이 사용자의 전자 메일 주소와 매핑되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-170">The default value of **User Identifier** is **user.userprincipalname** but LinkedIn Learning expects this to be mapped with the user's email address.</span></span> <span data-ttu-id="6ff2b-171">목록에서 **user.mail** 특성을 사용하거나 조직 구성을 기반으로 적절한 특성 값을 사용할 수 있기 위해서입니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-171">For that you can use **user.mail** attribute from the list or use the appropriate attribute value based on your organization configuration.</span></span> 

    ![Single Sign-on 구성](./media/active-directory-saas-linkedinlearning-tutorial/updateusermail.png)
    
9. <span data-ttu-id="6ff2b-173">**사용자 특성** 섹션에서 **기타 모든 사용자 특성 보기 및 편집**을 클릭하고 특성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-173">In **User Attributes** section, click **View and edit all other user attributes** and set the attributes.</span></span> <span data-ttu-id="6ff2b-174">사용자는 **전자 메일**, **부서**, **이름** 및 **성**이라는 이름의 4개 클레임을 추가해야 하며, 값은 **user.mail**, **user.department**, **user.givenname** 및 **user.surname**으로 각각 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-174">The user needs to add four claims named **email**, **department**, **firstname**, and **lastname** and the value is to be mapped with **user.mail**, **user.department**, **user.givenname**, and **user.surname** respectively</span></span>

    | <span data-ttu-id="6ff2b-175">특성 이름</span><span class="sxs-lookup"><span data-stu-id="6ff2b-175">Attribute Name</span></span> | <span data-ttu-id="6ff2b-176">특성 값</span><span class="sxs-lookup"><span data-stu-id="6ff2b-176">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="6ff2b-177">email</span><span class="sxs-lookup"><span data-stu-id="6ff2b-177">email</span></span>| <span data-ttu-id="6ff2b-178">user.mail</span><span class="sxs-lookup"><span data-stu-id="6ff2b-178">user.mail</span></span> |    
    | <span data-ttu-id="6ff2b-179">department</span><span class="sxs-lookup"><span data-stu-id="6ff2b-179">department</span></span>| <span data-ttu-id="6ff2b-180">user.department</span><span class="sxs-lookup"><span data-stu-id="6ff2b-180">user.department</span></span> |
    | <span data-ttu-id="6ff2b-181">firstname</span><span class="sxs-lookup"><span data-stu-id="6ff2b-181">firstname</span></span>| <span data-ttu-id="6ff2b-182">user.givenname</span><span class="sxs-lookup"><span data-stu-id="6ff2b-182">user.givenname</span></span> |
    | <span data-ttu-id="6ff2b-183">lastname</span><span class="sxs-lookup"><span data-stu-id="6ff2b-183">lastname</span></span>| <span data-ttu-id="6ff2b-184">user.surname</span><span class="sxs-lookup"><span data-stu-id="6ff2b-184">user.surname</span></span> |
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-linkedinlearning-tutorial/userattribute.png)
    
    <span data-ttu-id="6ff2b-186">a.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-186">a.</span></span> <span data-ttu-id="6ff2b-187">**특성 추가**를 클릭하여 특성 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-187">Click **Add Attribute** to open the attribute dialog.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-linkedinLearning-tutorial/tutorial_attribute_04.png)

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-linkedinLearning-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="6ff2b-190">b.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-190">b.</span></span> <span data-ttu-id="6ff2b-191">**이름** 텍스트 상자에서 해당 행에 표시된 특성 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-191">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="6ff2b-192">c.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-192">c.</span></span> <span data-ttu-id="6ff2b-193">**값** 목록에서 해당 행에 대해 표시된 특성을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-193">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="6ff2b-194">d.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-194">d.</span></span> <span data-ttu-id="6ff2b-195">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-195">Click **Ok**</span></span>

10. <span data-ttu-id="6ff2b-196">**이름** 특성에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-196">Perform the following steps on the **name** attribute-</span></span>

    <span data-ttu-id="6ff2b-197">a.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-197">a.</span></span> <span data-ttu-id="6ff2b-198">특성을 클릭하여 **특성 편집** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-198">Click on the attribute to open the **Edit Attribute** window.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-linkedinLearning-tutorial/url_update.png)

    <span data-ttu-id="6ff2b-200">b.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-200">b.</span></span> <span data-ttu-id="6ff2b-201">**네임스페이스**에서 URL 값을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-201">Delete the URL value from the **namespace**.</span></span>
    
    <span data-ttu-id="6ff2b-202">c.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-202">c.</span></span> <span data-ttu-id="6ff2b-203">**확인**을 클릭하여 설정을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-203">Click **Ok** to save the setting.</span></span>

11. <span data-ttu-id="6ff2b-204">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 XML 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-204">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_certificate.png) 

12. <span data-ttu-id="6ff2b-206">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-206">Click **Save**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_400.png)

13. <span data-ttu-id="6ff2b-208">**LinkedIn 관리 설정** 섹션으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-208">Go to **LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="6ff2b-209">XML 파일 업로드 옵션을 클릭하여 Azure Portal에서 다운로드한 XML 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-209">Upload the XML file you downloaded from the Azure portal by clicking the Upload XML file option.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_metadata_03.png)

14. <span data-ttu-id="6ff2b-211">**설정**을 클릭하여 SSO를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-211">Click **On** to enable SSO.</span></span> <span data-ttu-id="6ff2b-212">SSO 상태가 **연결 안 됨**에서 **연결됨**으로 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-212">SSO status changes from **Not Connected** to **Connected**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_05.png)

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6ff2b-214">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="6ff2b-214">Creating an Azure AD test user</span></span>
<span data-ttu-id="6ff2b-215">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-215">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="6ff2b-217">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="6ff2b-217">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6ff2b-218">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-218">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6ff2b-220">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-220">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6ff2b-222">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-222">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6ff2b-224">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-224">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6ff2b-226">a.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-226">a.</span></span> <span data-ttu-id="6ff2b-227">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-227">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6ff2b-228">b.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-228">b.</span></span> <span data-ttu-id="6ff2b-229">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-229">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6ff2b-230">c.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-230">c.</span></span> <span data-ttu-id="6ff2b-231">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-231">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="6ff2b-232">d.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-232">d.</span></span> <span data-ttu-id="6ff2b-233">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-233">Click **Create**.</span></span> 

### <a name="creating-a-linkedin-learning-test-user"></a><span data-ttu-id="6ff2b-234">LinkedIn Learning 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="6ff2b-234">Creating a LinkedIn Learning test user</span></span>

<span data-ttu-id="6ff2b-235">LinkedIn Learning 응용 프로그램은</span><span class="sxs-lookup"><span data-stu-id="6ff2b-235">Linked Learning Application supports.</span></span> <span data-ttu-id="6ff2b-236">Just-In-Time 사용자 프로비전을 지원하며 인증 후에는 응용 프로그램에서 자동으로 사용자가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-236">Just in time user provisioning and after authentication users are created in the application automatically.</span></span> <span data-ttu-id="6ff2b-237">LinkedIn Learning 포털의 관리 설정 페이지에서 **Automatically Assign licenses**(라이선스 자동 할당) 스위치를 전환하여 JIT(Just-in-time) 프로비저닝을 사용하도록 활성화하면 사용자에게 라이선스가 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-237">On the admin settings page on the LinkedIn Learning portal flip the switch **Automatically Assign licenses** to active to enable Just in time provisioning and this will also assign a license to the user.</span></span>
   
   ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-linkedinLearning-tutorial/LinkedinUserprovswitch.png)

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="6ff2b-239">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="6ff2b-239">Assigning the Azure AD test user</span></span>

<span data-ttu-id="6ff2b-240">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 LinkedIn Learning에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-240">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LinkedIn Learning.</span></span>

![사용자 할당][200] 

<span data-ttu-id="6ff2b-242">**Britta Simon을 LinkedIn Learning에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="6ff2b-242">**To assign Britta Simon to LinkedIn Learning, perform the following steps:**</span></span>

1. <span data-ttu-id="6ff2b-243">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-243">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="6ff2b-245">응용 프로그램 목록에서 **LinkedIn Learning**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-245">In the applications list, select **LinkedIn Learning**.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_0001.png) 

3. <span data-ttu-id="6ff2b-247">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-247">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="6ff2b-249">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-249">Click **Add** button.</span></span> <span data-ttu-id="6ff2b-250">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="6ff2b-252">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-252">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="6ff2b-253">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6ff2b-254">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6ff2b-255">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="6ff2b-255">Testing single sign-on</span></span>

<span data-ttu-id="6ff2b-256">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-256">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="6ff2b-257">액세스 패널에서 LinkedIn Learning 타일을 클릭하면 Azure 로그온 페이지가 표시되고 로그온이 완료되면 LinkedIn Learning 응용 프로그램에 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ff2b-257">When you click the LinkedIn Learning tile in the Access Panel, you should get the Azure Sign-on page and on after successful sign-on, you should get into your LinkedIn Learning application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6ff2b-258">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="6ff2b-258">Additional resources</span></span>

* [<span data-ttu-id="6ff2b-259">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="6ff2b-259">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6ff2b-260">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="6ff2b-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_203.png