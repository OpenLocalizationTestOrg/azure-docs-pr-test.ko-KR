---
title: "자습서: Splunk Enterprise and Splunk Cloud와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory 및 Splunk Enterprise and Splunk Cloud 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b3e2b4a9-749c-4895-813d-db46f8dfdbf8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/09/2017
ms.author: jeedes
ms.openlocfilehash: b78e9b7161207a74880e912241d5e965b353d1c5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-splunk-enterprise-and-splunk-cloud"></a><span data-ttu-id="3e01b-103">자습서: Splunk Enterprise and Splunk Cloud와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="3e01b-103">Tutorial: Azure Active Directory integration with Splunk Enterprise and Splunk Cloud</span></span>

<span data-ttu-id="3e01b-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Splunk Enterprise and Splunk Cloud를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="3e01b-104">In this tutorial, you learn how to integrate Splunk Enterprise and Splunk Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3e01b-105">Splunk Enterprise and Splunk Cloud를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e01b-105">Integrating Splunk Enterprise and Splunk Cloud with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3e01b-106">Azure AD에서 사용자의 Splunk Enterprise and Splunk Cloud에 대한 액세스 권한을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e01b-106">You can control in Azure AD who has access to Splunk Enterprise and Splunk Cloud</span></span>
- <span data-ttu-id="3e01b-107">사용자가 해당 Azure AD 계정으로 Splunk Enterprise and Splunk Cloud SSO(Single Sign-On)에 자동으로 로그온되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e01b-107">You can enable your users to automatically get signed-on to Splunk Enterprise and Splunk Cloud single sign-on (SSO) with their Azure AD accounts</span></span>
- <span data-ttu-id="3e01b-108">단일 중앙 위치인 Azure 클래식 포털에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e01b-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="3e01b-109">Azure AD와의 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory를 사용한 응용 프로그램 액세스 및 Single Sign-On](active-directory-appssoaccess-whatis.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3e01b-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3e01b-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="3e01b-110">Prerequisites</span></span>

<span data-ttu-id="3e01b-111">Splunk Enterprise and Splunk Cloud와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3e01b-111">To configure Azure AD integration with Splunk Enterprise and Splunk Cloud, you need the following items:</span></span>

- <span data-ttu-id="3e01b-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="3e01b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3e01b-113">Splunk Enterprise and Splunk Cloud SSO가 사용하도록 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="3e01b-113">A Splunk Enterprise or Splunk Cloud SSO enabled subscription</span></span>


>[!NOTE]
><span data-ttu-id="3e01b-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3e01b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
>

<span data-ttu-id="3e01b-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e01b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3e01b-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e01b-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="3e01b-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e01b-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="3e01b-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="3e01b-118">Scenario description</span></span>
<span data-ttu-id="3e01b-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e01b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="3e01b-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e01b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3e01b-121">갤러리에서 Splunk Enterprise and Splunk Cloud 추가</span><span class="sxs-lookup"><span data-stu-id="3e01b-121">Adding Splunk Enterprise and Splunk Cloud from the gallery</span></span>
2. <span data-ttu-id="3e01b-122">Azure AD SSO 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="3e01b-122">Configuring and testing Azure AD SSO</span></span>


## <a name="add-splunk-enterprise-and-splunk-cloud-from-the-gallery"></a><span data-ttu-id="3e01b-123">갤러리에서 Splunk Enterprise and Splunk Cloud 추가</span><span class="sxs-lookup"><span data-stu-id="3e01b-123">Add Splunk Enterprise and Splunk Cloud from the gallery</span></span>
<span data-ttu-id="3e01b-124">Splunk Enterprise and Splunk Cloud의 Azure AD 통합을 구성하려면 갤러리의 Splunk Enterprise and Splunk Cloud를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e01b-124">To configure the integration of Splunk Enterprise and Splunk Cloud into Azure AD, you need to add Splunk Enterprise and Splunk Cloud from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3e01b-125">**갤러리에서 Splunk Enterprise and Splunk Cloud를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="3e01b-125">**To add Splunk Enterprise and Splunk Cloud from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3e01b-126">**Azure 클래식 포털**의 왼쪽 탐색 창에서 **Active Directory**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3e01b-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>

    ![Active Directory][1]

2. <span data-ttu-id="3e01b-128">**디렉터리** 목록에서 디렉터리 통합을 사용하도록 설정할 디렉터리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3e01b-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="3e01b-129">응용 프로그램 보기를 열려면 디렉터리 보기의 최상위 메뉴에서 **응용 프로그램** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3e01b-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![응용 프로그램][2]

4. <span data-ttu-id="3e01b-131">페이지 맨 아래에 있는 **추가** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3e01b-131">Click **Add** at the bottom of the page.</span></span>

    ![응용 프로그램][3]

5. <span data-ttu-id="3e01b-133">**수행할 작업** 대화 상자에서 **갤러리에서 응용 프로그램 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3e01b-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>

    ![응용 프로그램][4]

6. <span data-ttu-id="3e01b-135">검색 상자에 **Splunk Enterprise or Splunk Cloud**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3e01b-135">In the search box, type **Splunk Enterprise or Splunk Cloud**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_01.png)

7. <span data-ttu-id="3e01b-137">결과 창에서 **Splunk Enterprise and Splunk Cloud**를 선택하고 **완료**를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3e01b-137">In the results pane, select **Splunk Enterprise and Splunk Cloud**, and then click **Complete** to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_02.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="3e01b-139">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="3e01b-139">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="3e01b-140">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Splunk Enterprise and Splunk Cloud에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="3e01b-140">In this section, you configure and test Azure AD single sign-on with Splunk Enterprise and Splunk Cloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3e01b-141">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Splunk Enterprise and Splunk Cloud 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e01b-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Splunk Enterprise and Splunk Cloud is to a user in Azure AD.</span></span> <span data-ttu-id="3e01b-142">즉, Azure AD 사용자와 Splunk Enterprise and Splunk Cloud의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e01b-142">In other words, a link relationship between an Azure AD user and the related user in Splunk Enterprise and Splunk Cloud needs to be established.</span></span>

<span data-ttu-id="3e01b-143">이 연결 관계는 Azure AD의 **사용자 이름** 값을 Splunk Enterprise and Splunk Cloud의 **Username** 값으로 할당하여 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3e01b-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Splunk Enterprise and Splunk Cloud.</span></span>

<span data-ttu-id="3e01b-144">Splunk Enterprise and Splunk Cloud에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e01b-144">To configure and test Azure AD single sign-on with Splunk Enterprise and Splunk Cloud, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3e01b-145">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e01b-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3e01b-146">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3e01b-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3e01b-147">**[Splunk Enterprise and Splunk Cloud 테스트 사용자 만들기](#creating-a-splunk-enterprise-and-splunk-cloud-test-user)** - Britta Simon의 Azure AD 표현과 연결되는 대응 사용자를 Splunk Enterprise and Splunk Cloud에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3e01b-147">**[Creating a Splunk Enterprise and Splunk Cloud test user](#creating-a-splunk-enterprise-and-splunk-cloud-test-user)** - to have a counterpart of Britta Simon in Splunk Enterprise and Splunk Cloud that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="3e01b-148">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e01b-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3e01b-149">**[Single Sign-On 테스트](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3e01b-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="3e01b-150">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="3e01b-150">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="3e01b-151">이 섹션에서는 클래식 포털에서 Azure AD SSO를 사용하도록 설정하고 Splunk Enterprise and Splunk Cloud 응용 프로그램에서 SSO를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="3e01b-151">In this section, you enable Azure AD SSO in the classic portal and configure SSO in your Splunk Enterprise and Splunk Cloud application.</span></span>


<span data-ttu-id="3e01b-152">**Splunk Enterprise and Splunk Cloud에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="3e01b-152">**To configure Azure AD single sign-on with Splunk Enterprise and Splunk Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="3e01b-153">클래식 포털의 **Splunk Enterprise and Splunk Cloud** 응용 프로그램 통합 페이지에서 **Single Sign-On 구성**을 클릭하여 **Single Sign-On 구성** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3e01b-153">In the classic portal, on the **Splunk Enterprise and Splunk Cloud** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
     
    ![Single Sign-on 구성][6] 

2. <span data-ttu-id="3e01b-155">**Splunk Enterprise and Splunk Cloud에 대한 사용자 로그온 방법을 선택하십시오.** 페이지에서 **Azure AD Single Sign-On**을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3e01b-155">On the **How would you like users to sign on to Splunk Enterprise and Splunk Cloud** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_03.png) 

3. <span data-ttu-id="3e01b-157">**앱 설정 구성** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3e01b-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_04.png) 
  1. <span data-ttu-id="3e01b-159">**로그인 URL** 텍스트 상자에서 `https://<splunkserverUrl>/en-US/app/launcher/home` 패턴으로 사용자가 Splunk Enterprise and Splunk Cloud 응용 프로그램에 로그인하는 데 사용하는 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3e01b-159">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Splunk Enterprise and Splunk Cloud application using the following pattern: `https://<splunkserverUrl>/en-US/app/launcher/home`</span></span>
  2. <span data-ttu-id="3e01b-160">**식별자** 텍스트 상자에 Splunk Server의 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3e01b-160">In the **Identifier** textbox, type the URL of your Splunk Server.</span></span>
  3. <span data-ttu-id="3e01b-161">**회신 URL** 텍스트 상자에 다음 패턴으로 URL을 입력합니다. `https://<splunkserver>/saml/acs`</span><span class="sxs-lookup"><span data-stu-id="3e01b-161">In the **Reply URL** textbox, type the URL with the following pattern: `https://<splunkserver>/saml/acs`</span></span>
  4. <span data-ttu-id="3e01b-162">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="3e01b-162">Click **Next**.</span></span>
 
4. <span data-ttu-id="3e01b-163">**Splunk Enterprise and Splunk Cloud에서 Azure AD Single Sign-on 구성** 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3e01b-163">On the **Configure single sign-on at Splunk Enterprise and Splunk Cloud** page, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_05.png)
  1. <span data-ttu-id="3e01b-165">**메타데이터 다운로드**를 클릭하고 파일을 컴퓨터에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="3e01b-165">Click **Download metadata**, and then save the file on your computer.</span></span>
  2. <span data-ttu-id="3e01b-166">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="3e01b-166">Click **Next**.</span></span>

5. <span data-ttu-id="3e01b-167">응용 프로그램에 대해 구성된 SSO를 얻으려면 Splunk Enterprise and Splunk Cloud 지원 팀에 문의하고 다음을 제공하세요.</span><span class="sxs-lookup"><span data-stu-id="3e01b-167">To get SSO configured for your application, contact Splunk Enterprise and Splunk Cloud support team and provide them with the following:</span></span>

    * <span data-ttu-id="3e01b-168">다운로드한 **페더레이션 메타데이터**</span><span class="sxs-lookup"><span data-stu-id="3e01b-168">The downloaded **federaton metadata**</span></span>
6. <span data-ttu-id="3e01b-169">클래식 포털에서 Single Sign-On 구성 확인을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3e01b-169">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
    
    ![Azure AD Single Sign-On][10]

7. <span data-ttu-id="3e01b-171">**Single Sign-On 확인** 페이지에서 **완료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3e01b-171">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
 
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="3e01b-173">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="3e01b-173">Create an Azure AD test user</span></span>
<span data-ttu-id="3e01b-174">이 섹션에서는 클래식 포털에서 Britta Simon이라는 테스트 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3e01b-174">In this section, you create a test user in the classic portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][20]

<span data-ttu-id="3e01b-176">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="3e01b-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3e01b-177">**Azure 클래식 포털**의 왼쪽 탐색 창에서 **Active Directory**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3e01b-177">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="3e01b-179">**디렉터리** 목록에서 디렉터리 통합을 사용하도록 설정할 디렉터리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3e01b-179">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="3e01b-180">사용자 목록을 표시하려면 위쪽 메뉴에서 **사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3e01b-180">To display the list of users, in the menu on the top, click **Users**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3e01b-182">**사용자 추가** 대화 상자를 열려면 아래쪽 도구 모음에서 **사용자 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3e01b-182">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="3e01b-184">**이 사용자에 대한 정보 입력** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3e01b-184">On the **Tell us about this user** dialog page, perform the following steps:</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_05.png) 
  1. <span data-ttu-id="3e01b-186">사용자 유형에서 조직의 새 사용자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3e01b-186">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="3e01b-187">사용자 이름 **텍스트 상자**에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3e01b-187">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="3e01b-188">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="3e01b-188">Click **Next**.</span></span>

