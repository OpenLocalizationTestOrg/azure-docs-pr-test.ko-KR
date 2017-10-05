---
title: "자습서: TOPdesk - Public과 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory 및 TOPdesk - Public 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0873299f-ce70-457b-addc-e57c5801275f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: f21fe0b363776974108ff460060e4c15a51a58a3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-topdesk---public"></a><span data-ttu-id="3a636-103">자습서: TOPdesk - Public과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="3a636-103">Tutorial: Azure Active Directory integration with TOPdesk - Public</span></span>

<span data-ttu-id="3a636-104">이 자습서에서는 Azure AD(Azure Active Directory)와 TOPdesk - Public을 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-104">In this tutorial, you learn how to integrate TOPdesk - Public with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3a636-105">TOPdesk - Public을 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-105">Integrating TOPdesk - Public with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3a636-106">TOPdesk - Public에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-106">You can control in Azure AD who has access to TOPdesk - Public.</span></span>
- <span data-ttu-id="3a636-107">사용자가 해당 Azure AD 계정으로 TOPdesk - Public에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-107">You can enable your users to automatically get signed-on to TOPdesk - Public (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="3a636-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="3a636-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3a636-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3a636-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="3a636-110">Prerequisites</span></span>

<span data-ttu-id="3a636-111">TOPdesk - Public과 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-111">To configure Azure AD integration with TOPdesk - Public, you need the following items:</span></span>

- <span data-ttu-id="3a636-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="3a636-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3a636-113">TOPdesk - Public Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="3a636-113">A TOPdesk - Public single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3a636-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3a636-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3a636-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="3a636-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3a636-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3a636-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="3a636-118">Scenario description</span></span>
<span data-ttu-id="3a636-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3a636-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3a636-121">갤러리에서 TOPdesk-Public 추가</span><span class="sxs-lookup"><span data-stu-id="3a636-121">Adding TOPdesk - Public from the gallery</span></span>
2. <span data-ttu-id="3a636-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="3a636-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-topdesk---public-from-the-gallery"></a><span data-ttu-id="3a636-123">갤러리에서 TOPdesk-Public 추가</span><span class="sxs-lookup"><span data-stu-id="3a636-123">Adding TOPdesk - Public from the gallery</span></span>
<span data-ttu-id="3a636-124">TOPdesk - Public이 Azure AD에 통합되도록 구성하려면 갤러리의 TOPdesk - Public을 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-124">To configure the integration of TOPdesk - Public into Azure AD, you need to add TOPdesk - Public from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3a636-125">**갤러리에서 TOPdesk - Public을 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="3a636-125">**To add TOPdesk - Public from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3a636-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory 단추][1]

2. <span data-ttu-id="3a636-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3a636-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-129">Then go to **All applications**.</span></span>

    ![엔터프라이즈 응용 프로그램 블레이드][2]
    
3. <span data-ttu-id="3a636-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![새 응용 프로그램 단추][3]

