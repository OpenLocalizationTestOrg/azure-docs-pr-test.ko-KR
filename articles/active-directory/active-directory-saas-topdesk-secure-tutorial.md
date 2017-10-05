---
title: "자습서: TOPdesk - Secure와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory에서 TOPdesk - Secure을 사용하여 Single Sign-On, 자동화된 프로비전 등을 사용하도록 설정하는 방법을 알아봅니다."
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
ms.openlocfilehash: 28f0542dbe87bb34c83a7852db7c3a9fef055ce9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-topdesk---secure"></a><span data-ttu-id="92f38-103">자습서: TOPdesk - Secure와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="92f38-103">Tutorial: Azure Active Directory integration with TOPdesk - Secure</span></span>
<span data-ttu-id="92f38-104">이 자습서는 Azure 및 TOPdesk - Secure의 통합을 보여 주기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="92f38-104">The objective of this tutorial is to show the integration of Azure and TOPdesk - Secure.</span></span>  
<span data-ttu-id="92f38-105">이 자습서에 설명된 시나리오에서는 사용자에게 이미 다음 항목이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="92f38-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="92f38-106">유효한 Azure 구독</span><span class="sxs-lookup"><span data-stu-id="92f38-106">A valid Azure subscription</span></span>
* <span data-ttu-id="92f38-107">TOPdesk - Secure Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="92f38-107">A TOPdesk - Secure single sign-on enabled subscription</span></span>

<span data-ttu-id="92f38-108">이 자습서를 완료한 후 TOPdesk – Secure에 할당한 Azure AD 사용자가 TOPdesk – Secure 회사 사이트 (서비스 공급자가 시작한 로그온)에서나 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 사용하여 응용 프로그램에 Single Sign-On할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92f38-108">After completing this tutorial, the Azure AD users you have assigned to TOPdesk - Secure will be able to single sign into the application at your TOPdesk - Secure company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="92f38-109">이 자습서에 설명된 시나리오는 다음 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92f38-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="92f38-110">TOPdesk - Secure에 응용 프로그램 통합 사용</span><span class="sxs-lookup"><span data-stu-id="92f38-110">Enabling the application integration for TOPdesk - Secure</span></span>
2. <span data-ttu-id="92f38-111">Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="92f38-111">Configuring single sign-on</span></span>
3. <span data-ttu-id="92f38-112">사용자 프로비전 구성</span><span class="sxs-lookup"><span data-stu-id="92f38-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="92f38-113">사용자 할당</span><span class="sxs-lookup"><span data-stu-id="92f38-113">Assigning users</span></span>

<span data-ttu-id="92f38-114">![시나리오](./media/active-directory-saas-topdesk-secure-tutorial/IC790596.png "시나리오")</span><span class="sxs-lookup"><span data-stu-id="92f38-114">![Scenario](./media/active-directory-saas-topdesk-secure-tutorial/IC790596.png "Scenario")</span></span>

## <a name="enabling-the-application-integration-for-topdesk---secure"></a><span data-ttu-id="92f38-115">TOPdesk - Secure에 응용 프로그램 통합 사용</span><span class="sxs-lookup"><span data-stu-id="92f38-115">Enabling the application integration for TOPdesk - Secure</span></span>
<span data-ttu-id="92f38-116">이 섹션은 TOPdesk - Secure에 응용 프로그램 통합을 사용하도록 설정하는 방법을 간략하게 설명하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="92f38-116">The objective of this section is to outline how to enable the application integration for TOPdesk - Secure.</span></span>

### <a name="to-enable-the-application-integration-for-topdesk---secure-perform-the-following-steps"></a><span data-ttu-id="92f38-117">TOPdesk - Secure에 응용 프로그램 통합을 사용하도록 설정하려면</span><span class="sxs-lookup"><span data-stu-id="92f38-117">To enable the application integration for TOPdesk - Secure, perform the following steps:</span></span>
1. <span data-ttu-id="92f38-118">Azure 클래식 포털의 왼쪽 탐색 창에서 **Active Directory**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="92f38-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="92f38-119">![Active Directory](./media/active-directory-saas-topdesk-secure-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="92f38-119">![Active Directory](./media/active-directory-saas-topdesk-secure-tutorial/IC700993.png "Active Directory")</span></span>

