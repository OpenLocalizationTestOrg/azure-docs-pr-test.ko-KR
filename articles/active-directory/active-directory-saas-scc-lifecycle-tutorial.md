---
title: "자습서: SCC LifeCycle과 Azure Active Directory 통합 | Microsoft Docs"
description: "로그온, 자동화 된 프로 비전 등와 Azure Active Directory tooenable toouse SCC LifeCycle single 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: c10c313c5fc157ed70d2ccecfb930a8a765f8444
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-scc-lifecycle"></a><span data-ttu-id="a30ee-103">자습서: SCC LifeCycle과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="a30ee-103">Tutorial: Azure Active Directory integration with SCC LifeCycle</span></span>
<span data-ttu-id="a30ee-104">hello이이 자습서는 Azure와 SCC LifeCycle tooshow hello 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="a30ee-104">hello objective of this tutorial is tooshow hello integration of Azure and SCC LifeCycle.</span></span>  

<span data-ttu-id="a30ee-105">이 자습서에 설명 된 hello 시나리오 다음 항목 hello 이미 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a30ee-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="a30ee-106">유효한 Azure 구독</span><span class="sxs-lookup"><span data-stu-id="a30ee-106">A valid Azure subscription</span></span>
* <span data-ttu-id="a30ee-107">SCC LifeCycle SSO(Single Sign-On)가 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="a30ee-107">A SCC LifeCycle single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="a30ee-108">이 자습서를 완료 하면 Azure AD 할당 한 사용자는 수명 주기 됩니다 tooSCC 수 toosingle 기호 hello 응용 프로그램으로 SCC LifeCycle 회사 사이트 (서비스 공급자에서 시작 된 로그온)에서 hello 또는 hello를 사용 하 여 [소개 액세스 패널 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a30ee-108">After completing this tutorial, hello Azure AD users you have assigned tooSCC LifeCycle will be able toosingle sign into hello application at your SCC LifeCycle company site (service provider initiated sign on), or using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="a30ee-109">이 자습서에 설명 된 hello 시나리오 hello 빌딩 블록을 다음으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a30ee-109">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

1. <span data-ttu-id="a30ee-110">SCC LifeCycle에 대 한 hello 응용 프로그램 통합 사용</span><span class="sxs-lookup"><span data-stu-id="a30ee-110">Enabling hello application integration for SCC LifeCycle</span></span>
2. <span data-ttu-id="a30ee-111">SSO(Single Sign-On) 구성</span><span class="sxs-lookup"><span data-stu-id="a30ee-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="a30ee-112">사용자 프로비전 구성</span><span class="sxs-lookup"><span data-stu-id="a30ee-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="a30ee-113">사용자 할당</span><span class="sxs-lookup"><span data-stu-id="a30ee-113">Assigning users</span></span>

<span data-ttu-id="a30ee-114">![시나리오](./media/active-directory-saas-scc-lifecycle-tutorial/IC794120.png "시나리오")</span><span class="sxs-lookup"><span data-stu-id="a30ee-114">![Scenario](./media/active-directory-saas-scc-lifecycle-tutorial/IC794120.png "Scenario")</span></span>

## <a name="enable-hello-application-integration-for-scc-lifecycle"></a><span data-ttu-id="a30ee-115">SCC LifeCycle에 대 한 hello 응용 프로그램 통합을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="a30ee-115">Enable hello application integration for SCC LifeCycle</span></span>
<span data-ttu-id="a30ee-116">hello이이 섹션의 목적은 toooutline 어떻게 SCC LifeCycle에 대 한 tooenable hello 응용 프로그램 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="a30ee-116">hello objective of this section is toooutline how tooenable hello application integration for SCC LifeCycle.</span></span>

<span data-ttu-id="a30ee-117">**SCC LifeCycle에 대 한 tooenable hello 응용 프로그램 통합 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="a30ee-117">**tooenable hello application integration for SCC LifeCycle, perform hello following steps:**</span></span>

1. <span data-ttu-id="a30ee-118">Hello hello 왼쪽된 탐색 창에서 Azure 클래식 포털에서에서 클릭 **Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="a30ee-118">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="a30ee-119">![Active Directory](./media/active-directory-saas-scc-lifecycle-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="a30ee-119">![Active Directory](./media/active-directory-saas-scc-lifecycle-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="a30ee-120">Hello에서 **디렉터리** 목록, 선택 hello 디렉터리 tooenable 디렉터리 통합을 구하려는 합니다.</span><span class="sxs-lookup"><span data-stu-id="a30ee-120">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="a30ee-121">tooopen hello 응용 프로그램 보기 hello 디렉터리 보기에서 클릭 **응용 프로그램** hello 상단 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="a30ee-121">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    <span data-ttu-id="a30ee-122">![응용 프로그램](./media/active-directory-saas-scc-lifecycle-tutorial/IC700994.png "응용 프로그램")</span><span class="sxs-lookup"><span data-stu-id="a30ee-122">![Applications](./media/active-directory-saas-scc-lifecycle-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="a30ee-123">클릭 **추가** hello hello 페이지 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a30ee-123">Click **Add** at hello bottom of hello page.</span></span>
   
    <span data-ttu-id="a30ee-124">![응용 프로그램 추가](./media/active-directory-saas-scc-lifecycle-tutorial/IC749321.png "응용 프로그램 추가")</span><span class="sxs-lookup"><span data-stu-id="a30ee-124">![Add application](./media/active-directory-saas-scc-lifecycle-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="a30ee-125">Hello에 **하 신 toodo 원하는** 대화 상자에서 클릭 **hello 갤러리에서 응용 프로그램 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="a30ee-125">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    <span data-ttu-id="a30ee-126">![갤러리에서 응용 프로그램 추가](./media/active-directory-saas-scc-lifecycle-tutorial/IC749322.png "갤러리에서 응용 프로그램 추가")</span><span class="sxs-lookup"><span data-stu-id="a30ee-126">![Add an application from gallerry](./media/active-directory-saas-scc-lifecycle-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="a30ee-127">Hello에 **검색 상자**, 형식 **SCC LifeCycle**합니다.</span><span class="sxs-lookup"><span data-stu-id="a30ee-127">In hello **search box**, type **SCC LifeCycle**.</span></span>
   
    <span data-ttu-id="a30ee-128">![응용 프로그램 갤러리](./media/active-directory-saas-scc-lifecycle-tutorial/IC794121.png "응용 프로그램 갤러리")</span><span class="sxs-lookup"><span data-stu-id="a30ee-128">![Application Gallery](./media/active-directory-saas-scc-lifecycle-tutorial/IC794121.png "Application Gallery")</span></span>
7. <span data-ttu-id="a30ee-129">Hello 결과 창에서 선택 **SCC LifeCycle**, 클릭 하 고 **완료** tooadd hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="a30ee-129">In hello results pane, select **SCC LifeCycle**, and then click **Complete** tooadd hello application.</span></span>
   
    <span data-ttu-id="a30ee-130">![SCC LifeCycle](./media/active-directory-saas-scc-lifecycle-tutorial/IC795082.png "SCC LifeCycle")</span><span class="sxs-lookup"><span data-stu-id="a30ee-130">![SCC LifeCycle](./media/active-directory-saas-scc-lifecycle-tutorial/IC795082.png "SCC LifeCycle")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="a30ee-131">Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="a30ee-131">Configure single sign-on</span></span>

<span data-ttu-id="a30ee-132">hello이이 섹션의 목적은 toooutline 페더레이션을 사용 하 여 Azure AD에서 자신의 계정으로 tooenable 사용자 tooauthenticate tooSCC 수명 주기 hello SAML 프로토콜에 따라 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="a30ee-132">hello objective of this section is toooutline how tooenable users tooauthenticate tooSCC LifeCycle with their account in Azure AD using federation based on hello SAML protocol.</span></span>

<span data-ttu-id="a30ee-133">**tooconfigure 단일 로그온 hello 다음 단계를 수행 하십시오.**</span><span class="sxs-lookup"><span data-stu-id="a30ee-133">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="a30ee-134">Hello hello에 Azure 클래식 포털에서에서 **SCC LifeCycle** 응용 프로그램 통합 페이지에서 클릭 **single sign on 구성** tooopen hello * * Single Sign-on 구성 * * 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="a30ee-134">In hello Azure classic portal, on hello **SCC LifeCycle** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On ** dialog.</span></span>
   
    <span data-ttu-id="a30ee-135">![Single Sign-On 구성](./media/active-directory-saas-scc-lifecycle-tutorial/IC794122.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="a30ee-135">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC794122.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="a30ee-136">Hello에 **어떻게 tooSCC 수명 주기에서 사용자가 toosign 보 시겠습니까** 페이지에서 **Microsoft Azure AD Single Sign-on**, 클릭 하 고 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="a30ee-136">On hello **How would you like users toosign on tooSCC LifeCycle** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="a30ee-137">![Single Sign-On 구성](./media/active-directory-saas-scc-lifecycle-tutorial/IC794123.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="a30ee-137">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC794123.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="a30ee-138">Hello에 **앱 URL 구성** 페이지 hello **로그온 URL** textbox hello URL 입력에서 사용 하는 사용자가 toosign tooyour SCC LifeCycle 응용 프로그램 패턴 hello를 사용 하 여 "*https:// bs1.scc.com/lc7/welcome/customer/PICTtest.aspx*"를 클릭 하 고 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="a30ee-138">On hello **Configure App URL** page, in hello **Sign On URL** textbox, type hello URL used by your users toosign on tooyour SCC LifeCycle application using hello following pattern "*https://bs1.scc.com/lc7/welcome/customer/PICTtest.aspx*", and then click **Next**.</span></span>
   
    <span data-ttu-id="a30ee-139">![앱 URL 구성](./media/active-directory-saas-scc-lifecycle-tutorial/IC794124.png "앱 URL 구성")</span><span class="sxs-lookup"><span data-stu-id="a30ee-139">![Configure App URL](./media/active-directory-saas-scc-lifecycle-tutorial/IC794124.png "Configure App URL")</span></span>
4. <span data-ttu-id="a30ee-140">Hello에 **SCC LifeCycle에서 single sign on 구성** 페이지 **메타 데이터 다운로드**, 메타 데이터 파일을 컴퓨터에 로컬로 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="a30ee-140">On hello **Configure single sign-on at SCC LifeCycle** page, click **Download metadata**, and then save metadata file locally on your computer.</span></span>
   
   <span data-ttu-id="a30ee-141">![Single Sign-On 구성](./media/active-directory-saas-scc-lifecycle-tutorial/IC795083.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="a30ee-141">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC795083.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="a30ee-142">해당 메타 데이터 파일 tooSCC LifeCycle 지원 팀으로 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="a30ee-142">Forward that Metadata file tooSCC LifeCycle Support team.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="a30ee-143">Single sign on에 toobe hello SCC LifeCycle 지원 팀으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a30ee-143">Single sign-on has toobe enabled by hello SCC LifeCycle support team.</span></span>
   > 
   > 

6. <span data-ttu-id="a30ee-144">Azure 클래식 포털 hello에 hello single sign on 구성 확인을 선택한 다음 클릭 **완료** tooclose hello **Single Sign-on 구성** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="a30ee-144">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="a30ee-145">![Single Sign-On 구성](./media/active-directory-saas-scc-lifecycle-tutorial/IC794125.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="a30ee-145">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC794125.png "Configure Single Sign-On")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="a30ee-146">사용자 프로비전 구성</span><span class="sxs-lookup"><span data-stu-id="a30ee-146">Configure user provisioning</span></span>

<span data-ttu-id="a30ee-147">Tooenable Azure AD 사용자가 toolog SCC LifeCycle에 주문 하 고에서 SCC LifeCycle에 이들 프로 비전 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a30ee-147">In order tooenable Azure AD users toolog into SCC LifeCycle, they must be provisioned into SCC LifeCycle.</span></span> <span data-ttu-id="a30ee-148">사용자에 대 한 있습니다 tooconfigure tooSCC 수명 주기를 프로 비전 작업 항목이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a30ee-148">There is no action item for you tooconfigure user provisioning tooSCC LifeCycle.</span></span>

<span data-ttu-id="a30ee-149">SCC LifeCycle에 할당 된 사용자 시도 toolog 때 필요한 경우 SCC LifeCycle 계정이 자동으로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a30ee-149">When an assigned user tries toolog into SCC LifeCycle, an SCC LifeCycle account is automatically created if necessary.</span></span>

>[!NOTE]
><span data-ttu-id="a30ee-150">다른 SCC LifeCycle 사용자 계정 만들기 도구를 사용할 수 있습니다 또는 AAD 사용자 계정을 tooprovision SCC LifeCycle에서 제공 된 Api입니다.</span><span class="sxs-lookup"><span data-stu-id="a30ee-150">You can use any other SCC LifeCycle user account creation tools or APIs provided by SCC LifeCycle tooprovision AAD user accounts.</span></span>
> 
> 

## <a name="assign-users"></a><span data-ttu-id="a30ee-151">사용자 할당</span><span class="sxs-lookup"><span data-stu-id="a30ee-151">Assign users</span></span>
<span data-ttu-id="a30ee-152">tootest 구성에 tooallow 할당 하 여 응용 프로그램 액세스 tooit를 사용 하 여 원하는 toogrant hello Azure AD 사용자가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a30ee-152">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="a30ee-153">**tooassign 사용자 tooSCC 수명 주기 단계를 수행 하는 hello를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="a30ee-153">**tooassign users tooSCC LifeCycle, perform hello following steps:**</span></span>

1. <span data-ttu-id="a30ee-154">Azure 클래식 포털 hello 테스트 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a30ee-154">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="a30ee-155">Hello에 * * SCC LifeCycle * * 응용 프로그램 통합 페이지에서 클릭 **사용자 할당**합니다.</span><span class="sxs-lookup"><span data-stu-id="a30ee-155">On hello **SCC LifeCycle **application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="a30ee-156">![사용자 할당](./media/active-directory-saas-scc-lifecycle-tutorial/IC794126.png "사용자 할당")</span><span class="sxs-lookup"><span data-stu-id="a30ee-156">![Assign Users](./media/active-directory-saas-scc-lifecycle-tutorial/IC794126.png "Assign Users")</span></span>
3. <span data-ttu-id="a30ee-157">테스트 사용자 선택, 클릭 **할당**, 클릭 하 고 **예** tooconfirm 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="a30ee-157">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
    <span data-ttu-id="a30ee-158">![예](./media/active-directory-saas-scc-lifecycle-tutorial/IC767830.png "예")</span><span class="sxs-lookup"><span data-stu-id="a30ee-158">![Yes](./media/active-directory-saas-scc-lifecycle-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="a30ee-159">SSO 설정 tootest 원하는 hello 액세스 패널을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a30ee-159">If you want tootest your SSO settings, open hello Access Panel.</span></span> <span data-ttu-id="a30ee-160">액세스 패널 hello에 대 한 자세한 내용은 참조 하십시오. [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a30ee-160">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

