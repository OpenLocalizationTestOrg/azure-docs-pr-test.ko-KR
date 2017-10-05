---
title: "자습서: Lucidchart와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory 및 Lucidchart 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1068d364-11f3-43b5-bd6d-26f00ecd5baa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: 2dea669f03c893632c08d30feeb3173efc2d8243
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lucidchart"></a><span data-ttu-id="e4994-103">자습서: Lucidchart와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="e4994-103">Tutorial: Azure Active Directory integration with Lucidchart</span></span>

<span data-ttu-id="e4994-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Lucidchart를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e4994-104">In this tutorial, you learn how to integrate Lucidchart with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e4994-105">Lucidchart를 Azure AD와 통합하면 다음과 같은 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4994-105">Integrating Lucidchart with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e4994-106">Lucidchart에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4994-106">You can control in Azure AD who has access to Lucidchart</span></span>
- <span data-ttu-id="e4994-107">사용자가 해당 Azure AD 계정으로 Lucidchart에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4994-107">You can enable your users to automatically get signed-on to Lucidchart (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e4994-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4994-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e4994-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e4994-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e4994-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="e4994-110">Prerequisites</span></span>

<span data-ttu-id="e4994-111">Lucidchart와 Azure AD의 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e4994-111">To configure Azure AD integration with Lucidchart, you need the following items:</span></span>

- <span data-ttu-id="e4994-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="e4994-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e4994-113">Lucidchart Single Sign-on이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="e4994-113">A Lucidchart single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e4994-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e4994-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e4994-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4994-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e4994-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="e4994-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e4994-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4994-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e4994-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="e4994-118">Scenario description</span></span>
<span data-ttu-id="e4994-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4994-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e4994-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4994-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e4994-121">갤러리에서 Lucidchart 추가</span><span class="sxs-lookup"><span data-stu-id="e4994-121">Adding Lucidchart from the gallery</span></span>
2. <span data-ttu-id="e4994-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="e4994-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lucidchart-from-the-gallery"></a><span data-ttu-id="e4994-123">갤러리에서 Lucidchart 추가</span><span class="sxs-lookup"><span data-stu-id="e4994-123">Adding Lucidchart from the gallery</span></span>
<span data-ttu-id="e4994-124">Lucidchart의 Azure AD 통합을 구성하려면 갤러리의 Lucidchart를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4994-124">To configure the integration of Lucidchart into Azure AD, you need to add Lucidchart from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e4994-125">**갤러리에서 Lucidchart를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="e4994-125">**To add Lucidchart from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e4994-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4994-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e4994-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e4994-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e4994-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e4994-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="e4994-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4994-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="e4994-133">검색 상자에 **Lucidchart**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e4994-133">In the search box, type **Lucidchart**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_search.png)

5. <span data-ttu-id="e4994-135">결과 패널에서 **Lucidchart**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e4994-135">In the results panel, select **Lucidchart**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e4994-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="e4994-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e4994-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Lucidchart에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="e4994-138">In this section, you configure and test Azure AD single sign-on with Lucidchart based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e4994-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Lucidchart 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4994-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Lucidchart is to a user in Azure AD.</span></span> <span data-ttu-id="e4994-140">즉, Azure AD 사용자와 Lucidchart의 관련 사용자 간에 연결 관계가 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4994-140">In other words, a link relationship between an Azure AD user and the related user in Lucidchart needs to be established.</span></span>

<span data-ttu-id="e4994-141">Lucidchart에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 연결 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e4994-141">In Lucidchart, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e4994-142">Lucidchart에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4994-142">To configure and test Azure AD single sign-on with Lucidchart, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e4994-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4994-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e4994-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e4994-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e4994-145">**[Lucidchart 테스트 사용자 만들기](#creating-a-lucidchart-test-user)** - Britta Simon의 Azure AD 표현과 연결되는 대응 사용자를 Lucidchart에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e4994-145">**[Creating a Lucidchart test user](#creating-a-lucidchart-test-user)** - to have a counterpart of Britta Simon in Lucidchart that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e4994-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4994-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e4994-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e4994-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e4994-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="e4994-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e4994-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Lucidchart 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="e4994-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Lucidchart application.</span></span>

<span data-ttu-id="e4994-150">**Lucidchart에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="e4994-150">**To configure Azure AD single sign-on with Lucidchart, perform the following steps:**</span></span>

1. <span data-ttu-id="e4994-151">Azure Portal의 **Lucidchart** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4994-151">In the Azure portal, on the **Lucidchart** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="e4994-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e4994-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_samlbase.png)