2. <span data-ttu-id="92f38-120">**디렉터리** 목록에서 디렉터리 통합을 사용하도록 설정할 디렉터리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="92f38-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="92f38-121">응용 프로그램 보기를 열려면 디렉터리 보기의 최상위 메뉴에서 **응용 프로그램** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="92f38-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="92f38-122">![응용 프로그램](./media/active-directory-saas-topdesk-secure-tutorial/IC700994.png "응용 프로그램")</span><span class="sxs-lookup"><span data-stu-id="92f38-122">![Applications](./media/active-directory-saas-topdesk-secure-tutorial/IC700994.png "Applications")</span></span>

4. <span data-ttu-id="92f38-123">페이지 맨 아래에 있는 **추가** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="92f38-123">Click **Add** at the bottom of the page.</span></span>
   
    <span data-ttu-id="92f38-124">![응용 프로그램 추가](./media/active-directory-saas-topdesk-secure-tutorial/IC749321.png "응용 프로그램 추가")</span><span class="sxs-lookup"><span data-stu-id="92f38-124">![Add application](./media/active-directory-saas-topdesk-secure-tutorial/IC749321.png "Add application")</span></span>

5. <span data-ttu-id="92f38-125">**수행할 작업** 대화 상자에서 **갤러리에서 응용 프로그램 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="92f38-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    <span data-ttu-id="92f38-126">![갤러리에서 응용 프로그램 추가](./media/active-directory-saas-topdesk-secure-tutorial/IC749322.png "갤러리에서 응용 프로그램 추가")</span><span class="sxs-lookup"><span data-stu-id="92f38-126">![Add an application from gallerry](./media/active-directory-saas-topdesk-secure-tutorial/IC749322.png "Add an application from gallerry")</span></span>

6. <span data-ttu-id="92f38-127">**검색 상자**에 **TOPdesk - Secure**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="92f38-127">In the **search box**, type **TOPdesk - Secure**.</span></span>
   
    <span data-ttu-id="92f38-128">![응용 프로그램 갤러리](./media/active-directory-saas-topdesk-secure-tutorial/IC790597.png "응용 프로그램 갤러리")</span><span class="sxs-lookup"><span data-stu-id="92f38-128">![Application Gallery](./media/active-directory-saas-topdesk-secure-tutorial/IC790597.png "Application Gallery")</span></span>

7. <span data-ttu-id="92f38-129">결과 창에서 **TOPdesk - Secure**를 선택하고 **완료**를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="92f38-129">In the results pane, select **TOPdesk - Secure**, and then click **Complete** to add the application.</span></span>
   
    <span data-ttu-id="92f38-130">![TOPdesk - Secure](./media/active-directory-saas-topdesk-secure-tutorial/IC791933.png "TOPdesk - Secure")</span><span class="sxs-lookup"><span data-stu-id="92f38-130">![TOPdesk - Secure](./media/active-directory-saas-topdesk-secure-tutorial/IC791933.png "TOPdesk - Secure")</span></span>

## <a name="configuring-single-sign-on"></a><span data-ttu-id="92f38-131">Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="92f38-131">Configuring single sign-on</span></span>
<span data-ttu-id="92f38-132">이 섹션은 사용자가 SAML 프로토콜 기반 페더레이션을 사용하여 Azure AD의 계정으로 TOPdesk - Secure에 인증할 수 있게 하는 방법을 간략하게 설명하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="92f38-132">The objective of this section is to outline how to enable users to authenticate to TOPdesk - Secure with their account in Azure AD using federation based on the SAML protocol.</span></span>  
<span data-ttu-id="92f38-133">TOPdesk - Secure에 대한 Single Sign-On을 구성하려면 로고 아이콘 파일을 업로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="92f38-133">Configuring single sign-on for TOPdesk - Secure requires you to upload a logo icon file.</span></span> <span data-ttu-id="92f38-134">아이콘 파일을 가져오려면 TOPdesk 지원팀에 문의합니다.</span><span class="sxs-lookup"><span data-stu-id="92f38-134">To get the icon file, contact the TOPdesk support team.</span></span>

