---
title: "자습서: Bynder와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 Bynder 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 4fb0ab26-b3b9-420a-8072-a0be80ea021e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: 6786d7eb6a11405278ef7267f25279f9e39b3bde
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bynder"></a><span data-ttu-id="1dc5e-103">자습서: Bynder와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="1dc5e-103">Tutorial: Azure Active Directory integration with Bynder</span></span>
<span data-ttu-id="1dc5e-104">이 자습서에서는 Bynder와 Azure AD(Azure Active Directory)를 통합하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-104">The objective of this tutorial is to show you how to integrate Bynder with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1dc5e-105">Bynder를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-105">Integrating Bynder with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="1dc5e-106">Bynder에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-106">You can control in Azure AD who has access to Bynder</span></span>
* <span data-ttu-id="1dc5e-107">사용자가 해당 Azure AD 계정으로 Bynder SSO(Single Sign-on)에 자동으로 로그온되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-107">You can enable your users to automatically get signed-on to Bynder single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="1dc5e-108">단일 중앙 위치인 Azure 클래식 포털에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="1dc5e-109">Azure AD와의 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory를 사용한 응용 프로그램 액세스 및 Single Sign-On](active-directory-appssoaccess-whatis.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1dc5e-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="1dc5e-110">Prerequisites</span></span>
<span data-ttu-id="1dc5e-111">Bynder와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-111">To configure Azure AD integration with Bynder, you need the following items:</span></span>

* <span data-ttu-id="1dc5e-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="1dc5e-112">An Azure AD subscription</span></span>
* <span data-ttu-id="1dc5e-113">Bynder SSO(Single Sign-On)가 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="1dc5e-113">A Bynder single-sign on (SSO) enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="1dc5e-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="1dc5e-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="1dc5e-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="1dc5e-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1dc5e-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="1dc5e-118">Scenario description</span></span>
<span data-ttu-id="1dc5e-119">이 자습서는 테스트 환경에서 Microsoft Azure AD SSO를 테스트하는 데 도움을 주기 위해 제공되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-119">The objective of this tutorial is to enable you to test Microsoft Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="1dc5e-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1dc5e-121">갤러리에서 Bynder 추가</span><span class="sxs-lookup"><span data-stu-id="1dc5e-121">Adding Bynder from the gallery</span></span>
2. <span data-ttu-id="1dc5e-122">Microsoft Azure AD SSO 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="1dc5e-122">Configuring and testing Microsoft Azure AD SSO</span></span>

## <a name="add-bynder-from-the-gallery"></a><span data-ttu-id="1dc5e-123">갤러리에서 Bynder 추가</span><span class="sxs-lookup"><span data-stu-id="1dc5e-123">Add Bynder from the gallery</span></span>
<span data-ttu-id="1dc5e-124">Bynder의 Azure AD 통합을 구성하려면 갤러리의 Bynder를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-124">To configure the integration of Bynder into Azure AD, you need to add Bynder from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1dc5e-125">**갤러리에서 Bynder를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="1dc5e-125">**To add Bynder from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1dc5e-126">**Azure 클래식 포털**의 왼쪽 탐색 창에서 **Active Directory**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-126">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="1dc5e-128">**디렉터리** 목록에서 디렉터리 통합을 사용하도록 설정할 디렉터리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="1dc5e-129">응용 프로그램 보기를 열려면 디렉터리 보기의 최상위 메뉴에서 **응용 프로그램** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![응용 프로그램][2]
4. <span data-ttu-id="1dc5e-131">페이지 맨 아래에 있는 **추가** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-131">Click **Add** at the bottom of the page.</span></span>
   
    ![응용 프로그램][3]
5. <span data-ttu-id="1dc5e-133">**수행할 작업** 대화 상자에서 **갤러리에서 응용 프로그램 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![응용 프로그램][4]
6. <span data-ttu-id="1dc5e-135">검색 상자에 **Bynder**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-135">In the search box, type **Bynder**.</span></span>
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_01.png)
7. <span data-ttu-id="1dc5e-137">결과 창에서 **Bynder**를 선택하고 **완료**를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-137">In the results panel, select **Bynder**, and then click **Complete** to add the application.</span></span>
   
    ![갤러리에서 앱 선택](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_001.png)

