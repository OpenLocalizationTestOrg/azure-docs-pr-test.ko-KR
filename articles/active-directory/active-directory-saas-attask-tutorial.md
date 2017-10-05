---
title: "자습서: Azure Active Directory와 통합 @Task| Microsoft Docs"
description: "Azure Active Directory와 @Task 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: aab8bd2f-f9dd-42da-a18e-d707865687d7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: ebb19ca6cbaf04106fbce937d95651e709854cfd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-task"></a><span data-ttu-id="60b7c-103">자습서: @Task와(과) Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="60b7c-103">Tutorial: Azure Active Directory integration with @Task</span></span>
<span data-ttu-id="60b7c-104">이 자습서에서는 @Task와(과) Azure AD(Azure Active Directory)를 통합하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-104">The objective of this tutorial is to show you how to integrate @Task with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="60b7c-105">@Task을(를) Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-105">Integrating @Task with Azure AD provides you with the following benefits:</span></span> 

* <span data-ttu-id="60b7c-106">@Task에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-106">You can control in Azure AD who has access to @Task</span></span>
* <span data-ttu-id="60b7c-107">사용자가 해당 Azure AD 계정으로 @Task에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-107">You can enable your users to automatically get signed-on to @Task (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="60b7c-108">단일 중앙 위치인 Azure 클래식 포털에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-108">You can manage your accounts in one central location - the Azure classic Portal</span></span>

