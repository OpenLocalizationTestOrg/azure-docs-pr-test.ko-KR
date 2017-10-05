---
title: "자습서: Wizergos Productivity Software와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory 및 Wizergos Productivity Software 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: acc04396-13c5-4c24-ab9a-30fbc9234ebd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/20/2017
ms.author: jeedes
ms.openlocfilehash: 73b3bc05aeb337c12acb7e47c0dbebe6d0196530
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wizergos-productivity-software"></a><span data-ttu-id="7a7f0-103">자습서: Wizergos Productivity Software와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="7a7f0-103">Tutorial: Azure Active Directory integration with Wizergos Productivity Software</span></span>
<span data-ttu-id="7a7f0-104">이 자습서에서는 Wizergos Productivity Software와 Azure AD(Azure Active Directory)를 통합하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-104">The objective of this tutorial is to show you how to integrate Wizergos Productivity Software  with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7a7f0-105">Wizergos Productivity Software를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-105">Integrating Wizergos Productivity Software with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="7a7f0-106">Wizergos Productivity Software에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-106">You can control in Azure AD who has access to Wizergos Productivity Software</span></span>
* <span data-ttu-id="7a7f0-107">사용자가 해당 Azure AD 계정으로 Wizergos Productivity Software SSO(Single Sign-on)에 자동으로 로그온되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-107">You can enable your users to automatically get signed-on to Wizergos Productivity Software single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="7a7f0-108">단일 중앙 위치인 Azure 클래식 포털에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="7a7f0-109">Azure AD와의 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory를 사용한 응용 프로그램 액세스 및 Single Sign-On](active-directory-appssoaccess-whatis.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7a7f0-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="7a7f0-110">Prerequisites</span></span>
<span data-ttu-id="7a7f0-111">Wizergos Productivity Software와의 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-111">To configure Azure AD integration with Wizergos Productivity Software, you need the following items:</span></span>

* <span data-ttu-id="7a7f0-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="7a7f0-112">An Azure AD subscription</span></span>
* <span data-ttu-id="7a7f0-113">Wizergos Productivity Software SSO가 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="7a7f0-113">A Wizergos Productivity Software SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="7a7f0-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="7a7f0-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="7a7f0-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="7a7f0-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7a7f0-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="7a7f0-118">Scenario description</span></span>
<span data-ttu-id="7a7f0-119">이 자습서는 테스트 환경에서 Azure AD SSO를 테스트하는 데 도움을 주기 위해 제공되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="7a7f0-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7a7f0-121">갤러리에서 Wizergos Productivity Software 추가</span><span class="sxs-lookup"><span data-stu-id="7a7f0-121">Adding Wizergos Productivity Software from the gallery</span></span>
2. <span data-ttu-id="7a7f0-122">Azure AD SSO 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="7a7f0-122">Configuring and testing Azure AD SSO</span></span>

## <a name="adding-wizergos-productivity-software-from-the-gallery"></a><span data-ttu-id="7a7f0-123">갤러리에서 Wizergos Productivity Software 추가</span><span class="sxs-lookup"><span data-stu-id="7a7f0-123">Adding Wizergos Productivity Software from the gallery</span></span>
<span data-ttu-id="7a7f0-124">Wizergos Productivity Software의 Azure AD 통합을 구성하려면 갤러리의 Wizergos Productivity Software를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-124">To configure the integration of Wizergos Productivity Software into Azure AD, you need to add Wizergos Productivity Software from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7a7f0-125">**갤러리에서 Wizergos Productivity Software를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="7a7f0-125">**To add Wizergos Productivity Software from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7a7f0-126">**Azure 클래식 포털**의 왼쪽 탐색 창에서 **Active Directory**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-126">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="7a7f0-128">**디렉터리** 목록에서 디렉터리 통합을 사용하도록 설정할 디렉터리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="7a7f0-129">응용 프로그램 보기를 열려면 디렉터리 보기의 최상위 메뉴에서 **응용 프로그램** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![응용 프로그램][2]
4. <span data-ttu-id="7a7f0-131">페이지 맨 아래에 있는 **추가** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-131">Click **Add** at the bottom of the page.</span></span>
   
    ![응용 프로그램][3]
