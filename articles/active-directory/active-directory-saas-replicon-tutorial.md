---
title: "자습서: Replicon과 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory에서 Replicon을 사용하여 Single Sign-On, 자동화된 프로비전 등을 사용하도록 설정하는 방법을 알아봅니다."
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
ms.openlocfilehash: 2aeeceb61191962b62892b8409218684f76c6fa8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-replicon"></a><span data-ttu-id="43766-103">자습서: Replicon과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="43766-103">Tutorial: Azure Active Directory integration with Replicon</span></span>
<span data-ttu-id="43766-104">이 자습서는 Azure 및 Replicon의 통합을 보여주기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="43766-104">The objective of this tutorial is to show the integration of Azure and Replicon.</span></span> <span data-ttu-id="43766-105">이 자습서에 설명된 시나리오에서는 사용자에게 이미 다음 항목이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="43766-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="43766-106">유효한 Azure 구독</span><span class="sxs-lookup"><span data-stu-id="43766-106">A valid Azure subscription</span></span>
* <span data-ttu-id="43766-107">Replicon 테넌트</span><span class="sxs-lookup"><span data-stu-id="43766-107">A Replicon tenant</span></span>

<span data-ttu-id="43766-108">이 자습서를 완료한 후 Replicon에 할당한 Azure AD 사용자가 Replicon 회사 사이트(서비스 공급자가 시작한 로그온)에서 또는 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 사용하여 응용 프로그램에 Single Sign-On 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43766-108">After completing this tutorial, the Azure AD users you have assigned to Replicon will be able to single sign into the application at your Replicon company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="43766-109">이 자습서에 설명된 시나리오는 다음 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43766-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="43766-110">Replicon에 응용 프로그램 통합 사용</span><span class="sxs-lookup"><span data-stu-id="43766-110">Enabling the application integration for Replicon</span></span>
2. <span data-ttu-id="43766-111">SSO(Single Sign-On) 구성</span><span class="sxs-lookup"><span data-stu-id="43766-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="43766-112">사용자 프로비전 구성</span><span class="sxs-lookup"><span data-stu-id="43766-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="43766-113">사용자 할당</span><span class="sxs-lookup"><span data-stu-id="43766-113">Assigning users</span></span>

