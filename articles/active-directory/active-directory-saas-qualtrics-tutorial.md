---
title: "자습서: Qualtrics와 Azure Active Directory 통합 | Microsoft Docs"
description: "어떻게 tooenable Azure Active Directory와 Qualtrics toouse single sign on, 자동화 된 프로비저닝 및 더에 대해 알아봅니다."
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
ms.openlocfilehash: 941642e74b90bb13a5ce37ce6665cfa32cd86016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-qualtrics"></a><span data-ttu-id="3839f-103">자습서: Qualtrics와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="3839f-103">Tutorial: Azure Active Directory integration with Qualtrics</span></span>
<span data-ttu-id="3839f-104">hello이이 자습서는 Azure와 Qualtrics tooshow hello 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="3839f-104">hello objective of this tutorial is tooshow hello integration of Azure and Qualtrics.</span></span>  

<span data-ttu-id="3839f-105">이 자습서에 설명 된 hello 시나리오 다음 항목 hello 이미 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3839f-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="3839f-106">유효한 Azure 구독</span><span class="sxs-lookup"><span data-stu-id="3839f-106">A valid Azure subscription</span></span>
* <span data-ttu-id="3839f-107">Qualtrics SSO(Single Sign-On)가 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="3839f-107">A Qualtrics single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="3839f-108">이 자습서를 완료 한 후 hello Azure AD 사용자 tooQualtrics 배정 됩니다 Qualtrics 회사 사이트 (서비스 공급자에서 시작 된 로그온)에서 또는 hello를 사용 하 여 hello 응용 프로그램에 수 toosingle 로그인 [toohello 소개 액세스 패널](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3839f-108">After completing this tutorial, hello Azure AD users you have assigned tooQualtrics will be able toosingle sign into hello application at your Qualtrics company site (service provider initiated sign on), or using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="3839f-109">이 자습서에 설명 된 hello 시나리오 hello 빌딩 블록을 다음으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3839f-109">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

1. <span data-ttu-id="3839f-110">Qualtrics에 대 한 hello 응용 프로그램 통합 사용</span><span class="sxs-lookup"><span data-stu-id="3839f-110">Enabling hello application integration for Qualtrics</span></span>
2. <span data-ttu-id="3839f-111">SSO(Single Sign-On) 구성</span><span class="sxs-lookup"><span data-stu-id="3839f-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="3839f-112">사용자 프로비전 구성</span><span class="sxs-lookup"><span data-stu-id="3839f-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="3839f-113">사용자 할당</span><span class="sxs-lookup"><span data-stu-id="3839f-113">Assigning users</span></span>

<span data-ttu-id="3839f-114">![시나리오](./media/active-directory-saas-qualtrics-tutorial/IC789542.png "시나리오")</span><span class="sxs-lookup"><span data-stu-id="3839f-114">![Scenario](./media/active-directory-saas-qualtrics-tutorial/IC789542.png "Scenario")</span></span>

## <a name="enabling-hello-application-integration-for-qualtrics"></a><span data-ttu-id="3839f-115">Qualtrics에 대 한 hello 응용 프로그램 통합 사용</span><span class="sxs-lookup"><span data-stu-id="3839f-115">Enabling hello application integration for Qualtrics</span></span>
<span data-ttu-id="3839f-116">hello이이 섹션의 목적은 toooutline 어떻게 Qualtrics에 tooenable hello 응용 프로그램 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="3839f-116">hello objective of this section is toooutline how tooenable hello application integration for Qualtrics.</span></span>

<span data-ttu-id="3839f-117">**tooenable hello 응용 프로그램 통합을 Qualtrics에 대 한 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="3839f-117">**tooenable hello application integration for Qualtrics, perform hello following steps:**</span></span>

1. <span data-ttu-id="3839f-118">Hello hello 왼쪽된 탐색 창에서 Azure 클래식 포털에서에서 클릭 **Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="3839f-118">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="3839f-119">![Active Directory](./media/active-directory-saas-qualtrics-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="3839f-119">![Active Directory](./media/active-directory-saas-qualtrics-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="3839f-120">Hello에서 **디렉터리** 목록, 선택 hello 디렉터리 tooenable 디렉터리 통합을 구하려는 합니다.</span><span class="sxs-lookup"><span data-stu-id="3839f-120">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="3839f-121">tooopen hello 응용 프로그램 보기 hello 디렉터리 보기에서 클릭 **응용 프로그램** hello 상단 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="3839f-121">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
   <span data-ttu-id="3839f-122">![응용 프로그램](./media/active-directory-saas-qualtrics-tutorial/IC700994.png "응용 프로그램")</span><span class="sxs-lookup"><span data-stu-id="3839f-122">![Applications](./media/active-directory-saas-qualtrics-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="3839f-123">클릭 **추가** hello hello 페이지 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3839f-123">Click **Add** at hello bottom of hello page.</span></span>
   
   <span data-ttu-id="3839f-124">![응용 프로그램 추가](./media/active-directory-saas-qualtrics-tutorial/IC749321.png "응용 프로그램 추가")</span><span class="sxs-lookup"><span data-stu-id="3839f-124">![Add application](./media/active-directory-saas-qualtrics-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="3839f-125">Hello에 **하 신 toodo 원하는** 대화 상자에서 클릭 **hello 갤러리에서 응용 프로그램 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="3839f-125">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
   <span data-ttu-id="3839f-126">![갤러리에서 응용 프로그램 추가](./media/active-directory-saas-qualtrics-tutorial/IC749322.png "갤러리에서 응용 프로그램 추가")</span><span class="sxs-lookup"><span data-stu-id="3839f-126">![Add an application from gallerry](./media/active-directory-saas-qualtrics-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="3839f-127">Hello에 **검색 상자**, 형식 **Qualtrics**합니다.</span><span class="sxs-lookup"><span data-stu-id="3839f-127">In hello **search box**, type **Qualtrics**.</span></span>
   
   <span data-ttu-id="3839f-128">![응용 프로그램 갤러리](./media/active-directory-saas-qualtrics-tutorial/IC789543.png "응용 프로그램 갤러리")</span><span class="sxs-lookup"><span data-stu-id="3839f-128">![Application Gallery](./media/active-directory-saas-qualtrics-tutorial/IC789543.png "Application Gallery")</span></span>
7. <span data-ttu-id="3839f-129">Hello 결과 창에서 선택 **Qualtrics**, 클릭 하 고 **완료** tooadd hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="3839f-129">In hello results pane, select **Qualtrics**, and then click **Complete** tooadd hello application.</span></span>
   
   <span data-ttu-id="3839f-130">![Qualtrics](./media/active-directory-saas-qualtrics-tutorial/IC789544.png "Qualtrics")</span><span class="sxs-lookup"><span data-stu-id="3839f-130">![Qualtrics](./media/active-directory-saas-qualtrics-tutorial/IC789544.png "Qualtrics")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="3839f-131">Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="3839f-131">Configure single sign-on</span></span>

<span data-ttu-id="3839f-132">hello이이 섹션의 목적은 toooutline 페더레이션을 사용 하 여 Azure AD에서 자신의 계정으로 tooenable 사용자 tooauthenticate tooQualtrics hello SAML 프로토콜에 따라 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="3839f-132">hello objective of this section is toooutline how tooenable users tooauthenticate tooQualtrics with their account in Azure AD using federation based on hello SAML protocol.</span></span>

<span data-ttu-id="3839f-133">**tooconfigure 단일 로그온 hello 다음 단계를 수행 하십시오.**</span><span class="sxs-lookup"><span data-stu-id="3839f-133">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="3839f-134">Hello hello에 Azure 클래식 포털에서에서 **Qualtrics** 응용 프로그램 통합 페이지에서 클릭 **single sign on 구성** tooopen hello **Single Sign-on 구성** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="3839f-134">In hello Azure classic portal, on hello **Qualtrics** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="3839f-135">![Single Sign-On 구성](./media/active-directory-saas-qualtrics-tutorial/IC789545.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="3839f-135">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789545.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="3839f-136">Hello에 **어떻게 tooQualtrics에 사용자가 toosign 보 시겠습니까** 페이지에서 **Microsoft Azure AD Single Sign-on**, 클릭 하 고 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="3839f-136">On hello **How would you like users toosign on tooQualtrics** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="3839f-137">![Single Sign-On 구성](./media/active-directory-saas-qualtrics-tutorial/IC789546.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="3839f-137">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789546.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="3839f-138">Hello에 **앱 URL 구성** 페이지 hello에서 **Qualtrics 로그온 URL** 텍스트 상자에 URL (예:: "*https://ssotest2ut1.qualtrics.com*"), 클릭하고**다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="3839f-138">On hello **Configure App URL** page, in hello **Qualtrics Sign On URL** textbox, type your URL (e.g.: “*https://ssotest2ut1.qualtrics.com*"), and then click **Next**.</span></span>
   
   <span data-ttu-id="3839f-139">![앱 URL 구성](./media/active-directory-saas-qualtrics-tutorial/IC789547.png "앱 URL 구성")</span><span class="sxs-lookup"><span data-stu-id="3839f-139">![Configure App URL](./media/active-directory-saas-qualtrics-tutorial/IC789547.png "Configure App URL")</span></span>
4. <span data-ttu-id="3839f-140">Hello에 **Qualtrics에서 single sign on 구성** 페이지 **메타 데이터 다운로드**, hello 메타 데이터 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="3839f-140">On hello **Configure single sign-on at Qualtrics** page, click **Download metadata**, and then save hello metadata file on your computer.</span></span>
   
   <span data-ttu-id="3839f-141">![Single Sign-On 구성](./media/active-directory-saas-qualtrics-tutorial/IC789548.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="3839f-141">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789548.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="3839f-142">Hello 메타 데이터 파일 toohello Qualtrics 지원 팀에 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="3839f-142">Send hello metadata file toohello Qualtrics support team.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="3839f-143">hello SSO 구성에 toobe hello Qualtrics 지원 팀에서 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3839f-143">hello SSO configuration has toobe performed by hello Qualtrics support team.</span></span> <span data-ttu-id="3839f-144">Hello 구성이 완료 되는 즉시 알림을 받아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3839f-144">You will get a notification as soon as hello configuration has been completed.</span></span>
   > 
   > 
6. <span data-ttu-id="3839f-145">Azure 클래식 포털 hello에 hello single sign on 구성 확인을 선택한 다음 클릭 **완료** tooclose hello **Single Sign-on 구성** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="3839f-145">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="3839f-146">![Single Sign-On 구성](./media/active-directory-saas-qualtrics-tutorial/IC789549.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="3839f-146">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789549.png "Configure Single Sign-On")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="3839f-147">사용자 프로비전 구성</span><span class="sxs-lookup"><span data-stu-id="3839f-147">Configure user provisioning</span></span>

<span data-ttu-id="3839f-148">사용자에 대 한 있습니다 tooconfigure tooQualtrics 프로 비전 작업 항목이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3839f-148">There is no action item for you tooconfigure user provisioning tooQualtrics.</span></span> <span data-ttu-id="3839f-149">Toolog hello 액세스 패널을 사용 하 여 Qualtrics에 시도 하는 할당된 된 사용자, Qualtrics hello 사용자의 존재 여부를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3839f-149">When an assigned user tries toolog into Qualtrics using hello access panel, Qualtrics checks whether hello user exists.</span></span>  

<span data-ttu-id="3839f-150">사용할 수 있는 사용자 계정이 없으면 자동으로 Qualtrics에 의해 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="3839f-150">If there is no user account available yet, it is automatically created by Qualtrics.</span></span>

## <a name="assign-users"></a><span data-ttu-id="3839f-151">사용자 할당</span><span class="sxs-lookup"><span data-stu-id="3839f-151">Assign users</span></span>
<span data-ttu-id="3839f-152">tootest 구성에 tooallow 할당 하 여 응용 프로그램 액세스 tooit를 사용 하 여 원하는 toogrant hello Azure AD 사용자가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="3839f-152">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="3839f-153">**tooassign 사용자 tooQualtrics hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="3839f-153">**tooassign users tooQualtrics, perform hello following steps:**</span></span>

1. <span data-ttu-id="3839f-154">Azure 클래식 포털 hello 테스트 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3839f-154">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="3839f-155">Hello에 **Qualtrics** 응용 프로그램 통합 페이지에서 클릭 **사용자 할당**합니다.</span><span class="sxs-lookup"><span data-stu-id="3839f-155">On hello **Qualtrics** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="3839f-156">![사용자 할당](./media/active-directory-saas-qualtrics-tutorial/IC789550.png "사용자 할당")</span><span class="sxs-lookup"><span data-stu-id="3839f-156">![Assign Users](./media/active-directory-saas-qualtrics-tutorial/IC789550.png "Assign Users")</span></span>
3. <span data-ttu-id="3839f-157">테스트 사용자 선택, 클릭 **할당**, 클릭 하 고 **예** tooconfirm 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="3839f-157">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
   <span data-ttu-id="3839f-158">![예](./media/active-directory-saas-qualtrics-tutorial/IC767830.png "예")</span><span class="sxs-lookup"><span data-stu-id="3839f-158">![Yes](./media/active-directory-saas-qualtrics-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="3839f-159">SSO 설정 tootest 원하는 hello 액세스 패널을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3839f-159">If you want tootest your SSO settings, open hello Access Panel.</span></span> <span data-ttu-id="3839f-160">액세스 패널 hello에 대 한 자세한 내용은 참조 하십시오. [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3839f-160">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

