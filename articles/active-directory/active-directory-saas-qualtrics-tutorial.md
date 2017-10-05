---
title: "자습서: Qualtrics와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory에서 Qualtrics를 사용하여 Single Sign-On, 자동화된 프로비전 등을 사용하도록 설정하는 방법을 알아봅니다."
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 4df889ab-2685-4d15-a163-1ba26567eeda
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: 2fcde595a40dafda7549f5bccb582b57585b314e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-qualtrics"></a><span data-ttu-id="2fa05-103">자습서: Qualtrics와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="2fa05-103">Tutorial: Azure Active Directory integration with Qualtrics</span></span>
<span data-ttu-id="2fa05-104">이 자습서는 Azure 및 Qualtrics의 통합을 보여주기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2fa05-104">The objective of this tutorial is to show the integration of Azure and Qualtrics.</span></span>  

<span data-ttu-id="2fa05-105">이 자습서에 설명된 시나리오에서는 사용자에게 이미 다음 항목이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="2fa05-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="2fa05-106">유효한 Azure 구독</span><span class="sxs-lookup"><span data-stu-id="2fa05-106">A valid Azure subscription</span></span>
* <span data-ttu-id="2fa05-107">Qualtrics SSO(Single Sign-On)가 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="2fa05-107">A Qualtrics single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="2fa05-108">이 자습서를 완료한 후 Qualtrics에 할당한 Azure AD 사용자가 Qualtrics 회사 사이트(서비스 공급자가 시작한 로그온)에서 또는 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 사용하여 응용 프로그램에 Single Sign-On할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fa05-108">After completing this tutorial, the Azure AD users you have assigned to Qualtrics will be able to single sign into the application at your Qualtrics company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="2fa05-109">이 자습서에 설명된 시나리오는 다음 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fa05-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="2fa05-110">Qualtrics에 응용 프로그램 통합 사용</span><span class="sxs-lookup"><span data-stu-id="2fa05-110">Enabling the application integration for Qualtrics</span></span>
2. <span data-ttu-id="2fa05-111">SSO(Single Sign-On) 구성</span><span class="sxs-lookup"><span data-stu-id="2fa05-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="2fa05-112">사용자 프로비전 구성</span><span class="sxs-lookup"><span data-stu-id="2fa05-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="2fa05-113">사용자 할당</span><span class="sxs-lookup"><span data-stu-id="2fa05-113">Assigning users</span></span>

<span data-ttu-id="2fa05-114">![시나리오](./media/active-directory-saas-qualtrics-tutorial/IC789542.png "시나리오")</span><span class="sxs-lookup"><span data-stu-id="2fa05-114">![Scenario](./media/active-directory-saas-qualtrics-tutorial/IC789542.png "Scenario")</span></span>

## <a name="enabling-the-application-integration-for-qualtrics"></a><span data-ttu-id="2fa05-115">Qualtrics에 응용 프로그램 통합 사용</span><span class="sxs-lookup"><span data-stu-id="2fa05-115">Enabling the application integration for Qualtrics</span></span>
<span data-ttu-id="2fa05-116">이 섹션은 Qualtrics에 응용 프로그램 통합을 사용하도록 설정하는 방법을 간략하게 설명하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2fa05-116">The objective of this section is to outline how to enable the application integration for Qualtrics.</span></span>

<span data-ttu-id="2fa05-117">**Qualtrics에 응용 프로그램 통합을 사용하도록 설정하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="2fa05-117">**To enable the application integration for Qualtrics, perform the following steps:**</span></span>

