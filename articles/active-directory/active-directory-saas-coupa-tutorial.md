---
title: "자습서: Coupa와 Azure Active Directory 통합 | Microsoft Docs"
description: "어떻게 tooenable Azure Active Directory와 Coupa toouse single sign on, 자동화 된 프로비저닝 및 더에 대해 알아봅니다."
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 47f27746-9057-4b9c-991e-3abf77710f73
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 87e98573718d27d408c886466a374a987f58faa2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-coupa"></a><span data-ttu-id="c4c38-103">자습서: Coupa와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="c4c38-103">Tutorial: Azure Active Directory integration with Coupa</span></span>
<span data-ttu-id="c4c38-104">hello이이 자습서는 Azure와 Coupa tooshow hello 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c38-104">hello objective of this tutorial is tooshow hello integration of Azure and Coupa.</span></span>  
<span data-ttu-id="c4c38-105">이 자습서에 설명 된 hello 시나리오 다음 항목 hello 이미 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c38-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="c4c38-106">유효한 Azure 구독</span><span class="sxs-lookup"><span data-stu-id="c4c38-106">A valid Azure subscription</span></span>
* <span data-ttu-id="c4c38-107">Coupa SSO(Single Sign-On)가 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="c4c38-107">A Coupa single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="c4c38-108">이 자습서를 완료 한 후 hello Azure AD 사용자 tooCoupa 배정 됩니다 hello를 사용 하 여 hello 응용 프로그램에 수 toosingle 로그인 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c38-108">After completing this tutorial, hello Azure AD users you have assigned tooCoupa will be able toosingle sign into hello application using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="c4c38-109">이 자습서에 설명 된 hello 시나리오 hello 빌딩 블록을 다음으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4c38-109">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

* <span data-ttu-id="c4c38-110">Coupa에 대 한 hello 응용 프로그램 통합 사용</span><span class="sxs-lookup"><span data-stu-id="c4c38-110">Enabling hello application integration for Coupa</span></span>
* <span data-ttu-id="c4c38-111">Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="c4c38-111">Configuring single sign-on</span></span>
* <span data-ttu-id="c4c38-112">사용자 프로비전 구성</span><span class="sxs-lookup"><span data-stu-id="c4c38-112">Configuring user provisioning</span></span>
* <span data-ttu-id="c4c38-113">사용자 할당</span><span class="sxs-lookup"><span data-stu-id="c4c38-113">Assigning users</span></span>

<span data-ttu-id="c4c38-114">![시나리오](./media/active-directory-saas-coupa-tutorial/IC791897.png "시나리오")</span><span class="sxs-lookup"><span data-stu-id="c4c38-114">![Scenario](./media/active-directory-saas-coupa-tutorial/IC791897.png "Scenario")</span></span>

## <a name="enable-hello-application-integration-for-coupa"></a><span data-ttu-id="c4c38-115">Coupa에 대 한 hello 응용 프로그램 통합 사용</span><span class="sxs-lookup"><span data-stu-id="c4c38-115">Enable hello application integration for Coupa</span></span>
<span data-ttu-id="c4c38-116">hello이이 섹션의 목적은 toooutline 어떻게 Coupa에 대 한 tooenable hello 응용 프로그램 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c38-116">hello objective of this section is toooutline how tooenable hello application integration for Coupa.</span></span>

<span data-ttu-id="c4c38-117">**Coupa에 대 한 tooenable hello 응용 프로그램 통합 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="c4c38-117">**tooenable hello application integration for Coupa, perform hello following steps:**</span></span>