3. <span data-ttu-id="e4994-155">**Lucidchart 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e4994-155">On the **Lucidchart Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_url.png)

    <span data-ttu-id="e4994-157">**로그온 URL** 텍스트 상자에 URL을 입력합니다. `https://chart2.office.lucidchart.com/saml/sso/azure`</span><span class="sxs-lookup"><span data-stu-id="e4994-157">In the **Sign-on URL** textbox, type a URL as: `https://chart2.office.lucidchart.com/saml/sso/azure`</span></span>

4. <span data-ttu-id="e4994-158">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 메타데이터 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="e4994-158">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_certificate.png) 

5. <span data-ttu-id="e4994-160">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4994-160">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-lucidchart-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e4994-162">다른 웹 브라우저 창에서 Lucidchart 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="e4994-162">In a different web browser window, log into your Lucidchart company site as an administrator.</span></span>

7. <span data-ttu-id="e4994-163">위쪽의 메뉴에서 **팀**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4994-163">In the menu on the top, click **Team**.</span></span>
   
    <span data-ttu-id="e4994-164">![팀](./media/active-directory-saas-lucidchart-tutorial/ic791190.png "팀")</span><span class="sxs-lookup"><span data-stu-id="e4994-164">![Team](./media/active-directory-saas-lucidchart-tutorial/ic791190.png "Team")</span></span>

8. <span data-ttu-id="e4994-165">**응용 프로그램 \> SAML 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4994-165">Click **Applications \> Manage SAML**.</span></span>
   
    <span data-ttu-id="e4994-166">![SAML 관리](./media/active-directory-saas-lucidchart-tutorial/ic791191.png "SAML 관리")</span><span class="sxs-lookup"><span data-stu-id="e4994-166">![Manage SAML](./media/active-directory-saas-lucidchart-tutorial/ic791191.png "Manage SAML")</span></span>

9. <span data-ttu-id="e4994-167">**SAML 인증 설정** 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e4994-167">On the **SAML Authentication Settings** dialog page, perform the following steps:</span></span>
   
    <span data-ttu-id="e4994-168">a.</span><span class="sxs-lookup"><span data-stu-id="e4994-168">a.</span></span> <span data-ttu-id="e4994-169">**SAML 인증 사용**을 선택한 다음 **옵션**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4994-169">Select **Enable SAML Authentication**, and then click **Optional**.</span></span>

    <span data-ttu-id="e4994-170">![SAML 인증 설정](./media/active-directory-saas-lucidchart-tutorial/ic791192.png "SAML 인증 설정")</span><span class="sxs-lookup"><span data-stu-id="e4994-170">![SAML Authentication Settings](./media/active-directory-saas-lucidchart-tutorial/ic791192.png "SAML Authentication Settings")</span></span>
 
    <span data-ttu-id="e4994-171">b.</span><span class="sxs-lookup"><span data-stu-id="e4994-171">b.</span></span> <span data-ttu-id="e4994-172">**도메인** 텍스트 상자에서 도메인을 입력한 다음 **인증서 변경**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4994-172">In the **Domain** textbox, type your domain, and then click **Change Certificate**.</span></span>

    <span data-ttu-id="e4994-173">![인증서 변경](./media/active-directory-saas-lucidchart-tutorial/ic791193.png "인증서 변경")</span><span class="sxs-lookup"><span data-stu-id="e4994-173">![Change Certificate](./media/active-directory-saas-lucidchart-tutorial/ic791193.png "Change Certificate")</span></span>
 
    <span data-ttu-id="e4994-174">c.</span><span class="sxs-lookup"><span data-stu-id="e4994-174">c.</span></span> <span data-ttu-id="e4994-175">다운로드한 메타데이터 파일을 열고 내용을 복사한 다음 **메타데이터 업로드** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="e4994-175">Open your downloaded metadata file, copy the content, and then paste it into the **Upload Metadata** textbox.</span></span>

    <span data-ttu-id="e4994-176">![메타데이터 업로드](./media/active-directory-saas-lucidchart-tutorial/ic791194.png "메타데이터 업로드")</span><span class="sxs-lookup"><span data-stu-id="e4994-176">![Upload Metadata](./media/active-directory-saas-lucidchart-tutorial/ic791194.png "Upload Metadata")</span></span>
 
    <span data-ttu-id="e4994-177">d.</span><span class="sxs-lookup"><span data-stu-id="e4994-177">d.</span></span> <span data-ttu-id="e4994-178">**신규 사용자를 자동으로 팀에 추가**를 선택한 다음 **변경 내용 저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4994-178">Select **Automatically Add new users to the team**, and then click **Save changes**.</span></span>

    <span data-ttu-id="e4994-179">![변경 내용 저장](./media/active-directory-saas-lucidchart-tutorial/ic791195.png "변경 내용 저장")</span><span class="sxs-lookup"><span data-stu-id="e4994-179">![Save Changes](./media/active-directory-saas-lucidchart-tutorial/ic791195.png "Save Changes")</span></span>

