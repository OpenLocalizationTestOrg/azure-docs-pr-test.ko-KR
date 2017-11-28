---
title: "자습서: Cisco Webex와 Azure Active Directory 통합 | Microsoft Docs"
description: "어떻게 toouse Cisco Webex와 Azure Active Directory tooenable single sign on, 자동화 된 프로비저닝 및 더에 대해 알아봅니다."
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 26704ca7-13ed-4261-bf24-fd6252e2072b
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 9fc11e58a7acaa6fbfb32eeccbfbf85984950e67
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cisco-webex"></a><span data-ttu-id="1c298-103">자습서: Cisco Webex와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="1c298-103">Tutorial: Azure Active Directory Integration with Cisco Webex</span></span>
<span data-ttu-id="1c298-104">hello이이 자습서는 Azure와 Cisco Webex tooshow hello 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c298-104">hello objective of this tutorial is tooshow hello integration of Azure and Cisco Webex.</span></span>  
<span data-ttu-id="1c298-105">이 자습서에 설명 된 hello 시나리오 다음 항목 hello 이미 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c298-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="1c298-106">유효한 Azure 구독</span><span class="sxs-lookup"><span data-stu-id="1c298-106">A valid Azure subscription</span></span>
* <span data-ttu-id="1c298-107">Cisco Webex 테넌트</span><span class="sxs-lookup"><span data-stu-id="1c298-107">A Cisco Webex tenant</span></span>

