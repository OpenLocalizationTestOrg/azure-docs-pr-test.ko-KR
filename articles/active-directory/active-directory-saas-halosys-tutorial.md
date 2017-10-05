---
title: "자습서: Halosys와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory에서 Halosys를 사용하여 Single Sign-On, 자동화된 프로비전 등을 사용하도록 설정하는 방법을 알아봅니다."
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 42a0eb7c-5cb7-44a9-b00b-b0e7df4b63e8
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 18c5cd8eb4ca211f8ae2b8dd994c0e8c48625a2f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-halosys"></a><span data-ttu-id="33415-103">자습서: Halosys와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="33415-103">Tutorial: Azure Active Directory integration with Halosys</span></span>

<span data-ttu-id="33415-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Halosys를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="33415-104">In this tutorial, you learn how to integrate Halosys with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="33415-105">Halosys를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="33415-105">Integrating Halosys with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="33415-106">Halosys에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33415-106">You can control in Azure AD who has access to Halosys</span></span>
- <span data-ttu-id="33415-107">사용자가 해당 Azure AD 계정으로 Halosys에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33415-107">You can enable your users to automatically get signed-on to Halosys (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="33415-108">단일 중앙 위치인 Azure 클래식 포털에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33415-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="33415-109">Azure AD와의 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory를 사용한 응용 프로그램 액세스 및 Single Sign-On](active-directory-appssoaccess-whatis.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="33415-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="33415-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="33415-110">Prerequisites</span></span>

<span data-ttu-id="33415-111">Halosys와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="33415-111">To configure Azure AD integration with Halosys, you need the following items:</span></span>

- <span data-ttu-id="33415-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="33415-112">An Azure AD subscription</span></span>
- <span data-ttu-id="33415-113">Halosys Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="33415-113">A Halosys single-sign on enabled subscription</span></span>


> [!NOTE] 
> <span data-ttu-id="33415-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="33415-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="33415-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="33415-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="33415-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="33415-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="33415-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33415-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="33415-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="33415-118">Scenario description</span></span>
<span data-ttu-id="33415-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="33415-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="33415-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33415-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="33415-121">갤러리에서 Halosys 추가</span><span class="sxs-lookup"><span data-stu-id="33415-121">Adding Halosys from the gallery</span></span>
2. <span data-ttu-id="33415-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="33415-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-halosys-from-the-gallery"></a><span data-ttu-id="33415-123">갤러리에서 Halosys 추가</span><span class="sxs-lookup"><span data-stu-id="33415-123">Adding Halosys from the gallery</span></span>
<span data-ttu-id="33415-124">Halosys의 Azure AD 통합을 구성하려면 갤러리의 Halosys를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="33415-124">To configure the integration of Halosys into Azure AD, you need to add Halosys from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="33415-125">**갤러리에서 Halosys를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="33415-125">**To add Halosys from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="33415-126">**Azure 클래식 포털**의 왼쪽 탐색 창에서 **Active Directory**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="33415-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>

    ![Active Directory][1]
2. <span data-ttu-id="33415-128">**디렉터리** 목록에서 디렉터리 통합을 사용하도록 설정할 디렉터리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="33415-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="33415-129">응용 프로그램 보기를 열려면 디렉터리 보기의 최상위 메뉴에서 **응용 프로그램** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="33415-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![응용 프로그램][2]

4. <span data-ttu-id="33415-131">페이지 맨 아래에 있는 **추가** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="33415-131">Click **Add** at the bottom of the page.</span></span>

    ![응용 프로그램][3]

5. <span data-ttu-id="33415-133">**수행할 작업** 대화 상자에서 **갤러리에서 응용 프로그램 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="33415-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>

    ![응용 프로그램][4]

6. <span data-ttu-id="33415-135">검색 상자에 **Halosys**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="33415-135">In the search box, type **Halosys**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_01.png)
    
7. <span data-ttu-id="33415-137">결과 창에서 **Halosys**를 선택하고 **완료**를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="33415-137">In the results pane, select **Halosys**, and then click **Complete** to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_011.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="33415-139">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="33415-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="33415-140">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Halosys에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="33415-140">In this section, you configure and test Azure AD single sign-on with Halosys based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="33415-141">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Halosys 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="33415-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Halosys is to a user in Azure AD.</span></span> <span data-ttu-id="33415-142">즉, Azure AD 사용자와 Halosys의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="33415-142">In other words, a link relationship between an Azure AD user and the related user in Halosys needs to be established.</span></span>

<span data-ttu-id="33415-143">이 연결 관계는 Azure AD의 **사용자 이름** 값을 Halosys의 **Username** 값으로 할당하여 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="33415-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Halosys.</span></span>

