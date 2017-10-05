---
title: "자습서: Pingboard와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 Pingboard 간에 Single Sign-On을 구성하는 방법을 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 008c670a8043da0c67ccefde48d5ef721c75d97c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pingboard"></a><span data-ttu-id="34985-103">자습서: Pingboard와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="34985-103">Tutorial: Azure Active Directory integration with Pingboard</span></span>

<span data-ttu-id="34985-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Pingboard를 통합하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="34985-104">In this tutorial, you learn how to integrate Pingboard with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="34985-105">Pingboard를 Azure AD와 통합하면 다음과 같은 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34985-105">Integrating Pingboard with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="34985-106">Azure AD에서 Pingboard에 대한 액세스 권한이 있는 사용자를 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34985-106">You can control in Azure AD who has access to Pingboard</span></span>
- <span data-ttu-id="34985-107">사용자가 해당 Azure AD 계정으로 Pingboard에 자동으로 SSO(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34985-107">You can enable your users to automatically get signed-on to Pingboard (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="34985-108">단일 중앙 위치인 Azure 관리 포털에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34985-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="34985-109">Azure AD와의 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory를 사용한 응용 프로그램 액세스 및 Single Sign-On](active-directory-appssoaccess-whatis.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="34985-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="34985-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="34985-110">Prerequisites</span></span>

<span data-ttu-id="34985-111">Pingboard와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="34985-111">To configure Azure AD integration with Pingboard, you need the following items:</span></span>

- <span data-ttu-id="34985-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="34985-112">An Azure AD subscription</span></span>
- <span data-ttu-id="34985-113">Pingboard Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="34985-113">A Pingboard single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="34985-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="34985-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="34985-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="34985-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="34985-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="34985-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="34985-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34985-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="34985-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="34985-118">Scenario description</span></span>
<span data-ttu-id="34985-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="34985-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="34985-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34985-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="34985-121">갤러리에서 Pingboard 추가</span><span class="sxs-lookup"><span data-stu-id="34985-121">Adding Pingboard from the gallery</span></span>
2. <span data-ttu-id="34985-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="34985-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pingboard-from-the-gallery"></a><span data-ttu-id="34985-123">갤러리에서 Pingboard 추가</span><span class="sxs-lookup"><span data-stu-id="34985-123">Adding Pingboard from the gallery</span></span>
<span data-ttu-id="34985-124">Pingboard와 Azure AD의 통합을 구성하려면 갤러리의 Pingboard를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="34985-124">To configure the integration of Pingboard into Azure AD, you need to add Pingboard from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="34985-125">**갤러리에서 Pingboard를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="34985-125">**To add Pingboard from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="34985-126">**[Azure 관리 포털](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="34985-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="34985-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="34985-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="34985-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="34985-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="34985-131">대화 상자 위쪽에 있는 **추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="34985-131">Click **Add** button on the top of the dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="34985-133">검색 상자에 **Pingboard**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="34985-133">In the search box, type **Pingboard**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_search.png)

5. <span data-ttu-id="34985-135">결과 창에서 **Pingboard**를 선택하고 **추가** 단추를 클릭하여 해당 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="34985-135">In the results panel, select **Pingboard**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="34985-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="34985-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="34985-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Pingboard에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="34985-138">In this section, you configure and test Azure AD single sign-on with Pingboard based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="34985-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Pingboard 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="34985-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Pingboard is to a user in Azure AD.</span></span> <span data-ttu-id="34985-140">즉, Azure AD 사용자와 Pingboard의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="34985-140">In other words, a link relationship between an Azure AD user and the related user in Pingboard needs to be established.</span></span>

<span data-ttu-id="34985-141">이 연결 관계는 Azure AD의 **사용자 이름** 값을 Pingboard의 **Username** 값으로 할당하여 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="34985-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Pingboard.</span></span>

<span data-ttu-id="34985-142">Pingboard에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="34985-142">To configure and test Azure AD single sign-on with Pingboard, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="34985-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="34985-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="34985-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="34985-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="34985-145">**[Pingboard 테스트 사용자 만들기](#creating-a-pingboard-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 Pingboard에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="34985-145">**[Creating a Pingboard test user](#creating-a-pingboard-test-user)** - to have a counterpart of Britta Simon in Pingboard that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="34985-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="34985-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="34985-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="34985-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="34985-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="34985-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="34985-149">이 섹션에서는 Azure 관리 포털에서 Azure AD Single Sign-On을 사용하도록 설정하고 Pingboard 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="34985-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Pingboard application.</span></span>

<span data-ttu-id="34985-150">**Pingboard에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="34985-150">**To configure Azure AD single sign-on with Pingboard, perform the following steps:**</span></span>

1. <span data-ttu-id="34985-151">Azure 관리 포털의 **Pingboard** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="34985-151">In the Azure Management portal, on the **Pingboard** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-On 구성][4]

2. <span data-ttu-id="34985-153">**Single sign on** 대화 상자에서 **모드**로 **SAML 기반 로그온**을 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="34985-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_samlbase.png)

3. <span data-ttu-id="34985-155">**Pingboard 도메인 및 URL** 섹션에서 **IDP 시작 모드**로 응용 프로그램을 구성하려는 경우 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="34985-155">On the **Pingboard Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_url.png)

    <span data-ttu-id="34985-157">a.</span><span class="sxs-lookup"><span data-stu-id="34985-157">a.</span></span> <span data-ttu-id="34985-158">**식별자** 텍스트 상자에 해당 값으로 `http://<entity-id>.pingboard.com/sp`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="34985-158">In the **Identifier** textbox, type the value as: `http://<entity-id>.pingboard.com/sp`</span></span>

    <span data-ttu-id="34985-159">b.</span><span class="sxs-lookup"><span data-stu-id="34985-159">b.</span></span> <span data-ttu-id="34985-160">**회신 URL** 텍스트 상자에 다음 패턴으로 URL을 입력합니다.`https://<entity-id>.pingboard.com/auth/saml/consume`</span><span class="sxs-lookup"><span data-stu-id="34985-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<entity-id>.pingboard.com/auth/saml/consume`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="34985-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="34985-161">Please note that these are not the real values.</span></span> <span data-ttu-id="34985-162">실제 식별자 및 회신 URL로 해당 값을 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="34985-162">You have to update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="34985-163">식별자에는 고유한 문자열 값을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="34985-163">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="34985-164">이러한 값을 얻으려면 [Pingboard 클라이언트 지원 팀](https://support.pingboard.com/)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="34985-164">Contact [Pingboard Client support team](https://support.pingboard.com/) to get these values.</span></span> 

4. <span data-ttu-id="34985-165">**SP** 시작 모드에서 응용 프로그램을 구성하려면 **고급 URL 설정 표시**를 선택하세요.</span><span class="sxs-lookup"><span data-stu-id="34985-165">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_sp_initiated01.png)

    <span data-ttu-id="34985-167">a.</span><span class="sxs-lookup"><span data-stu-id="34985-167">a.</span></span> <span data-ttu-id="34985-168">**로그인 URL** 텍스트 상자에서 값으로 `http://<sub-domain>.pingboard.com/sign_in`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="34985-168">In the **Sign-on URL** textbox, type the value as: `http://<sub-domain>.pingboard.com/sign_in`</span></span>
     
5. <span data-ttu-id="34985-169">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 XML 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="34985-169">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_certificate.png) 

