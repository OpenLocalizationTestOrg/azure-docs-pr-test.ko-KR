---
title: "자습서: Salesforce Sandbox와 Azure Active Directory 통합 | Microsoft Docs"
description: "어떻게 tooenable Azure Active Directory와 Salesforce 샌드박스 toouse single sign on, 자동화 된 프로비저닝 및 더에 대해 알아봅니다."
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: ee54c39e-ce20-42a4-8531-da7b5f40f57c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: deccd6a07b57c8ba56b7e1c3f3ab311813ca017b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce-sandbox"></a><span data-ttu-id="cc551-103">자습서: Salesforce Sandbox와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="cc551-103">Tutorial: Azure Active Directory integration with Salesforce Sandbox</span></span>

<span data-ttu-id="cc551-104">hello이이 자습서는 Azure 및 Salesforce Sandbox의 tooshow hello 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc551-104">hello objective of this tutorial is tooshow hello integration of Azure and Salesforce Sandbox.</span></span>  

>[!TIP]
><span data-ttu-id="cc551-105">피드백에 대 한 참조 hello [Azure 지원 페이지](http://go.microsoft.com/fwlink/?LinkId=521878)합니다.</span><span class="sxs-lookup"><span data-stu-id="cc551-105">For feedback, see hello [Azure support page](http://go.microsoft.com/fwlink/?LinkId=521878).</span></span> 
> 

<span data-ttu-id="cc551-106">샌드박스 제공 하면 hello 기능 toocreate 다양 한 개발, 것과 같은 용도 대 한 별도 환경에서 조직의 여러 복사본 hello 데이터와 Salesforce 프로덕션에서 응용 프로그램을 그대로 유지 하지 않고 학습 및 테스트 하 고, 조직입니다.</span><span class="sxs-lookup"><span data-stu-id="cc551-106">Sandboxes give you hello ability toocreate multiple copies of your organization in separate environments for a variety of purposes, such as development, testing, and training, without compromising hello data and applications in your Salesforce production organization.</span></span>  

<span data-ttu-id="cc551-107">자세한 내용은 [샌드박스 개요](https://help.salesforce.com/HTViewHelpDoc?id=create_test_instance.htm&language=en_US)</span><span class="sxs-lookup"><span data-stu-id="cc551-107">For more details, see [Sandbox Overview](https://help.salesforce.com/HTViewHelpDoc?id=create_test_instance.htm&language=en_US)</span></span>

<span data-ttu-id="cc551-108">이 자습서에 설명 된 hello 시나리오 다음 항목 hello 이미 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc551-108">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="cc551-109">유효한 Azure 구독</span><span class="sxs-lookup"><span data-stu-id="cc551-109">A valid Azure subscription</span></span>
* <span data-ttu-id="cc551-110">Salesforce.com에서 샌드박스</span><span class="sxs-lookup"><span data-stu-id="cc551-110">A sandbox in Salesforce.com</span></span>

<span data-ttu-id="cc551-111">하면 유효한 샌드박스가 Salesforce.com에 아직 없는 경우 Salesforce toocontact을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc551-111">If you don’t have a valid sandbox in Salesforce.com yet, you need toocontact Salesforce.</span></span>

<span data-ttu-id="cc551-112">이 자습서에 설명 된 hello 시나리오 hello 빌딩 블록을 다음으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc551-112">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

1. <span data-ttu-id="cc551-113">Salesforce Sandbox에 대 한 hello 응용 프로그램 통합 사용</span><span class="sxs-lookup"><span data-stu-id="cc551-113">Enabling hello application integration for Salesforce Sandbox</span></span>
2. <span data-ttu-id="cc551-114">SSO(Single Sign-On) 구성</span><span class="sxs-lookup"><span data-stu-id="cc551-114">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="cc551-115">도메인 사용</span><span class="sxs-lookup"><span data-stu-id="cc551-115">Enabling your domain</span></span>
4. <span data-ttu-id="cc551-116">사용자 프로비전 구성</span><span class="sxs-lookup"><span data-stu-id="cc551-116">Configuring user provisioning</span></span>
5. <span data-ttu-id="cc551-117">사용자 할당</span><span class="sxs-lookup"><span data-stu-id="cc551-117">Assigning users</span></span>

<span data-ttu-id="cc551-118">![시나리오](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769571.png "시나리오")</span><span class="sxs-lookup"><span data-stu-id="cc551-118">![Scenario](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769571.png "Scenario")</span></span>

## <a name="enable-hello-application-integration-for-salesforce-sandbox"></a><span data-ttu-id="cc551-119">Salesforce Sandbox에 대 한 hello 응용 프로그램 통합을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="cc551-119">Enable hello application integration for Salesforce Sandbox</span></span>
<span data-ttu-id="cc551-120">hello이이 섹션의 목적은 toooutline 어떻게 Salesforce sandbox에 tooenable hello 응용 프로그램 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc551-120">hello objective of this section is toooutline how tooenable hello application integration for Salesforce sandbox.</span></span>

<span data-ttu-id="cc551-121">**Salesforce sandbox에 tooenable hello 응용 프로그램 통합 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="cc551-121">**tooenable hello application integration for Salesforce sandbox, perform hello following steps:**</span></span>

1. <span data-ttu-id="cc551-122">Hello hello 왼쪽된 탐색 창에서 Azure 클래식 포털에서에서 클릭 **Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="cc551-122">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="cc551-123">![Active Directory](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="cc551-123">![Active Directory](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="cc551-124">Hello에서 **디렉터리** 목록, 선택 hello 디렉터리 tooenable 디렉터리 통합을 구하려는 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc551-124">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="cc551-125">tooopen hello 응용 프로그램 보기 hello 디렉터리 보기에서 클릭 **응용 프로그램** hello 상단 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc551-125">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
   <span data-ttu-id="cc551-126">![응용 프로그램](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700994.png "응용 프로그램")</span><span class="sxs-lookup"><span data-stu-id="cc551-126">![Applications](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="cc551-127">tooopen hello **응용 프로그램 갤러리**, 클릭 **앱 추가**, 클릭 하 고 **내 조직 toouse 응용 프로그램 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="cc551-127">tooopen hello **Application Gallery**, click **Add An App**, and then click **Add an application for my organization toouse**.</span></span>
   
   <span data-ttu-id="cc551-128">![어떻게 하 시겠습니까 toodo 원하는? ] (./media/active-directory-saas-salesforce-sandbox-tutorial/IC700995.png "하 신 toodo 원하는?")</span><span class="sxs-lookup"><span data-stu-id="cc551-128">![What do you want toodo?](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700995.png "What do you want toodo?")</span></span>
5. <span data-ttu-id="cc551-129">Hello에 **검색 상자**, 형식 **Salesforce Sandbox**합니다.</span><span class="sxs-lookup"><span data-stu-id="cc551-129">In hello **search box**, type **Salesforce Sandbox**.</span></span>
   
   <span data-ttu-id="cc551-130">![응용 프로그램 갤러리](./media/active-directory-saas-salesforce-sandbox-tutorial/IC710978.png "응용 프로그램 갤러리")</span><span class="sxs-lookup"><span data-stu-id="cc551-130">![Application Gallery](./media/active-directory-saas-salesforce-sandbox-tutorial/IC710978.png "Application Gallery")</span></span>
6. <span data-ttu-id="cc551-131">Hello 결과 창에서 선택 **Salesforce Sandbox**, 클릭 하 고 **완료** tooadd hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="cc551-131">In hello results pane, select **Salesforce Sandbox**, and then click **Complete** tooadd hello application.</span></span>
   
   <span data-ttu-id="cc551-132">![Salesforce 샌드박스](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746474.png "Salesforce 샌드박스")</span><span class="sxs-lookup"><span data-stu-id="cc551-132">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746474.png "Salesforce Sandbox")</span></span>
   
## <a name="configur-single-sign-on-sso"></a><span data-ttu-id="cc551-133">SSO(Single Sign-On) 구성</span><span class="sxs-lookup"><span data-stu-id="cc551-133">Configur single sign-on (SSO)</span></span>

<span data-ttu-id="cc551-134">hello이이 섹션의 목적은 toooutline 페더레이션을 사용 하 여 Azure AD에서 자신의 계정으로 tooenable 사용자 tooauthenticate tooSalesforce hello SAML 프로토콜에 따라 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="cc551-134">hello objective of this section is toooutline how tooenable users tooauthenticate tooSalesforce with their account in Azure AD using federation based on hello SAML protocol.</span></span>

<span data-ttu-id="cc551-135">**tooconfigure 단일 로그온 hello 다음 단계를 수행 하십시오.**</span><span class="sxs-lookup"><span data-stu-id="cc551-135">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="cc551-136">Hello hello에 Azure 클래식 포털에서에서 **Salesforce Sandbox** 응용 프로그램 통합 페이지에서 클릭 **single sign on 구성** tooopen hello **Single Sign-on 구성** 대화 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="cc551-136">In hello Azure classic portal, on hello **Salesforce Sandbox** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="cc551-137">![Single Sign-On 구성](./media/active-directory-saas-salesforce-sandbox-tutorial/IC749323.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="cc551-137">![Configure single sign-on](./media/active-directory-saas-salesforce-sandbox-tutorial/IC749323.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="cc551-138">Hello에 **어떻게 tooSalesforce Sandbox에 사용자가 toosign 보 시겠습니까** 페이지에서 **Microsoft Azure AD Single Sign-on**, 클릭 하 고 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="cc551-138">On hello **How would you like users toosign on tooSalesforce Sandbox** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="cc551-139">![Salesforce 샌드박스](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746479.png "Salesforce 샌드박스")</span><span class="sxs-lookup"><span data-stu-id="cc551-139">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746479.png "Salesforce Sandbox")</span></span>
3. <span data-ttu-id="cc551-140">Hello에 **앱 URL 구성** 페이지 hello **로그온 URL** textbox hello 패턴으로 URL을 입력 `http://company.my.salesforce.com`, 클릭 하 고 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="cc551-140">On hello **Configure App URL** page, in hello **Sign On URL** textbox, type your URL using hello following pattern `http://company.my.salesforce.com`, and then click **Next**.</span></span>
   
   <span data-ttu-id="cc551-141">![앱 URL 구성](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781022.png "앱 URL 구성")</span><span class="sxs-lookup"><span data-stu-id="cc551-141">![Configure App URL](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781022.png "Configure App URL")</span></span>
4. <span data-ttu-id="cc551-142">이미 구성한 single sign on 다른 Salesforce Sandbox 인스턴스 디렉터리의 경우 hello 구성도 해야 **식별자** toohave hello hello와 같은 값 **로그온 URL**합니다.</span><span class="sxs-lookup"><span data-stu-id="cc551-142">If you have already configured single sign-on for another Salesforce Sandbox instance in your directory, then you must also configure hello **Identifier** toohave hello same value as hello **Sign on URL**.</span></span> 
 * <span data-ttu-id="cc551-143">hello **식별자** hello를 확인 하 여 필드를 찾을 수 **고급 설정 표시** hello에 확인란 **앱 URL 구성** hello 대화 상자의 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="cc551-143">hello **Identifier** field can be found by checking hello **Show advanced settings** checkbox on hello **Configure App URL** page of hello dialog.</span></span>
5. <span data-ttu-id="cc551-144">Hello에 **Salesforce 샌드박스에서 single sign on 구성** 페이지 **다운로드 인증서**, hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc551-144">On hello **Configure single sign-on at Salesforce Sandbox** page, click **Download certificate**, and then save hello certificate file on your computer.</span></span>
   
   <span data-ttu-id="cc551-145">![Single Sign-On 구성](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781023.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="cc551-145">![Configure Single Sign-On](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781023.png "Configure Single Sign-On")</span></span>
6. <span data-ttu-id="cc551-146">다른 웹 브라우저 창에서 Salesforce 샌드박스에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="cc551-146">In a different web browser window, log into your Salesforce sandbox as an administrator.</span></span>
7. <span data-ttu-id="cc551-147">Hello 메뉴에서 hello 위에 표시를 클릭 **설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="cc551-147">In hello menu on hello top, click **Setup**.</span></span>
   
   <span data-ttu-id="cc551-148">![설치](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781024.png "설치")</span><span class="sxs-lookup"><span data-stu-id="cc551-148">![Setup](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781024.png "Setup")</span></span>
8. <span data-ttu-id="cc551-149">Hello hello 왼쪽의 탐색 창에서 클릭 **보안 제어**, 클릭 하 고 **Single Sign On 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="cc551-149">In hello navigation pane on hello left, click **Security Controls**, and then click **Single Sign-On Settings**.</span></span>
   
   <span data-ttu-id="cc551-150">![Single Sign-On 설정](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781025.png "Single Sign-On 설정")</span><span class="sxs-lookup"><span data-stu-id="cc551-150">![Single Sign-On Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781025.png "Single Sign-On Settings")</span></span>
9. <span data-ttu-id="cc551-151">Single Sign-on 설정 섹션 hello hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc551-151">On hello Single Sign-On Settings section, perform hello following steps:</span></span>
   
   <span data-ttu-id="cc551-152">![Single Sign-On 설정](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781026.png "Single Sign-On 설정")</span><span class="sxs-lookup"><span data-stu-id="cc551-152">![Single Sign-On Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781026.png "Single Sign-On Settings")</span></span>  
 1.  <span data-ttu-id="cc551-153">**SAML 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cc551-153">Select **SAML Enabled**.</span></span> 
 2.  <span data-ttu-id="cc551-154">**새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cc551-154">Click **New**.</span></span>
10. <span data-ttu-id="cc551-155">SAML Single Sign-on 설정 섹션 hello hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc551-155">On hello SAML Single Sign-On Settings section, perform hello following steps:</span></span>
    
    <span data-ttu-id="cc551-156">![SAML Single Sign-On 설정](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781027.png "SAML Single Sign-On 설정")</span><span class="sxs-lookup"><span data-stu-id="cc551-156">![SAML Single Sign-On Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781027.png "SAML Single Sign-On Settings")</span></span>  
 1. <span data-ttu-id="cc551-157">Hello 이름 텍스트 상자에 입력 hello 구성의 hello 이름 (예:: *SPSSOWAAD\_테스트*).</span><span class="sxs-lookup"><span data-stu-id="cc551-157">In hello Name textbox, type hello name of hello configuration (e.g.: *SPSSOWAAD\_Test*).</span></span> 
 2. <span data-ttu-id="cc551-158">Hello hello에 Azure 클래식 포털에서에서 **Salesforce 샌드박스에서 single sign on 구성** 대화 상자 페이지에서 복사 hello **발급자 URL** 값을 복사한 다음 hello에 붙여 넣을 **발급자**텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="cc551-158">In hello Azure classic portal, on hello **Configure single sign-on at Salesforce Sandbox** dialogue page, copy hello **Issuer URL** value, and then paste it into hello **Issuer** textbox.</span></span>
 3. <span data-ttu-id="cc551-159">Hello에 **엔터티 Id** 텍스트 상자에 **https://test.salesforce.com** 인스턴스인 경우 hello 첫 번째 Salesforce Sandbox tooyour 디렉터리를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc551-159">In hello **Entity Id** textbox, type **https://test.salesforce.com** if this is hello first Salesforce Sandbox instance that you are adding tooyour directory.</span></span> <span data-ttu-id="cc551-160">Hello에 대 한 한 다음 Salesforce Sandbox의 인스턴스를 이미 추가한 경우 **엔터티 ID** hello에서 형식을 **로그온 URL**를이 형식에:`http://company.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="cc551-160">If you have already added an instance of Salesforce Sandbox, then for hello **Entity ID** type in hello **Sign On URL**, which should be in this format: `http://company.my.salesforce.com`</span></span>   
 4. <span data-ttu-id="cc551-161">클릭 **찾아보기** tooupload hello 인증서를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc551-161">Click **Browse** tooupload hello downloaded certificate.</span></span>  
 5. <span data-ttu-id="cc551-162">으로 **SAML Id 유형**선택, **어설션 hello 사용자 개체에서 hello 페더레이션 ID가 포함 되어**합니다.</span><span class="sxs-lookup"><span data-stu-id="cc551-162">As **SAML Identity Type**, select **Assertion contains hello Federation ID from hello User object**.</span></span> 
 6. <span data-ttu-id="cc551-163">으로 **SAML Id 위치**선택, **hello hello Subject 문의 NameIdentifier 요소에 Id가**합니다.</span><span class="sxs-lookup"><span data-stu-id="cc551-163">As **SAML Identity Location**, select **Identity is in hello NameIdentifier element of hello Subject statement**.</span></span>
 7. <span data-ttu-id="cc551-164">Hello hello에 Azure 클래식 포털에서에서 **Salesforce 샌드박스에서 single sign on 구성** 대화 상자 페이지에서 복사 hello **원격 로그인 URL** 값을 복사한 다음 hello에 붙여 넣을 **Id 공급자 로그인 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="cc551-164">In hello Azure classic portal, on hello **Configure single sign-on at Salesforce Sandbox** dialogue page, copy hello **Remote Login URL** value, and then paste it into hello **Identity Provider Login URL** textbox.</span></span> 
 8. <span data-ttu-id="cc551-165">SFDC는 SAML 로그아웃을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cc551-165">SFDC does not support SAML logout.</span></span>  <span data-ttu-id="cc551-166">문제를 해결 붙여 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0' hello로 **Identity Provider Logout URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="cc551-166">As a workaround, paste 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0' it into hello **Identity Provider Logout URL** textbox.</span></span>
 9. <span data-ttu-id="cc551-167">**서비스 공급자가 시작한 요청 바인딩**에서 **HTTP Post**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cc551-167">As **Service Provider Initiated Request Binding**, select **HTTP POST**.</span></span> 
 10. <span data-ttu-id="cc551-168">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cc551-168">Click **Save**.</span></span>
11. <span data-ttu-id="cc551-169">Azure 클래식 포털 hello에 hello single sign on 구성 확인을 선택한 다음 클릭 **완료** tooclose hello **Single Sign-on 구성** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="cc551-169">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="cc551-170">![Single Sign-On 구성](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781028.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="cc551-170">![Configure Single Sign-On](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781028.png "Configure Single Sign-On")</span></span>

## <a name="enable-your-domain"></a><span data-ttu-id="cc551-171">도메인 활성화</span><span class="sxs-lookup"><span data-stu-id="cc551-171">Enable your domain</span></span>
<span data-ttu-id="cc551-172">이 섹션에서는 이미 도메인을 만들었다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="cc551-172">This section assumes that you already have created a domain.</span></span>  <span data-ttu-id="cc551-173">자세한 내용은 [도메인 이름 정의](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cc551-173">For more details, see [Defining Your Domain Name](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).</span></span>

<span data-ttu-id="cc551-174">**tooenable 해당 도메인을 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="cc551-174">**tooenable your domain, perform hello following steps:**</span></span>

1. <span data-ttu-id="cc551-175">Hello 왼쪽된 탐색 창에서 클릭 **도메인 관리**, 클릭 하 고 **내 도메인입니다.**</span><span class="sxs-lookup"><span data-stu-id="cc551-175">In hello left navigation pane, click **Domain Management**, and then click **My Domain.**</span></span>
   
   <span data-ttu-id="cc551-176">![내 도메인](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781029.png "내 도메인")</span><span class="sxs-lookup"><span data-stu-id="cc551-176">![My Domain](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781029.png "My Domain")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="cc551-177">도메인이 올바르게 구성되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cc551-177">Please make sure that your domain has been configured correctly.</span></span> 
   > 
2. <span data-ttu-id="cc551-178">Hello에 **로그인 페이지 설정** 섹션에서 클릭 **편집**,으로 다음 **인증 서비스**선택, 이전 hello에서 hello SAML Single Sign-on 설정의 hello 이름 섹션을 마지막으로 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="cc551-178">In hello **Login Page Settings** section, click **Edit**, then, as **Authentication Service**, select hello name of hello SAML Single Sign-On Setting from hello previous section, and finally click **Save**.</span></span>
   
   <span data-ttu-id="cc551-179">![내 도메인](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781030.png "내 도메인")</span><span class="sxs-lookup"><span data-stu-id="cc551-179">![My Domain](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781030.png "My Domain")</span></span>

<span data-ttu-id="cc551-180">구성 된 도메인이 되는 즉시 사용자가 hello 도메인 URL toologin toohello Salesforce sandbox를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc551-180">As soon as you have a domain configured, your users should use hello domain URL toologin toohello Salesforce sandbox.</span></span>  

<span data-ttu-id="cc551-181">hello URL tooget hello 값 hello 이전 섹션에서 만든 hello SSO 프로필을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc551-181">tooget hello value of hello URL, click hello SSO profile you have created in hello previous section.</span></span>

## <a name="configure-user-provisioning"></a><span data-ttu-id="cc551-182">사용자 프로비전 구성</span><span class="sxs-lookup"><span data-stu-id="cc551-182">Configure user provisioning</span></span>
<span data-ttu-id="cc551-183">이 섹션의 hello 목적은 toooutline 어떻게 tooSalesforce 샌드박스 계정 tooenable Active Directory 사용자의 사용자 프로 비전 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc551-183">hello objective of this section is toooutline how tooenable user provisioning of Active Directory user accounts tooSalesforce Sandbox.</span></span>

<span data-ttu-id="cc551-184">**tooconfigure 사용자 프로비저닝, hello 다음 단계를 수행:**</span><span class="sxs-lookup"><span data-stu-id="cc551-184">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="cc551-185">Hello 위쪽 탐색 모음에서 hello Salesforce 포털에서 사용자 메뉴 이름 tooexpand 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc551-185">In hello Salesforce portal, in hello top navigation bar, select your name tooexpand your user menu:</span></span>
   
   <span data-ttu-id="cc551-186">![내 설정](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698773.png "내 설정")</span><span class="sxs-lookup"><span data-stu-id="cc551-186">![My Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698773.png "My Settings")</span></span>
2. <span data-ttu-id="cc551-187">사용자 메뉴에서 선택 **내 설정** tooopen 프로그램 **내 설정** 페이지.</span><span class="sxs-lookup"><span data-stu-id="cc551-187">From your user menu, select **My Settings** tooopen your **My Settings** page.</span></span>
3. <span data-ttu-id="cc551-188">Hello 왼쪽된 창에서 클릭 **개인** tooexpand 개인 섹션 hello 및 클릭 **Reset My Security Token**:</span><span class="sxs-lookup"><span data-stu-id="cc551-188">In hello left pane, click **Personal** tooexpand hello Personal section, and then click **Reset My Security Token**:</span></span>
   
   <span data-ttu-id="cc551-189">![내 설정](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698774.png "내 설정")</span><span class="sxs-lookup"><span data-stu-id="cc551-189">![My Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698774.png "My Settings")</span></span>
4. <span data-ttu-id="cc551-190">Hello에 **Reset My Security Token** 페이지 **보안 토큰 재설정** toorequest Salesforce.com 보안 토큰이 포함 된 전자 메일입니다.</span><span class="sxs-lookup"><span data-stu-id="cc551-190">On hello **Reset My Security Token** page, click **Reset Security Token** toorequest an email that contains your Salesforce.com security token.</span></span>
   
   <span data-ttu-id="cc551-191">![새 토큰](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698776.png "새 토큰")</span><span class="sxs-lookup"><span data-stu-id="cc551-191">![New Token](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698776.png "New Token")</span></span>
5. <span data-ttu-id="cc551-192">"**Salesforce.com.com 보안 확인**"을 제목으로 Salesforce.com에서 온 이메일의 받은 편지함을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cc551-192">Check your email inbox for an email from Salesforce.com with “**salesforce.com.com security confirmation**” as subject.</span></span>
6. <span data-ttu-id="cc551-193">이 전자 메일 및 복사 hello 보안 토큰 값을 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc551-193">Review this email and copy hello security token value.</span></span>
7. <span data-ttu-id="cc551-194">Hello hello에 Azure 클래식 포털에서에서 **salesforce Sandbox** 응용 프로그램 통합 페이지에서 클릭 **사용자 프로비저닝을 구성할** tooopen hello **사용자 프로비저닝 구성**대화 상자.</span><span class="sxs-lookup"><span data-stu-id="cc551-194">In hello Azure classic portal, on hello **salesforce Sandbox** application integration page, click **Configure user provisioning** tooopen hello **Configure User Provisioning** dialog.</span></span>
   
   <span data-ttu-id="cc551-195">![사용자 프로비전 구성](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769573.png "사용자 프로비전 구성")</span><span class="sxs-lookup"><span data-stu-id="cc551-195">![Configure user provisioning](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769573.png "Configure user provisioning")</span></span>
8. <span data-ttu-id="cc551-196">Hello에 **프로그램 Salesforce Sandbox 자격 증명 tooenable 자동 사용자 프로비저닝 입력** 페이지 hello 다음 구성 설정을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc551-196">On hello **Enter your Salesforce Sandbox credentials tooenable automatic user provisioning** page, provide hello following configuration settings:</span></span>
   
   <span data-ttu-id="cc551-197">![Salesforce 샌드박스](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746476.png "Salesforce 샌드박스")</span><span class="sxs-lookup"><span data-stu-id="cc551-197">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746476.png "Salesforce Sandbox")</span></span>   
 1. <span data-ttu-id="cc551-198">Hello에 **Salesforce Sandbox 관리자 사용자 이름** 텍스트 상자에 Salesforce 계정에 hello 이름 **시스템 관리자** 할당 Salesforce.com에 프로필입니다.</span><span class="sxs-lookup"><span data-stu-id="cc551-198">In hello **Salesforce Sandbox Admin User Name** textbox, type a Salesforce sandbox account name that has hello **System Administrator** profile in Salesforce.com assigned.</span></span>
 2. <span data-ttu-id="cc551-199">Hello에 **Salesforce Sandbox 관리자 암호** textbox를이 계정에 대 한 hello 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc551-199">In hello **Salesforce Sandbox Admin Password** textbox, type hello password for this account.</span></span>
 3. <span data-ttu-id="cc551-200">Hello에 **사용자 보안 토큰** 텍스트 붙여넣기 hello 보안 토큰 값입니다.</span><span class="sxs-lookup"><span data-stu-id="cc551-200">In hello **User Security Token** textbox, paste hello security token value.</span></span>
 4. <span data-ttu-id="cc551-201">클릭 **유효성 검사** tooverify 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc551-201">Click **Validate** tooverify your configuration.</span></span>
 5. <span data-ttu-id="cc551-202">Hello 클릭 **다음** 단추 tooopen hello **확인** 페이지.</span><span class="sxs-lookup"><span data-stu-id="cc551-202">Click hello **Next** button tooopen hello **Confirmation** page.</span></span>
9. <span data-ttu-id="cc551-203">Hello에 **확인** 페이지 **완료** toosave 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc551-203">On hello **Confirmation** page, click **Complete** toosave your configuration.</span></span>
   
## <a name="assigning-users"></a><span data-ttu-id="cc551-204">사용자 할당</span><span class="sxs-lookup"><span data-stu-id="cc551-204">Assigning users</span></span>

<span data-ttu-id="cc551-205">tootest 구성에 tooallow 할당 하 여 응용 프로그램 액세스 tooit를 사용 하 여 원하는 toogrant hello Azure AD 사용자가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc551-205">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="cc551-206">**tooassign 사용자 tooSalesforce 샌드박스 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="cc551-206">**tooassign users tooSalesforce Sandbox, perform hello following steps:**</span></span>

1. <span data-ttu-id="cc551-207">Azure 클래식 포털 hello 테스트 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cc551-207">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="cc551-208">Hello에 * * Salesforce Sandbox * * 응용 프로그램 통합 페이지에서 클릭 **사용자 할당**합니다.</span><span class="sxs-lookup"><span data-stu-id="cc551-208">On hello **Salesforce Sandbox **application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="cc551-209">![사용자 할당](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769574.png "사용자 할당")</span><span class="sxs-lookup"><span data-stu-id="cc551-209">![Assign users](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769574.png "Assign users")</span></span>
3. <span data-ttu-id="cc551-210">테스트 사용자 선택, 클릭 **할당**, 클릭 하 고 **예** tooconfirm 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc551-210">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
   <span data-ttu-id="cc551-211">![예](./media/active-directory-saas-salesforce-sandbox-tutorial/IC767830.png "예")</span><span class="sxs-lookup"><span data-stu-id="cc551-211">![Yes](./media/active-directory-saas-salesforce-sandbox-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="cc551-212">이제 10 분 동안 기다렸다가 hello 계정 동기화 된 tooSalesforce 샌드박스 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc551-212">You should now wait for 10 minutes and verify that hello account has been synchronized tooSalesforce Sandbox.</span></span>

<span data-ttu-id="cc551-213">SSO 설정 tootest 원하는 hello 액세스 패널을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="cc551-213">If you want tootest your SSO settings, open hello Access Panel.</span></span> <span data-ttu-id="cc551-214">액세스 패널 hello에 대 한 자세한 내용은 참조 하십시오. [액세스 패널 소개 toohello](https://msdn.microsoft.com/library/dn308586)합니다.</span><span class="sxs-lookup"><span data-stu-id="cc551-214">For more details about hello Access Panel, see [Introduction toohello Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

