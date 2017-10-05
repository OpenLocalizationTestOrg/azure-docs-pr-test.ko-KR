---
title: "자습서: Cisco Webex와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory에서 Cisco Webex를 사용하여 Single Sign-On, 자동화된 프로비전 등을 사용하도록 설정하는 방법을 알아봅니다."
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
ms.openlocfilehash: b44b1a5b3e988a51db3325ec8a181651fa84e768
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cisco-webex"></a><span data-ttu-id="807c4-103">자습서: Cisco Webex와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="807c4-103">Tutorial: Azure Active Directory Integration with Cisco Webex</span></span>
<span data-ttu-id="807c4-104">이 자습서는 Azure 및 Cisco Webex의 통합을 보여 주기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="807c4-104">The objective of this tutorial is to show the integration of Azure and Cisco Webex.</span></span>  
<span data-ttu-id="807c4-105">이 자습서에 설명된 시나리오에서는 사용자에게 이미 다음 항목이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="807c4-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="807c4-106">유효한 Azure 구독</span><span class="sxs-lookup"><span data-stu-id="807c4-106">A valid Azure subscription</span></span>
* <span data-ttu-id="807c4-107">Cisco Webex 테넌트</span><span class="sxs-lookup"><span data-stu-id="807c4-107">A Cisco Webex tenant</span></span>

<span data-ttu-id="807c4-108">이 자습서를 완료한 후 Cisco Webex에 할당한 Azure AD 사용자가 Cisco Webex 회사 사이트(서비스 공급자가 시작한 로그온)에서 또는 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 사용하여 응용 프로그램에 Single Sign-On 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="807c4-108">After completing this tutorial, the Azure AD users you have assigned to Cisco Webex will be able to single sign into the application at your Cisco Webex company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="807c4-109">이 자습서에 설명된 시나리오는 다음 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="807c4-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

* <span data-ttu-id="807c4-110">Cisco Webex에 응용 프로그램 통합 사용</span><span class="sxs-lookup"><span data-stu-id="807c4-110">Enabling the application integration for Cisco Webex</span></span>
* <span data-ttu-id="807c4-111">SSO(Single Sign-On) 구성</span><span class="sxs-lookup"><span data-stu-id="807c4-111">Configuring single sign-on (SSO)</span></span>
* <span data-ttu-id="807c4-112">사용자 프로비전 구성</span><span class="sxs-lookup"><span data-stu-id="807c4-112">Configuring user provisioning</span></span>
* <span data-ttu-id="807c4-113">사용자 할당</span><span class="sxs-lookup"><span data-stu-id="807c4-113">Assigning users</span></span>