## <a name="configure-and-test-microsoft-azure-ad-sso"></a><span data-ttu-id="1dc5e-139">Microsoft Azure AD SSO 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="1dc5e-139">Configure and test Microsoft Azure AD SSO</span></span>
<span data-ttu-id="1dc5e-140">이 섹션은 "Britta Simon"이라는 테스트 사용자를 기반으로 Bynder에서 Microsoft Azure AD SSO를 구성하고 테스트하는 방법을 보여 주기 위해 작성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-140">The objective of this section is to show you how to configure and test Microsoft Azure AD SSO with Bynder based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1dc5e-141">SSO가 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Bynder 사용자가 누군지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-141">For SSO to work, Azure AD needs to know what the counterpart user in Bynder to an user in Azure AD is.</span></span> <span data-ttu-id="1dc5e-142">즉, Azure AD 사용자와 Bynder의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-142">In other words, a link relationship between an Azure AD user and the related user in Bynder needs to be established.</span></span>

<span data-ttu-id="1dc5e-143">이 연결 관계는 Azure AD의 **사용자 이름** 값을 Bynder의 **Username** 값으로 할당하여 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Bynder.</span></span>

<span data-ttu-id="1dc5e-144">Bynder에서 Microsoft Azure AD SSO를 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-144">To configure and test Microsoft Azure AD SSO with Bynder, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1dc5e-145">**[Microsoft Azure AD Single Sign-On 구성](#configuring-azure-ad-single-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-145">**[Configuring Microsoft Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1dc5e-146">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Microsoft Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Microsoft Azure AD Single Sign-On with Britta Simon.</span></span>
3. <span data-ttu-id="1dc5e-147">**[Bynder 테스트 사용자 만들기](#creating-a-bynder-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 Bynder에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-147">**[Creating a Bynder test user](#creating-a-bynder-test-user)** - to have a counterpart of Britta Simon in Bynder that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="1dc5e-148">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Microsoft Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Microsoft Azure AD Single Sign-On.</span></span>
5. <span data-ttu-id="1dc5e-149">**[Single Sign-On 테스트](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-microsoft-azure-ad-sso"></a><span data-ttu-id="1dc5e-150">Microsoft Azure AD SSO 구성</span><span class="sxs-lookup"><span data-stu-id="1dc5e-150">Configuring Microsoft Azure AD SSO</span></span>
<span data-ttu-id="1dc5e-151">이 섹션에서는 클래식 포털에서 Microsoft Azure AD SSO를 사용하도록 설정하고 Bynder 응용 프로그램에서 SSO를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-151">In this section, you enable Microsoft Azure AD SSO in the classic portal and configure SSO in your Bynder application.</span></span>

<span data-ttu-id="1dc5e-152">**Bynder에서 Microsoft Azure AD SSO를 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="1dc5e-152">**To configure Microsoft Azure AD SSO with Bynder, perform the following steps:**</span></span>

1. <span data-ttu-id="1dc5e-153">클래식 포털의 **Bynder** 응용 프로그램 통합 페이지에서 **Single Sign-on 구성**을 클릭하여 **Single Sign-on 구성** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-153">In the classic portal, on the **Bynder** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Single Sign-On 구성][6] 
2. <span data-ttu-id="1dc5e-155">**Bynder에 대한 사용자 로그온 방법을 선택하십시오.** 페이지에서 **Microsoft Azure AD Single Sign-on**을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-155">On the **How would you like users to sign on to Bynder** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_03.png)
3. <span data-ttu-id="1dc5e-157">**앱 설정 구성** 대화 상자 페이지에서 **IDP 시작 모드**로 응용 프로그램을 구성하려는 경우 다음 단계를 수행하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-157">On the **Configure App Settings** dialog page, If you wish to configure the application in **IDP initiated mode**, perform the following steps and click **Next**:</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_04.png)
  1. <span data-ttu-id="1dc5e-159">**회신 URL** 텍스트 상자에 다음 패턴으로 URL을 입력합니다.`https://<company name>.getbynder.com/sso/SAML/authenticate/`</span><span class="sxs-lookup"><span data-stu-id="1dc5e-159">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.getbynder.com/sso/SAML/authenticate/`</span></span>
  2. <span data-ttu-id="1dc5e-160">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-160">Click **Next**.</span></span>
4. <span data-ttu-id="1dc5e-161">**앱 설정 구성** 대화 상자 페이지에서 **SP 시작 모드**로 응용 프로그램을 구성하려는 경우 **"고급 설정 표시(선택 사항)"**를 클릭하고 **로그온 URL**을 입력한 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-161">If you wish to configure the application in **SP initiated mode** on the **Configure App Settings** dialog page, then click on the **“Show advanced settings (optional)”** and then enter the **Sign On URL** and click **Next**.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_10.png)
  1. <span data-ttu-id="1dc5e-163">**로그온 URL** 텍스트 상자에서 다음 패턴 `https://<company name>.getbynder.com/login/`을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-163">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<company name>.getbynder.com/login/`</span></span>
  2. <span data-ttu-id="1dc5e-164">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-164">Click **Next**.</span></span>
  
   >[!NOTE]
   ><span data-ttu-id="1dc5e-165">이 자습서의 로그온 URL 값은 자리 표시자일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-165">The value for the Sign On URL in this tutorial is just a placeholfer.</span></span> <span data-ttu-id="1dc5e-166">작업 환경에 대한 실제 값을 가져오려면 Bynder에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-166">To get the actual vlaue for your environment, contact Bynder.</span></span>
   >

5. <span data-ttu-id="1dc5e-167">**Bynder에서 Single Sign-On 구성** 페이지에서 다음 단계를 수행하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-167">On the **Configure single sign-on at Bynder** page, perform the following steps and click **Next**:</span></span>
   
    ![Single Sign-On 구성](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_05.png)  
  1. <span data-ttu-id="1dc5e-169">**메타데이터 다운로드**를 클릭하고 파일을 컴퓨터에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-169">Click **Download metadata**, and then save the file on your computer.</span></span>
  2. <span data-ttu-id="1dc5e-170">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-170">Click **Next**.</span></span>
6. <span data-ttu-id="1dc5e-171">응용 프로그램에 대해 SSO를 구성하려면 Bynder 지원 팀에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-171">To get SSO configured for your application, contact your Bynder support team.</span></span> <span data-ttu-id="1dc5e-172">다운로드한 메타데이터 파일을 첨부하고 Bynder 팀에서 SSO를 설정할 수 있게 공유하세요.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-172">Attach the downloaded metadata file and share it with Bynder team to set up SSO on their side.</span></span>
7. <span data-ttu-id="1dc5e-173">클래식 포털에서 Single Sign-On 구성 확인을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-173">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
8. <span data-ttu-id="1dc5e-175">**Single Sign-On 확인** 페이지에서 **완료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-175">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="1dc5e-177">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="1dc5e-177">Create an Azure AD test user</span></span>
<span data-ttu-id="1dc5e-178">이 섹션의 목적은 클래식 포털에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-178">The objective of this section is to create a test user in the classic portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][20]

<span data-ttu-id="1dc5e-180">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="1dc5e-180">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1dc5e-181">**Azure 클래식 포털**의 왼쪽 탐색 창에서 **Active Directory**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-181">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-bynder-tutorial/create_aaduser_09.png)
2. <span data-ttu-id="1dc5e-183">**디렉터리** 목록에서 디렉터리 통합을 사용하도록 설정할 디렉터리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-183">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="1dc5e-184">사용자 목록을 표시하려면 위쪽 메뉴에서 **사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-184">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-bynder-tutorial/create_aaduser_03.png)
4. <span data-ttu-id="1dc5e-186">**사용자 추가** 대화 상자를 열려면 아래쪽 도구 모음에서 **사용자 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-186">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-bynder-tutorial/create_aaduser_04.png)
5. <span data-ttu-id="1dc5e-188">**이 사용자에 대한 정보 입력** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-188">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-bynder-tutorial/create_aaduser_05.png)
  1. <span data-ttu-id="1dc5e-190">사용자 유형에서 조직의 새 사용자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-190">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="1dc5e-191">사용자 이름 **텍스트 상자**에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-191">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="1dc5e-192">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-192">Click **Next**.</span></span>
6. <span data-ttu-id="1dc5e-193">**사용자 프로필** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-193">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-bynder-tutorial/create_aaduser_06.png)
  1. <span data-ttu-id="1dc5e-195">**이름** 텍스트 상자에 **Britta**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-195">In the **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="1dc5e-196">**성** 텍스트 상자에 **Simon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-196">In the **Last Name** textbox, type, **Simon**.</span></span> 
  3. <span data-ttu-id="1dc5e-197">**표시 이름** 텍스트 상자에 **Britta Simon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-197">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="1dc5e-198">**역할** 목록에서 **사용자**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-198">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="1dc5e-199">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-199">Click **Next**.</span></span>
7. <span data-ttu-id="1dc5e-200">**임시 암호 가져오기** 대화 상자 페이지에서 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-200">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-bynder-tutorial/create_aaduser_07.png)
8. <span data-ttu-id="1dc5e-202">**임시 암호 가져오기** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-202">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-bynder-tutorial/create_aaduser_08.png)
   1. <span data-ttu-id="1dc5e-204">**새 암호**값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-204">Write down the value of the **New Password**.</span></span>
   2. <span data-ttu-id="1dc5e-205">페이지 맨 아래에 있는 **완료**을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-205">Click **Complete**.</span></span>   

### <a name="create-a-bynder-test-user"></a><span data-ttu-id="1dc5e-206">Bynder 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="1dc5e-206">Create a Bynder test user</span></span>
<span data-ttu-id="1dc5e-207">이 섹션은 Bynder에서 Britta Simon이라는 사용자를 만들기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-207">The objective of this section is to create a user called Britta Simon in Bynder.</span></span> <span data-ttu-id="1dc5e-208">Bynder는 적시에 프로비전을 지원하며 기본적으로 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-208">Bynder supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="1dc5e-209">이 섹션에 작업 항목이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-209">There is no action item for you in this section.</span></span> <span data-ttu-id="1dc5e-210">새 사용자가 아직 존재하지 않는 경우 Bynder에 액세스하는 동안 만들어질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-210">A new user will be created during an attempt to access Bynder if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="1dc5e-211">사용자를 수동으로 만들어야 하는 경우 Bynder 지원 팀에 문의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-211">If you need to create an user manually, you need to contact the Bynder support team.</span></span> 
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="1dc5e-212">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="1dc5e-212">Assign the Azure AD test user</span></span>
<span data-ttu-id="1dc5e-213">이 섹션은 Britta Simon에게 Bynder에 대한 액세스 권한을 부여하여 Azure SSO를 사용할 수 있도록 하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-213">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Bynder.</span></span>

   ![사용자 할당][200]

<span data-ttu-id="1dc5e-215">**Britta Simon을 Bynder에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="1dc5e-215">**To assign Britta Simon to Bynder, perform the following steps:**</span></span>

1. <span data-ttu-id="1dc5e-216">클래식 포털에서 응용 프로그램 보기를 열려면 디렉터리 보기의 최상위 메뉴에서 **응용 프로그램** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-216">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![사용자 할당][201]
2. <span data-ttu-id="1dc5e-218">응용 프로그램 목록에서 **Bynder**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-218">In the applications list, select **Bynder**.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_50.png)
3. <span data-ttu-id="1dc5e-220">위쪽의 메뉴에서 **사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-220">In the menu on the top, click **Users**.</span></span>
   
    ![사용자 할당][203]
4. <span data-ttu-id="1dc5e-222">사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-222">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="1dc5e-223">아래쪽 도구 모음에서 **할당**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-223">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![사용자 할당][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="1dc5e-225">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="1dc5e-225">Test single sign-on</span></span>
<span data-ttu-id="1dc5e-226">이 섹션은 액세스 패널을 사용하여 Microsoft Azure AD SSO 구성을 테스트하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-226">The objective of this section is to test your Microsoft Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="1dc5e-227">액세스 패널에서 Bynder 타일을 클릭하면 Bynder 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5e-227">When you click the Bynder tile in the Access Panel, you should get automatically signed-on to your Bynder application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1dc5e-228">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="1dc5e-228">Additional resources</span></span>
* [<span data-ttu-id="1dc5e-229">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="1dc5e-229">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1dc5e-230">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="1dc5e-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_205.png
