---
title: "자습서: ScreenSteps와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory 및 ScreenSteps 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 4563fe94-a88f-4895-a07f-79df44889cf9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jeedes
ms.openlocfilehash: b6ded8ba1adf03fdccbdb7573c09fae1857c8b16
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-screensteps"></a><span data-ttu-id="bc7bc-103">자습서: ScreenSteps와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="bc7bc-103">Tutorial: Azure Active Directory integration with ScreenSteps</span></span>

<span data-ttu-id="bc7bc-104">이 자습서에서는 Azure AD(Azure Active Directory)와 ScreenSteps를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-104">In this tutorial, you learn how to integrate ScreenSteps with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bc7bc-105">ScreenSteps를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-105">Integrating ScreenSteps with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="bc7bc-106">ScreenSteps에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-106">You can control in Azure AD who has access to ScreenSteps.</span></span>
- <span data-ttu-id="bc7bc-107">사용자가 해당 Azure AD 계정으로 ScreenSteps에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-107">You can enable your users to automatically get signed-on to ScreenSteps (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="bc7bc-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="bc7bc-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bc7bc-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="bc7bc-110">Prerequisites</span></span>

<span data-ttu-id="bc7bc-111">ScreenSteps와의 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-111">To configure Azure AD integration with ScreenSteps, you need the following items:</span></span>

- <span data-ttu-id="bc7bc-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="bc7bc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bc7bc-113">ScreenSteps Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="bc7bc-113">A ScreenSteps single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bc7bc-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bc7bc-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bc7bc-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bc7bc-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bc7bc-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="bc7bc-118">Scenario description</span></span>
<span data-ttu-id="bc7bc-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bc7bc-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bc7bc-121">갤러리에서 ScreenSteps 추가</span><span class="sxs-lookup"><span data-stu-id="bc7bc-121">Adding ScreenSteps from the gallery</span></span>
2. <span data-ttu-id="bc7bc-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="bc7bc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-screensteps-from-the-gallery"></a><span data-ttu-id="bc7bc-123">갤러리에서 ScreenSteps 추가</span><span class="sxs-lookup"><span data-stu-id="bc7bc-123">Adding ScreenSteps from the gallery</span></span>
<span data-ttu-id="bc7bc-124">ScreenSteps가 Azure AD에 통합되도록 구성하려면 갤러리에서 ScreenSteps를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-124">To configure the integration of ScreenSteps into Azure AD, you need to add ScreenSteps from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="bc7bc-125">**갤러리에서 ScreenSteps를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="bc7bc-125">**To add ScreenSteps from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="bc7bc-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory 단추][1]

2. <span data-ttu-id="bc7bc-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="bc7bc-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-129">Then go to **All applications**.</span></span>

    ![엔터프라이즈 응용 프로그램 블레이드][2]
    
3. <span data-ttu-id="bc7bc-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![새 응용 프로그램 단추][3]

