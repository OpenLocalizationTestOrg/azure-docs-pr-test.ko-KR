---
title: "자습서: SciQuest Spend Director와 Azure Active Directory 통합 | Microsoft 문서"
description: "Azure Active Directory 및 SciQuest Spend Director 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 9fab641b-292e-4bef-91d1-8ccc4f3a0c1f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: 84b707668dc45e92e6151f422f1c919f638533b1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sciquest-spend-director"></a><span data-ttu-id="54d73-103">자습서: SciQuest Spend Director와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="54d73-103">Tutorial: Azure Active Directory integration with SciQuest Spend Director</span></span>
<span data-ttu-id="54d73-104">이 자습서에서는 SciQuest Spend Director와 Azure AD(Azure Active Directory)를 통합하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-104">The objective of this tutorial is to show you how to integrate SciQuest Spend Director with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="54d73-105">SciQuest Spend Director를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-105">Integrating SciQuest Spend Director with Azure AD provides you with the following benefits:</span></span> 

* <span data-ttu-id="54d73-106">SciQuest Spend Director에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-106">You can control in Azure AD who has access to SciQuest Spend Director</span></span> 
* <span data-ttu-id="54d73-107">사용자가 해당 Azure AD 계정으로 SciQuest Spend Director에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-107">You can enable your users to automatically get signed-on to SciQuest Spend Director (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="54d73-108">단일 중앙 위치인 Azure 클래식 포털에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="54d73-109">Azure AD와의 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory를 사용한 응용 프로그램 액세스 및 Single Sign-On](active-directory-appssoaccess-whatis.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="54d73-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="54d73-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="54d73-110">Prerequisites</span></span>
<span data-ttu-id="54d73-111">SciQuest Spend Director와의 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-111">To configure Azure AD integration with SciQuest Spend Director, you need the following items:</span></span>

* <span data-ttu-id="54d73-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="54d73-112">An Azure AD subscription</span></span>
* <span data-ttu-id="54d73-113">SciQuest Spend Director Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="54d73-113">A SciQuest Spend Director single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="54d73-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="54d73-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="54d73-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="54d73-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="54d73-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="54d73-118">Scenario Description</span></span>
<span data-ttu-id="54d73-119">이 자습서는 테스트 환경에서 Azure AD Single Sign-on을 테스트하는 데 도움을 주기 위해 제공되었습니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="54d73-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="54d73-121">갤러리에서 SciQuest Spend Director 추가</span><span class="sxs-lookup"><span data-stu-id="54d73-121">Adding SciQuest Spend Director from the gallery</span></span> 
2. <span data-ttu-id="54d73-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="54d73-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sciquest-spend-director-from-the-gallery"></a><span data-ttu-id="54d73-123">갤러리에서 SciQuest Spend Director 추가</span><span class="sxs-lookup"><span data-stu-id="54d73-123">Adding SciQuest Spend Director from the gallery</span></span>
<span data-ttu-id="54d73-124">SciQuest Spend Director의 Azure AD 통합을 구성하려면 갤러리의 SciQuest Spend Director를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-124">To configure the integration of SciQuest Spend Director into Azure AD, you need to add SciQuest Spend Director from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="54d73-125">**갤러리에서 SciQuest Spend Director를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="54d73-125">**To add SciQuest Spend Director from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="54d73-126">**Azure 클래식 포털**의 왼쪽 탐색 창에서 **Active Directory**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]

2. <span data-ttu-id="54d73-128">**디렉터리** 목록에서 디렉터리 통합을 사용하도록 설정할 디렉터리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="54d73-129">응용 프로그램 보기를 열려면 디렉터리 보기의 최상위 메뉴에서 **응용 프로그램** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![응용 프로그램][2]

4. <span data-ttu-id="54d73-131">페이지 맨 아래에 있는 **추가** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-131">Click **Add** at the bottom of the page.</span></span>
   
    ![응용 프로그램][3]

5. <span data-ttu-id="54d73-133">**수행할 작업** 대화 상자에서 **갤러리에서 응용 프로그램 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![응용 프로그램][4]

6. <span data-ttu-id="54d73-135">검색 상자에 **sciQuest spend director**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-135">In the search box, type **sciQuest spend director**.</span></span>
   
    ![응용 프로그램][5]