1. <span data-ttu-id="c4c38-118">Hello hello 왼쪽된 탐색 창에서 Azure 클래식 포털에서에서 클릭 **Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c38-118">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="c4c38-119">![Active Directory](./media/active-directory-saas-coupa-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="c4c38-119">![Active Directory](./media/active-directory-saas-coupa-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="c4c38-120">Hello에서 **디렉터리** 목록, 선택 hello 디렉터리 tooenable 디렉터리 통합을 구하려는 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c38-120">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="c4c38-121">tooopen hello 응용 프로그램 보기 hello 디렉터리 보기에서 클릭 **응용 프로그램** hello 상단 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c38-121">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
   <span data-ttu-id="c4c38-122">![응용 프로그램](./media/active-directory-saas-coupa-tutorial/IC700994.png "응용 프로그램")</span><span class="sxs-lookup"><span data-stu-id="c4c38-122">![Applications](./media/active-directory-saas-coupa-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="c4c38-123">클릭 **추가** hello hello 페이지 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4c38-123">Click **Add** at hello bottom of hello page.</span></span>
   
   <span data-ttu-id="c4c38-124">![응용 프로그램 추가](./media/active-directory-saas-coupa-tutorial/IC749321.png "응용 프로그램 추가")</span><span class="sxs-lookup"><span data-stu-id="c4c38-124">![Add application](./media/active-directory-saas-coupa-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="c4c38-125">Hello에 **하 신 toodo 원하는** 대화 상자에서 클릭 **hello 갤러리에서 응용 프로그램 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c38-125">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
   <span data-ttu-id="c4c38-126">![갤러리에서 응용 프로그램 추가](./media/active-directory-saas-coupa-tutorial/IC749322.png "갤러리에서 응용 프로그램 추가")</span><span class="sxs-lookup"><span data-stu-id="c4c38-126">![Add an application from gallerry](./media/active-directory-saas-coupa-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="c4c38-127">Hello에 **검색 상자**, 형식 **Coupa**합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c38-127">In hello **search box**, type **Coupa**.</span></span>
   
   <span data-ttu-id="c4c38-128">![응용 프로그램 갤러리](./media/active-directory-saas-coupa-tutorial/IC791898.png "응용 프로그램 갤러리")</span><span class="sxs-lookup"><span data-stu-id="c4c38-128">![Application Gallery](./media/active-directory-saas-coupa-tutorial/IC791898.png "Application Gallery")</span></span>
7. <span data-ttu-id="c4c38-129">Hello 결과 창에서 선택 **Coupa**, 클릭 하 고 **완료** tooadd hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="c4c38-129">In hello results pane, select **Coupa**, and then click **Complete** tooadd hello application.</span></span>
   
   <span data-ttu-id="c4c38-130">![Coupa](./media/active-directory-saas-coupa-tutorial/IC791899.png "Coupa")</span><span class="sxs-lookup"><span data-stu-id="c4c38-130">![Coupa](./media/active-directory-saas-coupa-tutorial/IC791899.png "Coupa")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="c4c38-131">Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="c4c38-131">Configure single sign-on</span></span>

<span data-ttu-id="c4c38-132">hello이이 섹션의 목적은 toooutline 페더레이션을 사용 하 여 Azure AD에서 자신의 계정으로 tooenable 사용자 tooauthenticate tooCoupa hello SAML 프로토콜에 따라 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="c4c38-132">hello objective of this section is toooutline how tooenable users tooauthenticate tooCoupa with their account in Azure AD using federation based on hello SAML protocol.</span></span>  

<span data-ttu-id="c4c38-133">Single sign on Coupa에 대 한 구성 하려면 인증서에서 지문 값 tooretrieve 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c38-133">Configuring single sign-on for Coupa requires you tooretrieve a thumbprint value from a certificate.</span></span> <span data-ttu-id="c4c38-134">이 절차에 익숙하지 않은 경우 참조 [어떻게 tooretrieve 인증서의 지문 값](http://youtu.be/YKQF266SAxI)합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c38-134">If you are not familiar with this procedure, see [How tooretrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span></span>

<span data-ttu-id="c4c38-135">**tooconfigure 단일 로그온 hello 다음 단계를 수행 하십시오.**</span><span class="sxs-lookup"><span data-stu-id="c4c38-135">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="c4c38-136">관리자 권한으로 Coupa 회사 사이트 tooyour에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c38-136">Sign on tooyour Coupa company site as an administrator.</span></span>
2. <span data-ttu-id="c4c38-137">너무 이동**설치 \> 보안 제어**합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c38-137">Go too**Setup \> Security Control**.</span></span>
   
   <span data-ttu-id="c4c38-138">![보안 제어](./media/active-directory-saas-coupa-tutorial/IC791900.png "보안 제어")</span><span class="sxs-lookup"><span data-stu-id="c4c38-138">![Security Controls](./media/active-directory-saas-coupa-tutorial/IC791900.png "Security Controls")</span></span>
3. <span data-ttu-id="c4c38-139">toodownload hello Coupa 메타 데이터 파일 tooyour 컴퓨터 클릭 **다운로드 하 여 SP 메타 데이터를 가져와**합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c38-139">toodownload hello Coupa metadata file tooyour computer, click **Download and import SP metadata**.</span></span>
   
   <span data-ttu-id="c4c38-140">![Coupa SP 메타데이터](./media/active-directory-saas-coupa-tutorial/IC791901.png "Coupa SP 메타데이터")</span><span class="sxs-lookup"><span data-stu-id="c4c38-140">![Coupa SP metadata](./media/active-directory-saas-coupa-tutorial/IC791901.png "Coupa SP metadata")</span></span>
4. <span data-ttu-id="c4c38-141">다른 브라우저 창에서 toohello Azure 클래식 포털에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c38-141">In a different browser window, sign on toohello Azure classic portal.</span></span>
5. <span data-ttu-id="c4c38-142">Hello에 **Coupa** 응용 프로그램 통합 페이지에서 클릭 **single sign on 구성** tooopen hello **Single Sign-on 구성** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="c4c38-142">On hello **Coupa** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="c4c38-143">![Single Sign-On 구성](./media/active-directory-saas-coupa-tutorial/IC791902.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="c4c38-143">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791902.png "Configure Single Sign-On")</span></span>
6. <span data-ttu-id="c4c38-144">Hello에 **어떻게 tooCoupa에 사용자가 toosign 보 시겠습니까** 페이지에서 **Microsoft Azure AD Single Sign-on**, 클릭 하 고 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c38-144">On hello **How would you like users toosign on tooCoupa** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="c4c38-145">![Single Sign-On 구성](./media/active-directory-saas-coupa-tutorial/IC791903.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="c4c38-145">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791903.png "Configure Single Sign-On")</span></span>
7. <span data-ttu-id="c4c38-146">Hello에 **앱 URL 구성** 페이지 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c38-146">On hello **Configure App URL** page, perform hello following steps:</span></span>
   
   <span data-ttu-id="c4c38-147">![앱 URL 구성](./media/active-directory-saas-coupa-tutorial/IC791904.png "앱 URL 구성")</span><span class="sxs-lookup"><span data-stu-id="c4c38-147">![Configure App URL](./media/active-directory-saas-coupa-tutorial/IC791904.png "Configure App URL")</span></span>   
   1. <span data-ttu-id="c4c38-148">Hello에 **로그온 URL** tooyour Coupa 응용 프로그램에서 사용자가 toosign 프로그램에서 사용 하는 URL 입력 텍스트 (예:: "*http://company.Coupa.com*").</span><span class="sxs-lookup"><span data-stu-id="c4c38-148">In hello **Sign On URL** textbox, type URL used by your users toosign on tooyour Coupa application (e.g.: “*http://company.Coupa.com*”).</span></span>
   2. <span data-ttu-id="c4c38-149">다운로드 한 Coupa 메타 데이터 파일을 열고 hello 복사 **AssertionConsumerService index/URL**합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c38-149">Open your downloaded Coupa metadata file, and then copy hello **AssertionConsumerService index/URL**.</span></span>
   3. <span data-ttu-id="c4c38-150">Hello에 **Coupa 회신 URL** 텍스트 붙여넣기 hello **AssertionConsumerService index/URL** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c4c38-150">In hello **Coupa Reply URL** textbox, paste hello **AssertionConsumerService index/URL** value.</span></span>
   4. <span data-ttu-id="c4c38-151">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="c4c38-151">Click **Next**.</span></span>
8. <span data-ttu-id="c4c38-152">Hello에 **Coupa에서 single sign on 구성** 페이지, toodownload 메타 데이터 파일을 클릭 하 여 **메타 데이터 다운로드**, hello 파일을 컴퓨터에 로컬로 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c38-152">On hello **Configure single sign-on at Coupa** page, toodownload your metadata file, click **Download metadata**, and then save hello file locally on your computer.</span></span>
   
   <span data-ttu-id="c4c38-153">![Single Sign-On 구성](./media/active-directory-saas-coupa-tutorial/IC791905.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="c4c38-153">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791905.png "Configure Single Sign-On")</span></span>
9. <span data-ttu-id="c4c38-154">Hello Coupa 회사 사이트에서 이동 너무**설치 \> 보안 제어**합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c38-154">On hello Coupa company site, go too**Setup \> Security Control**.</span></span>
   
   <span data-ttu-id="c4c38-155">![보안 제어](./media/active-directory-saas-coupa-tutorial/IC791900.png "보안 제어")</span><span class="sxs-lookup"><span data-stu-id="c4c38-155">![Security Controls](./media/active-directory-saas-coupa-tutorial/IC791900.png "Security Controls")</span></span>
10. <span data-ttu-id="c4c38-156">Hello에 **Coupa 자격 증명을 사용 하 여 로그인** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c38-156">In hello **Log in using Coupa credentials** section, perform hello following steps:</span></span>  

   <span data-ttu-id="c4c38-157">![Coupa 자격 증명을 사용하여 로그인](./media/active-directory-saas-coupa-tutorial/IC791906.png "Coupa 자격 증명을 사용하여 로그인")</span><span class="sxs-lookup"><span data-stu-id="c4c38-157">![Log in using Coupa credentials](./media/active-directory-saas-coupa-tutorial/IC791906.png "Log in using Coupa credentials")</span></span> 
   1. <span data-ttu-id="c4c38-158">**SAML을 사용하여 로그인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c38-158">Select **Log in using SAML**.</span></span>
   2. <span data-ttu-id="c4c38-159">클릭 **찾아보기** tooupload 다운로드 한 Azure Active 메타 데이터 파일.</span><span class="sxs-lookup"><span data-stu-id="c4c38-159">Click **Browse** tooupload your downloaded Azure Active metadata file.</span></span>
   3. <span data-ttu-id="c4c38-160">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c38-160">Click **Save**.</span></span>
11. <span data-ttu-id="c4c38-161">Azure 클래식 포털 hello에 hello single sign on 구성 확인을 선택한 다음 클릭 **완료** tooclose hello **Single Sign-on 구성** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="c4c38-161">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
    
   <span data-ttu-id="c4c38-162">![Single Sign-On 구성](./media/active-directory-saas-coupa-tutorial/IC791907.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="c4c38-162">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791907.png "Configure Single Sign-On")</span></span>
    
## <a name="configure-user-provisioning"></a><span data-ttu-id="c4c38-163">사용자 프로비전 구성</span><span class="sxs-lookup"><span data-stu-id="c4c38-163">Configure user provisioning</span></span>

<span data-ttu-id="c4c38-164">Tooenable Azure AD 사용자가 toolog Coupa에 주문 하 고에 Coupa에 이들 프로 비전 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c38-164">In order tooenable Azure AD users toolog into Coupa, they must be provisioned into Coupa.</span></span>  

* <span data-ttu-id="c4c38-165">Hello Coupa의 경우에서 프로 비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="c4c38-165">In hello case of Coupa, provisioning is a manual task.</span></span>

<span data-ttu-id="c4c38-166">**tooconfigure 사용자 프로비저닝, hello 다음 단계를 수행:**</span><span class="sxs-lookup"><span data-stu-id="c4c38-166">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="c4c38-167">Tooyour 로그인 **Coupa** 회사 사이트에서 관리자 권한으로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c38-167">Log in tooyour **Coupa** company site as administrator.</span></span>
2. <span data-ttu-id="c4c38-168">Hello 메뉴에서 hello 위에 표시를 클릭 **설치**, 클릭 하 고 **사용자**합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c38-168">In hello menu on hello top, click **Setup**, and then click **Users**.</span></span>
   
   <span data-ttu-id="c4c38-169">![사용자](./media/active-directory-saas-coupa-tutorial/IC791908.png "사용자")</span><span class="sxs-lookup"><span data-stu-id="c4c38-169">![Users](./media/active-directory-saas-coupa-tutorial/IC791908.png "Users")</span></span>
3. <span data-ttu-id="c4c38-170">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c38-170">Click **Create**.</span></span>
   
   <span data-ttu-id="c4c38-171">![사용자 만들기](./media/active-directory-saas-coupa-tutorial/IC791909.png "사용자 만들기")</span><span class="sxs-lookup"><span data-stu-id="c4c38-171">![Create Users](./media/active-directory-saas-coupa-tutorial/IC791909.png "Create Users")</span></span>
4. <span data-ttu-id="c4c38-172">Hello에 **사용자 만들** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c38-172">In hello **User Create** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="c4c38-173">![사용자 세부 정보](./media/active-directory-saas-coupa-tutorial/IC791910.png "사용자 세부 정보")</span><span class="sxs-lookup"><span data-stu-id="c4c38-173">![User Details](./media/active-directory-saas-coupa-tutorial/IC791910.png "User Details")</span></span>
   
   1. <span data-ttu-id="c4c38-174">형식 hello **로그인**, **이름**, **성**, **Single Sign-on ID**, **전자 메일** 의 특성을 유효한 Azure Active Directory 계정을 tooprovision hello에 관련 텍스트 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="c4c38-174">Type hello **Login**, **First name**, **Last Name**, **Single Sign-On ID**, **Email** attributes of a valid Azure Active Directory account you want tooprovision into hello related textboxes.</span></span>
   2. <span data-ttu-id="c4c38-175">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c38-175">Click **Create**.</span></span>   
   >[!NOTE]
   ><span data-ttu-id="c4c38-176">따라 활성화 hello Azure Active Directory 계정 소유자 링크 tooconfirm hello 계정 사용 하 여 전자 메일을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4c38-176">hello Azure Active Directory account holder will get an email with a link tooconfirm hello account before it becomes active.</span></span> 
   > 

>[!NOTE]
><span data-ttu-id="c4c38-177">다른 Coupa 사용자 계정 만들기 도구를 사용할 수 있습니다 또는 AAD 사용자 계정을 tooprovision Coupa에서 제공 된 Api입니다.</span><span class="sxs-lookup"><span data-stu-id="c4c38-177">You can use any other Coupa user account creation tools or APIs provided by Coupa tooprovision AAD user accounts.</span></span> 
> 

## <a name="assign-users"></a><span data-ttu-id="c4c38-178">사용자 할당</span><span class="sxs-lookup"><span data-stu-id="c4c38-178">Assign users</span></span>
<span data-ttu-id="c4c38-179">tootest 구성에 tooallow 할당 하 여 응용 프로그램 액세스 tooit를 사용 하 여 원하는 toogrant hello Azure AD 사용자가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c38-179">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="c4c38-180">**tooassign 사용자 tooCoupa hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="c4c38-180">**tooassign users tooCoupa, perform hello following steps:**</span></span>

1. <span data-ttu-id="c4c38-181">Azure 클래식 포털 hello 테스트 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c4c38-181">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="c4c38-182">Hello에 * * Coupa * * 응용 프로그램 통합 페이지에서 클릭 **사용자 할당**합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c38-182">On hello **Coupa **application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="c4c38-183">![사용자 할당](./media/active-directory-saas-coupa-tutorial/IC791911.png "사용자 할당")</span><span class="sxs-lookup"><span data-stu-id="c4c38-183">![Assign Users](./media/active-directory-saas-coupa-tutorial/IC791911.png "Assign Users")</span></span>
3. <span data-ttu-id="c4c38-184">테스트 사용자 선택, 클릭 **할당**, 클릭 하 고 **예** tooconfirm 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c38-184">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
   <span data-ttu-id="c4c38-185">![예](./media/active-directory-saas-coupa-tutorial/IC767830.png "예")</span><span class="sxs-lookup"><span data-stu-id="c4c38-185">![Yes](./media/active-directory-saas-coupa-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="c4c38-186">Single sign on 설정 tootest 원하는 hello 액세스 패널을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c4c38-186">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="c4c38-187">액세스 패널 hello에 대 한 자세한 내용은 참조 하십시오. [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c38-187">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

