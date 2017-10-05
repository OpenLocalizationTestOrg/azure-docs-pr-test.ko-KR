---
title: "자습서: GitHub와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 GitHub 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4395bd95-05de-4deb-87a5-dc3bc8ac4d95
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 9dc12bc2e313bcb2000724d035156c5054d14e1c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-github"></a><span data-ttu-id="d5b79-103">자습서: GitHub와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="d5b79-103">Tutorial: Azure Active Directory integration with GitHub</span></span>

<span data-ttu-id="d5b79-104">이 자습서에서는 Azure AD(Azure Active Directory)와 GitHub를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-104">In this tutorial, you learn how to integrate GitHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d5b79-105">GitHub를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-105">Integrating GitHub with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d5b79-106">GitHub에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-106">You can control in Azure AD who has access to GitHub</span></span>
- <span data-ttu-id="d5b79-107">사용자가 해당 Azure AD 계정으로 GitHub에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-107">You can enable your users to automatically get signed-on to GitHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d5b79-108">단일 중앙 위치인 Azure 관리 포털에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="d5b79-109">Azure AD와의 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory를 사용한 응용 프로그램 액세스 및 Single Sign-On](active-directory-appssoaccess-whatis.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d5b79-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d5b79-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d5b79-110">Prerequisites</span></span>

<span data-ttu-id="d5b79-111">GitHub와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-111">To configure Azure AD integration with GitHub, you need the following items:</span></span>

- <span data-ttu-id="d5b79-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="d5b79-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d5b79-113">GitHub Single Sign-On을 사용하도록 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="d5b79-113">A GitHub single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="d5b79-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="d5b79-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d5b79-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="d5b79-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="d5b79-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="d5b79-118">Scenario description</span></span>
<span data-ttu-id="d5b79-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d5b79-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d5b79-121">갤러리에서 GitHub 추가</span><span class="sxs-lookup"><span data-stu-id="d5b79-121">Adding GitHub from the gallery</span></span>
2. <span data-ttu-id="d5b79-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="d5b79-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-github-from-the-gallery"></a><span data-ttu-id="d5b79-123">갤러리에서 GitHub 추가</span><span class="sxs-lookup"><span data-stu-id="d5b79-123">Adding GitHub from the gallery</span></span>
<span data-ttu-id="d5b79-124">Azure AD에 GitHub 통합을 구성하려면 갤러리의 GitHub를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-124">To configure the integration of GitHub into Azure AD, you need to add GitHub from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d5b79-125">**갤러리에서 GitHub를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="d5b79-125">**To add GitHub from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d5b79-126">**[Azure 관리 포털](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d5b79-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d5b79-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="d5b79-131">대화 상자 위쪽에 있는 **추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-131">Click **Add** button on the top of the dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="d5b79-133">검색 상자에서 **GitHub.com**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-133">In the search box, type **GitHub.com**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-github-tutorial/tutorial_github_search02.png)

5. <span data-ttu-id="d5b79-135">결과 창에서 **GitHub**를 선택하고 **추가** 단추를 클릭하여 해당 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-135">In the results panel, select **GitHub**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-github-tutorial/tutorial_github_search_result02.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d5b79-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="d5b79-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d5b79-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 GitHub에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-138">In this section, you configure and test Azure AD single sign-on with GitHub based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d5b79-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 GitHub 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-139">For single sign-on to work, Azure AD needs to know what the counterpart user in GitHub is to a user in Azure AD.</span></span> <span data-ttu-id="d5b79-140">즉, Azure AD 사용자와 GitHub의 관련 사용자 간에 연결이 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-140">In other words, a link relationship between an Azure AD user and the related user in GitHub needs to be established.</span></span>

<span data-ttu-id="d5b79-141">이 연결 관계는 Azure AD의 **사용자 이름** 값을 GitHub의 **Username** 값으로 할당하여 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in GitHub.</span></span>

<span data-ttu-id="d5b79-142">GitHub에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-142">To configure and test Azure AD single sign-on with GitHub, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d5b79-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d5b79-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d5b79-145">**[GitHub 테스트 사용자 만들기](#creating-a-GitHub-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 GitHub에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-145">**[Creating a GitHub test user](#creating-a-GitHub-test-user)** - to have a counterpart of Britta Simon in GitHub that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="d5b79-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d5b79-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d5b79-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="d5b79-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d5b79-149">이 섹션에서는 Azure 관리 포털에서 Azure AD Single Sign-On을 사용하도록 설정하고 GitHub 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your GitHub application.</span></span>

<span data-ttu-id="d5b79-150">**GitHub에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="d5b79-150">**To configure Azure AD single sign-on with GitHub, perform the following steps:**</span></span>

1. <span data-ttu-id="d5b79-151">Azure 관리 포털의 **GitHub** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-151">In the Azure Management portal, on the **GitHub** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-On 구성][4]

2. <span data-ttu-id="d5b79-153">**Single sign on** 대화 상자에서 **모드**로 **SAML 기반 로그온**을 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Single Sign-On 구성](./media/active-directory-saas-github-tutorial/tutorial_github_01.png)

3. <span data-ttu-id="d5b79-155">**GitHub 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-155">On the **GitHub Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-github-tutorial/tutorial_github_saml011.png)

    <span data-ttu-id="d5b79-157">a.</span><span class="sxs-lookup"><span data-stu-id="d5b79-157">a.</span></span> <span data-ttu-id="d5b79-158">**로그인 URL** 텍스트 상자에서 값으로 `https://github.com/orgs/<entity-id>/sso`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-158">In the **Sign-on URL** textbox, type the value as: `https://github.com/orgs/<entity-id>/sso`</span></span>

    <span data-ttu-id="d5b79-159">b.</span><span class="sxs-lookup"><span data-stu-id="d5b79-159">b.</span></span> <span data-ttu-id="d5b79-160">**식별자** 텍스트 상자에서 `https://github.com/orgs/<entity-id>` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-160">In the **Identifier** textbox, type a URL using the following pattern: `https://github.com/orgs/<entity-id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d5b79-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-161">Please note that these are not the real values.</span></span> <span data-ttu-id="d5b79-162">이러한 값을 실제 로그인 URL 및 식별자로 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-162">You have to update these values with the actual Sing-on URL and Identifier.</span></span> <span data-ttu-id="d5b79-163">식별자에는 고유한 문자열 값을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-163">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="d5b79-164">GitHub 관리자 섹션으로 이동하여 이러한 값을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-164">Go to GitHub Admin section to retrieve these values.</span></span> 

4. <span data-ttu-id="d5b79-165">**사용자 특성** 섹션에서 **사용자 식별자**를 user.mail로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-165">On the **User Attributes** section, select **User Identifier** as user.mail.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-github-tutorial/tutorial_github_attribute_new01.png)
    
5. <span data-ttu-id="d5b79-167">**SAML 서명 인증서** 섹션에서 **새 인증서 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-167">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-github-tutorial/tutorial_github_03.png)

6. <span data-ttu-id="d5b79-169">**새 인증서 만들기** 대화 상자에서 달력 아이콘을 클릭하고 **만료 날짜**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-169">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="d5b79-170">그런 후 **저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-170">Then click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-github-tutorial/tutorial_general_300.png)