<span data-ttu-id="807c4-114">![시나리오](./media/active-directory-saas-cisco-webex-tutorial/IC777614.png "시나리오")</span><span class="sxs-lookup"><span data-stu-id="807c4-114">![Scenario](./media/active-directory-saas-cisco-webex-tutorial/IC777614.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-cisco-webex"></a><span data-ttu-id="807c4-115">Cisco Webex에 응용 프로그램 통합 사용</span><span class="sxs-lookup"><span data-stu-id="807c4-115">Enable the application integration for Cisco Webex</span></span>
<span data-ttu-id="807c4-116">이 섹션은 Cisco Webex에 응용 프로그램 통합을 사용하도록 설정하는 방법을 간략하게 설명하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="807c4-116">The objective of this section is to outline how to enable the application integration for Cisco Webex.</span></span>

<span data-ttu-id="807c4-117">**Cisco Webex에 응용 프로그램 통합을 사용하도록 설정하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="807c4-117">**To enable the application integration for Cisco Webex, perform the following steps:**</span></span>

1. <span data-ttu-id="807c4-118">Azure 클래식 포털의 왼쪽 탐색 창에서 **Active Directory**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="807c4-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="807c4-119">![Active Directory](./media/active-directory-saas-cisco-webex-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="807c4-119">![Active Directory](./media/active-directory-saas-cisco-webex-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="807c4-120">**디렉터리** 목록에서 디렉터리 통합을 사용하도록 설정할 디렉터리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="807c4-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="807c4-121">응용 프로그램 보기를 열려면 디렉터리 보기의 최상위 메뉴에서 **응용 프로그램** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="807c4-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="807c4-122">![응용 프로그램](./media/active-directory-saas-cisco-webex-tutorial/IC700994.png "응용 프로그램")</span><span class="sxs-lookup"><span data-stu-id="807c4-122">![Applications](./media/active-directory-saas-cisco-webex-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="807c4-123">페이지 맨 아래에 있는 **추가** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="807c4-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="807c4-124">![응용 프로그램 추가](./media/active-directory-saas-cisco-webex-tutorial/IC749321.png "응용 프로그램 추가")</span><span class="sxs-lookup"><span data-stu-id="807c4-124">![Add application](./media/active-directory-saas-cisco-webex-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="807c4-125">**수행할 작업** 대화 상자에서 **갤러리에서 응용 프로그램 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="807c4-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="807c4-126">![갤러리에서 응용 프로그램 추가](./media/active-directory-saas-cisco-webex-tutorial/IC749322.png "갤러리에서 응용 프로그램 추가")</span><span class="sxs-lookup"><span data-stu-id="807c4-126">![Add an application from gallerry](./media/active-directory-saas-cisco-webex-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="807c4-127">**검색 상자**에 **Cisco Webex**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="807c4-127">In the **search box**, type **Cisco Webex**.</span></span>
   
   <span data-ttu-id="807c4-128">![응용 프로그램 갤러리](./media/active-directory-saas-cisco-webex-tutorial/IC777615.png "응용 프로그램 갤러리")</span><span class="sxs-lookup"><span data-stu-id="807c4-128">![Application Gallery](./media/active-directory-saas-cisco-webex-tutorial/IC777615.png "Application Gallery")</span></span>
7. <span data-ttu-id="807c4-129">결과 창에서 **Cisco Webex**를 선택하고 **완료**를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="807c4-129">In the results pane, select **Cisco Webex**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="807c4-130">![Cisco Webex](./media/active-directory-saas-cisco-webex-tutorial/IC777616.png "Cisco Webex")</span><span class="sxs-lookup"><span data-stu-id="807c4-130">![Cisco Webex](./media/active-directory-saas-cisco-webex-tutorial/IC777616.png "Cisco Webex")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="807c4-131">Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="807c4-131">Configure single sign-on</span></span>

<span data-ttu-id="807c4-132">이 섹션은 사용자가 SAML 프로토콜 기반 페더레이션을 사용하여 Azure AD의 계정으로 Cisco Webex에 인증할 수 있게 하는 방법을 간략하게 설명하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="807c4-132">The objective of this section is to outline how to enable users to authenticate to Cisco Webex with their account in Azure AD using federation based on the SAML protocol.</span></span>  

<span data-ttu-id="807c4-133">이 절차의 일부로 base-64로 인코딩된 인증서 파일을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="807c4-133">As part of this procedure, you are required to create a base-64 encoded certificate.</span></span> <span data-ttu-id="807c4-134">이 절차를 잘 모르는 경우 [이진 인증서를 텍스트 파일로 변환하는 방법](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="807c4-134">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>

<span data-ttu-id="807c4-135">**Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="807c4-135">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="807c4-136">Azure 클래식 포털의 **Cisco Webex** 응용 프로그램 통합 페이지에서 **Single Sign-On 구성**을 클릭하여 **Single Sign-On 구성** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="807c4-136">In the Azure classic portal, on the **Cisco Webex** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="807c4-137">![Single Sign-On 구성](./media/active-directory-saas-cisco-webex-tutorial/IC777617.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="807c4-137">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777617.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="807c4-138">**Cisco Webex에 대한 사용자 로그온 방법을 선택하세요.** 페이지에서 **Microsoft Azure AD Single Sign-on**을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="807c4-138">On the **How would you like users to sign on to Cisco Webex** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="807c4-139">![Single Sign-On 구성](./media/active-directory-saas-cisco-webex-tutorial/IC777618.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="807c4-139">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777618.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="807c4-140">**앱 URL 구성** 페이지에서 다음 단계를 수행하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="807c4-140">On the **Configure App URL** page, perform the following steps, and then click **Next**.</span></span>
   
   <span data-ttu-id="807c4-141">![앱 URL 구성](./media/active-directory-saas-cisco-webex-tutorial/IC777619.png "앱 URL 구성")</span><span class="sxs-lookup"><span data-stu-id="807c4-141">![Configure app URL](./media/active-directory-saas-cisco-webex-tutorial/IC777619.png "Configure app URL")</span></span>   
   1. <span data-ttu-id="807c4-142">**URL에 로그온** 텍스트 상자에 Cisco Webex 테넌트 URL을 입력합니다(예: *http://contoso.webex.com*).</span><span class="sxs-lookup"><span data-stu-id="807c4-142">In the **Sing On URL** textbox, type your Cisco Webex tenant URL (e.g.: *http://contoso.webex.com*).</span></span>
   2. <span data-ttu-id="807c4-143">**Cisco Webex 회신 URL** 텍스트 상자에 **Cisco Webex AssertionConsumerService URL**(예: *https://company.webex.com/dispatcher/SAML2AuthService?siteurl=company*)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="807c4-143">In the **Cisco Webex Reply URL** textbox, type your **Cisco Webex AssertionConsumerService URL** (e.g.: *https://company.webex.com/dispatcher/SAML2AuthService?siteurl=company*).</span></span>
4. <span data-ttu-id="807c4-144">**Cisco Webex에서 Single Sign-On 구성** 페이지에서 인증서를 다운로드하려면 **인증서 다운로드**를 클릭한 다음 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="807c4-144">On the **Configure single sign-on at Cisco Webex** page, to download your certificate, click **Download certificate**, and then save the certificate file on your computer.</span></span>
   
   <span data-ttu-id="807c4-145">![Single Sign-On 구성](./media/active-directory-saas-cisco-webex-tutorial/IC777620.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="807c4-145">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777620.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="807c4-146">다른 웹 브라우저 창에서 Cisco Webex 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="807c4-146">In a different web browser window, log into your Cisco Webex company site as an administrator.</span></span>
6. <span data-ttu-id="807c4-147">위쪽의 메뉴에서 **사이트 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="807c4-147">In the menu on the top, click **Site Administration**.</span></span>
   
   <span data-ttu-id="807c4-148">![사이트 관리](./media/active-directory-saas-cisco-webex-tutorial/IC777621.png "사이트 관리")</span><span class="sxs-lookup"><span data-stu-id="807c4-148">![Site Administration](./media/active-directory-saas-cisco-webex-tutorial/IC777621.png "Site Administration")</span></span>
7. <span data-ttu-id="807c4-149">**사이트 관리** 섹션에서 **SSO 구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="807c4-149">In the **Manage Site** section, click **SSO Configuration**.</span></span>
   
   <span data-ttu-id="807c4-150">![SSO 구성](./media/active-directory-saas-cisco-webex-tutorial/IC777622.png "SSO 구성")</span><span class="sxs-lookup"><span data-stu-id="807c4-150">![SSO Configuration](./media/active-directory-saas-cisco-webex-tutorial/IC777622.png "SSO Configuration")</span></span>
8. <span data-ttu-id="807c4-151">페더레이션된 웹 SSO 구성 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="807c4-151">In the Federated Web SSO Configuration section, perform the following steps:</span></span>
   
   <span data-ttu-id="807c4-152">![페더레이션 SSO 구성](./media/active-directory-saas-cisco-webex-tutorial/IC777623.png "페더레이션 SSO 구성")</span><span class="sxs-lookup"><span data-stu-id="807c4-152">![Federated SSO Configuration](./media/active-directory-saas-cisco-webex-tutorial/IC777623.png "Federated SSO Configuration")</span></span>  
   1. <span data-ttu-id="807c4-153">**페더레이션 프로토콜** 목록에서 **SAML 2.0**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="807c4-153">From the **Federation Protocol** list, select **SAML 2.0**.</span></span>
   2. <span data-ttu-id="807c4-154">다운로드한 인증서에서 **Base-64로 인코딩된** 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="807c4-154">Create a **Base-64 encoded** file from your downloaded certificate.</span></span>  
    >[!TIP]
    ><span data-ttu-id="807c4-155">자세한 내용은 [이진 인증서를 텍스트 파일로 변환하는 방법](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="807c4-155">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>
    >  
   3. <span data-ttu-id="807c4-156">메모장에서 Base-64로 인코딩된 인증서를 열고 콘텐츠를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="807c4-156">Open your base-64 encoded certificate in notepad, and then copy the content of it.</span></span>
   4. <span data-ttu-id="807c4-157">**SAML 메타데이터 가져오기**를 클릭하고 Base-64로 인코딩된 인증서를 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="807c4-157">Click **Import SAML Metadata**, and then paste your base-64 encoded certificate.</span></span>
   5. <span data-ttu-id="807c4-158">Azure 클래식 포털의 **Cisco Webex에 대한 Single Sign-On 구성** 대화 상자 페이지에서 **발급자 URL** 값을 복사한 다음 **SAML(IdP ID)의 발급자** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="807c4-158">In the Azure classic portal, on the **Configure single sign-on at Cisco Webex** dialog page, copy the **Issuer URL** value, and then paste it into the **Issuer for SAML (IdP ID)** textbox.</span></span>
   6. <span data-ttu-id="807c4-159">Azure 클래식 포털의 **Cisco Webex에 대한 Single Sign-On 구성** 대화 상자 페이지에서 **원격 로그인 URL** 값을 복사한 다음 **고객 SSO 서비스 로그인 URL 발급자** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="807c4-159">In the Azure classic portal, on the **Configure single sign-on at Cisco Webex** dialog page, copy the **Remote Login URL** value, and then paste it into the **Customer SSO Service Login URL** textbox.</span></span>
   7. <span data-ttu-id="807c4-160">**NameID 형식** 목록에서 **전자 메일 주소**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="807c4-160">From the **NameID Format** list, select **Email address**.</span></span>
   8. <span data-ttu-id="807c4-161">**AuthnContextClassRef** 텍스트 상자에 **urn:oasis:names:tc:SAML:2.0:ac:classes:Password**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="807c4-161">In the **AuthnContextClassRef** textbox, type **urn:oasis:names:tc:SAML:2.0:ac:classes:Password**.</span></span>
   9. <span data-ttu-id="807c4-162">Azure 클래식 포털의 **Cisco Webex에 대한 Single Sign-On 구성** 대화 상자 페이지에서 **원격 로그아웃 URL** 값을 복사한 다음 **고객 SSO 서비스 로그아웃 URL 발급자** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="807c4-162">In the Azure classic portal, on the **Configure single sign-on at Cisco Webex** dialog page, copy the **Remote Logout URL** value, and then paste it into the **Customer SSO Service Logout URL** textbox.</span></span>
   10. <span data-ttu-id="807c4-163">**업데이트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="807c4-163">Click **Update**.</span></span>
9. <span data-ttu-id="807c4-164">Azure 클래식 포털의 **Cisco Webex에서 Single Sign-On 구성** 대화 상자 페이지에서 Single Sign-On 구성 확인을 선택한 다음 **완료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="807c4-164">In the Azure classic portal, on the **Configure single sign-on at Cisco Webex** dialog page, select the single sign-on configuration confirmation, and then click **Complete**.</span></span>
   
   <span data-ttu-id="807c4-165">![Single Sign-On 구성](./media/active-directory-saas-cisco-webex-tutorial/IC777624.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="807c4-165">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777624.png "Configure single sign-on")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="807c4-166">사용자 프로비전 구성</span><span class="sxs-lookup"><span data-stu-id="807c4-166">Configure user provisioning</span></span>

<span data-ttu-id="807c4-167">Azure AD 사용자가 Cisco Webex에 로그인할 수 있도록 하려면 Cisco Webex로 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="807c4-167">In order to enable Azure AD users to log into Cisco Webex, they must be provisioned into Cisco Webex.</span></span>  

* <span data-ttu-id="807c4-168">Cisco Webex의 경우 프로비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="807c4-168">In the case of Cisco Webex, provisioning is a manual task.</span></span>

<span data-ttu-id="807c4-169">**사용자 계정을 프로비전하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="807c4-169">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="807c4-170">**Cisco Webex** 테넌트에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="807c4-170">Log in to your **Cisco Webex** tenant.</span></span>
2. <span data-ttu-id="807c4-171">**사용자 관리 \> 사용자 추가**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="807c4-171">Go to **Manage Users \> Add User**.</span></span>
   
   <span data-ttu-id="807c4-172">![사용자 추가](./media/active-directory-saas-cisco-webex-tutorial/IC777625.png "사용자 추가")</span><span class="sxs-lookup"><span data-stu-id="807c4-172">![Add users](./media/active-directory-saas-cisco-webex-tutorial/IC777625.png "Add users")</span></span>
3. <span data-ttu-id="807c4-173">사용자 추가 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="807c4-173">On the Add User section, perform the following steps:</span></span>
   
   <span data-ttu-id="807c4-174">![사용자 추가](./media/active-directory-saas-cisco-webex-tutorial/IC777626.png "사용자 추가")</span><span class="sxs-lookup"><span data-stu-id="807c4-174">![Add user](./media/active-directory-saas-cisco-webex-tutorial/IC777626.png "Add user")</span></span>   
   1. <span data-ttu-id="807c4-175">**계정 유형**으로 **호스트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="807c4-175">As **Account Type**, select **Host**.</span></span>
   2. <span data-ttu-id="807c4-176">**이름, 성**, **사용자 이름**, **전자 메일**, **암호**, **암호 확인** 텍스트 상자에 기존 Azure AD 사용자의 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="807c4-176">Type the information of an existing Azure AD user into the following textboxes: **First name, Last name**, **User name**, **Email**, **Password**, **Confirm Password**.</span></span>
   3. <span data-ttu-id="807c4-177">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="807c4-177">Click **Add**.</span></span>

>[!NOTE]
><span data-ttu-id="807c4-178">다른 Cisco Webex 사용자 계정 생성 도구 또는 Cisco Webex가 제공한 API를 사용하여 AAD 사용자 계정을 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="807c4-178">You can use any other Cisco Webex user account creation tools or APIs provided by Cisco Webex to provision AAD user accounts.</span></span> 
> 

## <a name="assign-users"></a><span data-ttu-id="807c4-179">사용자 할당</span><span class="sxs-lookup"><span data-stu-id="807c4-179">Assign users</span></span>
<span data-ttu-id="807c4-180">구성을 테스트하려면 응용 프로그램 사용을 허용하려는 Azure AD 사용자를 할당하여 액세스 권한을 부여해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="807c4-180">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="807c4-181">**Cisco Webex에 사용자를 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="807c4-181">**To assign users to Cisco Webex, perform the following steps:**</span></span>

1. <span data-ttu-id="807c4-182">Azure 클래식 포털에서 테스트 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="807c4-182">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="807c4-183">**Cisco Webex** 응용 프로그램 통합 페이지에서 **사용자 할당**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="807c4-183">On the **Cisco Webex** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="807c4-184">![사용자 할당](./media/active-directory-saas-cisco-webex-tutorial/IC777627.png "사용자 할당")</span><span class="sxs-lookup"><span data-stu-id="807c4-184">![Assign users](./media/active-directory-saas-cisco-webex-tutorial/IC777627.png "Assign users")</span></span>
3. <span data-ttu-id="807c4-185">테스트 사용자를 선택하고 **할당**을 클릭한 다음 **예**를 클릭하여 할당을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="807c4-185">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="807c4-186">![예](./media/active-directory-saas-cisco-webex-tutorial/IC767830.png "예")</span><span class="sxs-lookup"><span data-stu-id="807c4-186">![Yes](./media/active-directory-saas-cisco-webex-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="807c4-187">Single Sign-On 설정을 테스트하려면 액세스 패널을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="807c4-187">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="807c4-188">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="807c4-188">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

