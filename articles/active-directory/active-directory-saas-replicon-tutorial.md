---
title: "자습서: Replicon과 Azure Active Directory 통합 | Microsoft Docs"
description: "어떻게 tooenable Azure Active Directory와 Replicon toouse single sign on, 자동화 된 프로비저닝 및 더에 대해 알아봅니다."
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 02a62f15-917c-417c-8d80-fe685e3fd601
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: 4949eaf959265cfa4f732a2b73317fffe6312a17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-replicon"></a><span data-ttu-id="58782-103">자습서: Replicon과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="58782-103">Tutorial: Azure Active Directory integration with Replicon</span></span>
<span data-ttu-id="58782-104">hello이이 자습서는 Azure와 Replicon tooshow hello 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="58782-104">hello objective of this tutorial is tooshow hello integration of Azure and Replicon.</span></span> <span data-ttu-id="58782-105">이 자습서에 설명 된 hello 시나리오 다음 항목 hello 이미 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="58782-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="58782-106">유효한 Azure 구독</span><span class="sxs-lookup"><span data-stu-id="58782-106">A valid Azure subscription</span></span>
* <span data-ttu-id="58782-107">Replicon 테넌트</span><span class="sxs-lookup"><span data-stu-id="58782-107">A Replicon tenant</span></span>