1. <span data-ttu-id="2fa05-118">Azure 클래식 포털의 왼쪽 탐색 창에서 **Active Directory**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2fa05-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="2fa05-119">![Active Directory](./media/active-directory-saas-qualtrics-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="2fa05-119">![Active Directory](./media/active-directory-saas-qualtrics-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="2fa05-120">**디렉터리** 목록에서 디렉터리 통합을 사용하도록 설정할 디렉터리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2fa05-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="2fa05-121">응용 프로그램 보기를 열려면 디렉터리 보기의 최상위 메뉴에서 **응용 프로그램** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2fa05-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="2fa05-122">![응용 프로그램](./media/active-directory-saas-qualtrics-tutorial/IC700994.png "응용 프로그램")</span><span class="sxs-lookup"><span data-stu-id="2fa05-122">![Applications](./media/active-directory-saas-qualtrics-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="2fa05-123">페이지 맨 아래에 있는 **추가** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2fa05-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="2fa05-124">![응용 프로그램 추가](./media/active-directory-saas-qualtrics-tutorial/IC749321.png "응용 프로그램 추가")</span><span class="sxs-lookup"><span data-stu-id="2fa05-124">![Add application](./media/active-directory-saas-qualtrics-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="2fa05-125">**수행할 작업** 대화 상자에서 **갤러리에서 응용 프로그램 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2fa05-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="2fa05-126">![갤러리에서 응용 프로그램 추가](./media/active-directory-saas-qualtrics-tutorial/IC749322.png "갤러리에서 응용 프로그램 추가")</span><span class="sxs-lookup"><span data-stu-id="2fa05-126">![Add an application from gallerry](./media/active-directory-saas-qualtrics-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="2fa05-127">**검색 상자**에 **Qualtrics**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2fa05-127">In the **search box**, type **Qualtrics**.</span></span>
   
   <span data-ttu-id="2fa05-128">![응용 프로그램 갤러리](./media/active-directory-saas-qualtrics-tutorial/IC789543.png "응용 프로그램 갤러리")</span><span class="sxs-lookup"><span data-stu-id="2fa05-128">![Application Gallery](./media/active-directory-saas-qualtrics-tutorial/IC789543.png "Application Gallery")</span></span>
7. <span data-ttu-id="2fa05-129">결과 창에서 **Qualtrics**를 선택하고 **완료**를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2fa05-129">In the results pane, select **Qualtrics**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="2fa05-130">![Qualtrics](./media/active-directory-saas-qualtrics-tutorial/IC789544.png "Qualtrics")</span><span class="sxs-lookup"><span data-stu-id="2fa05-130">![Qualtrics](./media/active-directory-saas-qualtrics-tutorial/IC789544.png "Qualtrics")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="2fa05-131">Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="2fa05-131">Configure single sign-on</span></span>

<span data-ttu-id="2fa05-132">이 섹션은 사용자가 SAML 프로토콜 기반 페더레이션을 사용하여 Azure AD의 계정으로 Qualtrics에 인증할 수 있게 하는 방법을 간략하게 설명하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2fa05-132">The objective of this section is to outline how to enable users to authenticate to Qualtrics with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="2fa05-133">**Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="2fa05-133">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="2fa05-134">Azure 클래식 포털의 **Qualtrics** 응용 프로그램 통합 페이지에서 **Single Sign-On 구성**을 클릭하여 **Single Sign-On 구성** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2fa05-134">In the Azure classic portal, on the **Qualtrics** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="2fa05-135">![Single Sign-On 구성](./media/active-directory-saas-qualtrics-tutorial/IC789545.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="2fa05-135">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789545.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="2fa05-136">**Qualtrics에 대한 사용자 로그온 방법 선택** 페이지에서 **Microsoft Azure AD Single Sign-On**을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2fa05-136">On the **How would you like users to sign on to Qualtrics** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="2fa05-137">![Single Sign-On 구성](./media/active-directory-saas-qualtrics-tutorial/IC789546.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="2fa05-137">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789546.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="2fa05-138">**앱 URL 구성** 페이지의 **Qualtrics 로그온 URL** 텍스트 상자에 URL(예: “*https://ssotest2ut1.qualtrics.com*”)을 입력한 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2fa05-138">On the **Configure App URL** page, in the **Qualtrics Sign On URL** textbox, type your URL (e.g.: “*https://ssotest2ut1.qualtrics.com*"), and then click **Next**.</span></span>
   
   <span data-ttu-id="2fa05-139">![앱 URL 구성](./media/active-directory-saas-qualtrics-tutorial/IC789547.png "앱 URL 구성")</span><span class="sxs-lookup"><span data-stu-id="2fa05-139">![Configure App URL](./media/active-directory-saas-qualtrics-tutorial/IC789547.png "Configure App URL")</span></span>
4. <span data-ttu-id="2fa05-140">**Qualtrics에서 Single Sign-On 구성** 페이지에서 **메타데이터 다운로드**를 클릭한 다음 컴퓨터에 메타데이터 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="2fa05-140">On the **Configure single sign-on at Qualtrics** page, click **Download metadata**, and then save the metadata file on your computer.</span></span>
   
   <span data-ttu-id="2fa05-141">![Single Sign-On 구성](./media/active-directory-saas-qualtrics-tutorial/IC789548.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="2fa05-141">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789548.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="2fa05-142">메타데이터를 Qualtrics 지원팀에 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="2fa05-142">Send the metadata file to the Qualtrics support team.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="2fa05-143">SSO 구성을 Qualtrics 지원팀에서 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fa05-143">The SSO configuration has to be performed by the Qualtrics support team.</span></span> <span data-ttu-id="2fa05-144">구성이 완료되는 즉시 알림을 받아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fa05-144">You will get a notification as soon as the configuration has been completed.</span></span>
   > 
   > 
6. <span data-ttu-id="2fa05-145">Azure 클래식 포털에서 Single Sign-On 구성 확인을 선택하고 **완료**를 클릭하여 **Single Sign-On 구성** 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="2fa05-145">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="2fa05-146">![Single Sign-On 구성](./media/active-directory-saas-qualtrics-tutorial/IC789549.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="2fa05-146">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789549.png "Configure Single Sign-On")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="2fa05-147">사용자 프로비전 구성</span><span class="sxs-lookup"><span data-stu-id="2fa05-147">Configure user provisioning</span></span>

<span data-ttu-id="2fa05-148">Qualtrics를 프로비전하는 사용자를 구성할 작업 항목이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2fa05-148">There is no action item for you to configure user provisioning to Qualtrics.</span></span> <span data-ttu-id="2fa05-149">할당된 사용자가 액세스 패널을 사용하여 Qualtrics에 로그인하려는 경우 Qualtrics는 사용자가 존재하는지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2fa05-149">When an assigned user tries to log into Qualtrics using the access panel, Qualtrics checks whether the user exists.</span></span>  

<span data-ttu-id="2fa05-150">사용할 수 있는 사용자 계정이 없으면 자동으로 Qualtrics에 의해 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="2fa05-150">If there is no user account available yet, it is automatically created by Qualtrics.</span></span>

## <a name="assign-users"></a><span data-ttu-id="2fa05-151">사용자 할당</span><span class="sxs-lookup"><span data-stu-id="2fa05-151">Assign users</span></span>
<span data-ttu-id="2fa05-152">구성을 테스트하려면 응용 프로그램 사용을 허용하려는 Azure AD 사용자를 할당하여 액세스 권한을 부여해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fa05-152">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="2fa05-153">**Qualtrics에 사용자를 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="2fa05-153">**To assign users to Qualtrics, perform the following steps:**</span></span>

1. <span data-ttu-id="2fa05-154">Azure 클래식 포털에서 테스트 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2fa05-154">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="2fa05-155">**Qualtrics** 응용 프로그램 통합 페이지에서 **사용자 할당**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2fa05-155">On the **Qualtrics** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="2fa05-156">![사용자 할당](./media/active-directory-saas-qualtrics-tutorial/IC789550.png "사용자 할당")</span><span class="sxs-lookup"><span data-stu-id="2fa05-156">![Assign Users](./media/active-directory-saas-qualtrics-tutorial/IC789550.png "Assign Users")</span></span>
3. <span data-ttu-id="2fa05-157">테스트 사용자를 선택하고 **할당**을 클릭한 다음 **예**를 클릭하여 할당을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2fa05-157">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="2fa05-158">![예](./media/active-directory-saas-qualtrics-tutorial/IC767830.png "예")</span><span class="sxs-lookup"><span data-stu-id="2fa05-158">![Yes](./media/active-directory-saas-qualtrics-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="2fa05-159">SSO 설정을 테스트하려면 액세스 패널을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2fa05-159">If you want to test your SSO settings, open the Access Panel.</span></span> <span data-ttu-id="2fa05-160">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2fa05-160">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

