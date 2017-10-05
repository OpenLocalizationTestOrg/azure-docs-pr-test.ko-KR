---
title: "자습서: Coupa와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory에서 Coupa를 사용하여 Single Sign-On, 자동화된 프로비전 등을 사용하도록 설정하는 방법을 알아봅니다."
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
ms.openlocfilehash: c952975919cfd948f1b9ea93ff2ac2641a53f923
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-coupa"></a><span data-ttu-id="54cd6-103">자습서: Coupa와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="54cd6-103">Tutorial: Azure Active Directory integration with Coupa</span></span>
<span data-ttu-id="54cd6-104">이 자습서는 Azure 및 Coupa의 통합을 보여주기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="54cd6-104">The objective of this tutorial is to show the integration of Azure and Coupa.</span></span>  
<span data-ttu-id="54cd6-105">이 자습서에 설명된 시나리오에서는 사용자에게 이미 다음 항목이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="54cd6-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="54cd6-106">유효한 Azure 구독</span><span class="sxs-lookup"><span data-stu-id="54cd6-106">A valid Azure subscription</span></span>
* <span data-ttu-id="54cd6-107">Coupa SSO(Single Sign-On)가 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="54cd6-107">A Coupa single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="54cd6-108">이 자습서를 완료한 후 Coupa에 할당한 Azure AD 사용자가 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 사용하여 응용 프로그램에 Single Sign-On 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54cd6-108">After completing this tutorial, the Azure AD users you have assigned to Coupa will be able to single sign into the application using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="54cd6-109">이 자습서에 설명된 시나리오는 다음 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54cd6-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

* <span data-ttu-id="54cd6-110">Coupa에 응용 프로그램 통합 사용</span><span class="sxs-lookup"><span data-stu-id="54cd6-110">Enabling the application integration for Coupa</span></span>
* <span data-ttu-id="54cd6-111">Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="54cd6-111">Configuring single sign-on</span></span>
* <span data-ttu-id="54cd6-112">사용자 프로비전 구성</span><span class="sxs-lookup"><span data-stu-id="54cd6-112">Configuring user provisioning</span></span>
* <span data-ttu-id="54cd6-113">사용자 할당</span><span class="sxs-lookup"><span data-stu-id="54cd6-113">Assigning users</span></span>

