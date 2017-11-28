---
title: "자습서: TOPdesk - Secure와 Azure Active Directory 통합 | Microsoft Docs"
description: "자세한 내용은 방법 toouse TOPdesk-Azure Active Directory tooenable single sign on, 자동화 된 프로 비전 등을 사용 하 여 보안!입니다."
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 8e149d2d-7849-48ec-9993-31f4ade5fdb4
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 10fe420d1691c2845b89c779486ffd6fcd736432
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-topdesk---secure"></a><span data-ttu-id="010f7-103">자습서: TOPdesk - Secure와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="010f7-103">Tutorial: Azure Active Directory integration with TOPdesk - Secure</span></span>
<span data-ttu-id="010f7-104">hello이이 자습서는 Azure와 TOPdesk tooshow hello 통합-보안을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="010f7-104">hello objective of this tutorial is tooshow hello integration of Azure and TOPdesk - Secure.</span></span>  
<span data-ttu-id="010f7-105">이 자습서에 설명 된 hello 시나리오 다음 항목 hello 이미 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="010f7-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="010f7-106">유효한 Azure 구독</span><span class="sxs-lookup"><span data-stu-id="010f7-106">A valid Azure subscription</span></span>
* <span data-ttu-id="010f7-107">TOPdesk - Secure Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="010f7-107">A TOPdesk - Secure single sign-on enabled subscription</span></span>

