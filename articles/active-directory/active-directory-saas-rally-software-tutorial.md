---
title: "자습서: Rally Software와 Azure Active Directory 통합| Microsoft Azure"
description: "Azure Active Directory 및 Rally Software 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ba25fade-e152-42dd-8377-a30bbc48c3ed
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: jeedes
ms.openlocfilehash: 6481c9ef0ca71419ccfa6f7956f4702985743df3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rally-software"></a><span data-ttu-id="30c9d-103">자습서: Rally Software와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="30c9d-103">Tutorial: Azure Active Directory integration with Rally Software</span></span>

<span data-ttu-id="30c9d-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Rally Software를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-104">In this tutorial, you learn how to integrate Rally Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="30c9d-105">Rally Software를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-105">Integrating Rally Software with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="30c9d-106">Rally Software에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-106">You can control in Azure AD who has access to Rally Software.</span></span>
- <span data-ttu-id="30c9d-107">사용자가 해당 Azure AD 계정으로 Rally Software에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-107">You can enable your users to automatically get signed-on to Rally Software (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="30c9d-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="30c9d-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="30c9d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="30c9d-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="30c9d-110">Prerequisites</span></span>

<span data-ttu-id="30c9d-111">Rally Software와의 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-111">To configure Azure AD integration with Rally Software, you need the following items:</span></span>

- <span data-ttu-id="30c9d-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="30c9d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="30c9d-113">Rally Software Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="30c9d-113">A Rally Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="30c9d-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="30c9d-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="30c9d-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="30c9d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="30c9d-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="30c9d-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="30c9d-118">Scenario description</span></span>
<span data-ttu-id="30c9d-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="30c9d-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="30c9d-121">갤러리에서 Rally Software 추가</span><span class="sxs-lookup"><span data-stu-id="30c9d-121">Adding Rally Software from the gallery</span></span>
2. <span data-ttu-id="30c9d-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="30c9d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-rally-software-from-the-gallery"></a><span data-ttu-id="30c9d-123">갤러리에서 Rally Software 추가</span><span class="sxs-lookup"><span data-stu-id="30c9d-123">Adding Rally Software from the gallery</span></span>
<span data-ttu-id="30c9d-124">Rally Software의 Azure AD 통합을 구성하려면 갤러리의 Rally Software를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-124">To configure the integration of Rally Software into Azure AD, you need to add Rally Software from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="30c9d-125">**갤러리에서 Rally Software를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="30c9d-125">**To add Rally Software from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="30c9d-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory 단추][1]

2. <span data-ttu-id="30c9d-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="30c9d-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-129">Then go to **All applications**.</span></span>

    ![엔터프라이즈 응용 프로그램 블레이드][2]
    
3. <span data-ttu-id="30c9d-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![새 응용 프로그램 단추][3]

