---
title: "자습서: JIRA SAML SSO by Microsoft와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 JIRA SAML SSO by Microsoft 사이에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0dc847b9-eec4-4c31-845e-0144ddedc4a7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: b5f7813c8244d2964b6894ae49cd64e0ee71b704
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jira-saml-sso-by-microsoft"></a><span data-ttu-id="d3577-103">자습서: JIRA SAML SSO by Microsoft와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="d3577-103">Tutorial: Azure Active Directory integration with JIRA SAML SSO by Microsoft</span></span>

<span data-ttu-id="d3577-104">이 자습서에서는 Azure AD(Azure Active Directory)와 JIRA SAML SSO by Microsoft를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-104">In this tutorial, you learn how to integrate JIRA SAML SSO by Microsoft with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d3577-105">Azure AD와 JIRA SAML SSO by Microsoft를 통합하면 다음과 같은 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-105">Integrating JIRA SAML SSO by Microsoft with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d3577-106">JIRA SAML SSO by Microsoft에 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-106">You can control in Azure AD who has access to JIRA SAML SSO by Microsoft</span></span>
- <span data-ttu-id="d3577-107">사용자가 자신의 Azure AD 계정으로 JIRA SAML SSO by Microsoft에 자동으로 로그온(Single Sign-On) 되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-107">You can enable your users to automatically get signed-on to JIRA SAML SSO by Microsoft (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d3577-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d3577-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d3577-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d3577-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d3577-110">Prerequisites</span></span>

<span data-ttu-id="d3577-111">JIRA SAML SSO by Microsoft와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-111">To configure Azure AD integration with JIRA SAML SSO by Microsoft, you need the following items:</span></span>

- <span data-ttu-id="d3577-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="d3577-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d3577-113">JIRA 서버 응용 프로그램이 Windows 64비트 서버(온-프레미스 또는 클라우드 IaaS 인프라)에 설치되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-113">JIRA server application installed on a Windows 64-bit server (on premise or on the cloud IaaS infrastructure)</span></span>
- <span data-ttu-id="d3577-114">JIRA 서버에서 HTTPS를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-114">JIRA server is HTTPS enabled</span></span>
- <span data-ttu-id="d3577-115">지원되는 JIRA 플러그 인 버전은 아래 섹션에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-115">Note the supported versions for JIRA Plugin are mentioned in below section.</span></span>
- <span data-ttu-id="d3577-116">JIRA 서버가 인터넷에 연결되어 있고 인증을 위해 특히 Azure AD 로그인 페이지에 접속되고 Azure AD에서 토큰을 받을 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-116">JIRA server is reachable on internet particularly to Azure AD Login page for authentication and should able to receive the token from Azure AD</span></span>
- <span data-ttu-id="d3577-117">JIRA에 관리자 자격 증명이 설정되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-117">Admin credentials are set up in JIRA</span></span>
- <span data-ttu-id="d3577-118">JIRA에서 WebSudo를 사용하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-118">WebSudo is disabled in JIRA</span></span>
- <span data-ttu-id="d3577-119">JIRA 서버 응용 프로그램에서 생성된 테스트 사용자</span><span class="sxs-lookup"><span data-stu-id="d3577-119">Test user created in the JIRA server application</span></span>

> [!NOTE]
> <span data-ttu-id="d3577-120">이 자습서의 단계를 테스트하기 위해 JIRA의 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-120">To test the steps in this tutorial, we do not recommend using a production environment of JIRA.</span></span> <span data-ttu-id="d3577-121">응용 프로그램 개발 또는 스테이징 환경에서 통합을 먼저 테스트 한 다음 프로덕션 환경을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="d3577-121">Test the integration first in development or staging environment of the application and then use the production environment.</span></span>

<span data-ttu-id="d3577-122">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-122">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d3577-123">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="d3577-123">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d3577-124">Azure AD 평가판 환경이 없으면 [평가판 제품](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-124">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="supported-versions-of-jira"></a><span data-ttu-id="d3577-125">지원되는 JIRA 버전</span><span class="sxs-lookup"><span data-stu-id="d3577-125">Supported versions of JIRA</span></span> 