7. <span data-ttu-id="54d73-137">결과 창에서 **SciQuest Spend Director**를 선택한 다음 **완료**를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-137">In the results pane, select **SciQuest Spend Director**, and then click **Complete** to add the application.</span></span>
   
    ![응용 프로그램][6]

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="54d73-139">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="54d73-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="54d73-140">이 섹션은 "Britta Simon"이라는 테스트 사용자를 기반으로 SciQuest Spend Director에서 Azure AD Single Sign-on을 구성하고 테스트하는 방법을 보여 주기 위해 작성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with SciQuest Spend Director based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="54d73-141">Single Sign-on이 작동되려면 Azure AD는 Azure AD의 사용자에 해당하는 SciQuest Spend Director의 사용자가 누군지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-141">For single sign-on to work, Azure AD needs to know what the counterpart user in SciQuest Spend Director to an user in Azure AD is.</span></span> <span data-ttu-id="54d73-142">즉, Azure AD 사용자와 SciQuest Spend Director의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-142">In other words, a link relationship between an Azure AD user and the related user in SciQuest Spend Director needs to be established.</span></span>  
<span data-ttu-id="54d73-143">이 연결 관계는 Azure AD의 **사용자 이름** 값을 SciQuest Spend Director의 **Username** 값으로 할당하여 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in SciQuest Spend Director.</span></span>

<span data-ttu-id="54d73-144">SciQuest Spend Director에서 Azure AD Single Sign-on을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-144">To configure and test Azure AD single sign-on with SciQuest Spend Director, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="54d73-145">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-145">**[Configuring Azure AD Single Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="54d73-146">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="54d73-147">**[SciQuest Spend Director 테스트 사용자 만들기](#creating-a-halogen-software-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 SciQuest Spend Director에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-147">**[Creating a SciQuest Spend Director test user](#creating-a-halogen-software-test-user)** - to have a counterpart of Britta Simon in SciQuest Spend Director that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="54d73-148">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-On을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="54d73-149">**[Single Sign-On 테스트](#testing-single-sign-on)** - 구성이 작동하는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-single-sign-on"></a><span data-ttu-id="54d73-150">Azure AD Single Sign-on 구성</span><span class="sxs-lookup"><span data-stu-id="54d73-150">Configuring Azure AD Single Single Sign-On</span></span>
<span data-ttu-id="54d73-151">이 섹션은 Azure 클래식 포털에서 Azure AD Single Sign-On을 사용하도록 설정하고 SciQuest Spend Director 응용 프로그램에서 Single Sign-On을 구성하는 방법을 설명하기 위해 제공되었습니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-151">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your SciQuest Spend Director application.</span></span>

<span data-ttu-id="54d73-152">**SciQuest Spend Director에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="54d73-152">**To configure Azure AD single sign-on with SciQuest Spend Director, perform the following steps:**</span></span>

1. <span data-ttu-id="54d73-153">Azure 클래식 포털의 **SciQuest Spend Director** 응용 프로그램 통합 페이지에서 **Single Sign-On 구성**을 클릭하여 **Single Sign-On 구성** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-153">In the Azure classic portal, on the **SciQuest Spend Director** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Single Sign-on 구성][8]

2. <span data-ttu-id="54d73-155">**사용자가 SciQuest Spend Director에 로그인하는 방법을 선택하십시오.** 페이지에서 **Azure AD Single Sign-On**을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-155">On the **How would you like users to sign on to SciQuest Spend Director** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][9]

3. <span data-ttu-id="54d73-157">**앱 설정 구성** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span> 
   
    ![앱 설정 구성][10]
   
     <span data-ttu-id="54d73-159">a.</span><span class="sxs-lookup"><span data-stu-id="54d73-159">a.</span></span> <span data-ttu-id="54d73-160">**로그인 URL** 텍스트 상자에서 *https://.*sciquest.com/.** 패턴을 사용하여 사용자가 SciQuest Spend Director 응용 프로그램에 로그온하는 데 사용하는 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-160">In the **Sign On URL** textbox, type your URL used by your users to sign on to your SciQuest Spend Director application using the following pattern: *https://.*sciquest.com/.**</span></span>
   
     <span data-ttu-id="54d73-161">b.</span><span class="sxs-lookup"><span data-stu-id="54d73-161">b.</span></span> <span data-ttu-id="54d73-162">**회신 URL** 텍스트 상자의 **로그인 URL** 텍스트 상자에서 입력한 것과 동일한 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-162">In the **Reply URL** textbox, type the same value you have typed into the **Sign On URL** textbox.</span></span> 
   
     <span data-ttu-id="54d73-163">c.</span><span class="sxs-lookup"><span data-stu-id="54d73-163">c.</span></span> <span data-ttu-id="54d73-164">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-164">Click **Next**.</span></span>

4. <span data-ttu-id="54d73-165">**SciQuest Spend Director에서 Single Sign-On 구성** 페이지에서 **메타데이터 다운로드**를 클릭한 다음 메타데이터 파일을 컴퓨터에 로컬로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-165">On the **Configure single sign-on at SciQuest Spend Director** page, click **Download metadata**, and then save the metadata file locally on your computer.</span></span>
   
    ![Azure AD Connect의 정의][11]

5. <span data-ttu-id="54d73-167">위에서 다운로드한 메타데이터를 사용하여 이 인증 방법을 설정하도록 SciQuest 지원 팀에 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-167">Contact SciQuest support to enable this authentication method using the above downloaded metadata.</span></span>

6. <span data-ttu-id="54d73-168">Azure 클래식 포털에서 Single Sign-On 구성 확인을 선택하고 **완료**를 클릭하여 **Single Sign-On 구성** 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-168">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span> 
   
    ![Azure AD Connect의 정의][15]

7. <span data-ttu-id="54d73-170">**Single Sign-On 확인** 페이지에서 **완료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-170">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="54d73-171">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="54d73-171">Creating an Azure AD test user</span></span>
<span data-ttu-id="54d73-172">이 섹션의 목적은 Azure 클래식 포털에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-172">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>

<span data-ttu-id="54d73-173">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="54d73-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="54d73-174">**Azure 클래식 포털**의 왼쪽 탐색 창에서 **Active Directory**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-174">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Azure AD Connect의 정의][100] 

2. <span data-ttu-id="54d73-176">**디렉터리** 목록에서 디렉터리 통합을 사용하도록 설정할 디렉터리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-176">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="54d73-177">사용자 목록을 표시하려면 위쪽 메뉴에서 **사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-177">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Azure AD Connect의 정의][101] 