<span data-ttu-id="1c298-108">이 자습서를 완료 한 후 할당 한 Webex 됩니다 tooCisco 수 toosingle 기호 hello 응용 프로그램으로 Cisco Webex 회사 사이트 (서비스 공급자에서 시작 된 로그온)에서 Azure AD 사용자 hello 또는 hello를 사용 하 여 [toohello 소개 액세스 패널](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1c298-108">After completing this tutorial, hello Azure AD users you have assigned tooCisco Webex will be able toosingle sign into hello application at your Cisco Webex company site (service provider initiated sign on), or using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="1c298-109">이 자습서에 설명 된 hello 시나리오 hello 빌딩 블록을 다음으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c298-109">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

* <span data-ttu-id="1c298-110">Cisco Webex에 대 한 hello 응용 프로그램 통합 사용</span><span class="sxs-lookup"><span data-stu-id="1c298-110">Enabling hello application integration for Cisco Webex</span></span>
* <span data-ttu-id="1c298-111">SSO(Single Sign-On) 구성</span><span class="sxs-lookup"><span data-stu-id="1c298-111">Configuring single sign-on (SSO)</span></span>
* <span data-ttu-id="1c298-112">사용자 프로비전 구성</span><span class="sxs-lookup"><span data-stu-id="1c298-112">Configuring user provisioning</span></span>
* <span data-ttu-id="1c298-113">사용자 할당</span><span class="sxs-lookup"><span data-stu-id="1c298-113">Assigning users</span></span>

<span data-ttu-id="1c298-114">![시나리오](./media/active-directory-saas-cisco-webex-tutorial/IC777614.png "시나리오")</span><span class="sxs-lookup"><span data-stu-id="1c298-114">![Scenario](./media/active-directory-saas-cisco-webex-tutorial/IC777614.png "Scenario")</span></span>

## <a name="enable-hello-application-integration-for-cisco-webex"></a><span data-ttu-id="1c298-115">Cisco Webex에 대 한 hello 응용 프로그램 통합을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="1c298-115">Enable hello application integration for Cisco Webex</span></span>
<span data-ttu-id="1c298-116">hello이이 섹션의 목적은 toooutline 어떻게 Cisco Webex에 대 한 tooenable hello 응용 프로그램 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c298-116">hello objective of this section is toooutline how tooenable hello application integration for Cisco Webex.</span></span>

<span data-ttu-id="1c298-117">**Cisco Webex에 대 한 tooenable hello 응용 프로그램 통합 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="1c298-117">**tooenable hello application integration for Cisco Webex, perform hello following steps:**</span></span>

1. <span data-ttu-id="1c298-118">Hello hello 왼쪽된 탐색 창에서 Azure 클래식 포털에서에서 클릭 **Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="1c298-118">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="1c298-119">![Active Directory](./media/active-directory-saas-cisco-webex-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="1c298-119">![Active Directory](./media/active-directory-saas-cisco-webex-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="1c298-120">Hello에서 **디렉터리** 목록, 선택 hello 디렉터리 tooenable 디렉터리 통합을 구하려는 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c298-120">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="1c298-121">tooopen hello 응용 프로그램 보기 hello 디렉터리 보기에서 클릭 **응용 프로그램** hello 상단 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c298-121">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
   <span data-ttu-id="1c298-122">![응용 프로그램](./media/active-directory-saas-cisco-webex-tutorial/IC700994.png "응용 프로그램")</span><span class="sxs-lookup"><span data-stu-id="1c298-122">![Applications](./media/active-directory-saas-cisco-webex-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="1c298-123">클릭 **추가** hello hello 페이지 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c298-123">Click **Add** at hello bottom of hello page.</span></span>
   
   <span data-ttu-id="1c298-124">![응용 프로그램 추가](./media/active-directory-saas-cisco-webex-tutorial/IC749321.png "응용 프로그램 추가")</span><span class="sxs-lookup"><span data-stu-id="1c298-124">![Add application](./media/active-directory-saas-cisco-webex-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="1c298-125">Hello에 **하 신 toodo 원하는** 대화 상자에서 클릭 **hello 갤러리에서 응용 프로그램 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="1c298-125">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
   <span data-ttu-id="1c298-126">![갤러리에서 응용 프로그램 추가](./media/active-directory-saas-cisco-webex-tutorial/IC749322.png "갤러리에서 응용 프로그램 추가")</span><span class="sxs-lookup"><span data-stu-id="1c298-126">![Add an application from gallerry](./media/active-directory-saas-cisco-webex-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="1c298-127">Hello에 **검색 상자**, 형식 **Cisco Webex**합니다.</span><span class="sxs-lookup"><span data-stu-id="1c298-127">In hello **search box**, type **Cisco Webex**.</span></span>
   
   <span data-ttu-id="1c298-128">![응용 프로그램 갤러리](./media/active-directory-saas-cisco-webex-tutorial/IC777615.png "응용 프로그램 갤러리")</span><span class="sxs-lookup"><span data-stu-id="1c298-128">![Application Gallery](./media/active-directory-saas-cisco-webex-tutorial/IC777615.png "Application Gallery")</span></span>
7. <span data-ttu-id="1c298-129">Hello 결과 창에서 선택 **Cisco Webex**, 클릭 하 고 **완료** tooadd hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="1c298-129">In hello results pane, select **Cisco Webex**, and then click **Complete** tooadd hello application.</span></span>
   
   <span data-ttu-id="1c298-130">![Cisco Webex](./media/active-directory-saas-cisco-webex-tutorial/IC777616.png "Cisco Webex")</span><span class="sxs-lookup"><span data-stu-id="1c298-130">![Cisco Webex](./media/active-directory-saas-cisco-webex-tutorial/IC777616.png "Cisco Webex")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="1c298-131">Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="1c298-131">Configure single sign-on</span></span>

<span data-ttu-id="1c298-132">hello이이 섹션의 목적은 toooutline 페더레이션을 사용 하 여 Azure AD에서 자신의 계정으로 tooenable 사용자 tooauthenticate tooCisco Webex hello SAML 프로토콜에 따라 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="1c298-132">hello objective of this section is toooutline how tooenable users tooauthenticate tooCisco Webex with their account in Azure AD using federation based on hello SAML protocol.</span></span>  

<span data-ttu-id="1c298-133">이 절차의 일부로 필수 toocreate e-64로 인코딩된 인증서 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c298-133">As part of this procedure, you are required toocreate a base-64 encoded certificate.</span></span> <span data-ttu-id="1c298-134">이 절차에 익숙하지 않은 경우 참조 [어떻게 tooconvert 이진은 텍스트 파일에을 인증서](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="1c298-134">If you are not familiar with this procedure, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>

<span data-ttu-id="1c298-135">**tooconfigure 단일 로그온 hello 다음 단계를 수행 하십시오.**</span><span class="sxs-lookup"><span data-stu-id="1c298-135">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="1c298-136">Hello hello에 Azure 클래식 포털에서에서 **Cisco Webex** 응용 프로그램 통합 페이지에서 클릭 **single sign on 구성** tooopen hello **Single Sign-on 구성** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="1c298-136">In hello Azure classic portal, on hello **Cisco Webex** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="1c298-137">![Single Sign-On 구성](./media/active-directory-saas-cisco-webex-tutorial/IC777617.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="1c298-137">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777617.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="1c298-138">Hello에 **어떻게 tooCisco Webex에 사용자가 toosign 보 시겠습니까** 페이지에서 **Microsoft Azure AD Single Sign-on**, 클릭 하 고 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="1c298-138">On hello **How would you like users toosign on tooCisco Webex** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="1c298-139">![Single Sign-On 구성](./media/active-directory-saas-cisco-webex-tutorial/IC777618.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="1c298-139">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777618.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="1c298-140">Hello에 **앱 URL 구성** 페이지 hello 다음 단계를 수행 하 고 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="1c298-140">On hello **Configure App URL** page, perform hello following steps, and then click **Next**.</span></span>
   
   <span data-ttu-id="1c298-141">![앱 URL 구성](./media/active-directory-saas-cisco-webex-tutorial/IC777619.png "앱 URL 구성")</span><span class="sxs-lookup"><span data-stu-id="1c298-141">![Configure app URL](./media/active-directory-saas-cisco-webex-tutorial/IC777619.png "Configure app URL")</span></span>   
   1. <span data-ttu-id="1c298-142">Hello에 **로그온 URL** 텍스트 상자에 Cisco Webex 테 넌 트 URL (예:: *http://contoso.webex.com*).</span><span class="sxs-lookup"><span data-stu-id="1c298-142">In hello **Sing On URL** textbox, type your Cisco Webex tenant URL (e.g.: *http://contoso.webex.com*).</span></span>
   2. <span data-ttu-id="1c298-143">Hello에 **Cisco Webex 회신 URL** 텍스트 상자에을 입력 하면 **Cisco Webex AssertionConsumerService URL** (예:: *https://company.webex.com/dispatcher/SAML2AuthService?siteurl=company* ).</span><span class="sxs-lookup"><span data-stu-id="1c298-143">In hello **Cisco Webex Reply URL** textbox, type your **Cisco Webex AssertionConsumerService URL** (e.g.: *https://company.webex.com/dispatcher/SAML2AuthService?siteurl=company*).</span></span>
4. <span data-ttu-id="1c298-144">Hello에 **Cisco Webex에서 single sign on 구성** 페이지, toodownload 인증서를 클릭 하 여 **다운로드 인증서**, hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c298-144">On hello **Configure single sign-on at Cisco Webex** page, toodownload your certificate, click **Download certificate**, and then save hello certificate file on your computer.</span></span>
   
   <span data-ttu-id="1c298-145">![Single Sign-On 구성](./media/active-directory-saas-cisco-webex-tutorial/IC777620.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="1c298-145">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777620.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="1c298-146">다른 웹 브라우저 창에서 Cisco Webex 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="1c298-146">In a different web browser window, log into your Cisco Webex company site as an administrator.</span></span>
6. <span data-ttu-id="1c298-147">Hello 메뉴에서 hello 위에 표시를 클릭 **사이트 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="1c298-147">In hello menu on hello top, click **Site Administration**.</span></span>
   
   <span data-ttu-id="1c298-148">![사이트 관리](./media/active-directory-saas-cisco-webex-tutorial/IC777621.png "사이트 관리")</span><span class="sxs-lookup"><span data-stu-id="1c298-148">![Site Administration](./media/active-directory-saas-cisco-webex-tutorial/IC777621.png "Site Administration")</span></span>
7. <span data-ttu-id="1c298-149">Hello에 **사이트 관리** 섹션에서 클릭 **SSO 구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="1c298-149">In hello **Manage Site** section, click **SSO Configuration**.</span></span>
   
   <span data-ttu-id="1c298-150">![SSO 구성](./media/active-directory-saas-cisco-webex-tutorial/IC777622.png "SSO 구성")</span><span class="sxs-lookup"><span data-stu-id="1c298-150">![SSO Configuration](./media/active-directory-saas-cisco-webex-tutorial/IC777622.png "SSO Configuration")</span></span>
8. <span data-ttu-id="1c298-151">Hello 페더레이션 웹 SSO 구성 섹션에서에서 단계를 수행 하는 hello를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c298-151">In hello Federated Web SSO Configuration section, perform hello following steps:</span></span>
   
   <span data-ttu-id="1c298-152">![페더레이션 SSO 구성](./media/active-directory-saas-cisco-webex-tutorial/IC777623.png "페더레이션 SSO 구성")</span><span class="sxs-lookup"><span data-stu-id="1c298-152">![Federated SSO Configuration](./media/active-directory-saas-cisco-webex-tutorial/IC777623.png "Federated SSO Configuration")</span></span>  
   1. <span data-ttu-id="1c298-153">Hello에서 **페더레이션 프로토콜** 목록에서 **SAML 2.0**합니다.</span><span class="sxs-lookup"><span data-stu-id="1c298-153">From hello **Federation Protocol** list, select **SAML 2.0**.</span></span>
   2. <span data-ttu-id="1c298-154">다운로드한 인증서에서 **Base-64로 인코딩된** 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1c298-154">Create a **Base-64 encoded** file from your downloaded certificate.</span></span>  
    >[!TIP]
    ><span data-ttu-id="1c298-155">자세한 내용은 참조 하십시오. [어떻게 tooconvert 이진은 텍스트 파일에을 인증서](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="1c298-155">For more details, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>
    >  
   3. <span data-ttu-id="1c298-156">메모장을 선택한 다음의 콘텐츠 복사 hello에서 e-64로 인코딩된 인증서를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1c298-156">Open your base-64 encoded certificate in notepad, and then copy hello content of it.</span></span>
   4. <span data-ttu-id="1c298-157">**SAML 메타데이터 가져오기**를 클릭하고 Base-64로 인코딩된 인증서를 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="1c298-157">Click **Import SAML Metadata**, and then paste your base-64 encoded certificate.</span></span>
   5. <span data-ttu-id="1c298-158">Hello hello에 Azure 클래식 포털에서에서 **Cisco Webex에서 single sign on 구성** 대화 상자 페이지에서 복사 hello **발급자 URL** 값을 복사한 다음 hello에 붙여 넣을 **(IdP ID)SAML발급자** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="1c298-158">In hello Azure classic portal, on hello **Configure single sign-on at Cisco Webex** dialog page, copy hello **Issuer URL** value, and then paste it into hello **Issuer for SAML (IdP ID)** textbox.</span></span>
   6. <span data-ttu-id="1c298-159">Hello hello에 Azure 클래식 포털에서에서 **Cisco Webex에서 single sign on 구성** 대화 상자 페이지에서 복사 hello **원격 로그인 URL** 값을 복사한 다음 hello에 붙여 넣을 **고객 SSO 서비스 로그인 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="1c298-159">In hello Azure classic portal, on hello **Configure single sign-on at Cisco Webex** dialog page, copy hello **Remote Login URL** value, and then paste it into hello **Customer SSO Service Login URL** textbox.</span></span>
   7. <span data-ttu-id="1c298-160">Hello에서 **NameID 형식** 목록에서 **전자 메일 주소**합니다.</span><span class="sxs-lookup"><span data-stu-id="1c298-160">From hello **NameID Format** list, select **Email address**.</span></span>
   8. <span data-ttu-id="1c298-161">Hello에 **AuthnContextClassRef** 텍스트 상자에 **urn: oasis: 이름: tc: SAML:2.0:ac:classes:Password**합니다.</span><span class="sxs-lookup"><span data-stu-id="1c298-161">In hello **AuthnContextClassRef** textbox, type **urn:oasis:names:tc:SAML:2.0:ac:classes:Password**.</span></span>
   9. <span data-ttu-id="1c298-162">Hello hello에 Azure 클래식 포털에서에서 **Cisco Webex에서 single sign on 구성** 대화 상자 페이지에서 복사 hello **원격 로그 아웃 URL** 값을 복사한 다음 hello에 붙여 넣을 **고객 SSO 서비스 로그 아웃 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="1c298-162">In hello Azure classic portal, on hello **Configure single sign-on at Cisco Webex** dialog page, copy hello **Remote Logout URL** value, and then paste it into hello **Customer SSO Service Logout URL** textbox.</span></span>
   10. <span data-ttu-id="1c298-163">**업데이트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1c298-163">Click **Update**.</span></span>
9. <span data-ttu-id="1c298-164">Hello hello에 Azure 클래식 포털에서에서 **Cisco Webex에서 single sign on 구성** 대화 상자 페이지에서 hello single sign on 구성 확인을 선택한 다음 클릭 **완료**합니다.</span><span class="sxs-lookup"><span data-stu-id="1c298-164">In hello Azure classic portal, on hello **Configure single sign-on at Cisco Webex** dialog page, select hello single sign-on configuration confirmation, and then click **Complete**.</span></span>
   
   <span data-ttu-id="1c298-165">![Single Sign-On 구성](./media/active-directory-saas-cisco-webex-tutorial/IC777624.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="1c298-165">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777624.png "Configure single sign-on")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="1c298-166">사용자 프로비전 구성</span><span class="sxs-lookup"><span data-stu-id="1c298-166">Configure user provisioning</span></span>

<span data-ttu-id="1c298-167">Tooenable Azure AD 사용자가 toolog Cisco Webex에 주문 하 고에 Cisco Webex에 이들 프로 비전 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c298-167">In order tooenable Azure AD users toolog into Cisco Webex, they must be provisioned into Cisco Webex.</span></span>  

* <span data-ttu-id="1c298-168">Hello Cisco Webex의 경우에서 프로 비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="1c298-168">In hello case of Cisco Webex, provisioning is a manual task.</span></span>

<span data-ttu-id="1c298-169">**사용자 계정 수행 tooprovision hello 다음 단계:**</span><span class="sxs-lookup"><span data-stu-id="1c298-169">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="1c298-170">Tooyour 로그인 **Cisco Webex** 테 넌 트입니다.</span><span class="sxs-lookup"><span data-stu-id="1c298-170">Log in tooyour **Cisco Webex** tenant.</span></span>
2. <span data-ttu-id="1c298-171">너무 이동**사용자 관리 \> 사용자 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="1c298-171">Go too**Manage Users \> Add User**.</span></span>
   
   <span data-ttu-id="1c298-172">![사용자 추가](./media/active-directory-saas-cisco-webex-tutorial/IC777625.png "사용자 추가")</span><span class="sxs-lookup"><span data-stu-id="1c298-172">![Add users](./media/active-directory-saas-cisco-webex-tutorial/IC777625.png "Add users")</span></span>
3. <span data-ttu-id="1c298-173">사용자 추가 섹션 hello hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c298-173">On hello Add User section, perform hello following steps:</span></span>
   
   <span data-ttu-id="1c298-174">![사용자 추가](./media/active-directory-saas-cisco-webex-tutorial/IC777626.png "사용자 추가")</span><span class="sxs-lookup"><span data-stu-id="1c298-174">![Add user](./media/active-directory-saas-cisco-webex-tutorial/IC777626.png "Add user")</span></span>   
   1. <span data-ttu-id="1c298-175">**계정 유형**으로 **호스트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1c298-175">As **Account Type**, select **Host**.</span></span>
   2. <span data-ttu-id="1c298-176">Hello 다음 텍스트 상자에 기존 Azure AD 사용자의 hello 정보를 입력: **이름, 성**, **사용자 이름**, **전자 메일**, **암호**, **암호 확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="1c298-176">Type hello information of an existing Azure AD user into hello following textboxes: **First name, Last name**, **User name**, **Email**, **Password**, **Confirm Password**.</span></span>
   3. <span data-ttu-id="1c298-177">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1c298-177">Click **Add**.</span></span>

>[!NOTE]
><span data-ttu-id="1c298-178">다른 Cisco Webex 사용자 계정 만들기 도구를 사용할 수 있습니다 또는 AAD 사용자 계정을 tooprovision Cisco Webex에서 제공 된 Api입니다.</span><span class="sxs-lookup"><span data-stu-id="1c298-178">You can use any other Cisco Webex user account creation tools or APIs provided by Cisco Webex tooprovision AAD user accounts.</span></span> 
> 

## <a name="assign-users"></a><span data-ttu-id="1c298-179">사용자 할당</span><span class="sxs-lookup"><span data-stu-id="1c298-179">Assign users</span></span>
<span data-ttu-id="1c298-180">tootest 구성에 tooallow 할당 하 여 응용 프로그램 액세스 tooit를 사용 하 여 원하는 toogrant hello Azure AD 사용자가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c298-180">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="1c298-181">**tooassign 사용자 tooCisco Webex hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="1c298-181">**tooassign users tooCisco Webex, perform hello following steps:**</span></span>

1. <span data-ttu-id="1c298-182">Azure 클래식 포털 hello 테스트 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1c298-182">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="1c298-183">Hello에 **Cisco Webex** 응용 프로그램 통합 페이지에서 클릭 **사용자 할당**합니다.</span><span class="sxs-lookup"><span data-stu-id="1c298-183">On hello **Cisco Webex** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="1c298-184">![사용자 할당](./media/active-directory-saas-cisco-webex-tutorial/IC777627.png "사용자 할당")</span><span class="sxs-lookup"><span data-stu-id="1c298-184">![Assign users](./media/active-directory-saas-cisco-webex-tutorial/IC777627.png "Assign users")</span></span>
3. <span data-ttu-id="1c298-185">테스트 사용자 선택, 클릭 **할당**, 클릭 하 고 **예** tooconfirm 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c298-185">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
   <span data-ttu-id="1c298-186">![예](./media/active-directory-saas-cisco-webex-tutorial/IC767830.png "예")</span><span class="sxs-lookup"><span data-stu-id="1c298-186">![Yes](./media/active-directory-saas-cisco-webex-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="1c298-187">Single sign on 설정 tootest 원하는 hello 액세스 패널을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1c298-187">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="1c298-188">액세스 패널 hello에 대 한 자세한 내용은 참조 하십시오. [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1c298-188">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