<span data-ttu-id="60b7c-109">Azure AD와의 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory를 사용한 응용 프로그램 액세스 및 Single Sign-On](active-directory-appssoaccess-whatis.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60b7c-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="60b7c-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="60b7c-110">Prerequisites</span></span>
<span data-ttu-id="60b7c-111">Azure AD와의 통합을 구성 하려면 @Task, 다음 항목이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-111">To configure Azure AD integration with @Task, you need the following items:</span></span>

* <span data-ttu-id="60b7c-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="60b7c-112">An Azure AD subscription</span></span>
* <span data-ttu-id="60b7c-113">@Task Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="60b7c-113">An @Task single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="60b7c-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="60b7c-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="60b7c-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="60b7c-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="60b7c-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="60b7c-118">Scenario Description</span></span>
<span data-ttu-id="60b7c-119">이 자습서는 테스트 환경에서 Azure AD Single Sign-on을 테스트하는 데 도움을 주기 위해 제공되었습니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="60b7c-120">이 자습서에 설명된 시나리오는 다음 세 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-120">The scenario outlined in this tutorial consists of three main building blocks:</span></span>

1. <span data-ttu-id="60b7c-121">갤러리에서 @Task 추가</span><span class="sxs-lookup"><span data-stu-id="60b7c-121">Adding @Task from the gallery</span></span> 
2. <span data-ttu-id="60b7c-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="60b7c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-task-from-the-gallery"></a><span data-ttu-id="60b7c-123">갤러리에서 @Task 추가</span><span class="sxs-lookup"><span data-stu-id="60b7c-123">Adding @Task from the gallery</span></span>
<span data-ttu-id="60b7c-124">@Task의 Azure AD 통합을 구성하려면 갤러리의 @Task을(를) 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-124">To configure the integration of @Task into Azure AD, you need to add @Task from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="60b7c-125">**갤러리에서 @Task을(를) 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="60b7c-125">**To add @Task from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="60b7c-126">**Azure 클래식 포털**의 왼쪽 탐색 창에서 **Active Directory**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1] 
2. <span data-ttu-id="60b7c-128">**디렉터리** 목록에서 디렉터리 통합을 사용하도록 설정할 디렉터리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="60b7c-129">응용 프로그램 보기를 열려면 디렉터리 보기의 최상위 메뉴에서 **응용 프로그램** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![응용 프로그램][2] 
4. <span data-ttu-id="60b7c-131">페이지 맨 아래에 있는 **추가** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-131">Click **Add** at the bottom of the page.</span></span>
   
    ![응용 프로그램][3] 
5. <span data-ttu-id="60b7c-133">**수행할 작업** 대화 상자에서 **갤러리에서 응용 프로그램 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![응용 프로그램][4] 
6. <span data-ttu-id="60b7c-135">검색 상자에서 **@Task**을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60b7c-135">In the search box, type **@Task**.</span></span>
   
    ![응용 프로그램][5] 
7. <span data-ttu-id="60b7c-137">결과 창에서 **@Task**을(를) 선택하고 **완료**를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-137">In the results pane, select **@Task**, and then click **Complete** to add the application.</span></span>
   
    ![응용 프로그램][30] 

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="60b7c-139">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="60b7c-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="60b7c-140">이 섹션은 "Britta Simon"이라는 테스트 사용자를 기반으로 @Task(으)로 Azure AD Single Sign-On을 구성하고 테스트하는 방법을 보여주기 위해 작성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with @Task based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="60b7c-141">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 @Task 사용자가 누군지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-141">For single sign-on to work, Azure AD needs to know what the counterpart user in @Task to an user in Azure AD is.</span></span> <span data-ttu-id="60b7c-142">즉, Azure AD 사용자와 @Task의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-142">In other words, a link relationship between an Azure AD user and the related user in @Task needs to be established.</span></span>   
<span data-ttu-id="60b7c-143">이 연결 관계는 Azure AD의 **사용자 이름** 값을 @Task의 **Username** 값으로 할당하여 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in @Task.</span></span>

<span data-ttu-id="60b7c-144">구성 하 여 Azure AD single sign-on 테스트와 @Task, 다음과 같은 문서 블록을 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-144">To configure and test Azure AD single sign-on with @Task, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="60b7c-145">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="60b7c-146">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="60b7c-147">**[@Tasktest 사용자 만들기](#creating-a-halogen-software-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 @Taskthat에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-147">**[Creating a @Tasktest user](#creating-a-halogen-software-test-user)** - to have a counterpart of Britta Simon in @Taskthat is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="60b7c-148">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="60b7c-149">**[Single Sign-On 테스트](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="60b7c-150">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="60b7c-150">Configuring Azure AD Single Sign-On</span></span>
<span data-ttu-id="60b7c-151">이 섹션은 Azure 클래식 포털에서 Azure AD Single Sign-On을 사용하도록 설정하고 @Task 응용 프로그램에서 Single Sign-On을 구성하는 방법을 설명하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-151">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your @Task application.</span></span>

<span data-ttu-id="60b7c-152">**Azure AD single sign on를 구성 하려면 @Task, 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="60b7c-152">**To configure Azure AD single sign-on with @Task, perform the following steps:**</span></span>

1. <span data-ttu-id="60b7c-153">Azure 클래식 포털의 **@Task** 응용 프로그램 통합 페이지에서 **Single Sign-on 구성**을 클릭하여 **Single Sign-on 구성** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-153">In the Azure classic portal, on the **@Task** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Single Sign-on 구성][6] 
2. <span data-ttu-id="60b7c-155">**@Task에 대한 사용자 로그온 방법 선택** 페이지에서 **Azure AD Single Sign-On**을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-155">On the **How would you like users to sign on to @Task** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][7] 
3. <span data-ttu-id="60b7c-157">**앱 설정 구성** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![앱 설정 구성][8] 
   
     <span data-ttu-id="60b7c-159">a.</span><span class="sxs-lookup"><span data-stu-id="60b7c-159">a.</span></span> <span data-ttu-id="60b7c-160">**로그온 URL** 텍스트 상자에 사용자가 @Task 응용 프로그램에 로그인하는 데 사용하는 URL을 입력합니다(예: *https://<Tenant name>.attask-ondemand.com*).</span><span class="sxs-lookup"><span data-stu-id="60b7c-160">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your @Task application (e.g.:*https://<Tenant name>.attask-ondemand.com*).</span></span>
   
     <span data-ttu-id="60b7c-161">b.</span><span class="sxs-lookup"><span data-stu-id="60b7c-161">b.</span></span> <span data-ttu-id="60b7c-162">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-162">Click **Next**.</span></span>
4. <span data-ttu-id="60b7c-163">**@Task에서 Single Sign-On 구성** 페이지에서 **메타데이터 다운로드**를 클릭한 다음 컴퓨터에 로컬로 메타데이터 파일을 저장한 다음 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-163">On the **Configure single sign-on at @Task** page, click **Download metadata**, save the metadata file locally on your computer, and then click **Next**.</span></span>
   
    ![Azure AD Connect의 정의][9] 
5. <span data-ttu-id="60b7c-165">@Task 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-165">Sign-on to your @Task company site as administrator.</span></span>
6. <span data-ttu-id="60b7c-166">**Single Sign On 구성**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-166">Go to **Single Sign On Configuration**.</span></span>
7. <span data-ttu-id="60b7c-167">**Single Sign-On** 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-167">On the **Single Sign-On** dialog, perform the following steps</span></span>
   
    ![Single Sign-On 구성][23]
   
    <span data-ttu-id="60b7c-169">a.</span><span class="sxs-lookup"><span data-stu-id="60b7c-169">a.</span></span> <span data-ttu-id="60b7c-170">**형식**으로 **SAML 2.0**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-170">As **Type**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="60b7c-171">b.</span><span class="sxs-lookup"><span data-stu-id="60b7c-171">b.</span></span> <span data-ttu-id="60b7c-172">**서비스 공급자 ID**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-172">Select **Service Provider ID**.</span></span>
   
    <span data-ttu-id="60b7c-173">c.</span><span class="sxs-lookup"><span data-stu-id="60b7c-173">c.</span></span> <span data-ttu-id="60b7c-174">Azure 클래식 포털에서 **원격 로그인 URL**을 복사한 다음 **로그인 포털 URL** 텍스트 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-174">On the Azure classic portal, copy the **Remote Login URL**, and then paste it into the **Login Portal URL** textbox.</span></span>
   
    <span data-ttu-id="60b7c-175">d.</span><span class="sxs-lookup"><span data-stu-id="60b7c-175">d.</span></span> <span data-ttu-id="60b7c-176">Azure 클래식 포털에서 **Single Sign-Out 서비스 URL**을 복사한 다음 **로그아웃 URL** 텍스트 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-176">On the Azure classic portal, copy the **Single Sign-Out Service URL**, and then paste it into the **Sign-Out URL** textbox.</span></span>
   
    <span data-ttu-id="60b7c-177">e.</span><span class="sxs-lookup"><span data-stu-id="60b7c-177">e.</span></span> <span data-ttu-id="60b7c-178">Azure 클래식 포털에서 **암호 변경 URL**을 복사한 다음 **암호 변경 URL** 텍스트 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-178">On the Azure classic portal, copy the **Change Password URL**, and then paste it into the **Change Password URL** textbox.</span></span>
   
    <span data-ttu-id="60b7c-179">f.</span><span class="sxs-lookup"><span data-stu-id="60b7c-179">f.</span></span> <span data-ttu-id="60b7c-180">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-180">Click **Save**.</span></span>
8. <span data-ttu-id="60b7c-181">Azure 클래식 포털에서 Single Sign-On 구성 확인을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-181">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    ![Azure AD Connect의 정의][10]
9. <span data-ttu-id="60b7c-183">**Single Sign-On 확인** 페이지에서 **완료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-183">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Connect의 정의][11]

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="60b7c-185">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="60b7c-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="60b7c-186">이 섹션의 목적은 Azure 클래식 포털에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-186">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>  

![Azure AD 사용자 만들기][20]

<span data-ttu-id="60b7c-188">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="60b7c-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="60b7c-189">**Azure 클래식 포털**의 왼쪽 탐색 창에서 **Active Directory**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-189">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-attask-tutorial/create_aaduser_02.png) 
2. <span data-ttu-id="60b7c-191">**디렉터리** 목록에서 디렉터리 통합을 사용하도록 설정할 디렉터리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-191">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="60b7c-192">사용자 목록을 표시하려면 위쪽 메뉴에서 **사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-192">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-attask-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="60b7c-194">**사용자 추가** 대화 상자를 열려면 아래쪽 도구 모음에서 **사용자 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-194">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span> 
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-attask-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="60b7c-196">**이 사용자에 대한 정보 입력** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-196">On the **Tell us about this user** dialog page, perform the following steps:</span></span> 
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-attask-tutorial/create_aaduser_05.png) 
   
    <span data-ttu-id="60b7c-198">a.</span><span class="sxs-lookup"><span data-stu-id="60b7c-198">a.</span></span> <span data-ttu-id="60b7c-199">사용자 유형에서 조직의 새 사용자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-199">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="60b7c-200">b.</span><span class="sxs-lookup"><span data-stu-id="60b7c-200">b.</span></span> <span data-ttu-id="60b7c-201">사용자 이름 **텍스트 상자**에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-201">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="60b7c-202">c.</span><span class="sxs-lookup"><span data-stu-id="60b7c-202">c.</span></span> <span data-ttu-id="60b7c-203">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-203">Click **Next**.</span></span>
6. <span data-ttu-id="60b7c-204">**사용자 프로필** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-204">On the **User Profile** dialog page, perform the following steps:</span></span> 
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-attask-tutorial/create_aaduser_06.png) 
   
    <span data-ttu-id="60b7c-206">a.</span><span class="sxs-lookup"><span data-stu-id="60b7c-206">a.</span></span> <span data-ttu-id="60b7c-207">**이름** 텍스트 상자에 **Britta**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-207">In the **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="60b7c-208">b.</span><span class="sxs-lookup"><span data-stu-id="60b7c-208">b.</span></span> <span data-ttu-id="60b7c-209">**성** 텍스트 상자에 **Simon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-209">In the **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="60b7c-210">c.</span><span class="sxs-lookup"><span data-stu-id="60b7c-210">c.</span></span> <span data-ttu-id="60b7c-211">**표시 이름** 텍스트 상자에 **Britta Simon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-211">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="60b7c-212">d.</span><span class="sxs-lookup"><span data-stu-id="60b7c-212">d.</span></span> <span data-ttu-id="60b7c-213">**역할** 목록에서 **사용자**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-213">In the **Role** list, select **User**.</span></span>

    <span data-ttu-id="60b7c-214">e.</span><span class="sxs-lookup"><span data-stu-id="60b7c-214">e.</span></span> <span data-ttu-id="60b7c-215">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-215">Click **Next**.</span></span>