6.  <span data-ttu-id="3e01b-189">**사용자 프로필** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3e01b-189">On the **User Profile** dialog page, perform the following steps:</span></span>
  
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_06.png) 
  1. <span data-ttu-id="3e01b-191">**이름** 텍스트 상자에 **Britta**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3e01b-191">In the **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="3e01b-192">**성** 텍스트 상자에 **Simon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3e01b-192">In the **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="3e01b-193">**표시 이름** 텍스트 상자에 **Britta Simon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3e01b-193">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="3e01b-194">**역할** 목록에서 **사용자**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3e01b-194">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="3e01b-195">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="3e01b-195">Click **Next**.</span></span>

7. <span data-ttu-id="3e01b-196">**임시 암호 가져오기** 대화 상자 페이지에서 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3e01b-196">On the **Get temporary password** dialog page, click **create**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="3e01b-198">**임시 암호 가져오기** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3e01b-198">On the **Get temporary password** dialog page, perform the following steps:</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_08.png) 
  1. <span data-ttu-id="3e01b-200">**새 암호**값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="3e01b-200">Write down the value of the **New Password**.</span></span>
  2. <span data-ttu-id="3e01b-201">**완료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3e01b-201">Click **Complete**.</span></span>   

### <a name="create-a-splunk-enterprise-and-splunk-cloud-test-user"></a><span data-ttu-id="3e01b-202">Splunk Enterprise and Splunk Cloud 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="3e01b-202">Create a Splunk Enterprise and Splunk Cloud test user</span></span>

