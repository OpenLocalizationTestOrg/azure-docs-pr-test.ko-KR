---
title: "자습서: LinkedIn Elevate와 Azure Active Directory 통합 | Microsoft 문서"
description: "Azure Active Directory와 LinkedIn Elevate 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2ad9941b-c574-42c3-bd0f-5d6ec68537ef
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: jeedes
ms.openlocfilehash: 5336543e06d60be555722a615568b12048c2aa2f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-elevate"></a><span data-ttu-id="5ede9-103">자습서: LinkedIn Elevate와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="5ede9-103">Tutorial: Azure Active Directory integration with LinkedIn Elevate</span></span>

<span data-ttu-id="5ede9-104">이 자습서에서는 LinkedIn Elevate를 Azure AD(Azure Active Directory)와 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-104">In this tutorial, you learn how to integrate LinkedIn Elevate with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5ede9-105">LinkedIn Elevate를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-105">Integrating LinkedIn Elevate with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5ede9-106">LinkedIn Elevate에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-106">You can control in Azure AD who has access to LinkedIn Elevate</span></span>
- <span data-ttu-id="5ede9-107">사용자의 Azure AD 계정으로 LinkedIn Elevate에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-107">You can enable your users to automatically get signed-on to LinkedIn Elevate (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5ede9-108">단일 중앙 위치인 Azure 관리 포털에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="5ede9-109">Azure AD와의 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory를 사용한 응용 프로그램 액세스 및 Single Sign-On](active-directory-appssoaccess-whatis.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5ede9-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5ede9-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="5ede9-110">Prerequisites</span></span>

<span data-ttu-id="5ede9-111">LinkedIn Elevate와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-111">To configure Azure AD integration with LinkedIn Elevate, you need the following items:</span></span>

- <span data-ttu-id="5ede9-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="5ede9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5ede9-113">LinkedIn Elevate Single Sign-On을 사용하도록 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="5ede9-113">A LinkedIn Elevate single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5ede9-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5ede9-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5ede9-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="5ede9-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5ede9-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="5ede9-118">Scenario description</span></span>
<span data-ttu-id="5ede9-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5ede9-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5ede9-121">갤러리에서 LinkedIn Elevate 추가</span><span class="sxs-lookup"><span data-stu-id="5ede9-121">Adding LinkedIn Elevate from the gallery</span></span>
2. <span data-ttu-id="5ede9-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="5ede9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-elevate-from-the-gallery"></a><span data-ttu-id="5ede9-123">갤러리에서 LinkedIn Elevate 추가</span><span class="sxs-lookup"><span data-stu-id="5ede9-123">Adding LinkedIn Elevate from the gallery</span></span>
<span data-ttu-id="5ede9-124">LinkedIn Elevate가 Azure AD로 통합되도록 구성하려면 LinkedIn Elevate를 갤러리에서 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-124">To configure the integration of LinkedIn Elevate into Azure AD, you need to add LinkedIn Elevate from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5ede9-125">**갤러리에서 LinkedIn Elevate를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="5ede9-125">**To add LinkedIn Elevate from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5ede9-126">**[Azure 관리 포털](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5ede9-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5ede9-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="5ede9-131">대화 상자 위쪽에 있는 **추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-131">Click **Add** button on the top of the dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="5ede9-133">검색 상자에서 **LinkedIn Elevate**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-133">In the search box, type **LinkedIn Elevate**.</span></span> <span data-ttu-id="5ede9-134">결과 패널에서 **LinkedIn Elevate**를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-134">From results panel, click **LinkedIn Elevate** to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_000.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5ede9-136">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="5ede9-136">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5ede9-137">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 LinkedIn Elevate에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-137">In this section, you configure and test Azure AD single sign-on with LinkedIn Elevate based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5ede9-138">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 LinkedIn Elevate 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-138">For single sign-on to work, Azure AD needs to know what the counterpart user in LinkedIn Elevate is to a user in Azure AD.</span></span> <span data-ttu-id="5ede9-139">즉, Azure AD 사용자와 LinkedIn Elevate의 관련 사용자 간에 연결 관계가 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-139">In other words, a link relationship between an Azure AD user and the related user in LinkedIn Elevate needs to be established.</span></span>

<span data-ttu-id="5ede9-140">이 연결 관계는 Azure AD의 **사용자 이름** 값을 LinkedIn Elevate의 **Username** 값으로 할당하여 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-140">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in LinkedIn Elevate.</span></span>

<span data-ttu-id="5ede9-141">LinkedIn Elevate에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-141">To configure and test Azure AD single sign-on with LinkedIn Elevate, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5ede9-142">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5ede9-143">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5ede9-144">**[LinkedIn Elevate 테스트 사용자 만들기](#creating-a-linkedin-elevate-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-144">**[Creating a LinkedIn Elevate test user](#creating-a-linkedin-elevate-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="5ede9-145">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-145">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5ede9-146">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-146">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5ede9-147">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="5ede9-147">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5ede9-148">이 섹션에서는 Azure 관리 포털에서 Azure AD Single Sign-On을 사용하도록 설정하고 LinkedIn Elevate 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-148">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your LinkedIn Elevate application.</span></span>

<span data-ttu-id="5ede9-149">**LinkedIn Elevate에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="5ede9-149">**To configure Azure AD single sign-on with LinkedIn Elevate, perform the following steps:**</span></span>

1. <span data-ttu-id="5ede9-150">Azure 관리 포털의 **LinkedIn Elevate** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-150">In the Azure Management portal, on the **LinkedIn Elevate** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="5ede9-152">**Single sign on** 대화 상자에서 **모드**로 **SAML 기반 로그온**을 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-152">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedin_01.png)

3. <span data-ttu-id="5ede9-154">다른 웹 브라우저 창에서 LinkedIn Elevate 테넌트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-154">In a different web browser window, sign-on to your LinkedIn Elevate tenant as an administrator.</span></span>

4. <span data-ttu-id="5ede9-155">**계정 센터**의 **설정** 아래에서 **전역 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-155">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="5ede9-156">드롭다운 목록에서 **Elevate - Elevate AAD 테스트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-156">Also, select **Elevate - Elevate AAD Test** from the dropdown list.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_01.png)