<span data-ttu-id="33415-144">Halosys에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="33415-144">To configure and test Azure AD single sign-on with Halosys, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="33415-145">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="33415-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="33415-146">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="33415-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="33415-147">**[Halosys 테스트 사용자 만들기](#creating-a-halosys-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 Halosys에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="33415-147">**[Creating a Halosys test user](#creating-a-halosys-test-user)** - to have a counterpart of Britta Simon in Halosys that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="33415-148">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="33415-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="33415-149">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="33415-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="33415-150">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="33415-150">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="33415-151">이 섹션에서는 클래식 포털에서 Azure AD Single Sign-On을 사용하도록 설정하고 Halosys 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="33415-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your Halosys application.</span></span>


<span data-ttu-id="33415-152">**Halosys에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="33415-152">**To configure Azure AD single sign-on with Halosys, perform the following steps:**</span></span>

1. <span data-ttu-id="33415-153">클래식 포털의 **Halosys** 응용 프로그램 통합 페이지에서 **Single Sign-On 구성**을 클릭하여 **Single Sign-On 구성** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="33415-153">In the classic portal, on the **Halosys** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
     
    ![Single Sign-On 구성][6] 

2. <span data-ttu-id="33415-155">**Halosys에 대한 사용자 로그온 방법 선택** 페이지에서 **Azure AD Single Sign-on**을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="33415-155">On the **How would you like users to sign on to Halosys** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_03.png) 

3. <span data-ttu-id="33415-157">**앱 설정 구성** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="33415-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_04.png) 

    <span data-ttu-id="33415-159">a.</span><span class="sxs-lookup"><span data-stu-id="33415-159">a.</span></span> <span data-ttu-id="33415-160">**로그온 URL** 텍스트 상자에 `https://<company-name>.Halosys.com/client-api/api` 패턴을 사용하여 사용자가 Halosys 응용 프로그램에 로그온하는 데 사용할 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="33415-160">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Halosys application using the following pattern: `https://<company-name>.Halosys.com/client-api/api`.</span></span>

    <span data-ttu-id="33415-161">b.**식별자 URL** 텍스트 상자에 `https://<company-name>.Halosys.com` 패턴으로 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="33415-161">b.In the **Identifier URL** textbox, type the URL in the following pattern: `https://<company-name>.Halosys.com`.</span></span>   
         
4. <span data-ttu-id="33415-162">**Halosys에서 Single Sign-On 구성** 페이지에서 **메타데이터 다운로드**를 클릭한 다음 컴퓨터에 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="33415-162">On the **Configure single sign-on at Halosys** page, click **Download metadata**, and then save the file on your computer:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_05.png)
   
5. <span data-ttu-id="33415-164">응용 프로그램에 대해 구성된 SSO를 얻으려면 Halosys 지원 팀에 문의하고 다음을 제공하세요.</span><span class="sxs-lookup"><span data-stu-id="33415-164">To get SSO configured for your application, contact Halosys support team and provide them with the following:</span></span>

    <span data-ttu-id="33415-165">• 다운로드한 **메타데이터 파일**</span><span class="sxs-lookup"><span data-stu-id="33415-165">• The downloaded **metadata file**</span></span>
    
    <span data-ttu-id="33415-166">• **SAML SSO URL**</span><span class="sxs-lookup"><span data-stu-id="33415-166">• The **SAML SSO URL**</span></span>
    

6. <span data-ttu-id="33415-167">클래식 포털에서 Single Sign-On 구성 확인을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="33415-167">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
    
    ![Azure AD Single Sign-On][10]

7. <span data-ttu-id="33415-169">**Single Sign-On 확인** 페이지에서 **완료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="33415-169">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
 
    ![Azure AD Single Sign-On][11]


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="33415-171">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="33415-171">Creating an Azure AD test user</span></span>
<span data-ttu-id="33415-172">이 섹션에서는 클래식 포털에서 Britta Simon이라는 테스트 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="33415-172">In this section, you create a test user in the classic portal called Britta Simon.</span></span>


![Azure AD 사용자 만들기][20]

<span data-ttu-id="33415-174">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="33415-174">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="33415-175">**Azure 클래식 포털**의 왼쪽 탐색 창에서 **Active Directory**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="33415-175">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-Halosys-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="33415-177">**디렉터리** 목록에서 디렉터리 통합을 사용하도록 설정할 디렉터리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="33415-177">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="33415-178">사용자 목록을 표시하려면 위쪽 메뉴에서 **사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="33415-178">To display the list of users, in the menu on the top, click **Users**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-Halosys-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="33415-180">**사용자 추가** 대화 상자를 열려면 아래쪽 도구 모음에서 **사용자 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="33415-180">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-Halosys-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="33415-182">에 **이 사용자에 대해 알리기** 대화 상자 페이지에서 다음 단계를 수행: ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-Halosys-tutorial/create_aaduser_05.png)</span><span class="sxs-lookup"><span data-stu-id="33415-182">On the **Tell us about this user** dialog page, perform the following steps:  ![Creating an Azure AD test user](./media/active-directory-saas-Halosys-tutorial/create_aaduser_05.png)</span></span> 

    <span data-ttu-id="33415-183">a.</span><span class="sxs-lookup"><span data-stu-id="33415-183">a.</span></span> <span data-ttu-id="33415-184">사용자 유형에서 조직의 새 사용자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="33415-184">As Type Of User, select New user in your organization.</span></span>

    <span data-ttu-id="33415-185">b.</span><span class="sxs-lookup"><span data-stu-id="33415-185">b.</span></span> <span data-ttu-id="33415-186">사용자 이름 **텍스트 상자**에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="33415-186">In the User Name **textbox**, type **BrittaSimon**.</span></span>

    <span data-ttu-id="33415-187">c.</span><span class="sxs-lookup"><span data-stu-id="33415-187">c.</span></span> <span data-ttu-id="33415-188">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="33415-188">Click **Next**.</span></span>