<span data-ttu-id="010f7-108">Hello Azure AD 사용자를이 자습서를 완료 한 후 지정한 tooTOPdesk-보안가 topdesk-Secure 회사 사이트 (서비스 공급자에서 시작 된 로그온)에서 hello 응용 프로그램에 수 toosingle 로그인 이거나 hello를 사용 하 여 [소개 액세스 패널 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="010f7-108">After completing this tutorial, hello Azure AD users you have assigned tooTOPdesk - Secure will be able toosingle sign into hello application at your TOPdesk - Secure company site (service provider initiated sign on), or using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="010f7-109">이 자습서에 설명 된 hello 시나리오 hello 빌딩 블록을 다음으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="010f7-109">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

1. <span data-ttu-id="010f7-110">TOPdesk-Secure에 대 한 hello 응용 프로그램 통합 사용</span><span class="sxs-lookup"><span data-stu-id="010f7-110">Enabling hello application integration for TOPdesk - Secure</span></span>
2. <span data-ttu-id="010f7-111">Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="010f7-111">Configuring single sign-on</span></span>
3. <span data-ttu-id="010f7-112">사용자 프로비전 구성</span><span class="sxs-lookup"><span data-stu-id="010f7-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="010f7-113">사용자 할당</span><span class="sxs-lookup"><span data-stu-id="010f7-113">Assigning users</span></span>

<span data-ttu-id="010f7-114">![시나리오](./media/active-directory-saas-topdesk-secure-tutorial/IC790596.png "시나리오")</span><span class="sxs-lookup"><span data-stu-id="010f7-114">![Scenario](./media/active-directory-saas-topdesk-secure-tutorial/IC790596.png "Scenario")</span></span>

## <a name="enabling-hello-application-integration-for-topdesk---secure"></a><span data-ttu-id="010f7-115">TOPdesk-Secure에 대 한 hello 응용 프로그램 통합 사용</span><span class="sxs-lookup"><span data-stu-id="010f7-115">Enabling hello application integration for TOPdesk - Secure</span></span>
<span data-ttu-id="010f7-116">hello이이 섹션의 목적은 toooutline 어떻게 TOPdesk-Secure에 대 한 tooenable hello 응용 프로그램 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="010f7-116">hello objective of this section is toooutline how tooenable hello application integration for TOPdesk - Secure.</span></span>

### <a name="tooenable-hello-application-integration-for-topdesk---secure-perform-hello-following-steps"></a><span data-ttu-id="010f7-117">TOPdesk-Secure에 tooenable hello 응용 프로그램 통합 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="010f7-117">tooenable hello application integration for TOPdesk - Secure, perform hello following steps:</span></span>
1. <span data-ttu-id="010f7-118">Hello hello 왼쪽된 탐색 창에서 Azure 클래식 포털에서에서 클릭 **Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="010f7-118">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="010f7-119">![Active Directory](./media/active-directory-saas-topdesk-secure-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="010f7-119">![Active Directory](./media/active-directory-saas-topdesk-secure-tutorial/IC700993.png "Active Directory")</span></span>

2. <span data-ttu-id="010f7-120">Hello에서 **디렉터리** 목록, 선택 hello 디렉터리 tooenable 디렉터리 통합을 구하려는 합니다.</span><span class="sxs-lookup"><span data-stu-id="010f7-120">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="010f7-121">tooopen hello 응용 프로그램 보기 hello 디렉터리 보기에서 클릭 **응용 프로그램** hello 상단 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="010f7-121">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    <span data-ttu-id="010f7-122">![응용 프로그램](./media/active-directory-saas-topdesk-secure-tutorial/IC700994.png "응용 프로그램")</span><span class="sxs-lookup"><span data-stu-id="010f7-122">![Applications](./media/active-directory-saas-topdesk-secure-tutorial/IC700994.png "Applications")</span></span>

4. <span data-ttu-id="010f7-123">클릭 **추가** hello hello 페이지 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="010f7-123">Click **Add** at hello bottom of hello page.</span></span>
   
    <span data-ttu-id="010f7-124">![응용 프로그램 추가](./media/active-directory-saas-topdesk-secure-tutorial/IC749321.png "응용 프로그램 추가")</span><span class="sxs-lookup"><span data-stu-id="010f7-124">![Add application](./media/active-directory-saas-topdesk-secure-tutorial/IC749321.png "Add application")</span></span>

5. <span data-ttu-id="010f7-125">Hello에 **하 신 toodo 원하는** 대화 상자에서 클릭 **hello 갤러리에서 응용 프로그램 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="010f7-125">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    <span data-ttu-id="010f7-126">![갤러리에서 응용 프로그램 추가](./media/active-directory-saas-topdesk-secure-tutorial/IC749322.png "갤러리에서 응용 프로그램 추가")</span><span class="sxs-lookup"><span data-stu-id="010f7-126">![Add an application from gallerry](./media/active-directory-saas-topdesk-secure-tutorial/IC749322.png "Add an application from gallerry")</span></span>

6. <span data-ttu-id="010f7-127">Hello에 **검색 상자**, 형식 **TOPdesk-Secure**합니다.</span><span class="sxs-lookup"><span data-stu-id="010f7-127">In hello **search box**, type **TOPdesk - Secure**.</span></span>
   
    <span data-ttu-id="010f7-128">![응용 프로그램 갤러리](./media/active-directory-saas-topdesk-secure-tutorial/IC790597.png "응용 프로그램 갤러리")</span><span class="sxs-lookup"><span data-stu-id="010f7-128">![Application Gallery](./media/active-directory-saas-topdesk-secure-tutorial/IC790597.png "Application Gallery")</span></span>

7. <span data-ttu-id="010f7-129">Hello 결과 창에서 선택 **TOPdesk-Secure**, 클릭 하 고 **완료** tooadd hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="010f7-129">In hello results pane, select **TOPdesk - Secure**, and then click **Complete** tooadd hello application.</span></span>
   
    <span data-ttu-id="010f7-130">![TOPdesk - Secure](./media/active-directory-saas-topdesk-secure-tutorial/IC791933.png "TOPdesk - Secure")</span><span class="sxs-lookup"><span data-stu-id="010f7-130">![TOPdesk - Secure](./media/active-directory-saas-topdesk-secure-tutorial/IC791933.png "TOPdesk - Secure")</span></span>

## <a name="configuring-single-sign-on"></a><span data-ttu-id="010f7-131">Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="010f7-131">Configuring single sign-on</span></span>
<span data-ttu-id="010f7-132">hello이이 섹션의 목적은 toooutline 어떻게 tooenable 사용자 tooauthenticate tooTOPdesk-hello SAML 프로토콜 기반의 페더레이션을 사용 하 여 Azure AD에서 자신의 계정으로 보안을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="010f7-132">hello objective of this section is toooutline how tooenable users tooauthenticate tooTOPdesk - Secure with their account in Azure AD using federation based on hello SAML protocol.</span></span>  
<span data-ttu-id="010f7-133">구성 single sign on TOPdesk-Secure에 대 한 하려면 로고 아이콘 파일을 tooupload 합니다.</span><span class="sxs-lookup"><span data-stu-id="010f7-133">Configuring single sign-on for TOPdesk - Secure requires you tooupload a logo icon file.</span></span> <span data-ttu-id="010f7-134">tooget hello 아이콘 파일 연락처 hello TOPdesk 지원 팀입니다.</span><span class="sxs-lookup"><span data-stu-id="010f7-134">tooget hello icon file, contact hello TOPdesk support team.</span></span>

### <a name="tooconfigure-single-sign-on-perform-hello-following-steps"></a><span data-ttu-id="010f7-135">tooconfigure 단일 로그온 hello 다음 단계를 수행 하십시오.</span><span class="sxs-lookup"><span data-stu-id="010f7-135">tooconfigure single sign-on, perform hello following steps:</span></span>
1. <span data-ttu-id="010f7-136">Tooyour 로그온 **TOPdesk-Secure** 회사 사이트에 관리자 권한으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="010f7-136">Sign on tooyour **TOPdesk - Secure** company site as an administrator.</span></span>
2. <span data-ttu-id="010f7-137">Hello에 **TOPdesk** 메뉴를 클릭 하 여 **설정을**합니다.</span><span class="sxs-lookup"><span data-stu-id="010f7-137">In hello **TOPdesk** menu, click **Settings**.</span></span>
   
    <span data-ttu-id="010f7-138">![설정](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "설정")</span><span class="sxs-lookup"><span data-stu-id="010f7-138">![Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Settings")</span></span>

3. <span data-ttu-id="010f7-139">**로그인 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="010f7-139">Click **Login Settings**.</span></span>
   
    <span data-ttu-id="010f7-140">![로그인 설정](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "로그인 설정")</span><span class="sxs-lookup"><span data-stu-id="010f7-140">![Login Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Login Settings")</span></span>

4. <span data-ttu-id="010f7-141">Hello 확장 **로그인 설정** 메뉴를 차례로 클릭 **일반**합니다.</span><span class="sxs-lookup"><span data-stu-id="010f7-141">Expand hello **Login Settings** menu, and then click **General**.</span></span>
   
    <span data-ttu-id="010f7-142">![일반](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "일반")</span><span class="sxs-lookup"><span data-stu-id="010f7-142">![General](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "General")</span></span>

5. <span data-ttu-id="010f7-143">Hello에 **Secure** hello의 섹션 **SAML 로그인** 구성 섹션에서 단계를 수행 하는 hello를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="010f7-143">In hello **Secure** section of hello **SAML login** configuration section, perform hello following steps:</span></span>
   
    <span data-ttu-id="010f7-144">![기술 설정](./media/active-directory-saas-topdesk-secure-tutorial/IC790855.png "기술 설정")</span><span class="sxs-lookup"><span data-stu-id="010f7-144">![Technical Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790855.png "Technical Settings")</span></span>
   
    <span data-ttu-id="010f7-145">a.</span><span class="sxs-lookup"><span data-stu-id="010f7-145">a.</span></span> <span data-ttu-id="010f7-146">클릭 **다운로드** toodownload hello 공용 메타 데이터 파일을 한 다음 컴퓨터에 로컬로 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="010f7-146">Click **Download** toodownload hello public metadata file, and then save it locally on your computer.</span></span>
   
    <span data-ttu-id="010f7-147">b.</span><span class="sxs-lookup"><span data-stu-id="010f7-147">b.</span></span> <span data-ttu-id="010f7-148">Hello 메타 데이터 파일을 열고 찾은 후 hello **AssertionConsumerService** 노드.</span><span class="sxs-lookup"><span data-stu-id="010f7-148">Open hello metadata file, and then locate hello **AssertionConsumerService** node.</span></span>
    
    <span data-ttu-id="010f7-149">![Assertion Consumer Service](./media/active-directory-saas-topdesk-secure-tutorial/IC790856.png "Assertion Consumer Service")</span><span class="sxs-lookup"><span data-stu-id="010f7-149">![Assertion Consumer Service](./media/active-directory-saas-topdesk-secure-tutorial/IC790856.png "Assertion Consumer Service")</span></span>
   
    <span data-ttu-id="010f7-150">c.</span><span class="sxs-lookup"><span data-stu-id="010f7-150">c.</span></span> <span data-ttu-id="010f7-151">복사 hello **AssertionConsumerService** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="010f7-151">Copy hello **AssertionConsumerService** value.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="010f7-152">Hello에 대 한 값 hello 필요 합니다 **앱 URL 구성** 이 자습서의 뒷부분에 나오는 섹션.</span><span class="sxs-lookup"><span data-stu-id="010f7-152">You will need hello value in hello **Configure App URL** section later in this tutorial.</span></span>
    > 
    > 

6. <span data-ttu-id="010f7-153">다른 웹 브라우저 창에서 **Azure 클래식 포털** 에 관리자 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="010f7-153">In a different web browser window, log into your **Azure classic portal** as an administrator.</span></span>

7. <span data-ttu-id="010f7-154">Hello에 **TOPdesk-Secure** 응용 프로그램 통합 페이지에서 클릭 **single sign on 구성** tooopen hello * * Single Sign-on 구성 * * 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="010f7-154">On hello **TOPdesk - Secure** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On ** dialog.</span></span>
   
    <span data-ttu-id="010f7-155">![Single Sign-On 구성](./media/active-directory-saas-topdesk-secure-tutorial/IC790602.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="010f7-155">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790602.png "Configure Single Sign-On")</span></span>

8. <span data-ttu-id="010f7-156">Hello에 **방법을 tooTOPdesk-에 toosign 사용자 같은 보안** 페이지에서 **Microsoft Azure AD Single Sign-on**, 클릭 하 고 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="010f7-156">On hello **How would you like users toosign on tooTOPdesk - Secure** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="010f7-157">![Single Sign-On 구성](./media/active-directory-saas-topdesk-secure-tutorial/IC790603.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="010f7-157">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790603.png "Configure Single Sign-On")</span></span>

9. <span data-ttu-id="010f7-158">Hello에 **앱 URL 구성** 페이지 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="010f7-158">On hello **Configure App URL** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="010f7-159">![앱 URL 구성](./media/active-directory-saas-topdesk-secure-tutorial/IC790604.png "앱 URL 구성")</span><span class="sxs-lookup"><span data-stu-id="010f7-159">![Configure App URL](./media/active-directory-saas-topdesk-secure-tutorial/IC790604.png "Configure App URL")</span></span>
   
    <span data-ttu-id="010f7-160">a.</span><span class="sxs-lookup"><span data-stu-id="010f7-160">a.</span></span> <span data-ttu-id="010f7-161">Hello에 **TOPdesk-Secure 로그온 URL** 사용자 toosign TOPdesk-Secure 응용 프로그램에 사용 하는 형식 hello URL 텍스트 상자 (예:: "*https://qssolutions.topdesk.net*").</span><span class="sxs-lookup"><span data-stu-id="010f7-161">In hello **TOPdesk - Secure Sign On URL** textbox, type hello URL used by your users toosign into your TOPdesk - Secure application (e.g.: "*https://qssolutions.topdesk.net*").</span></span>
   
    <span data-ttu-id="010f7-162">b.</span><span class="sxs-lookup"><span data-stu-id="010f7-162">b.</span></span> <span data-ttu-id="010f7-163">Hello에 **TOPdesk – Public 회신 URL** 텍스트 붙여넣기 hello **TOPdesk-Secure AssertionConsumerService URL** (예:: "*https://qssolutions.topdesk.net/tas/public/login/saml*")</span><span class="sxs-lookup"><span data-stu-id="010f7-163">In hello **TOPdesk – Public Reply URL** textbox, paste hello **TOPdesk - Secure AssertionConsumerService URL** (e.g.: "*https://qssolutions.topdesk.net/tas/public/login/saml*")</span></span>
   
    <span data-ttu-id="010f7-164">c.</span><span class="sxs-lookup"><span data-stu-id="010f7-164">c.</span></span> <span data-ttu-id="010f7-165">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="010f7-165">Click **Next**.</span></span>

10. <span data-ttu-id="010f7-166">Hello에 **TOPdesk-Secure에서 single sign on 구성** 페이지, toodownload 메타 데이터 파일을 클릭 하 여 **메타 데이터 다운로드**, hello 파일을 컴퓨터에 로컬로 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="010f7-166">On hello **Configure single sign-on at TOPdesk - Secure** page, toodownload your metadata file, click **Download metadata**, and then save hello file locally on your computer.</span></span>
    
    <span data-ttu-id="010f7-167">![Single Sign-On 구성](./media/active-directory-saas-topdesk-secure-tutorial/IC790605.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="010f7-167">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790605.png "Configure Single Sign-On")</span></span>

11. <span data-ttu-id="010f7-168">toocreate 인증서 파일을 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="010f7-168">toocreate a certificate file, perform hello following steps:</span></span>
    
    <span data-ttu-id="010f7-169">![인증서](./media/active-directory-saas-topdesk-secure-tutorial/IC790606.png "인증서")</span><span class="sxs-lookup"><span data-stu-id="010f7-169">![Certificate](./media/active-directory-saas-topdesk-secure-tutorial/IC790606.png "Certificate")</span></span>
    
    <span data-ttu-id="010f7-170">a.</span><span class="sxs-lookup"><span data-stu-id="010f7-170">a.</span></span> <span data-ttu-id="010f7-171">Hello open 다운로드 한 메타 데이터 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="010f7-171">Open hello downloaded metadata file.</span></span>
    <span data-ttu-id="010f7-172">b.</span><span class="sxs-lookup"><span data-stu-id="010f7-172">b.</span></span> <span data-ttu-id="010f7-173">Hello 확장 **RoleDescriptor** 노드에 **xsi: type** 의 **fed: ApplicationServiceType**합니다.</span><span class="sxs-lookup"><span data-stu-id="010f7-173">Expand hello **RoleDescriptor** node that has a **xsi:type** of **fed:ApplicationServiceType**.</span></span>
    <span data-ttu-id="010f7-174">c.</span><span class="sxs-lookup"><span data-stu-id="010f7-174">c.</span></span> <span data-ttu-id="010f7-175">Hello의 hello 값을 복사 **X509Certificate** 노드.</span><span class="sxs-lookup"><span data-stu-id="010f7-175">Copy hello value of hello **X509Certificate** node.</span></span>
    <span data-ttu-id="010f7-176">d.</span><span class="sxs-lookup"><span data-stu-id="010f7-176">d.</span></span> <span data-ttu-id="010f7-177">복사 저장 hello **X509Certificate** 파일에서 컴퓨터에 로컬로 값입니다.</span><span class="sxs-lookup"><span data-stu-id="010f7-177">Save hello copied **X509Certificate** value locally on your computer in a file.</span></span>

12. <span data-ttu-id="010f7-178">Topdesk-Secure 회사 사이트에 hello **TOPdesk** 메뉴를 클릭 하 여 **설정을**합니다.</span><span class="sxs-lookup"><span data-stu-id="010f7-178">On your TOPdesk - Secure company site, in hello **TOPdesk** menu, click **Settings**.</span></span>
    
    <span data-ttu-id="010f7-179">![설정](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "설정")</span><span class="sxs-lookup"><span data-stu-id="010f7-179">![Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Settings")</span></span>

13. <span data-ttu-id="010f7-180">**로그인 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="010f7-180">Click **Login Settings**.</span></span>
    
    <span data-ttu-id="010f7-181">![로그인 설정](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "로그인 설정")</span><span class="sxs-lookup"><span data-stu-id="010f7-181">![Login Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Login Settings")</span></span>

14. <span data-ttu-id="010f7-182">Hello 확장 **로그인 설정** 메뉴를 차례로 클릭 **일반**합니다.</span><span class="sxs-lookup"><span data-stu-id="010f7-182">Expand hello **Login Settings** menu, and then click **General**.</span></span>
    
    <span data-ttu-id="010f7-183">![일반](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "일반")</span><span class="sxs-lookup"><span data-stu-id="010f7-183">![General](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "General")</span></span>

15. <span data-ttu-id="010f7-184">Hello에 **공용** 섹션에서 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="010f7-184">In hello **Public** section, click **Add**.</span></span>
    
    <span data-ttu-id="010f7-185">![추가](./media/active-directory-saas-topdesk-secure-tutorial/IC790607.png "추가")</span><span class="sxs-lookup"><span data-stu-id="010f7-185">![Add](./media/active-directory-saas-topdesk-secure-tutorial/IC790607.png "Add")</span></span>

16. <span data-ttu-id="010f7-186">Hello에 **SAML 구성 도우미** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="010f7-186">On hello **SAML configuration assistant** dialog page, perform hello following steps:</span></span>
    
    <span data-ttu-id="010f7-187">![SAML 구성 도우미](./media/active-directory-saas-topdesk-secure-tutorial/IC790608.png "SAML 구성 도우미")</span><span class="sxs-lookup"><span data-stu-id="010f7-187">![SAML Configuration Assistant](./media/active-directory-saas-topdesk-secure-tutorial/IC790608.png "SAML Configuration Assistant")</span></span>
    
    <span data-ttu-id="010f7-188">a.</span><span class="sxs-lookup"><span data-stu-id="010f7-188">a.</span></span> <span data-ttu-id="010f7-189">다운로드 한 메타 데이터 파일 tooupload **페더레이션 메타 데이터**, 클릭 **찾아보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="010f7-189">tooupload your downloaded metadata file, under **Federation Metadata**, click **Browse**.</span></span>

    <span data-ttu-id="010f7-190">b.</span><span class="sxs-lookup"><span data-stu-id="010f7-190">b.</span></span> <span data-ttu-id="010f7-191">인증서 파일 tooupload **Certificate (RSA)**, 클릭 **찾아보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="010f7-191">tooupload your certificate file, under **Certificate (RSA)**, click **Browse**.</span></span>

    <span data-ttu-id="010f7-192">c.</span><span class="sxs-lookup"><span data-stu-id="010f7-192">c.</span></span> <span data-ttu-id="010f7-193">아래에서 hello TOPdesk 지원 팀에서 받은 tooupload hello 로고 파일 **로고 아이콘**, 클릭 **찾아보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="010f7-193">tooupload hello logo file you got from hello TOPdesk support team, under **Logo icon**, click **Browse**.</span></span>

    <span data-ttu-id="010f7-194">d.</span><span class="sxs-lookup"><span data-stu-id="010f7-194">d.</span></span> <span data-ttu-id="010f7-195">Hello에 **사용자 이름 특성** 텍스트 상자에 **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**합니다.</span><span class="sxs-lookup"><span data-stu-id="010f7-195">In hello **User name attribute** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span>

    <span data-ttu-id="010f7-196">e.</span><span class="sxs-lookup"><span data-stu-id="010f7-196">e.</span></span> <span data-ttu-id="010f7-197">Hello에 **표시 이름** 텍스트 상자, 구성에 대 한 이름 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="010f7-197">In hello **Display name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="010f7-198">f.</span><span class="sxs-lookup"><span data-stu-id="010f7-198">f.</span></span> <span data-ttu-id="010f7-199">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="010f7-199">Click **Save**.</span></span>

17. <span data-ttu-id="010f7-200">Azure 클래식 포털 hello에 hello single sign on 구성 확인을 선택한 다음 클릭 **완료** tooclose hello **Single Sign-on 구성** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="010f7-200">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="010f7-201">![Single Sign-On 구성](./media/active-directory-saas-topdesk-secure-tutorial/IC790609.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="010f7-201">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790609.png "Configure Single Sign-On")</span></span>

## <a name="configuring-user-provisioning"></a><span data-ttu-id="010f7-202">사용자 프로비전 구성</span><span class="sxs-lookup"><span data-stu-id="010f7-202">Configuring user provisioning</span></span>
<span data-ttu-id="010f7-203">TOPdesk-에 순서 tooenable Azure AD 사용자가 toolog에서 안전은 프로 비전 해야 TOPdesk-Secure에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="010f7-203">In order tooenable Azure AD users toolog into TOPdesk - Secure, they must be provisioned into TOPdesk - Secure.</span></span>  
<span data-ttu-id="010f7-204">TOPdesk-hello 경우에서 안전한 프로 비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="010f7-204">In hello case of TOPdesk - Secure, provisioning is a manual task.</span></span>

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a><span data-ttu-id="010f7-205">tooconfigure 사용자 프로비저닝, hello 다음 단계를 수행:</span><span class="sxs-lookup"><span data-stu-id="010f7-205">tooconfigure user provisioning, perform hello following steps:</span></span>
1. <span data-ttu-id="010f7-206">Tooyour 로그온 **TOPdesk-Secure** 회사 사이트에서 관리자 권한으로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="010f7-206">Sign on tooyour **TOPdesk - Secure** company site as administrator.</span></span>
2. <span data-ttu-id="010f7-207">Hello 메뉴에서 hello 위에 표시를 클릭 **TOPdesk \> 새로 \> 지원 파일 \> 연산자**합니다.</span><span class="sxs-lookup"><span data-stu-id="010f7-207">In hello menu on hello top, click **TOPdesk \> New \> Support Files \> Operator**.</span></span>
   
    <span data-ttu-id="010f7-208">![연산자](./media/active-directory-saas-topdesk-secure-tutorial/IC790610.png "연산자")</span><span class="sxs-lookup"><span data-stu-id="010f7-208">![Operator](./media/active-directory-saas-topdesk-secure-tutorial/IC790610.png "Operator")</span></span>

3. <span data-ttu-id="010f7-209">Hello에 **New 연산자** 대화 상자에서 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="010f7-209">On hello **New Operator** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="010f7-210">![새로운 연산자](./media/active-directory-saas-topdesk-secure-tutorial/IC790611.png "새로운 연산자")</span><span class="sxs-lookup"><span data-stu-id="010f7-210">![New Operator](./media/active-directory-saas-topdesk-secure-tutorial/IC790611.png "New Operator")</span></span>
   
    <span data-ttu-id="010f7-211">a.</span><span class="sxs-lookup"><span data-stu-id="010f7-211">a.</span></span> <span data-ttu-id="010f7-212">Hello 일반 탭을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="010f7-212">Click hello General tab.</span></span>
   
    <span data-ttu-id="010f7-213">b.</span><span class="sxs-lookup"><span data-stu-id="010f7-213">b.</span></span> <span data-ttu-id="010f7-214">Hello에 **Surname** hello 텍스트 상자 **일반** 섹션 tooprovision 하려는 유효한 Azure Active Directory 계정의 hello 마지막 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="010f7-214">In hello **Surname** textbox of hello **General** section, type hello last name of a valid Azure Active Directory account you want tooprovision.</span></span>
   
    <span data-ttu-id="010f7-215">c.</span><span class="sxs-lookup"><span data-stu-id="010f7-215">c.</span></span> <span data-ttu-id="010f7-216">선택 된 **사이트** hello 계정 hello에 대 한 **위치** 섹션.</span><span class="sxs-lookup"><span data-stu-id="010f7-216">Select a **Site** for hello account in hello **Location** section.</span></span>
   
    <span data-ttu-id="010f7-217">d.</span><span class="sxs-lookup"><span data-stu-id="010f7-217">d.</span></span> <span data-ttu-id="010f7-218">Hello에 **로그인 이름** hello 텍스트 상자 **TOPdesk Login** 섹션에서 사용자에 대 한 로그인 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="010f7-218">In hello **Login Name** textbox of hello **TOPdesk Login** section, type a login name for your user.</span></span>
   
    <span data-ttu-id="010f7-219">e.</span><span class="sxs-lookup"><span data-stu-id="010f7-219">e.</span></span> <span data-ttu-id="010f7-220">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="010f7-220">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="010f7-221">모든 다른 TOPdesk-Secure 사용자 계정 만들기 도구 또는 TOPdesk-에서 제공 된 Api tooprovision AAD 사용자 계정을 보안을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="010f7-221">You can use any other TOPdesk - Secure user account creation tools or APIs provided by TOPdesk - Secure tooprovision AAD user accounts.</span></span>
> 
> 

## <a name="assigning-users"></a><span data-ttu-id="010f7-222">사용자 할당</span><span class="sxs-lookup"><span data-stu-id="010f7-222">Assigning users</span></span>
<span data-ttu-id="010f7-223">tootest 구성에 tooallow 할당 하 여 응용 프로그램 액세스 tooit를 사용 하 여 원하는 toogrant hello Azure AD 사용자가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="010f7-223">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

### <a name="tooassign-users-tootopdesk---secure-perform-hello-following-steps"></a><span data-ttu-id="010f7-224">tooassign 사용자 tooTOPdesk-Secure에 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="010f7-224">tooassign users tooTOPdesk - Secure, perform hello following steps:</span></span>
1. <span data-ttu-id="010f7-225">Azure 클래식 포털 hello 테스트 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="010f7-225">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="010f7-226">Hello에 * * TOPdesk-Secure * * 응용 프로그램 통합 페이지에서 클릭 **사용자 할당**합니다.</span><span class="sxs-lookup"><span data-stu-id="010f7-226">On hello **TOPdesk - Secure **application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="010f7-227">![사용자 할당](./media/active-directory-saas-topdesk-secure-tutorial/IC790612.png "사용자 할당")</span><span class="sxs-lookup"><span data-stu-id="010f7-227">![Assign Users](./media/active-directory-saas-topdesk-secure-tutorial/IC790612.png "Assign Users")</span></span>

3. <span data-ttu-id="010f7-228">테스트 사용자 선택, 클릭 **할당**, 클릭 하 고 **예** tooconfirm 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="010f7-228">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
    <span data-ttu-id="010f7-229">![예](./media/active-directory-saas-topdesk-secure-tutorial/IC767830.png "예")</span><span class="sxs-lookup"><span data-stu-id="010f7-229">![Yes](./media/active-directory-saas-topdesk-secure-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="010f7-230">Single sign on 설정 tootest 원하는 hello 액세스 패널을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="010f7-230">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="010f7-231">액세스 패널 hello에 대 한 자세한 내용은 참조 하십시오. [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="010f7-231">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