7. <span data-ttu-id="d5b79-172">**SAML 서명 인증서** 섹션에서 **새 인증서 활성화**를 선택한 후 **저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-172">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-github-tutorial/tutorial_github_04.png)

8. <span data-ttu-id="d5b79-174">팝업 **롤오버 인증서** 창에서 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-174">On the pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-github-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="d5b79-176">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-176">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-github-tutorial/tutorial_github_05.png) 

10. <span data-ttu-id="d5b79-178">**GitHub 구성** 섹션에서 **GitHub 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-178">On the **GitHub Configuration** section, click **Configure GitHub** to open **Configure sign-on** window.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-github-tutorial/tutorial_github_06.png) 

    ![Single Sign-On 구성](./media/active-directory-saas-github-tutorial/tutorial_github_07.png)

11. <span data-ttu-id="d5b79-181">다른 웹 브라우저 창에서 GitHub 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-181">In a different web browser window, log into your GitHub organization site as an administrator.</span></span>

12. <span data-ttu-id="d5b79-182">**설정**으로 이동하고 **보안**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-182">Navigate to **Settings** and click **Security**</span></span>

    ![설정](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_03.png)

13. <span data-ttu-id="d5b79-184">**SAML 인증 사용** 상자를 확인하여 Single Sign-On 구성 필드를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-184">Check the **Enable SAML authentication** box, revealing the Single Sign-on configuration fields.</span></span> <span data-ttu-id="d5b79-185">그런 다음 Single Sign-On URL 값을 사용하여 Azure AD 구성에서 Single Sign-On URL을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-185">Then, use the single sign-on URL value to update the Single sign-on URL on Azure AD configuration.</span></span>

    ![설정](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_13.png)

