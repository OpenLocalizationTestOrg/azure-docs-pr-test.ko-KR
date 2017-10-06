---
title: "자습서: Central Desktop와 Azure Active Directory 통합 | Microsoft Docs"
description: "어떻게 tooenable Azure Active Directory와 Central Desktop toouse single sign on, 자동화 된 프로비저닝 및 더에 대해 알아봅니다."
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: b805d485-93db-49b4-807a-18d446c7090e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 93036ae801c446ce476288c00579931ba10a843b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-central-desktop"></a><span data-ttu-id="f7754-103">자습서: Central Desktop와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="f7754-103">Tutorial: Azure Active Directory integration with Central Desktop</span></span>
<span data-ttu-id="f7754-104">hello이이 자습서는 Azure와 Central Desktop tooshow hello 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7754-104">hello objective of this tutorial is tooshow hello integration of Azure and Central Desktop.</span></span> <span data-ttu-id="f7754-105">이 자습서에 설명 된 hello 시나리오 다음 항목 hello 이미 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7754-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="f7754-106">유효한 Azure 구독</span><span class="sxs-lookup"><span data-stu-id="f7754-106">A valid Azure subscription</span></span>
* <span data-ttu-id="f7754-107">Central desktop single sign on가 설정된 구독 / Central desktop 테넌트</span><span class="sxs-lookup"><span data-stu-id="f7754-107">A Central desktop single sign on enabled subscription / Central desktop tenant</span></span>

<span data-ttu-id="f7754-108">이 자습서에 설명 된 hello 시나리오 hello 빌딩 블록을 다음으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7754-108">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

* <span data-ttu-id="f7754-109">Central Desktop에 대 한 hello 응용 프로그램 통합 사용</span><span class="sxs-lookup"><span data-stu-id="f7754-109">Enabling hello application integration for Central Desktop</span></span>
* <span data-ttu-id="f7754-110">SSO(Single Sign-On) 구성</span><span class="sxs-lookup"><span data-stu-id="f7754-110">Configuring single sign-on (SSO)</span></span>
* <span data-ttu-id="f7754-111">사용자 프로비전 구성</span><span class="sxs-lookup"><span data-stu-id="f7754-111">Configuring user provisioning</span></span>
* <span data-ttu-id="f7754-112">사용자 할당</span><span class="sxs-lookup"><span data-stu-id="f7754-112">Assigning users</span></span>

<span data-ttu-id="f7754-113">![시나리오](./media/active-directory-saas-central-desktop-tutorial/IC769558.png "시나리오")</span><span class="sxs-lookup"><span data-stu-id="f7754-113">![Scenario](./media/active-directory-saas-central-desktop-tutorial/IC769558.png "Scenario")</span></span>

## <a name="enable-hello-application-integration-for-central-desktop"></a><span data-ttu-id="f7754-114">Central Desktop에 대 한 hello 응용 프로그램 통합을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="f7754-114">Enable hello application integration for Central Desktop</span></span>
<span data-ttu-id="f7754-115">hello이이 섹션의 목적은 toooutline 어떻게 Central Desktop에 대 한 tooenable hello 응용 프로그램 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7754-115">hello objective of this section is toooutline how tooenable hello application integration for Central Desktop.</span></span>

<span data-ttu-id="f7754-116">**Central Desktop에 대 한 tooenable hello 응용 프로그램 통합 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="f7754-116">**tooenable hello application integration for Central Desktop, perform hello following steps:**</span></span>