5. <span data-ttu-id="7a7f0-133">**수행할 작업** 대화 상자에서 **갤러리에서 응용 프로그램 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![응용 프로그램][4]
6. <span data-ttu-id="7a7f0-135">검색 상자에 **Wizergos Productivity Software**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-135">In the search box, type **Wizergos Productivity Software**.</span></span>
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_01.png)
7. <span data-ttu-id="7a7f0-137">결과 창에서 **Wizergos Productivity Software**를 선택하고 **완료**를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-137">In the results panel, select **Wizergos Productivity Software**, and then click **Complete** to add the application.</span></span>
   
    ![갤러리에서 앱 선택](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_001.png)

## <a name="configure-and-test-azure-ad-sso"></a><span data-ttu-id="7a7f0-139">Azure AD SSO 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="7a7f0-139">Configure and test Azure AD SSO</span></span>
<span data-ttu-id="7a7f0-140">이 섹션은 "Britta Simon"이라는 테스트 사용자를 기반으로 Wizergos Productivity Software에서 Azure AD SSO를 구성하고 테스트하는 방법을 보여 주기 위해 작성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-140">The objective of this section is to show you how to configure and test Azure AD SSO with Wizergos Productivity Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7a7f0-141">SSO가 작동되려면 Azure AD는 Azure AD의 사용자에 해당하는 Wizergos Productivity Software의 사용자가 누군지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-141">For SSO to work, Azure AD needs to know what the counterpart user in Wizergos Productivity Software to an user in Azure AD is.</span></span> <span data-ttu-id="7a7f0-142">즉, Azure AD 사용자와 Wizergos Productivity Software의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-142">In other words, a link relationship between an Azure AD user and the related user in Wizergos Productivity Software needs to be established.</span></span>

<span data-ttu-id="7a7f0-143">이 연결 관계는 Azure AD의 **사용자 이름** 값을 Wizergos Productivity Software의 **Username** 값으로 할당하여 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Wizergos Productivity Software.</span></span>