5. <span data-ttu-id="5ede9-158">**OR Click Here to load and copy individual fields from the form**(또는 양식에서 개별 필드를 로드하여 복사하려면 여기를 클릭)을 클릭하고 **엔터티 Id** 및 **ACS(Assertion Consumer Access) URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-158">Click on **OR Click Here to load and copy individual fields from the form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_03.png)

6. <span data-ttu-id="5ede9-160">**IdP 시작** 모드에서 SSO를 구성하려면 Azure Portal의 **LinkedIn Elevate 도메인 및 URL**에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-160">On Azure Portal, under **LinkedIn Elevate Domain and URLs**, perform the following steps if you want to configure SSO in **IdP Initiated** mode</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_signon_01.png)

    <span data-ttu-id="5ede9-162">a.</span><span class="sxs-lookup"><span data-stu-id="5ede9-162">a.</span></span> <span data-ttu-id="5ede9-163">**식별자** 텍스트 상자에 LinkedIn 포털에서 복사한 **엔티티 ID**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-163">In the **Identifier** textbox, enter the **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="5ede9-164">b.</span><span class="sxs-lookup"><span data-stu-id="5ede9-164">b.</span></span> <span data-ttu-id="5ede9-165">**회신 URL** 텍스트 상자에 LinkedIn 포털에서 복사한 **ACS(Assertion Consumer Access) URL**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-165">In the **Reply URL** textbox, enter the **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

7. <span data-ttu-id="5ede9-166">**SP 시작**에서 SSO를 구성하려면 구성 섹션에서 고급 URL 설정 표시 옵션을 클릭하고 다음 패턴으로 로그인 URL을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-166">If you want to configure SSO in **SP Initiated**, then click Show Advanced URL setting option in the configuration section and configure the sign on URL with the following pattern:</span></span>

    `https://www.linkedin.com/checkpoint/enterprise/login/<AccountId>?application=elevate&applicationInstanceId=<InstanceId>` 
    
    ![Single Sign-On 구성](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_signon_02.png) 
    