4. <span data-ttu-id="54d73-179">**사용자 추가** 대화 상자를 열려면 아래쪽 도구 모음에서 **사용자 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-179">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span> 
   
    ![Azure AD Connect의 정의][102] 

5. <span data-ttu-id="54d73-181">**이 사용자에 대한 정보 입력** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-181">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Azure AD Connect의 정의][103] 
   
    <span data-ttu-id="54d73-183">a.</span><span class="sxs-lookup"><span data-stu-id="54d73-183">a.</span></span> <span data-ttu-id="54d73-184">**사용자 유형**에서 **조직의 새 사용자**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-184">As **Type Of User**, select **New user in your organization**.</span></span>
   
    <span data-ttu-id="54d73-185">b.</span><span class="sxs-lookup"><span data-stu-id="54d73-185">b.</span></span> <span data-ttu-id="54d73-186">사용자 이름 **텍스트 상자**에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-186">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="54d73-187">c.</span><span class="sxs-lookup"><span data-stu-id="54d73-187">c.</span></span> <span data-ttu-id="54d73-188">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-188">Click **Next**.</span></span>

6. <span data-ttu-id="54d73-189">**사용자 프로필** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-189">On the **User Profile** dialog page, perform the following steps:</span></span> 
   
    ![Azure AD Connect의 정의][104] 
   
    <span data-ttu-id="54d73-191">a.</span><span class="sxs-lookup"><span data-stu-id="54d73-191">a.</span></span> <span data-ttu-id="54d73-192">**이름** 텍스트 상자에 **Britta**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-192">In the **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="54d73-193">b.</span><span class="sxs-lookup"><span data-stu-id="54d73-193">b.</span></span> <span data-ttu-id="54d73-194">**성** 텍스트 상자에 **Simon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-194">In the **Last Name** txtbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="54d73-195">c.</span><span class="sxs-lookup"><span data-stu-id="54d73-195">c.</span></span> <span data-ttu-id="54d73-196">**표시 이름** 텍스트 상자에 **Britta Simon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-196">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="54d73-197">d.</span><span class="sxs-lookup"><span data-stu-id="54d73-197">d.</span></span> <span data-ttu-id="54d73-198">**역할** 목록에서 **사용자**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-198">In the **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="54d73-199">e.</span><span class="sxs-lookup"><span data-stu-id="54d73-199">e.</span></span> <span data-ttu-id="54d73-200">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-200">Click **Next**.</span></span>

7. <span data-ttu-id="54d73-201">**임시 암호 가져오기** 대화 상자 페이지에서 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-201">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Azure AD Connect의 정의][105]  

8. <span data-ttu-id="54d73-203">**임시 암호 가져오기** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-203">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Azure AD Connect의 정의][106]   
   
    <span data-ttu-id="54d73-205">a.</span><span class="sxs-lookup"><span data-stu-id="54d73-205">a.</span></span> <span data-ttu-id="54d73-206">**새 암호**값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-206">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="54d73-207">b.</span><span class="sxs-lookup"><span data-stu-id="54d73-207">b.</span></span> <span data-ttu-id="54d73-208">**완료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-208">Click **Complete**.</span></span>   