7. <span data-ttu-id="60b7c-216">**임시 암호 가져오기** 대화 상자 페이지에서 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-216">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-attask-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="60b7c-218">**임시 암호 가져오기** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-218">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-attask-tutorial/create_aaduser_08.png) 
   
    <span data-ttu-id="60b7c-220">a.</span><span class="sxs-lookup"><span data-stu-id="60b7c-220">a.</span></span> <span data-ttu-id="60b7c-221">**새 암호**값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-221">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="60b7c-222">b.</span><span class="sxs-lookup"><span data-stu-id="60b7c-222">b.</span></span> <span data-ttu-id="60b7c-223">**완료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-223">Click **Complete**.</span></span>   

### <a name="creating-an-task-test-user"></a><span data-ttu-id="60b7c-224">@Task 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="60b7c-224">Creating an @Task test user</span></span>
<span data-ttu-id="60b7c-225">이 섹션에서는 @Task에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-225">The objective of this section is to create a user called Britta Simon in @Task.</span></span>

<span data-ttu-id="60b7c-226">**Britta Simon 라는 사용자를 만들려면 @Task, 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="60b7c-226">**To create a user called Britta Simon in @Task, perform the following steps:**</span></span>

1. <span data-ttu-id="60b7c-227">@Task 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-227">Sign on to your @Task company site as administrator.</span></span>
2. <span data-ttu-id="60b7c-228">위쪽의 메뉴에서 **사람**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-228">In the menu on the top, click **People**.</span></span>
3. <span data-ttu-id="60b7c-229">**새 사람**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-229">Click **New Person**.</span></span> 
4. <span data-ttu-id="60b7c-230">새로운 사용자 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-230">On the New Person dialog, perform the following steps:</span></span>
   
    ![@Task 테스트 사용자 만들기][21] 
   
    <span data-ttu-id="60b7c-232">a.</span><span class="sxs-lookup"><span data-stu-id="60b7c-232">a.</span></span> <span data-ttu-id="60b7c-233">**이름** 텍스트 상자에 "Britta"를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-233">In the **First Name** textbox, type "Britta".</span></span>
   
    <span data-ttu-id="60b7c-234">b.</span><span class="sxs-lookup"><span data-stu-id="60b7c-234">b.</span></span> <span data-ttu-id="60b7c-235">**성** 텍스트 상자에 "Simon"을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-235">In the **Last Name** textbox, type "Simon".</span></span>
   
    <span data-ttu-id="60b7c-236">c.</span><span class="sxs-lookup"><span data-stu-id="60b7c-236">c.</span></span> <span data-ttu-id="60b7c-237">**전자 메일 주소** 텍스트 상자에 Azure Active Directory의 Britta Simon 메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-237">In the **Email Address** textbox, type Britta Simon's email address in Azure Active Directory.</span></span>
   
    <span data-ttu-id="60b7c-238">d.</span><span class="sxs-lookup"><span data-stu-id="60b7c-238">d.</span></span> <span data-ttu-id="60b7c-239">**사람 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-239">Click **Add Person**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="60b7c-240">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="60b7c-240">Assigning the Azure AD test user</span></span>
