---
title: "자습서: SAML SSO for Jira by resolution GmbH와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory 및 SAML SSO for Jira by resolution GmbH 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 20e18819-e330-4e40-bd8d-2ff3b98e035f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: jeedes
ms.openlocfilehash: cde5983710185d1e46a5601b16bbfb1c0fcae382
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-saml-sso-for-jira-by-resolution-gmbh"></a><span data-ttu-id="aae8e-103">자습서: SAML SSO for Jira by resolution GmbH와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="aae8e-103">Tutorial: Azure Active Directory integration with SAML SSO for Jira by resolution GmbH</span></span>

<span data-ttu-id="aae8e-104">이 자습서에서는 Azure AD(Azure Active Directory)와 SAML SSO for Jira by resolution GmbH를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-104">In this tutorial, you learn how to integrate SAML SSO for Jira by resolution GmbH with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="aae8e-105">SAML SSO for Jira by resolution GmbH와 Azure AD를 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-105">Integrating SAML SSO for Jira by resolution GmbH with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="aae8e-106">SAML SSO for Jira by resolution GmbH에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-106">You can control in Azure AD who has access to SAML SSO for Jira by resolution GmbH</span></span>
- <span data-ttu-id="aae8e-107">사용자가 해당 Azure AD 계정으로 SAML SSO for Jira by resolution GmbH에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-107">You can enable your users to automatically get signed-on to SAML SSO for Jira by resolution GmbH (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="aae8e-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="aae8e-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="aae8e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aae8e-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="aae8e-110">Prerequisites</span></span>

<span data-ttu-id="aae8e-111">SAML SSO for Jira by resolution GmbH와 Azure AD를 통합하도록 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-111">To configure Azure AD integration with SAML SSO for Jira by resolution GmbH, you need the following items:</span></span>

- <span data-ttu-id="aae8e-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="aae8e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="aae8e-113">SAML SSO for Jira by resolution GmbH Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="aae8e-113">A SAML SSO for Jira by resolution GmbH single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="aae8e-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="aae8e-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="aae8e-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="aae8e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="aae8e-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="aae8e-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="aae8e-118">Scenario description</span></span>
<span data-ttu-id="aae8e-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="aae8e-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="aae8e-121">갤러리에서 SAML SSO for Jira by resolution GmbH 추가</span><span class="sxs-lookup"><span data-stu-id="aae8e-121">Adding SAML SSO for Jira by resolution GmbH from the gallery</span></span>
2. <span data-ttu-id="aae8e-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="aae8e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-saml-sso-for-jira-by-resolution-gmbh-from-the-gallery"></a><span data-ttu-id="aae8e-123">갤러리에서 SAML SSO for Jira by resolution GmbH 추가</span><span class="sxs-lookup"><span data-stu-id="aae8e-123">Adding SAML SSO for Jira by resolution GmbH from the gallery</span></span>
<span data-ttu-id="aae8e-124">Azure AD에 SAML SSO for Jira by resolution GmbH를 통합하도록 구성하려면 갤러리에서 관리되는 SaaS 앱 목록으로 SAML SSO for Jira by resolution GmbH를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-124">To configure the integration of SAML SSO for Jira by resolution GmbH into Azure AD, you need to add SAML SSO for Jira by resolution GmbH from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="aae8e-125">**갤러리에서 SAML SSO for Jira by resolution GmbH를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="aae8e-125">**To add SAML SSO for Jira by resolution GmbH from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="aae8e-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="aae8e-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="aae8e-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="aae8e-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="aae8e-133">검색 상자에서 **SAML SSO for Jira by resolution GmbH**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-133">In the search box, type **SAML SSO for Jira by resolution GmbH**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_search.png)