14. <span data-ttu-id="d5b79-187">다음 필드를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-187">Configure the following fields:</span></span>

    <span data-ttu-id="d5b79-188">a.</span><span class="sxs-lookup"><span data-stu-id="d5b79-188">a.</span></span> <span data-ttu-id="d5b79-189">**로그인 URL**: Azure AD의 **GitHub 구성** 섹션에서 **SAML Single Sign-On 서비스 URL**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-189">**Sign on URL**: Enter **SAML Single sign-on Service URL** from the **Configure GitHub** section on Azure AD</span></span>

    <span data-ttu-id="d5b79-190">b.</span><span class="sxs-lookup"><span data-stu-id="d5b79-190">b.</span></span> <span data-ttu-id="d5b79-191">**발급자**: Azure AD의 **GitHub 구성** 섹션에서 **SAML 엔터티 ID**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-191">**Issuer**: Enter **SAML Entity ID** from the **Configure GitHub** section on Azure AD</span></span>

    <span data-ttu-id="d5b79-192">c.</span><span class="sxs-lookup"><span data-stu-id="d5b79-192">c.</span></span> <span data-ttu-id="d5b79-193">**공용 인증서**: Azure AD에서 다운로드한 인증서를 메모장에서 열고 "BEGIN CERTIFICATE"(인증서 시작) 및 "END CERTIFICATE"(인증서 끝)를 포함한 내용을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-193">**Public Certificate**: Open the downloaded certificate from Azure AD in a notepad and copy the content including "BEGIN CERTIFICATE" and "END CERTIFICATE"</span></span>

    ![설정](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_051.png)

15. <span data-ttu-id="d5b79-195">**SAML 구성 테스트**를 클릭하여 SSO 동안 유효성 검사 실패 또는 오류가 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-195">Click on **Test SAML configuration** to confirm that no validation failures or errors during SSO.</span></span>

    ![설정](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_06.png)

16. <span data-ttu-id="d5b79-197">페이지 맨 아래에 있는 **저장**</span><span class="sxs-lookup"><span data-stu-id="d5b79-197">Click **Save**</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d5b79-198">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="d5b79-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="d5b79-199">이 섹션의 목적은 Azure 관리 포털에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-199">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="d5b79-201">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="d5b79-201">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d5b79-202">**Azure 관리 포털**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-202">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-github-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d5b79-204">**사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭하여 사용자 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-204">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-github-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d5b79-206">대화 상자 위쪽에서 **추가**를 클릭하여 **사용자** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-206">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-github-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d5b79-208">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-208">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-github-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d5b79-210">a.</span><span class="sxs-lookup"><span data-stu-id="d5b79-210">a.</span></span> <span data-ttu-id="d5b79-211">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-211">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d5b79-212">b.</span><span class="sxs-lookup"><span data-stu-id="d5b79-212">b.</span></span> <span data-ttu-id="d5b79-213">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-213">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d5b79-214">c.</span><span class="sxs-lookup"><span data-stu-id="d5b79-214">c.</span></span> <span data-ttu-id="d5b79-215">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-215">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d5b79-216">d.</span><span class="sxs-lookup"><span data-stu-id="d5b79-216">d.</span></span> <span data-ttu-id="d5b79-217">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-217">Click **Create**.</span></span> 


### <a name="creating-a-github-test-user"></a><span data-ttu-id="d5b79-218">GitHub 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="d5b79-218">Creating a GitHub test user</span></span>

<span data-ttu-id="d5b79-219">Azure AD 사용자가 GitHub에 로그인하려면 GitHub에 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-219">In order to enable Azure AD users to log into GitHub, they must be provisioned into GitHub.</span></span>  
<span data-ttu-id="d5b79-220">GitHub의 경우 프로비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-220">In the case of GitHub, provisioning is a manual task.</span></span>

