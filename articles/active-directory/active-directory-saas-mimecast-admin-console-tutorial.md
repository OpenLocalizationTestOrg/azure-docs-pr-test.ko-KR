---
title: "자습서: Azure Active Directory와 Mimecast 관리 콘솔의 통합 | Microsoft Docs"
description: "Azure Active Directory와 Mimecast 관리 콘솔 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 81c50614-f49b-4bbc-97d5-3cf77154305f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: jeedes
ms.openlocfilehash: f401f592d79ad954aa466de74d3e3fbb18aa9a5b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mimecast-admin-console"></a><span data-ttu-id="65ca7-103">자습서: Azure Active Directory와 Mimecast 관리 콘솔의 통합</span><span class="sxs-lookup"><span data-stu-id="65ca7-103">Tutorial: Azure Active Directory integration with Mimecast Admin Console</span></span>

<span data-ttu-id="65ca7-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Mimecast 관리 콘솔을 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-104">In this tutorial, you learn how to integrate Mimecast Admin Console with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="65ca7-105">Mimecast 관리 콘솔을 Azure AD와 통합하면 다음과 같은 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-105">Integrating Mimecast Admin Console with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="65ca7-106">Mimecast 관리 콘솔에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-106">You can control in Azure AD who has access to Mimecast Admin Console.</span></span>
- <span data-ttu-id="65ca7-107">사용자가 자신의 Azure AD 계정으로 Mimecast 관리 콘솔에 자동으로 로그온(Single Sign-On) 되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-107">You can enable your users to automatically get signed-on to Mimecast Admin Console (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="65ca7-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="65ca7-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="65ca7-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="65ca7-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="65ca7-110">Prerequisites</span></span>

<span data-ttu-id="65ca7-111">Mimecast 관리 콘솔과 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-111">To configure Azure AD integration with Mimecast Admin Console, you need the following items:</span></span>

- <span data-ttu-id="65ca7-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="65ca7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="65ca7-113">Mimecast 관리 콘솔 Single Sign-On이 활성화된 구독</span><span class="sxs-lookup"><span data-stu-id="65ca7-113">A Mimecast Admin Console single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="65ca7-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="65ca7-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="65ca7-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="65ca7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="65ca7-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="65ca7-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="65ca7-118">Scenario description</span></span>
<span data-ttu-id="65ca7-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="65ca7-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="65ca7-121">갤러리에서 Mimecast 관리 콘솔 추가</span><span class="sxs-lookup"><span data-stu-id="65ca7-121">Adding Mimecast Admin Console from the gallery</span></span>
2. <span data-ttu-id="65ca7-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="65ca7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mimecast-admin-console-from-the-gallery"></a><span data-ttu-id="65ca7-123">갤러리에서 Mimecast 관리 콘솔 추가</span><span class="sxs-lookup"><span data-stu-id="65ca7-123">Adding Mimecast Admin Console from the gallery</span></span>
<span data-ttu-id="65ca7-124">Mimecast 관리 콘솔이 Azure AD에 통합되도록 구성하려면 갤러리에서 Mimecast 관리 콘솔을 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-124">To configure the integration of Mimecast Admin Console into Azure AD, you need to add Mimecast Admin Console from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="65ca7-125">**갤러리에서 Mimecast 관리 콘솔을 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="65ca7-125">**To add Mimecast Admin Console from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="65ca7-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory 단추][1]

2. <span data-ttu-id="65ca7-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="65ca7-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-129">Then go to **All applications**.</span></span>

    ![엔터프라이즈 응용 프로그램 블레이드][2]
    
3. <span data-ttu-id="65ca7-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![새 응용 프로그램 단추][3]