<span data-ttu-id="60b7c-241">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 @Task에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-241">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to @Task.</span></span>

![사용자 할당][200] 

<span data-ttu-id="60b7c-243">**Britta Simon를 할당 하려면 @Task, 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="60b7c-243">**To assign Britta Simon to @Task, perform the following steps:**</span></span>

1. <span data-ttu-id="60b7c-244">Azure 클래식 포털에서 응용 프로그램 보기를 열려면 디렉터리 보기의 최상위 메뉴에서 **응용 프로그램** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-244">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![사용자 할당][201] 
2. <span data-ttu-id="60b7c-246">응용 프로그램 목록에서 **@Task**을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60b7c-246">In the applications list, select **@Task**.</span></span>
   
    ![사용자 할당][202] 
3. <span data-ttu-id="60b7c-248">위쪽의 메뉴에서 **사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-248">In the menu on the top, click **Users**.</span></span>
   
    ![사용자 할당][203] 
4. <span data-ttu-id="60b7c-250">사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-250">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="60b7c-251">아래쪽 도구 모음에서 **할당**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-251">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![사용자 할당][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="60b7c-253">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="60b7c-253">Testing Single Sign-On</span></span>
<span data-ttu-id="60b7c-254">이 섹션은 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-254">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="60b7c-255">액세스 패널에서 @Task 타일을 클릭하면 @Task 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="60b7c-255">When you click the @Task tile in the Access Panel, you should get automatically signed-on to your @Task application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="60b7c-256">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="60b7c-256">Additional Resources</span></span>
* [<span data-ttu-id="60b7c-257">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="60b7c-257">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="60b7c-258">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="60b7c-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-attask-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-attask-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-attask-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-attask-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_01.png
[30]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_02.png


[6]: ./media/active-directory-saas-attask-tutorial/tutorial_general_05.png
[7]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_03.png
[8]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_04.png
[9]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_05.png
[10]: ./media/active-directory-saas-attask-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-attask-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-attask-tutorial/tutorial_general_100.png
[21]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_08.png


[23]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_06.png

[200]: ./media/active-directory-saas-attask-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-attask-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_09.png
[203]: ./media/active-directory-saas-attask-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-attask-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-attask-tutorial/tutorial_general_205.png






