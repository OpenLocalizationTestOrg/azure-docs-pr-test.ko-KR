---
title: "자습서: TalentLMS와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 TalentLMS 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c903d20d-18e3-42b0-b997-6349c5412dde
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: f28d6fbfad9dae578a20db7218b7e3b174ed859c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-talentlms"></a><span data-ttu-id="4fc6b-103">자습서: TalentLMS와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="4fc6b-103">Tutorial: Azure Active Directory integration with TalentLMS</span></span>

<span data-ttu-id="4fc6b-104">이 자습서에서는 Azure AD(Azure Active Directory)와 TalentLMS를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-104">In this tutorial, you learn how to integrate TalentLMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4fc6b-105">TalentLMS를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-105">Integrating TalentLMS with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4fc6b-106">TalentLMS에 액세스할 수 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-106">You can control in Azure AD who has access to TalentLMS</span></span>
- <span data-ttu-id="4fc6b-107">사용자가 자신의 Azure AD 계정으로 TalentLMS에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-107">You can enable your users to automatically get signed-on to TalentLMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4fc6b-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="4fc6b-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4fc6b-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="4fc6b-110">Prerequisites</span></span>

<span data-ttu-id="4fc6b-111">TalentLMS와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-111">To configure Azure AD integration with TalentLMS, you need the following items:</span></span>

- <span data-ttu-id="4fc6b-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="4fc6b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4fc6b-113">TalentLMS Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="4fc6b-113">A TalentLMS single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4fc6b-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4fc6b-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4fc6b-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4fc6b-117">Azure AD 평가판 환경이 없으면 [평가판 제품](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4fc6b-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="4fc6b-118">Scenario description</span></span>
<span data-ttu-id="4fc6b-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4fc6b-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4fc6b-121">갤러리에서 TalentLMS 추가</span><span class="sxs-lookup"><span data-stu-id="4fc6b-121">Adding TalentLMS from the gallery</span></span>
2. <span data-ttu-id="4fc6b-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="4fc6b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-talentlms-from-the-gallery"></a><span data-ttu-id="4fc6b-123">갤러리에서 TalentLMS 추가</span><span class="sxs-lookup"><span data-stu-id="4fc6b-123">Adding TalentLMS from the gallery</span></span>
<span data-ttu-id="4fc6b-124">TalentLMS가 Azure AD에 통합되도록 구성하려면 갤러리의 TalentLMS를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-124">To configure the integration of TalentLMS into Azure AD, you need to add TalentLMS from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4fc6b-125">**갤러리에서 TalentLMS를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="4fc6b-125">**To add TalentLMS from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4fc6b-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4fc6b-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4fc6b-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="4fc6b-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="4fc6b-133">검색 상자에 **TalentLMS**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-133">In the search box, type **TalentLMS**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_search.png)

5. <span data-ttu-id="4fc6b-135">결과 패널에서 **TalentLMS**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-135">In the results panel, select **TalentLMS**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4fc6b-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="4fc6b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4fc6b-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 사용하여 TalentLMS에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-138">In this section, you configure and test Azure AD single sign-on with TalentLMS based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4fc6b-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 TalentLMS 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-139">For single sign-on to work, Azure AD needs to know what the counterpart user in TalentLMS is to a user in Azure AD.</span></span> <span data-ttu-id="4fc6b-140">즉, Azure AD 사용자와 TalentLMS의 관련 사용자 간에 연결 관계를 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-140">In other words, a link relationship between an Azure AD user and the related user in TalentLMS needs to be established.</span></span>

<span data-ttu-id="4fc6b-141">TalentLMS에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 연결 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-141">In TalentLMS, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="4fc6b-142">TalentLMS에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-142">To configure and test Azure AD single sign-on with TalentLMS, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4fc6b-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="4fc6b-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4fc6b-145">**[TalentLMS 테스트 사용자 만들기](#creating-a-talentlms-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 TalentLMS에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-145">**[Creating a TalentLMS test user](#creating-a-talentlms-test-user)** - to have a counterpart of Britta Simon in TalentLMS that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="4fc6b-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4fc6b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4fc6b-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="4fc6b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4fc6b-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 TalentLMS 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TalentLMS application.</span></span>

<span data-ttu-id="4fc6b-150">**TalentLMS에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="4fc6b-150">**To configure Azure AD single sign-on with TalentLMS, perform the following steps:**</span></span>

1. <span data-ttu-id="4fc6b-151">Azure Portal의 **TalentLMS** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-151">In the Azure portal, on the **TalentLMS** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="4fc6b-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_samlbase.png)