<span data-ttu-id="3e01b-203">이 섹션에서는 Splunk Enterprise and Splunk Cloud에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3e01b-203">In this section, you create a user called Britta Simon in Splunk Enterprise and Splunk Cloud.</span></span> <span data-ttu-id="3e01b-204">Splunk Enterprise and Splunk Cloud 지원 팀과 협의하여 Splunk Enterprise and Splunk Cloud 플랫폼에 사용자를 추가하세요.</span><span class="sxs-lookup"><span data-stu-id="3e01b-204">Please work with Splunk Enterprise and Splunk Cloud support team to add the users in the Splunk Enterprise and Splunk Cloud platform.</span></span>


### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="3e01b-205">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="3e01b-205">Assign the Azure AD test user</span></span>

<span data-ttu-id="3e01b-206">이 섹션에서는 Azure SSO를 사용할 수 있도록 Britta Simon에게 Splunk Enterprise and Splunk Cloud에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="3e01b-206">In this section, you enable Britta Simon to use Azure SSOy granting her access to Splunk Enterprise and Splunk Cloud.</span></span>

![사용자 할당][200] 

<span data-ttu-id="3e01b-208">**Splunk Enterprise and Splunk Cloud에 Britta Simon을 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="3e01b-208">**To assign Britta Simon to Splunk Enterprise and Splunk Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="3e01b-209">클래식 포털에서 응용 프로그램 보기를 열려면 디렉터리 보기의 최상위 메뉴에서 **응용 프로그램** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3e01b-209">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="3e01b-211">응용 프로그램 목록에서 **Splunk Enterprise and Splunk Cloud**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3e01b-211">In the applications list, select **Splunk Enterprise and Splunk Cloud**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_50.png) 