8. <span data-ttu-id="5ede9-168">LinkedIn Elevate 응용 프로그램은 특정 형식의 SAML 어설션이 필요하기 때문에 SAML 토큰 특성 구성에 사용자 지정 특성 매핑을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-168">Your LinkedIn Elevate application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="5ede9-169">다음 스크린샷은 이에 대한 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-169">The following screenshot shows an example for this.</span></span> <span data-ttu-id="5ede9-170">**사용자 ID**의 기본값은 **user.userprincipalname**이지만 LinkedIn Elevate에는 이것이 사용자의 전자 메일 주소와 매핑되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-170">The default value of **User Identifier** is **user.userprincipalname** but LinkedIn Elevate expects this to be mapped with the user's email address.</span></span> <span data-ttu-id="5ede9-171">목록에서 **user.mail** 특성을 사용하거나 조직 구성을 기반으로 적절한 특성 값을 사용할 수 있기 위해서입니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-171">For that you can use **user.mail** attribute from the list or use the appropriate attribute value based on your organization configuration.</span></span> 

    ![Single Sign-on 구성](./media/active-directory-saas-linkedinElevate-tutorial/updateusermail.png)

9. <span data-ttu-id="5ede9-173">**사용자 특성** 섹션에서 **기타 모든 사용자 특성 보기 및 편집**을 클릭하고 특성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-173">In **User Attributes** section, click **View and edit all other user attributes** and set the attributes.</span></span> <span data-ttu-id="5ede9-174">**department**라는 또 다른 클레임을 추가하고 값을 **user.department**에 매핑해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-174">You need to add another claim named **department** and the value needs to be mapped to **user.department**.</span></span>

    | <span data-ttu-id="5ede9-175">특성 이름</span><span class="sxs-lookup"><span data-stu-id="5ede9-175">Attribute Name</span></span> | <span data-ttu-id="5ede9-176">특성 값</span><span class="sxs-lookup"><span data-stu-id="5ede9-176">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="5ede9-177">department</span><span class="sxs-lookup"><span data-stu-id="5ede9-177">department</span></span>| <span data-ttu-id="5ede9-178">user.department</span><span class="sxs-lookup"><span data-stu-id="5ede9-178">user.department</span></span> |

      ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-linkedinElevate-tutorial/userattribute.png)

      <span data-ttu-id="5ede9-180">a.</span><span class="sxs-lookup"><span data-stu-id="5ede9-180">a.</span></span> <span data-ttu-id="5ede9-181">[특성 추가]를 클릭하여 특성 세부 정보 페이지를 열고, 아래와 같이 부서 특성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-181">Click on Add attribute to open the attribute details page add the department attribute as shown below-</span></span>

      ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-linkedinElevate-tutorial/adduserattribute.png)

      <span data-ttu-id="5ede9-183">b.</span><span class="sxs-lookup"><span data-stu-id="5ede9-183">b.</span></span> <span data-ttu-id="5ede9-184">**확인**을 클릭하여 해당 특성을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-184">Click on **Ok** to save the attribute.</span></span>

      <span data-ttu-id="5ede9-185">c.</span><span class="sxs-lookup"><span data-stu-id="5ede9-185">c.</span></span> <span data-ttu-id="5ede9-186">특성 **emailaddress**의 이름을 **email**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-186">Change the name of the attribute **emailaddress** to **email**.</span></span>


10. <span data-ttu-id="5ede9-187">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 XML 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-187">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_certificate.png) 

11. <span data-ttu-id="5ede9-189">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-189">Click **Save**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_400.png)

12. <span data-ttu-id="5ede9-191">**LinkedIn 관리 설정** 섹션으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-191">Go to **LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="5ede9-192">XML 파일 업로드 옵션을 클릭하여 Azure Portal에서 방금 다운로드한 XML 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-192">Upload the XML file you just downloaded from the Azure portal by clicking on the Upload XML file option.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_metadata_03.png)