> [!TIP]
> <span data-ttu-id="e4994-180">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4994-180">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e4994-181">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4994-181">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e4994-182">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4994-182">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e4994-183">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="e4994-183">Creating an Azure AD test user</span></span>
<span data-ttu-id="e4994-184">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e4994-184">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="e4994-186">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="e4994-186">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e4994-187">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4994-187">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e4994-189">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4994-189">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e4994-191">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4994-191">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e4994-193">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e4994-193">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e4994-195">a.</span><span class="sxs-lookup"><span data-stu-id="e4994-195">a.</span></span> <span data-ttu-id="e4994-196">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e4994-196">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e4994-197">b.</span><span class="sxs-lookup"><span data-stu-id="e4994-197">b.</span></span> <span data-ttu-id="e4994-198">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e4994-198">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e4994-199">c.</span><span class="sxs-lookup"><span data-stu-id="e4994-199">c.</span></span> <span data-ttu-id="e4994-200">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="e4994-200">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e4994-201">d.</span><span class="sxs-lookup"><span data-stu-id="e4994-201">d.</span></span> <span data-ttu-id="e4994-202">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4994-202">Click **Create**.</span></span>
 
### <a name="creating-a-lucidchart-test-user"></a><span data-ttu-id="e4994-203">Lucidchart 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="e4994-203">Creating a Lucidchart test user</span></span>

<span data-ttu-id="e4994-204">Lucidchart를 프로비전하는 사용자를 구성할 작업 항목이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e4994-204">There is no action item for you to configure user provisioning to Lucidchart.</span></span>  <span data-ttu-id="e4994-205">할당된 사용자가 액세스 패널을 사용하여 Lucidchart에 로그인하려는 경우 Lucidchart는 사용자가 존재하는지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e4994-205">When an assigned user tries to log into Lucidchart using the access panel, Lucidchart checks whether the user exists.</span></span>  

<span data-ttu-id="e4994-206">사용할 수 있는 사용자 계정이 없으면 자동으로 Lucidchart에 의해 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4994-206">If there is no user account available yet, it is automatically created by Lucidchart.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e4994-207">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="e4994-207">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e4994-208">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Lucidchart에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="e4994-208">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Lucidchart.</span></span>

![사용자 할당][200] 

<span data-ttu-id="e4994-210">**Britta Simon을 Lucidchart에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="e4994-210">**To assign Britta Simon to Lucidchart, perform the following steps:**</span></span>

1. <span data-ttu-id="e4994-211">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4994-211">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="e4994-213">응용 프로그램 목록에서 **Lucidchart**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e4994-213">In the applications list, select **Lucidchart**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_app.png) 

3. <span data-ttu-id="e4994-215">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4994-215">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="e4994-217">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4994-217">Click **Add** button.</span></span> <span data-ttu-id="e4994-218">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e4994-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="e4994-220">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e4994-220">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e4994-221">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4994-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e4994-222">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4994-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e4994-223">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="e4994-223">Testing single sign-on</span></span>

<span data-ttu-id="e4994-224">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="e4994-224">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e4994-225">액세스 패널에서 Lucidchart 타일을 클릭하면 Lucidchart 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4994-225">When you click the Lucidchart tile in the Access Panel, you should get automatically signed-on to your Lucidchart application.</span></span>
<span data-ttu-id="e4994-226">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e4994-226">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e4994-227">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="e4994-227">Additional resources</span></span>

* [<span data-ttu-id="e4994-228">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="e4994-228">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e4994-229">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="e4994-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_203.png