<span data-ttu-id="43766-114">![시나리오](./media/active-directory-saas-replicon-tutorial/IC777798.png "시나리오")</span><span class="sxs-lookup"><span data-stu-id="43766-114">![Scenario](./media/active-directory-saas-replicon-tutorial/IC777798.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-replicon"></a><span data-ttu-id="43766-115">Replicon에 응용 프로그램 통합 사용</span><span class="sxs-lookup"><span data-stu-id="43766-115">Enable the application integration for Replicon</span></span>
<span data-ttu-id="43766-116">이 섹션은 Replicon에 응용 프로그램 통합을 사용하도록 설정하는 방법을 간략하게 설명하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="43766-116">The objective of this section is to outline how to enable the application integration for Replicon.</span></span>

<span data-ttu-id="43766-117">**Replicon에 응용 프로그램 통합을 사용하도록 설정하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="43766-117">**To enable the application integration for Replicon, perform the following steps:**</span></span>

1. <span data-ttu-id="43766-118">Azure 클래식 포털의 왼쪽 탐색 창에서 **Active Directory**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="43766-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="43766-119">![Active Directory](./media/active-directory-saas-replicon-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="43766-119">![Active Directory](./media/active-directory-saas-replicon-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="43766-120">**디렉터리** 목록에서 디렉터리 통합을 사용하도록 설정할 디렉터리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="43766-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="43766-121">응용 프로그램 보기를 열려면 디렉터리 보기의 최상위 메뉴에서 **응용 프로그램** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="43766-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="43766-122">![응용 프로그램](./media/active-directory-saas-replicon-tutorial/IC700994.png "응용 프로그램")</span><span class="sxs-lookup"><span data-stu-id="43766-122">![Applications](./media/active-directory-saas-replicon-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="43766-123">페이지 맨 아래에 있는 **추가** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="43766-123">Click **Add** at the bottom of the page.</span></span>
   
    <span data-ttu-id="43766-124">![응용 프로그램 추가](./media/active-directory-saas-replicon-tutorial/IC749321.png "응용 프로그램 추가")</span><span class="sxs-lookup"><span data-stu-id="43766-124">![Add application](./media/active-directory-saas-replicon-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="43766-125">**수행할 작업** 대화 상자에서 **갤러리에서 응용 프로그램 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="43766-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    <span data-ttu-id="43766-126">![갤러리에서 응용 프로그램 추가](./media/active-directory-saas-replicon-tutorial/IC749322.png "갤러리에서 응용 프로그램 추가")</span><span class="sxs-lookup"><span data-stu-id="43766-126">![Add an application from gallerry](./media/active-directory-saas-replicon-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="43766-127">**검색 상자**에 **Replicon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="43766-127">In the **search box**, type **Replicon**.</span></span>
   
    <span data-ttu-id="43766-128">![응용 프로그램 갤러리](./media/active-directory-saas-replicon-tutorial/IC777799.png "응용 프로그램 갤러리")</span><span class="sxs-lookup"><span data-stu-id="43766-128">![Application gallery](./media/active-directory-saas-replicon-tutorial/IC777799.png "Application gallery")</span></span>
7. <span data-ttu-id="43766-129">결과 창에서 **Replicon**을 선택하고 **완료**를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="43766-129">In the results pane, select **Replicon**, and then click **Complete** to add the application.</span></span>
   
    <span data-ttu-id="43766-130">![Replicon](./media/active-directory-saas-replicon-tutorial/IC777800.png "Replicon")</span><span class="sxs-lookup"><span data-stu-id="43766-130">![Replicon](./media/active-directory-saas-replicon-tutorial/IC777800.png "Replicon")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="43766-131">Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="43766-131">Configure single sign-on</span></span>

<span data-ttu-id="43766-132">이 섹션은 사용자가 SAML 프로토콜 기반 페더레이션을 사용하여 Azure AD의 계정으로 Replicon에 인증할 수 있게 하는 방법을 간략하게 설명하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="43766-132">The objective of this section is to outline how to enable users to authenticate to Replicon with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="43766-133">**Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="43766-133">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="43766-134">Azure 클래식 포털의 **Replicon** 응용 프로그램 통합 페이지에서 **Single Sign-On 구성**을 클릭하여 **Single Sign-On 구성** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="43766-134">In the Azure classic portal, on the **Replicon** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="43766-135">![Single Sign-On 구성](./media/active-directory-saas-replicon-tutorial/IC777801.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="43766-135">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC777801.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="43766-136">**Replicon에 대한 사용자 로그온 방법** 페이지에서 **Microsoft Azure AD Single Sign-On**을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="43766-136">On the **How would you like users to sign on to Replicon** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="43766-137">![Single Sign-On 구성](./media/active-directory-saas-replicon-tutorial/IC777802.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="43766-137">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC777802.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="43766-138">**앱 URL 구성** 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="43766-138">On the **Configure App URL** page, perform the following steps:</span></span>
   
    <span data-ttu-id="43766-139">![앱 URL 구성](./media/active-directory-saas-replicon-tutorial/IC777803.png "앱 URL 구성")</span><span class="sxs-lookup"><span data-stu-id="43766-139">![Configure app URL](./media/active-directory-saas-replicon-tutorial/IC777803.png "Configure app URL")</span></span>
  1. <span data-ttu-id="43766-140">**Replicon 로그온 URL** 텍스트 상자에서 Replicon 테넌트 URL을 입력(예: *https://na2.replicon.com/company/saml2/sp-sso/post*)합니다.</span><span class="sxs-lookup"><span data-stu-id="43766-140">In the **Replicon Sign On URL** textbox, type your Replicon tenant URL (e.g.: *https://na2.replicon.com/company/saml2/sp-sso/post*).</span></span>
  2. <span data-ttu-id="43766-141">**Replicon 회신 URL** 텍스트 상자에 Replicon **AssertionConsumerService** URL(예: *https://global.replicon.com/!/saml2/company/sso/post*)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="43766-141">In the **Replicon Reply URL** textbox, type your Replicon **AssertionConsumerService** URL(e.g.: *https://global.replicon.com/!/saml2/company/sso/post*).</span></span>  
      
     >[!NOTE]
     ><span data-ttu-id="43766-142">**https://global.replicon.com/!/saml2/\<YourCompanyKey\>**의 Replicon 메타데이터에서 URL을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43766-142">You can get the URL from the Replicon metadata at: **https://global.replicon.com/!/saml2/\<YourCompanyKey\>**.</span></span>
     > 
     > 
 
  3. <span data-ttu-id="43766-143">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="43766-143">Click **Next**.</span></span>

4. <span data-ttu-id="43766-144">**Replicon에서 Single Sign-On 구성** 페이지에서 **메타데이터를 다운로드**를 클릭한 다음 메타데이터를 컴퓨터에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="43766-144">On the **Configure single sign-on at Replicon** page, to download your metadata, click **Download metadata**, and then save the metadata on your computer.</span></span>
   
    <span data-ttu-id="43766-145">![Single Sign-On 구성](./media/active-directory-saas-replicon-tutorial/IC777804.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="43766-145">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC777804.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="43766-146">다른 웹 브라우저 창에서 Replicon 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="43766-146">In a different web browser window, log into your Replicon company site as an administrator.</span></span>

6. <span data-ttu-id="43766-147">다음 단계를 수행하여 SAML 2.0을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="43766-147">To configure SAML 2.0, perform the following steps:</span></span>
   
    <span data-ttu-id="43766-148">![SAML 인증 사용](./media/active-directory-saas-replicon-tutorial/IC777805.png "SAML 인증 사용")</span><span class="sxs-lookup"><span data-stu-id="43766-148">![Enable SAML authentication](./media/active-directory-saas-replicon-tutorial/IC777805.png "Enable SAML authentication")</span></span>
  
  1. <span data-ttu-id="43766-149">**EnableSAML Authentication2** 대화 상자를 표시하려면 URL에서 회사 키 다음에 **/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="43766-149">To display the **EnableSAML Authentication2** dialog, append the following to your URL, after your company key: **/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span></span>  
    * <span data-ttu-id="43766-150">전체 URL의 스키마는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="43766-150">The following shows the schema of the complete URL:</span></span>  
   <span data-ttu-id="43766-151">**https://na2.replicon.com/\<YourCompanyKey\>/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span><span class="sxs-lookup"><span data-stu-id="43766-151">**https://na2.replicon.com/\<YourCompanyKey\>/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span></span>
   2. <span data-ttu-id="43766-152">**+**을(를) 클릭하여 **v20Configuration** 섹션을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="43766-152">Click the **+** to expand the **v20Configuration** section.</span></span>
   3. <span data-ttu-id="43766-153">**+**을(를) 클릭하여 **metaDataConfiguration** 섹션을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="43766-153">Click the **+** to expand the **metaDataConfiguration** section.</span></span>
   4. <span data-ttu-id="43766-154">**파일 선택**을 클릭하여 ID 공급자 메타데이터 XML 파일을 선택하고 **제출**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="43766-154">Click **Choose File**, to select your identity provider metadata XML file, and click **Submit**.</span></span>

7. <span data-ttu-id="43766-155">Azure 클래식 포털에서 Single Sign-On 구성 확인을 선택하고 **완료**를 클릭하여 **Single Sign-On 구성** 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="43766-155">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="43766-156">![Single Sign-On 구성](./media/active-directory-saas-replicon-tutorial/IC778418.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="43766-156">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC778418.png "Configure single sign-on")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="43766-157">사용자 프로비전 구성</span><span class="sxs-lookup"><span data-stu-id="43766-157">Configure user provisioning</span></span>

<span data-ttu-id="43766-158">Azure AD 사용자가 Replicon에 로그인할 수 있도록 하려면 Replicon으로 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="43766-158">In order to enable Azure AD users to log into Replicon, they must be provisioned into Replicon.</span></span>  

<span data-ttu-id="43766-159">Replicon의 경우 프로비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="43766-159">In the case of Replicon, provisioning is a manual task.</span></span>

<span data-ttu-id="43766-160">**사용자 프로비전을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="43766-160">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="43766-161">웹 브라우저 창에서 Replicon 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="43766-161">In a web browser window, log into your Replicon company site as an administrator.</span></span>
2. <span data-ttu-id="43766-162">**관리 \> 사용자**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="43766-162">Go to **Administration \> Users**.</span></span>
   
    <span data-ttu-id="43766-163">![사용자](./media/active-directory-saas-replicon-tutorial/IC777806.png "사용자")</span><span class="sxs-lookup"><span data-stu-id="43766-163">![Users](./media/active-directory-saas-replicon-tutorial/IC777806.png "Users")</span></span>
3. <span data-ttu-id="43766-164">**+사용자 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="43766-164">Click **+Add User**.</span></span>
   
    <span data-ttu-id="43766-165">![사용자 추가](./media/active-directory-saas-replicon-tutorial/IC777807.png "사용자 추가")</span><span class="sxs-lookup"><span data-stu-id="43766-165">![Add User](./media/active-directory-saas-replicon-tutorial/IC777807.png "Add User")</span></span>
4. <span data-ttu-id="43766-166">**사용자 프로필** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="43766-166">In the **User Profile** section, perform the following steps:</span></span>
   
    <span data-ttu-id="43766-167">![사용자 프로필](./media/active-directory-saas-replicon-tutorial/IC777808.png "사용자 프로필")</span><span class="sxs-lookup"><span data-stu-id="43766-167">![User profile](./media/active-directory-saas-replicon-tutorial/IC777808.png "User profile")</span></span>
   
  1. <span data-ttu-id="43766-168">**로그인 이름** 텍스트 상자에 프로비전하려는 Azure AD 사용자의 Azure AD 메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="43766-168">In the **Login Name** textbox, type the Azure AD email address of the Azure AD user you want to provision.</span></span>
  2. <span data-ttu-id="43766-169">**인증 유형**으로 **SSO**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="43766-169">As **Authentication Type**, select **SSO**.</span></span>
  3. <span data-ttu-id="43766-170">**부서** 텍스트 상자에 사용자의 부서를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="43766-170">In the **Department** textbox, type the user’s department.</span></span>
  4. <span data-ttu-id="43766-171">**직원 형식**으로 **관리자**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="43766-171">As **Employee Type**, select **Administrator**.</span></span>
  5. <span data-ttu-id="43766-172">**사용자 프로필 저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="43766-172">Click **Save User Profile**.</span></span>

>[!NOTE]
><span data-ttu-id="43766-173">다른 Replicon 사용자 계정 생성 도구 또는 Replicon이 제공한 API를 사용하여 AAD 사용자 계정을 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43766-173">You can use any other Replicon user account creation tools or APIs provided by Replicon to provision AAD user accounts.</span></span>
> 
> 

## <a name="assign-users"></a><span data-ttu-id="43766-174">사용자 할당</span><span class="sxs-lookup"><span data-stu-id="43766-174">Assign users</span></span>
<span data-ttu-id="43766-175">구성을 테스트하려면 응용 프로그램 사용을 허용하려는 Azure AD 사용자를 할당하여 액세스 권한을 부여해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="43766-175">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="43766-176">**Replicon에 사용자를 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="43766-176">**To assign users to Replicon, perform the following steps:**</span></span>

1. <span data-ttu-id="43766-177">Azure 클래식 포털에서 테스트 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="43766-177">In the Azure classic portal, create a test account.</span></span>

2. <span data-ttu-id="43766-178">**Replicon** 응용 프로그램 통합 페이지에서 **사용자 할당**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="43766-178">On the **Replicon** application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="43766-179">![사용자 할당](./media/active-directory-saas-replicon-tutorial/IC777809.png "사용자 할당")</span><span class="sxs-lookup"><span data-stu-id="43766-179">![Assign users](./media/active-directory-saas-replicon-tutorial/IC777809.png "Assign users")</span></span>

3. <span data-ttu-id="43766-180">테스트 사용자를 선택하고 **할당**을 클릭한 다음 **예**를 클릭하여 할당을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="43766-180">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
    <span data-ttu-id="43766-181">![예](./media/active-directory-saas-replicon-tutorial/IC767830.png "예")</span><span class="sxs-lookup"><span data-stu-id="43766-181">![Yes](./media/active-directory-saas-replicon-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="43766-182">Single Sign-On 설정을 테스트하려면 액세스 패널을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="43766-182">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="43766-183">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="43766-183">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