<span data-ttu-id="7a7f0-144">BynWizergos Productivity Software에서 Azure AD Single Sign-on을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-144">To configure and test Azure AD single sign-on with BynWizergos Productivity Softwareder, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7a7f0-145">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7a7f0-146">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-on 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7a7f0-147">**[Wizergos Productivity Software 테스트 사용자 만들기](#creating-a-wizergos-productivity-software-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 Wizergos Productivity Software에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-147">**[Creating a Wizergos Productivity Software test user](#creating-a-wizergos-productivity-software-test-user)** - to have a counterpart of Britta Simon in Wizergos Productivity Software that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="7a7f0-148">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7a7f0-149">**[Single Sign-On 테스트](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-sso"></a><span data-ttu-id="7a7f0-150">Azure AD SSO 구성</span><span class="sxs-lookup"><span data-stu-id="7a7f0-150">Configuring Azure AD SSO</span></span>
<span data-ttu-id="7a7f0-151">이 섹션에서는 클래식 포털에서 Azure AD Single Sign-On을 사용하도록 설정하고 Wizergos Productivity Software 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your Wizergos Productivity Software application.</span></span>

<span data-ttu-id="7a7f0-152">**Wizergos Productivity Software에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="7a7f0-152">**To configure Azure AD single sign-on with Wizergos Productivity Software, perform the following steps:**</span></span>

1. <span data-ttu-id="7a7f0-153">클래식 포털의 **Wizergos Productivity Software** 응용 프로그램 통합 페이지에서 **Single Sign-On 구성**을 클릭하여 **Single Sign-On 구성** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-153">In the classic portal, on the **Wizergos Productivity Software** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Single Sign-on 구성][6] 
2. <span data-ttu-id="7a7f0-155">**Wizergos Productivity Software에 대한 사용자 로그온 방법을 선택하십시오.** 페이지에서 **Azure AD Single Sign-On**을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-155">On the **How would you like users to sign on to Wizergos Productivity Software** page, select **Azure AD Single Sign-On**, and then click **Next**:</span></span>
   
    ![Single Sign-On 구성](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_03.png)
3. <span data-ttu-id="7a7f0-157">**앱 설정 구성** 대화 상자 페이지에서 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-157">On the **Configure App Settings** dialog page, click **Next**:</span></span>
   
    ![Single Sign-On 구성](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_04.png)
4. <span data-ttu-id="7a7f0-159">**Wizergos Productivity Software에서 Single Sign-On 구성** 페이지에서 **인증서 다운로드**를 클릭하여 컴퓨터에 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-159">On the **Configure single sign-on at Wizergos Productivity Software** page, click **Download certificate**, and then save the file on your computer:</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_05.png)
5. <span data-ttu-id="7a7f0-161">다른 웹 브라우저 창에서 Wizergos Productivity Software 테넌트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-161">In a different web browser window, sign-on to your Wizergos Productivity Software tenant as an administrator.</span></span>
6. <span data-ttu-id="7a7f0-162">햄버거 메뉴에서 **관리자**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-162">From the hamburger menu, select **Admin**.</span></span>
   
    ![앱 쪽에서 Single Sign-On 구성](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_000.png)
7. <span data-ttu-id="7a7f0-164">왼쪽 메뉴의 관리자 페이지에서 **인증**을 선택하고 **Azure AD**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-164">In Admin page on left hand menu select **AUTHENTICATION** and click on **Azure AD**.</span></span>
   
    ![앱 쪽에서 Single Sign-On 구성](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_002.png)
8. <span data-ttu-id="7a7f0-166">**인증** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-166">Perform the following steps on **AUTHENTICATION** section.</span></span>
   
    ![앱 쪽에서 Single Sign-On 구성](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_003.png)
  1. <span data-ttu-id="7a7f0-168">**업로드** 버튼을 클릭하여 Azure AD에서 다운로드한 인증서를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-168">Click **UPLOAD** button to upload the downloaded certificate from Azure AD.</span></span> 
  2. <span data-ttu-id="7a7f0-169">**발급자 URL** 텍스트 상자에 Azure AD 응용 프로그램 구성 마법사에서 나온 **발급자 URL** 값을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-169">In the **Issuer URL** textbox put the value of **Issuer URL** from Azure AD application configuration wizard.</span></span>
  3. <span data-ttu-id="7a7f0-170">**Single Sign-On URL** 텍스트 상자에 Azure AD 응용 프로그램 구성 마법사의 **Single Sign-on 서비스 URL** 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-170">In the **Single Sign-On URL** textbox put the value of **Single Sign-on Service URL** from Azure AD application configuration wizard.</span></span>
  4. <span data-ttu-id="7a7f0-171">**Single Sign-Out URL** 텍스트 상자에 Azure AD 응용 프로그램 구성 마법사의 **Single Sign-Out 서비스 URL** 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-171">In the **Single Sign-Out URL** textbox put the value of **Single Sign-out Service URL** from Azure AD application configuration wizard.</span></span>
  5. <span data-ttu-id="7a7f0-172">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-172">Click **Save** button.</span></span>
9. <span data-ttu-id="7a7f0-173">클래식 포털에서 Single Sign-On 구성 확인을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-173">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
10. <span data-ttu-id="7a7f0-175">**Single Sign-On 확인** 페이지에서 **완료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-175">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
    
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="7a7f0-177">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="7a7f0-177">Create an Azure AD test user</span></span>
<span data-ttu-id="7a7f0-178">이 섹션의 목적은 클래식 포털에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-178">The objective of this section is to create a test user in the classic portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][20]

<span data-ttu-id="7a7f0-180">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="7a7f0-180">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7a7f0-181">**Azure 클래식 포털**의 왼쪽 탐색 창에서 **Active Directory**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-181">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_09.png)
2. <span data-ttu-id="7a7f0-183">**디렉터리** 목록에서 디렉터리 통합을 사용하도록 설정할 디렉터리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-183">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="7a7f0-184">사용자 목록을 표시하려면 위쪽 메뉴에서 **사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-184">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_03.png)
4. <span data-ttu-id="7a7f0-186">**사용자 추가** 대화 상자를 열려면 아래쪽 도구 모음에서 **사용자 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-186">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_04.png)
5. <span data-ttu-id="7a7f0-188">**이 사용자에 대한 정보 입력** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-188">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_05.png) 
  1. <span data-ttu-id="7a7f0-190">사용자 유형에서 조직의 새 사용자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-190">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="7a7f0-191">사용자 이름 **텍스트 상자**에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-191">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="7a7f0-192">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-192">Click **Next**.</span></span>
