---
title: "자습서: Soonr Workplace와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory 및 Soonr Workplace 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
editor: na
ms.assetid: b75f5f00-ea8b-4850-ae2e-134e5d678d97
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 76946e4af624d70f2202601ee935523ca3db4314
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-soonr-workplace"></a><span data-ttu-id="1052e-103">자습서: Soonr Workplace와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="1052e-103">Tutorial: Azure Active Directory integration with Soonr Workplace</span></span>

<span data-ttu-id="1052e-104">이 자습서에서는 Soonr Workplace와 Azure AD(Azure Active Directory)를 통합하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1052e-104">The objective of this tutorial is to show you how to integrate Soonr Workplace with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="1052e-105">Soonr Workplace를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="1052e-105">Integrating Soonr Workplace with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1052e-106">Soonr Workplace에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1052e-106">You can control in Azure AD who has access to Soonr Workplace</span></span>
- <span data-ttu-id="1052e-107">사용자가 해당 Azure AD 계정으로 Soonr Workplace에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1052e-107">You can enable your users to automatically get signed-on to Soonr Workplace (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1052e-108">단일 중앙 위치인 Azure 클래식 포털에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1052e-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="1052e-109">Azure AD와의 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory를 사용한 응용 프로그램 액세스 및 Single Sign-On](active-directory-appssoaccess-whatis.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1052e-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1052e-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="1052e-110">Prerequisites</span></span>

<span data-ttu-id="1052e-111">Soonr Workplace와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1052e-111">To configure Azure AD integration with Soonr Workplace, you need the following items:</span></span>

- <span data-ttu-id="1052e-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="1052e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1052e-113">Soonr Workplace Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="1052e-113">A Soonr Workplace single-sign on enabled subscription</span></span>


> [!NOTE] 
> <span data-ttu-id="1052e-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1052e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="1052e-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1052e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1052e-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="1052e-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="1052e-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1052e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="1052e-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="1052e-118">Scenario description</span></span>
<span data-ttu-id="1052e-119">이 자습서는 테스트 환경에서 Azure AD Single Sign-on을 테스트하는 데 도움을 주기 위해 제공되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1052e-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="1052e-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1052e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1052e-121">갤러리에서 Soonr Workplace 추가</span><span class="sxs-lookup"><span data-stu-id="1052e-121">Adding Soonr Workplace from the gallery</span></span>
2. <span data-ttu-id="1052e-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="1052e-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-soonr-workplace-from-the-gallery"></a><span data-ttu-id="1052e-123">갤러리에서 Soonr Workplace 추가</span><span class="sxs-lookup"><span data-stu-id="1052e-123">Adding Soonr Workplace from the gallery</span></span>
<span data-ttu-id="1052e-124">Soonr Workplace의 Azure AD 통합을 구성하려면 갤러리의 Soonr Workplace를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1052e-124">To configure the integration of Soonr Workplace into Azure AD, you need to add Soonr Workplace from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1052e-125">**갤러리에서 Soonr Workplace를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="1052e-125">**To add Soonr Workplace from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1052e-126">**Azure 클래식 포털**의 왼쪽 탐색 창에서 **Active Directory**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1052e-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1052e-128">**디렉터리** 목록에서 디렉터리 통합을 사용하도록 설정할 디렉터리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1052e-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="1052e-129">응용 프로그램 보기를 열려면 디렉터리 보기의 최상위 메뉴에서 **응용 프로그램** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1052e-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![응용 프로그램][2]

4. <span data-ttu-id="1052e-131">페이지 맨 아래에 있는 **추가** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1052e-131">Click **Add** at the bottom of the page.</span></span>

    ![응용 프로그램][3]

5. <span data-ttu-id="1052e-133">**수행할 작업** 대화 상자에서 **갤러리에서 응용 프로그램 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1052e-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
 
    ![응용 프로그램][4]

6. <span data-ttu-id="1052e-135">검색 상자에 **Soonr Workplace**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1052e-135">In the search box, type **Soonr Workplace**.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_01.png)

7. <span data-ttu-id="1052e-137">결과 창에서 **Soonr Workplace**를 선택하고 **완료**를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1052e-137">In the results pane, select **Soonr Workplace**, and then click **Complete** to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_02.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1052e-139">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="1052e-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1052e-140">이 섹션은 "Britta Simon"이라는 테스트 사용자를 기반으로 Soonr Workplace에서 Azure AD Single Sign-On을 구성하고 테스트하는 방법을 보여 주기 위해 작성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1052e-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with Soonr Workplace based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1052e-141">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Soonr Workplace 사용자가 누군지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1052e-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Soonr Workplace to an user in Azure AD is.</span></span> <span data-ttu-id="1052e-142">즉, Azure AD 사용자와 Soonr Workplace의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1052e-142">In other words, a link relationship between an Azure AD user and the related user in Soonr Workplace needs to be established.</span></span>  

<span data-ttu-id="1052e-143">이 연결 관계는 Azure AD의 **사용자 이름** 값을 Soonr Workplace의 **Username** 값으로 할당하여 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1052e-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Soonr Workplace.</span></span>

<span data-ttu-id="1052e-144">Soonr Workplace에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1052e-144">To configure and test Azure AD single sign-on with Soonr Workplace, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1052e-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="1052e-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1052e-146">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1052e-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1052e-147">**[Soonr Workplace 테스트 사용자 만들기](#creating-a-soonr-workplace-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 Soonr Workplace에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1052e-147">**[Creating a Soonr Workplace test user](#creating-a-soonr-workplace-test-user)** - to have a counterpart of Britta Simon in Soonr Workplace that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="1052e-148">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-On을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="1052e-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1052e-149">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1052e-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1052e-150">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="1052e-150">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1052e-151">이 섹션에서는 클래식 포털에서 Azure AD Single Sign-On을 사용하도록 설정하고 Soonr Workplace 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="1052e-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your Soonr Workplace application.</span></span>


<span data-ttu-id="1052e-152">**Soonr Workplace에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="1052e-152">**To configure Azure AD single sign-on with Soonr Workplace, perform the following steps:**</span></span>

1. <span data-ttu-id="1052e-153">Azure 클래식 포털의 **Soonr Workplace** 응용 프로그램 통합 페이지에서 **Single Sign-On 구성**을 클릭하여 **Single Sign-On 구성** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1052e-153">In the Azure classic portal, on the **Soonr Workplace** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>

    ![Single Sign-on 구성][6] 

2. <span data-ttu-id="1052e-155">**Soonr Workplace에 대한 사용자 로그온 방법 선택** 페이지에서 **Azure AD Single Sign-On**을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1052e-155">On the **How would you like users to sign on to Soonr Workplace** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_03.png) 

3. <span data-ttu-id="1052e-157">**앱 설정 구성** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1052e-157">On the **Configure App Settings** dialog page, perform the following steps:.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_04.png) 

    <span data-ttu-id="1052e-159">a.</span><span class="sxs-lookup"><span data-stu-id="1052e-159">a.</span></span> <span data-ttu-id="1052e-160">**로그온 URL** 텍스트 상자에서 `https://<server-name>.soonr.com/singlesignon/saml/SSO` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1052e-160">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<server-name>.soonr.com/singlesignon/saml/SSO`.</span></span>

    <span data-ttu-id="1052e-161">b.</span><span class="sxs-lookup"><span data-stu-id="1052e-161">b.</span></span> <span data-ttu-id="1052e-162">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="1052e-162">Click **Next**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1052e-163">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="1052e-163">Please note that this is not the real value.</span></span> <span data-ttu-id="1052e-164">이 값은 실제 로그인 URL로 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1052e-164">You have to update this value with the actual Sign On URL.</span></span> <span data-ttu-id="1052e-165">이 값을 얻으려면 Soonr Workplace 지원 팀에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="1052e-165">Contact Soonr Workplace support team to get this value.</span></span>

4. <span data-ttu-id="1052e-166">**Soonr Workplace에서 Single Sign-On 구성** 페이지에서 **메타데이터 다운로드**를 클릭한 다음 컴퓨터에 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="1052e-166">On the **Configure single sign-on at Soonr Workplace** page, click **Download metadata** and then save the file on your computer:</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_05.png) 

5. <span data-ttu-id="1052e-168">응용 프로그램에 대해 구성된 SSO를 얻으려면 Soonr Workplace 지원 팀에 문의하고 다음을 제공하십시오.</span><span class="sxs-lookup"><span data-stu-id="1052e-168">To get SSO configured for your application, contact your Soonr Workplace support team and provide them with the following:</span></span> 

    <span data-ttu-id="1052e-169">•  다운로드한 **메타데이터** 파일</span><span class="sxs-lookup"><span data-stu-id="1052e-169">•  The downloaded **Metadata** file</span></span>

    <span data-ttu-id="1052e-170">• **발급자 URL**</span><span class="sxs-lookup"><span data-stu-id="1052e-170">•  The **Issuer URL**</span></span>

    <span data-ttu-id="1052e-171">• **SAML SSO URL**</span><span class="sxs-lookup"><span data-stu-id="1052e-171">•  The **SAML SSO URL**</span></span>

    <span data-ttu-id="1052e-172">• **Single Sign-Out 서비스 URL**</span><span class="sxs-lookup"><span data-stu-id="1052e-172">•  The **Single Sign-Out Service URL**</span></span>

    >[!NOTE]
    ><span data-ttu-id="1052e-173">이 응용 프로그램은 <a href="https://azure.microsoft.com/en-us/marketplace/partners/autotask-corporataion/autotask/">Autotask 작업 공간</a>으로 대체되며 Azure AD를 사용한 응용 프로그램 구성은 <a href="https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-autotaskworkplace-tutorial">이</a> 자습서를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1052e-173">This application is superseded by <a href="https://azure.microsoft.com/en-us/marketplace/partners/autotask-corporataion/autotask/">Autotask Workplace</a> and you can refer <a href="https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-autotaskworkplace-tutorial">this</a> tutorial for configuring the application with Azure AD.</span></span>
   
6. <span data-ttu-id="1052e-174">Azure 클래식 포털에서 Single Sign-On 구성 확인을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1052e-174">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>

    ![Azure AD Single Sign-On][10]

7. <span data-ttu-id="1052e-176">**Single Sign-On 확인** 페이지에서 **완료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1052e-176">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
  
    ![Azure AD Single Sign-On][11]



### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1052e-178">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="1052e-178">Creating an Azure AD test user</span></span>
<span data-ttu-id="1052e-179">이 섹션의 목적은 Azure 클래식 포털에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1052e-179">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>  

![Azure AD 사용자 만들기][20]

<span data-ttu-id="1052e-181">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="1052e-181">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1052e-182">**Azure 클래식 포털**의 왼쪽 탐색 창에서 **Active Directory**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1052e-182">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-soonr-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="1052e-184">**디렉터리** 목록에서 디렉터리 통합을 사용하도록 설정할 디렉터리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1052e-184">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="1052e-185">사용자 목록을 표시하려면 위쪽 메뉴에서 **사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1052e-185">To display the list of users, in the menu on the top, click **Users**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-soonr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1052e-187">**사용자 추가** 대화 상자를 열려면 아래쪽 도구 모음에서 **사용자 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1052e-187">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-soonr-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="1052e-189">**이 사용자에 대한 정보 입력** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1052e-189">On the **Tell us about this user** dialog page, perform the following steps:</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-soonr-tutorial/create_aaduser_05.png) 

    <span data-ttu-id="1052e-191">a.</span><span class="sxs-lookup"><span data-stu-id="1052e-191">a.</span></span> <span data-ttu-id="1052e-192">사용자 유형에서 조직의 새 사용자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1052e-192">As Type Of User, select New user in your organization.</span></span>

    <span data-ttu-id="1052e-193">b.</span><span class="sxs-lookup"><span data-stu-id="1052e-193">b.</span></span> <span data-ttu-id="1052e-194">사용자 이름 **텍스트 상자**에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1052e-194">In the User Name **textbox**, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1052e-195">c.</span><span class="sxs-lookup"><span data-stu-id="1052e-195">c.</span></span> <span data-ttu-id="1052e-196">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1052e-196">Click **Next**.</span></span>

6.  <span data-ttu-id="1052e-197">**사용자 프로필** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1052e-197">On the **User Profile** dialog page, perform the following steps:</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-soonr-tutorial/create_aaduser_06.png) 

    <span data-ttu-id="1052e-199">a.</span><span class="sxs-lookup"><span data-stu-id="1052e-199">a.</span></span> <span data-ttu-id="1052e-200">**이름** 텍스트 상자에 **Britta**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1052e-200">In the **First Name** textbox, type **Britta**.</span></span>  

    <span data-ttu-id="1052e-201">b.</span><span class="sxs-lookup"><span data-stu-id="1052e-201">b.</span></span> <span data-ttu-id="1052e-202">**성** 텍스트 상자에 **Simon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1052e-202">In the **Last Name** textbox, type, **Simon**.</span></span>

    <span data-ttu-id="1052e-203">c.</span><span class="sxs-lookup"><span data-stu-id="1052e-203">c.</span></span> <span data-ttu-id="1052e-204">**표시 이름** 텍스트 상자에 **Britta Simon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1052e-204">In the **Display Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="1052e-205">d.</span><span class="sxs-lookup"><span data-stu-id="1052e-205">d.</span></span> <span data-ttu-id="1052e-206">**역할** 목록에서 **사용자**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1052e-206">In the **Role** list, select **User**.</span></span>

    <span data-ttu-id="1052e-207">e.</span><span class="sxs-lookup"><span data-stu-id="1052e-207">e.</span></span> <span data-ttu-id="1052e-208">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1052e-208">Click **Next**.</span></span>

7. <span data-ttu-id="1052e-209">**임시 암호 가져오기** 대화 상자 페이지에서 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1052e-209">On the **Get temporary password** dialog page, click **create**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-soonr-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="1052e-211">**임시 암호 가져오기** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1052e-211">On the **Get temporary password** dialog page, perform the following steps:</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-soonr-tutorial/create_aaduser_08.png) 

    <span data-ttu-id="1052e-213">a.</span><span class="sxs-lookup"><span data-stu-id="1052e-213">a.</span></span> <span data-ttu-id="1052e-214">**새 암호**값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="1052e-214">Write down the value of the **New Password**.</span></span>

    <span data-ttu-id="1052e-215">b.</span><span class="sxs-lookup"><span data-stu-id="1052e-215">b.</span></span> <span data-ttu-id="1052e-216">페이지 맨 아래에 있는 **완료**을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1052e-216">Click **Complete**.</span></span>   