6. <span data-ttu-id="34985-171">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="34985-171">Click **Save** button.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-pingboard-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="34985-173">Pingboard 쪽에서 SSO를 구성하려면 새 브라우저 창을 열고 Pingboard 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="34985-173">To configure SSO on Pingboard side, open a new browser window and log in to your Pingboard Account.</span></span> <span data-ttu-id="34985-174">Single Sign-On을 설정하려면 Pingboard 관리자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="34985-174">You must be a Pingboard admin to set up single sign on.</span></span>

8. <span data-ttu-id="34985-175">상단 메뉴에서 **앱 > 통합**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="34985-175">From the top menu select **Apps > Integrations**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-pingboard-tutorial/Pingboard_integration.png)

9.  <span data-ttu-id="34985-177">**통합** 페이지에서 **"Azure Active Directory"** 타일을 찾아 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="34985-177">On the **Integrations** page, find the **"Azure Active Directory"** tile, and click it.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-pingboard-tutorial/Pingboard_aad.png)

10. <span data-ttu-id="34985-179">다음에 나오는 모달에서 **"구성"**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="34985-179">In the modal that follows click **"Configure"**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-pingboard-tutorial/Pingboard_configure.png)

11. <span data-ttu-id="34985-181">다음 페이지에서 "Azure SSO 통합을 사용합니다."라는 메시지를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34985-181">On the following page, you will notice that "Azure SSO Integration is enabled.".</span></span> <span data-ttu-id="34985-182">다운로드한 메타데이터 XML 파일을 메모장에서 열고 **IDP 메타데이터**에 콘텐츠를 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="34985-182">Open the downloaded Metadata XML file in a notepad and paste the content in **IDP Metadata**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-pingboard-tutorial/Pingboard_sso_configure.png)

