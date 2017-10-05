---
title: "자습서: Benefitsolver와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory에서 Benefitsolver를 사용하여 Single Sign-On, 자동화된 프로비전 등을 사용하도록 설정하는 방법을 알아봅니다."
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: cf4529b1-3fb6-4475-82b7-2ceedcb70b3c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: 8a13dd5ebd872f86247158379b28bc291a9c9d83
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-benefitsolver"></a><span data-ttu-id="4dfbc-103">자습서: Benefitsolver와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="4dfbc-103">Tutorial: Azure Active Directory integration with Benefitsolver</span></span>
<span data-ttu-id="4dfbc-104">이 자습서는 Azure 및 Benefitsolver의 통합을 보여 주기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4dfbc-104">The objective of this tutorial is to show the integration of Azure and Benefitsolver.</span></span>  

<span data-ttu-id="4dfbc-105">이 자습서에 설명된 시나리오에서는 사용자에게 이미 다음 항목이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfbc-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="4dfbc-106">유효한 Azure 구독</span><span class="sxs-lookup"><span data-stu-id="4dfbc-106">A valid Azure subscription</span></span>
* <span data-ttu-id="4dfbc-107">Benefitsolver SSO(Single Sign-On)가 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="4dfbc-107">A Benefitsolver single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="4dfbc-108">이 자습서를 완료한 후 Benefitsolver에 할당한 Azure AD 사용자가 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 사용하여 응용 프로그램에 Single Sign-On 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfbc-108">After completing this tutorial, the Azure AD users you have assigned to Benefitsolver will be able to single sign into the application using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="4dfbc-109">이 자습서에 설명된 시나리오는 다음 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfbc-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="4dfbc-110">Benefitsolver에 응용 프로그램 통합 사용</span><span class="sxs-lookup"><span data-stu-id="4dfbc-110">Enabling the application integration for Benefitsolver</span></span>
2. <span data-ttu-id="4dfbc-111">SSO(Single Sign-On) 구성</span><span class="sxs-lookup"><span data-stu-id="4dfbc-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="4dfbc-112">사용자 프로비전 구성</span><span class="sxs-lookup"><span data-stu-id="4dfbc-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="4dfbc-113">사용자 할당</span><span class="sxs-lookup"><span data-stu-id="4dfbc-113">Assigning users</span></span>

<span data-ttu-id="4dfbc-114">![시나리오](./media/active-directory-saas-benefitsolver-tutorial/IC804820.png "시나리오")</span><span class="sxs-lookup"><span data-stu-id="4dfbc-114">![Scenario](./media/active-directory-saas-benefitsolver-tutorial/IC804820.png "Scenario")</span></span>

## <a name="enabling-the-application-integration-for-benefitsolver"></a><span data-ttu-id="4dfbc-115">Benefitsolver에 응용 프로그램 통합 사용</span><span class="sxs-lookup"><span data-stu-id="4dfbc-115">Enabling the application integration for Benefitsolver</span></span>
<span data-ttu-id="4dfbc-116">이 섹션은 Benefitsolver에 응용 프로그램 통합을 사용하도록 설정하는 방법을 간략하게 설명하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4dfbc-116">The objective of this section is to outline how to enable the application integration for Benefitsolver.</span></span>