### <a name="creating-a-soonr-workplace-test-user"></a><span data-ttu-id="1052e-217">Soonr Workplace 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="1052e-217">Creating a Soonr Workplace test user</span></span>

<span data-ttu-id="1052e-218">이 섹션은 Soonr Workplace에서 Britta Simon이라는 사용자를 만들기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1052e-218">The objective of this section is to create a user called Britta Simon in Soonr Workplace.</span></span> <span data-ttu-id="1052e-219">플랫폼에서 사용자를 만들려면 Soonr Workplace 지원 팀과 작업하세요.</span><span class="sxs-lookup"><span data-stu-id="1052e-219">Please work with Soonr Workplace support team to create a user in the platform.</span></span> <span data-ttu-id="1052e-220"><a href="https://na01.safelinks.protection.outlook.com/?url=http%3A%2F%2Fsoonr.com%2FAWPHelp%2FContent%2F0_HOME%2FSupport_for_End_Clients.htm&data=01%7C01%7Cv-saikra%40microsoft.com%7Ccbb4367ab09b4dacaac408d3eebe3f42%7C72f988bf86f141af91ab2d7cd011db47%7C1&sdata=FB92qtE6m%2Fd8yox7AnL2f1h%2FGXwSkma9x9H8Pz0955M%3D&reserved=0/">여기</a>에서 Soonr과 함께 지원 티켓을 발생시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1052e-220">You can raise the support ticket with Soonr from <a href="https://na01.safelinks.protection.outlook.com/?url=http%3A%2F%2Fsoonr.com%2FAWPHelp%2FContent%2F0_HOME%2FSupport_for_End_Clients.htm&data=01%7C01%7Cv-saikra%40microsoft.com%7Ccbb4367ab09b4dacaac408d3eebe3f42%7C72f988bf86f141af91ab2d7cd011db47%7C1&sdata=FB92qtE6m%2Fd8yox7AnL2f1h%2FGXwSkma9x9H8Pz0955M%3D&reserved=0/">here</a>.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1052e-221">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="1052e-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1052e-222">이 섹션의 목적은 Britta Simon에게 Soonr Workplace 액세스 권한을 부여하여 Azure Single Sign-On을 사용할 수 있도록 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1052e-222">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to Soonr Workplace.</span></span>

