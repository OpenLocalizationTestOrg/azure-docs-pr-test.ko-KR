---
title: "자습서: SAP HANA Cloud Platform과 Azure Active Directory 통합 | Microsoft Docs"
description: "어떻게 tooenable Azure Active Directory와 SAP HANA Cloud Platform toouse single sign on, 자동화 된 프로비저닝 및 더에 대해 알아봅니다."
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: bd398225-8bd8-4697-9a44-af6e6679113a
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: cc6610969b1c7b08f776e6969a5977fc75eb9ab4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana-cloud-platform"></a><span data-ttu-id="e1de6-103">자습서: SAP HANA Cloud Platform과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="e1de6-103">Tutorial: Azure Active Directory integration with SAP HANA Cloud Platform</span></span>
<span data-ttu-id="e1de6-104">hello이이 자습서는 Azure와 SAP HANA Cloud Platform tooshow hello 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1de6-104">hello objective of this tutorial is tooshow hello integration of Azure and SAP HANA Cloud Platform.</span></span>

<span data-ttu-id="e1de6-105">이 자습서에 설명 된 hello 시나리오 다음 항목 hello 이미 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1de6-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="e1de6-106">유효한 Azure 구독</span><span class="sxs-lookup"><span data-stu-id="e1de6-106">A valid Azure subscription</span></span>
* <span data-ttu-id="e1de6-107">SAP HANA Cloud Platform 계정</span><span class="sxs-lookup"><span data-stu-id="e1de6-107">A SAP HANA Cloud Platform account</span></span>

