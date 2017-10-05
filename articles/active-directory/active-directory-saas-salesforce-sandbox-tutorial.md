---
title: "자습서: Salesforce Sandbox와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory에서 Salesforce Sandbox를 사용하여 Single Sign-On, 자동화된 프로비저닝 등을 사용하도록 설정하는 방법을 알아봅니다."
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
ms.openlocfilehash: 32835e79188806bb2ff319eea23b1b52ab585ab1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce-sandbox"></a><span data-ttu-id="d5c93-103">자습서: Salesforce Sandbox와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="d5c93-103">Tutorial: Azure Active Directory integration with Salesforce Sandbox</span></span>

<span data-ttu-id="d5c93-104">이 자습서는 Azure 및 Salesforce Sandbox의 통합을 보여 주기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d5c93-104">The objective of this tutorial is to show the integration of Azure and Salesforce Sandbox.</span></span>  

>[!TIP]
><span data-ttu-id="d5c93-105">피드백에 대 한 참조는 [Azure 지원 페이지](http://go.microsoft.com/fwlink/?LinkId=521878)합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c93-105">For feedback, see the [Azure support page](http://go.microsoft.com/fwlink/?LinkId=521878).</span></span> 
> 

<span data-ttu-id="d5c93-106">샌드박스는 Salesforce 프로덕션 조직에서 데이터 및 응용 프로그램을 손상시키지 않고 개발, 테스트 및 훈련과 같은 다양한 목적으로 별도의 환경에서 조직의 여러 복사본을 만들 수 있는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c93-106">Sandboxes give you the ability to create multiple copies of your organization in separate environments for a variety of purposes, such as development, testing, and training, without compromising the data and applications in your Salesforce production organization.</span></span>  

<span data-ttu-id="d5c93-107">자세한 내용은 [샌드박스 개요](https://help.salesforce.com/HTViewHelpDoc?id=create_test_instance.htm&language=en_US)</span><span class="sxs-lookup"><span data-stu-id="d5c93-107">For more details, see [Sandbox Overview](https://help.salesforce.com/HTViewHelpDoc?id=create_test_instance.htm&language=en_US)</span></span>

<span data-ttu-id="d5c93-108">이 자습서에 설명된 시나리오에서는 사용자에게 이미 다음 항목이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c93-108">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="d5c93-109">유효한 Azure 구독</span><span class="sxs-lookup"><span data-stu-id="d5c93-109">A valid Azure subscription</span></span>
* <span data-ttu-id="d5c93-110">Salesforce.com에서 샌드박스</span><span class="sxs-lookup"><span data-stu-id="d5c93-110">A sandbox in Salesforce.com</span></span>

<span data-ttu-id="d5c93-111">Salesforce.com에 유효한 샌드박스가 없는 경우 Salesforce에 문의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c93-111">If you don’t have a valid sandbox in Salesforce.com yet, you need to contact Salesforce.</span></span>

<span data-ttu-id="d5c93-112">이 자습서에 설명된 시나리오는 다음 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5c93-112">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="d5c93-113">Salesforce Sandbox에 응용 프로그램 통합 사용</span><span class="sxs-lookup"><span data-stu-id="d5c93-113">Enabling the application integration for Salesforce Sandbox</span></span>
2. <span data-ttu-id="d5c93-114">SSO(Single Sign-On) 구성</span><span class="sxs-lookup"><span data-stu-id="d5c93-114">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="d5c93-115">도메인 사용</span><span class="sxs-lookup"><span data-stu-id="d5c93-115">Enabling your domain</span></span>
4. <span data-ttu-id="d5c93-116">사용자 프로비전 구성</span><span class="sxs-lookup"><span data-stu-id="d5c93-116">Configuring user provisioning</span></span>
5. <span data-ttu-id="d5c93-117">사용자 할당</span><span class="sxs-lookup"><span data-stu-id="d5c93-117">Assigning users</span></span>

<span data-ttu-id="d5c93-118">![시나리오](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769571.png "시나리오")</span><span class="sxs-lookup"><span data-stu-id="d5c93-118">![Scenario](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769571.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-salesforce-sandbox"></a><span data-ttu-id="d5c93-119">Salesforce 샌드박스에 응용 프로그램 통합 사용</span><span class="sxs-lookup"><span data-stu-id="d5c93-119">Enable the application integration for Salesforce Sandbox</span></span>
<span data-ttu-id="d5c93-120">이 섹션에서는 Salesforce 샌드박스에 응용 프로그램 통합을 사용하도록 설정하는 방법을 간략하게 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c93-120">The objective of this section is to outline how to enable the application integration for Salesforce sandbox.</span></span>

<span data-ttu-id="d5c93-121">**Salesforce 샌드박스에 응용 프로그램 통합을 사용하도록 설정하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="d5c93-121">**To enable the application integration for Salesforce sandbox, perform the following steps:**</span></span>

1. <span data-ttu-id="d5c93-122">Azure 클래식 포털의 왼쪽 탐색 창에서 **Active Directory**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c93-122">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="d5c93-123">![Active Directory](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="d5c93-123">![Active Directory](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="d5c93-124">**디렉터리** 목록에서 디렉터리 통합을 사용하도록 설정할 디렉터리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c93-124">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="d5c93-125">응용 프로그램 보기를 열려면 디렉터리 보기의 최상위 메뉴에서 **응용 프로그램** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c93-125">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="d5c93-126">![응용 프로그램](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700994.png "응용 프로그램")</span><span class="sxs-lookup"><span data-stu-id="d5c93-126">![Applications](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="d5c93-127">**응용 프로그램 갤러리**를 열려면 **앱 추가**를 클릭한 다음 **조직에서 사용할 응용 프로그램 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c93-127">To open the **Application Gallery**, click **Add An App**, and then click **Add an application for my organization to use**.</span></span>
   
   <span data-ttu-id="d5c93-128">![원하는 작업을 선택하세요.] (./media/active-directory-saas-salesforce-sandbox-tutorial/IC700995.png "원하는 작업을 선택하세요.")</span><span class="sxs-lookup"><span data-stu-id="d5c93-128">![What do you want to do?](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700995.png "What do you want to do?")</span></span>
5. <span data-ttu-id="d5c93-129">**검색 상자**에 **Salesforce Sandbox**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c93-129">In the **search box**, type **Salesforce Sandbox**.</span></span>
   
   <span data-ttu-id="d5c93-130">![응용 프로그램 갤러리](./media/active-directory-saas-salesforce-sandbox-tutorial/IC710978.png "응용 프로그램 갤러리")</span><span class="sxs-lookup"><span data-stu-id="d5c93-130">![Application Gallery](./media/active-directory-saas-salesforce-sandbox-tutorial/IC710978.png "Application Gallery")</span></span>
6. <span data-ttu-id="d5c93-131">결과 창에서 **Salesforce Sandbox**를 선택하고 **완료**를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c93-131">In the results pane, select **Salesforce Sandbox**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="d5c93-132">![Salesforce 샌드박스](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746474.png "Salesforce 샌드박스")</span><span class="sxs-lookup"><span data-stu-id="d5c93-132">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746474.png "Salesforce Sandbox")</span></span>
   
## <a name="configur-single-sign-on-sso"></a><span data-ttu-id="d5c93-133">SSO(Single Sign-On) 구성</span><span class="sxs-lookup"><span data-stu-id="d5c93-133">Configur single sign-on (SSO)</span></span>

<span data-ttu-id="d5c93-134">이 섹션은 사용자가 SAML 프로토콜 기반 페더레이션을 사용하여 Azure AD의 계정으로 Salesforce에 인증할 수 있게 하는 방법을 간략하게 설명하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d5c93-134">The objective of this section is to outline how to enable users to authenticate to Salesforce with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="d5c93-135">**Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="d5c93-135">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="d5c93-136">Azure 클래식 포털의 **Salesforce Sandbox** 응용 프로그램 통합 페이지에서 **Single Sign-On 구성**을 클릭하여 **Single Sign-On 구성** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d5c93-136">In the Azure classic portal, on the **Salesforce Sandbox** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="d5c93-137">![Single Sign-On 구성](./media/active-directory-saas-salesforce-sandbox-tutorial/IC749323.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="d5c93-137">![Configure single sign-on](./media/active-directory-saas-salesforce-sandbox-tutorial/IC749323.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="d5c93-138">**Salesforce Sandbox에 대한 사용자 로그온 방법을 선택하세요.** 페이지에서 **Microsoft Azure AD Single Sign-On**을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c93-138">On the **How would you like users to sign on to Salesforce Sandbox** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="d5c93-139">![Salesforce 샌드박스](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746479.png "Salesforce 샌드박스")</span><span class="sxs-lookup"><span data-stu-id="d5c93-139">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746479.png "Salesforce Sandbox")</span></span>
3. <span data-ttu-id="d5c93-140">**앱 URL 구성** 페이지의 **로그온 URL** 텍스트 상자에 `http://company.my.salesforce.com` 패턴을 사용하여 URL을 입력하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c93-140">On the **Configure App URL** page, in the **Sign On URL** textbox, type your URL using the following pattern `http://company.my.salesforce.com`, and then click **Next**.</span></span>
   
   <span data-ttu-id="d5c93-141">![앱 URL 구성](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781022.png "앱 URL 구성")</span><span class="sxs-lookup"><span data-stu-id="d5c93-141">![Configure App URL](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781022.png "Configure App URL")</span></span>
4. <span data-ttu-id="d5c93-142">디렉터리의 다른 Salesforce Sandbox 인스턴스에 대한 Single Sign-On을 이미 구성한 경우 **로그온 URL**과 같은 값으로 **식별자**도 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c93-142">If you have already configured single sign-on for another Salesforce Sandbox instance in your directory, then you must also configure the **Identifier** to have the same value as the **Sign on URL**.</span></span> 
 * <span data-ttu-id="d5c93-143">대화 상자의 **앱 URL 구성** 페이지에서 **고급 설정 표시** 확인란을 선택하여 **식별자** 필드를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5c93-143">The **Identifier** field can be found by checking the **Show advanced settings** checkbox on the **Configure App URL** page of the dialog.</span></span>
5. <span data-ttu-id="d5c93-144">**Salesforce Sandbox에서 Single Sign-On 구성** 페이지에서 **인증서 다운로드**를 클릭한 다음 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c93-144">On the **Configure single sign-on at Salesforce Sandbox** page, click **Download certificate**, and then save the certificate file on your computer.</span></span>
   
   <span data-ttu-id="d5c93-145">![Single Sign-On 구성](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781023.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="d5c93-145">![Configure Single Sign-On](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781023.png "Configure Single Sign-On")</span></span>
6. <span data-ttu-id="d5c93-146">다른 웹 브라우저 창에서 Salesforce 샌드박스에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c93-146">In a different web browser window, log into your Salesforce sandbox as an administrator.</span></span>
7. <span data-ttu-id="d5c93-147">위쪽의 메뉴에서 **설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c93-147">In the menu on the top, click **Setup**.</span></span>
   
   <span data-ttu-id="d5c93-148">![설치](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781024.png "설치")</span><span class="sxs-lookup"><span data-stu-id="d5c93-148">![Setup](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781024.png "Setup")</span></span>
8. <span data-ttu-id="d5c93-149">왼쪽의 탐색 창에서 **보안 제어**를 클릭한 다음 **Single Sign-On 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c93-149">In the navigation pane on the left, click **Security Controls**, and then click **Single Sign-On Settings**.</span></span>
   
   <span data-ttu-id="d5c93-150">![Single Sign-On 설정](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781025.png "Single Sign-On 설정")</span><span class="sxs-lookup"><span data-stu-id="d5c93-150">![Single Sign-On Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781025.png "Single Sign-On Settings")</span></span>
9. <span data-ttu-id="d5c93-151">Single Sign-On 설정 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c93-151">On the Single Sign-On Settings section, perform the following steps:</span></span>
   
   <span data-ttu-id="d5c93-152">![Single Sign-On 설정](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781026.png "Single Sign-On 설정")</span><span class="sxs-lookup"><span data-stu-id="d5c93-152">![Single Sign-On Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781026.png "Single Sign-On Settings")</span></span>  
 1.  <span data-ttu-id="d5c93-153">**SAML 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c93-153">Select **SAML Enabled**.</span></span> 
 2.  <span data-ttu-id="d5c93-154">**새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c93-154">Click **New**.</span></span>
10. <span data-ttu-id="d5c93-155">SAML Single Sign-On 설정 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c93-155">On the SAML Single Sign-On Settings section, perform the following steps:</span></span>
    
    <span data-ttu-id="d5c93-156">![SAML Single Sign-On 설정](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781027.png "SAML Single Sign-On 설정")</span><span class="sxs-lookup"><span data-stu-id="d5c93-156">![SAML Single Sign-On Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781027.png "SAML Single Sign-On Settings")</span></span>  
 1. <span data-ttu-id="d5c93-157">이름 텍스트 상자에 구성의 이름을 입력합니다(예: *SPSSOWAAD\_Test*).</span><span class="sxs-lookup"><span data-stu-id="d5c93-157">In the Name textbox, type the name of the configuration (e.g.: *SPSSOWAAD\_Test*).</span></span> 
 2. <span data-ttu-id="d5c93-158">Azure 클래식 포털의 **Salesforce Sandbox에서 Single Sign-On 구성** 대화 상자 페이지에서 **발급자 URL** 값을 복사하여 **발급자** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="d5c93-158">In the Azure classic portal, on the **Configure single sign-on at Salesforce Sandbox** dialogue page, copy the **Issuer URL** value, and then paste it into the **Issuer** textbox.</span></span>
 3. <span data-ttu-id="d5c93-159">디렉터리에 처음으로 추가하는 Salesforce Sandbox 인스턴스인 경우 **엔터티 ID** 텍스트 상자에 **https://test.salesforce.com**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c93-159">In the **Entity Id** textbox, type **https://test.salesforce.com** if this is the first Salesforce Sandbox instance that you are adding to your directory.</span></span> <span data-ttu-id="d5c93-160">Salesforce Sandbox의 인스턴스를 이미 추가한 경우에는 **엔터티 ID**에 **로그온 URL**을 입력합니다. 형식은 다음과 같아야 합니다. `http://company.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="d5c93-160">If you have already added an instance of Salesforce Sandbox, then for the **Entity ID** type in the **Sign On URL**, which should be in this format: `http://company.my.salesforce.com`</span></span>   
 4. <span data-ttu-id="d5c93-161">다운로드한 인증서를 업로드하려면 **찾아보기** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c93-161">Click **Browse** to upload the downloaded certificate.</span></span>  
 5. <span data-ttu-id="d5c93-162">**SAML ID 유형**으로 **사용자 개체에서 페더레이션 ID를 포함하는 어설션**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c93-162">As **SAML Identity Type**, select **Assertion contains the Federation ID from the User object**.</span></span> 
 6. <span data-ttu-id="d5c93-163">**SAML ID 위치**로 **Subject 문의 NameIdentifier 요소에 ID 포함**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c93-163">As **SAML Identity Location**, select **Identity is in the NameIdentifier element of the Subject statement**.</span></span>
 7. <span data-ttu-id="d5c93-164">Azure 클래식 포털의 **Salesforce Sandbox에서 Single Sign-On 구성** 대화 상자 페이지에서 **원격 로그인 URL** 값을 복사한 다음 **ID 공급자 로그인 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="d5c93-164">In the Azure classic portal, on the **Configure single sign-on at Salesforce Sandbox** dialogue page, copy the **Remote Login URL** value, and then paste it into the **Identity Provider Login URL** textbox.</span></span> 
 8. <span data-ttu-id="d5c93-165">SFDC는 SAML 로그아웃을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d5c93-165">SFDC does not support SAML logout.</span></span>  <span data-ttu-id="d5c93-166">해결 방법으로 **ID 공급자 로그아웃 URL** 텍스트 상자에 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0'을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="d5c93-166">As a workaround, paste 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0' it into the **Identity Provider Logout URL** textbox.</span></span>
 9. <span data-ttu-id="d5c93-167">**서비스 공급자가 시작한 요청 바인딩**에서 **HTTP Post**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c93-167">As **Service Provider Initiated Request Binding**, select **HTTP POST**.</span></span> 
 10. <span data-ttu-id="d5c93-168">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c93-168">Click **Save**.</span></span>
11. <span data-ttu-id="d5c93-169">Azure 클래식 포털에서 Single Sign-On 구성 확인을 선택하고 **완료**를 클릭하여 **Single Sign-On 구성** 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="d5c93-169">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="d5c93-170">![Single Sign-On 구성](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781028.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="d5c93-170">![Configure Single Sign-On](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781028.png "Configure Single Sign-On")</span></span>

## <a name="enable-your-domain"></a><span data-ttu-id="d5c93-171">도메인 활성화</span><span class="sxs-lookup"><span data-stu-id="d5c93-171">Enable your domain</span></span>
<span data-ttu-id="d5c93-172">이 섹션에서는 이미 도메인을 만들었다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c93-172">This section assumes that you already have created a domain.</span></span>  <span data-ttu-id="d5c93-173">자세한 내용은 [도메인 이름 정의](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d5c93-173">For more details, see [Defining Your Domain Name](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).</span></span>

<span data-ttu-id="d5c93-174">**도메인을 사용하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="d5c93-174">**To enable your domain, perform the following steps:**</span></span>

1. <span data-ttu-id="d5c93-175">왼쪽 탐색 창에서 **도메인 관리**를 클릭한 다음 **내 도메인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c93-175">In the left navigation pane, click **Domain Management**, and then click **My Domain.**</span></span>
   
   <span data-ttu-id="d5c93-176">![내 도메인](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781029.png "내 도메인")</span><span class="sxs-lookup"><span data-stu-id="d5c93-176">![My Domain](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781029.png "My Domain")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="d5c93-177">도메인이 올바르게 구성되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c93-177">Please make sure that your domain has been configured correctly.</span></span> 
   > 
2. <span data-ttu-id="d5c93-178">**로그인 페이지 설정** 섹션에서 **편집**을 클릭한 다음 **인증 서비스**로 이전 섹션에서 SAML Single Sign-On 설정의 이름을 선택하고 마지막으로 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c93-178">In the **Login Page Settings** section, click **Edit**, then, as **Authentication Service**, select the name of the SAML Single Sign-On Setting from the previous section, and finally click **Save**.</span></span>
   
   <span data-ttu-id="d5c93-179">![내 도메인](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781030.png "내 도메인")</span><span class="sxs-lookup"><span data-stu-id="d5c93-179">![My Domain](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781030.png "My Domain")</span></span>

<span data-ttu-id="d5c93-180">도메인이 구성되면 바로 사용자가 Salesforce 샌드박스에 로그인하는 도메인 URL을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c93-180">As soon as you have a domain configured, your users should use the domain URL to login to the Salesforce sandbox.</span></span>  

<span data-ttu-id="d5c93-181">URL의 값을 가져오려면 이전 섹션에서 만든 SSO 프로필을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c93-181">To get the value of the URL, click the SSO profile you have created in the previous section.</span></span>

## <a name="configure-user-provisioning"></a><span data-ttu-id="d5c93-182">사용자 프로비전 구성</span><span class="sxs-lookup"><span data-stu-id="d5c93-182">Configure user provisioning</span></span>
<span data-ttu-id="d5c93-183">이 섹션은 Salesforce Sandbox에 Active Directory 사용자 계정을 사용자 프로비저닝할 수 있도록 설정하는 방법을 간략하게 설명하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d5c93-183">The objective of this section is to outline how to enable user provisioning of Active Directory user accounts to Salesforce Sandbox.</span></span>

<span data-ttu-id="d5c93-184">**사용자 프로비전을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="d5c93-184">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="d5c93-185">Salesforce 포털의 위쪽 탐색 모음에서 사용자 메뉴를 확장하려면 사용자 이름을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c93-185">In the Salesforce portal, in the top navigation bar, select your name to expand your user menu:</span></span>
   
   <span data-ttu-id="d5c93-186">![내 설정](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698773.png "내 설정")</span><span class="sxs-lookup"><span data-stu-id="d5c93-186">![My Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698773.png "My Settings")</span></span>
2. <span data-ttu-id="d5c93-187">사용자 메뉴에서 **내 설정**을 선택하여 **내 설정** 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d5c93-187">From your user menu, select **My Settings** to open your **My Settings** page.</span></span>
3. <span data-ttu-id="d5c93-188">왼쪽 창에서 **개인**을 클릭하여 개인 섹션을 확장한 다음 **내 보안 토큰 재설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c93-188">In the left pane, click **Personal** to expand the Personal section, and then click **Reset My Security Token**:</span></span>
   
   <span data-ttu-id="d5c93-189">![내 설정](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698774.png "내 설정")</span><span class="sxs-lookup"><span data-stu-id="d5c93-189">![My Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698774.png "My Settings")</span></span>
4. <span data-ttu-id="d5c93-190">**내 보안 토큰 재설정** 페이지에서 **보안 토큰 재설정**을 클릭하여 Salesforce.com 보안 토큰이 포함된 메일을 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c93-190">On the **Reset My Security Token** page, click **Reset Security Token** to request an email that contains your Salesforce.com security token.</span></span>
   
   <span data-ttu-id="d5c93-191">![새 토큰](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698776.png "새 토큰")</span><span class="sxs-lookup"><span data-stu-id="d5c93-191">![New Token](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698776.png "New Token")</span></span>
5. <span data-ttu-id="d5c93-192">"**Salesforce.com.com 보안 확인**"을 제목으로 Salesforce.com에서 온 이메일의 받은 편지함을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c93-192">Check your email inbox for an email from Salesforce.com with “**salesforce.com.com security confirmation**” as subject.</span></span>
6. <span data-ttu-id="d5c93-193">이 이메일을 검토하고 보안 토큰 값을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c93-193">Review this email and copy the security token value.</span></span>
7. <span data-ttu-id="d5c93-194">Azure 클래식 포털의 **salesforce Sandbox** 응용 프로그램 통합 페이지에서 **사용자 프로비저닝 구성**을 클릭하여 **사용자 프로비저닝 구성** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d5c93-194">In the Azure classic portal, on the **salesforce Sandbox** application integration page, click **Configure user provisioning** to open the **Configure User Provisioning** dialog.</span></span>
   
   <span data-ttu-id="d5c93-195">![사용자 프로비전 구성](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769573.png "사용자 프로비전 구성")</span><span class="sxs-lookup"><span data-stu-id="d5c93-195">![Configure user provisioning](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769573.png "Configure user provisioning")</span></span>
8. <span data-ttu-id="d5c93-196">**Salesforce Sandbox 자격 증명을 입력하여 자동 사용자 프로비저닝 사용** 페이지에서 다음 구성 설정을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c93-196">On the **Enter your Salesforce Sandbox credentials to enable automatic user provisioning** page, provide the following configuration settings:</span></span>
   
   <span data-ttu-id="d5c93-197">![Salesforce 샌드박스](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746476.png "Salesforce 샌드박스")</span><span class="sxs-lookup"><span data-stu-id="d5c93-197">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746476.png "Salesforce Sandbox")</span></span>   
 1. <span data-ttu-id="d5c93-198">**Salesforce Sandbox 관리자 이름** 텍스트 상자에 Salesforce.com의 **시스템 관리자** 프로필이 할당된 Salesforce Sandbox 계정 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c93-198">In the **Salesforce Sandbox Admin User Name** textbox, type a Salesforce sandbox account name that has the **System Administrator** profile in Salesforce.com assigned.</span></span>
 2. <span data-ttu-id="d5c93-199">**Salesforce Sandbox 관리자 암호** 텍스트 상자에 이 계정의 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c93-199">In the **Salesforce Sandbox Admin Password** textbox, type the password for this account.</span></span>
 3. <span data-ttu-id="d5c93-200">**사용자 보안 토큰** 텍스트 상자에 보안 토큰 값을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="d5c93-200">In the **User Security Token** textbox, paste the security token value.</span></span>
 4. <span data-ttu-id="d5c93-201">**유효성 검사** 를 클릭하여 구성을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c93-201">Click **Validate** to verify your configuration.</span></span>
 5. <span data-ttu-id="d5c93-202">**다음** 단추를 클릭하여 **확인** 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d5c93-202">Click the **Next** button to open the **Confirmation** page.</span></span>
9. <span data-ttu-id="d5c93-203">**확인** 페이지에서 **완료**를 클릭하여 구성을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c93-203">On the **Confirmation** page, click **Complete** to save your configuration.</span></span>
   
## <a name="assigning-users"></a><span data-ttu-id="d5c93-204">사용자 할당</span><span class="sxs-lookup"><span data-stu-id="d5c93-204">Assigning users</span></span>

<span data-ttu-id="d5c93-205">구성을 테스트하려면 응용 프로그램 사용을 허용하려는 Azure AD 사용자를 할당하여 액세스 권한을 부여해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c93-205">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="d5c93-206">**Salesforce 샌드박스에 사용자를 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="d5c93-206">**To assign users to Salesforce Sandbox, perform the following steps:**</span></span>

1. <span data-ttu-id="d5c93-207">Azure 클래식 포털에서 테스트 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d5c93-207">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="d5c93-208">**Salesforce Sandbox** 응용 프로그램 통합 페이지에서 **사용자 할당**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c93-208">On the **Salesforce Sandbox **application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="d5c93-209">![사용자 할당](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769574.png "사용자 할당")</span><span class="sxs-lookup"><span data-stu-id="d5c93-209">![Assign users](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769574.png "Assign users")</span></span>
3. <span data-ttu-id="d5c93-210">테스트 사용자를 선택하고 **할당**을 클릭한 다음 **예**를 클릭하여 할당을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c93-210">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="d5c93-211">![예](./media/active-directory-saas-salesforce-sandbox-tutorial/IC767830.png "예")</span><span class="sxs-lookup"><span data-stu-id="d5c93-211">![Yes](./media/active-directory-saas-salesforce-sandbox-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="d5c93-212">이제 10분 동안 기다린 후 계정이 Salesforce Sandbox에 동기화되었는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c93-212">You should now wait for 10 minutes and verify that the account has been synchronized to Salesforce Sandbox.</span></span>

<span data-ttu-id="d5c93-213">SSO 설정을 테스트하려면 액세스 패널을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d5c93-213">If you want to test your SSO settings, open the Access Panel.</span></span> <span data-ttu-id="d5c93-214">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](https://msdn.microsoft.com/library/dn308586)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d5c93-214">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