### <a name="to-configure-single-sign-on-perform-the-following-steps"></a><span data-ttu-id="92f38-135">Single Sign-On을 구성하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="92f38-135">To configure single sign-on, perform the following steps:</span></span>
1. <span data-ttu-id="92f38-136">**TOPdesk - Secure** 회사 사이트에 관리자 권한으로 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="92f38-136">Sign on to your **TOPdesk - Secure** company site as an administrator.</span></span>
2. <span data-ttu-id="92f38-137">**TOPdesk** 메뉴에서 **설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="92f38-137">In the **TOPdesk** menu, click **Settings**.</span></span>
   
    <span data-ttu-id="92f38-138">![설정](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "설정")</span><span class="sxs-lookup"><span data-stu-id="92f38-138">![Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Settings")</span></span>

3. <span data-ttu-id="92f38-139">**로그인 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="92f38-139">Click **Login Settings**.</span></span>
   
    <span data-ttu-id="92f38-140">![로그인 설정](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "로그인 설정")</span><span class="sxs-lookup"><span data-stu-id="92f38-140">![Login Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Login Settings")</span></span>

4. <span data-ttu-id="92f38-141">**로그인 설정** 메뉴를 확장한 다음 **일반**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="92f38-141">Expand the **Login Settings** menu, and then click **General**.</span></span>
   
    <span data-ttu-id="92f38-142">![일반](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "일반")</span><span class="sxs-lookup"><span data-stu-id="92f38-142">![General](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "General")</span></span>

5. <span data-ttu-id="92f38-143">**SAML 로그인** 구성 섹션의 **보안** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="92f38-143">In the **Secure** section of the **SAML login** configuration section, perform the following steps:</span></span>
   
    <span data-ttu-id="92f38-144">![기술 설정](./media/active-directory-saas-topdesk-secure-tutorial/IC790855.png "기술 설정")</span><span class="sxs-lookup"><span data-stu-id="92f38-144">![Technical Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790855.png "Technical Settings")</span></span>
   
    <span data-ttu-id="92f38-145">a.</span><span class="sxs-lookup"><span data-stu-id="92f38-145">a.</span></span> <span data-ttu-id="92f38-146">**다운로드** 를 클릭하여 공용 메타데이터 파일을 다운로드한 다음 컴퓨터에 로컬 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="92f38-146">Click **Download** to download the public metadata file, and then save it locally on your computer.</span></span>
   
    <span data-ttu-id="92f38-147">b.</span><span class="sxs-lookup"><span data-stu-id="92f38-147">b.</span></span> <span data-ttu-id="92f38-148">메타데이터 파일을 열고 **AssertionConsumerService** 노드를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="92f38-148">Open the metadata file, and then locate the **AssertionConsumerService** node.</span></span>
    
    <span data-ttu-id="92f38-149">![Assertion Consumer Service](./media/active-directory-saas-topdesk-secure-tutorial/IC790856.png "Assertion Consumer Service")</span><span class="sxs-lookup"><span data-stu-id="92f38-149">![Assertion Consumer Service](./media/active-directory-saas-topdesk-secure-tutorial/IC790856.png "Assertion Consumer Service")</span></span>
   
    <span data-ttu-id="92f38-150">c.</span><span class="sxs-lookup"><span data-stu-id="92f38-150">c.</span></span> <span data-ttu-id="92f38-151">**AssertionConsumerService** 값을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="92f38-151">Copy the **AssertionConsumerService** value.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="92f38-152">해당 값은 자습서 뒷부분의 **앱 URL 구성** 섹션에서 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="92f38-152">You will need the value in the **Configure App URL** section later in this tutorial.</span></span>
    > 
    > 

6. <span data-ttu-id="92f38-153">다른 웹 브라우저 창에서 **Azure 클래식 포털** 에 관리자 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="92f38-153">In a different web browser window, log into your **Azure classic portal** as an administrator.</span></span>

7. <span data-ttu-id="92f38-154">에 **TOPdesk-Secure** 응용 프로그램 통합 페이지에서 클릭 **single sign on 구성** 열려는 * * Single Sign-on 구성 * * 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="92f38-154">On the **TOPdesk - Secure** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On ** dialog.</span></span>
   
    <span data-ttu-id="92f38-155">![Single Sign-On 구성](./media/active-directory-saas-topdesk-secure-tutorial/IC790602.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="92f38-155">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790602.png "Configure Single Sign-On")</span></span>

8. <span data-ttu-id="92f38-156">**TOPdesk - Secure에 대한 사용자 로그온 방법을 선택하세요.** 페이지에서 **Microsoft Azure AD Single Sign-On**을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="92f38-156">On the **How would you like users to sign on to TOPdesk - Secure** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="92f38-157">![Single Sign-On 구성](./media/active-directory-saas-topdesk-secure-tutorial/IC790603.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="92f38-157">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790603.png "Configure Single Sign-On")</span></span>

9. <span data-ttu-id="92f38-158">**앱 URL 구성** 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="92f38-158">On the **Configure App URL** page, perform the following steps:</span></span>
   
    <span data-ttu-id="92f38-159">![앱 URL 구성](./media/active-directory-saas-topdesk-secure-tutorial/IC790604.png "앱 URL 구성")</span><span class="sxs-lookup"><span data-stu-id="92f38-159">![Configure App URL](./media/active-directory-saas-topdesk-secure-tutorial/IC790604.png "Configure App URL")</span></span>
   
    <span data-ttu-id="92f38-160">a.</span><span class="sxs-lookup"><span data-stu-id="92f38-160">a.</span></span> <span data-ttu-id="92f38-161">**TOPdesk - Secure Sign On URL** 텍스트 상자에서 TOPdesk - 사용자가 Secure 응용 프로그램 로그인에 사용한 URL을 입력합니다(예: "*https://qssolutions.topdesk.net*").</span><span class="sxs-lookup"><span data-stu-id="92f38-161">In the **TOPdesk - Secure Sign On URL** textbox, type the URL used by your users to sign into your TOPdesk - Secure application (e.g.: "*https://qssolutions.topdesk.net*").</span></span>
   
    <span data-ttu-id="92f38-162">b.</span><span class="sxs-lookup"><span data-stu-id="92f38-162">b.</span></span> <span data-ttu-id="92f38-163">**TOPdesk – Public Reply URL** 텍스트 상자에서 **TOPdesk - Secure AssertionConsumerService URL**을 붙여넣습니다 (예: "*https://qssolutions.topdesk.net/tas/public/login/saml*")</span><span class="sxs-lookup"><span data-stu-id="92f38-163">In the **TOPdesk – Public Reply URL** textbox, paste the **TOPdesk - Secure AssertionConsumerService URL** (e.g.: "*https://qssolutions.topdesk.net/tas/public/login/saml*")</span></span>
   
    <span data-ttu-id="92f38-164">c.</span><span class="sxs-lookup"><span data-stu-id="92f38-164">c.</span></span> <span data-ttu-id="92f38-165">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="92f38-165">Click **Next**.</span></span>

10. <span data-ttu-id="92f38-166">**TOPdesk - Secure에서 Single Sign-On 구성** 페이지에서 메타데이터를 다운로드하려면 **메타데이터 다운로드**를 클릭한 다음 컴퓨터에 로컬 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="92f38-166">On the **Configure single sign-on at TOPdesk - Secure** page, to download your metadata file, click **Download metadata**, and then save the file locally on your computer.</span></span>
    
    <span data-ttu-id="92f38-167">![Single Sign-On 구성](./media/active-directory-saas-topdesk-secure-tutorial/IC790605.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="92f38-167">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790605.png "Configure Single Sign-On")</span></span>

11. <span data-ttu-id="92f38-168">인증서 파일을 만들려면 다음 단계를 수행하십시오.</span><span class="sxs-lookup"><span data-stu-id="92f38-168">To create a certificate file, perform the following steps:</span></span>
    
    <span data-ttu-id="92f38-169">![인증서](./media/active-directory-saas-topdesk-secure-tutorial/IC790606.png "인증서")</span><span class="sxs-lookup"><span data-stu-id="92f38-169">![Certificate](./media/active-directory-saas-topdesk-secure-tutorial/IC790606.png "Certificate")</span></span>
    
    <span data-ttu-id="92f38-170">a.</span><span class="sxs-lookup"><span data-stu-id="92f38-170">a.</span></span> <span data-ttu-id="92f38-171">다운로드한 메타데이터 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="92f38-171">Open the downloaded metadata file.</span></span>
    <span data-ttu-id="92f38-172">b.</span><span class="sxs-lookup"><span data-stu-id="92f38-172">b.</span></span> <span data-ttu-id="92f38-173">**fed:ApplicationServiceType**의 **xsi:type**을 가진 **RoleDescriptor** 노드를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="92f38-173">Expand the **RoleDescriptor** node that has a **xsi:type** of **fed:ApplicationServiceType**.</span></span>
    <span data-ttu-id="92f38-174">c.</span><span class="sxs-lookup"><span data-stu-id="92f38-174">c.</span></span> <span data-ttu-id="92f38-175">**X509Certificate** 노드의 값을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="92f38-175">Copy the value of the **X509Certificate** node.</span></span>
    <span data-ttu-id="92f38-176">ㄹ.</span><span class="sxs-lookup"><span data-stu-id="92f38-176">d.</span></span> <span data-ttu-id="92f38-177">복사한 **X509Certificate** 값을 컴퓨터에 파일로 로컬 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="92f38-177">Save the copied **X509Certificate** value locally on your computer in a file.</span></span>

12. <span data-ttu-id="92f38-178">TOPdesk - Secure 회사 사이트의 **TOPdesk** 메뉴에서 **설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="92f38-178">On your TOPdesk - Secure company site, in the **TOPdesk** menu, click **Settings**.</span></span>
    
    <span data-ttu-id="92f38-179">![설정](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "설정")</span><span class="sxs-lookup"><span data-stu-id="92f38-179">![Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Settings")</span></span>

13. <span data-ttu-id="92f38-180">**로그인 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="92f38-180">Click **Login Settings**.</span></span>
    
    <span data-ttu-id="92f38-181">![로그인 설정](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "로그인 설정")</span><span class="sxs-lookup"><span data-stu-id="92f38-181">![Login Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Login Settings")</span></span>

14. <span data-ttu-id="92f38-182">**로그인 설정** 메뉴를 확장한 다음 **일반**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="92f38-182">Expand the **Login Settings** menu, and then click **General**.</span></span>
    
    <span data-ttu-id="92f38-183">![일반](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "일반")</span><span class="sxs-lookup"><span data-stu-id="92f38-183">![General](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "General")</span></span>

15. <span data-ttu-id="92f38-184">**공용** 섹션에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="92f38-184">In the **Public** section, click **Add**.</span></span>
    
    <span data-ttu-id="92f38-185">![추가](./media/active-directory-saas-topdesk-secure-tutorial/IC790607.png "추가")</span><span class="sxs-lookup"><span data-stu-id="92f38-185">![Add](./media/active-directory-saas-topdesk-secure-tutorial/IC790607.png "Add")</span></span>

16. <span data-ttu-id="92f38-186">**SAML 구성 도우미** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="92f38-186">On the **SAML configuration assistant** dialog page, perform the following steps:</span></span>
    
    <span data-ttu-id="92f38-187">![SAML 구성 도우미](./media/active-directory-saas-topdesk-secure-tutorial/IC790608.png "SAML 구성 도우미")</span><span class="sxs-lookup"><span data-stu-id="92f38-187">![SAML Configuration Assistant](./media/active-directory-saas-topdesk-secure-tutorial/IC790608.png "SAML Configuration Assistant")</span></span>
    
    <span data-ttu-id="92f38-188">a.</span><span class="sxs-lookup"><span data-stu-id="92f38-188">a.</span></span> <span data-ttu-id="92f38-189">다운로드한 메타데이터 파일을 업로드하려면 **페더레이션 메타데이터**에서 **찾아보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="92f38-189">To upload your downloaded metadata file, under **Federation Metadata**, click **Browse**.</span></span>

    <span data-ttu-id="92f38-190">b.</span><span class="sxs-lookup"><span data-stu-id="92f38-190">b.</span></span> <span data-ttu-id="92f38-191">인증서 파일을 업로드하려면 **인증서(RSA)**에서 **찾아보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="92f38-191">To upload your certificate file, under **Certificate (RSA)**, click **Browse**.</span></span>

    <span data-ttu-id="92f38-192">c.</span><span class="sxs-lookup"><span data-stu-id="92f38-192">c.</span></span> <span data-ttu-id="92f38-193">TOPdesk 지원팀에서 받은 로고 파일을 업로드하려면 **로고 아이콘**에서 **찾아보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="92f38-193">To upload the logo file you got from the TOPdesk support team, under **Logo icon**, click **Browse**.</span></span>

    <span data-ttu-id="92f38-194">ㄹ.</span><span class="sxs-lookup"><span data-stu-id="92f38-194">d.</span></span> <span data-ttu-id="92f38-195">**사용자 이름 특성** 텍스트 상자에 **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="92f38-195">In the **User name attribute** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span>

    <span data-ttu-id="92f38-196">e.</span><span class="sxs-lookup"><span data-stu-id="92f38-196">e.</span></span> <span data-ttu-id="92f38-197">**이름 표시** 텍스트 상자에 구성할 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="92f38-197">In the **Display name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="92f38-198">f.</span><span class="sxs-lookup"><span data-stu-id="92f38-198">f.</span></span> <span data-ttu-id="92f38-199">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="92f38-199">Click **Save**.</span></span>

17. <span data-ttu-id="92f38-200">Azure 클래식 포털에서 Single Sign-On 구성 확인을 선택하고 **완료**를 클릭하여 **Single Sign-On 구성** 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="92f38-200">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="92f38-201">![Single Sign-On 구성](./media/active-directory-saas-topdesk-secure-tutorial/IC790609.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="92f38-201">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790609.png "Configure Single Sign-On")</span></span>

## <a name="configuring-user-provisioning"></a><span data-ttu-id="92f38-202">사용자 프로비전 구성</span><span class="sxs-lookup"><span data-stu-id="92f38-202">Configuring user provisioning</span></span>
<span data-ttu-id="92f38-203">Azure AD 사용자가 TOPdesk - Secure에 로그인 할 수 있도록 하려면 TOPdesk - Secure으로 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="92f38-203">In order to enable Azure AD users to log into TOPdesk - Secure, they must be provisioned into TOPdesk - Secure.</span></span>  
<span data-ttu-id="92f38-204">TOPdesk - Secure의 경우 프로비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="92f38-204">In the case of TOPdesk - Secure, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="92f38-205">사용자 프로비저닝을 구성하려면</span><span class="sxs-lookup"><span data-stu-id="92f38-205">To configure user provisioning, perform the following steps:</span></span>
1. <span data-ttu-id="92f38-206">**TOPdesk - Secure** 회사 사이트에 관리자 권한으로 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="92f38-206">Sign on to your **TOPdesk - Secure** company site as administrator.</span></span>
2. <span data-ttu-id="92f38-207">위쪽 메뉴에서 **TOPdesk \> 새로 만들기 \> 지원 파일 \> 연산자** 순으로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="92f38-207">In the menu on the top, click **TOPdesk \> New \> Support Files \> Operator**.</span></span>
   
    <span data-ttu-id="92f38-208">![연산자](./media/active-directory-saas-topdesk-secure-tutorial/IC790610.png "연산자")</span><span class="sxs-lookup"><span data-stu-id="92f38-208">![Operator](./media/active-directory-saas-topdesk-secure-tutorial/IC790610.png "Operator")</span></span>

3. <span data-ttu-id="92f38-209">**새로운 연산자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="92f38-209">On the **New Operator** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="92f38-210">![새로운 연산자](./media/active-directory-saas-topdesk-secure-tutorial/IC790611.png "새로운 연산자")</span><span class="sxs-lookup"><span data-stu-id="92f38-210">![New Operator](./media/active-directory-saas-topdesk-secure-tutorial/IC790611.png "New Operator")</span></span>
   
    <span data-ttu-id="92f38-211">a.</span><span class="sxs-lookup"><span data-stu-id="92f38-211">a.</span></span> <span data-ttu-id="92f38-212">일반 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="92f38-212">Click the General tab.</span></span>
   
    <span data-ttu-id="92f38-213">b.</span><span class="sxs-lookup"><span data-stu-id="92f38-213">b.</span></span> <span data-ttu-id="92f38-214">**성** 텍스트 상자의 **일반** 섹션에서 프로비전하려는 유효한 Azure Active Directory 계정의 성을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="92f38-214">In the **Surname** textbox of the **General** section, type the last name of a valid Azure Active Directory account you want to provision.</span></span>
   
    <span data-ttu-id="92f38-215">c.</span><span class="sxs-lookup"><span data-stu-id="92f38-215">c.</span></span> <span data-ttu-id="92f38-216">**위치** 섹션에서 계정에 대한 **사이트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="92f38-216">Select a **Site** for the account in the **Location** section.</span></span>
   
    <span data-ttu-id="92f38-217">ㄹ.</span><span class="sxs-lookup"><span data-stu-id="92f38-217">d.</span></span> <span data-ttu-id="92f38-218">**TOPdesk 로그인** 섹션의 **로그인 이름** 텍스트 상자에서 사용자의 로그인 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="92f38-218">In the **Login Name** textbox of the **TOPdesk Login** section, type a login name for your user.</span></span>
   
    <span data-ttu-id="92f38-219">e.</span><span class="sxs-lookup"><span data-stu-id="92f38-219">e.</span></span> <span data-ttu-id="92f38-220">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="92f38-220">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="92f38-221">다른 TOPdesk - Secure 사용자 계정 생성 도구 또는 TOPdesk - Secure이 제공한 API를 사용하여 AAD 사용자 계정을 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92f38-221">You can use any other TOPdesk - Secure user account creation tools or APIs provided by TOPdesk - Secure to provision AAD user accounts.</span></span>
> 
> 

## <a name="assigning-users"></a><span data-ttu-id="92f38-222">사용자 할당</span><span class="sxs-lookup"><span data-stu-id="92f38-222">Assigning users</span></span>
<span data-ttu-id="92f38-223">구성을 테스트하려면 응용 프로그램 사용을 허용하려는 Azure AD 사용자를 할당하여 액세스 권한을 부여해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="92f38-223">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

### <a name="to-assign-users-to-topdesk---secure-perform-the-following-steps"></a><span data-ttu-id="92f38-224">TOPdesk - Secure에 사용자를 할당하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="92f38-224">To assign users to TOPdesk - Secure, perform the following steps:</span></span>
1. <span data-ttu-id="92f38-225">Azure 클래식 포털에서 테스트 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="92f38-225">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="92f38-226">에 * * TOPdesk-Secure * * 응용 프로그램 통합 페이지에서 클릭 **사용자 할당**합니다.</span><span class="sxs-lookup"><span data-stu-id="92f38-226">On the **TOPdesk - Secure **application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="92f38-227">![사용자 할당](./media/active-directory-saas-topdesk-secure-tutorial/IC790612.png "사용자 할당")</span><span class="sxs-lookup"><span data-stu-id="92f38-227">![Assign Users](./media/active-directory-saas-topdesk-secure-tutorial/IC790612.png "Assign Users")</span></span>

3. <span data-ttu-id="92f38-228">테스트 사용자를 선택하고 **할당**을 클릭한 다음 **예**를 클릭하여 할당을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="92f38-228">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
    <span data-ttu-id="92f38-229">![예](./media/active-directory-saas-topdesk-secure-tutorial/IC767830.png "예")</span><span class="sxs-lookup"><span data-stu-id="92f38-229">![Yes](./media/active-directory-saas-topdesk-secure-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="92f38-230">Single Sign-On 설정을 테스트하려면 액세스 패널을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="92f38-230">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="92f38-231">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="92f38-231">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