### <a name="creating-a-sciquest-spend-director-test-user"></a><span data-ttu-id="54d73-209">SciQuest Spend Director 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="54d73-209">Creating a SciQuest Spend Director test user</span></span>
<span data-ttu-id="54d73-210">이 섹션의 목적은 SciQuest Spend Director에서 Britta Simon이라는 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-210">The objective of this section is to create a user called Britta Simon in SciQuest Spend Director.</span></span>

<span data-ttu-id="54d73-211">테스트 계정을 만들려면 SciQuest Spend Director 지원 팀에 문의한 후 테스트 계정에 대한 세부 정보를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-211">You need to contact your SciQuest Spend Director support team and provide them with the details about your test account to get it created.</span></span>

<span data-ttu-id="54d73-212">또는 SciQuest Spend Director에서 지원되는 Single Sign-On 기능인 Just-in-Tme 프로비저닝을 활용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-212">Alternatively, you can also leverage just-in-time provisioning, a single sign-on feature that is supported by SciQuest Spend Director.</span></span>  
<span data-ttu-id="54d73-213">Just-in-Tme 프로비전을 사용하도록 설정한 경우 계정이 없는 사용자가 Single Sign-On 시도를 수행하는 동안 SciQuest Spend Director에서 사용자 계정이 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-213">If just-in-time provisioning is enabled, users are automatically created by SciQuest Spend Director during a single sign-on attempt if they don't exist.</span></span> <span data-ttu-id="54d73-214">이 기능을 사용하여 Single Sign-On 해당 사용자를 수동으로 만들 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-214">This feature eliminates the need to manually create single sign-on counterpart users.</span></span>

<span data-ttu-id="54d73-215">Just-in-Tme 프로비저닝을 사용하도록 설정하려면 SciQuest Spend Director 지원 팀에 문의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-215">To get just-in-time provisioning enabled, you need to contact your your SciQuest Spend Director support team.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="54d73-216">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="54d73-216">Assigning the Azure AD test user</span></span>
<span data-ttu-id="54d73-217">이 섹션의 목적은 Britta Simon에게 SciQuest Spend Director에 대한 액세스 권한을 부여하여 Single Sign-On을 사용할 수 있도록 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-217">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to SciQuest Spend Director.</span></span>

![Azure AD Connect의 정의][200]

<span data-ttu-id="54d73-219">**SciQuest Spend Director에 Britta Simon를 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="54d73-219">**To assign Britta Simon to SciQuest Spend Director, perform the following steps:**</span></span>

1. <span data-ttu-id="54d73-220">Azure 클래식 포털에서 응용 프로그램 보기를 열려면 디렉터리 보기의 최상위 메뉴에서 **응용 프로그램** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-220">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Azure AD Connect의 정의][201]

2. <span data-ttu-id="54d73-222">응용 프로그램 목록에서 **SciQuest Spend Director**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-222">In the applications list, select **SciQuest Spend Director**.</span></span>
   
    ![Azure AD Connect의 정의][202]

3. <span data-ttu-id="54d73-224">위쪽의 메뉴에서 **사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-224">In the menu on the top, click **Users**.</span></span>
   
    ![Azure AD Connect의 정의][203]

4. <span data-ttu-id="54d73-226">사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-226">In the Users list, select **Britta Simon**.</span></span>
   
    ![Azure AD Connect의 정의][204]

5. <span data-ttu-id="54d73-228">아래쪽 도구 모음에서 **할당**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-228">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Azure AD Connect의 정의][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="54d73-230">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="54d73-230">Testing Single Sign-On</span></span>
<span data-ttu-id="54d73-231">이 섹션은 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-231">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="54d73-232">액세스 패널에서 SciQuest Spend Director 타일을 클릭하면 SciQuest Spend Director 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="54d73-232">When you click the SciQuest Spend Director tile in the Access Panel, you should get automatically signed-on to your SciQuest Spend Director application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="54d73-233">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="54d73-233">Additional Resources</span></span>
* [<span data-ttu-id="54d73-234">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="54d73-234">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="54d73-235">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="54d73-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->
[1]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_01.png
[6]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_05.png
[8]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_06.png
[9]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_07.png
[10]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_08.png
[11]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_03.png
[15]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_04.png

[100]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_09.png 
[101]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_10.png 
[102]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_11.png 
[103]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_12.png 
[104]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_13.png 
[105]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_14.png 
[106]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_15.png 
[200]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_16.png 
[201]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_17.png 
[202]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_06.png
[203]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_18.png
[204]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_19.png
[205]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_20.png