4. <span data-ttu-id="65ca7-133">검색 상자에 **Mimecast 관리 콘솔**를 입력하고 결과 패널에서 **Mimecast 관리 콘솔**을 선택한 후 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-133">In the search box, type **Mimecast Admin Console**, select **Mimecast Admin Console** from result panel then click **Add** button to add the application.</span></span>

    ![결과 목록에서 Mimecast 관리 콘솔](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="65ca7-135">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="65ca7-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="65ca7-136">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Mimecast 관리 콘솔에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-136">In this section, you configure and test Azure AD single sign-on with Mimecast Admin Console based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="65ca7-137">Single Sign-On이 작동하려면 Azure AD 사용자에 해당하는 Mimecast 관리 콘솔 사용자가 누구인지 Azure AD에서 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Mimecast Admin Console is to a user in Azure AD.</span></span> <span data-ttu-id="65ca7-138">즉, Azure AD 사용자와 Mimecast 관리 콘솔의 관련 사용자 간에 링크 관계가 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-138">In other words, a link relationship between an Azure AD user and the related user in Mimecast Admin Console needs to be established.</span></span>

<span data-ttu-id="65ca7-139">Mimecast 관리 콘솔에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-139">In Mimecast Admin Console, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="65ca7-140">Mimecast 관리 콘솔에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-140">To configure and test Azure AD single sign-on with Mimecast Admin Console, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="65ca7-141">**[Azure AD Single Sign-On 구성](#configure-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="65ca7-142">**[Azure AD 테스트 사용자 만들기](#create-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="65ca7-143">**[Mimecast 관리 콘솔 테스트 사용자 만들기](#create-a-mimecast-admin-console-test-user)** - Britta Simon의 Azure AD 표현과 연결되는 대응 사용자를 Mimecast 관리 콘솔에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-143">**[Create a Mimecast Admin Console test user](#create-a-mimecast-admin-console-test-user)** - to have a counterpart of Britta Simon in Mimecast Admin Console that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="65ca7-144">**[Azure AD 테스트 사용자 할당](#assign-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="65ca7-145">**[Single Sign-On 테스트](#test-single-sign-on)** - 구성이 작동하는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="65ca7-146">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="65ca7-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="65ca7-147">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Mimecast 관리 콘솔 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Mimecast Admin Console application.</span></span>

<span data-ttu-id="65ca7-148">**Mimecast 관리 콘솔에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="65ca7-148">**To configure Azure AD single sign-on with Mimecast Admin Console, perform the following steps:**</span></span>

1. <span data-ttu-id="65ca7-149">Azure Portal의 **Mimecast 관리 콘솔** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-149">In the Azure portal, on the **Mimecast Admin Console** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-On 구성 링크][4]

2. <span data-ttu-id="65ca7-151">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_samlbase.png)

3. <span data-ttu-id="65ca7-153">**Mimecast 관리 콘솔 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-153">On the **Mimecast Admin Console Domain and URLs** section, perform the following steps:</span></span>

    ![Mimecast 관리 콘솔 도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_url.png)

    <span data-ttu-id="65ca7-155">**로그온 URL** 텍스트 상자에서 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-155">In the **Sign-on URL** textbox, type the URL:</span></span>
    | |
    | -- |
    | `https://webmail-uk.mimecast.com`|
    | `https://webmail-us.mimecast.com`|

    > [!NOTE] 
    > <span data-ttu-id="65ca7-156">로그인 URL은 특정 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-156">The sign on URL is region specific.</span></span>

4. <span data-ttu-id="65ca7-157">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-157">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![인증서 다운로드 링크](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_certificate.png) 

5. <span data-ttu-id="65ca7-159">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-159">Click **Save** button.</span></span>

    ![Single Sign-On 구성 저장 단추](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="65ca7-161">**Mimecast 관리 콘솔 구성** 섹션에서 **Mimecast 관리 콘솔 구성**을 클릭하고 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-161">On the **Mimecast Admin Console Configuration** section, click **Configure Mimecast Admin Console** to open **Configure sign-on** window.</span></span> <span data-ttu-id="65ca7-162">**빠른 참조 섹션**에서 **SAML 엔터티 ID 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-162">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Mimecast 관리 콘솔 구성](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_configure.png) 

7. <span data-ttu-id="65ca7-164">다른 웹 브라우저 창에서 Mimecast 관리 콘솔에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-164">In a different web browser window, log into your Mimecast Admin Console as an administrator.</span></span>

8. <span data-ttu-id="65ca7-165">**서비스 \> 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-165">Go to **Services \> Application**.</span></span>

    <span data-ttu-id="65ca7-166">![서비스](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794998.png "서비스")</span><span class="sxs-lookup"><span data-stu-id="65ca7-166">![Services](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794998.png "Services")</span></span>

9. <span data-ttu-id="65ca7-167">**인증 프로필**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-167">Click **Authentication Profiles**.</span></span>

    <span data-ttu-id="65ca7-168">![인증 프로필](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794999.png "인증 프로필")</span><span class="sxs-lookup"><span data-stu-id="65ca7-168">![Authentication Profiles](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794999.png "Authentication Profiles")</span></span>
    
10. <span data-ttu-id="65ca7-169">**새 인증 프로필**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-169">Click **New Authentication Profile**.</span></span>

    <span data-ttu-id="65ca7-170">![새 인증 프로필](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795000.png "새 인증 프로필")</span><span class="sxs-lookup"><span data-stu-id="65ca7-170">![New Authentication Profiles](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795000.png "New Authentication Profiles")</span></span>

11. <span data-ttu-id="65ca7-171">**인증 프로필** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-171">In the **Authentication Profile** section, perform the following steps:</span></span>

    <span data-ttu-id="65ca7-172">![인증 프로필](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795015.png "인증 프로필")</span><span class="sxs-lookup"><span data-stu-id="65ca7-172">![Authentication Profile](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795015.png "Authentication Profile")</span></span>
    
    <span data-ttu-id="65ca7-173">a.</span><span class="sxs-lookup"><span data-stu-id="65ca7-173">a.</span></span> <span data-ttu-id="65ca7-174">**설명** 텍스트 상자에 구성 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-174">In the **Description** textbox, type a name for your configuration.</span></span>
    
    <span data-ttu-id="65ca7-175">b.</span><span class="sxs-lookup"><span data-stu-id="65ca7-175">b.</span></span> <span data-ttu-id="65ca7-176">**Mimecast 관리 콘솔에 SAML 인증 적용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-176">Select **Enforce SAML Authentication for Mimecast Admin Console**.</span></span>
    
    <span data-ttu-id="65ca7-177">c.</span><span class="sxs-lookup"><span data-stu-id="65ca7-177">c.</span></span> <span data-ttu-id="65ca7-178">**공급자**로 **Azure Active Directory**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-178">As **Provider**, select **Azure Active Directory**.</span></span>
    
    <span data-ttu-id="65ca7-179">d.</span><span class="sxs-lookup"><span data-stu-id="65ca7-179">d.</span></span> <span data-ttu-id="65ca7-180">Azure Portal에서 복사한 **SAML 엔터티 ID**를 **발급자 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-180">Paste **SAML Entity ID**, which you have copied from the Azure portal into the **Issuer URL** textbox.</span></span>
    
    <span data-ttu-id="65ca7-181">e.</span><span class="sxs-lookup"><span data-stu-id="65ca7-181">e.</span></span> <span data-ttu-id="65ca7-182">Azure Portal에서 복사한 **SAML Single Sign-On 서비스 URL**을 **로그인 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-182">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal into the **Login URL** textbox.</span></span>

    <span data-ttu-id="65ca7-183">f.</span><span class="sxs-lookup"><span data-stu-id="65ca7-183">f.</span></span> <span data-ttu-id="65ca7-184">Azure Portal에서 복사한 **SAML Single Sign-On 서비스 URL**을 **로그아웃 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-184">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal into the **Logout URL** textbox.</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="65ca7-185">로그인 URL 값과 로그아웃 URL 값은 Mimecast 관리 콘솔에 대해 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-185">The Login URL value and the Logout URL value are for the Mimecast Admin Console the same.</span></span>
    
    <span data-ttu-id="65ca7-186">g.</span><span class="sxs-lookup"><span data-stu-id="65ca7-186">g.</span></span> <span data-ttu-id="65ca7-187">메모장에서 Azure Portal로부터 다운로드한 base-64 인증서를 열고, 첫 줄(“*--*”) 및 마지막 줄(“*--*”)을 제거하고, 나머지 내용을 클립보드에 복사한 다음 **ID 공급자 인증서(메타데이터)** 텍스트 상자로 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-187">Open your base-64 certificate downloaded from Azure portal in notepad, remove the first line (“*--*“) and the last line (“*--*“), copy the remaining content of it into your clipboard, and then paste it to the **Identity Provider Certificate (Metadata)** textbox.</span></span>
    
    <span data-ttu-id="65ca7-188">h.</span><span class="sxs-lookup"><span data-stu-id="65ca7-188">h.</span></span> <span data-ttu-id="65ca7-189">**Single Sign-On 허용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-189">Select **Allow Single Sign On**.</span></span>
    
    <span data-ttu-id="65ca7-190">i.</span><span class="sxs-lookup"><span data-stu-id="65ca7-190">i.</span></span> <span data-ttu-id="65ca7-191">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-191">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="65ca7-192">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="65ca7-193">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="65ca7-194">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="65ca7-195">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="65ca7-195">Create an Azure AD test user</span></span>

<span data-ttu-id="65ca7-196">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-196">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Azure AD 테스트 사용자 만들기][100]

<span data-ttu-id="65ca7-198">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="65ca7-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="65ca7-199">Azure Portal의 왼쪽 창에서 **Azure Active Directory** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-199">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Azure Active Directory 단추](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="65ca7-201">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-201">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !["사용자 및 그룹" 및 "모든 사용자" 링크](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="65ca7-203">**사용자** 대화 상자를 열려면 **모든 사용자** 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-203">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![추가 단추](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="65ca7-205">**사용자** 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-205">In the **User** dialog box, perform the following steps:</span></span>

    ![사용자 대화 상자](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_04.png)

    <span data-ttu-id="65ca7-207">a.</span><span class="sxs-lookup"><span data-stu-id="65ca7-207">a.</span></span> <span data-ttu-id="65ca7-208">**이름** 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-208">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="65ca7-209">b.</span><span class="sxs-lookup"><span data-stu-id="65ca7-209">b.</span></span> <span data-ttu-id="65ca7-210">**사용자 이름** 상자에 사용자인 Britta Simon의 전자 메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-210">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="65ca7-211">c.</span><span class="sxs-lookup"><span data-stu-id="65ca7-211">c.</span></span> <span data-ttu-id="65ca7-212">**암호 표시** 확인란을 선택한 다음 **암호** 상자에 표시된 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-212">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="65ca7-213">d.</span><span class="sxs-lookup"><span data-stu-id="65ca7-213">d.</span></span> <span data-ttu-id="65ca7-214">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-214">Click **Create**.</span></span>
 
### <a name="create-a-mimecast-admin-console-test-user"></a><span data-ttu-id="65ca7-215">Mimecast 관리 콘솔 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="65ca7-215">Create a Mimecast Admin Console test user</span></span>

<span data-ttu-id="65ca7-216">Azure AD 사용자가 Mimecast 관리 콘솔에 로그인하려면 Mimecast 관리 콘솔에 프로비전해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-216">In order to enable Azure AD users to log into Mimecast Admin Console, they must be provisioned into Mimecast Admin Console.</span></span> <span data-ttu-id="65ca7-217">Mimecast 관리 콘솔의 경우 프로비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-217">In the case of Mimecast Admin Console, provisioning is a manual task.</span></span>

* <span data-ttu-id="65ca7-218">사용자를 만들려면 먼저 도메인을 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-218">You need to register a domain before you can create users.</span></span>

<span data-ttu-id="65ca7-219">**사용자 프로비전을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="65ca7-219">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="65ca7-220">**Mimecast 관리 콘솔** 에 관리자 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-220">Sign on to your **Mimecast Admin Console** as administrator.</span></span>
2. <span data-ttu-id="65ca7-221">**디렉터리 \> 내부**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-221">Go to **Directories \> Internal**.</span></span>
   
   <span data-ttu-id="65ca7-222">![디렉터리](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795003.png "디렉터리")</span><span class="sxs-lookup"><span data-stu-id="65ca7-222">![Directories](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795003.png "Directories")</span></span>
3. <span data-ttu-id="65ca7-223">**새 도메인에 등록**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-223">Click **Register New Domain**.</span></span>
   
   <span data-ttu-id="65ca7-224">![새 도메인에 등록](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795004.png "새 도메인에 등록")</span><span class="sxs-lookup"><span data-stu-id="65ca7-224">![Register New Domain](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795004.png "Register New Domain")</span></span>
4. <span data-ttu-id="65ca7-225">새 도메인을 만든 후 **새 주소**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-225">After your new domain has been created, click **New Address**.</span></span>
   
   <span data-ttu-id="65ca7-226">![새 주소](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795005.png "새 주소")</span><span class="sxs-lookup"><span data-stu-id="65ca7-226">![New Address](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795005.png "New Address")</span></span>
5. <span data-ttu-id="65ca7-227">새 주소 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-227">In the new address dialog, perform the following steps:</span></span>
   
   <span data-ttu-id="65ca7-228">![저장](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795006.png "저장")</span><span class="sxs-lookup"><span data-stu-id="65ca7-228">![Save](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795006.png "Save")</span></span>
   
   <span data-ttu-id="65ca7-229">a.</span><span class="sxs-lookup"><span data-stu-id="65ca7-229">a.</span></span> <span data-ttu-id="65ca7-230">관련된 텍스트 상자에 프로비전할 유효한 Azure AD 계정의 **이메일 주소**, **전역 이름**, **암호** 및 **암호 확인** 특성을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-230">Type the **Email Address**, **Global Name**, **Password**, and **Confirm Password** attributes of a valid Azure AD account you want to provision into the related textboxes.</span></span>

   <span data-ttu-id="65ca7-231">b.</span><span class="sxs-lookup"><span data-stu-id="65ca7-231">b.</span></span> <span data-ttu-id="65ca7-232">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-232">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="65ca7-233">Mimecast 관리 콘솔 사용자 계정 만들기 도구 또는 Mimecast 관리 콘솔에서 제공된 API를 사용하여 Azure AD 사용자 계정을 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-233">You can use any other Mimecast Admin Console user account creation tools or APIs provided by Mimecast Admin Console to provision Azure AD user accounts.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="65ca7-234">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="65ca7-234">Assign the Azure AD test user</span></span>

<span data-ttu-id="65ca7-235">이 섹션에서는 Britta Simon이 Azure Single Sign-On을 사용할 수 있도록 Mimecast 관리 콘솔에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-235">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Mimecast Admin Console.</span></span>

![사용자 역할 할당][200] 

<span data-ttu-id="65ca7-237">**Mimecast 관리 콘솔에 Britta Simon을 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="65ca7-237">**To assign Britta Simon to Mimecast Admin Console, perform the following steps:**</span></span>

1. <span data-ttu-id="65ca7-238">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-238">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="65ca7-240">응용 프로그램 목록에서 **Mimecast 관리 콘솔**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-240">In the applications list, select **Mimecast Admin Console**.</span></span>

    ![응용 프로그램 목록에서 Mimecast 관리 콘솔 링크](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_app.png)  

3. <span data-ttu-id="65ca7-242">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-242">In the menu on the left, click **Users and groups**.</span></span>

    !["사용자 및 그룹" 링크][202]

4. <span data-ttu-id="65ca7-244">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-244">Click **Add** button.</span></span> <span data-ttu-id="65ca7-245">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![할당 추가 창][203]

5. <span data-ttu-id="65ca7-247">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-247">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="65ca7-248">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="65ca7-249">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="65ca7-250">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="65ca7-250">Test single sign-on</span></span>

<span data-ttu-id="65ca7-251">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-251">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="65ca7-252">액세스 패널에서 Mimecast 관리 콘솔 타일을 클릭하면 Mimecast 관리 콘솔 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="65ca7-252">When you click the Mimecast Admin Console tile in the Access Panel, you should get automatically signed-on to your Mimecast Admin Console application.</span></span>
<span data-ttu-id="65ca7-253">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="65ca7-253">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="65ca7-254">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="65ca7-254">Additional resources</span></span>

* [<span data-ttu-id="65ca7-255">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="65ca7-255">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="65ca7-256">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="65ca7-256">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_203.png