<span data-ttu-id="d3577-126">현재 기준으로 다음 버전의 JIRA가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-126">As of now, following versions of JIRA are supported:</span></span>

- <span data-ttu-id="d3577-127">JIRA 코어 및 소프트웨어: 6.0 ~ 7.2.0</span><span class="sxs-lookup"><span data-stu-id="d3577-127">JIRA Core and Software: 6.0 to 7.2.0</span></span>
- <span data-ttu-id="d3577-128">JIRA 서비스 데스크: 3.0 ~ 3.2</span><span class="sxs-lookup"><span data-stu-id="d3577-128">JIRA Service Desk: 3.0 to 3.2</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d3577-129">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="d3577-129">Scenario description</span></span>
<span data-ttu-id="d3577-130">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-130">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d3577-131">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-131">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d3577-132">갤러리에서 JIRA SAML SSO by Microsoft 추가</span><span class="sxs-lookup"><span data-stu-id="d3577-132">Adding JIRA SAML SSO by Microsoft from the gallery</span></span>
2. <span data-ttu-id="d3577-133">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="d3577-133">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jira-saml-sso-by-microsoft-from-the-gallery"></a><span data-ttu-id="d3577-134">갤러리에서 JIRA SAML SSO by Microsoft 추가</span><span class="sxs-lookup"><span data-stu-id="d3577-134">Adding JIRA SAML SSO by Microsoft from the gallery</span></span>
<span data-ttu-id="d3577-135">JIRA SAML SSO by Microsoft가 Azure AD에 통합되도록 구성하려면 갤러리에서 JIRA SAML SSO by Microsoft를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-135">To configure the integration of JIRA SAML SSO by Microsoft into Azure AD, you need to add JIRA SAML SSO by Microsoft from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d3577-136">**갤러리에서 JIRA SAML SSO by Microsoft를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="d3577-136">**To add JIRA SAML SSO by Microsoft from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d3577-137">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-137">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d3577-139">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-139">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d3577-140">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-140">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="d3577-142">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-142">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="d3577-144">검색 상자에 **JIRA SAML SSO by Microsoft**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-144">In the search box, type **JIRA SAML SSO by Microsoft**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_search.png)

5. <span data-ttu-id="d3577-146">결과 패널에서 **JIRA SAML SSO by Microsoft**를 선택한 다음 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-146">In the results panel, select **JIRA SAML SSO by Microsoft**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d3577-148">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="d3577-148">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d3577-149">이 섹션에서는 “Britta Simon”이라는 테스트 사용자를 기반으로 JIRA SAML SSO by Microsoft에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-149">In this section, you configure and test Azure AD single sign-on with JIRA SAML SSO by Microsoft based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d3577-150">Single Sign-On이 작동하려면 Azure AD의 사용자에 해당하는 JIRA SAML SSO by Microsoft의 사용자가 누구인지 Azure AD에서 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-150">For single sign-on to work, Azure AD needs to know what the counterpart user in JIRA SAML SSO by Microsoft is to a user in Azure AD.</span></span> <span data-ttu-id="d3577-151">즉, Azure AD 사용자와 JIRA SAML SSO by Microsoft의 관련 사용자 간에 링크 관계가 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-151">In other words, a link relationship between an Azure AD user and the related user in JIRA SAML SSO by Microsoft needs to be established.</span></span>