5. <span data-ttu-id="aae8e-135">결과 창에서 **SAML SSO for Jira by resolution GmbH**를 선택한 다음 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-135">In the results panel, select **SAML SSO for Jira by resolution GmbH**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="aae8e-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="aae8e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="aae8e-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 하여 SAML SSO for Jira by resolution GmbH에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-138">In this section, you configure and test Azure AD single sign-on with SAML SSO for Jira by resolution GmbH based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="aae8e-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 SAML SSO for Jira by resolution GmbH 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SAML SSO for Jira by resolution GmbH is to a user in Azure AD.</span></span> <span data-ttu-id="aae8e-140">즉 Azure AD 사용자와 SAML SSO for Jira by resolution GmbH의 관련 사용자 간의 링크 관계가 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-140">In other words, a link relationship between an Azure AD user and the related user in SAML SSO for Jira by resolution GmbH needs to be established.</span></span>

<span data-ttu-id="aae8e-141">SAML SSO for Jira by resolution GmbH에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-141">In SAML SSO for Jira by resolution GmbH, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="aae8e-142">SAML SSO for Jira by resolution GmbH에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-142">To configure and test Azure AD single sign-on with SAML SSO for Jira by resolution GmbH, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="aae8e-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="aae8e-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="aae8e-145">**[SAML SSO for Jira by resolution GmbH 테스트 사용자 만들기](#creating-a-saml-sso-for-jira-by-resolution-gmbh-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 SAML SSO for Jira by resolution GmbH에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-145">**[Creating a SAML SSO for Jira by resolution GmbH test user](#creating-a-saml-sso-for-jira-by-resolution-gmbh-test-user)** - to have a counterpart of Britta Simon in SAML SSO for Jira by resolution GmbH that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="aae8e-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="aae8e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="aae8e-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="aae8e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="aae8e-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 SAML SSO for Jira by resolution GmbH 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SAML SSO for Jira by resolution GmbH application.</span></span>

<span data-ttu-id="aae8e-150">**SAML SSO for Jira by resolution GmbH에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="aae8e-150">**To configure Azure AD single sign-on with SAML SSO for Jira by resolution GmbH, perform the following steps:**</span></span>

1. <span data-ttu-id="aae8e-151">Azure Portal의 **SAML SSO for Jira by resolution GmbH** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-151">In the Azure portal, on the **SAML SSO for Jira by resolution GmbH** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="aae8e-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_samlbase.png)