3. <span data-ttu-id="3e01b-213">위쪽의 메뉴에서 **사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3e01b-213">In the menu on the top, click **Users**.</span></span>

    ![사용자 할당][203]

4. <span data-ttu-id="3e01b-215">사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3e01b-215">In the Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="3e01b-216">아래쪽 도구 모음에서 **할당**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3e01b-216">In the toolbar on the bottom, click **Assign**.</span></span>

    ![사용자 할당][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="3e01b-218">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="3e01b-218">Test single sign-on</span></span>

<span data-ttu-id="3e01b-219">이 섹션에서는 액세스 패널을 사용하여 Azure AD SSO 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="3e01b-219">In this section, you test your Azure AD SSOonfiguration using the Access Panel.</span></span>

<span data-ttu-id="3e01b-220">액세스 패널에서 Splunk Enterprise and Splunk Cloud 타일을 클릭하면 Splunk Enterprise and Splunk Cloud 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e01b-220">When you click the Splunk Enterprise and Splunk Cloud tile in the Access Panel, you should get automatically signed-on to your Splunk Enterprise and Splunk Cloud application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="3e01b-221">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="3e01b-221">Additional resources</span></span>

* [<span data-ttu-id="3e01b-222">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="3e01b-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3e01b-223">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="3e01b-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_205.png
