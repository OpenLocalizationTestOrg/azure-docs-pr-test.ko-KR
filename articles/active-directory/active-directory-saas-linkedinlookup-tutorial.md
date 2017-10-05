---
title: "자습서: LinkedIn Lookup과 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 LinkedIn Lookup 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a2757a39-1ead-4a3e-91e4-270be3055683
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: e296431866a8611b30e72f286884890adf0f7e50
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-lookup"></a><span data-ttu-id="d0833-103">자습서: LinkedIn Lookup과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="d0833-103">Tutorial: Azure Active Directory integration with LinkedIn Lookup</span></span>

<span data-ttu-id="d0833-104">이 자습서에서는 LinkedIn Lookup을 Azure AD(Azure Active Directory)와 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-104">In this tutorial, you learn how to integrate LinkedIn Lookup with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d0833-105">LinkedIn Lookup을 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-105">Integrating LinkedIn Lookup with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d0833-106">LinkedIn Lookup에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-106">You can control in Azure AD who has access to LinkedIn Lookup</span></span>
- <span data-ttu-id="d0833-107">사용자의 Azure AD 계정으로 LinkedIn Lookup에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-107">You can enable your users to automatically get signed-on to LinkedIn Lookup (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d0833-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d0833-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d0833-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d0833-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d0833-110">Prerequisites</span></span>

<span data-ttu-id="d0833-111">LinkedIn Lookup과 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-111">To configure Azure AD integration with LinkedIn Lookup, you need the following items:</span></span>

- <span data-ttu-id="d0833-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="d0833-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d0833-113">LinkedIn Lookup Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="d0833-113">An LinkedIn Lookup single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d0833-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d0833-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d0833-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="d0833-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d0833-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d0833-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="d0833-118">Scenario description</span></span>
<span data-ttu-id="d0833-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d0833-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d0833-121">갤러리에서 LinkedIn Lookup 추가</span><span class="sxs-lookup"><span data-stu-id="d0833-121">Adding LinkedIn Lookup from the gallery</span></span>
2. <span data-ttu-id="d0833-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="d0833-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-lookup-from-the-gallery"></a><span data-ttu-id="d0833-123">갤러리에서 LinkedIn Lookup 추가</span><span class="sxs-lookup"><span data-stu-id="d0833-123">Adding LinkedIn Lookup from the gallery</span></span>
<span data-ttu-id="d0833-124">LinkedIn Lookup이 Azure AD에 통합되도록 구성하려면 갤러리에서 LinkedIn Lookup을 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-124">To configure the integration of LinkedIn Lookup into Azure AD, you need to add LinkedIn Lookup from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d0833-125">**갤러리에서 LinkedIn Lookup을 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="d0833-125">**To add LinkedIn Lookup from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d0833-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d0833-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d0833-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="d0833-131">대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭하여 새 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-131">Click **New application** button on the top of the dialog to add new application.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="d0833-133">검색 상자에 **LinkedIn Lookup**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-133">In the search box, type **LinkedIn Lookup**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_search.png)

5. <span data-ttu-id="d0833-135">결과 패널에서 **LinkedIn Lookup**을 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-135">In the results panel, select **LinkedIn Lookup**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d0833-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="d0833-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d0833-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 LinkedIn Lookup에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-138">In this section, you configure and test Azure AD single sign-on with LinkedIn Lookup based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d0833-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 대응하는 LinkedIn Lookup 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-139">For single sign-on to work, Azure AD needs to know what the counterpart user in LinkedIn Lookup is to a user in Azure AD.</span></span> <span data-ttu-id="d0833-140">즉, Azure AD 사용자와 LinkedIn Lookup의 관련 사용자 간에 연결 관계가 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-140">In other words, a link relationship between an Azure AD user and the related user in LinkedIn Lookup needs to be established.</span></span>

<span data-ttu-id="d0833-141">이 연결 관계는 Azure AD의 **사용자 이름** 값을 LinkedIn Lookup의 **Username** 값으로 할당하여 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in LinkedIn Lookup.</span></span>

<span data-ttu-id="d0833-142">LinkedIn Lookup에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-142">To configure and test Azure AD single sign-on with LinkedIn Lookup, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d0833-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d0833-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d0833-145">**[LinkedIn Lookup 테스트 사용자 만들기](#creating-an-linkedin-lookup-test-user)** - Britta Simon의 Azure AD 표현과 연결되는 대응 사용자를 LinkedIn Lookup에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-145">**[Creating an LinkedIn Lookup test user](#creating-an-linkedin-lookup-test-user)** - to have a counterpart of Britta Simon in LinkedIn Lookup that is linked to the Azure AD representation.</span></span>
4. <span data-ttu-id="d0833-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d0833-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d0833-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="d0833-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d0833-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 LinkedIn Lookup 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LinkedIn Lookup application.</span></span>

<span data-ttu-id="d0833-150">**LinkedIn Lookup에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="d0833-150">**To configure Azure AD single sign-on with LinkedIn Lookup, perform the following steps:**</span></span>

1. <span data-ttu-id="d0833-151">Azure Portal의 **LinkedIn Lookup** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-151">In the Azure portal, on the **LinkedIn Lookup** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="d0833-153">**Single Sign-On** 대화 상자의 **모드**에서 **SAML 기반 로그온**을 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-153">On the **Single sign-on** dialog, in **Mode** select **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-On 구성](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_samlbase.png)