3. <span data-ttu-id="aae8e-155">**IDP** 시작 모드에서 응용 프로그램을 구성하려면 **SAML SSO for Jira by resolution GmbH 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-155">On the **SAML SSO for Jira by resolution GmbH Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_url_1.png)

    <span data-ttu-id="aae8e-157">a.</span><span class="sxs-lookup"><span data-stu-id="aae8e-157">a.</span></span> <span data-ttu-id="aae8e-158">**식별자** 텍스트 상자에서 `https://<server-base-url>/plugins/servlet/samlsso` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>

    <span data-ttu-id="aae8e-159">b.</span><span class="sxs-lookup"><span data-stu-id="aae8e-159">b.</span></span> <span data-ttu-id="aae8e-160">**회신 URL** 텍스트 상자에 다음 패턴으로 URL을 입력합니다.`https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="aae8e-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>

4. <span data-ttu-id="aae8e-161">**고급 URL 설정 표시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="aae8e-162">**SP** 시작 모드에서 응용 프로그램을 구성하려면:</span><span class="sxs-lookup"><span data-stu-id="aae8e-162">If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_url_2.png)

    <span data-ttu-id="aae8e-164">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="aae8e-164">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="aae8e-165">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-165">These values are not real.</span></span> <span data-ttu-id="aae8e-166">이러한 값을 실제 식별자, 회신 URL 및 로그온 URL로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-166">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="aae8e-167">이러한 값을 얻으려면 [SAML SSO for Jira by resolution GmbH 지원 팀](https://www.resolution.de/go/support)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="aae8e-167">Contact [SAML SSO for Jira by resolution GmbH Client support team](https://www.resolution.de/go/support) to get these values.</span></span> 

5. <span data-ttu-id="aae8e-168">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 메타데이터 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-168">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_certificate.png) 

6. <span data-ttu-id="aae8e-170">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-170">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-samlssojira-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="aae8e-172">다른 웹 브라우저 창에서 **SAML SSO for Jira by resolution GmbH 관리 포털**에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-172">In a different web browser window, log in to your **SAML SSO for Jira by resolution GmbH admin portal** as an administrator.</span></span>

8. <span data-ttu-id="aae8e-173">마우스로 선 위를 가리키고 **추가 기능**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-173">Hover on cog and click the **Add-ons**.</span></span>
    
    ![Single Sign-on 구성](./media/active-directory-saas-samlssojira-tutorial/addon1.png)

9. <span data-ttu-id="aae8e-175">[관리자 액세스] 페이지로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-175">You are redirected to Administrator Access page.</span></span> <span data-ttu-id="aae8e-176">**암호**를 입력하고 **확인** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-176">Enter the **Password** and click **Confirm** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-samlssojira-tutorial/addon2.png)

10. <span data-ttu-id="aae8e-178">[추가 기능] 탭 섹션에서 **새 추가 기능 찾기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-178">Under Add-ons tab section, click **Find new add-ons**.</span></span> <span data-ttu-id="aae8e-179">**SAML Single Sign On(SSO) for JIRA**를 검색하고 **설치** 단추를 클릭하여 새 SAML 플러그 인을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-179">Search **SAML Single Sign On (SSO) for JIRA** and click **Install** button to install the new SAML plugin.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-samlssojira-tutorial/addon7.png)

11. <span data-ttu-id="aae8e-181">플러그 인 설치가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-181">The plugin installation will start.</span></span> <span data-ttu-id="aae8e-182">**닫기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-182">Click **Close**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-samlssojira-tutorial/addon8.png)

    ![Single Sign-on 구성](./media/active-directory-saas-samlssojira-tutorial/addon9.png)

12. <span data-ttu-id="aae8e-185">**관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-185">Click **Manage**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-samlssojira-tutorial/addon10.png)
    
13. <span data-ttu-id="aae8e-187">**구성**을 클릭하여 새 플러그 인을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-187">Click **Configure** to configure the new plugin.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-samlssojira-tutorial/addon11.png)

14. <span data-ttu-id="aae8e-189">**SAML SingleSignOn 플러그 인 구성** 페이지에서 **추가 ID 공급자 추가** 단추를 클릭하여 ID 공급자의 설정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-189">On **SAML SingleSignOn Plugin Configuration** page, click **Add additional Identity Provider** button to configure the settings of Identity Provider.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-samlssojira-tutorial/addon4.png)

15. <span data-ttu-id="aae8e-191">이 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-191">Perform following steps on this page:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-samlssojira-tutorial/addon5.png)
 
    <span data-ttu-id="aae8e-193">a.</span><span class="sxs-lookup"><span data-stu-id="aae8e-193">a.</span></span> <span data-ttu-id="aae8e-194">ID 공급자의 **이름**(예: Azure AD)을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-194">Add **Name** of the Identity Provider (e.g Azure AD).</span></span>
    
    <span data-ttu-id="aae8e-195">b.</span><span class="sxs-lookup"><span data-stu-id="aae8e-195">b.</span></span> <span data-ttu-id="aae8e-196">ID 공급자의 **설명**(예: Azure AD)을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-196">Add **Description** of the Identity Provider (e.g Azure AD).</span></span>

    <span data-ttu-id="aae8e-197">c.</span><span class="sxs-lookup"><span data-stu-id="aae8e-197">c.</span></span> <span data-ttu-id="aae8e-198">**XML**을 클릭하고 Azure Portal에서 다운로드한 **메타데이터** 파일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-198">Click **XML** and select the **Metadata** file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="aae8e-199">d.</span><span class="sxs-lookup"><span data-stu-id="aae8e-199">d.</span></span> <span data-ttu-id="aae8e-200">**로드** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-200">Click **Load** button.</span></span>

    <span data-ttu-id="aae8e-201">e.</span><span class="sxs-lookup"><span data-stu-id="aae8e-201">e.</span></span> <span data-ttu-id="aae8e-202">IdP 메타데이터를 읽고 스크린샷에서 강조 표시된 대로 필드를 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-202">It reads the IdP metadata and populates the fields as highlighted in the screenshot.</span></span> 

16. <span data-ttu-id="aae8e-203">**설정 저장** 단추를 클릭하여 해당 설정을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-203">Click **Save settings** button to save the settings.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-samlssojira-tutorial/addon6.png)

> [!TIP]
> <span data-ttu-id="aae8e-205">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-205">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="aae8e-206">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-206">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="aae8e-207">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-207">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="aae8e-208">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="aae8e-208">Creating an Azure AD test user</span></span>
<span data-ttu-id="aae8e-209">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-209">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="aae8e-211">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="aae8e-211">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="aae8e-212">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-212">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="aae8e-214">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-214">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="aae8e-216">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-216">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="aae8e-218">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-218">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="aae8e-220">a.</span><span class="sxs-lookup"><span data-stu-id="aae8e-220">a.</span></span> <span data-ttu-id="aae8e-221">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-221">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="aae8e-222">b.</span><span class="sxs-lookup"><span data-stu-id="aae8e-222">b.</span></span> <span data-ttu-id="aae8e-223">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-223">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="aae8e-224">c.</span><span class="sxs-lookup"><span data-stu-id="aae8e-224">c.</span></span> <span data-ttu-id="aae8e-225">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-225">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="aae8e-226">d.</span><span class="sxs-lookup"><span data-stu-id="aae8e-226">d.</span></span> <span data-ttu-id="aae8e-227">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-227">Click **Create**.</span></span>
 
### <a name="creating-a-saml-sso-for-jira-by-resolution-gmbh-test-user"></a><span data-ttu-id="aae8e-228">SAML SSO for Jira by resolution GmbH 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="aae8e-228">Creating a SAML SSO for Jira by resolution GmbH test user</span></span>

<span data-ttu-id="aae8e-229">Azure AD 사용자가 SAML SSO for Jira by resolution GmbH에 로그인할 수 있게 하려면 해당 사용자를 SAML SSO for Jira by resolution GmbH에 프로비전해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-229">To enable Azure AD users to log in to SAML SSO for Jira by resolution GmbH, they must be provisioned into SAML SSO for Jira by resolution GmbH.</span></span>  
<span data-ttu-id="aae8e-230">SAML SSO for Jira by resolution GmbH에서 프로비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-230">In SAML SSO for Jira by resolution GmbH, provisioning is a manual task.</span></span>

<span data-ttu-id="aae8e-231">**사용자 계정을 프로비전하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="aae8e-231">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="aae8e-232">SAML SSO for Jira by resolution GmbH 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-232">Log in to your SAML SSO for Jira by resolution GmbH company site as an administrator.</span></span>

2. <span data-ttu-id="aae8e-233">마우스로 선 위를 가리키고 **사용자 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-233">Hover on cog and click the **User management**.</span></span>

    ![직원 추가](./media/active-directory-saas-samlssojira-tutorial/user1.png) 

3. <span data-ttu-id="aae8e-235">리디렉션된 [관리자 액세스] 페이지에서 **암호**를 입력하고 **확인** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-235">You are redirected to Administrator Access page to enter **Password** and click **Confirm** button.</span></span>

    ![직원 추가](./media/active-directory-saas-samlssojira-tutorial/user2.png) 

4. <span data-ttu-id="aae8e-237">**사용자 관리** 탭 섹션 아래에서  **사용자 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-237">Under **User management** tab section, click **create user**.</span></span>

    ![직원 추가](./media/active-directory-saas-samlssojira-tutorial/user3.png) 

5. <span data-ttu-id="aae8e-239">**“새 사용자 만들기”** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-239">On the **“Create new user”** dialog page, perform the following steps:</span></span>

    ![직원 추가](./media/active-directory-saas-samlssojira-tutorial/user4.png) 

    <span data-ttu-id="aae8e-241">a.</span><span class="sxs-lookup"><span data-stu-id="aae8e-241">a.</span></span> <span data-ttu-id="aae8e-242">**이메일 주소** 텍스트 상자에서 Brittasimon@contoso.com과 같은 사용자의 이메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-242">In the **Email address** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="aae8e-243">b.</span><span class="sxs-lookup"><span data-stu-id="aae8e-243">b.</span></span> <span data-ttu-id="aae8e-244">**전체 이름** 텍스트 상자에서 Britta Simon과 같은 사용자의 전체 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-244">In the **Full Name** textbox, type full name of the user like Britta Simon.</span></span>

    <span data-ttu-id="aae8e-245">c.</span><span class="sxs-lookup"><span data-stu-id="aae8e-245">c.</span></span> <span data-ttu-id="aae8e-246">**사용자 이름** 텍스트 상자에서 Brittasimon@contoso.com과 같은 사용자의 이메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-246">In the **Username** textbox, type the email of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="aae8e-247">d.</span><span class="sxs-lookup"><span data-stu-id="aae8e-247">d.</span></span> <span data-ttu-id="aae8e-248">**암호** 텍스트 상자에서 사용자에 대한 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-248">In the **Password** textbox, type the password of user.</span></span>

    <span data-ttu-id="aae8e-249">e.</span><span class="sxs-lookup"><span data-stu-id="aae8e-249">e.</span></span> <span data-ttu-id="aae8e-250">**사용자 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-250">Click **Create user**.</span></span>   

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="aae8e-251">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="aae8e-251">Assigning the Azure AD test user</span></span>

<span data-ttu-id="aae8e-252">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 SAML SSO for Jira by resolution GmbH에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-252">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SAML SSO for Jira by resolution GmbH.</span></span>

![사용자 할당][200] 

<span data-ttu-id="aae8e-254">**Britta Simon을 SAML SSO for Jira by resolution GmbH에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="aae8e-254">**To assign Britta Simon to SAML SSO for Jira by resolution GmbH, perform the following steps:**</span></span>

1. <span data-ttu-id="aae8e-255">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-255">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="aae8e-257">응용 프로그램 목록에서 **SAML SSO for Jira by resolution GmbH**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-257">In the applications list, select **SAML SSO for Jira by resolution GmbH**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_app.png) 

3. <span data-ttu-id="aae8e-259">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-259">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="aae8e-261">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-261">Click **Add** button.</span></span> <span data-ttu-id="aae8e-262">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-262">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="aae8e-264">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-264">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="aae8e-265">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-265">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="aae8e-266">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-266">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="aae8e-267">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="aae8e-267">Testing single sign-on</span></span>

<span data-ttu-id="aae8e-268">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-268">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="aae8e-269">[액세스 패널]에서 [SAML SSO for Jira by resolution GmbH] 타일을 클릭하면 SAML SSO for Jira by resolution GmbH 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="aae8e-269">When you click the SAML SSO for Jira by resolution GmbH tile in the Access Panel, you should get automatically signed-on to your SAML SSO for Jira by resolution GmbH application.</span></span>
<span data-ttu-id="aae8e-270">액세스 패널에 대한 자세한 내용은 [Azure 시작](active-directory-saas-access-panel-introduction.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="aae8e-270">For more information about the Access Panel, see [introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="aae8e-271">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="aae8e-271">Additional resources</span></span>

* [<span data-ttu-id="aae8e-272">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="aae8e-272">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="aae8e-273">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="aae8e-273">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_203.png