<span data-ttu-id="d3577-152">JIRA SAML SSO by Microsoft에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-152">In JIRA SAML SSO by Microsoft, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d3577-153">JIRA SAML SSO by Microsoft에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-153">To configure and test Azure AD single sign-on with JIRA SAML SSO by Microsoft, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d3577-154">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-154">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d3577-155">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-155">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d3577-156">**[JIRA SAML SSO by Microsoft 테스트 사용자 만들기](#creating-a-jira-saml-sso-by-microsoft-test-user)** - Britta Simon의 Azure AD 표현과 연결된 사용자를 JIRA SAML SSO by Microsoft에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-156">**[Creating a JIRA SAML SSO by Microsoft test user](#creating-a-jira-saml-sso-by-microsoft-test-user)** - to have a counterpart of Britta Simon in JIRA SAML SSO by Microsoft that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d3577-157">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-157">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d3577-158">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-158">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d3577-159">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="d3577-159">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d3577-160">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 JIRA SAML SSO by Microsoft 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-160">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your JIRA SAML SSO by Microsoft application.</span></span>

<span data-ttu-id="d3577-161">**JIRA SAML SSO by Microsoft에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="d3577-161">**To configure Azure AD single sign-on with JIRA SAML SSO by Microsoft, perform the following steps:**</span></span>

1. <span data-ttu-id="d3577-162">Azure Portal의 **JIRA SAML SSO by Microsoft** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-162">In the Azure portal, on the **JIRA SAML SSO by Microsoft** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="d3577-164">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-164">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_samlbase.png)

3. <span data-ttu-id="d3577-166">**JIRA SAML SSO by Microsoft 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-166">On the **JIRA SAML SSO by Microsoft Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_url.png)

    <span data-ttu-id="d3577-168">a.</span><span class="sxs-lookup"><span data-stu-id="d3577-168">a.</span></span> <span data-ttu-id="d3577-169">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<domain:port>/plugins/servlet/saml/auth`</span><span class="sxs-lookup"><span data-stu-id="d3577-169">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<domain:port>/plugins/servlet/saml/auth`</span></span>

    <span data-ttu-id="d3577-170">b.</span><span class="sxs-lookup"><span data-stu-id="d3577-170">b.</span></span> <span data-ttu-id="d3577-171">**식별자** 텍스트 상자에서 `https://<domain:port>/` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-171">In the **Identifier** textbox, type a URL using the following pattern: `https://<domain:port>/`</span></span>

    <span data-ttu-id="d3577-172">c.</span><span class="sxs-lookup"><span data-stu-id="d3577-172">c.</span></span> <span data-ttu-id="d3577-173">**회신 URL** 텍스트 상자에 다음 패턴으로 URL을 입력합니다.`https://<domain:port>/plugins/servlet/saml/auth`</span><span class="sxs-lookup"><span data-stu-id="d3577-173">In the **Reply URL** textbox, type a URL using the following pattern: `https://<domain:port>/plugins/servlet/saml/auth`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d3577-174">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-174">These values are not real.</span></span> <span data-ttu-id="d3577-175">이러한 값을 실제 식별자, 회신 URL 및 로그온 URL로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-175">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="d3577-176">명명된 URL인 경우 포트는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-176">Port is optional in case it’s a named URL.</span></span> <span data-ttu-id="d3577-177">이러한 값은 JIRA 플러그 인 구성 중에 수신되며 자습서의 뒷부분에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-177">These values are received during the configuration of Jira plugin, which is explained later in the tutorial.</span></span>
 
4. <span data-ttu-id="d3577-178">**메타데이터** URL을 생성하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-178">To generate the **Metadata** url, perform the following steps:</span></span>

    <span data-ttu-id="d3577-179">a.</span><span class="sxs-lookup"><span data-stu-id="d3577-179">a.</span></span> <span data-ttu-id="d3577-180">**앱 등록**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-180">Click **App registrations**.</span></span>
    
    ![Single Sign-on 구성](./media/active-directory-saas-jiramicrosoft-tutorial/appregistrations.png)
   
    <span data-ttu-id="d3577-182">b.</span><span class="sxs-lookup"><span data-stu-id="d3577-182">b.</span></span> <span data-ttu-id="d3577-183">**끝점**을 클릭하여 **끝점** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-183">Click **Endpoints** to open **Endpoints** dialog box.</span></span>  
    
    ![Single Sign-on 구성](./media/active-directory-saas-jiramicrosoft-tutorial/endpointicon.png)

    <span data-ttu-id="d3577-185">c.</span><span class="sxs-lookup"><span data-stu-id="d3577-185">c.</span></span> <span data-ttu-id="d3577-186">복사 단추를 클릭하여 **페더레이션 메타데이터 문서** URL을 복사하여 메모장에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-186">Click the copy button to copy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Single Sign-on 구성](./media/active-directory-saas-jiramicrosoft-tutorial/endpoint.png)
     
    <span data-ttu-id="d3577-188">d.</span><span class="sxs-lookup"><span data-stu-id="d3577-188">d.</span></span> <span data-ttu-id="d3577-189">이제 **JIRA SAML SSO by Microsoft**의 속성 페이지로 이동하고 **복사** 단추를 사용하여 **응용 프로그램 ID**를 복사하여 메모장에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-189">Now go to the property page of **JIRA SAML SSO by Microsoft** and copy the **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-jiramicrosoft-tutorial/appid.png)

    <span data-ttu-id="d3577-191">e.</span><span class="sxs-lookup"><span data-stu-id="d3577-191">e.</span></span> <span data-ttu-id="d3577-192">`<FEDERATION METADATA DOCUMENT url>?appid=<application id>` 패턴을 사용하여 **메타데이터 URL**을 생성하고 이 값을 메모장에 복사합니다. 나중에 플러그 인 구성에 사용되기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-192">Generate the **Metadata URL** using the following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>` and copy this value in notepad as it is used later for the configuration of the plugin.</span></span>