6. <span data-ttu-id="7a7f0-193">**사용자 프로필** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-193">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_06.png)
  1. <span data-ttu-id="7a7f0-195">**이름** 텍스트 상자에 **Britta**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-195">In the **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="7a7f0-196">**성** 텍스트 상자에 **Simon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-196">In the **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="7a7f0-197">**표시 이름** 텍스트 상자에 **Britta Simon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-197">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="7a7f0-198">**역할** 목록에서 **사용자**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-198">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="7a7f0-199">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-199">Click **Next**.</span></span>
7. <span data-ttu-id="7a7f0-200">**임시 암호 가져오기** 대화 상자 페이지에서 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-200">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_07.png)
8. <span data-ttu-id="7a7f0-202">**임시 암호 가져오기** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-202">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_08.png)
  1. <span data-ttu-id="7a7f0-204">**새 암호**값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-204">Write down the value of the **New Password**.</span></span>
  2. <span data-ttu-id="7a7f0-205">페이지 맨 아래에 있는 **완료**을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-205">Click **Complete**.</span></span>   

### <a name="create-a-wizergos-productivity-software-test-user"></a><span data-ttu-id="7a7f0-206">Wizergos Productivity Software 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="7a7f0-206">Create a Wizergos Productivity Software test user</span></span>
<span data-ttu-id="7a7f0-207">이 섹션에서는 Wizergos Productivity Software에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-207">In this section, you create a user called Britta Simon in Wizergos Productivity Software.</span></span> <span data-ttu-id="7a7f0-208">Wizergos Productivity Software 플랫폼에 사용자를 추가하려면 [support@wizergos.com](emailTo:support@wizergos.com) 을 통해 Wizergos Productivity Software 지원 팀과 함께 작업하세요.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-208">Please work with Wizergos Productivity Software support team via [support@wizergos.com](emailTo:support@wizergos.com) to add the users in the Wizergos Productivity Software platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="7a7f0-209">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="7a7f0-209">Assign the Azure AD test user</span></span>
<span data-ttu-id="7a7f0-210">이 섹션은 Britta Simon에게 Wizergos Productivity Software에 대한 액세스 권한을 부여하여 Azure SSO를 사용할 수 있기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-210">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Wizergos Productivity Software.</span></span>

  ![사용자 할당][200]

<span data-ttu-id="7a7f0-212">**Britta Simon을 Wizergos Productivity Software에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="7a7f0-212">**To assign Britta Simon to Wizergos Productivity Software, perform the following steps:**</span></span>

1. <span data-ttu-id="7a7f0-213">클래식 포털에서 응용 프로그램 보기를 열려면 디렉터리 보기의 최상위 메뉴에서 **응용 프로그램** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-213">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![사용자 할당][201]
2. <span data-ttu-id="7a7f0-215">응용 프로그램 목록에서 **Wizergos Productivity Software**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-215">In the applications list, select **Wizergos Productivity Software**.</span></span>
   
    ![Single Sign-On 구성](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_50.png)
3. <span data-ttu-id="7a7f0-217">위쪽의 메뉴에서 **사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-217">In the menu on the top, click **Users**.</span></span>
   
    ![사용자 할당][203]
4. <span data-ttu-id="7a7f0-219">사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-219">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="7a7f0-220">아래쪽 도구 모음에서 **할당**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-220">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![사용자 할당][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="7a7f0-222">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="7a7f0-222">Test single sign-on</span></span>
<span data-ttu-id="7a7f0-223">이 섹션은 액세스 패널을 사용하여 Azure AD SSO 구성을 테스트하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-223">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="7a7f0-224">액세스 패널에서 Wizergos Productivity Software 타일을 클릭하면 Wizergos Productivity Software 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a7f0-224">When you click the Wizergos Productivity Software tile in the Access Panel, you should get automatically signed-on to your Wizergos Productivity Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7a7f0-225">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="7a7f0-225">Additional resources</span></span>
* [<span data-ttu-id="7a7f0-226">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="7a7f0-226">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7a7f0-227">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="7a7f0-227">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_205.png