13. <span data-ttu-id="5ede9-194">**설정**을 클릭하여 SSO를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-194">Click **On** to enable SSO.</span></span> <span data-ttu-id="5ede9-195">SSO 상태가 **연결 안 됨**에서 **연결됨**으로 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-195">SSO status will change from **Not Connected** to **Connected**</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_05.png)

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5ede9-197">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="5ede9-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="5ede9-198">이 섹션의 목적은 Azure 관리 포털에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-198">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="5ede9-200">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="5ede9-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5ede9-201">**Azure 관리 포털**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-201">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5ede9-203">**사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭하여 사용자 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-203">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5ede9-205">대화 상자 위쪽에서 **추가**를 클릭하여 **사용자** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-205">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5ede9-207">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5ede9-209">a.</span><span class="sxs-lookup"><span data-stu-id="5ede9-209">a.</span></span> <span data-ttu-id="5ede9-210">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5ede9-211">b.</span><span class="sxs-lookup"><span data-stu-id="5ede9-211">b.</span></span> <span data-ttu-id="5ede9-212">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5ede9-213">c.</span><span class="sxs-lookup"><span data-stu-id="5ede9-213">c.</span></span> <span data-ttu-id="5ede9-214">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="5ede9-215">d.</span><span class="sxs-lookup"><span data-stu-id="5ede9-215">d.</span></span> <span data-ttu-id="5ede9-216">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-216">Click **Create**.</span></span> 

### <a name="creating-a-linkedin-elevate-test-user"></a><span data-ttu-id="5ede9-217">LinkedIn Elevate 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="5ede9-217">Creating a LinkedIn Elevate test user</span></span>

<span data-ttu-id="5ede9-218">Linked Elevate 응용 프로그램이 JIT(Just-in-time) 사용자 프로비저닝을 지원하며 인증 후에 응용 프로그램에서 사용자가 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-218">Linked Elevate Application supports Just in time user provisioning and after authentication users will be created in the application automatically.</span></span> <span data-ttu-id="5ede9-219">LinkedIn Elevate 포털의 관리 설정 페이지에서 **Automatically Assign licenses**(라이선스 자동 할당) 스위치를 전환하여 JIT(Just-in-time) 프로비저닝을 사용하도록 활성화하면 사용자에게 라이선스가 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-219">On the admin settings page on the LinkedIn Elevate portal flip the switch **Automatically Assign licenses** to active to enable Just in time provisioning and this will also assign a license to the user.</span></span>

   ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-linkedinElevate-tutorial/LinkedinUserprovswitch.png)

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="5ede9-221">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="5ede9-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="5ede9-222">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 LinkedIn Elevate에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-222">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to LinkedIn Elevate.</span></span>

![사용자 할당][200] 

<span data-ttu-id="5ede9-224">**Britta Simon을 LinkedIn Elevate에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="5ede9-224">**To assign Britta Simon to LinkedIn Elevate, perform the following steps:**</span></span>

1. <span data-ttu-id="5ede9-225">Azure 관리 포털에서 응용 프로그램 보기를 열고 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-225">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="5ede9-227">응용 프로그램 목록에서 **LinkedIn Elevate**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-227">In the applications list, select **LinkedIn Elevate**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_0001.png) 

3. <span data-ttu-id="5ede9-229">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-229">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="5ede9-231">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-231">Click **Add** button.</span></span> <span data-ttu-id="5ede9-232">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="5ede9-234">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5ede9-235">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5ede9-236">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5ede9-237">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="5ede9-237">Testing single sign-on</span></span>

<span data-ttu-id="5ede9-238">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-238">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="5ede9-239">액세스 패널에서 LinkedIn Elevate 타일을 클릭하면 Azure 로그온 페이지가 표시되고 로그온이 완료되면 LinkedIn Elevate 응용 프로그램에 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ede9-239">When you click the LinkedIn Elevate tile in the Access Panel, you should get the Azure Sign-on page and on after successful sign-on, you should get into your LinkedIn Elevate application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5ede9-240">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="5ede9-240">Additional resources</span></span>

* [<span data-ttu-id="5ede9-241">자습서: Azure Active Directory를 사용한 자동 사용자 프로비전을 위한 LinkedIn Elevate 구성</span><span class="sxs-lookup"><span data-stu-id="5ede9-241">Tutorial: Configuring LinkedIn Elevate for automatic user provisioning with Azure Active Directory</span></span>](active-directory-saas-linkedinelevate-provisioning-tutorial.md)
* [<span data-ttu-id="5ede9-242">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="5ede9-242">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5ede9-243">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="5ede9-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_203.png