<span data-ttu-id="e1de6-108">이 자습서를 완료 한 후 hello를 사용 하 여 hello 응용 프로그램에 수 toosingle 기호 HANA Cloud Platform 됩니다 tooSAP를 할당 한 Azure AD 사용자 hello [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e1de6-108">After completing this tutorial, hello Azure AD users you have assigned tooSAP HANA Cloud Platform will be able toosingle sign into hello application using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

>[!IMPORTANT]
><span data-ttu-id="e1de6-109">Toodeploy 사용자의 응용 프로그램 또는 단일 계정 tootest 로그온 하 여 SAP HANA Cloud Platform에 tooan 응용 프로그램을 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1de6-109">You need toodeploy your own application or subscribe tooan application on your SAP HANA Cloud Platform account tootest single sign on.</span></span> <span data-ttu-id="e1de6-110">이 자습서에서는 응용 프로그램은 hello 계정에 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1de6-110">In this tutorial, an application is deployed in hello account.</span></span>
> 
> 

<span data-ttu-id="e1de6-111">이 자습서에 설명 된 hello 시나리오 hello 빌딩 블록을 다음으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1de6-111">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

1. <span data-ttu-id="e1de6-112">SAP HANA Cloud Platform에 대 한 hello 응용 프로그램 통합 사용</span><span class="sxs-lookup"><span data-stu-id="e1de6-112">Enabling hello application integration for SAP HANA Cloud Platform</span></span>
2. <span data-ttu-id="e1de6-113">SSO(Single Sign-On) 구성</span><span class="sxs-lookup"><span data-stu-id="e1de6-113">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="e1de6-114">역할 tooa 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="e1de6-114">Assigning a role tooa user</span></span>
4. <span data-ttu-id="e1de6-115">사용자 할당</span><span class="sxs-lookup"><span data-stu-id="e1de6-115">Assigning users</span></span>

<span data-ttu-id="e1de6-116">![시나리오](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790795.png "시나리오")</span><span class="sxs-lookup"><span data-stu-id="e1de6-116">![Scenario](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790795.png "Scenario")</span></span>

## <a name="enabling-hello-application-integration-for-sap-hana-cloud-platform"></a><span data-ttu-id="e1de6-117">SAP HANA Cloud Platform에 대 한 hello 응용 프로그램 통합 사용</span><span class="sxs-lookup"><span data-stu-id="e1de6-117">Enabling hello application integration for SAP HANA Cloud Platform</span></span>
<span data-ttu-id="e1de6-118">이 섹션의 hello 목표 toooutline를 어떻게는 SAP HANA Cloud Platform에 대 한 tooenable hello 응용 프로그램 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1de6-118">hello objective of this section is toooutline how tooenable hello application integration for SAP HANA Cloud Platform.</span></span>

<span data-ttu-id="e1de6-119">**SAP HANA Cloud Platform에 대 한 tooenable hello 응용 프로그램 통합 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="e1de6-119">**tooenable hello application integration for SAP HANA Cloud Platform, perform hello following steps:**</span></span>

1. <span data-ttu-id="e1de6-120">Azure 관리 포털 hello hello 왼쪽된 탐색 창에서 클릭 **Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="e1de6-120">In hello Azure Management Portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="e1de6-121">![Active Directory](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="e1de6-121">![Active Directory](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="e1de6-122">Hello에서 **디렉터리** 목록, 선택 hello 디렉터리 tooenable 디렉터리 통합을 구하려는 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1de6-122">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="e1de6-123">tooopen hello 응용 프로그램 보기 hello 디렉터리 보기에서 클릭 **응용 프로그램** hello 상단 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1de6-123">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    <span data-ttu-id="e1de6-124">![응용 프로그램](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700994.png "응용 프로그램")</span><span class="sxs-lookup"><span data-stu-id="e1de6-124">![Applications](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="e1de6-125">클릭 **추가** hello hello 페이지 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1de6-125">Click **Add** at hello bottom of hello page.</span></span>
   
    <span data-ttu-id="e1de6-126">![응용 프로그램 추가](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749321.png "응용 프로그램 추가")</span><span class="sxs-lookup"><span data-stu-id="e1de6-126">![Add application](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="e1de6-127">Hello에 **하 신 toodo 원하는** 대화 상자에서 클릭 **hello 갤러리에서 응용 프로그램 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="e1de6-127">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    <span data-ttu-id="e1de6-128">![갤러리에서 응용 프로그램 추가](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749322.png "갤러리에서 응용 프로그램 추가")</span><span class="sxs-lookup"><span data-stu-id="e1de6-128">![Add an application from gallerry](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="e1de6-129">Hello에 **검색 상자**, 형식 **SAP HANA Cloud Platform**합니다.</span><span class="sxs-lookup"><span data-stu-id="e1de6-129">In hello **search box**, type **SAP HANA Cloud Platform**.</span></span>
   
    <span data-ttu-id="e1de6-130">![응용 프로그램 갤러리](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790796.png "응용 프로그램 갤러리")</span><span class="sxs-lookup"><span data-stu-id="e1de6-130">![Application Gallery](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790796.png "Application Gallery")</span></span>
7. <span data-ttu-id="e1de6-131">Hello 결과 창에서 선택 **SAP HANA Cloud Platform**, 클릭 하 고 **완료** tooadd hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="e1de6-131">In hello results pane, select **SAP HANA Cloud Platform**, and then click **Complete** tooadd hello application.</span></span>
   
    <span data-ttu-id="e1de6-132">![SAP Hana](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793929.png "SAP Hana")</span><span class="sxs-lookup"><span data-stu-id="e1de6-132">![SAP Hana](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793929.png "SAP Hana")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="e1de6-133">Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="e1de6-133">Configure single sign-on</span></span>

<span data-ttu-id="e1de6-134">hello이이 섹션의 목적은 toooutline 페더레이션을 사용 하 여 Azure AD에서 자신의 계정으로 tooenable 사용자 tooauthenticate tooSAP HANA Cloud Platform hello SAML 프로토콜에 따라 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="e1de6-134">hello objective of this section is toooutline how tooenable users tooauthenticate tooSAP HANA Cloud Platform with their account in Azure AD using federation based on hello SAML protocol.</span></span>

<span data-ttu-id="e1de6-135">이 절차의 일부로, 필요한 tooupload e-64로 인코딩된 인증서 tooyour SAP HANA Cloud Platform 테 넌 트가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1de6-135">As part of this procedure, you are required tooupload a base-64 encoded certificate tooyour SAP HANA Cloud Platform tenant.</span></span>  

<span data-ttu-id="e1de6-136">이 절차에 익숙하지 않은 경우 참조 [어떻게 tooconvert 이진은 텍스트 파일에을 인증서](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="e1de6-136">If you are not familiar with this procedure, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>

<span data-ttu-id="e1de6-137">**tooconfigure 단일 로그온 hello 다음 단계를 수행 하십시오.**</span><span class="sxs-lookup"><span data-stu-id="e1de6-137">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="e1de6-138">Hello hello에 Azure 클래식 포털에서에서 **SAP HANA Cloud Platform** 응용 프로그램 통합 페이지에서 클릭 **single sign on 구성** tooopen hello **Single Sign-on 구성**대화 상자.</span><span class="sxs-lookup"><span data-stu-id="e1de6-138">In hello Azure classic portal, on hello **SAP HANA Cloud Platform** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="e1de6-139">![Single Sign-On 구성](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC778552.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="e1de6-139">![Configure single sign-on](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC778552.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="e1de6-140">Hello에 **어떻게 tooSAP HANA Cloud Platform에 사용자가 toosign 보 시겠습니까** 페이지에서 **Microsoft Azure AD Single Sign-on**, 클릭 하 고 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="e1de6-140">On hello **How would you like users toosign on tooSAP HANA Cloud Platform** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="e1de6-141">![Single Sign-On 구성](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790797.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="e1de6-141">![Configure Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790797.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="e1de6-142">다른 웹 브라우저 창에서 https://account에서 toohello SAP HANA Cloud Platform Cockpit에 로그인 합니다. \<가로 호스트\>.ondemand.com/cockpit (예:: *https://account.hanatrial.ondemand.com/cockpit*).</span><span class="sxs-lookup"><span data-stu-id="e1de6-142">In a different web browser window, sign on toohello SAP HANA Cloud Platform Cockpit at https://account.\<landscape host\>.ondemand.com/cockpit (e.g.: *https://account.hanatrial.ondemand.com/cockpit*).</span></span>
4. <span data-ttu-id="e1de6-143">Hello 클릭 **신뢰** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1de6-143">Click hello **Trust** tab.</span></span>
   
    <span data-ttu-id="e1de6-144">![신뢰](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790800.png "신뢰")</span><span class="sxs-lookup"><span data-stu-id="e1de6-144">![Trust](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790800.png "Trust")</span></span>
5. <span data-ttu-id="e1de6-145">트러스트 관리 섹션에서 단계를 수행 하는 hello를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1de6-145">In trust management section, perform hello following steps:</span></span>
   
    <span data-ttu-id="e1de6-146">![메타 데이터 가져오기](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793930.png "메타 데이터 가져오기")</span><span class="sxs-lookup"><span data-stu-id="e1de6-146">![Get Metadata](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793930.png "Get Metadata")</span></span>
   
   1. <span data-ttu-id="e1de6-147">Hello 클릭 **Local Service Provider** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1de6-147">Click hello **Local Service Provider** tab.</span></span>
   2. <span data-ttu-id="e1de6-148">toodownload hello SAP HANA Cloud Platform 메타 데이터 파일을 클릭 하 여 **Get Metadata**합니다.</span><span class="sxs-lookup"><span data-stu-id="e1de6-148">toodownload hello SAP HANA Cloud Platform metadata file, click **Get Metadata**.</span></span>
6. <span data-ttu-id="e1de6-149">Hello 활성 Azure 클래식 포털 hello **앱 URL 구성** 페이지 hello 다음 단계를 수행 하 고 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="e1de6-149">In hello Azure Active classic portal, on hello **Configure App URL** page, perform hello following steps, and then click **Next**.</span></span>
   
    <span data-ttu-id="e1de6-150">![앱 URL 구성](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790798.png "앱 URL 구성")</span><span class="sxs-lookup"><span data-stu-id="e1de6-150">![Configure App URL](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790798.png "Configure App URL")</span></span>
   
   1. <span data-ttu-id="e1de6-151">Hello에 **로그온 URL** 텍스트 상자에 사용자가 toosign 프로그램에서 사용 하는 hello URL 입력 하면 **SAP HANA Cloud Platform** 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="e1de6-151">In hello **Sign On URL** textbox, type hello URL used by your users toosign into your **SAP HANA Cloud Platform** application.</span></span> <span data-ttu-id="e1de6-152">SAP HANA Cloud Platform 응용 프로그램에서 보호 된 리소스의 hello 계정별 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="e1de6-152">This is hello account-specific URL of a protected resource in your SAP HANA Cloud Platform application.</span></span> <span data-ttu-id="e1de6-153">hello URL 기반으로 패턴 hello: *https://\<applicationName\>\<accountName\>.\< 가로 호스트\>.ondemand.com/\<경로\_를\_보호\_리소스\>*  (예:: *https://xleavep1941203872trial.hanatrial.ondemand.com/xleave*)</span><span class="sxs-lookup"><span data-stu-id="e1de6-153">hello URL is based on hello following pattern: *https://\<applicationName\>\<accountName\>.\<landscape host\>.ondemand.com/\<path\_to\_protected\_resource\>* (e.g.: *https://xleavep1941203872trial.hanatrial.ondemand.com/xleave*)</span></span>
      
     >[!NOTE]
     ><span data-ttu-id="e1de6-154">Hello 사용자 tooauthenticate 필요한 SAP HANA Cloud Platform 응용 프로그램에 hello URL입니다.</span><span class="sxs-lookup"><span data-stu-id="e1de6-154">This is hello URL in your SAP HANA Cloud Platform application that requires hello user tooauthenticate.</span></span>
     > 

   2. <span data-ttu-id="e1de6-155">Hello 다운로드 한 SAP HANA Cloud Platform 메타 데이터 파일을 열고 찾은 후 hello **ns3:** 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="e1de6-155">Open hello downloaded SAP HANA Cloud Platform metadata file, and then locate hello **ns3:AssertionConsumerService** tag.</span></span>
   3. <span data-ttu-id="e1de6-156">Hello의 hello 값을 복사 **위치** 특성을 선택한 다음 hello에 붙여 넣을 **SAP HANA Cloud Platform 회신 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="e1de6-156">Copy hello value of hello **Location** attribute, and then paste it into hello **SAP HANA Cloud Platform Reply URL** textbox.</span></span>

7. <span data-ttu-id="e1de6-157">Hello에 **SAP HANA Cloud Platform에서 single sign on 구성** 페이지, toodownload 메타 데이터를 클릭 하 여 **메타 데이터 다운로드**, hello 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1de6-157">On hello **Configure single sign-on at SAP HANA Cloud Platform** page, toodownload your metadata, click **Download metadata**, and then save hello file on your computer.</span></span>
   
    <span data-ttu-id="e1de6-158">![Single Sign-On 구성](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790799.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="e1de6-158">![Configure Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790799.png "Configure Single Sign-On")</span></span>
8. <span data-ttu-id="e1de6-159">Hello에 SAP HANA Cloud Platform Cockpit hello에 **Local Service Provider** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1de6-159">On hello SAP HANA Cloud Platform Cockpit, in hello **Local Service Provider** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="e1de6-160">![신뢰 관리](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793931.png "신뢰 관리")</span><span class="sxs-lookup"><span data-stu-id="e1de6-160">![Trust Management](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793931.png "Trust Management")</span></span>
   
  1. <span data-ttu-id="e1de6-161">**편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e1de6-161">Click **Edit**.</span></span>
  2. <span data-ttu-id="e1de6-162">**구성 유형**으로 **사용자 지정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e1de6-162">As **Configuration Type**, select **Custom**.</span></span>
  3. <span data-ttu-id="e1de6-163">으로 **Local Provider Name**, hello 기본값을 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="e1de6-163">As **Local Provider Name**, leave hello default value.</span></span>
  4. <span data-ttu-id="e1de6-164">toogenerate는 **서명 키** 및 **서명 인증서** 키 쌍을 클릭 **Generate Key Pair**합니다.</span><span class="sxs-lookup"><span data-stu-id="e1de6-164">toogenerate a **Signing Key** and a **Signing Certificate** key pair, click **Generate Key Pair**.</span></span>
  5. <span data-ttu-id="e1de6-165">**주 전파**로 **사용 안 함**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e1de6-165">As **Principal Propagation**, select **Disabled**.</span></span>
  6. <span data-ttu-id="e1de6-166">**강제 인증**으로 **사용 안 함**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e1de6-166">As **Force Authentication**, select **Disabled**.</span></span>
  7. <span data-ttu-id="e1de6-167">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e1de6-167">Click **Save**.</span></span>

9. <span data-ttu-id="e1de6-168">Hello 클릭 **Trusted Identity Provider** 탭을 클릭 한 다음 **Add Trusted Identity Provider**합니다.</span><span class="sxs-lookup"><span data-stu-id="e1de6-168">Click hello **Trusted Identity Provider** tab, and then click **Add Trusted Identity Provider**.</span></span>
   
    <span data-ttu-id="e1de6-169">![신뢰 관리](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790802.png "신뢰 관리")</span><span class="sxs-lookup"><span data-stu-id="e1de6-169">![Trust Management](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790802.png "Trust Management")</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="e1de6-170">신뢰할 수 있는 id 공급자의 toomanage hello 목록 toohave hello Local Service Provider 섹션에서에서 Custom 구성 유형을 hello를 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1de6-170">toomanage hello list of trusted identity providers, you need toohave chosen hello Custom configuration type in hello Local Service Provider section.</span></span> <span data-ttu-id="e1de6-171">Default 구성 유형의 편집할 수 없는 암시적인 트러스트가 toohello SAP ID 서비스 구조가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1de6-171">For Default configuration type, you have a non-editable and implicit trust toohello SAP ID Service.</span></span> <span data-ttu-id="e1de6-172">없음의 경우 신뢰 설정이 필요 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e1de6-172">For None, you don't have any trust settings.</span></span>
    > 
    > 

10. <span data-ttu-id="e1de6-173">Hello 클릭 **일반** 탭을 클릭 한 다음 **찾아보기** tooupload hello 메타 데이터 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1de6-173">Click hello **General** tab, and then click **Browse** tooupload hello downloaded metadata file.</span></span>
    
    <span data-ttu-id="e1de6-174">![신뢰 관리](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793932.png "신뢰 관리")</span><span class="sxs-lookup"><span data-stu-id="e1de6-174">![Trust Management](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793932.png "Trust Management")</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="e1de6-175">Hello 메타 데이터 파일을 업로드 한 후 hello에 대 한 값 **Single Sign on URL**, **단일 로그 아웃 URL** 및 **서명 인증서** 가 자동으로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="e1de6-175">After uploading hello metadata file, hello values for **Single Sign-on URL**, **Single Logout URL** and **Signing Certificate** are populated automatically.</span></span>
    > 
    > 

11. <span data-ttu-id="e1de6-176">Hello 클릭 **특성** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1de6-176">Click hello **Attributes** tab.</span></span>
12. <span data-ttu-id="e1de6-177">Hello에 **특성** 탭 hello 다음 단계를 수행 하십시오.</span><span class="sxs-lookup"><span data-stu-id="e1de6-177">On hello **Attributes** tab, perform hello following step:</span></span>
    
    <span data-ttu-id="e1de6-178">![특성](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790804.png "특성")</span><span class="sxs-lookup"><span data-stu-id="e1de6-178">![Attributes](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790804.png "Attributes")</span></span> 
  * <span data-ttu-id="e1de6-179">클릭 **add assertion-based Attribute**, 다음 hello 다음 어설션 기반 특성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1de6-179">Click **Add Assertion-Based Attribute**, and then add hello following assertion-based attributes:</span></span>
       
    | <span data-ttu-id="e1de6-180">어설션 특성</span><span class="sxs-lookup"><span data-stu-id="e1de6-180">Assertion Attribute</span></span> | <span data-ttu-id="e1de6-181">보안 주체 특성</span><span class="sxs-lookup"><span data-stu-id="e1de6-181">Principal Attribute</span></span> |
    | --- | --- |
    | <span data-ttu-id="e1de6-182">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname</span><span class="sxs-lookup"><span data-stu-id="e1de6-182">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname</span></span> |<span data-ttu-id="e1de6-183">firstname</span><span class="sxs-lookup"><span data-stu-id="e1de6-183">firstname</span></span> |
    | <span data-ttu-id="e1de6-184">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname</span><span class="sxs-lookup"><span data-stu-id="e1de6-184">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname</span></span> |<span data-ttu-id="e1de6-185">Lastname</span><span class="sxs-lookup"><span data-stu-id="e1de6-185">lastname</span></span> |
    | <span data-ttu-id="e1de6-186">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress</span><span class="sxs-lookup"><span data-stu-id="e1de6-186">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress</span></span> |<span data-ttu-id="e1de6-187">email</span><span class="sxs-lookup"><span data-stu-id="e1de6-187">email</span></span> 
   
     >[!NOTE]
     ><span data-ttu-id="e1de6-188">hello 특성의 hello 구성 방법을 HCP hello 응용 프로그램이 개발 되는, 즉 hello SAML 응답에서에서 예상 되는 이름 (Principal Attribute)에 액세스할 hello 코드에서이 특성 및 특성에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="e1de6-188">hello configuration of hello Attributes depends on how hello application(s) on HCP are developed, i.e. which attribute(s) they expect in hello SAML response and under which name (Principal Attribute) they access this attribute in hello code.</span></span>
     > 
     >  

    1.  <span data-ttu-id="e1de6-189">hello **Default Attribute** hello 스크린샷은 단지 설명을 위해 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1de6-189">hello **Default Attribute** in hello screenshot is just for illustration purposes.</span></span> <span data-ttu-id="e1de6-190">없으면 toomake hello 시나리오 작업에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1de6-190">It is not required toomake hello scenario work.</span></span>   
    2.  <span data-ttu-id="e1de6-191">이름 및 값에 대 한 hello **Principal Attribute** hello에 표시 된 스크린 샷 hello 응용 프로그램을 개발 하는 방법에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="e1de6-191">hello names and values for **Principal Attribute** shown in hello screenshot depend on how hello application is developed.</span></span> <span data-ttu-id="e1de6-192">응용 프로그램에 다른 매핑이 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1de6-192">It is possible that your application requires different mappings.</span></span>
     
13. <span data-ttu-id="e1de6-193">Hello hello에 Azure 클래식 포털에서에서 **SAP HANA Cloud Platform에서 single sign on 구성** 대화 상자 페이지 hello single sign on 구성 확인을 선택한 다음 **완료**합니다.</span><span class="sxs-lookup"><span data-stu-id="e1de6-193">In hello Azure classic portal, on hello **Configure single sign-on at SAP HANA Cloud Platform** dialogue page, select hello single sign-on configuration confirmation, and then click **Complete**.</span></span>
    
    <span data-ttu-id="e1de6-194">![Single Sign-On 구성](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC796933.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="e1de6-194">![Configure Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC796933.png "Configure Single Sign-On")</span></span>

###<a name="assertion-based-groups"></a><span data-ttu-id="e1de6-195">어설션 기반 그룹</span><span class="sxs-lookup"><span data-stu-id="e1de6-195">Assertion-based groups</span></span>
<span data-ttu-id="e1de6-196">선택적 단계로, Azure Active Directory ID 공급자에 대한 어설션 기반 그룹을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1de6-196">As an optional step, you can configure assertion-based groups for your Azure Active Directory Identity Provider.</span></span>

<span data-ttu-id="e1de6-197">SAP HANA Cloud Platform의 그룹을 사용 하면 하나 toodynamically 할당 아니면 더 많은 사용자가 tooone 또는 SAP HANA Cloud Platform 응용 프로그램에서 더 많은 역할 결정 hello SAML 특성의 값으로 2.0 어설션 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1de6-197">Using groups on SAP HANA Cloud Platform allows you toodynamically assign one or more users tooone or more roles in your SAP HANA Cloud Platform applications, determined by values of attributes in hello SAML 2.0 assertion.</span></span> 

<span data-ttu-id="e1de6-198">예를 들어 hello 어설션이 있으면 hello 특성 "*계약 임시 =*", 모든 영향을 받는 사용자 toobe 추가 toohello 그룹 경우가"*임시*"입니다.</span><span class="sxs-lookup"><span data-stu-id="e1de6-198">For example, if hello assertion contains hello attribute "*contract=temporary*", you may want all affected users toobe added toohello group "*TEMPORARY*".</span></span> <span data-ttu-id="e1de6-199">hello 그룹 "*임시*" SAP HANA Cloud Platform 계정에 배포 된 하나 이상의 응용 프로그램에서 하나 이상의 역할을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1de6-199">hello group "*TEMPORARY*" may contain one or more roles from one or more applications deployed in your SAP HANA Cloud Platform account.</span></span>
 
<span data-ttu-id="e1de6-200">사용 하 여 어설션 기반 그룹 toosimultaneously 하려는 경우 여러 사용자가 tooone 또는 SAP HANA Cloud Platform 계정에서 응용 프로그램의 추가 역할을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1de6-200">Use assertion-based groups when you want toosimultaneously assign many users tooone or more roles of applications in your SAP HANA Cloud Platform account.</span></span> <span data-ttu-id="e1de6-201">Tooassign만 한 명 또는 소수의 사용자 toospecific 역할 수를 원하는 경우 hello에 직접 할당 하는 것이 좋습니다 "**권한 부여**" hello SAP HANA Cloud Platform cockpit의 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1de6-201">If you want tooassign only a single or small number of users toospecific roles, we recommend assigning them directly in hello “**Authorizations**” tab of hello SAP HANA Cloud Platform cockpit.</span></span>

## <a name="assign-a-role-tooa-user"></a><span data-ttu-id="e1de6-202">역할 tooa 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="e1de6-202">Assign a role tooa user</span></span>
<span data-ttu-id="e1de6-203">Tooenable Azure AD 사용자가 toolog SAP HANA Cloud Platform에 주문 하 고, SAP HANA Cloud Platform toothem hello에에서 대 한 역할을 할당 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1de6-203">In order tooenable Azure AD users toolog into SAP HANA Cloud Platform, you must assign roles in hello SAP HANA Cloud Platform toothem.</span></span>

<span data-ttu-id="e1de6-204">**역할 tooa 사용자 tooassign hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="e1de6-204">**tooassign a role tooa user, perform hello following steps:**</span></span>

1. <span data-ttu-id="e1de6-205">Tooyour 로그인 **SAP HANA Cloud Platform** 환경을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1de6-205">Log in tooyour **SAP HANA Cloud Platform** cockpit.</span></span>
2. <span data-ttu-id="e1de6-206">Hello 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1de6-206">Perform hello following:</span></span>
   
   <span data-ttu-id="e1de6-207">![권한 부여](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790805.png "권한 부여")</span><span class="sxs-lookup"><span data-stu-id="e1de6-207">![Authorizations](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790805.png "Authorizations")</span></span>
   
  1. <span data-ttu-id="e1de6-208">**권한 부여**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e1de6-208">Click **Authorization**.</span></span>
  2. <span data-ttu-id="e1de6-209">Hello 클릭 **사용자** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1de6-209">Click hello **Users** tab.</span></span>
  3. <span data-ttu-id="e1de6-210">Hello에 **사용자** 형식 hello 사용자의 전자 메일 주소 텍스트 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="e1de6-210">In hello **User** textbox, type hello user’s email address.</span></span>
  4. <span data-ttu-id="e1de6-211">클릭 **할당** tooassign hello 사용자 tooa 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="e1de6-211">Click **Assign** tooassign hello user tooa role.</span></span>
  5. <span data-ttu-id="e1de6-212">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e1de6-212">Click **Save**.</span></span>

## <a name="assign-users"></a><span data-ttu-id="e1de6-213">사용자 할당</span><span class="sxs-lookup"><span data-stu-id="e1de6-213">Assign users</span></span>
<span data-ttu-id="e1de6-214">tootest 구성에 tooallow 할당 하 여 응용 프로그램 액세스 tooit를 사용 하 여 원하는 toogrant hello Azure AD 사용자가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1de6-214">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="e1de6-215">**tooassign 사용자 tooSAP HANA Cloud Platform hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="e1de6-215">**tooassign users tooSAP HANA Cloud Platform, perform hello following steps:**</span></span>

1. <span data-ttu-id="e1de6-216">Azure 클래식 포털 hello 테스트 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e1de6-216">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="e1de6-217">Hello에 **SAP HANA Cloud Platform** 응용 프로그램 통합 페이지에서 클릭 **사용자 할당**합니다.</span><span class="sxs-lookup"><span data-stu-id="e1de6-217">On hello **SAP HANA Cloud Platform** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="e1de6-218">![사용자 할당](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790806.png "사용자 할당")</span><span class="sxs-lookup"><span data-stu-id="e1de6-218">![Assign Users](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790806.png "Assign Users")</span></span>
3. <span data-ttu-id="e1de6-219">테스트 사용자 선택, 클릭 **할당**, 클릭 하 고 **예** tooconfirm 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1de6-219">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
   <span data-ttu-id="e1de6-220">![예](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC767830.png "예")</span><span class="sxs-lookup"><span data-stu-id="e1de6-220">![Yes](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="e1de6-221">SSO 설정 tootest 원하는 hello 액세스 패널을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e1de6-221">If you want tootest your SSO settings, open hello Access Panel.</span></span> <span data-ttu-id="e1de6-222">액세스 패널 hello에 대 한 자세한 내용은 참조 하십시오. [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e1de6-222">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