4. <span data-ttu-id="30c9d-133">검색 상자에 **Rally Software**를 입력하고 결과 패널에서 **Rally Software**를 선택한 후 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-133">In the search box, type **Rally Software**, select **Rally Software** from result panel then click **Add** button to add the application.</span></span>

    ![결과 목록의 Rally Software](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="30c9d-135">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="30c9d-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="30c9d-136">이 섹션에서는 “Britta Simon”이라는 테스트 사용자를 기반으로 Rally Software에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-136">In this section, you configure and test Azure AD single sign-on with Rally Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="30c9d-137">Single Sign-On이 작동하려면 Azure AD에서 Azure AD의 사용자에 해당하는 Rally Software의 사용자가 누군지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Rally Software is to a user in Azure AD.</span></span> <span data-ttu-id="30c9d-138">즉, Azure AD 사용자와 Rally Software의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-138">In other words, a link relationship between an Azure AD user and the related user in Rally Software needs to be established.</span></span>

<span data-ttu-id="30c9d-139">Rally Software에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-139">In Rally Software, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="30c9d-140">Rally Software에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-140">To configure and test Azure AD single sign-on with Rally Software, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="30c9d-141">**[Azure AD Single Sign-On 구성](#configure-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="30c9d-142">**[Azure AD 테스트 사용자 만들기](#create-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="30c9d-143">**[Rally Software 테스트 사용자 만들기](#create-a-rally-software-test-user)** - Britta Simon의 Azure AD 사용자 표현과 연결되는 대응 사용자를 Rally Software에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-143">**[Create a Rally Software test user](#create-a-rally-software-test-user)** - to have a counterpart of Britta Simon in Rally Software that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="30c9d-144">**[Azure AD 테스트 사용자 할당](#assign-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="30c9d-145">**[Single Sign-On 테스트](#test-single-sign-on)** - 구성이 작동하는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="30c9d-146">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="30c9d-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="30c9d-147">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Rally Software 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Rally Software application.</span></span>

<span data-ttu-id="30c9d-148">**Rally Software에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="30c9d-148">**To configure Azure AD single sign-on with Rally Software, perform the following steps:**</span></span>

1. <span data-ttu-id="30c9d-149">Azure Portal의 **Rally Software** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-149">In the Azure portal, on the **Rally Software** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-On 구성 링크][4]

2. <span data-ttu-id="30c9d-151">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_samlbase.png)

3. <span data-ttu-id="30c9d-153">**Rally Software 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-153">On the **Rally Software Domain and URLs** section, perform the following steps:</span></span>

    ![Rally Software 도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_url.png)

    <span data-ttu-id="30c9d-155">a.</span><span class="sxs-lookup"><span data-stu-id="30c9d-155">a.</span></span> <span data-ttu-id="30c9d-156">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<tenant-name>.rally.com`</span><span class="sxs-lookup"><span data-stu-id="30c9d-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.rally.com`</span></span>

    <span data-ttu-id="30c9d-157">b.</span><span class="sxs-lookup"><span data-stu-id="30c9d-157">b.</span></span> <span data-ttu-id="30c9d-158">**식별자** 텍스트 상자에서 `https://<tenant-name>.rally.com` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenant-name>.rally.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="30c9d-159">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-159">These values are not real.</span></span> <span data-ttu-id="30c9d-160">실제 로그온 URL 및 식별자로 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="30c9d-161">이러한 값을 얻으려면 [Rally Software 클라이언트 지원 팀](https://help.rallydev.com/)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="30c9d-161">Contact [Rally Software Client support team](https://help.rallydev.com/) to get these values.</span></span> 
 


4. <span data-ttu-id="30c9d-162">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 메타데이터 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![인증서 다운로드 링크](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_certificate.png) 

5. <span data-ttu-id="30c9d-164">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-164">Click **Save** button.</span></span>

    ![Single Sign-On 구성 저장 단추](./media/active-directory-saas-rally-software-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="30c9d-166">**Rally Software 구성** 섹션에서 **Rally Software 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-166">On the **Rally Software Configuration** section, click **Configure Rally Software** to open **Configure sign-on** window.</span></span> <span data-ttu-id="30c9d-167">**빠른 참조** 섹션에서 **로그아웃 URL 및 SAML 엔터티 ID**를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-167">Copy the **Sign-Out URL, and SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Rally 소프트웨어 구성](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_configure.png) 

7. <span data-ttu-id="30c9d-169">**Rally Software** 테넌트에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-169">Log in to your **Rally Software** tenant.</span></span>

8. <span data-ttu-id="30c9d-170">위쪽의 도구 모음에서 **설정**을 클릭한 다음 **구독**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-170">In the toolbar on the top, click **Setup**, and then select **Subscription**.</span></span>
   
    <span data-ttu-id="30c9d-171">![구독](./media/active-directory-saas-rally-software-tutorial/ic769531.png "구독")</span><span class="sxs-lookup"><span data-stu-id="30c9d-171">![Subscription](./media/active-directory-saas-rally-software-tutorial/ic769531.png "Subscription")</span></span>

9. <span data-ttu-id="30c9d-172">**작업** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-172">Click the **Action** button.</span></span> <span data-ttu-id="30c9d-173">도구 모음 맨 위 오른쪽에서 **구독 편집**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-173">Select **Edit Subscription** at the top right side of the toolbar.</span></span>

10. <span data-ttu-id="30c9d-174">**구독** 대화 상자 페이지에서 다음 단계를 수행하고 **저장 및 닫기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-174">On the **Subscription** dialog page, perform the following steps, and then click **Save & Close**:</span></span>
   
    <span data-ttu-id="30c9d-175">![인증](./media/active-directory-saas-rally-software-tutorial/ic769542.png "인증")</span><span class="sxs-lookup"><span data-stu-id="30c9d-175">![Authentication](./media/active-directory-saas-rally-software-tutorial/ic769542.png "Authentication")</span></span>
   
    <span data-ttu-id="30c9d-176">a.</span><span class="sxs-lookup"><span data-stu-id="30c9d-176">a.</span></span> <span data-ttu-id="30c9d-177">인증 드롭다운에서 **Rally 또는 SSO 인증**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-177">Select **Rally or SSO authentication** from Authentication dropdown.</span></span>

    <span data-ttu-id="30c9d-178">b.</span><span class="sxs-lookup"><span data-stu-id="30c9d-178">b.</span></span> <span data-ttu-id="30c9d-179">Azure Portal에서 복사한 **SAML 엔터티 ID** 값을 **ID 공급자 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-179">In the **Identity provider URL** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="30c9d-180">c.</span><span class="sxs-lookup"><span data-stu-id="30c9d-180">c.</span></span> <span data-ttu-id="30c9d-181">Azure Portal에서 복사한 **로그아웃 URL** 값을 **SSO 로그아웃** 텍스트 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-181">In the **SSO Logout** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

> [!TIP]
> <span data-ttu-id="30c9d-182">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-182">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="30c9d-183">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-183">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="30c9d-184">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-184">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="30c9d-185">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="30c9d-185">Create an Azure AD test user</span></span>

<span data-ttu-id="30c9d-186">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-186">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Azure AD 테스트 사용자 만들기][100]

<span data-ttu-id="30c9d-188">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="30c9d-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="30c9d-189">Azure Portal의 왼쪽 창에서 **Azure Active Directory** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-189">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Azure Active Directory 단추](./media/active-directory-saas-rally-software-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="30c9d-191">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-191">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !["사용자 및 그룹" 및 "모든 사용자" 링크](./media/active-directory-saas-rally-software-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="30c9d-193">**사용자** 대화 상자를 열려면 **모든 사용자** 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-193">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![추가 단추](./media/active-directory-saas-rally-software-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="30c9d-195">**사용자** 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-195">In the **User** dialog box, perform the following steps:</span></span>

    ![사용자 대화 상자](./media/active-directory-saas-rally-software-tutorial/create_aaduser_04.png)

    <span data-ttu-id="30c9d-197">a.</span><span class="sxs-lookup"><span data-stu-id="30c9d-197">a.</span></span> <span data-ttu-id="30c9d-198">**이름** 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-198">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="30c9d-199">b.</span><span class="sxs-lookup"><span data-stu-id="30c9d-199">b.</span></span> <span data-ttu-id="30c9d-200">**사용자 이름** 상자에 사용자인 Britta Simon의 전자 메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-200">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="30c9d-201">c.</span><span class="sxs-lookup"><span data-stu-id="30c9d-201">c.</span></span> <span data-ttu-id="30c9d-202">**암호 표시** 확인란을 선택한 다음 **암호** 상자에 표시된 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-202">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="30c9d-203">d.</span><span class="sxs-lookup"><span data-stu-id="30c9d-203">d.</span></span> <span data-ttu-id="30c9d-204">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-204">Click **Create**.</span></span>
 
### <a name="create-a-rally-software-test-user"></a><span data-ttu-id="30c9d-205">Rally Software 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="30c9d-205">Create a Rally Software test user</span></span>

<span data-ttu-id="30c9d-206">Azure AD 사용자가 로그인할 수 있도록 Azure Active Directory 사용자 이름을 사용하여 Rally Software 응용 프로그램에 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-206">For Azure AD users to be able to sign in, they must be provisioned to the Rally Software application using their Azure Active Directory user names.</span></span>

<span data-ttu-id="30c9d-207">**사용자 프로비전을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="30c9d-207">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="30c9d-208">Rally Software 테넌트에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-208">Log in to your Rally Software tenant.</span></span>

2. <span data-ttu-id="30c9d-209">**설정 \> 사용자**를 클릭한 후 **+ 새 사용자 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-209">Go to **Setup \> USERS**, and then click **+ Add New**.</span></span>
   
    <span data-ttu-id="30c9d-210">![사용자](./media/active-directory-saas-rally-software-tutorial/ic781039.png "사용자")</span><span class="sxs-lookup"><span data-stu-id="30c9d-210">![Users](./media/active-directory-saas-rally-software-tutorial/ic781039.png "Users")</span></span>

3. <span data-ttu-id="30c9d-211">이름을 새 사용자 텍스트 상자에 입력한 다음 **세부 정보 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-211">Type the name in the New User textbox, and then click **Add with Details**.</span></span>

4. <span data-ttu-id="30c9d-212">**사용자 만들기** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-212">In the **Create User** section, perform the following steps:</span></span>
   
    <span data-ttu-id="30c9d-213">![사용자 만들기](./media/active-directory-saas-rally-software-tutorial/ic781040.png "사용자 만들기")</span><span class="sxs-lookup"><span data-stu-id="30c9d-213">![Create User](./media/active-directory-saas-rally-software-tutorial/ic781040.png "Create User")</span></span>

    <span data-ttu-id="30c9d-214">a.</span><span class="sxs-lookup"><span data-stu-id="30c9d-214">a.</span></span> <span data-ttu-id="30c9d-215">**사용자 이름** 텍스트 상자에 사용자 이름(예: **Brittsimon**)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-215">In the **User Name** textbox, type the name of user like **Brittsimon**.</span></span>
   
    <span data-ttu-id="30c9d-216">b.</span><span class="sxs-lookup"><span data-stu-id="30c9d-216">b.</span></span> <span data-ttu-id="30c9d-217">**전자 메일 주소** 텍스트 상자에 **brittasimon@contoso.com**과 같은 사용자의 메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-217">In **E-mail Address** textbox, enter the email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="30c9d-218">c.</span><span class="sxs-lookup"><span data-stu-id="30c9d-218">c.</span></span> <span data-ttu-id="30c9d-219">**이름** 텍스트 상자에 사용자의 이름(예: **Britta**)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-219">In **First Name** text box, enter the first name of user like **Britta**.</span></span>

    <span data-ttu-id="30c9d-220">d.</span><span class="sxs-lookup"><span data-stu-id="30c9d-220">d.</span></span> <span data-ttu-id="30c9d-221">**성** 텍스트 상자에 사용자의 성(예: **Simon**)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-221">In **Last Name** text box, enter the last name of user like **Simon**.</span></span>

    <span data-ttu-id="30c9d-222">e.</span><span class="sxs-lookup"><span data-stu-id="30c9d-222">e.</span></span> <span data-ttu-id="30c9d-223">**저장 후 닫기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-223">Click **Save & Close**.</span></span>

   >[!NOTE]
   ><span data-ttu-id="30c9d-224">다른 Rally Software 사용자 계정 생성 도구 또는 Rally Software가 제공한 API를 사용하여 Azure AD 사용자 계정을 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-224">You can use any other Rally Software user account creation tools or APIs provided by Rally Software to provision Azure AD user accounts.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="30c9d-225">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="30c9d-225">Assign the Azure AD test user</span></span>

<span data-ttu-id="30c9d-226">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Rally Software에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Rally Software.</span></span>

![사용자 역할 할당][200] 

<span data-ttu-id="30c9d-228">**Britta Simon을 Rally Software에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="30c9d-228">**To assign Britta Simon to Rally Software, perform the following steps:**</span></span>

1. <span data-ttu-id="30c9d-229">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-229">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="30c9d-231">응용 프로그램 목록에서 **Rally Software**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-231">In the applications list, select **Rally Software**.</span></span>

    ![응용 프로그램 목록의 Rally Software 링크](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_app.png)  

3. <span data-ttu-id="30c9d-233">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-233">In the menu on the left, click **Users and groups**.</span></span>

    !["사용자 및 그룹" 링크][202]

4. <span data-ttu-id="30c9d-235">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-235">Click **Add** button.</span></span> <span data-ttu-id="30c9d-236">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![할당 추가 창][203]

5. <span data-ttu-id="30c9d-238">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="30c9d-239">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="30c9d-240">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="30c9d-241">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="30c9d-241">Test single sign-on</span></span>

<span data-ttu-id="30c9d-242">이 섹션은 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-242">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="30c9d-243">액세스 패널에서 Rally Software 타일을 클릭하면 Rally Software 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="30c9d-243">When you click the Rally Software tile in the Access Panel, you should get automatically signed-on to your Rally Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="30c9d-244">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="30c9d-244">Additional resources</span></span>

* [<span data-ttu-id="30c9d-245">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="30c9d-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="30c9d-246">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="30c9d-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_203.png