### <a name="to-enable-the-application-integration-for-benefitsolver-perform-the-following-steps"></a><span data-ttu-id="4dfbc-117">Benefitsolver에 응용 프로그램 통합을 사용하도록 설정하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfbc-117">To enable the application integration for Benefitsolver, perform the following steps:</span></span>
1. <span data-ttu-id="4dfbc-118">Azure 클래식 포털의 왼쪽 탐색 창에서 **Active Directory**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfbc-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="4dfbc-119">![Active Directory](./media/active-directory-saas-benefitsolver-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="4dfbc-119">![Active Directory](./media/active-directory-saas-benefitsolver-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="4dfbc-120">**디렉터리** 목록에서 디렉터리 통합을 사용하도록 설정할 디렉터리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfbc-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="4dfbc-121">응용 프로그램 보기를 열려면 디렉터리 보기의 최상위 메뉴에서 **응용 프로그램** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfbc-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="4dfbc-122">![응용 프로그램](./media/active-directory-saas-benefitsolver-tutorial/IC700994.png "응용 프로그램")</span><span class="sxs-lookup"><span data-stu-id="4dfbc-122">![Applications](./media/active-directory-saas-benefitsolver-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="4dfbc-123">페이지 맨 아래에 있는 **추가** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfbc-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="4dfbc-124">![응용 프로그램 추가](./media/active-directory-saas-benefitsolver-tutorial/IC749321.png "응용 프로그램 추가")</span><span class="sxs-lookup"><span data-stu-id="4dfbc-124">![Add application](./media/active-directory-saas-benefitsolver-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="4dfbc-125">**수행할 작업** 대화 상자에서 **갤러리에서 응용 프로그램 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfbc-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="4dfbc-126">![갤러리에서 응용 프로그램 추가](./media/active-directory-saas-benefitsolver-tutorial/IC749322.png "갤러리에서 응용 프로그램 추가")</span><span class="sxs-lookup"><span data-stu-id="4dfbc-126">![Add an application from gallerry](./media/active-directory-saas-benefitsolver-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="4dfbc-127">**검색 상자**에 **Benefitsolver**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfbc-127">In the **search box**, type **Benefitsolver**.</span></span>
   
   <span data-ttu-id="4dfbc-128">![응용 프로그램 갤러리](./media/active-directory-saas-benefitsolver-tutorial/IC804821.png "응용 프로그램 갤러리")</span><span class="sxs-lookup"><span data-stu-id="4dfbc-128">![Application Gallery](./media/active-directory-saas-benefitsolver-tutorial/IC804821.png "Application Gallery")</span></span>
7. <span data-ttu-id="4dfbc-129">결과 창에서 **Benefitsolver**를 선택하고 **완료**를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfbc-129">In the results pane, select **Benefitsolver**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="4dfbc-130">![Benefitssolver](./media/active-directory-saas-benefitsolver-tutorial/IC804822.png "Benefitssolver")</span><span class="sxs-lookup"><span data-stu-id="4dfbc-130">![Benefitssolver](./media/active-directory-saas-benefitsolver-tutorial/IC804822.png "Benefitssolver")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="4dfbc-131">Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="4dfbc-131">Configure single sign-on</span></span>

<span data-ttu-id="4dfbc-132">이 섹션은 사용자가 SAML 프로토콜 기반 페더레이션을 사용하여 Azure AD의 계정으로 Benefitsolver에 인증할 수 있게 하는 방법을 간략하게 설명하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4dfbc-132">The objective of this section is to outline how to enable users to authenticate to Benefitsolver with their account in Azure AD using federation based on the SAML protocol.</span></span>  

<span data-ttu-id="4dfbc-133">Benefitsolver 응용 프로그램은 특정 서식에서 SAML 어설션을 예상하며, **SAML 토큰 특성** 구성에 사용자 지정 특성 매핑을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfbc-133">Your Benefitsolver application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **saml token attributes** configuration.</span></span> 

<span data-ttu-id="4dfbc-134">다음 스크린샷은 이에 대한 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4dfbc-134">The following screenshot shows an example for this.</span></span>

<span data-ttu-id="4dfbc-135">![특성](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "특성")</span><span class="sxs-lookup"><span data-stu-id="4dfbc-135">![Attributes](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Attributes")</span></span>

<span data-ttu-id="4dfbc-136">**Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="4dfbc-136">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="4dfbc-137">Azure 클래식 포털의 **Benefitsolver** 응용 프로그램 통합 페이지에서 **Single Sign-On 구성**을 클릭하여 **Single Sign-On 구성** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4dfbc-137">In the Azure classic portal, on the **Benefitsolver** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="4dfbc-138">![Single Sign-On 구성](./media/active-directory-saas-benefitsolver-tutorial/IC804824.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="4dfbc-138">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804824.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="4dfbc-139">**Benefitsolver에 대한 사용자 로그온 방법을 선택하십시오.** 페이지에서 **Microsoft Azure AD Single Sign-On**을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfbc-139">On the **How would you like users to sign on to Benefitsolver** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="4dfbc-140">![Single Sign-On 구성](./media/active-directory-saas-benefitsolver-tutorial/IC804825.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="4dfbc-140">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804825.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="4dfbc-141">**앱 설정 구성** 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfbc-141">On the **Configure App Settings** page, perform the following steps:</span></span>
   
   <span data-ttu-id="4dfbc-142">![앱 설정 구성](./media/active-directory-saas-benefitsolver-tutorial/IC804826.png "앱 설정 구성")</span><span class="sxs-lookup"><span data-stu-id="4dfbc-142">![Configure App Settings](./media/active-directory-saas-benefitsolver-tutorial/IC804826.png "Configure App Settings")</span></span>
   
   1. <span data-ttu-id="4dfbc-143">**로그온 URL** 텍스트 상자에 **http://azure.benefitsolver.com**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfbc-143">In the **Sign On URL** textbox, type **http://azure.benefitsolver.com**.</span></span>
   2. <span data-ttu-id="4dfbc-144">**회신 URL** 텍스트 상자에 **https://www.benefitsolver.com/benefits/BenefitSolverView?page_name=single_signon_saml**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfbc-144">In the **Reply URL** textbox, type **https://www.benefitsolver.com/benefits/BenefitSolverView?page_name=single_signon_saml**.</span></span>  
   3. <span data-ttu-id="4dfbc-145">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="4dfbc-145">Click **Next**.</span></span>
4. <span data-ttu-id="4dfbc-146">**Benefitsolver에서 Single Sign-On 구성** 페이지에서 메타데이터를 다운로드하려면 **메타데이터 다운로드**를 클릭한 다음 메타데이터 파일을 컴퓨터에 로컬로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfbc-146">On the **Configure single sign-on at Benefitsolver** page, to download your metadata, click **Download metadata**, and then save the metadata file locally on your computer.</span></span>
   
   <span data-ttu-id="4dfbc-147">![Single Sign-On 구성](./media/active-directory-saas-benefitsolver-tutorial/IC804827.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="4dfbc-147">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804827.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="4dfbc-148">다운로드한 메타데이터 파일을 Benefitsolver 지원팀에 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="4dfbc-148">Send the downloaded metadata file to your Benefitsolver support team.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="4dfbc-149">Benefitsolver 지원팀은 실제 SSO 구성을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfbc-149">Your Benefitsolver support team has to do the actual SSO configuration.</span></span> <span data-ttu-id="4dfbc-150">구독에 SSO를 사용하도록 설정하면 알림을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfbc-150">You will get a notification when SSO has been enabled for your subscription.</span></span>
   >

6. <span data-ttu-id="4dfbc-151">Azure 클래식 포털에서 Single Sign-On 구성 확인을 선택하고 **완료**를 클릭하여 **Single Sign-On 구성** 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfbc-151">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="4dfbc-152">![Single Sign-On 구성](./media/active-directory-saas-benefitsolver-tutorial/IC804828.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="4dfbc-152">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804828.png "Configure Single Sign-On")</span></span>
7. <span data-ttu-id="4dfbc-153">위쪽 메뉴에서 **특성** to open the **SAML Token 특성** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4dfbc-153">In the menu on the top, click **Attributes** to open the **SAML Token Attributes** dialog.</span></span>
   
   <span data-ttu-id="4dfbc-154">![특성](./media/active-directory-saas-benefitsolver-tutorial/IC795920.png "특성")</span><span class="sxs-lookup"><span data-stu-id="4dfbc-154">![Attributes](./media/active-directory-saas-benefitsolver-tutorial/IC795920.png "Attributes")</span></span>
8. <span data-ttu-id="4dfbc-155">필요한 특성 매핑을 추가하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfbc-155">To add the required attribute mappings, perform the following steps:</span></span>
   
   <span data-ttu-id="4dfbc-156">![특성](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "특성")</span><span class="sxs-lookup"><span data-stu-id="4dfbc-156">![Attributes](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Attributes")</span></span>
   
   | <span data-ttu-id="4dfbc-157">특성 이름</span><span class="sxs-lookup"><span data-stu-id="4dfbc-157">Attribute Name</span></span> | <span data-ttu-id="4dfbc-158">특성 값</span><span class="sxs-lookup"><span data-stu-id="4dfbc-158">Attribute Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="4dfbc-159">ClientID</span><span class="sxs-lookup"><span data-stu-id="4dfbc-159">ClientID</span></span> |<span data-ttu-id="4dfbc-160">Benefitsolver 지원팀에서 이 값을 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfbc-160">You need to get this value from your Benefitsolver support team.</span></span> |
   | <span data-ttu-id="4dfbc-161">ClientKey</span><span class="sxs-lookup"><span data-stu-id="4dfbc-161">ClientKey</span></span> |<span data-ttu-id="4dfbc-162">Benefitsolver 지원팀에서 이 값을 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfbc-162">You need to get this value from your Benefitsolver support team.</span></span> |
   | <span data-ttu-id="4dfbc-163">LogoutURL</span><span class="sxs-lookup"><span data-stu-id="4dfbc-163">LogoutURL</span></span> |<span data-ttu-id="4dfbc-164">Benefitsolver 지원팀에서 이 값을 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfbc-164">You need to get this value from your Benefitsolver support team.</span></span> |
   | <span data-ttu-id="4dfbc-165">EmployeeID</span><span class="sxs-lookup"><span data-stu-id="4dfbc-165">EmployeeID</span></span> |<span data-ttu-id="4dfbc-166">Benefitsolver 지원팀에서 이 값을 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfbc-166">You need to get this value from your Benefitsolver support team.</span></span> |
   
   1. <span data-ttu-id="4dfbc-167">위의 테이블의 각 데이터 행에서 **사용자 특성 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfbc-167">For each data row in the table above, click **add user attribute**.</span></span>
   2. <span data-ttu-id="4dfbc-168">**특성 이름** 텍스트 상자에서 해당 행에 표시된 특성 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfbc-168">In the **Attribute Name** textbox, type the attribute name shown for that row.</span></span>
   3. <span data-ttu-id="4dfbc-169">**특성 값** 텍스트 상자에서 해당 행에 표시된 특성 값을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfbc-169">In the **Attribute Value** textbox, select the attribute value shown for that row.</span></span>
   4. <span data-ttu-id="4dfbc-170">**완료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfbc-170">Click **Complete**.</span></span>
9. <span data-ttu-id="4dfbc-171">**변경 내용 적용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfbc-171">Click **Apply Changes**.</span></span>

## <a name="configure-user-provisioning"></a><span data-ttu-id="4dfbc-172">사용자 프로비전 구성</span><span class="sxs-lookup"><span data-stu-id="4dfbc-172">Configure user provisioning</span></span>
<span data-ttu-id="4dfbc-173">Azure AD 사용자가 Benefitsolver에 로그인할 수 있도록 하려면 Benefitsolver로 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfbc-173">In order to enable Azure AD users to log into Benefitsolver, they must be provisioned into Benefitsolver.</span></span>  

<span data-ttu-id="4dfbc-174">Benefitsolver의 경우 직원 데이터는 HRIS 시스템의 인구 조사 파일을 통해 주로 밤에 채워지는 응용 프로그램에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfbc-174">In the case of Benefitsolver, employee data is in your application populated through a Census file from your HRIS system (typically nightly).</span></span>  

>[!NOTE]
><span data-ttu-id="4dfbc-175">다른 Benefitsolver 사용자 계정 생성 도구 또는 Benefitsolver가 제공한 API를 사용하여 AAD 사용자 계정을 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfbc-175">You can use any other Benefitsolver user account creation tools or APIs provided by Benefitsolver to provision AAD user accounts.</span></span> 
> 

## <a name="assigning-users"></a><span data-ttu-id="4dfbc-176">사용자 할당</span><span class="sxs-lookup"><span data-stu-id="4dfbc-176">Assigning users</span></span>
<span data-ttu-id="4dfbc-177">구성을 테스트하려면 응용 프로그램 사용을 허용하려는 Azure AD 사용자를 할당하여 액세스 권한을 부여해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfbc-177">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

### <a name="to-assign-users-to-benefitsolver-perform-the-following-steps"></a><span data-ttu-id="4dfbc-178">Benefitsolver에 사용자를 할당하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfbc-178">To assign users to Benefitsolver, perform the following steps:</span></span>
1. <span data-ttu-id="4dfbc-179">Azure 클래식 포털에서 테스트 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4dfbc-179">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="4dfbc-180">에 * * Benefitsolver * * 응용 프로그램 통합 페이지에서 클릭 **사용자 할당**합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfbc-180">On the **Benefitsolver **application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="4dfbc-181">![사용자 할당](./media/active-directory-saas-benefitsolver-tutorial/IC804829.png "사용자 할당")</span><span class="sxs-lookup"><span data-stu-id="4dfbc-181">![Assign Users](./media/active-directory-saas-benefitsolver-tutorial/IC804829.png "Assign Users")</span></span>
3. <span data-ttu-id="4dfbc-182">테스트 사용자를 선택하고 **할당**을 클릭한 다음 **예**를 클릭하여 할당을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfbc-182">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="4dfbc-183">![예](./media/active-directory-saas-benefitsolver-tutorial/IC767830.png "예")</span><span class="sxs-lookup"><span data-stu-id="4dfbc-183">![Yes](./media/active-directory-saas-benefitsolver-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="4dfbc-184">Single Sign-On 설정을 테스트하려면 액세스 패널을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4dfbc-184">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="4dfbc-185">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4dfbc-185">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