5. <span data-ttu-id="d3577-193">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-193">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d3577-195">JIRA 플러그 인에 대한 다음 정보로 [Microsoft](mailto:waadpartners@microsoft.com)에 문의합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-195">Contact [Microsoft](mailto:waadpartners@microsoft.com) with the following information for the JIRA plugin.</span></span>
    
    *   <span data-ttu-id="d3577-196">고객 이름:</span><span class="sxs-lookup"><span data-stu-id="d3577-196">Customer Name:</span></span>
    *   <span data-ttu-id="d3577-197">주 도메인 이름:</span><span class="sxs-lookup"><span data-stu-id="d3577-197">Primary domain name:</span></span>
    *   <span data-ttu-id="d3577-198">Azure AD Premium: 예/아니요(플러그 인은 무료, 기본 및 프리미엄 SKU에 해당하는 모든 고객이 사용할 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="d3577-198">Azure AD Premium: Yes/No (Plugin will be available to all     the customer Free, Basic, and Premium SKU)</span></span>
    *   <span data-ttu-id="d3577-199">이 통합을 사용할 사용자의 수:</span><span class="sxs-lookup"><span data-stu-id="d3577-199">Number of users who will be using this integration:</span></span>
    *   <span data-ttu-id="d3577-200">JIRA 버전:</span><span class="sxs-lookup"><span data-stu-id="d3577-200">JIRA Version:</span></span>
    *   <span data-ttu-id="d3577-201">설명:</span><span class="sxs-lookup"><span data-stu-id="d3577-201">Comments:</span></span>

7. <span data-ttu-id="d3577-202">다른 웹 브라우저 창에서 JIRA 인스턴스에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-202">In a different web browser window, log in to your JIRA instance as an administrator.</span></span>

8. <span data-ttu-id="d3577-203">마우스로 선 위를 가리키고 **추가 기능**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-203">Hover on cog and click the **Add-ons**.</span></span>
    
    ![Single Sign-on 구성](./media/active-directory-saas-jiramicrosoft-tutorial/addon1.png)

9. <span data-ttu-id="d3577-205">추가 기능 탭 섹션에서 **추가 기능 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-205">Under Add-ons tab section, click **Manage add-ons**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-jiramicrosoft-tutorial/addon7.png)

10. <span data-ttu-id="d3577-207">Microsoft에서 제공하는 플러그 인을 수동으로 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-207">Manually upload the plugin provided by Microsoft.</span></span> <span data-ttu-id="d3577-208">플러그 인이 설치되면 **추가 기능 관리** 섹션의 **사용자가 설치한** 추가 기능 섹션에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-208">Once the plugin is installed, it appears in **User Installed** add-ons section of **Manage Add-on** section.</span></span>

11. <span data-ttu-id="d3577-209">**구성**을 클릭하여 새 플러그 인을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-209">Click **Configure** to configure the new plugin.</span></span>

12. <span data-ttu-id="d3577-210">구성 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-210">Perform following steps on configuration page:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-jiramicrosoft-tutorial/addon5.png)
 
    <span data-ttu-id="d3577-212">a.</span><span class="sxs-lookup"><span data-stu-id="d3577-212">a.</span></span> <span data-ttu-id="d3577-213">**메타데이터 URL**에 Azure AD에서 생성된 **메타데이터 URL**을 붙여넣고 **해결** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-213">In **Metadata URL** paste the **Metadata URL** generated from Azure AD and click the **Resolve** button.</span></span> <span data-ttu-id="d3577-214">그러면 IdP 메타데이터 URL을 읽어와서 모든 필드 정보가 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-214">It reads the IdP metadata URL and populates all the fields information.</span></span>

    > [!Note]
    > <span data-ttu-id="d3577-215">기본 SAML 사용자 ID 위치는 이름 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-215">Default SAML User ID location is Name Identifier.</span></span> <span data-ttu-id="d3577-216">이것을 특성 옵션으로 변경하고 적절한 특성 이름을 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-216">You can change this to an attribute option and enter the appropriate attribute name.</span></span>

    > [!TIP]
    > <span data-ttu-id="d3577-217">메타데이터를 확인하는 데 오류가 없도록 앱에 매핑된 인증서가 하나만 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-217">Ensure that there is only one certificate mapped against the app so that there is no error in resolving the metadata.</span></span> <span data-ttu-id="d3577-218">인증서가 여러 개 있으면 메타데이터를 확인할 때 관리자에게 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-218">If there are multiple certificates, upon resolving the metadata, admin gets an error.</span></span>
    
    <span data-ttu-id="d3577-219">b.</span><span class="sxs-lookup"><span data-stu-id="d3577-219">b.</span></span> <span data-ttu-id="d3577-220">**식별자, 회신 URL 및 로그인 URL** 값을 복사하여 Azure Portal에서 **JIRA SAML SSO by Microsoft 도메인 및 URL** 섹션의 **식별자, 회신 URL 및 로그인 URL** 텍스트 상자에 각각 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-220">Copy the **Identifier, Reply URL and Sign on URL** values and paste them in **Identifier, Reply URL and Sign on URL** textboxes respectively in **JIRA SAML SSO by Microsoft Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="d3577-221">c.</span><span class="sxs-lookup"><span data-stu-id="d3577-221">c.</span></span> <span data-ttu-id="d3577-222">**Login Button Name**(로그인 단추 이름)에 조직이 사용자의 로그인 화면에 표시하려는 단추의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-222">In **Login Button Name** type the name of button your organization wants the users to see on login screen.</span></span>

    <span data-ttu-id="d3577-223">d.</span><span class="sxs-lookup"><span data-stu-id="d3577-223">d.</span></span> <span data-ttu-id="d3577-224">**SAML User ID Locations**(SAML 사용자 ID 위치)에서 **User ID is in the NameIdentifier element of the Subject statement**(사용자 ID는 Subject 문의 NameIdentifier 요소에 있습니다.) 또는 **User ID is in an Attribute element**(사용자 ID는 Attribute 요소에 있습니다.)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-224">In **SAML User ID Locations** select either **User ID is in the NameIdentifier element of the Subject statement** or **User ID is in an Attribute element**.</span></span>  <span data-ttu-id="d3577-225">이 ID는 JIRA 사용자 ID여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-225">This ID has to be the JIRA user id.</span></span> <span data-ttu-id="d3577-226">사용자 ID가 일치하지 않으면 시스템에서 사용자 로그인을 허용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-226">If the user id is not matched, then system will not allow users to log in.</span></span> 
    
    <span data-ttu-id="d3577-227">e.</span><span class="sxs-lookup"><span data-stu-id="d3577-227">e.</span></span> <span data-ttu-id="d3577-228">**User ID is in an Attribute element**(사용자 ID는 Attribute 요소에 있습니다.) 옵션을 선택하는 경우 **특성 이름** 텍스트 상자에 사용자 ID가 필요한 특성의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-228">If you select **User ID is in an Attribute element** option, then in **Attribute name** textbox type the name of the attribute where User Id is expected.</span></span> 

    <span data-ttu-id="d3577-229">f.</span><span class="sxs-lookup"><span data-stu-id="d3577-229">f.</span></span> <span data-ttu-id="d3577-230">Azure AD에서 페더레이션된 도메인(예: ADFS 등)을 사용하는 경우 **Enable Home Realm Discovery**(홈 영역 검색 사용) 옵션을 클릭하고 **도메인 이름**을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-230">If you are using the federated domain (like ADFS etc.) with Azure AD, then click on the **Enable Home Realm Discovery** option and configure the **Domain Name**.</span></span>
    
    <span data-ttu-id="d3577-231">g.</span><span class="sxs-lookup"><span data-stu-id="d3577-231">g.</span></span> <span data-ttu-id="d3577-232">**도메인 이름**에 ADFS 기반 로그인인 경우 여기에 도메인 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-232">In **Domain Name** type the domain name here in case of the ADFS-based login.</span></span>

    <span data-ttu-id="d3577-233">h.</span><span class="sxs-lookup"><span data-stu-id="d3577-233">h.</span></span> <span data-ttu-id="d3577-234">사용자가 JIRA에서 로그아웃할 때 Azure AD에서 로그아웃하려면 **Enable Single Sign out**(Single Sign-Out 사용)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-234">Check **Enable Single Sign out** if you wish to log out from Azure AD when a user logs out from JIRA.</span></span> 

    <span data-ttu-id="d3577-235">i.</span><span class="sxs-lookup"><span data-stu-id="d3577-235">i.</span></span> <span data-ttu-id="d3577-236">**저장** 단추를 클릭하여 설정을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-236">Click **Save** button to save the settings.</span></span>

> [!TIP]
> <span data-ttu-id="d3577-237">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-237">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d3577-238">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-238">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d3577-239">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-239">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d3577-240">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="d3577-240">Creating an Azure AD test user</span></span>
<span data-ttu-id="d3577-241">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-241">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="d3577-243">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="d3577-243">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d3577-244">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-244">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d3577-246">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-246">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d3577-248">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-248">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d3577-250">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-250">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d3577-252">a.</span><span class="sxs-lookup"><span data-stu-id="d3577-252">a.</span></span> <span data-ttu-id="d3577-253">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-253">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d3577-254">b.</span><span class="sxs-lookup"><span data-stu-id="d3577-254">b.</span></span> <span data-ttu-id="d3577-255">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-255">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d3577-256">c.</span><span class="sxs-lookup"><span data-stu-id="d3577-256">c.</span></span> <span data-ttu-id="d3577-257">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-257">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d3577-258">d.</span><span class="sxs-lookup"><span data-stu-id="d3577-258">d.</span></span> <span data-ttu-id="d3577-259">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-259">Click **Create**.</span></span>
 
### <a name="creating-a-jira-saml-sso-by-microsoft-test-user"></a><span data-ttu-id="d3577-260">JIRA SAML SSO by Microsoft 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="d3577-260">Creating a JIRA SAML SSO by Microsoft test user</span></span>

<span data-ttu-id="d3577-261">Azure AD 사용자가 JIRA 온-프레미스 서버에 로그인할 수 있게 하려면 사용자를 JIRA SAML SSO by Microsoft에 프로비전해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-261">To enable Azure AD users to log in to JIRA on-premise server, they must be provisioned into JIRA SAML SSO by Microsoft.</span></span> <span data-ttu-id="d3577-262">JIRA SAML SSO by Microsoft의 경우 프로비전이 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-262">For JIRA SAML SSO by Microsoft, provisioning is a manual task.</span></span>

<span data-ttu-id="d3577-263">**사용자 계정을 프로비전하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="d3577-263">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="d3577-264">JIRA 온-프레미스 서버에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-264">Log in to your JIRA on-premise server as an administrator.</span></span>

2. <span data-ttu-id="d3577-265">마우스로 선 위를 가리키고 **사용자 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-265">Hover on cog and click the **User management**.</span></span>

    ![직원 추가](./media/active-directory-saas-jiramicrosoft-tutorial/user1.png) 

3. <span data-ttu-id="d3577-267">리디렉션된 [관리자 액세스] 페이지에서 **암호**를 입력하고 **확인** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-267">You are redirected to Administrator Access page to enter **Password** and click **Confirm** button.</span></span>

    ![직원 추가](./media/active-directory-saas-jiramicrosoft-tutorial/user2.png) 

4. <span data-ttu-id="d3577-269">**사용자 관리** 탭 섹션 아래에서  **사용자 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-269">Under **User management** tab section, click **create user**.</span></span>

    ![직원 추가](./media/active-directory-saas-jiramicrosoft-tutorial/user3.png) 

5. <span data-ttu-id="d3577-271">**“새 사용자 만들기”** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-271">On the **“Create new user”** dialog page, perform the following steps:</span></span>

    ![직원 추가](./media/active-directory-saas-jiramicrosoft-tutorial/user4.png) 

    <span data-ttu-id="d3577-273">a.</span><span class="sxs-lookup"><span data-stu-id="d3577-273">a.</span></span> <span data-ttu-id="d3577-274">**이메일 주소** 텍스트 상자에서 Brittasimon@contoso.com과 같은 사용자의 이메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-274">In the **Email address** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="d3577-275">b.</span><span class="sxs-lookup"><span data-stu-id="d3577-275">b.</span></span> <span data-ttu-id="d3577-276">**전체 이름** 텍스트 상자에서 Britta Simon과 같은 사용자의 전체 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-276">In the **Full Name** textbox, type full name of the user like Britta Simon.</span></span>

    <span data-ttu-id="d3577-277">c.</span><span class="sxs-lookup"><span data-stu-id="d3577-277">c.</span></span> <span data-ttu-id="d3577-278">**사용자 이름** 텍스트 상자에서 Brittasimon@contoso.com과 같은 사용자의 이메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-278">In the **Username** textbox, type the email of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="d3577-279">d.</span><span class="sxs-lookup"><span data-stu-id="d3577-279">d.</span></span> <span data-ttu-id="d3577-280">**암호** 텍스트 상자에서 사용자에 대한 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-280">In the **Password** textbox, type the password of user.</span></span>

    <span data-ttu-id="d3577-281">e.</span><span class="sxs-lookup"><span data-stu-id="d3577-281">e.</span></span> <span data-ttu-id="d3577-282">**사용자 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-282">Click **Create user**.</span></span>   

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d3577-283">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="d3577-283">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d3577-284">이 섹션에서는 Britta Simon이 Azure Single Sign-On을 사용할 수 있도록 JIRA SAML SSO by Microsoft에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-284">In this section, you enable Britta Simon to use Azure single sign-on by granting access to JIRA SAML SSO by Microsoft.</span></span>

![사용자 할당][200] 

<span data-ttu-id="d3577-286">**Britta Simon을 JIRA SAML SSO by Microsoft에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="d3577-286">**To assign Britta Simon to JIRA SAML SSO by Microsoft, perform the following steps:**</span></span>

1. <span data-ttu-id="d3577-287">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-287">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="d3577-289">응용 프로그램 목록에서 **JIRA SAML SSO by Microsoft**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-289">In the applications list, select **JIRA SAML SSO by Microsoft**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_app.png) 

3. <span data-ttu-id="d3577-291">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-291">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="d3577-293">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-293">Click **Add** button.</span></span> <span data-ttu-id="d3577-294">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-294">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="d3577-296">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-296">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d3577-297">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-297">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d3577-298">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-298">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d3577-299">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="d3577-299">Testing single sign-on</span></span>

<span data-ttu-id="d3577-300">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-300">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d3577-301">액세스 패널에서 JIRA SAML SSO by Microsoft 타일을 클릭하면 JIRA SAML SSO by Microsoft 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3577-301">When you click the JIRA SAML SSO by Microsoft tile in the Access Panel, you should get automatically signed-on to your JIRA SAML SSO by Microsoft application.</span></span>
<span data-ttu-id="d3577-302">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d3577-302">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d3577-303">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="d3577-303">Additional resources</span></span>

* [<span data-ttu-id="d3577-304">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="d3577-304">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d3577-305">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="d3577-305">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_203.png