1. <span data-ttu-id="f7754-117">Hello hello 왼쪽된 탐색 창에서 Azure 클래식 포털에서에서 클릭 **Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="f7754-117">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="f7754-118">![Active Directory](./media/active-directory-saas-central-desktop-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="f7754-118">![Active Directory](./media/active-directory-saas-central-desktop-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="f7754-119">Hello에서 **디렉터리** 목록, 선택 hello 디렉터리 tooenable 디렉터리 통합을 구하려는 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7754-119">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="f7754-120">tooopen hello 응용 프로그램 보기 hello 디렉터리 보기에서 클릭 **응용 프로그램** hello 상단 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7754-120">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
   <span data-ttu-id="f7754-121">![응용 프로그램](./media/active-directory-saas-central-desktop-tutorial/IC700994.png "응용 프로그램")</span><span class="sxs-lookup"><span data-stu-id="f7754-121">![Applications](./media/active-directory-saas-central-desktop-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="f7754-122">클릭 **추가** hello hello 페이지 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7754-122">Click **Add** at hello bottom of hello page.</span></span>
   
   <span data-ttu-id="f7754-123">![응용 프로그램 추가](./media/active-directory-saas-central-desktop-tutorial/IC749321.png "응용 프로그램 추가")</span><span class="sxs-lookup"><span data-stu-id="f7754-123">![Add application](./media/active-directory-saas-central-desktop-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="f7754-124">Hello에 **하 신 toodo 원하는** 대화 상자에서 클릭 **hello 갤러리에서 응용 프로그램 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="f7754-124">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
   <span data-ttu-id="f7754-125">![갤러리에서 응용 프로그램 추가](./media/active-directory-saas-central-desktop-tutorial/IC749322.png "갤러리에서 응용 프로그램 추가")</span><span class="sxs-lookup"><span data-stu-id="f7754-125">![Add an application from gallerry](./media/active-directory-saas-central-desktop-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="f7754-126">Hello에 **검색 상자**, 형식 **Central Desktop**합니다.</span><span class="sxs-lookup"><span data-stu-id="f7754-126">In hello **search box**, type **Central Desktop**.</span></span>
   
   <span data-ttu-id="f7754-127">![응용 프로그램 갤러리](./media/active-directory-saas-central-desktop-tutorial/IC769559.png "응용 프로그램 갤러리")</span><span class="sxs-lookup"><span data-stu-id="f7754-127">![Application gallery](./media/active-directory-saas-central-desktop-tutorial/IC769559.png "Application gallery")</span></span>
7. <span data-ttu-id="f7754-128">Hello 결과 창에서 선택 **Central Desktop**, 클릭 하 고 **완료** tooadd hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="f7754-128">In hello results pane, select **Central Desktop**, and then click **Complete** tooadd hello application.</span></span>
   
   <span data-ttu-id="f7754-129">![Central Desktop](./media/active-directory-saas-central-desktop-tutorial/IC769560.png "Central Desktop")</span><span class="sxs-lookup"><span data-stu-id="f7754-129">![Central Desktop](./media/active-directory-saas-central-desktop-tutorial/IC769560.png "Central Desktop")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="f7754-130">Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="f7754-130">Configure single sign-on</span></span>

<span data-ttu-id="f7754-131">hello이이 섹션의 목적은 toooutline 페더레이션을 사용 하 여 Azure AD에서 자신의 계정으로 tooenable 사용자 tooauthenticate tooCentral 데스크톱 hello SAML 프로토콜에 따라 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="f7754-131">hello objective of this section is toooutline how tooenable users tooauthenticate tooCentral Desktop with their account in Azure AD using federation based on hello SAML protocol.</span></span>

<span data-ttu-id="f7754-132">이 절차의 일부로 필수 tooupload e-64로 인코딩된 인증서 tooyour Central Desktop 테 넌 트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7754-132">As part of this procedure, you are required tooupload a base-64 encoded certificate tooyour Central Desktop tenant.</span></span>  
<span data-ttu-id="f7754-133">이 절차에 익숙하지 않은 경우 참조 [어떻게 tooconvert 이진은 텍스트 파일에을 인증서](http://youtu.be/PlgrzUZ-Y1o)합니다.</span><span class="sxs-lookup"><span data-stu-id="f7754-133">If you are not familiar with this procedure, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>

<span data-ttu-id="f7754-134">**tooconfigure 단일 로그온 hello 다음 단계를 수행 하십시오.**</span><span class="sxs-lookup"><span data-stu-id="f7754-134">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="f7754-135">Hello hello에 Azure 클래식 포털에서에서 **Central Desktop** 응용 프로그램 통합 페이지에서 클릭 **single sign on 구성** tooopen hello * * Single Sign-on 구성 * * 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="f7754-135">In hello Azure classic portal, on hello **Central Desktop** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On ** dialog.</span></span>
   
   <span data-ttu-id="f7754-136">![Single Sign-On 구성](./media/active-directory-saas-central-desktop-tutorial/IC749323.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="f7754-136">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC749323.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="f7754-137">Hello에 **어떻게 tooCentral 바탕 화면에 사용자가 toosign 보 시겠습니까** 페이지에서 **Microsoft Azure AD Single Sign-on**, 클릭 하 고 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="f7754-137">On hello **How would you like users toosign on tooCentral Desktop** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="f7754-138">![Single Sign-On 구성](./media/active-directory-saas-central-desktop-tutorial/IC777628.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="f7754-138">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC777628.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="f7754-139">Hello에 **앱 URL 구성** 페이지 hello 다음 단계를 수행 하 고 클릭 **다음**:</span><span class="sxs-lookup"><span data-stu-id="f7754-139">On hello **Configure App URL** page, perform hello following steps, and then click **Next**:</span></span> 
   
   1. <span data-ttu-id="f7754-140">Hello에 **중앙 데스크톱 로그인 URL** textbox Central Desktop 테 넌 트의 hello URL 입력 (예:: *http://contoso.centraldesktop.com*).</span><span class="sxs-lookup"><span data-stu-id="f7754-140">In hello **Central Desktop Sign In URL** textbox, type hello URL of your Central Desktop tenant (e.g.: *http://contoso.centraldesktop.com*).</span></span>
   2. <span data-ttu-id="f7754-141">Hello Central Desktop 회신 URL 텍스트 상자에 Central Desktop AssertionConsumerService URL (예:: https://contoso.centraldesktop.com/saml2-assertion.php).</span><span class="sxs-lookup"><span data-stu-id="f7754-141">In hello Central  Desktop Reply URL textbox, type your Central Desktop AssertionConsumerService URL (e.g.:  https://contoso.centraldesktop.com/saml2-assertion.php).</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="f7754-142">Hello central desktop 메타 데이터에서 hello 값을 가져올 수 있습니다 (예:: *http://contoso.centraldesktop.com*).</span><span class="sxs-lookup"><span data-stu-id="f7754-142">You can get hello value from hello central desktop metadata (e.g.: *http://contoso.centraldesktop.com*).</span></span>
   >  
   
   <span data-ttu-id="f7754-143">![앱 URL 구성](./media/active-directory-saas-central-desktop-tutorial/IC769561.png "앱 URL 구성")</span><span class="sxs-lookup"><span data-stu-id="f7754-143">![Configure app URL](./media/active-directory-saas-central-desktop-tutorial/IC769561.png "Configure app URL")</span></span>
4. <span data-ttu-id="f7754-144">Hello에 **Central Desktop에서 single sign on 구성** 페이지, toodownload 인증서를 클릭 하 여 **다운로드 인증서**, hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7754-144">On hello **Configure single sign-on at Central Desktop** page, toodownload your certificate, click **Download certificate**, and then save hello certificate file on your computer.</span></span>
   
  <span data-ttu-id="f7754-145">![Single Sign-On 구성](./media/active-directory-saas-central-desktop-tutorial/IC769562.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="f7754-145">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC769562.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="f7754-146">Tooyour 로그인 **Central Desktop** 테 넌 트입니다.</span><span class="sxs-lookup"><span data-stu-id="f7754-146">Log in tooyour **Central Desktop** tenant.</span></span>
6. <span data-ttu-id="f7754-147">너무 이동**설정**, 클릭 **고급**, 클릭 하 고 **Single Sign On**합니다.</span><span class="sxs-lookup"><span data-stu-id="f7754-147">Go too**Settings**, click **Advanced**, and then click **Single Sign On**.</span></span>
   
  <span data-ttu-id="f7754-148">![설정 - 고급](./media/active-directory-saas-central-desktop-tutorial/IC769563.png "설정 - 고급")</span><span class="sxs-lookup"><span data-stu-id="f7754-148">![Setup - Advanced](./media/active-directory-saas-central-desktop-tutorial/IC769563.png "Setup - Advanced")</span></span>
7. <span data-ttu-id="f7754-149">Hello에 **Single Sign-on 설정** 페이지 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7754-149">On hello **Single Sign On Settings** page, perform hello following steps:</span></span>
   
  <span data-ttu-id="f7754-150">![Single Sign On 설정](./media/active-directory-saas-central-desktop-tutorial/IC769564.png "Single Sign On 설정")</span><span class="sxs-lookup"><span data-stu-id="f7754-150">![Single Sign On Settings](./media/active-directory-saas-central-desktop-tutorial/IC769564.png "Single Sign On Settings")</span></span>
   
  1. <span data-ttu-id="f7754-151">**SAML v2 Single Sign-On 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f7754-151">Select **Enable SAML v2 Single Sign On**.</span></span>
  2. <span data-ttu-id="f7754-152">Hello hello에 Azure 클래식 포털에서에서 **Central Desktop에서 single sign on 구성** 페이지, 복사 hello **발급자 URL** 값을 복사한 다음 hello에 붙여 넣을 **SSO URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="f7754-152">In hello Azure classic portal, on hello **Configure single sign-on at Central Desktop** page, copy hello **Issuer URL** value, and then paste it into hello **SSO URL** textbox.</span></span>
  3. <span data-ttu-id="f7754-153">Hello hello에 Azure 클래식 포털에서에서 **Central Desktop에서 single sign on 구성** 페이지, 복사 hello **원격 로그인 URL** 값을 복사한 다음 hello에 붙여 넣을 **SSO 로그인 URL**텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="f7754-153">In hello Azure classic portal, on hello **Configure single sign-on at Central Desktop** page, copy hello **Remote Login URL** value, and then paste it into hello **SSO Login URL** textbox.</span></span>
  4. <span data-ttu-id="f7754-154">Hello hello에 Azure 클래식 포털에서에서 **Central Desktop에서 single sign on 구성** 페이지, 복사 hello **Single Sign-Out 서비스 URL** 값을 복사한 다음 hello에 붙여 넣을 **SSO로그아웃URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="f7754-154">In hello Azure classic portal, on hello **Configure single sign-on at Central Desktop** page, copy hello **Single Sign-Out Service URL** value, and then paste it into hello **SSO Logout URL** textbox.</span></span>
8. <span data-ttu-id="f7754-155">Hello에 **메시지 서명 확인 방법** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7754-155">In hello **Message Signature Verification Method** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="f7754-156">![메시지 서명 확인 방법](./media/active-directory-saas-central-desktop-tutorial/IC769565.png "메시지 서명 확인 방법")</span><span class="sxs-lookup"><span data-stu-id="f7754-156">![Message Signature Verification Method](./media/active-directory-saas-central-desktop-tutorial/IC769565.png "Message Signature Verification Method")</span></span>
   
  1. <span data-ttu-id="f7754-157">**인증서**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f7754-157">Select **Certificate**.</span></span>
  2. <span data-ttu-id="f7754-158">Hello에서 **SSO 인증서** 목록에서 **RSH SHA256**합니다.</span><span class="sxs-lookup"><span data-stu-id="f7754-158">From hello **SSO Certificate** list, select **RSH SHA256**.</span></span>
  3. <span data-ttu-id="f7754-159">인증서 다운로드 hello hello 텍스트 파일의 콘텐츠 복사 hello에서에서 텍스트 파일을 만들고 hello에 붙여 넣습니다 **SSO 인증서** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="f7754-159">Create a text file from hello downloaded certificate, copy hello content of hello text file, and then paste it into hello **SSO Certificate** field.</span></span>  
     >[!TIP]
     ><span data-ttu-id="f7754-160">자세한 내용은 참조 하십시오. [어떻게 tooconvert 이진은 텍스트 파일에을 인증서](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="f7754-160">For more details, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>
      >  
   4. <span data-ttu-id="f7754-161">선택 **링크 tooyour SAMLv2 로그인 페이지를 표시**합니다.</span><span class="sxs-lookup"><span data-stu-id="f7754-161">Select **Display a link tooyour SAMLv2 login page**.</span></span>
9. <span data-ttu-id="f7754-162">**업데이트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7754-162">Click **Update**.</span></span>
10. <span data-ttu-id="f7754-163">Azure 클래식 포털 hello에 hello single sign on 구성 확인을 선택한 다음 클릭 **완료** tooclose hello **Single Sign-on 구성** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="f7754-163">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="f7754-164">![Single Sign-On 구성](./media/active-directory-saas-central-desktop-tutorial/IC769566.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="f7754-164">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC769566.png "Configure single sign-on")</span></span>
    
## <a name="configure-user-provisioning"></a><span data-ttu-id="f7754-165">사용자 프로비전 구성</span><span class="sxs-lookup"><span data-stu-id="f7754-165">Configure user provisioning</span></span>

<span data-ttu-id="f7754-166">AAD 사용자 toobe 수 toosign에서, 프로 비전 된 toohello Central Desktop 응용 프로그램 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7754-166">For AAD users toobe able toosign in, they must be provisioned toohello Central Desktop application.</span></span> <span data-ttu-id="f7754-167">이 섹션에서는 Central Desktop에서 toocreate AAD 사용자 계정을 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7754-167">This section describes how toocreate AAD user accounts in Central Desktop.</span></span>

<span data-ttu-id="f7754-168">**tooprovision 사용자 계정 tooCentral 바탕 화면:**</span><span class="sxs-lookup"><span data-stu-id="f7754-168">**tooprovision user accounts tooCentral Desktop:**</span></span>
1. <span data-ttu-id="f7754-169">Central Desktop 테 넌 트 tooyour에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7754-169">Log in tooyour Central Desktop tenant.</span></span>
2. <span data-ttu-id="f7754-170">너무 이동**사람 \> 내부 멤버**합니다.</span><span class="sxs-lookup"><span data-stu-id="f7754-170">Go too**People \> Internal Members**.</span></span>
3. <span data-ttu-id="f7754-171">**내부 멤버 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7754-171">Click **Add Internal Members**.</span></span>
   
  <span data-ttu-id="f7754-172">![사람](./media/active-directory-saas-central-desktop-tutorial/IC781051.png "사람")</span><span class="sxs-lookup"><span data-stu-id="f7754-172">![People](./media/active-directory-saas-central-desktop-tutorial/IC781051.png "People")</span></span>
4. <span data-ttu-id="f7754-173">Hello에 **새 멤버의 전자 메일 주소** textbox tooprovision을 차례로 클릭 AAD 계정을 입력 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="f7754-173">In hello **Email Address of New Members** textbox, type an AAD account you want tooprovision, and then click **Next**.</span></span>
   
  <span data-ttu-id="f7754-174">![새 멤버의 전자 메일 주소](./media/active-directory-saas-central-desktop-tutorial/IC781052.png "새 멤버의 전자 메일 주소")</span><span class="sxs-lookup"><span data-stu-id="f7754-174">![Email Addresses of New Members](./media/active-directory-saas-central-desktop-tutorial/IC781052.png "Email Addresses of New Members")</span></span>
5. <span data-ttu-id="f7754-175">**내부 멤버 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7754-175">Click **Add Internal member(s)**.</span></span>
   
  <span data-ttu-id="f7754-176">![내부 멤버 추가](./media/active-directory-saas-central-desktop-tutorial/IC781053.png "내부 멤버 추가")</span><span class="sxs-lookup"><span data-stu-id="f7754-176">![Add Internal Member](./media/active-directory-saas-central-desktop-tutorial/IC781053.png "Add Internal Member")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="f7754-177">추가한 hello 사용자 tooclick tooactivate hello 계정 필요한 확인 링크를 포함 하는 메일을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7754-177">hello users you have added will receive an email that includes a confirmation link they need tooclick tooactivate hello account.</span></span>
   > 

>[!NOTE]
><span data-ttu-id="f7754-178">다른 Central Desktop 사용자 계정 만들기 도구를 사용할 수 있습니다 또는 AAD 사용자 계정을 tooprovision Central Desktop에서 제공 된 Api</span><span class="sxs-lookup"><span data-stu-id="f7754-178">You can use any other Central Desktop user account creation tools or APIs provided by Central Desktop tooprovision AAD user accounts</span></span>
>  

## <a name="assign-users"></a><span data-ttu-id="f7754-179">사용자 할당</span><span class="sxs-lookup"><span data-stu-id="f7754-179">Assign users</span></span>
<span data-ttu-id="f7754-180">tootest 구성에 tooallow 할당 하 여 응용 프로그램 액세스 tooit를 사용 하 여 원하는 toogrant hello Azure AD 사용자가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7754-180">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="f7754-181">**tooassign 사용자 tooCentral 바탕 화면 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="f7754-181">**tooassign users tooCentral Desktop, perform hello following steps:**</span></span>

1. <span data-ttu-id="f7754-182">Azure 클래식 포털 hello 테스트 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f7754-182">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="f7754-183">Hello에 **Central Desktop** 응용 프로그램 통합 페이지에서 클릭 **사용자 할당**합니다.</span><span class="sxs-lookup"><span data-stu-id="f7754-183">On hello **Central Desktop** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="f7754-184">![사용자 할당](./media/active-directory-saas-central-desktop-tutorial/IC769567.png "사용자 할당")</span><span class="sxs-lookup"><span data-stu-id="f7754-184">![Assign users](./media/active-directory-saas-central-desktop-tutorial/IC769567.png "Assign users")</span></span>
3. <span data-ttu-id="f7754-185">테스트 사용자 선택, 클릭 **할당**, 클릭 하 고 **예** tooconfirm 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7754-185">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
   <span data-ttu-id="f7754-186">![예](./media/active-directory-saas-central-desktop-tutorial/IC767830.png "예")</span><span class="sxs-lookup"><span data-stu-id="f7754-186">![Yes](./media/active-directory-saas-central-desktop-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="f7754-187">Single sign on 설정 tootest 원하는 hello 액세스 패널을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f7754-187">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="f7754-188">액세스 패널 hello에 대 한 자세한 내용은 참조 하십시오. [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f7754-188">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