12. <span data-ttu-id="34985-184">파일 유효성을 검사하여 모든 것이 올바르면 지금부터 Single Sign-on이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="34985-184">The file will be validated, and if everything is correct, single sign on will now be enabled</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="34985-185">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="34985-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="34985-186">이 섹션의 목적은 Azure 관리 포털에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="34985-186">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="34985-188">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="34985-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="34985-189">**Azure 관리 포털**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="34985-189">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-pingboard-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="34985-191">**사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭하여 사용자 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="34985-191">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-pingboard-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="34985-193">대화 상자 위쪽에서 **추가**를 클릭하여 **사용자** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="34985-193">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-pingboard-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="34985-195">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="34985-195">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-pingboard-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="34985-197">a.</span><span class="sxs-lookup"><span data-stu-id="34985-197">a.</span></span> <span data-ttu-id="34985-198">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="34985-198">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="34985-199">b.</span><span class="sxs-lookup"><span data-stu-id="34985-199">b.</span></span> <span data-ttu-id="34985-200">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="34985-200">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="34985-201">c.</span><span class="sxs-lookup"><span data-stu-id="34985-201">c.</span></span> <span data-ttu-id="34985-202">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="34985-202">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="34985-203">d.</span><span class="sxs-lookup"><span data-stu-id="34985-203">d.</span></span> <span data-ttu-id="34985-204">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="34985-204">Click **Create**.</span></span>
 
### <a name="creating-a-pingboard-test-user"></a><span data-ttu-id="34985-205">Pingboard 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="34985-205">Creating a Pingboard test user</span></span>

<span data-ttu-id="34985-206">Azure AD 사용자가 Pingboard에 로그인할 수 있도록 하려면 Pingboard로 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="34985-206">In order to enable Azure AD users to log into Pingboard, they must be provisioned into Pingboard.</span></span>  
<span data-ttu-id="34985-207">Pingboard의 경우 프로비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="34985-207">In the case of Pingboard, provisioning is a manual task.</span></span>

<span data-ttu-id="34985-208">**사용자 계정을 프로비전하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="34985-208">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="34985-209">Pingboard 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="34985-209">Log in to your Pingboard company site as an administrator.</span></span>

2. <span data-ttu-id="34985-210">**디렉터리** 페이지에서 **"직원 추가"** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="34985-210">Click **“Add Employee”** button on **Directory** page.</span></span>

    ![직원 추가](./media/active-directory-saas-pingboard-tutorial/create_testuser_add.png)

