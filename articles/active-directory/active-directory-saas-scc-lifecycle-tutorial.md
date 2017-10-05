---
title: "자습서: SCC LifeCycle과 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory에서 SCC LifeCycle를 사용하여 Single Sign-On, 자동화된 프로비전 등을 사용하도록 설정하는 방법을 알아봅니다."
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 9748bf38-ffc3-4d51-a1ae-207ce57104fa
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: 9a30bcca720ff135d0180d73f46e78403e9bca43
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-scc-lifecycle"></a><span data-ttu-id="83670-103">자습서: SCC LifeCycle과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="83670-103">Tutorial: Azure Active Directory integration with SCC LifeCycle</span></span>
<span data-ttu-id="83670-104">이 자습서는 Azure와 SCC LifeCycle의 통합을 보여주기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="83670-104">The objective of this tutorial is to show the integration of Azure and SCC LifeCycle.</span></span>  

<span data-ttu-id="83670-105">이 자습서에 설명된 시나리오에서는 사용자에게 이미 다음 항목이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="83670-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="83670-106">유효한 Azure 구독</span><span class="sxs-lookup"><span data-stu-id="83670-106">A valid Azure subscription</span></span>
* <span data-ttu-id="83670-107">SCC LifeCycle SSO(Single Sign-On)가 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="83670-107">A SCC LifeCycle single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="83670-108">이 자습서를 완료한 후 SCC LifeCycle에 할당한 Azure AD 사용자가 SCC LifeCycle 회사 사이트(서비스 공급자가 시작한 로그온)에서 또는 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 사용하여 응용 프로그램에 Single Sign-On할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83670-108">After completing this tutorial, the Azure AD users you have assigned to SCC LifeCycle will be able to single sign into the application at your SCC LifeCycle company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="83670-109">이 자습서에 설명된 시나리오는 다음 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83670-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="83670-110">SCC LifeCycle에 응용 프로그램 통합 사용</span><span class="sxs-lookup"><span data-stu-id="83670-110">Enabling the application integration for SCC LifeCycle</span></span>
2. <span data-ttu-id="83670-111">SSO(Single Sign-On) 구성</span><span class="sxs-lookup"><span data-stu-id="83670-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="83670-112">사용자 프로비전 구성</span><span class="sxs-lookup"><span data-stu-id="83670-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="83670-113">사용자 할당</span><span class="sxs-lookup"><span data-stu-id="83670-113">Assigning users</span></span>