3. <span data-ttu-id="d0833-155">다른 웹 브라우저 창에서 **LinkedIn Lookup** 웹 사이트에 관리자로 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-155">In a different web browser window, sign-on to your **LinkedIn Lookup** website as an administrator.</span></span>

4. <span data-ttu-id="d0833-156">**계정 센터**의 **설정** 아래에서 **전역 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-156">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="d0833-157">또한 드롭다운 목록에서 **Lookup**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-157">Also, select **Lookup** from the dropdown list.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_LinkedIn_admin_011.png)

5. <span data-ttu-id="d0833-159">**OR Click Here to load and copy individual fields from the form(또는 폼에서 개별 필드를 로드하여 복사하려면 여기를 클릭)**을 클릭하고 **엔터티 ID** 및 **ACS(Assertion Consumer Access) URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-159">Click **OR Click Here to load and copy individual fields from the form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_LinkedIn_admin_032.png)

6. <span data-ttu-id="d0833-161">Azure Portal의 **LinkedIn Lookup 도메인 및 URL** 섹션에서 **IDP** 시작 모드로 응용 프로그램을 구성하려는 경우 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-161">On Azure portal, under **LinkedIn Lookup Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_url.png)

    <span data-ttu-id="d0833-163">a.</span><span class="sxs-lookup"><span data-stu-id="d0833-163">a.</span></span> <span data-ttu-id="d0833-164">**식별자** 텍스트 상자에 LinkedIn 포털에서 복사한 **엔티티 ID**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-164">In the **Identifier** textbox, enter the **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="d0833-165">b.</span><span class="sxs-lookup"><span data-stu-id="d0833-165">b.</span></span> <span data-ttu-id="d0833-166">**회신 URL** 텍스트 상자에 LinkedIn 포털에서 복사한 **ACS(Assertion Consumer Access) URL**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-166">In the **Reply URL** textbox, enter the **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

7. <span data-ttu-id="d0833-167">**SP** 시작 모드에서 응용 프로그램을 구성하려면 **고급 URL 설정 표시**를 선택하세요.</span><span class="sxs-lookup"><span data-stu-id="d0833-167">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_url1.png)

    <span data-ttu-id="d0833-169">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://www.linkedIn.com/checkpoint/enterprise/login/<AccountId>?application=lookup`</span><span class="sxs-lookup"><span data-stu-id="d0833-169">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://www.linkedIn.com/checkpoint/enterprise/login/<AccountId>?application=lookup`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="d0833-170">이것은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-170">This is not real value.</span></span> <span data-ttu-id="d0833-171">이러한 값을 실제 로그온 URL로 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-171">The user has to update these values with the actual Sign-On URL.</span></span> <span data-ttu-id="d0833-172">이 값을 얻으려면 [LinkedIn Lookup 지원 팀](https://business.LinkedIn.com/lookup)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="d0833-172">Contact [LinkedIn Lookup Client support team](https://business.LinkedIn.com/lookup) to get this value.</span></span>

8. <span data-ttu-id="d0833-173">**LinkedIn Lookup** 응용 프로그램은 특정 형식의 SAML 어설션이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-173">Your **LinkedIn Lookup** application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="d0833-174">SAML 토큰 특성 구성에 사용자 지정 특성 매핑을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-174">The user has to add custom attribute mappings to the SAML token attributes configuration.</span></span> <span data-ttu-id="d0833-175">다음 스크린샷은 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-175">The following screenshot shows an example.</span></span> <span data-ttu-id="d0833-176">**사용자 ID**의 기본값은 **user.userprincipalname**이지만 LinkedIn Lookup에서는 이것이 사용자의 전자 메일 주소와 매핑되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-176">The default value of **User Identifier** is **user.userprincipalname** but LinkedIn Lookup expects this to be mapped with the user's email address.</span></span> <span data-ttu-id="d0833-177">목록에서 **user.mail** 특성을 사용하거나 조직 구성을 기반으로 적절한 특성 값을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-177">You can use **user.mail** attribute from the list or use the appropriate attribute value based on your organization configuration.</span></span> 

    ![Single Sign-on 구성](./media/active-directory-saas-LinkedInlookup-tutorial/updateusermail.png)
    