3. <span data-ttu-id="4fc6b-155">**TalentLMS 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-155">On the **TalentLMS Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_url.png)

    <span data-ttu-id="4fc6b-157">a.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-157">a.</span></span> <span data-ttu-id="4fc6b-158">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<tenant-name>.TalentLMSapp.com`</span><span class="sxs-lookup"><span data-stu-id="4fc6b-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.TalentLMSapp.com`</span></span>

    <span data-ttu-id="4fc6b-159">b.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-159">b.</span></span> <span data-ttu-id="4fc6b-160">**식별자** 텍스트 상자에서 `http://<tenant-name>.talentlms.com` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-160">In the **Identifier** textbox, type a URL using the following pattern: `http://<tenant-name>.talentlms.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4fc6b-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-161">These values are not real.</span></span> <span data-ttu-id="4fc6b-162">실제 로그온 URL 및 식별자로 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="4fc6b-163">이러한 값을 얻으려면 [TalentLMS 클라이언트 지원 팀](https://www.talentlms.com/contact)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-163">Contact [TalentLMS Client support team](https://www.talentlms.com/contact) to get these values.</span></span> 
 
4. <span data-ttu-id="4fc6b-164">**SAML 서명 인증서** 섹션에서 인증서의 **지문** 값을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-164">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value from the certificate.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_certificate.png) 

5. <span data-ttu-id="4fc6b-166">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-166">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-talentlms-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4fc6b-168">**TalentLMS 구성** 섹션에서 **TalentLMS 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-168">On the **TalentLMS Configuration** section, click **Configure TalentLMS** to open **Configure sign-on** window.</span></span> <span data-ttu-id="4fc6b-169">**빠른 참조 섹션**에서 **로그아웃 URL, SAML 엔터티 ID 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_configure.png)  

7. <span data-ttu-id="4fc6b-171">다른 웹 브라우저 창에서 TalentLMS 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-171">In a different web browser window, log in to your TalentLMS company site as an administrator.</span></span>

8. <span data-ttu-id="4fc6b-172">**계정 및 설정** 섹션에서 **사용자** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-172">In the **Account & Settings** section, click the **Users** tab.</span></span>
   
    <span data-ttu-id="4fc6b-173">![계정 & 설정](./media/active-directory-saas-talentlms-tutorial/IC777296.png "계정 & 설정")</span><span class="sxs-lookup"><span data-stu-id="4fc6b-173">![Account & Settings](./media/active-directory-saas-talentlms-tutorial/IC777296.png "Account & Settings")</span></span>

9. <span data-ttu-id="4fc6b-174">**SSO(Single Sign-On)**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-174">Click **Single Sign-On (SSO)**,</span></span>