<span data-ttu-id="83670-114">![시나리오](./media/active-directory-saas-scc-lifecycle-tutorial/IC794120.png "시나리오")</span><span class="sxs-lookup"><span data-stu-id="83670-114">![Scenario](./media/active-directory-saas-scc-lifecycle-tutorial/IC794120.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-scc-lifecycle"></a><span data-ttu-id="83670-115">SCC LifeCycle에 응용 프로그램 통합 사용</span><span class="sxs-lookup"><span data-stu-id="83670-115">Enable the application integration for SCC LifeCycle</span></span>
<span data-ttu-id="83670-116">이 섹션은 SCC LifeCycle에 응용 프로그램 통합을 사용하도록 설정하는 방법을 간략하게 설명하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="83670-116">The objective of this section is to outline how to enable the application integration for SCC LifeCycle.</span></span>

<span data-ttu-id="83670-117">**SCC LifeCycle에 응용 프로그램 통합을 사용하도록 설정하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="83670-117">**To enable the application integration for SCC LifeCycle, perform the following steps:**</span></span>

1. <span data-ttu-id="83670-118">Azure 클래식 포털의 왼쪽 탐색 창에서 **Active Directory**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="83670-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="83670-119">![Active Directory](./media/active-directory-saas-scc-lifecycle-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="83670-119">![Active Directory](./media/active-directory-saas-scc-lifecycle-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="83670-120">**디렉터리** 목록에서 디렉터리 통합을 사용하도록 설정할 디렉터리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="83670-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="83670-121">응용 프로그램 보기를 열려면 디렉터리 보기의 최상위 메뉴에서 **응용 프로그램** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="83670-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="83670-122">![응용 프로그램](./media/active-directory-saas-scc-lifecycle-tutorial/IC700994.png "응용 프로그램")</span><span class="sxs-lookup"><span data-stu-id="83670-122">![Applications](./media/active-directory-saas-scc-lifecycle-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="83670-123">페이지 맨 아래에 있는 **추가** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="83670-123">Click **Add** at the bottom of the page.</span></span>
   
    <span data-ttu-id="83670-124">![응용 프로그램 추가](./media/active-directory-saas-scc-lifecycle-tutorial/IC749321.png "응용 프로그램 추가")</span><span class="sxs-lookup"><span data-stu-id="83670-124">![Add application](./media/active-directory-saas-scc-lifecycle-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="83670-125">**수행할 작업** 대화 상자에서 **갤러리에서 응용 프로그램 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="83670-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    <span data-ttu-id="83670-126">![갤러리에서 응용 프로그램 추가](./media/active-directory-saas-scc-lifecycle-tutorial/IC749322.png "갤러리에서 응용 프로그램 추가")</span><span class="sxs-lookup"><span data-stu-id="83670-126">![Add an application from gallerry](./media/active-directory-saas-scc-lifecycle-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="83670-127">**검색 상자**에 **SCC LifeCycle**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="83670-127">In the **search box**, type **SCC LifeCycle**.</span></span>
   
    <span data-ttu-id="83670-128">![응용 프로그램 갤러리](./media/active-directory-saas-scc-lifecycle-tutorial/IC794121.png "응용 프로그램 갤러리")</span><span class="sxs-lookup"><span data-stu-id="83670-128">![Application Gallery](./media/active-directory-saas-scc-lifecycle-tutorial/IC794121.png "Application Gallery")</span></span>
7. <span data-ttu-id="83670-129">결과 창에서 **SCC LifeCycle**를 선택하고 **완료**를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="83670-129">In the results pane, select **SCC LifeCycle**, and then click **Complete** to add the application.</span></span>
   
    <span data-ttu-id="83670-130">![SCC LifeCycle](./media/active-directory-saas-scc-lifecycle-tutorial/IC795082.png "SCC LifeCycle")</span><span class="sxs-lookup"><span data-stu-id="83670-130">![SCC LifeCycle](./media/active-directory-saas-scc-lifecycle-tutorial/IC795082.png "SCC LifeCycle")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="83670-131">Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="83670-131">Configure single sign-on</span></span>

<span data-ttu-id="83670-132">이 섹션은 사용자가 SAML 프로토콜 기반 페더레이션을 사용하여 Azure AD의 계정으로 SCC LifeCycle에 인증할 수 있게 하는 방법을 간략하게 설명하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="83670-132">The objective of this section is to outline how to enable users to authenticate to SCC LifeCycle with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="83670-133">**Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="83670-133">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="83670-134">Azure 클래식 포털의 **SCC LifeCycle** 응용 프로그램 통합 페이지에서 **Single Sign-On 구성**을 클릭하여 **Single Sign-On 구성 ** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="83670-134">In the Azure classic portal, on the **SCC LifeCycle** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On ** dialog.</span></span>
   
    <span data-ttu-id="83670-135">![Single Sign-On 구성](./media/active-directory-saas-scc-lifecycle-tutorial/IC794122.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="83670-135">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC794122.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="83670-136">**SCC LifeCycle에 대한 사용자 로그온 방법 선택** 페이지에서 **Microsoft Azure AD Single Sign-On**을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="83670-136">On the **How would you like users to sign on to SCC LifeCycle** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="83670-137">![Single Sign-On 구성](./media/active-directory-saas-scc-lifecycle-tutorial/IC794123.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="83670-137">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC794123.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="83670-138">**앱 URL 구성** 페이지의 **로그온 URL** 텍스트 상자에 다음 패턴 “*https://bs1.scc.com/lc7/welcome/customer/PICTtest.aspx*”을 사용하여 SCC LifeCycle 응용 프로그램에 로그온하기 위해 사용자가 사용한 URL을 입력한 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="83670-138">On the **Configure App URL** page, in the **Sign On URL** textbox, type the URL used by your users to sign on to your SCC LifeCycle application using the following pattern "*https://bs1.scc.com/lc7/welcome/customer/PICTtest.aspx*", and then click **Next**.</span></span>
   
    <span data-ttu-id="83670-139">![앱 URL 구성](./media/active-directory-saas-scc-lifecycle-tutorial/IC794124.png "앱 URL 구성")</span><span class="sxs-lookup"><span data-stu-id="83670-139">![Configure App URL](./media/active-directory-saas-scc-lifecycle-tutorial/IC794124.png "Configure App URL")</span></span>
4. <span data-ttu-id="83670-140">**SCC LifeCycle에서 Single Sign-On 구성** 페이지에서 **메타데이터 다운로드**를 클릭한 다음 컴퓨터에 로컬로 메타데이터 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="83670-140">On the **Configure single sign-on at SCC LifeCycle** page, click **Download metadata**, and then save metadata file locally on your computer.</span></span>
   
   <span data-ttu-id="83670-141">![Single Sign-On 구성](./media/active-directory-saas-scc-lifecycle-tutorial/IC795083.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="83670-141">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC795083.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="83670-142">SCC LifeCycle 지원팀에 해당 메타데이터 파일을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="83670-142">Forward that Metadata file to SCC LifeCycle Support team.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="83670-143">Single Sign-On은 SCC LifeCycle 지원팀에서 사용할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="83670-143">Single sign-on has to be enabled by the SCC LifeCycle support team.</span></span>
   > 
   > 

6. <span data-ttu-id="83670-144">Azure 클래식 포털에서 Single Sign-On 구성 확인을 선택하고 **완료**를 클릭하여 **Single Sign-On 구성** 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="83670-144">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="83670-145">![Single Sign-On 구성](./media/active-directory-saas-scc-lifecycle-tutorial/IC794125.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="83670-145">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC794125.png "Configure Single Sign-On")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="83670-146">사용자 프로비전 구성</span><span class="sxs-lookup"><span data-stu-id="83670-146">Configure user provisioning</span></span>

<span data-ttu-id="83670-147">Azure AD 사용자가 SCC LifeCycle에 로그인할 수 있도록 하려면 SCC LifeCycle로 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="83670-147">In order to enable Azure AD users to log into SCC LifeCycle, they must be provisioned into SCC LifeCycle.</span></span> <span data-ttu-id="83670-148">SCC LifeCycle를 프로비전하는 사용자를 구성할 작업 항목이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="83670-148">There is no action item for you to configure user provisioning to SCC LifeCycle.</span></span>

<span data-ttu-id="83670-149">할당된 사용자가 SCC LifeCycle에 로그인하려고 하는 경우, 필요하면 SCC LifeCycle 계정이 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="83670-149">When an assigned user tries to log into SCC LifeCycle, an SCC LifeCycle account is automatically created if necessary.</span></span>

>[!NOTE]
><span data-ttu-id="83670-150">다른 SCC LifeCycle 사용자 계정 생성 도구 또는 SCC LifeCycle이 제공한 API를 사용하여 AAD 사용자 계정을 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83670-150">You can use any other SCC LifeCycle user account creation tools or APIs provided by SCC LifeCycle to provision AAD user accounts.</span></span>
> 
> 

## <a name="assign-users"></a><span data-ttu-id="83670-151">사용자 할당</span><span class="sxs-lookup"><span data-stu-id="83670-151">Assign users</span></span>
<span data-ttu-id="83670-152">구성을 테스트하려면 응용 프로그램 사용을 허용하려는 Azure AD 사용자를 할당하여 액세스 권한을 부여해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="83670-152">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="83670-153">**SCC LifeCycle에 사용자를 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="83670-153">**To assign users to SCC LifeCycle, perform the following steps:**</span></span>

1. <span data-ttu-id="83670-154">Azure 클래식 포털에서 테스트 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="83670-154">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="83670-155">**SCC LifeCycle **응용 프로그램 통합 페이지에서 **사용자 할당**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="83670-155">On the **SCC LifeCycle **application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="83670-156">![사용자 할당](./media/active-directory-saas-scc-lifecycle-tutorial/IC794126.png "사용자 할당")</span><span class="sxs-lookup"><span data-stu-id="83670-156">![Assign Users](./media/active-directory-saas-scc-lifecycle-tutorial/IC794126.png "Assign Users")</span></span>
3. <span data-ttu-id="83670-157">테스트 사용자를 선택하고 **할당**을 클릭한 다음 **예**를 클릭하여 할당을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="83670-157">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
    <span data-ttu-id="83670-158">![예](./media/active-directory-saas-scc-lifecycle-tutorial/IC767830.png "예")</span><span class="sxs-lookup"><span data-stu-id="83670-158">![Yes](./media/active-directory-saas-scc-lifecycle-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="83670-159">SSO 설정을 테스트하려면 액세스 패널을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="83670-159">If you want to test your SSO settings, open the Access Panel.</span></span> <span data-ttu-id="83670-160">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="83670-160">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