9. <span data-ttu-id="d0833-179">**사용자 특성** 섹션에서 **기타 모든 사용자 특성 보기 및 편집**을 클릭하고 특성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-179">In **User Attributes** section, click **View and edit all other user attributes** and set the attributes.</span></span> <span data-ttu-id="d0833-180">사용자는 **전자 메일**, **부서**, **이름** 및 **성**이라는 이름의 4개 클레임을 추가해야 하며, 값은 **user.mail**, **user.department**, **user.givenname** 및 **user.surname**으로 각각 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-180">The user needs to add four claims named **email**,  **department**, **firstname**, and **lastname** and the value is to be mapped with **user.mail**, **user.department**, **user.givenname**, and **user.surname** respectively</span></span>

    | <span data-ttu-id="d0833-181">특성 이름</span><span class="sxs-lookup"><span data-stu-id="d0833-181">Attribute Name</span></span> | <span data-ttu-id="d0833-182">특성 값</span><span class="sxs-lookup"><span data-stu-id="d0833-182">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="d0833-183">email</span><span class="sxs-lookup"><span data-stu-id="d0833-183">email</span></span>| <span data-ttu-id="d0833-184">user.mail</span><span class="sxs-lookup"><span data-stu-id="d0833-184">user.mail</span></span> |    
    | <span data-ttu-id="d0833-185">department</span><span class="sxs-lookup"><span data-stu-id="d0833-185">department</span></span>| <span data-ttu-id="d0833-186">user.department</span><span class="sxs-lookup"><span data-stu-id="d0833-186">user.department</span></span> |
    | <span data-ttu-id="d0833-187">firstname</span><span class="sxs-lookup"><span data-stu-id="d0833-187">firstname</span></span>| <span data-ttu-id="d0833-188">user.givenname</span><span class="sxs-lookup"><span data-stu-id="d0833-188">user.givenname</span></span> |
    | <span data-ttu-id="d0833-189">lastname</span><span class="sxs-lookup"><span data-stu-id="d0833-189">lastname</span></span>| <span data-ttu-id="d0833-190">user.surname</span><span class="sxs-lookup"><span data-stu-id="d0833-190">user.surname</span></span> |

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-LinkedInlookup-tutorial/userattribute.png)

    <span data-ttu-id="d0833-192">a.</span><span class="sxs-lookup"><span data-stu-id="d0833-192">a.</span></span> <span data-ttu-id="d0833-193">**특성 추가**를 클릭하여 **특성 추가** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-193">Click **Add Attribute** to open the **Add Attribute** dialog.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-LinkedInlookup-tutorial/4.png)
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-LinkedInlookup-tutorial/5.png)
   
    <span data-ttu-id="d0833-196">b.</span><span class="sxs-lookup"><span data-stu-id="d0833-196">b.</span></span> <span data-ttu-id="d0833-197">**이름** 텍스트 상자에서 해당 행에 표시된 특성 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-197">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="d0833-198">c.</span><span class="sxs-lookup"><span data-stu-id="d0833-198">c.</span></span> <span data-ttu-id="d0833-199">**값** 목록에서 해당 행에 대해 표시된 특성을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-199">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="d0833-200">d.</span><span class="sxs-lookup"><span data-stu-id="d0833-200">d.</span></span> <span data-ttu-id="d0833-201">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-201">Click **Ok**</span></span>

10. <span data-ttu-id="d0833-202">**이름** 특성에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-202">Perform the following steps on the **name** attribute-</span></span>

    <span data-ttu-id="d0833-203">a.</span><span class="sxs-lookup"><span data-stu-id="d0833-203">a.</span></span> <span data-ttu-id="d0833-204">특성을 클릭하여 **특성 편집** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-204">Click on the attribute to open the **Edit Attribute** window.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-LinkedInlookup-tutorial/url_update.png)

    <span data-ttu-id="d0833-206">b.</span><span class="sxs-lookup"><span data-stu-id="d0833-206">b.</span></span> <span data-ttu-id="d0833-207">**네임스페이스**에서 URL 값을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-207">Delete the URL value from the **namespace**.</span></span>
    
    <span data-ttu-id="d0833-208">c.</span><span class="sxs-lookup"><span data-stu-id="d0833-208">c.</span></span> <span data-ttu-id="d0833-209">**확인**을 클릭하여 설정을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-209">Click **Ok** to save the setting.</span></span>

10. <span data-ttu-id="d0833-210">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 XML 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-210">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_certificate.png) 

11. <span data-ttu-id="d0833-212">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-212">Click **Save** button.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_400.png)