![사용자 할당][200] 

<span data-ttu-id="1052e-224">**Britta Simon을 Soonr Workplace에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="1052e-224">**To assign Britta Simon to Soonr Workplace, perform the following steps:**</span></span>

1. <span data-ttu-id="1052e-225">Azure 클래식 포털에서 응용 프로그램 보기를 열려면 디렉터리 보기의 최상위 메뉴에서 **응용 프로그램** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1052e-225">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="1052e-227">응용 프로그램 목록에서 **Soonr Workplace**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1052e-227">In the applications list, select **Soonr Workplace**.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_50.png) 

1. <span data-ttu-id="1052e-229">위쪽의 메뉴에서 **사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1052e-229">In the menu on the top, click **Users**.</span></span>

    ![사용자 할당][203] 

1. <span data-ttu-id="1052e-231">사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1052e-231">In the Users list, select **Britta Simon**.</span></span>

2. <span data-ttu-id="1052e-232">아래쪽 도구 모음에서 **할당**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1052e-232">In the toolbar on the bottom, click **Assign**.</span></span>

    ![사용자 할당][205]



### <a name="testing-single-sign-on"></a><span data-ttu-id="1052e-234">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="1052e-234">Testing single sign-on</span></span>

<span data-ttu-id="1052e-235">이 섹션은 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1052e-235">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="1052e-236">액세스 패널에서 Soonr Workplace 타일을 클릭하면 Soonr Workplace 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="1052e-236">When you click the Soonr Workplace tile in the Access Panel, you should get automatically signed-on to your Soonr Workplace application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="1052e-237">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="1052e-237">Additional resources</span></span>

* [<span data-ttu-id="1052e-238">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="1052e-238">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1052e-239">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="1052e-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_205.png