4. <span data-ttu-id="3a636-133">검색 상자에서 **TOPdesk - Public**을 입력하고, 결과 패널에서 **TOPdesk - Public**을 선택한 다음, **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-133">In the search box, type **TOPdesk - Public**, select **TOPdesk - Public** from result panel then click **Add** button to add the application.</span></span>

    ![결과 목록의 TOPdesk-Public](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="3a636-135">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="3a636-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="3a636-136">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 하여 TOPdesk-Public에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-136">In this section, you configure and test Azure AD single sign-on with TOPdesk - Public based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3a636-137">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 TOPdesk-Public 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-137">For single sign-on to work, Azure AD needs to know what the counterpart user in TOPdesk - Public is to a user in Azure AD.</span></span> <span data-ttu-id="3a636-138">즉, Azure AD 사용자와 TOPdesk-Public의 관련 사용자 간에 링크 관계가 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-138">In other words, a link relationship between an Azure AD user and the related user in TOPdesk - Public needs to be established.</span></span>

<span data-ttu-id="3a636-139">TOPdesk-Public에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-139">In TOPdesk - Public, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="3a636-140">TOPdesk-Public에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-140">To configure and test Azure AD single sign-on with TOPdesk - Public, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3a636-141">**[Azure AD Single Sign-On 구성](#configure-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3a636-142">**[Azure AD 테스트 사용자 만들기](#create-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3a636-143">**[TOPdesk-Public 테스트 사용자 만들기](#create-a-topdesk---public-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 TOPdesk-Public에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-143">**[Create a TOPdesk - Public test user](#create-a-topdesk---public-test-user)** - to have a counterpart of Britta Simon in TOPdesk - Public that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3a636-144">**[Azure AD 테스트 사용자 할당](#assign-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3a636-145">**[Single Sign-On 테스트](#test-single-sign-on)** - 구성이 작동하는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="3a636-146">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="3a636-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="3a636-147">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 TOPdesk-Public 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TOPdesk - Public application.</span></span>

<span data-ttu-id="3a636-148">**TOPdesk-Public에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="3a636-148">**To configure Azure AD single sign-on with TOPdesk - Public, perform the following steps:**</span></span>

1. <span data-ttu-id="3a636-149">Azure Portal의 **TOPdesk-Public** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-149">In the Azure portal, on the **TOPdesk - Public** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-On 구성 링크][4]

2. <span data-ttu-id="3a636-151">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_samlbase.png)

3. <span data-ttu-id="3a636-153">**TOPdesk-Public 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-153">On the **TOPdesk - Public Domain and URLs** section, perform the following steps:</span></span>

    ![TOPdesk-Public 도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_url.png)

    <span data-ttu-id="3a636-155">a.</span><span class="sxs-lookup"><span data-stu-id="3a636-155">a.</span></span> <span data-ttu-id="3a636-156">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<companyname>.topdesk.net`</span><span class="sxs-lookup"><span data-stu-id="3a636-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.topdesk.net`</span></span>
    
    <span data-ttu-id="3a636-157">b.</span><span class="sxs-lookup"><span data-stu-id="3a636-157">b.</span></span> <span data-ttu-id="3a636-158">**식별자** 텍스트 상자에서 `https://<companyname>.topdesk.net/tas/public/login/verify` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.topdesk.net/tas/public/login/verify`</span></span>

    <span data-ttu-id="3a636-159">c.</span><span class="sxs-lookup"><span data-stu-id="3a636-159">c.</span></span> <span data-ttu-id="3a636-160">**회신 URL** 텍스트 상자에 다음 패턴으로 URL을 입력합니다.`https://<companyname>.topdesk.net/tas/public/login/saml`</span><span class="sxs-lookup"><span data-stu-id="3a636-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.topdesk.net/tas/public/login/saml`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="3a636-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-161">These values are not real.</span></span> <span data-ttu-id="3a636-162">이러한 값을 실제 식별자, 회신 URL 및 로그온 URL로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-162">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="3a636-163">회신 URL은 자습서의 뒷부분에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-163">Reply URL is explaned later in tutorial.</span></span> <span data-ttu-id="3a636-164">이러한 값을 얻으려면 [TOPdesk-Public 클라이언트 지원 팀](https://help.topdesk.com/saas/enterprise/user/)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="3a636-164">Contact [TOPdesk - Public Client support team](https://help.topdesk.com/saas/enterprise/user/) to get these values.</span></span>  

4. <span data-ttu-id="3a636-165">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 메타데이터 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![인증서 다운로드 링크](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_certificate.png) 

5. <span data-ttu-id="3a636-167">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-167">Click **Save** button.</span></span>

    ![Single Sign-On 구성 저장 단추](./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="3a636-169">**TOPdesk - Public 구성** 섹션에서 **TOPdesk - Public 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-169">On the **TOPdesk - Public Configuration** section, click **Configure TOPdesk - Public** to open **Configure sign-on** window.</span></span> <span data-ttu-id="3a636-170">**빠른 참조 섹션**에서 **로그아웃 URL, SAML 엔터티 ID 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-170">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![TOPdesk-Public 구성](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_configure.png) 

7. <span data-ttu-id="3a636-172">**TOPdesk - Public** 회사 사이트에 관리자 권한으로 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-172">Sign on to your **TOPdesk - Public** company site as an administrator.</span></span>

8. <span data-ttu-id="3a636-173">**TOPdesk** 메뉴에서 **설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-173">In the **TOPdesk** menu, click **Settings**.</span></span>
   
    <span data-ttu-id="3a636-174">![설정](./media/active-directory-saas-topdesk-public-tutorial/ic790598.png "설정")</span><span class="sxs-lookup"><span data-stu-id="3a636-174">![Settings](./media/active-directory-saas-topdesk-public-tutorial/ic790598.png "Settings")</span></span>

9. <span data-ttu-id="3a636-175">**로그인 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-175">Click **Login Settings**.</span></span>
   
    <span data-ttu-id="3a636-176">![로그인 설정](./media/active-directory-saas-topdesk-public-tutorial/ic790599.png "로그인 설정")</span><span class="sxs-lookup"><span data-stu-id="3a636-176">![Login Settings](./media/active-directory-saas-topdesk-public-tutorial/ic790599.png "Login Settings")</span></span>

10. <span data-ttu-id="3a636-177">**로그인 설정** 메뉴를 확장한 다음 **일반**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-177">Expand the **Login Settings** menu, and then click **General**.</span></span>
   
    <span data-ttu-id="3a636-178">![일반](./media/active-directory-saas-topdesk-public-tutorial/ic790600.png "일반")</span><span class="sxs-lookup"><span data-stu-id="3a636-178">![General](./media/active-directory-saas-topdesk-public-tutorial/ic790600.png "General")</span></span>

11. <span data-ttu-id="3a636-179">**SAML 로그인** 구성 섹션의 **공용** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-179">In the **Public** section of the **SAML login** configuration section, perform the following steps:</span></span>
   
    <span data-ttu-id="3a636-180">![기술 설정](./media/active-directory-saas-topdesk-public-tutorial/ic790601.png "기술 설정")</span><span class="sxs-lookup"><span data-stu-id="3a636-180">![Technical Settings](./media/active-directory-saas-topdesk-public-tutorial/ic790601.png "Technical Settings")</span></span>
   
    <span data-ttu-id="3a636-181">a.</span><span class="sxs-lookup"><span data-stu-id="3a636-181">a.</span></span> <span data-ttu-id="3a636-182">**다운로드** 를 클릭하여 공용 메타데이터 파일을 다운로드한 다음 컴퓨터에 로컬 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-182">Click **Download** to download the public metadata file, and then save it locally on your computer.</span></span>
   
    <span data-ttu-id="3a636-183">b.</span><span class="sxs-lookup"><span data-stu-id="3a636-183">b.</span></span> <span data-ttu-id="3a636-184">다운로드한 메타데이터 파일을 연 다음 **AssertionConsumerService** 노드를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-184">Open the downloaded metadata file, and then locate the **AssertionConsumerService** node.</span></span>

    <span data-ttu-id="3a636-185">![AssertionConsumerService](./media/active-directory-saas-topdesk-public-tutorial/ic790619.png "AssertionConsumerService")</span><span class="sxs-lookup"><span data-stu-id="3a636-185">![AssertionConsumerService](./media/active-directory-saas-topdesk-public-tutorial/ic790619.png "AssertionConsumerService")</span></span>
   
    <span data-ttu-id="3a636-186">c.</span><span class="sxs-lookup"><span data-stu-id="3a636-186">c.</span></span> <span data-ttu-id="3a636-187">**AssertionConsumerService** 값을 복사하고 이 값을 **TOPdesk - Public 도메인 및 URL** 섹션의 **회신 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-187">Copy the **AssertionConsumerService** value, paste this value in the **Reply URL** textbox in **TOPdesk - Public Domain and URLs** section.</span></span>      
   
12. <span data-ttu-id="3a636-188">인증서 파일을 만들려면 다음 단계를 수행하십시오.</span><span class="sxs-lookup"><span data-stu-id="3a636-188">To create a certificate file, perform the following steps:</span></span>
    
    <span data-ttu-id="3a636-189">![인증서](./media/active-directory-saas-topdesk-public-tutorial/ic790606.png "인증서")</span><span class="sxs-lookup"><span data-stu-id="3a636-189">![Certificate](./media/active-directory-saas-topdesk-public-tutorial/ic790606.png "Certificate")</span></span>
    
    <span data-ttu-id="3a636-190">a.</span><span class="sxs-lookup"><span data-stu-id="3a636-190">a.</span></span> <span data-ttu-id="3a636-191">Azure Portal에서 다운로드한 메타데이터 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-191">Open the downloaded metadata file from Azure portal.</span></span>
    
    <span data-ttu-id="3a636-192">b.</span><span class="sxs-lookup"><span data-stu-id="3a636-192">b.</span></span> <span data-ttu-id="3a636-193">**fed:ApplicationServiceType**의 **xsi:type**을 가진 **RoleDescriptor** 노드를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-193">Expand the **RoleDescriptor** node that has a **xsi:type** of **fed:ApplicationServiceType**.</span></span>
    
    <span data-ttu-id="3a636-194">c.</span><span class="sxs-lookup"><span data-stu-id="3a636-194">c.</span></span> <span data-ttu-id="3a636-195">**X509Certificate** 노드의 값을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-195">Copy the value of the **X509Certificate** node.</span></span>
    
    <span data-ttu-id="3a636-196">ㄹ.</span><span class="sxs-lookup"><span data-stu-id="3a636-196">d.</span></span> <span data-ttu-id="3a636-197">복사한 **X509Certificate** 값을 컴퓨터에 파일로 로컬 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-197">Save the copied **X509Certificate** value locally on your computer in a file.</span></span>

13. <span data-ttu-id="3a636-198">**공용** 섹션에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-198">In the **Public** section, click **Add**.</span></span>
    
    <span data-ttu-id="3a636-199">![SAML 로그인](./media/active-directory-saas-topdesk-public-tutorial/ic790625.png "SAML 로그인")</span><span class="sxs-lookup"><span data-stu-id="3a636-199">![SAML Login](./media/active-directory-saas-topdesk-public-tutorial/ic790625.png "SAML Login")</span></span>

14. <span data-ttu-id="3a636-200">**SAML 구성 도우미** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-200">On the **SAML configuration assistant** dialog page, perform the following steps:</span></span>
    
    <span data-ttu-id="3a636-201">![SAML 구성 도우미](./media/active-directory-saas-topdesk-public-tutorial/ic790608.png "SAML 구성 도우미")</span><span class="sxs-lookup"><span data-stu-id="3a636-201">![SAML Configuration Assistant](./media/active-directory-saas-topdesk-public-tutorial/ic790608.png "SAML Configuration Assistant")</span></span>
    
    <span data-ttu-id="3a636-202">a.</span><span class="sxs-lookup"><span data-stu-id="3a636-202">a.</span></span> <span data-ttu-id="3a636-203">Azure Portal에서 다운로드한 메타데이터 파일을 업로드하려면 **페더레이션 메타데이터**에서 **찾아보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-203">To upload your downloaded metadata file from Azure portal, under **Federation Metadata**, click **Browse**.</span></span>

    <span data-ttu-id="3a636-204">b.</span><span class="sxs-lookup"><span data-stu-id="3a636-204">b.</span></span> <span data-ttu-id="3a636-205">인증서 파일을 업로드하려면 **인증서(RSA)**에서 **찾아보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-205">To upload your certificate file, under **Certificate (RSA)**, click **Browse**.</span></span>

    <span data-ttu-id="3a636-206">c.</span><span class="sxs-lookup"><span data-stu-id="3a636-206">c.</span></span> <span data-ttu-id="3a636-207">TOPdesk 지원팀에서 받은 로고 파일을 업로드하려면 **로고 아이콘**에서 **찾아보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-207">To upload the logo file you got from the TOPdesk support team, under **Logo icon**, click **Browse**.</span></span>

    <span data-ttu-id="3a636-208">d.</span><span class="sxs-lookup"><span data-stu-id="3a636-208">d.</span></span> <span data-ttu-id="3a636-209">**사용자 이름 특성** 텍스트 상자에서 `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-209">In the **User name attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>

    <span data-ttu-id="3a636-210">e.</span><span class="sxs-lookup"><span data-stu-id="3a636-210">e.</span></span> <span data-ttu-id="3a636-211">**이름 표시** 텍스트 상자에 구성할 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-211">In the **Display name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="3a636-212">f.</span><span class="sxs-lookup"><span data-stu-id="3a636-212">f.</span></span> <span data-ttu-id="3a636-213">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-213">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="3a636-214">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-214">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3a636-215">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-215">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3a636-216">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-216">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="3a636-217">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="3a636-217">Create an Azure AD test user</span></span>

<span data-ttu-id="3a636-218">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-218">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Azure AD 테스트 사용자 만들기][100]

<span data-ttu-id="3a636-220">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="3a636-220">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3a636-221">Azure Portal의 왼쪽 창에서 **Azure Active Directory** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-221">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Azure Active Directory 단추](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="3a636-223">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-223">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !["사용자 및 그룹" 및 "모든 사용자" 링크](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="3a636-225">**사용자** 대화 상자를 열려면 **모든 사용자** 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-225">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![추가 단추](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="3a636-227">**사용자** 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-227">In the **User** dialog box, perform the following steps:</span></span>

    ![사용자 대화 상자](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_04.png)

    <span data-ttu-id="3a636-229">a.</span><span class="sxs-lookup"><span data-stu-id="3a636-229">a.</span></span> <span data-ttu-id="3a636-230">**이름** 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-230">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3a636-231">b.</span><span class="sxs-lookup"><span data-stu-id="3a636-231">b.</span></span> <span data-ttu-id="3a636-232">**사용자 이름** 상자에 사용자인 Britta Simon의 전자 메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-232">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="3a636-233">c.</span><span class="sxs-lookup"><span data-stu-id="3a636-233">c.</span></span> <span data-ttu-id="3a636-234">**암호 표시** 확인란을 선택한 다음 **암호** 상자에 표시된 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-234">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="3a636-235">d.</span><span class="sxs-lookup"><span data-stu-id="3a636-235">d.</span></span> <span data-ttu-id="3a636-236">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-236">Click **Create**.</span></span>
 
### <a name="create-a-topdesk---public-test-user"></a><span data-ttu-id="3a636-237">TOPdesk-Public 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="3a636-237">Create a TOPdesk - Public test user</span></span>

<span data-ttu-id="3a636-238">Azure AD 사용자가 TOPdesk - Public에 로그인할 수 있도록 하려면 사용자가 TOPdesk - Public으로 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-238">In order to enable Azure AD users to log into TOPdesk - Public, they must be provisioned into TOPdesk - Public.</span></span>  
<span data-ttu-id="3a636-239">TOPdesk - Public의 경우 프로비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-239">In the case of TOPdesk - Public, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="3a636-240">사용자 프로비저닝을 구성하려면</span><span class="sxs-lookup"><span data-stu-id="3a636-240">To configure user provisioning, perform the following steps:</span></span>
1. <span data-ttu-id="3a636-241">**TOPdesk - Public** 회사 사이트에 관리자 권한으로 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-241">Sign on to your **TOPdesk - Public** company site as administrator.</span></span>

2. <span data-ttu-id="3a636-242">위쪽 메뉴에서 **TOPdesk \> 새로 만들기 \> 지원 파일 \> 사람** 순으로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-242">In the menu on the top, click **TOPdesk \> New \> Support Files \> Person**.</span></span>
   
    <span data-ttu-id="3a636-243">![사람](./media/active-directory-saas-topdesk-public-tutorial/ic790628.png "사람")</span><span class="sxs-lookup"><span data-stu-id="3a636-243">![Person](./media/active-directory-saas-topdesk-public-tutorial/ic790628.png "Person")</span></span>

3. <span data-ttu-id="3a636-244">새로운 사용자 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-244">On the New Person dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="3a636-245">![새로운 사람](./media/active-directory-saas-topdesk-public-tutorial/ic790629.png "새로운 사람")</span><span class="sxs-lookup"><span data-stu-id="3a636-245">![New Person](./media/active-directory-saas-topdesk-public-tutorial/ic790629.png "New Person")</span></span>
   
    <span data-ttu-id="3a636-246">a.</span><span class="sxs-lookup"><span data-stu-id="3a636-246">a.</span></span> <span data-ttu-id="3a636-247">일반 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-247">Click the General tab.</span></span>

    <span data-ttu-id="3a636-248">b.</span><span class="sxs-lookup"><span data-stu-id="3a636-248">b.</span></span> <span data-ttu-id="3a636-249">**성** 텍스트 상자에서 사용자의 성을 입력합니다(예: Simon).</span><span class="sxs-lookup"><span data-stu-id="3a636-249">In the **Surname** textbox, type Surname of the user like Simon</span></span>
 
    <span data-ttu-id="3a636-250">c.</span><span class="sxs-lookup"><span data-stu-id="3a636-250">c.</span></span> <span data-ttu-id="3a636-251">계정에 대한 **사이트** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-251">Select a **Site** for the account.</span></span>
 
    <span data-ttu-id="3a636-252">ㄹ.</span><span class="sxs-lookup"><span data-stu-id="3a636-252">d.</span></span> <span data-ttu-id="3a636-253">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-253">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="3a636-254">다른 TOPdesk - Public 사용자 계정 생성 도구 또는 TOPdesk - Public에서 제공하는 API를 사용하여 Azure AD 사용자 계정을 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-254">You can use any other TOPdesk - Public user account creation tools or APIs provided by TOPdesk - Public to provision Azure AD user accounts.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="3a636-255">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="3a636-255">Assign the Azure AD test user</span></span>

<span data-ttu-id="3a636-256">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 TOPdesk - Public에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-256">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TOPdesk - Public.</span></span>

![사용자 역할 할당][200] 

<span data-ttu-id="3a636-258">**TOPdesk - Public에 Britta Simon을 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="3a636-258">**To assign Britta Simon to TOPdesk - Public, perform the following steps:**</span></span>

1. <span data-ttu-id="3a636-259">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-259">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="3a636-261">응용 프로그램 목록에서 **TOPdesk-Public**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-261">In the applications list, select **TOPdesk - Public**.</span></span>

    ![응용 프로그램 목록의 TOPdesk-Public 링크](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_app.png)  

3. <span data-ttu-id="3a636-263">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-263">In the menu on the left, click **Users and groups**.</span></span>

    !["사용자 및 그룹" 링크][202]

4. <span data-ttu-id="3a636-265">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-265">Click **Add** button.</span></span> <span data-ttu-id="3a636-266">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-266">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![할당 추가 창][203]

5. <span data-ttu-id="3a636-268">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-268">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3a636-269">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-269">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3a636-270">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-270">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="3a636-271">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="3a636-271">Test single sign-on</span></span>

<span data-ttu-id="3a636-272">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-272">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="3a636-273">액세스 패널에서 TOPdesk - Public 타일을 클릭하면 TOPdesk - Public 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a636-273">When you click the TOPdesk - Public tile in the Access Panel, you should get automatically signed-on to your TOPdesk - Public application.</span></span>
<span data-ttu-id="3a636-274">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3a636-274">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="3a636-275">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="3a636-275">Additional resources</span></span>

* [<span data-ttu-id="3a636-276">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="3a636-276">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3a636-277">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="3a636-277">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_203.png