10. <span data-ttu-id="4fc6b-175">Single Sign-On 섹션에서 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-175">In the Single Sign-On section, perform the following steps:</span></span>
   
    <span data-ttu-id="4fc6b-176">![Single Sign-On](./media/active-directory-saas-talentlms-tutorial/IC777297.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="4fc6b-176">![Single Sign-On](./media/active-directory-saas-talentlms-tutorial/IC777297.png "Single Sign-On")</span></span>   

    <span data-ttu-id="4fc6b-177">a.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-177">a.</span></span> <span data-ttu-id="4fc6b-178">**SSO 통합 형식** 목록에서 **SAML 2.0**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-178">From the **SSO integration type** list, select **SAML 2.0**.</span></span>

    <span data-ttu-id="4fc6b-179">b.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-179">b.</span></span> <span data-ttu-id="4fc6b-180">Azure Portal에서 복사한 **SAML 엔터티 ID** 값을 **ID 공급자(IDP)** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-180">In the **Identity provider (IDP)** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>
 
    <span data-ttu-id="4fc6b-181">c.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-181">c.</span></span> <span data-ttu-id="4fc6b-182">Azure Portal의 **지문** 값을 **Certificate Fingerprint**(인증서 지문) 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-182">Paste the **Thumbprint** value from Azure portal into the **Certificate fingerprint** textbox.</span></span>    

    <span data-ttu-id="4fc6b-183">d.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-183">d.</span></span>  <span data-ttu-id="4fc6b-184">Azure Portal에서 복사한 **SAML Single Sign-On 서비스 URL** 값을 **Remote sign-in URL**(원격 로그인 URL) 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-184">In the **Remote sign-in URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
 
    <span data-ttu-id="4fc6b-185">e.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-185">e.</span></span> <span data-ttu-id="4fc6b-186">Azure Portal에서 복사한 **로그아웃 URL** 값을 **Remote sign-out URL**(원격 로그아웃 URL) 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-186">In the **Remote sign-out URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="4fc6b-187">f.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-187">f.</span></span> <span data-ttu-id="4fc6b-188">다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-188">Fill in the following:</span></span> 

    * <span data-ttu-id="4fc6b-189">**TargetedID**(대상 ID) 텍스트 상자에 `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-189">In the **TargetedID** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`</span></span>
     
    * <span data-ttu-id="4fc6b-190">**이름** 텍스트 상자에 `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-190">In the **First name** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`</span></span>
    
    * <span data-ttu-id="4fc6b-191">**성** 텍스트 상자에 `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-191">In the **Last name** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`</span></span>
    
    * <span data-ttu-id="4fc6b-192">**메일** 텍스트 상자에 `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-192">In the **Email** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`</span></span>
    
11. <span data-ttu-id="4fc6b-193">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-193">Click **Save**.</span></span>
 
> [!TIP]
> <span data-ttu-id="4fc6b-194">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="4fc6b-195">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="4fc6b-196">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4fc6b-197">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="4fc6b-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="4fc6b-198">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="4fc6b-200">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="4fc6b-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4fc6b-201">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-talentlms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4fc6b-203">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-talentlms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4fc6b-205">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-talentlms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4fc6b-207">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-talentlms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4fc6b-209">a.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-209">a.</span></span> <span data-ttu-id="4fc6b-210">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4fc6b-211">b.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-211">b.</span></span> <span data-ttu-id="4fc6b-212">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4fc6b-213">c.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-213">c.</span></span> <span data-ttu-id="4fc6b-214">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="4fc6b-215">d.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-215">d.</span></span> <span data-ttu-id="4fc6b-216">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-216">Click **Create**.</span></span>
 
### <a name="creating-a-talentlms-test-user"></a><span data-ttu-id="4fc6b-217">TalentLMS 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="4fc6b-217">Creating a TalentLMS test user</span></span>

<span data-ttu-id="4fc6b-218">Azure AD 사용자가 TalentLMS에 로그인할 수 있도록 하려면 TalentLMS로 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-218">To enable Azure AD users to log in to TalentLMS, they must be provisioned into TalentLMS.</span></span> <span data-ttu-id="4fc6b-219">TalentLMS의 경우 프로비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-219">In the case of TalentLMS, provisioning is a manual task.</span></span>

<span data-ttu-id="4fc6b-220">**사용자 계정을 프로비전하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="4fc6b-220">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="4fc6b-221">자신의 **TalentLMS** 테넌트에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-221">Log in to your **TalentLMS** tenant.</span></span>

2. <span data-ttu-id="4fc6b-222">**사용자**를 클릭한 후 **사용자 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-222">Click **Users**, and then click **Add User**.</span></span>

3. <span data-ttu-id="4fc6b-223">**사용자 추가** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-223">On the **Add user** dialog page, perform the following steps:</span></span>
   
    <span data-ttu-id="4fc6b-224">![사용자 추가](./media/active-directory-saas-talentlms-tutorial/IC777299.png "사용자 추가")</span><span class="sxs-lookup"><span data-stu-id="4fc6b-224">![Add User](./media/active-directory-saas-talentlms-tutorial/IC777299.png "Add User")</span></span>  

    <span data-ttu-id="4fc6b-225">a.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-225">a.</span></span> <span data-ttu-id="4fc6b-226">**이름** 텍스트 상자에 사용자의 이름(예: **Britta**)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-226">In the **First name** textbox, enter the first name of user like **Britta**.</span></span>

    <span data-ttu-id="4fc6b-227">b.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-227">b.</span></span> <span data-ttu-id="4fc6b-228">**성** 텍스트 상자에 사용자의 성(예: **Simon**)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-228">In the **Last name** textbox, enter the last name of user like **Simon**.</span></span>
 
    <span data-ttu-id="4fc6b-229">c.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-229">c.</span></span> <span data-ttu-id="4fc6b-230">**전자 메일 주소** 텍스트 상자에 **brittasimon@contoso.com**과 같은 사용자의 메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-230">In the **Email address** textbox, enter the email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="4fc6b-231">d.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-231">d.</span></span> <span data-ttu-id="4fc6b-232">**사용자 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-232">Click **Add User**.</span></span>

>[!NOTE]
><span data-ttu-id="4fc6b-233">다른 TalentLMS 사용자 계정 생성 도구 또는 TalentLMS가 제공한 API를 사용하여 AAD 사용자 계정을 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-233">You can use any other TalentLMS user account creation tools or APIs provided by TalentLMS to provision AAD user accounts.</span></span>
 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="4fc6b-234">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="4fc6b-234">Assigning the Azure AD test user</span></span>

<span data-ttu-id="4fc6b-235">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 TalentLMS에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-235">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TalentLMS.</span></span>

![사용자 할당][200] 

<span data-ttu-id="4fc6b-237">**Britta Simon을 TalentLMS에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="4fc6b-237">**To assign Britta Simon to TalentLMS, perform the following steps:**</span></span>

1. <span data-ttu-id="4fc6b-238">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-238">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="4fc6b-240">응용 프로그램 목록에서 **TalentLMS**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-240">In the applications list, select **TalentLMS**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_app.png) 

3. <span data-ttu-id="4fc6b-242">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-242">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="4fc6b-244">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-244">Click **Add** button.</span></span> <span data-ttu-id="4fc6b-245">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="4fc6b-247">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-247">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="4fc6b-248">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4fc6b-249">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4fc6b-250">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="4fc6b-250">Testing single sign-on</span></span>

<span data-ttu-id="4fc6b-251">이 섹션은 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-251">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="4fc6b-252">액세스 패널에서 TalentLMS 타일을 클릭하면 TalentLMS 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6b-252">When you click the TalentLMS tile in the Access Panel, you should get automatically signed-on to your TalentLMS application</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4fc6b-253">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="4fc6b-253">Additional resources</span></span>

* [<span data-ttu-id="4fc6b-254">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="4fc6b-254">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4fc6b-255">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="4fc6b-255">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_203.png