<span data-ttu-id="54cd6-114">![시나리오](./media/active-directory-saas-coupa-tutorial/IC791897.png "시나리오")</span><span class="sxs-lookup"><span data-stu-id="54cd6-114">![Scenario](./media/active-directory-saas-coupa-tutorial/IC791897.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-coupa"></a><span data-ttu-id="54cd6-115">Coupa에 응용 프로그램 통합 사용</span><span class="sxs-lookup"><span data-stu-id="54cd6-115">Enable the application integration for Coupa</span></span>
<span data-ttu-id="54cd6-116">이 섹션은 Coupa에 응용 프로그램 통합을 사용하도록 설정하는 방법을 간략하게 설명하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="54cd6-116">The objective of this section is to outline how to enable the application integration for Coupa.</span></span>

<span data-ttu-id="54cd6-117">**Coupa에 응용 프로그램 통합을 사용하도록 설정하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="54cd6-117">**To enable the application integration for Coupa, perform the following steps:**</span></span>

1. <span data-ttu-id="54cd6-118">Azure 클래식 포털의 왼쪽 탐색 창에서 **Active Directory**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54cd6-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="54cd6-119">![Active Directory](./media/active-directory-saas-coupa-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="54cd6-119">![Active Directory](./media/active-directory-saas-coupa-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="54cd6-120">**디렉터리** 목록에서 디렉터리 통합을 사용하도록 설정할 디렉터리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="54cd6-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="54cd6-121">응용 프로그램 보기를 열려면 디렉터리 보기의 최상위 메뉴에서 **응용 프로그램** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54cd6-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="54cd6-122">![응용 프로그램](./media/active-directory-saas-coupa-tutorial/IC700994.png "응용 프로그램")</span><span class="sxs-lookup"><span data-stu-id="54cd6-122">![Applications](./media/active-directory-saas-coupa-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="54cd6-123">페이지 맨 아래에 있는 **추가** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54cd6-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="54cd6-124">![응용 프로그램 추가](./media/active-directory-saas-coupa-tutorial/IC749321.png "응용 프로그램 추가")</span><span class="sxs-lookup"><span data-stu-id="54cd6-124">![Add application](./media/active-directory-saas-coupa-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="54cd6-125">**수행할 작업** 대화 상자에서 **갤러리에서 응용 프로그램 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54cd6-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="54cd6-126">![갤러리에서 응용 프로그램 추가](./media/active-directory-saas-coupa-tutorial/IC749322.png "갤러리에서 응용 프로그램 추가")</span><span class="sxs-lookup"><span data-stu-id="54cd6-126">![Add an application from gallerry](./media/active-directory-saas-coupa-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="54cd6-127">**검색 상자**에 **Coupa**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="54cd6-127">In the **search box**, type **Coupa**.</span></span>
   
   <span data-ttu-id="54cd6-128">![응용 프로그램 갤러리](./media/active-directory-saas-coupa-tutorial/IC791898.png "응용 프로그램 갤러리")</span><span class="sxs-lookup"><span data-stu-id="54cd6-128">![Application Gallery](./media/active-directory-saas-coupa-tutorial/IC791898.png "Application Gallery")</span></span>
7. <span data-ttu-id="54cd6-129">결과 창에서 **Coupa**를 선택하고 **완료**를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="54cd6-129">In the results pane, select **Coupa**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="54cd6-130">![Coupa](./media/active-directory-saas-coupa-tutorial/IC791899.png "Coupa")</span><span class="sxs-lookup"><span data-stu-id="54cd6-130">![Coupa](./media/active-directory-saas-coupa-tutorial/IC791899.png "Coupa")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="54cd6-131">Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="54cd6-131">Configure single sign-on</span></span>

<span data-ttu-id="54cd6-132">이 섹션은 사용자가 SAML 프로토콜 기반 페더레이션을 사용하여 Azure AD의 계정으로 Coupa에 인증할 수 있게 하는 방법을 간략하게 설명하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="54cd6-132">The objective of this section is to outline how to enable users to authenticate to Coupa with their account in Azure AD using federation based on the SAML protocol.</span></span>  

<span data-ttu-id="54cd6-133">Coupa에 대한 Single Sign-on을 구성하려면 인증서의 손도장(thumbprint) 값을 검색해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="54cd6-133">Configuring single sign-on for Coupa requires you to retrieve a thumbprint value from a certificate.</span></span> <span data-ttu-id="54cd6-134">이 절차를 잘 모르는 경우 [인증서의 지문 값을 검색하는 방법](http://youtu.be/YKQF266SAxI)을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="54cd6-134">If you are not familiar with this procedure, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span></span>

<span data-ttu-id="54cd6-135">**Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="54cd6-135">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="54cd6-136">Coupa 회사 사이트에 관리자 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="54cd6-136">Sign on to your Coupa company site as an administrator.</span></span>
2. <span data-ttu-id="54cd6-137">**설치 \> 보안 제어**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="54cd6-137">Go to **Setup \> Security Control**.</span></span>
   
   <span data-ttu-id="54cd6-138">![보안 제어](./media/active-directory-saas-coupa-tutorial/IC791900.png "보안 제어")</span><span class="sxs-lookup"><span data-stu-id="54cd6-138">![Security Controls](./media/active-directory-saas-coupa-tutorial/IC791900.png "Security Controls")</span></span>
3. <span data-ttu-id="54cd6-139">컴퓨터에 Coupa 메타데이터 파일을 다운로드하려면 **SP 메타데이터 다운로드 및 가져오기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54cd6-139">To download the Coupa metadata file to your computer, click **Download and import SP metadata**.</span></span>
   
   <span data-ttu-id="54cd6-140">![Coupa SP 메타데이터](./media/active-directory-saas-coupa-tutorial/IC791901.png "Coupa SP 메타데이터")</span><span class="sxs-lookup"><span data-stu-id="54cd6-140">![Coupa SP metadata](./media/active-directory-saas-coupa-tutorial/IC791901.png "Coupa SP metadata")</span></span>
4. <span data-ttu-id="54cd6-141">다른 브라우저 창에서 Azure 클래식 포털에 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="54cd6-141">In a different browser window, sign on to the Azure classic portal.</span></span>
5. <span data-ttu-id="54cd6-142">**Coupa** 응용 프로그램 통합 페이지에서 **Single Sign-On 구성**을 클릭하여 **Single Sign-On 구성** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="54cd6-142">On the **Coupa** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="54cd6-143">![Single Sign-On 구성](./media/active-directory-saas-coupa-tutorial/IC791902.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="54cd6-143">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791902.png "Configure Single Sign-On")</span></span>
6. <span data-ttu-id="54cd6-144">**Coupa에 대한 사용자 로그온 방법을 선택하세요.** 페이지에서 **Microsoft Azure AD Single Sign-on**을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54cd6-144">On the **How would you like users to sign on to Coupa** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="54cd6-145">![Single Sign-On 구성](./media/active-directory-saas-coupa-tutorial/IC791903.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="54cd6-145">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791903.png "Configure Single Sign-On")</span></span>
7. <span data-ttu-id="54cd6-146">**앱 URL 구성** 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="54cd6-146">On the **Configure App URL** page, perform the following steps:</span></span>
   
   <span data-ttu-id="54cd6-147">![앱 URL 구성](./media/active-directory-saas-coupa-tutorial/IC791904.png "앱 URL 구성")</span><span class="sxs-lookup"><span data-stu-id="54cd6-147">![Configure App URL](./media/active-directory-saas-coupa-tutorial/IC791904.png "Configure App URL")</span></span>   
   1. <span data-ttu-id="54cd6-148">**로그온 URL** 텍스트 상자에 사용자가 Coupar 응용 프로그램에 로그인하는 데 사용하는 URL(예: “*http://company.Coupa.com*”)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="54cd6-148">In the **Sign On URL** textbox, type URL used by your users to sign on to your Coupa application (e.g.: “*http://company.Coupa.com*”).</span></span>
   2. <span data-ttu-id="54cd6-149">다운로드한 Coupa 메타데이터 파일을 연 다음 **AssertionConsumerService index/URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="54cd6-149">Open your downloaded Coupa metadata file, and then copy the **AssertionConsumerService index/URL**.</span></span>
   3. <span data-ttu-id="54cd6-150">**Coupa 회신 URL** 텍스트 상자에 **AssertionConsumerService index/URL** 값을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="54cd6-150">In the **Coupa Reply URL** textbox, paste the **AssertionConsumerService index/URL** value.</span></span>
   4. <span data-ttu-id="54cd6-151">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="54cd6-151">Click **Next**.</span></span>
8. <span data-ttu-id="54cd6-152">**Coupa에서 Single Sign-On 구성** 페이지에서 메타데이터를 다운로드하려면 **메타데이터 다운로드**를 클릭한 다음 컴퓨터에 로컬 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="54cd6-152">On the **Configure single sign-on at Coupa** page, to download your metadata file, click **Download metadata**, and then save the file locally on your computer.</span></span>
   
   <span data-ttu-id="54cd6-153">![Single Sign-On 구성](./media/active-directory-saas-coupa-tutorial/IC791905.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="54cd6-153">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791905.png "Configure Single Sign-On")</span></span>
9. <span data-ttu-id="54cd6-154">Coupa 회사 사이트에서 **설치 \> 보안 제어**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="54cd6-154">On the Coupa company site, go to **Setup \> Security Control**.</span></span>
   
   <span data-ttu-id="54cd6-155">![보안 제어](./media/active-directory-saas-coupa-tutorial/IC791900.png "보안 제어")</span><span class="sxs-lookup"><span data-stu-id="54cd6-155">![Security Controls](./media/active-directory-saas-coupa-tutorial/IC791900.png "Security Controls")</span></span>
10. <span data-ttu-id="54cd6-156">**Coupa 자격 증명을 사용하여 로그인** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="54cd6-156">In the **Log in using Coupa credentials** section, perform the following steps:</span></span>  

   <span data-ttu-id="54cd6-157">![Coupa 자격 증명을 사용하여 로그인](./media/active-directory-saas-coupa-tutorial/IC791906.png "Coupa 자격 증명을 사용하여 로그인")</span><span class="sxs-lookup"><span data-stu-id="54cd6-157">![Log in using Coupa credentials](./media/active-directory-saas-coupa-tutorial/IC791906.png "Log in using Coupa credentials")</span></span> 
   1. <span data-ttu-id="54cd6-158">**SAML을 사용하여 로그인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="54cd6-158">Select **Log in using SAML**.</span></span>
   2. <span data-ttu-id="54cd6-159">**찾아보기** 를 클릭하여 다운로드한 Azure Active 메타데이터 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="54cd6-159">Click **Browse** to upload your downloaded Azure Active metadata file.</span></span>
   3. <span data-ttu-id="54cd6-160">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54cd6-160">Click **Save**.</span></span>
11. <span data-ttu-id="54cd6-161">Azure 클래식 포털에서 Single Sign-On 구성 확인을 선택하고 **완료**를 클릭하여 **Single Sign-On 구성** 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="54cd6-161">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
    
   <span data-ttu-id="54cd6-162">![Single Sign-On 구성](./media/active-directory-saas-coupa-tutorial/IC791907.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="54cd6-162">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791907.png "Configure Single Sign-On")</span></span>
    
## <a name="configure-user-provisioning"></a><span data-ttu-id="54cd6-163">사용자 프로비전 구성</span><span class="sxs-lookup"><span data-stu-id="54cd6-163">Configure user provisioning</span></span>

<span data-ttu-id="54cd6-164">Azure AD 사용자가 Coupa에 로그인할 수 있도록 하려면 Coupa로 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="54cd6-164">In order to enable Azure AD users to log into Coupa, they must be provisioned into Coupa.</span></span>  

* <span data-ttu-id="54cd6-165">Coupa의 경우 프로비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="54cd6-165">In the case of Coupa, provisioning is a manual task.</span></span>

<span data-ttu-id="54cd6-166">**사용자 프로비전을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="54cd6-166">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="54cd6-167">**Coupa** 회사 사이트에 관리자 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="54cd6-167">Log in to your **Coupa** company site as administrator.</span></span>
2. <span data-ttu-id="54cd6-168">위쪽 메뉴에서 **설정**을 클릭한 다음 **사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54cd6-168">In the menu on the top, click **Setup**, and then click **Users**.</span></span>
   
   <span data-ttu-id="54cd6-169">![사용자](./media/active-directory-saas-coupa-tutorial/IC791908.png "사용자")</span><span class="sxs-lookup"><span data-stu-id="54cd6-169">![Users](./media/active-directory-saas-coupa-tutorial/IC791908.png "Users")</span></span>
3. <span data-ttu-id="54cd6-170">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54cd6-170">Click **Create**.</span></span>
   
   <span data-ttu-id="54cd6-171">![사용자 만들기](./media/active-directory-saas-coupa-tutorial/IC791909.png "사용자 만들기")</span><span class="sxs-lookup"><span data-stu-id="54cd6-171">![Create Users](./media/active-directory-saas-coupa-tutorial/IC791909.png "Create Users")</span></span>
4. <span data-ttu-id="54cd6-172">**사용자 만들기** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="54cd6-172">In the **User Create** section, perform the following steps:</span></span>
   
   <span data-ttu-id="54cd6-173">![사용자 세부 정보](./media/active-directory-saas-coupa-tutorial/IC791910.png "사용자 세부 정보")</span><span class="sxs-lookup"><span data-stu-id="54cd6-173">![User Details](./media/active-directory-saas-coupa-tutorial/IC791910.png "User Details")</span></span>
   
   1. <span data-ttu-id="54cd6-174">관련된 텍스트 상자에 프로비전할 유효한 Azure Active Directory 계정의 **로그인**, **이름**, **성**, **Single Sign-On ID**, **전자 메일** 특성을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="54cd6-174">Type the **Login**, **First name**, **Last Name**, **Single Sign-On ID**, **Email** attributes of a valid Azure Active Directory account you want to provision into the related textboxes.</span></span>
   2. <span data-ttu-id="54cd6-175">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54cd6-175">Click **Create**.</span></span>   
   >[!NOTE]
   ><span data-ttu-id="54cd6-176">Azure Active Directory 계정 보유자는 활성화되기 전에 계정을 확인하기 위한 링크가 포함된 전자 메일을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="54cd6-176">The Azure Active Directory account holder will get an email with a link to confirm the account before it becomes active.</span></span> 
   > 

>[!NOTE]
><span data-ttu-id="54cd6-177">다른 Coupa 사용자 계정 생성 도구 또는 Coupa가 제공한 API를 사용하여 AAD 사용자 계정을 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54cd6-177">You can use any other Coupa user account creation tools or APIs provided by Coupa to provision AAD user accounts.</span></span> 
> 

## <a name="assign-users"></a><span data-ttu-id="54cd6-178">사용자 할당</span><span class="sxs-lookup"><span data-stu-id="54cd6-178">Assign users</span></span>
<span data-ttu-id="54cd6-179">구성을 테스트하려면 응용 프로그램 사용을 허용하려는 Azure AD 사용자를 할당하여 액세스 권한을 부여해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="54cd6-179">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="54cd6-180">**Coupa에 사용자를 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="54cd6-180">**To assign users to Coupa, perform the following steps:**</span></span>

1. <span data-ttu-id="54cd6-181">Azure 클래식 포털에서 테스트 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="54cd6-181">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="54cd6-182">에 * * Coupa * * 응용 프로그램 통합 페이지에서 클릭 **사용자 할당**합니다.</span><span class="sxs-lookup"><span data-stu-id="54cd6-182">On the **Coupa **application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="54cd6-183">![사용자 할당](./media/active-directory-saas-coupa-tutorial/IC791911.png "사용자 할당")</span><span class="sxs-lookup"><span data-stu-id="54cd6-183">![Assign Users](./media/active-directory-saas-coupa-tutorial/IC791911.png "Assign Users")</span></span>
3. <span data-ttu-id="54cd6-184">테스트 사용자를 선택하고 **할당**을 클릭한 다음 **예**를 클릭하여 할당을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="54cd6-184">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="54cd6-185">![예](./media/active-directory-saas-coupa-tutorial/IC767830.png "예")</span><span class="sxs-lookup"><span data-stu-id="54cd6-185">![Yes](./media/active-directory-saas-coupa-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="54cd6-186">Single Sign-On 설정을 테스트하려면 액세스 패널을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="54cd6-186">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="54cd6-187">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="54cd6-187">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