<span data-ttu-id="58782-108">이 자습서를 완료 한 후 hello Azure AD 사용자 tooReplicon 배정 됩니다 Replicon 회사 사이트 (서비스 공급자에서 시작 된 로그온)에서 또는 hello를 사용 하 여 hello 응용 프로그램에 수 toosingle 로그인 [소개 toohello 액세스 패널](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="58782-108">After completing this tutorial, hello Azure AD users you have assigned tooReplicon will be able toosingle sign into hello application at your Replicon company site (service provider initiated sign on), or using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="58782-109">이 자습서에 설명 된 hello 시나리오 hello 빌딩 블록을 다음으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="58782-109">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

1. <span data-ttu-id="58782-110">Replicon에 대 한 hello 응용 프로그램 통합 사용</span><span class="sxs-lookup"><span data-stu-id="58782-110">Enabling hello application integration for Replicon</span></span>
2. <span data-ttu-id="58782-111">SSO(Single Sign-On) 구성</span><span class="sxs-lookup"><span data-stu-id="58782-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="58782-112">사용자 프로비전 구성</span><span class="sxs-lookup"><span data-stu-id="58782-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="58782-113">사용자 할당</span><span class="sxs-lookup"><span data-stu-id="58782-113">Assigning users</span></span>

<span data-ttu-id="58782-114">![시나리오](./media/active-directory-saas-replicon-tutorial/IC777798.png "시나리오")</span><span class="sxs-lookup"><span data-stu-id="58782-114">![Scenario](./media/active-directory-saas-replicon-tutorial/IC777798.png "Scenario")</span></span>

## <a name="enable-hello-application-integration-for-replicon"></a><span data-ttu-id="58782-115">Replicon에 대 한 hello 응용 프로그램 통합을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="58782-115">Enable hello application integration for Replicon</span></span>
<span data-ttu-id="58782-116">hello이이 섹션의 목적은 toooutline 어떻게 Replicon에 tooenable hello 응용 프로그램 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="58782-116">hello objective of this section is toooutline how tooenable hello application integration for Replicon.</span></span>

<span data-ttu-id="58782-117">**Replicon에 tooenable hello 응용 프로그램 통합 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="58782-117">**tooenable hello application integration for Replicon, perform hello following steps:**</span></span>

1. <span data-ttu-id="58782-118">Hello hello 왼쪽된 탐색 창에서 Azure 클래식 포털에서에서 클릭 **Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="58782-118">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="58782-119">![Active Directory](./media/active-directory-saas-replicon-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="58782-119">![Active Directory](./media/active-directory-saas-replicon-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="58782-120">Hello에서 **디렉터리** 목록, 선택 hello 디렉터리 tooenable 디렉터리 통합을 구하려는 합니다.</span><span class="sxs-lookup"><span data-stu-id="58782-120">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="58782-121">tooopen hello 응용 프로그램 보기 hello 디렉터리 보기에서 클릭 **응용 프로그램** hello 상단 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="58782-121">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    <span data-ttu-id="58782-122">![응용 프로그램](./media/active-directory-saas-replicon-tutorial/IC700994.png "응용 프로그램")</span><span class="sxs-lookup"><span data-stu-id="58782-122">![Applications](./media/active-directory-saas-replicon-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="58782-123">클릭 **추가** hello hello 페이지 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58782-123">Click **Add** at hello bottom of hello page.</span></span>
   
    <span data-ttu-id="58782-124">![응용 프로그램 추가](./media/active-directory-saas-replicon-tutorial/IC749321.png "응용 프로그램 추가")</span><span class="sxs-lookup"><span data-stu-id="58782-124">![Add application](./media/active-directory-saas-replicon-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="58782-125">Hello에 **하 신 toodo 원하는** 대화 상자에서 클릭 **hello 갤러리에서 응용 프로그램 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="58782-125">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    <span data-ttu-id="58782-126">![갤러리에서 응용 프로그램 추가](./media/active-directory-saas-replicon-tutorial/IC749322.png "갤러리에서 응용 프로그램 추가")</span><span class="sxs-lookup"><span data-stu-id="58782-126">![Add an application from gallerry](./media/active-directory-saas-replicon-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="58782-127">Hello에 **검색 상자**, 형식 **Replicon**합니다.</span><span class="sxs-lookup"><span data-stu-id="58782-127">In hello **search box**, type **Replicon**.</span></span>
   
    <span data-ttu-id="58782-128">![응용 프로그램 갤러리](./media/active-directory-saas-replicon-tutorial/IC777799.png "응용 프로그램 갤러리")</span><span class="sxs-lookup"><span data-stu-id="58782-128">![Application gallery](./media/active-directory-saas-replicon-tutorial/IC777799.png "Application gallery")</span></span>
7. <span data-ttu-id="58782-129">Hello 결과 창에서 선택 **Replicon**, 클릭 하 고 **완료** tooadd hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="58782-129">In hello results pane, select **Replicon**, and then click **Complete** tooadd hello application.</span></span>
   
    <span data-ttu-id="58782-130">![Replicon](./media/active-directory-saas-replicon-tutorial/IC777800.png "Replicon")</span><span class="sxs-lookup"><span data-stu-id="58782-130">![Replicon](./media/active-directory-saas-replicon-tutorial/IC777800.png "Replicon")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="58782-131">Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="58782-131">Configure single sign-on</span></span>

<span data-ttu-id="58782-132">hello이이 섹션의 목적은 toooutline 페더레이션을 사용 하 여 Azure AD에서 자신의 계정으로 tooenable 사용자 tooauthenticate tooReplicon hello SAML 프로토콜에 따라 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="58782-132">hello objective of this section is toooutline how tooenable users tooauthenticate tooReplicon with their account in Azure AD using federation based on hello SAML protocol.</span></span>

<span data-ttu-id="58782-133">**tooconfigure 단일 로그온 hello 다음 단계를 수행 하십시오.**</span><span class="sxs-lookup"><span data-stu-id="58782-133">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="58782-134">Hello hello에 Azure 클래식 포털에서에서 **Replicon** 응용 프로그램 통합 페이지에서 클릭 **single sign on 구성** tooopen hello **Single Sign-on 구성** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="58782-134">In hello Azure classic portal, on hello **Replicon** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="58782-135">![Single Sign-On 구성](./media/active-directory-saas-replicon-tutorial/IC777801.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="58782-135">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC777801.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="58782-136">Hello에 **어떻게 tooReplicon에 사용자가 toosign 보 시겠습니까** 페이지에서 **Microsoft Azure AD Single Sign-on**, 클릭 하 고 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="58782-136">On hello **How would you like users toosign on tooReplicon** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="58782-137">![Single Sign-On 구성](./media/active-directory-saas-replicon-tutorial/IC777802.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="58782-137">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC777802.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="58782-138">Hello에 **앱 URL 구성** 페이지 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="58782-138">On hello **Configure App URL** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="58782-139">![앱 URL 구성](./media/active-directory-saas-replicon-tutorial/IC777803.png "앱 URL 구성")</span><span class="sxs-lookup"><span data-stu-id="58782-139">![Configure app URL](./media/active-directory-saas-replicon-tutorial/IC777803.png "Configure app URL")</span></span>
  1. <span data-ttu-id="58782-140">Hello에 **Replicon 로그온 URL** 텍스트 상자에 Replicon 테 넌 트 URL (예:: *https://na2.replicon.com/company/saml2/sp-sso/post*).</span><span class="sxs-lookup"><span data-stu-id="58782-140">In hello **Replicon Sign On URL** textbox, type your Replicon tenant URL (e.g.: *https://na2.replicon.com/company/saml2/sp-sso/post*).</span></span>
  2. <span data-ttu-id="58782-141">Hello에 **Replicon 회신 URL** 텍스트 상자에 Replicon **AssertionConsumerService** URL (예:: *https://global.replicon.com/! / saml2/회사/sso/post*).</span><span class="sxs-lookup"><span data-stu-id="58782-141">In hello **Replicon Reply URL** textbox, type your Replicon **AssertionConsumerService** URL(e.g.: *https://global.replicon.com/!/saml2/company/sso/post*).</span></span>  
      
     >[!NOTE]
     ><span data-ttu-id="58782-142">Hello Replicon 메타 데이터에서 hello URL을 가져올 수 있습니다: **https://global.replicon.com/! /saml2/\<YourCompanyKey\>**합니다.</span><span class="sxs-lookup"><span data-stu-id="58782-142">You can get hello URL from hello Replicon metadata at: **https://global.replicon.com/!/saml2/\<YourCompanyKey\>**.</span></span>
     > 
     > 
 
  3. <span data-ttu-id="58782-143">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="58782-143">Click **Next**.</span></span>

4. <span data-ttu-id="58782-144">Hello에 **Replicon에서 single sign on 구성** 페이지, toodownload 메타 데이터를 클릭 하 여 **메타 데이터 다운로드**, 한 다음 컴퓨터에 hello 메타 데이터를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="58782-144">On hello **Configure single sign-on at Replicon** page, toodownload your metadata, click **Download metadata**, and then save hello metadata on your computer.</span></span>
   
    <span data-ttu-id="58782-145">![Single Sign-On 구성](./media/active-directory-saas-replicon-tutorial/IC777804.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="58782-145">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC777804.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="58782-146">다른 웹 브라우저 창에서 Replicon 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="58782-146">In a different web browser window, log into your Replicon company site as an administrator.</span></span>

6. <span data-ttu-id="58782-147">SAML 2.0 tooconfigure hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="58782-147">tooconfigure SAML 2.0, perform hello following steps:</span></span>
   
    <span data-ttu-id="58782-148">![SAML 인증 사용](./media/active-directory-saas-replicon-tutorial/IC777805.png "SAML 인증 사용")</span><span class="sxs-lookup"><span data-stu-id="58782-148">![Enable SAML authentication](./media/active-directory-saas-replicon-tutorial/IC777805.png "Enable SAML authentication")</span></span>
  
  1. <span data-ttu-id="58782-149">toodisplay hello **EnableSAML Authentication2** 대화 상자에서 회사 키 뒤 tooyour URL을 따라 hello 추가: **/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span><span class="sxs-lookup"><span data-stu-id="58782-149">toodisplay hello **EnableSAML Authentication2** dialog, append hello following tooyour URL, after your company key: **/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span></span>  
    * <span data-ttu-id="58782-150">hello 다음 hello 전체 URL의 hello 스키마를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="58782-150">hello following shows hello schema of hello complete URL:</span></span>  
   <span data-ttu-id="58782-151">**https://na2.replicon.com/\<YourCompanyKey\>/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span><span class="sxs-lookup"><span data-stu-id="58782-151">**https://na2.replicon.com/\<YourCompanyKey\>/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span></span>
   2. <span data-ttu-id="58782-152">Hello 클릭 ** + ** tooexpand hello **v20Configuration** 섹션.</span><span class="sxs-lookup"><span data-stu-id="58782-152">Click hello **+** tooexpand hello **v20Configuration** section.</span></span>
   3. <span data-ttu-id="58782-153">Hello 클릭 ** + ** tooexpand hello **metaDataConfiguration** 섹션.</span><span class="sxs-lookup"><span data-stu-id="58782-153">Click hello **+** tooexpand hello **metaDataConfiguration** section.</span></span>
   4. <span data-ttu-id="58782-154">클릭 **파일 선택**, tooselect identity 공급자 메타 데이터 XML 파일 및 클릭 **전송**합니다.</span><span class="sxs-lookup"><span data-stu-id="58782-154">Click **Choose File**, tooselect your identity provider metadata XML file, and click **Submit**.</span></span>

7. <span data-ttu-id="58782-155">Azure 클래식 포털 hello에 hello single sign on 구성 확인을 선택한 다음 클릭 **완료** tooclose hello **Single Sign-on 구성** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="58782-155">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="58782-156">![Single Sign-On 구성](./media/active-directory-saas-replicon-tutorial/IC778418.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="58782-156">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC778418.png "Configure single sign-on")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="58782-157">사용자 프로비전 구성</span><span class="sxs-lookup"><span data-stu-id="58782-157">Configure user provisioning</span></span>

<span data-ttu-id="58782-158">Tooenable Azure AD 사용자가 toolog Replicon에 주문 하 고에 Replicon에 이들 프로 비전 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="58782-158">In order tooenable Azure AD users toolog into Replicon, they must be provisioned into Replicon.</span></span>  

<span data-ttu-id="58782-159">Hello Replicon의 경우에서 프로 비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="58782-159">In hello case of Replicon, provisioning is a manual task.</span></span>

<span data-ttu-id="58782-160">**tooconfigure 사용자 프로비저닝, hello 다음 단계를 수행:**</span><span class="sxs-lookup"><span data-stu-id="58782-160">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="58782-161">웹 브라우저 창에서 Replicon 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="58782-161">In a web browser window, log into your Replicon company site as an administrator.</span></span>
2. <span data-ttu-id="58782-162">너무 이동**관리 \> 사용자**합니다.</span><span class="sxs-lookup"><span data-stu-id="58782-162">Go too**Administration \> Users**.</span></span>
   
    <span data-ttu-id="58782-163">![사용자](./media/active-directory-saas-replicon-tutorial/IC777806.png "사용자")</span><span class="sxs-lookup"><span data-stu-id="58782-163">![Users](./media/active-directory-saas-replicon-tutorial/IC777806.png "Users")</span></span>
3. <span data-ttu-id="58782-164">**+사용자 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="58782-164">Click **+Add User**.</span></span>
   
    <span data-ttu-id="58782-165">![사용자 추가](./media/active-directory-saas-replicon-tutorial/IC777807.png "사용자 추가")</span><span class="sxs-lookup"><span data-stu-id="58782-165">![Add User](./media/active-directory-saas-replicon-tutorial/IC777807.png "Add User")</span></span>
4. <span data-ttu-id="58782-166">Hello에 **사용자 프로필** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="58782-166">In hello **User Profile** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="58782-167">![사용자 프로필](./media/active-directory-saas-replicon-tutorial/IC777808.png "사용자 프로필")</span><span class="sxs-lookup"><span data-stu-id="58782-167">![User profile](./media/active-directory-saas-replicon-tutorial/IC777808.png "User profile")</span></span>
   
  1. <span data-ttu-id="58782-168">Hello에 **로그인 이름** 텍스트 형식 hello Azure AD 전자 메일 주소 하려는 hello Azure AD 사용자의 tooprovision 합니다.</span><span class="sxs-lookup"><span data-stu-id="58782-168">In hello **Login Name** textbox, type hello Azure AD email address of hello Azure AD user you want tooprovision.</span></span>
  2. <span data-ttu-id="58782-169">**인증 유형**으로 **SSO**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="58782-169">As **Authentication Type**, select **SSO**.</span></span>
  3. <span data-ttu-id="58782-170">Hello에 **부서** textbox hello 사용자의 부서를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="58782-170">In hello **Department** textbox, type hello user’s department.</span></span>
  4. <span data-ttu-id="58782-171">**직원 형식**으로 **관리자**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="58782-171">As **Employee Type**, select **Administrator**.</span></span>
  5. <span data-ttu-id="58782-172">**사용자 프로필 저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="58782-172">Click **Save User Profile**.</span></span>

>[!NOTE]
><span data-ttu-id="58782-173">다른 Replicon 사용자 계정 만들기 도구를 사용할 수 있습니다 또는 AAD 사용자 계정을 tooprovision Replicon에서 제공 된 Api입니다.</span><span class="sxs-lookup"><span data-stu-id="58782-173">You can use any other Replicon user account creation tools or APIs provided by Replicon tooprovision AAD user accounts.</span></span>
> 
> 

## <a name="assign-users"></a><span data-ttu-id="58782-174">사용자 할당</span><span class="sxs-lookup"><span data-stu-id="58782-174">Assign users</span></span>
<span data-ttu-id="58782-175">tootest 구성에 tooallow 할당 하 여 응용 프로그램 액세스 tooit를 사용 하 여 원하는 toogrant hello Azure AD 사용자가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="58782-175">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="58782-176">**tooassign 사용자 tooReplicon hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="58782-176">**tooassign users tooReplicon, perform hello following steps:**</span></span>

1. <span data-ttu-id="58782-177">Azure 클래식 포털 hello 테스트 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="58782-177">In hello Azure classic portal, create a test account.</span></span>

2. <span data-ttu-id="58782-178">Hello에 **Replicon** 응용 프로그램 통합 페이지에서 클릭 **사용자 할당**합니다.</span><span class="sxs-lookup"><span data-stu-id="58782-178">On hello **Replicon** application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="58782-179">![사용자 할당](./media/active-directory-saas-replicon-tutorial/IC777809.png "사용자 할당")</span><span class="sxs-lookup"><span data-stu-id="58782-179">![Assign users](./media/active-directory-saas-replicon-tutorial/IC777809.png "Assign users")</span></span>

3. <span data-ttu-id="58782-180">테스트 사용자 선택, 클릭 **할당**, 클릭 하 고 **예** tooconfirm 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="58782-180">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
    <span data-ttu-id="58782-181">![예](./media/active-directory-saas-replicon-tutorial/IC767830.png "예")</span><span class="sxs-lookup"><span data-stu-id="58782-181">![Yes](./media/active-directory-saas-replicon-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="58782-182">Single sign on 설정 tootest 원하는 hello 액세스 패널을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="58782-182">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="58782-183">액세스 패널 hello에 대 한 자세한 내용은 참조 하십시오. [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="58782-183">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