12. <span data-ttu-id="d0833-214">**LinkedIn 관리 설정** 섹션으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-214">Go to **LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="d0833-215">**Upload XML file(XML 파일 업로드)** 옵션을 클릭하여 Azure Portal에서 다운로드한 XML 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-215">Upload the XML file you downloaded from the Azure portal by clicking the **Upload XML file** option.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedIn_metadata_03.png)

13. <span data-ttu-id="d0833-217">**설정**을 클릭하여 SSO를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-217">Click **On** to enable SSO.</span></span> <span data-ttu-id="d0833-218">SSO 상태가 **연결 안 됨**에서 **연결됨**으로 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-218">SSO status changes from **Not Connected** to **Connected**</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedIn_admin_05.png)

> [!TIP]
> <span data-ttu-id="d0833-220">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-220">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d0833-221">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-221">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d0833-222">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-222">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d0833-223">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="d0833-223">Creating an Azure AD test user</span></span>
<span data-ttu-id="d0833-224">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-224">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="d0833-226">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="d0833-226">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d0833-227">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-227">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d0833-229">**사용자 및 그룹**으로 이동하여 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-229">Go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d0833-231">**추가**를 클릭하여 **사용자** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-231">Click **Add** to open the **User** dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d0833-233">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-233">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d0833-235">a.</span><span class="sxs-lookup"><span data-stu-id="d0833-235">a.</span></span> <span data-ttu-id="d0833-236">**이름** 텍스트 상자에 **Britta Simon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-236">In the **Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="d0833-237">b.</span><span class="sxs-lookup"><span data-stu-id="d0833-237">b.</span></span> <span data-ttu-id="d0833-238">**사용자 이름** 텍스트 상자에 Britta Simon의 **메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-238">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="d0833-239">c.</span><span class="sxs-lookup"><span data-stu-id="d0833-239">c.</span></span> <span data-ttu-id="d0833-240">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-240">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d0833-241">d.</span><span class="sxs-lookup"><span data-stu-id="d0833-241">d.</span></span> <span data-ttu-id="d0833-242">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-242">Click **Create**.</span></span>
 
### <a name="creating-an-linkedin-lookup-test-user"></a><span data-ttu-id="d0833-243">LinkedIn Lookup 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="d0833-243">Creating an LinkedIn Lookup test user</span></span>

<span data-ttu-id="d0833-244">LinkedIn Lookup 응용 프로그램이 JIT(Just-in-time) 사용자 프로비전을 지원하며 인증 후에 응용 프로그램에서 사용자가 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-244">Linked Lookup Application supports Just in Time (JIT) user provisioning and after authentication users are created in the application automatically.</span></span> <span data-ttu-id="d0833-245">**Automatically assign licenses**(라이선스 자동 할당)를 활성화하여 사용자에게 라이선스를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-245">Activate **Automatically assign licenses** to assign a license to the user.</span></span>
   
   ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedin_admin_license.png)

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d0833-247">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="d0833-247">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d0833-248">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 LinkedIn Lookup에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-248">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LinkedIn Lookup.</span></span>

![사용자 할당][200] 

<span data-ttu-id="d0833-250">**Britta Simon을 LinkedIn Lookup에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="d0833-250">**To assign Britta Simon to LinkedIn Lookup, perform the following steps:**</span></span>

1. <span data-ttu-id="d0833-251">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-251">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="d0833-253">응용 프로그램 목록에서 **LinkedIn Lookup**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-253">In the applications list, select **LinkedIn Lookup**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_app.png) 

3. <span data-ttu-id="d0833-255">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-255">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="d0833-257">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-257">Click **Add** button.</span></span> <span data-ttu-id="d0833-258">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-258">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="d0833-260">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-260">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d0833-261">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-261">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d0833-262">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-262">Click **Assign** button on **Add Assignment** dialog.</span></span>

    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d0833-263">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="d0833-263">Testing single sign-on</span></span>

<span data-ttu-id="d0833-264">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-264">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d0833-265">액세스 패널에서 LinkedIn Lookup 타일을 클릭하면 개인 LinkedIn 계정 세부 정보를 제공해야 하는 조직 페이지로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-265">When you click the LinkedIn Lookup tile in the Access Panel, you should be redirected to Organizational page where you have to provide your personal LinkedIn account details.</span></span> <span data-ttu-id="d0833-266">개인 계정이 LinkedIn 비즈니스 계정과 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="d0833-266">It links your personal account with your LinkedIn business account.</span></span> 

<span data-ttu-id="d0833-267">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d0833-267">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="d0833-268">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="d0833-268">Additional resources</span></span>

* [<span data-ttu-id="d0833-269">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="d0833-269">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d0833-270">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="d0833-270">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_203.png

