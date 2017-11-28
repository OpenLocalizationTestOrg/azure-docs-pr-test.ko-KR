---
title: "자습서: Benefitsolver와 Azure Active Directory 통합 | Microsoft Docs"
description: "방법을 toouse Benefitsolver tooenable Azure Active Directory와 single sign on, 자동화 된 프로비저닝 및 더에 대해 알아봅니다."
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
ms.openlocfilehash: 5bb8511ef9be1e386956188a93e899d6ebe56ed5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-benefitsolver"></a><span data-ttu-id="dadf9-103">자습서: Benefitsolver와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="dadf9-103">Tutorial: Azure Active Directory integration with Benefitsolver</span></span>
<span data-ttu-id="dadf9-104">hello이이 자습서는 Azure와 Benefitsolver tooshow hello 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="dadf9-104">hello objective of this tutorial is tooshow hello integration of Azure and Benefitsolver.</span></span>  

<span data-ttu-id="dadf9-105">이 자습서에 설명 된 hello 시나리오 다음 항목 hello 이미 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="dadf9-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="dadf9-106">유효한 Azure 구독</span><span class="sxs-lookup"><span data-stu-id="dadf9-106">A valid Azure subscription</span></span>
* <span data-ttu-id="dadf9-107">Benefitsolver SSO(Single Sign-On)가 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="dadf9-107">A Benefitsolver single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="dadf9-108">이 자습서를 완료 한 후 hello Azure AD 사용자 tooBenefitsolver 배정 됩니다 hello를 사용 하 여 hello 응용 프로그램에 수 toosingle 로그인 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="dadf9-108">After completing this tutorial, hello Azure AD users you have assigned tooBenefitsolver will be able toosingle sign into hello application using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="dadf9-109">이 자습서에 설명 된 hello 시나리오 hello 빌딩 블록을 다음으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dadf9-109">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

1. <span data-ttu-id="dadf9-110">Benefitsolver에 대 한 hello 응용 프로그램 통합 사용</span><span class="sxs-lookup"><span data-stu-id="dadf9-110">Enabling hello application integration for Benefitsolver</span></span>
2. <span data-ttu-id="dadf9-111">SSO(Single Sign-On) 구성</span><span class="sxs-lookup"><span data-stu-id="dadf9-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="dadf9-112">사용자 프로비전 구성</span><span class="sxs-lookup"><span data-stu-id="dadf9-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="dadf9-113">사용자 할당</span><span class="sxs-lookup"><span data-stu-id="dadf9-113">Assigning users</span></span>

<span data-ttu-id="dadf9-114">![시나리오](./media/active-directory-saas-benefitsolver-tutorial/IC804820.png "시나리오")</span><span class="sxs-lookup"><span data-stu-id="dadf9-114">![Scenario](./media/active-directory-saas-benefitsolver-tutorial/IC804820.png "Scenario")</span></span>

## <a name="enabling-hello-application-integration-for-benefitsolver"></a><span data-ttu-id="dadf9-115">Benefitsolver에 대 한 hello 응용 프로그램 통합 사용</span><span class="sxs-lookup"><span data-stu-id="dadf9-115">Enabling hello application integration for Benefitsolver</span></span>
<span data-ttu-id="dadf9-116">hello이이 섹션의 목적은 toooutline 어떻게 Benefitsolver에 tooenable hello 응용 프로그램 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="dadf9-116">hello objective of this section is toooutline how tooenable hello application integration for Benefitsolver.</span></span>