4. <span data-ttu-id="bc7bc-133">검색 상자에 **ScreenSteps**를 입력하고 결과 패널에서 **ScreenSteps**를 선택한 후 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-133">In the search box, type **ScreenSteps**, select **ScreenSteps** from result panel then click **Add** button to add the application.</span></span>

    ![결과 목록의 ScreenSteps](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="bc7bc-135">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="bc7bc-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="bc7bc-136">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 ScreenSteps에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-136">In this section, you configure and test Azure AD single sign-on with ScreenSteps based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="bc7bc-137">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 ScreenSteps 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-137">For single sign-on to work, Azure AD needs to know what the counterpart user in ScreenSteps is to a user in Azure AD.</span></span> <span data-ttu-id="bc7bc-138">즉, Azure AD 사용자와 ScreenSteps의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-138">In other words, a link relationship between an Azure AD user and the related user in ScreenSteps needs to be established.</span></span>

<span data-ttu-id="bc7bc-139">ScreenSteps에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-139">In ScreenSteps, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="bc7bc-140">ScreenSteps에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-140">To configure and test Azure AD single sign-on with ScreenSteps, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="bc7bc-141">**[Azure AD Single Sign-On 구성](#configure-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="bc7bc-142">**[Azure AD 테스트 사용자 만들기](#create-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bc7bc-143">**[ScreenSteps 테스트 사용자 만들기](#create-a-screensteps-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 ScreenSteps에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-143">**[Create a ScreenSteps test user](#create-a-screensteps-test-user)** - to have a counterpart of Britta Simon in ScreenSteps that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="bc7bc-144">**[Azure AD 테스트 사용자 할당](#assign-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bc7bc-145">**[Single Sign-On 테스트](#test-single-sign-on)** - 구성이 작동하는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="bc7bc-146">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="bc7bc-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="bc7bc-147">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 ScreenSteps 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ScreenSteps application.</span></span>

<span data-ttu-id="bc7bc-148">**ScreenSteps에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="bc7bc-148">**To configure Azure AD single sign-on with ScreenSteps, perform the following steps:**</span></span>

1. <span data-ttu-id="bc7bc-149">Azure Portal의 **ScreenSteps** 응용 프로그램 통합 페이지에서 **Single sign-on**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-149">In the Azure portal, on the **ScreenSteps** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-On 구성 링크][4]

2. <span data-ttu-id="bc7bc-151">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_samlbase.png)

3. <span data-ttu-id="bc7bc-153">**ScreenSteps 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-153">On the **ScreenSteps Domain and URLs** section, perform the following steps:</span></span>

    ![ScreenSteps 도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_url.png)

    <span data-ttu-id="bc7bc-155">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<tenantname>.ScreenSteps.com`</span><span class="sxs-lookup"><span data-stu-id="bc7bc-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenantname>.ScreenSteps.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="bc7bc-156">이 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-156">This value is not real.</span></span> <span data-ttu-id="bc7bc-157">자습서 뒷부분에 설명된 실제 로그온 URL로 이 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-157">Update this value with the actual Sign-On URL, which is explained later in this tutorial.</span></span> 

4. <span data-ttu-id="bc7bc-158">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-158">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![인증서 다운로드 링크](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_certificate.png) 

5. <span data-ttu-id="bc7bc-160">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-160">Click **Save** button.</span></span>

    ![Single Sign-On 구성 저장 단추](./media/active-directory-saas-screensteps-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="bc7bc-162">**ScreenSteps 구성** 섹션에서 **ScreenSteps 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-162">On the **ScreenSteps Configuration** section, click **Configure ScreenSteps** to open **Configure sign-on** window.</span></span> <span data-ttu-id="bc7bc-163">**빠른 참조 섹션**에서 **로그아웃 URL 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-163">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![ScreenSteps 구성](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_configure.png) 

7. <span data-ttu-id="bc7bc-165">다른 웹 브라우저 창에서 ScreenSteps 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-165">In a different web browser window, log into your ScreenSteps company site as an administrator.</span></span>

8. <span data-ttu-id="bc7bc-166">**계정 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-166">Click **Account Settings**.</span></span>

    <span data-ttu-id="bc7bc-167">![계정 관리](./media/active-directory-saas-screensteps-tutorial/ic778523.png "계정 관리")</span><span class="sxs-lookup"><span data-stu-id="bc7bc-167">![Account management](./media/active-directory-saas-screensteps-tutorial/ic778523.png "Account management")</span></span>

9. <span data-ttu-id="bc7bc-168">**Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-168">Click **Single Sign-on**.</span></span>

    <span data-ttu-id="bc7bc-169">![원격 인증](./media/active-directory-saas-screensteps-tutorial/ic778524.png "원격 인증")</span><span class="sxs-lookup"><span data-stu-id="bc7bc-169">![Remote authentication](./media/active-directory-saas-screensteps-tutorial/ic778524.png "Remote authentication")</span></span>

10. <span data-ttu-id="bc7bc-170">**Single Sign-on 끝점 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-170">Click **Create Single Sign-on Endpoint**.</span></span>

    <span data-ttu-id="bc7bc-171">![원격 인증](./media/active-directory-saas-screensteps-tutorial/ic778525.png "원격 인증")</span><span class="sxs-lookup"><span data-stu-id="bc7bc-171">![Remote authentication](./media/active-directory-saas-screensteps-tutorial/ic778525.png "Remote authentication")</span></span>

11. <span data-ttu-id="bc7bc-172">**Single Sign-on 끝점 만들기** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-172">In the **Create Single Sign-on Endpoint** section, perform the following steps:</span></span>

    <span data-ttu-id="bc7bc-173">![인증 끝점 만들기](./media/active-directory-saas-screensteps-tutorial/ic778526.png "인증 끝점 만들기")</span><span class="sxs-lookup"><span data-stu-id="bc7bc-173">![Create an authentication endpoint](./media/active-directory-saas-screensteps-tutorial/ic778526.png "Create an authentication endpoint")</span></span>
    
    <span data-ttu-id="bc7bc-174">a.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-174">a.</span></span> <span data-ttu-id="bc7bc-175">**제목** 텍스트 상자에 제목을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-175">In the **Title** textbox, type a title.</span></span>
    
    <span data-ttu-id="bc7bc-176">b.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-176">b.</span></span> <span data-ttu-id="bc7bc-177">**모드** 목록에서 **SAML**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-177">From the **Mode** list, select **SAML**.</span></span>
    
    <span data-ttu-id="bc7bc-178">c.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-178">c.</span></span> <span data-ttu-id="bc7bc-179">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-179">Click **Create**.</span></span>

12. <span data-ttu-id="bc7bc-180">새 끝점을 **편집**합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-180">**Edit** the new endpoint.</span></span>

    <span data-ttu-id="bc7bc-181">![끝점 편집](./media/active-directory-saas-screensteps-tutorial/ic778528.png "끝점 편집")</span><span class="sxs-lookup"><span data-stu-id="bc7bc-181">![Edit endpoint](./media/active-directory-saas-screensteps-tutorial/ic778528.png "Edit endpoint")</span></span>

13. <span data-ttu-id="bc7bc-182">**Single Sign-on 끝점 편집** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-182">In the **Edit Single Sign-on Endpoint** section, perform the following steps:</span></span>

    <span data-ttu-id="bc7bc-183">![원격 인증 끝점](./media/active-directory-saas-screensteps-tutorial/ic778527.png "원격 인증 끝점")</span><span class="sxs-lookup"><span data-stu-id="bc7bc-183">![Remote authentication endpoint](./media/active-directory-saas-screensteps-tutorial/ic778527.png "Remote authentication endpoint")</span></span>

    <span data-ttu-id="bc7bc-184">a.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-184">a.</span></span> <span data-ttu-id="bc7bc-185">**새 SAML 인증서 파일 업로드**를 클릭한 후 Azure Portal에서 다운로드한 인증서를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-185">Click **Upload new SAML Certificate file**, and then upload the certificate, which you have downloaded from Azure portal.</span></span>
    
    <span data-ttu-id="bc7bc-186">b.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-186">b.</span></span> <span data-ttu-id="bc7bc-187">Azure Portal에서 복사한 **SAML Single Sign-On 서비스 URL** 값을 **원격 로그인 URL** 텍스트 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-187">Paste **SAML Single Sign-On Service URL** value, which you have copied from the Azure portal into the **Remote Login URL** textbox.</span></span>
    
    <span data-ttu-id="bc7bc-188">c.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-188">c.</span></span> <span data-ttu-id="bc7bc-189">Azure Portal에서 복사한 **로그아웃 URL** 값을 **로그아웃 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-189">Paste **Sign-Out URL** value, which you have copied from the Azure portal into the **Log out URL** textbox.</span></span>
    
    <span data-ttu-id="bc7bc-190">d.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-190">d.</span></span> <span data-ttu-id="bc7bc-191">사용자가 프로비전될 때 사용자를 할당할 **그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-191">Select a **Group** to assign users to when they are provisioned.</span></span>
    
    <span data-ttu-id="bc7bc-192">e.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-192">e.</span></span> <span data-ttu-id="bc7bc-193">**업데이트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-193">Click **Update**.</span></span>

    <span data-ttu-id="bc7bc-194">f.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-194">f.</span></span> <span data-ttu-id="bc7bc-195">**SAML 소비자 URL**을 클립보드로 복사하여 **ScreenSteps 도메인 및 URL** 섹션의 **로그온 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-195">Copy the **SAML Consumer URL** to the clipboard and paste in to the **Sign-on URL** textbox in **ScreenSteps Domain and URLs** section.</span></span>
    
    <span data-ttu-id="bc7bc-196">g.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-196">g.</span></span> <span data-ttu-id="bc7bc-197">**Single Sign-On 끝점 편집**으로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-197">Return to the **Edit Single Sign-on Endpoint**.</span></span>
    
    <span data-ttu-id="bc7bc-198">h.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-198">h.</span></span> <span data-ttu-id="bc7bc-199">**계정의 기본값으로 지정** 단추를 클릭하여 ScreenSteps에 로그온하는 모든 사용자에 대해 이 끝점을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-199">Click the **Make default for account** button to use this endpoint for all users who log into ScreenSteps.</span></span> <span data-ttu-id="bc7bc-200">또는 **사이트에 추가** 단추를 클릭하여 이 끝점을 **ScreenSteps**의 특정 사이트에 대해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-200">Alternatively you can click the **Add to Site** button to use this endpoint for specific sites in **ScreenSteps**.</span></span>

> [!TIP]
> <span data-ttu-id="bc7bc-201">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-201">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="bc7bc-202">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-202">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="bc7bc-203">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-203">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="bc7bc-204">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="bc7bc-204">Create an Azure AD test user</span></span>

<span data-ttu-id="bc7bc-205">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-205">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Azure AD 테스트 사용자 만들기][100]

<span data-ttu-id="bc7bc-207">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="bc7bc-207">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="bc7bc-208">Azure Portal의 왼쪽 창에서 **Azure Active Directory** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-208">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Azure Active Directory 단추](./media/active-directory-saas-screensteps-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="bc7bc-210">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-210">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !["사용자 및 그룹" 및 "모든 사용자" 링크](./media/active-directory-saas-screensteps-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="bc7bc-212">**사용자** 대화 상자를 열려면 **모든 사용자** 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-212">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![추가 단추](./media/active-directory-saas-screensteps-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="bc7bc-214">**사용자** 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-214">In the **User** dialog box, perform the following steps:</span></span>

    ![사용자 대화 상자](./media/active-directory-saas-screensteps-tutorial/create_aaduser_04.png)

    <span data-ttu-id="bc7bc-216">a.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-216">a.</span></span> <span data-ttu-id="bc7bc-217">**이름** 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-217">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bc7bc-218">b.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-218">b.</span></span> <span data-ttu-id="bc7bc-219">**사용자 이름** 상자에 사용자인 Britta Simon의 전자 메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-219">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="bc7bc-220">c.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-220">c.</span></span> <span data-ttu-id="bc7bc-221">**암호 표시** 확인란을 선택한 다음 **암호** 상자에 표시된 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-221">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="bc7bc-222">d.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-222">d.</span></span> <span data-ttu-id="bc7bc-223">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-223">Click **Create**.</span></span>
 
### <a name="create-a-screensteps-test-user"></a><span data-ttu-id="bc7bc-224">ScreenSteps 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="bc7bc-224">Create a ScreenSteps test user</span></span>

<span data-ttu-id="bc7bc-225">이 섹션에서는 ScreenSteps에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-225">In this section, you create a user called Britta Simon in ScreenSteps.</span></span> <span data-ttu-id="bc7bc-226">ScreenSteps 플랫폼에서 사용자를 추가하려면 [ScreenSteps 클라이언트 지원 팀](https://www.screensteps.com/contact)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-226">Work with [ScreenSteps Client support team](https://www.screensteps.com/contact) to add the users in the ScreenSteps platform.</span></span> <span data-ttu-id="bc7bc-227">Single Sign-On을 사용하려면 먼저 사용자를 만들고 활성화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-227">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="bc7bc-228">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="bc7bc-228">Assign the Azure AD test user</span></span>

<span data-ttu-id="bc7bc-229">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 ScreenSteps에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-229">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ScreenSteps.</span></span>

![사용자 역할 할당][200] 

<span data-ttu-id="bc7bc-231">**Britta Simon을 ScreenSteps에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="bc7bc-231">**To assign Britta Simon to ScreenSteps, perform the following steps:**</span></span>

1. <span data-ttu-id="bc7bc-232">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-232">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="bc7bc-234">응용 프로그램 목록에서 **ScreenSteps**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-234">In the applications list, select **ScreenSteps**.</span></span>

    ![응용 프로그램 목록의 ScreenSteps 링크](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_app.png)  

3. <span data-ttu-id="bc7bc-236">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-236">In the menu on the left, click **Users and groups**.</span></span>

    !["사용자 및 그룹" 링크][202]

4. <span data-ttu-id="bc7bc-238">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-238">Click **Add** button.</span></span> <span data-ttu-id="bc7bc-239">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![할당 추가 창][203]

5. <span data-ttu-id="bc7bc-241">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-241">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="bc7bc-242">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bc7bc-243">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="bc7bc-244">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="bc7bc-244">Test single sign-on</span></span>

<span data-ttu-id="bc7bc-245">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-245">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="bc7bc-246">액세스 패널에서 ScreenSteps 타일을 클릭하면 ScreenSteps 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-246">When you click the ScreenSteps tile in the Access Panel, you should get automatically signed-on to your ScreenSteps application.</span></span>
<span data-ttu-id="bc7bc-247">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bc7bc-247">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="bc7bc-248">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="bc7bc-248">Additional resources</span></span>

* [<span data-ttu-id="bc7bc-249">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="bc7bc-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bc7bc-250">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="bc7bc-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_203.png