<span data-ttu-id="d5b79-221">**사용자 계정을 프로비전하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="d5b79-221">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="d5b79-222">GitHub 회사 사이트에 관리자 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-222">Log in to your GitHub company site as an administrator.</span></span>

2. <span data-ttu-id="d5b79-223">**피플**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-223">Click **People**.</span></span>

    <span data-ttu-id="d5b79-224">![사람](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_08.png "사람")</span><span class="sxs-lookup"><span data-stu-id="d5b79-224">![People](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_08.png "People")</span></span>

3. <span data-ttu-id="d5b79-225">**멤버 초대**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-225">Click **Invite member**.</span></span>

    <span data-ttu-id="d5b79-226">![사용자 초대](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_09.png "사용자 초대")</span><span class="sxs-lookup"><span data-stu-id="d5b79-226">![Invite Users](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_09.png "Invite Users")</span></span>

4. <span data-ttu-id="d5b79-227">**멤버 초대** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-227">On the **Invite member** dialog page, perform the following steps:</span></span>

    <span data-ttu-id="d5b79-228">a.</span><span class="sxs-lookup"><span data-stu-id="d5b79-228">a.</span></span> <span data-ttu-id="d5b79-229">**전자 메일** 텍스트 상자에 Britta Simon 계정의 전자 메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-229">In the **Email** textbox, type the email address of Britta Simon account.</span></span>

    <span data-ttu-id="d5b79-230">![피플 초대](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_10.png "피플 초대")</span><span class="sxs-lookup"><span data-stu-id="d5b79-230">![Invite People](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_10.png "Invite People")</span></span>
    
    <span data-ttu-id="d5b79-231">b.</span><span class="sxs-lookup"><span data-stu-id="d5b79-231">b.</span></span> <span data-ttu-id="d5b79-232">**초대 보내기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-232">Click **Send Invitation**.</span></span>

    <span data-ttu-id="d5b79-233">![피플 초대](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_11.png "피플 초대")</span><span class="sxs-lookup"><span data-stu-id="d5b79-233">![Invite People](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_11.png "Invite People")</span></span>

    > [!NOTE]
    > <span data-ttu-id="d5b79-234">Azure Active Directory 계정 보유자는 활성화되기 전에 전자 메일을 받고 링크를 따라 계정을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-234">The Azure Active Directory account holder will receive an email and follow a link to confirm their account before it becomes active.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d5b79-235">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="d5b79-235">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d5b79-236">이 섹션에서는 GitHub에 대한 액세스 권한을 부여하여 Britta Simon이 Azure Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-236">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to GitHub.</span></span>

![사용자 할당][200] 

<span data-ttu-id="d5b79-238">**Britta Simon을 GitHub에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="d5b79-238">**To assign Britta Simon to GitHub, perform the following steps:**</span></span>

1. <span data-ttu-id="d5b79-239">Azure 관리 포털에서 응용 프로그램 보기를 열고 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-239">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="d5b79-241">응용 프로그램 목록에서 **GitHub.com**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-241">In the applications list, select **GitHub.com**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-github-tutorial/tutorial_github_search_result021.png) 

3. <span data-ttu-id="d5b79-243">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-243">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="d5b79-245">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-245">Click **Add** button.</span></span> <span data-ttu-id="d5b79-246">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-246">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="d5b79-248">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-248">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d5b79-249">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-249">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d5b79-250">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-250">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="d5b79-251">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="d5b79-251">Testing single sign-on</span></span>

<span data-ttu-id="d5b79-252">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-252">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d5b79-253">액세스 패널에서 GitHub 타일을 클릭하면 GitHub 응용 프로그램에 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-253">When you click the GitHub tile in the Access Panel, you should get signed-on to your GitHub application.</span></span> <span data-ttu-id="d5b79-254">조직 계정으로 로그인하지만 개인 계정으로 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b79-254">You'll be logging in as an Organization account but then need to log in with your personal account.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="d5b79-255">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="d5b79-255">Additional resources</span></span>

* [<span data-ttu-id="d5b79-256">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="d5b79-256">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d5b79-257">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="d5b79-257">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-github-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-github-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-github-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-github-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-github-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-github-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-github-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-github-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-github-tutorial/tutorial_general_203.png