### <a name="tooenable-hello-application-integration-for-benefitsolver-perform-hello-following-steps"></a><span data-ttu-id="dadf9-117">Benefitsolver에 tooenable hello 응용 프로그램 통합 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="dadf9-117">tooenable hello application integration for Benefitsolver, perform hello following steps:</span></span>
1. <span data-ttu-id="dadf9-118">Hello hello 왼쪽된 탐색 창에서 Azure 클래식 포털에서에서 클릭 **Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="dadf9-118">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="dadf9-119">![Active Directory](./media/active-directory-saas-benefitsolver-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="dadf9-119">![Active Directory](./media/active-directory-saas-benefitsolver-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="dadf9-120">Hello에서 **디렉터리** 목록, 선택 hello 디렉터리 tooenable 디렉터리 통합을 구하려는 합니다.</span><span class="sxs-lookup"><span data-stu-id="dadf9-120">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="dadf9-121">tooopen hello 응용 프로그램 보기 hello 디렉터리 보기에서 클릭 **응용 프로그램** hello 상단 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="dadf9-121">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
   <span data-ttu-id="dadf9-122">![응용 프로그램](./media/active-directory-saas-benefitsolver-tutorial/IC700994.png "응용 프로그램")</span><span class="sxs-lookup"><span data-stu-id="dadf9-122">![Applications](./media/active-directory-saas-benefitsolver-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="dadf9-123">클릭 **추가** hello hello 페이지 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dadf9-123">Click **Add** at hello bottom of hello page.</span></span>
   
   <span data-ttu-id="dadf9-124">![응용 프로그램 추가](./media/active-directory-saas-benefitsolver-tutorial/IC749321.png "응용 프로그램 추가")</span><span class="sxs-lookup"><span data-stu-id="dadf9-124">![Add application](./media/active-directory-saas-benefitsolver-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="dadf9-125">Hello에 **하 신 toodo 원하는** 대화 상자에서 클릭 **hello 갤러리에서 응용 프로그램 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="dadf9-125">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
   <span data-ttu-id="dadf9-126">![갤러리에서 응용 프로그램 추가](./media/active-directory-saas-benefitsolver-tutorial/IC749322.png "갤러리에서 응용 프로그램 추가")</span><span class="sxs-lookup"><span data-stu-id="dadf9-126">![Add an application from gallerry](./media/active-directory-saas-benefitsolver-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="dadf9-127">Hello에 **검색 상자**, 형식 **Benefitsolver**합니다.</span><span class="sxs-lookup"><span data-stu-id="dadf9-127">In hello **search box**, type **Benefitsolver**.</span></span>
   
   <span data-ttu-id="dadf9-128">![응용 프로그램 갤러리](./media/active-directory-saas-benefitsolver-tutorial/IC804821.png "응용 프로그램 갤러리")</span><span class="sxs-lookup"><span data-stu-id="dadf9-128">![Application Gallery](./media/active-directory-saas-benefitsolver-tutorial/IC804821.png "Application Gallery")</span></span>
7. <span data-ttu-id="dadf9-129">Hello 결과 창에서 선택 **Benefitsolver**, 클릭 하 고 **완료** tooadd hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="dadf9-129">In hello results pane, select **Benefitsolver**, and then click **Complete** tooadd hello application.</span></span>
   
   <span data-ttu-id="dadf9-130">![Benefitssolver](./media/active-directory-saas-benefitsolver-tutorial/IC804822.png "Benefitssolver")</span><span class="sxs-lookup"><span data-stu-id="dadf9-130">![Benefitssolver](./media/active-directory-saas-benefitsolver-tutorial/IC804822.png "Benefitssolver")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="dadf9-131">Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="dadf9-131">Configure single sign-on</span></span>

<span data-ttu-id="dadf9-132">hello이이 섹션의 목적은 toooutline 페더레이션을 사용 하 여 Azure AD에서 자신의 계정으로 tooenable 사용자 tooauthenticate tooBenefitsolver hello SAML 프로토콜에 따라 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="dadf9-132">hello objective of this section is toooutline how tooenable users tooauthenticate tooBenefitsolver with their account in Azure AD using federation based on hello SAML protocol.</span></span>  

<span data-ttu-id="dadf9-133">Benefitsolver 응용 프로그램에 사용자 지정 특성 매핑을 tooyour tooadd 요구 하는 특정 형식으로 hello SAML 어설션이 **saml 토큰 특성** 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="dadf9-133">Your Benefitsolver application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour **saml token attributes** configuration.</span></span> 

<span data-ttu-id="dadf9-134">다음 스크린 샷 hello이에 대 한 예가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dadf9-134">hello following screenshot shows an example for this.</span></span>

<span data-ttu-id="dadf9-135">![특성](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "특성")</span><span class="sxs-lookup"><span data-stu-id="dadf9-135">![Attributes](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Attributes")</span></span>

<span data-ttu-id="dadf9-136">**tooconfigure 단일 로그온 hello 다음 단계를 수행 하십시오.**</span><span class="sxs-lookup"><span data-stu-id="dadf9-136">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="dadf9-137">Hello hello에 Azure 클래식 포털에서에서 **Benefitsolver** 응용 프로그램 통합 페이지에서 클릭 **single sign on 구성** tooopen hello **Single Sign-on 구성** 대화 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="dadf9-137">In hello Azure classic portal, on hello **Benefitsolver** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="dadf9-138">![Single Sign-On 구성](./media/active-directory-saas-benefitsolver-tutorial/IC804824.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="dadf9-138">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804824.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="dadf9-139">Hello에 **어떻게 tooBenefitsolver에 사용자가 toosign 보 시겠습니까** 페이지에서 **Microsoft Azure AD Single Sign-on**, 클릭 하 고 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="dadf9-139">On hello **How would you like users toosign on tooBenefitsolver** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="dadf9-140">![Single Sign-On 구성](./media/active-directory-saas-benefitsolver-tutorial/IC804825.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="dadf9-140">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804825.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="dadf9-141">Hello에 **앱 설정 구성** 페이지 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="dadf9-141">On hello **Configure App Settings** page, perform hello following steps:</span></span>
   
   <span data-ttu-id="dadf9-142">![앱 설정 구성](./media/active-directory-saas-benefitsolver-tutorial/IC804826.png "앱 설정 구성")</span><span class="sxs-lookup"><span data-stu-id="dadf9-142">![Configure App Settings](./media/active-directory-saas-benefitsolver-tutorial/IC804826.png "Configure App Settings")</span></span>
   
   1. <span data-ttu-id="dadf9-143">Hello에 **로그온 URL** 텍스트 상자에 **http://azure.benefitsolver.com**합니다.</span><span class="sxs-lookup"><span data-stu-id="dadf9-143">In hello **Sign On URL** textbox, type **http://azure.benefitsolver.com**.</span></span>
   2. <span data-ttu-id="dadf9-144">Hello에 **회신 URL** 텍스트 상자에 **https://www.benefitsolver.com/benefits/BenefitSolverView?page_name=single_signon_saml**합니다.</span><span class="sxs-lookup"><span data-stu-id="dadf9-144">In hello **Reply URL** textbox, type **https://www.benefitsolver.com/benefits/BenefitSolverView?page_name=single_signon_saml**.</span></span>  
   3. <span data-ttu-id="dadf9-145">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="dadf9-145">Click **Next**.</span></span>
4. <span data-ttu-id="dadf9-146">Hello에 **Benefitsolver에서 single sign on 구성** 페이지, toodownload 메타 데이터를 클릭 하 여 **메타 데이터 다운로드**, hello 메타 데이터 파일을 컴퓨터에 로컬로 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="dadf9-146">On hello **Configure single sign-on at Benefitsolver** page, toodownload your metadata, click **Download metadata**, and then save hello metadata file locally on your computer.</span></span>
   
   <span data-ttu-id="dadf9-147">![Single Sign-On 구성](./media/active-directory-saas-benefitsolver-tutorial/IC804827.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="dadf9-147">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804827.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="dadf9-148">Hello 다운로드 한 메타 데이터 파일 tooyour Benefitsolver 지원 팀에 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="dadf9-148">Send hello downloaded metadata file tooyour Benefitsolver support team.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="dadf9-149">Benefitsolver 지원 팀에 toodo hello 실제 SSO 구성을 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dadf9-149">Your Benefitsolver support team has toodo hello actual SSO configuration.</span></span> <span data-ttu-id="dadf9-150">구독에 SSO를 사용하도록 설정하면 알림을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dadf9-150">You will get a notification when SSO has been enabled for your subscription.</span></span>
   >

6. <span data-ttu-id="dadf9-151">Azure 클래식 포털 hello에 hello single sign on 구성 확인을 선택한 다음 클릭 **완료** tooclose hello **Single Sign-on 구성** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="dadf9-151">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="dadf9-152">![Single Sign-On 구성](./media/active-directory-saas-benefitsolver-tutorial/IC804828.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="dadf9-152">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804828.png "Configure Single Sign-On")</span></span>
7. <span data-ttu-id="dadf9-153">Hello 메뉴에서 hello 위에 표시를 클릭 **특성** tooopen hello **SAML 토큰 특성** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="dadf9-153">In hello menu on hello top, click **Attributes** tooopen hello **SAML Token Attributes** dialog.</span></span>
   
   <span data-ttu-id="dadf9-154">![특성](./media/active-directory-saas-benefitsolver-tutorial/IC795920.png "특성")</span><span class="sxs-lookup"><span data-stu-id="dadf9-154">![Attributes](./media/active-directory-saas-benefitsolver-tutorial/IC795920.png "Attributes")</span></span>
8. <span data-ttu-id="dadf9-155">tooadd hello 필요한 특성 매핑을 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="dadf9-155">tooadd hello required attribute mappings, perform hello following steps:</span></span>
   
   <span data-ttu-id="dadf9-156">![특성](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "특성")</span><span class="sxs-lookup"><span data-stu-id="dadf9-156">![Attributes](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Attributes")</span></span>
   
   | <span data-ttu-id="dadf9-157">특성 이름</span><span class="sxs-lookup"><span data-stu-id="dadf9-157">Attribute Name</span></span> | <span data-ttu-id="dadf9-158">특성 값</span><span class="sxs-lookup"><span data-stu-id="dadf9-158">Attribute Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="dadf9-159">ClientID</span><span class="sxs-lookup"><span data-stu-id="dadf9-159">ClientID</span></span> |<span data-ttu-id="dadf9-160">이 값이 필요한 tooget이 Benefitsolver 지원 팀에서.</span><span class="sxs-lookup"><span data-stu-id="dadf9-160">You need tooget this value from your Benefitsolver support team.</span></span> |
   | <span data-ttu-id="dadf9-161">ClientKey</span><span class="sxs-lookup"><span data-stu-id="dadf9-161">ClientKey</span></span> |<span data-ttu-id="dadf9-162">이 값이 필요한 tooget이 Benefitsolver 지원 팀에서.</span><span class="sxs-lookup"><span data-stu-id="dadf9-162">You need tooget this value from your Benefitsolver support team.</span></span> |
   | <span data-ttu-id="dadf9-163">LogoutURL</span><span class="sxs-lookup"><span data-stu-id="dadf9-163">LogoutURL</span></span> |<span data-ttu-id="dadf9-164">이 값이 필요한 tooget이 Benefitsolver 지원 팀에서.</span><span class="sxs-lookup"><span data-stu-id="dadf9-164">You need tooget this value from your Benefitsolver support team.</span></span> |
   | <span data-ttu-id="dadf9-165">EmployeeID</span><span class="sxs-lookup"><span data-stu-id="dadf9-165">EmployeeID</span></span> |<span data-ttu-id="dadf9-166">이 값이 필요한 tooget이 Benefitsolver 지원 팀에서.</span><span class="sxs-lookup"><span data-stu-id="dadf9-166">You need tooget this value from your Benefitsolver support team.</span></span> |
   
   1. <span data-ttu-id="dadf9-167">위의 hello 테이블의 각 데이터 행에 대 한 클릭 **사용자 특성 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="dadf9-167">For each data row in hello table above, click **add user attribute**.</span></span>
   2. <span data-ttu-id="dadf9-168">Hello에 **특성 이름** textbox, 해당 행에 대 한 표시 형식 hello 특성 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="dadf9-168">In hello **Attribute Name** textbox, type hello attribute name shown for that row.</span></span>
   3. <span data-ttu-id="dadf9-169">Hello에 **특성 값** textbox, 해당 행에 대해 표시 된 선택 hello 특성 값입니다.</span><span class="sxs-lookup"><span data-stu-id="dadf9-169">In hello **Attribute Value** textbox, select hello attribute value shown for that row.</span></span>
   4. <span data-ttu-id="dadf9-170">페이지 맨 아래에 있는 **완료**을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dadf9-170">Click **Complete**.</span></span>
9. <span data-ttu-id="dadf9-171">**변경 내용 적용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dadf9-171">Click **Apply Changes**.</span></span>

## <a name="configure-user-provisioning"></a><span data-ttu-id="dadf9-172">사용자 프로비전 구성</span><span class="sxs-lookup"><span data-stu-id="dadf9-172">Configure user provisioning</span></span>
<span data-ttu-id="dadf9-173">Tooenable Azure AD 사용자가 toolog Benefitsolver로 주문 하 고에 Benefitsolver에 이들 프로 비전 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dadf9-173">In order tooenable Azure AD users toolog into Benefitsolver, they must be provisioned into Benefitsolver.</span></span>  

<span data-ttu-id="dadf9-174">Hello 경우 Benefitsolver의 직원 데이터는 채워집니다 (일반적으로 nightly) HRIS 시스템에서 Census 파일을 통해 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="dadf9-174">In hello case of Benefitsolver, employee data is in your application populated through a Census file from your HRIS system (typically nightly).</span></span>  

>[!NOTE]
><span data-ttu-id="dadf9-175">다른 Benefitsolver 사용자 계정 만들기 도구를 사용할 수 있습니다 또는 AAD 사용자 계정을 Benefitsolver tooprovision에서 제공 된 Api입니다.</span><span class="sxs-lookup"><span data-stu-id="dadf9-175">You can use any other Benefitsolver user account creation tools or APIs provided by Benefitsolver tooprovision AAD user accounts.</span></span> 
> 

## <a name="assigning-users"></a><span data-ttu-id="dadf9-176">사용자 할당</span><span class="sxs-lookup"><span data-stu-id="dadf9-176">Assigning users</span></span>
<span data-ttu-id="dadf9-177">tootest 구성에 tooallow 할당 하 여 응용 프로그램 액세스 tooit를 사용 하 여 원하는 toogrant hello Azure AD 사용자가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="dadf9-177">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

### <a name="tooassign-users-toobenefitsolver-perform-hello-following-steps"></a><span data-ttu-id="dadf9-178">tooassign 사용자 tooBenefitsolver hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="dadf9-178">tooassign users tooBenefitsolver, perform hello following steps:</span></span>
1. <span data-ttu-id="dadf9-179">Azure 클래식 포털 hello 테스트 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dadf9-179">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="dadf9-180">Hello에 * * Benefitsolver * * 응용 프로그램 통합 페이지에서 클릭 **사용자 할당**합니다.</span><span class="sxs-lookup"><span data-stu-id="dadf9-180">On hello **Benefitsolver **application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="dadf9-181">![사용자 할당](./media/active-directory-saas-benefitsolver-tutorial/IC804829.png "사용자 할당")</span><span class="sxs-lookup"><span data-stu-id="dadf9-181">![Assign Users](./media/active-directory-saas-benefitsolver-tutorial/IC804829.png "Assign Users")</span></span>
3. <span data-ttu-id="dadf9-182">테스트 사용자 선택, 클릭 **할당**, 클릭 하 고 **예** tooconfirm 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="dadf9-182">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
   <span data-ttu-id="dadf9-183">![예](./media/active-directory-saas-benefitsolver-tutorial/IC767830.png "예")</span><span class="sxs-lookup"><span data-stu-id="dadf9-183">![Yes](./media/active-directory-saas-benefitsolver-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="dadf9-184">Single sign on 설정 tootest 원하는 hello 액세스 패널을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="dadf9-184">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="dadf9-185">액세스 패널 hello에 대 한 자세한 내용은 참조 하십시오. [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="dadf9-185">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