6.  <span data-ttu-id="33415-189">**사용자 프로필** 대화 상자 페이지에서 ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-Halosys-tutorial/create_aaduser_06.png) 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="33415-189">On the **User Profile** dialog page, perform the following steps: ![Creating an Azure AD test user](./media/active-directory-saas-Halosys-tutorial/create_aaduser_06.png)</span></span> 

    <span data-ttu-id="33415-190">a.</span><span class="sxs-lookup"><span data-stu-id="33415-190">a.</span></span> <span data-ttu-id="33415-191">**이름** 텍스트 상자에 **Britta**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="33415-191">In the **First Name** textbox, type **Britta**.</span></span>  

    <span data-ttu-id="33415-192">b.</span><span class="sxs-lookup"><span data-stu-id="33415-192">b.</span></span> <span data-ttu-id="33415-193">**성** 텍스트 상자에 **Simon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="33415-193">In the **Last Name** textbox, type, **Simon**.</span></span>

    <span data-ttu-id="33415-194">c.</span><span class="sxs-lookup"><span data-stu-id="33415-194">c.</span></span> <span data-ttu-id="33415-195">**표시 이름** 텍스트 상자에 **Britta Simon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="33415-195">In the **Display Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="33415-196">d.</span><span class="sxs-lookup"><span data-stu-id="33415-196">d.</span></span> <span data-ttu-id="33415-197">**역할** 목록에서 **사용자**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="33415-197">In the **Role** list, select **User**.</span></span>

    <span data-ttu-id="33415-198">e.</span><span class="sxs-lookup"><span data-stu-id="33415-198">e.</span></span> <span data-ttu-id="33415-199">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="33415-199">Click **Next**.</span></span>

7. <span data-ttu-id="33415-200">**임시 암호 가져오기** 대화 상자 페이지에서 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="33415-200">On the **Get temporary password** dialog page, click **create**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-Halosys-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="33415-202">**임시 암호 가져오기** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="33415-202">On the **Get temporary password** dialog page, perform the following steps:</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-Halosys-tutorial/create_aaduser_08.png) 

    <span data-ttu-id="33415-204">a.</span><span class="sxs-lookup"><span data-stu-id="33415-204">a.</span></span> <span data-ttu-id="33415-205">**새 암호**값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="33415-205">Write down the value of the **New Password**.</span></span>

    <span data-ttu-id="33415-206">b.</span><span class="sxs-lookup"><span data-stu-id="33415-206">b.</span></span> <span data-ttu-id="33415-207">**완료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="33415-207">Click **Complete**.</span></span>   



### <a name="creating-a-halosys-test-user"></a><span data-ttu-id="33415-208">Halosys 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="33415-208">Creating a Halosys test user</span></span>

<span data-ttu-id="33415-209">이 섹션에서는 Halosys에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="33415-209">In this section, you create a user called Britta Simon in Halosys.</span></span> <span data-ttu-id="33415-210">Halosys 플랫폼에서 사용자를 추가하려면 Halosys 지원 팀에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="33415-210">Please work with Halosys support team to add the users in the Halosys platform.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="33415-211">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="33415-211">Assigning the Azure AD test user</span></span>

<span data-ttu-id="33415-212">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Halosys에 대한 액세스를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="33415-212">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Halosys.</span></span>

![사용자 할당][200] 

<span data-ttu-id="33415-214">**Britta Simon을 Halosys에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="33415-214">**To assign Britta Simon to Halosys, perform the following steps:**</span></span>

1. <span data-ttu-id="33415-215">클래식 포털에서 응용 프로그램 보기를 열려면 디렉터리 보기의 최상위 메뉴에서 **응용 프로그램** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="33415-215">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="33415-217">응용 프로그램 목록에서 **Halosys**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="33415-217">In the applications list, select **Halosys**.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_50.png) 

3. <span data-ttu-id="33415-219">위쪽의 메뉴에서 **사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="33415-219">In the menu on the top, click **Users**.</span></span>

    ![사용자 할당][203]

4. <span data-ttu-id="33415-221">사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="33415-221">In the Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="33415-222">아래쪽 도구 모음에서 **할당**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="33415-222">In the toolbar on the bottom, click **Assign**.</span></span>

    ![사용자 할당][205]


### <a name="testing-single-sign-on"></a><span data-ttu-id="33415-224">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="33415-224">Testing single sign-on</span></span>

<span data-ttu-id="33415-225">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="33415-225">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="33415-226">액세스 패널에서 Halosys 타일을 클릭하면 Halosys 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="33415-226">When you click the Halosys tile in the Access Panel, you should get automatically signed-on to your Halosys application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="33415-227">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="33415-227">Additional resources</span></span>

* [<span data-ttu-id="33415-228">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="33415-228">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="33415-229">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="33415-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_205.png