3. <span data-ttu-id="34985-212">**“직원 추가”** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="34985-212">On the **“Add Employee”** dialog page, perform the following steps.</span></span>

    ![피플 초대](./media/active-directory-saas-pingboard-tutorial/create_testuser_name.png)

    <span data-ttu-id="34985-214">a.</span><span class="sxs-lookup"><span data-stu-id="34985-214">a.</span></span> <span data-ttu-id="34985-215">**전체 이름** 텍스트 상자에 전체 이름인 Britta Simon을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="34985-215">In the **Full Name** textbox, type the full name of Britta Simon.</span></span>

    <span data-ttu-id="34985-216">b.</span><span class="sxs-lookup"><span data-stu-id="34985-216">b.</span></span> <span data-ttu-id="34985-217">**전자 메일** 텍스트 상자에 Britta Simon 계정의 전자 메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="34985-217">In the **Email** textbox, type the email address of Britta Simon account.</span></span>

    <span data-ttu-id="34985-218">c.</span><span class="sxs-lookup"><span data-stu-id="34985-218">c.</span></span> <span data-ttu-id="34985-219">**직함** 텍스트 상자에 Britta Simon의 직함을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="34985-219">In the **Job Title** textbox, type the job title of Britta Simon.</span></span>

    <span data-ttu-id="34985-220">d.</span><span class="sxs-lookup"><span data-stu-id="34985-220">d.</span></span> <span data-ttu-id="34985-221">**위치** 드롭다운에서 Britta Simon의 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="34985-221">In the **Location** dropdown, select the location  of Britta Simon.</span></span>
    
    <span data-ttu-id="34985-222">e.</span><span class="sxs-lookup"><span data-stu-id="34985-222">e.</span></span> <span data-ttu-id="34985-223">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="34985-223">Click **Add**.</span></span>   

4. <span data-ttu-id="34985-224">사용자 추가를 확인하는 확인 화면이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="34985-224">A confirmation screen will come up to confirm the addition of user.</span></span>
    
    ![확인](./media/active-directory-saas-pingboard-tutorial/create_testuser_confirm.png)
        
    > [!NOTE]
    > <span data-ttu-id="34985-226">Azure Active Directory 계정 보유자는 활성화되기 전에 전자 메일을 받고 링크를 따라 계정을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="34985-226">The Azure Active Directory account holder will receive an email and follow a link to confirm their account before it becomes active.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="34985-227">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="34985-227">Assigning the Azure AD test user</span></span>

<span data-ttu-id="34985-228">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Pingboard에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="34985-228">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Pingboard.</span></span>

![사용자 할당][200] 

<span data-ttu-id="34985-230">**Britta Simon을 Pingboard에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="34985-230">**To assign Britta Simon to Pingboard, perform the following steps:**</span></span>

1. <span data-ttu-id="34985-231">Azure 관리 포털에서 응용 프로그램 보기를 열고 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="34985-231">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="34985-233">응용 프로그램 목록에서 **Pingboard**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="34985-233">In the applications list, select **Pingboard**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_app.png) 

3. <span data-ttu-id="34985-235">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="34985-235">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="34985-237">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="34985-237">Click **Add** button.</span></span> <span data-ttu-id="34985-238">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="34985-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="34985-240">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="34985-240">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="34985-241">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="34985-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="34985-242">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="34985-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="34985-243">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="34985-243">Testing single sign-on</span></span>

<span data-ttu-id="34985-244">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="34985-244">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="34985-245">액세스 패널에서 Pingboard 타일을 클릭하면 Pingboard 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="34985-245">When you click the Pingboard tile in the Access Panel, you should get automatically signed-on to your Pingboard application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="34985-246">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="34985-246">Additional resources</span></span>

* [<span data-ttu-id="34985-247">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="34985-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="34985-248">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="34985-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_203.png
