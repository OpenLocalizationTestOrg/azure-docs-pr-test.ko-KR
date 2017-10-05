---
title: "자습서: Workday와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 Workday 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e9da692e-4a65-4231-8ab3-bc9a87b10bca
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 164d5c644f120fa86e2b690649241892764b64b7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workday"></a><span data-ttu-id="d716f-103">자습서: Workday와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="d716f-103">Tutorial: Azure Active Directory integration with Workday</span></span>

<span data-ttu-id="d716f-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Workday를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-104">In this tutorial, you learn how to integrate Workday with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d716f-105">Workday를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-105">Integrating Workday with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d716f-106">Workday에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-106">You can control in Azure AD who has access to Workday</span></span>
- <span data-ttu-id="d716f-107">사용자가 자신의 Azure AD 계정으로 Workday에 자동으로 로그온(Single Sign-On) 되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-107">You can enable your users to automatically get signed-on to Workday (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d716f-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d716f-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d716f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d716f-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d716f-110">Prerequisites</span></span>

<span data-ttu-id="d716f-111">Workday와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-111">To configure Azure AD integration with Workday, you need the following items:</span></span>

- <span data-ttu-id="d716f-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="d716f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d716f-113">Workday Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="d716f-113">A Workday single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d716f-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d716f-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d716f-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="d716f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d716f-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d716f-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="d716f-118">Scenario description</span></span>
<span data-ttu-id="d716f-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d716f-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d716f-121">갤러리에서 Workday 추가</span><span class="sxs-lookup"><span data-stu-id="d716f-121">Adding Workday from the gallery</span></span>
2. <span data-ttu-id="d716f-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="d716f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workday-from-the-gallery"></a><span data-ttu-id="d716f-123">갤러리에서 Workday 추가</span><span class="sxs-lookup"><span data-stu-id="d716f-123">Adding Workday from the gallery</span></span>
<span data-ttu-id="d716f-124">Workday가 Azure AD에 통합되도록 구성하려면 갤러리에서 Workday를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-124">To configure the integration of Workday into Azure AD, you need to add Workday from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d716f-125">**갤러리에서 Workday를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="d716f-125">**To add Workday from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d716f-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d716f-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d716f-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="d716f-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="d716f-133">검색 상자에 **Workday**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-133">In the search box, type **Workday**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-workday-tutorial/tutorial_workday_search.png)

5. <span data-ttu-id="d716f-135">결과 창에서 **Workday**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-135">In the results panel, select **Workday**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-workday-tutorial/tutorial_workday_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d716f-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="d716f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d716f-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Workday에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-138">In this section, you configure and test Azure AD single sign-on with Workday based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d716f-139">Single Sign-On이 작동하려면 Azure AD 사용자에 해당하는 Workday 사용자가 누구인지 Azure AD에서 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Workday is to a user in Azure AD.</span></span> <span data-ttu-id="d716f-140">즉, Azure AD 사용자와 Workday의 관련 사용자 간에 링크 관계가 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-140">In other words, a link relationship between an Azure AD user and the related user in Workday needs to be established.</span></span>

<span data-ttu-id="d716f-141">이 링크 관계는 Azure AD의 **사용자 이름** 값을 Workday의 **Username** 값으로 할당하여 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Workday.</span></span>

<span data-ttu-id="d716f-142">Workday에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-142">To configure and test Azure AD single sign-on with Workday, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d716f-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d716f-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d716f-145">**[Workday 테스트 사용자 만들기](#creating-a-workday-test-user)** - Britta Simon의 Azure AD 표현과 연결되는 대응 사용자를 Workday에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-145">**[Creating a Workday test user](#creating-a-workday-test-user)** - to have a counterpart of Britta Simon in Workday that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d716f-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d716f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d716f-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="d716f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d716f-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Workday 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Workday application.</span></span>

<span data-ttu-id="d716f-150">**Workday에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="d716f-150">**To configure Azure AD single sign-on with Workday, perform the following steps:**</span></span>

1. <span data-ttu-id="d716f-151">Azure Portal의 **Workday** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-151">In the Azure portal, on the **Workday** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="d716f-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-workday-tutorial/tutorial_workday_samlbase.png)

3. <span data-ttu-id="d716f-155">**Workday 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-155">On the **Workday Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-workday-tutorial/tutorial_workday_url.png)

    <span data-ttu-id="d716f-157">a.</span><span class="sxs-lookup"><span data-stu-id="d716f-157">a.</span></span> <span data-ttu-id="d716f-158">**로그인 URL** 텍스트 상자에서 값으로 `https://impl.workday.com/<tenant>/login-saml2.htmld`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-158">In the **Sign-on URL** textbox, type the value as: `https://impl.workday.com/<tenant>/login-saml2.htmld`</span></span>

    <span data-ttu-id="d716f-159">b.</span><span class="sxs-lookup"><span data-stu-id="d716f-159">b.</span></span> <span data-ttu-id="d716f-160">**회신 URL** 텍스트 상자에 다음 패턴으로 URL을 입력합니다.`https://impl.workday.com/<tenant>/login-saml.htmld`</span><span class="sxs-lookup"><span data-stu-id="d716f-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://impl.workday.com/<tenant>/login-saml.htmld`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d716f-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-161">These values are not the real.</span></span> <span data-ttu-id="d716f-162">실제 로그온 URL 및 회신 URL을 사용하여 이러한 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-162">Update these values with the actual Sign-on URL and Reply URL.</span></span> <span data-ttu-id="d716f-163">회신 URL에 하위 도메인(예: www, wd2, wd3, wd3-impl, wd5, wd5-impl)이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-163">Your reply URL must have a subdomain for example: www, wd2, wd3, wd3-impl, wd5, wd5-impl).</span></span> <span data-ttu-id="d716f-164">"*http://www.myworkday.com*"과 같은 것은 작동하지만 "*http://myworkday.com*"은 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-164">Using something like "*http://www.myworkday.com*" works but "*http://myworkday.com*" does not.</span></span> <span data-ttu-id="d716f-165">이러한 값을 얻으려면 [Workday 클라이언트 지원 팀](https://www.workday.com/en-us/partners-services/services/support.html)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="d716f-165">Contact [Workday Client support team](https://www.workday.com/en-us/partners-services/services/support.html) to get these values.</span></span> 
 

4. <span data-ttu-id="d716f-166">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-166">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-workday-tutorial/tutorial_workday_certificate.png) 

5. <span data-ttu-id="d716f-168">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-168">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-workday-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d716f-170">**Workday 구성** 섹션에서 **Workday 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-170">On the **Workday Configuration** section, click **Configure Workday** to open **Configure sign-on** window.</span></span> <span data-ttu-id="d716f-171">**빠른 참조 섹션**에서 **로그아웃 URL, SAML 엔터티 ID 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-171">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    <span data-ttu-id="d716f-172">![Single Sign-On 구성](./media/active-directory-saas-workday-tutorial/tutorial_workday_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="d716f-172">![Configure Single Sign-On](./media/active-directory-saas-workday-tutorial/tutorial_workday_configure.png) 
<CS></span></span>
7. <span data-ttu-id="d716f-173">다른 웹 브라우저 창에서 Workday 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-173">In a different web browser window, log in to your Workday company site as an administrator.</span></span>

8. <span data-ttu-id="d716f-174">**메뉴 \> 워크벤치**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-174">Go to **Menu \> Workbench**.</span></span>
   
    <span data-ttu-id="d716f-175">![워크벤치](./media/active-directory-saas-workday-tutorial/IC782923.png "워크벤치")</span><span class="sxs-lookup"><span data-stu-id="d716f-175">![Workbench](./media/active-directory-saas-workday-tutorial/IC782923.png "Workbench")</span></span>

9. <span data-ttu-id="d716f-176">**계정 관리**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-176">Go to **Account Administration**.</span></span>
   
    <span data-ttu-id="d716f-177">![계정 관리](./media/active-directory-saas-workday-tutorial/IC782924.png "계정 관리")</span><span class="sxs-lookup"><span data-stu-id="d716f-177">![Account Administration](./media/active-directory-saas-workday-tutorial/IC782924.png "Account Administration")</span></span>

10. <span data-ttu-id="d716f-178">**테넌트 설정 편집 - 보안**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-178">Go to **Edit Tenant Setup – Security**.</span></span>
   
    <span data-ttu-id="d716f-179">![테넌트 보안 편집](./media/active-directory-saas-workday-tutorial/IC782925.png "테넌트 보안 편집")</span><span class="sxs-lookup"><span data-stu-id="d716f-179">![Edit Tenant Security](./media/active-directory-saas-workday-tutorial/IC782925.png "Edit Tenant Security")</span></span>

11. <span data-ttu-id="d716f-180">**리디렉션 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-180">In the **Redirection URLs** section, perform the following steps:</span></span>
   
    <span data-ttu-id="d716f-181">![리디렉션 URL](./media/active-directory-saas-workday-tutorial/IC7829581.png "리디렉션 URL")</span><span class="sxs-lookup"><span data-stu-id="d716f-181">![Redirection URLs](./media/active-directory-saas-workday-tutorial/IC7829581.png "Redirection URLs")</span></span>
   
    <span data-ttu-id="d716f-182">a.</span><span class="sxs-lookup"><span data-stu-id="d716f-182">a.</span></span> <span data-ttu-id="d716f-183">**행 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-183">Click **Add Row**.</span></span>
   
    <span data-ttu-id="d716f-184">b.</span><span class="sxs-lookup"><span data-stu-id="d716f-184">b.</span></span> <span data-ttu-id="d716f-185">**로그인 리디렉션 URL** 텍스트 상자 및 **모바일 리디렉션 URL** 텍스트 상자에서 Azure Portal의 **Workday 도메인 및 URL** 섹션에 입력한 **로그온 URL**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-185">In the **Login Redirect URL** textbox and the **Mobile Redirect URL** textbox, type the **Sign-on URL** you have entered on the **Workday Domain and URLs** section of the Azure portal.</span></span>
   
    <span data-ttu-id="d716f-186">c.</span><span class="sxs-lookup"><span data-stu-id="d716f-186">c.</span></span> <span data-ttu-id="d716f-187">Azure Portal의 **로그온 구성** 창에서 **로그아웃 URL**을 복사한 다음 **Logout Redirect URL**(로그아웃 리디렉션 URL) 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-187">In the Azure portal, on the **Configure sign-on** window, copy the **Sign-Out URL**, and then paste it into the **Logout Redirect URL** textbox.</span></span>
   
    <span data-ttu-id="d716f-188">d.</span><span class="sxs-lookup"><span data-stu-id="d716f-188">d.</span></span>  <span data-ttu-id="d716f-189">**환경** 텍스트 상자에서 환경 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-189">In **Environment** textbox, type the environment name.</span></span>  

    >[!NOTE]
    > <span data-ttu-id="d716f-190">테넌트 URL의 값에 연결된 환경 특성의 값은:</span><span class="sxs-lookup"><span data-stu-id="d716f-190">The value of the Environment attribute is tied to the value of the tenant URL:</span></span>  
    ><span data-ttu-id="d716f-191">-Workday 테넌트 URL의 도메인 이름이 impl로 시작되는 경우(예: *https://impl.workday.com/\<tenant\>/login-saml2.htmld*) **환경** 특성이 Implementation으로 설정되어있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-191">-If the domain name of the Workday tenant URL starts with impl for example: *https://impl.workday.com/\<tenant\>/login-saml2.htmld*), the **Environment** attribute must be set to Implementation.</span></span>  
    ><span data-ttu-id="d716f-192">-도메인 이름이 다르게 시작되면 일치하는 **환경** 값을 [Workday 클라이언트 지원 팀](https://www.workday.com/en-us/partners-services/services/support.html)에 문의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-192">-If the domain name starts with something else, you need to contact [Workday Client support team](https://www.workday.com/en-us/partners-services/services/support.html) to get the matching **Environment** value.</span></span>

12. <span data-ttu-id="d716f-193">**SAML 설정** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-193">In the **SAML Setup** section, perform the following steps:</span></span>
   
    <span data-ttu-id="d716f-194">![SAML 설정](./media/active-directory-saas-workday-tutorial/IC782926.png "SAML 설정")</span><span class="sxs-lookup"><span data-stu-id="d716f-194">![SAML Setup](./media/active-directory-saas-workday-tutorial/IC782926.png "SAML Setup")</span></span>
   
    <span data-ttu-id="d716f-195">a.</span><span class="sxs-lookup"><span data-stu-id="d716f-195">a.</span></span>  <span data-ttu-id="d716f-196">**SAML 인증 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-196">Select **Enable SAML Authentication**.</span></span>
   
    <span data-ttu-id="d716f-197">b.</span><span class="sxs-lookup"><span data-stu-id="d716f-197">b.</span></span>  <span data-ttu-id="d716f-198">**행 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-198">Click **Add Row**.</span></span>

13. <span data-ttu-id="d716f-199">SAML ID 공급자 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-199">In the SAML Identity Providers section, perform the following steps:</span></span>
   
    <span data-ttu-id="d716f-200">![SAML ID 공급자](./media/active-directory-saas-workday-tutorial/IC7829271.png "SAML ID 공급자")</span><span class="sxs-lookup"><span data-stu-id="d716f-200">![SAML Identity Providers](./media/active-directory-saas-workday-tutorial/IC7829271.png "SAML Identity Providers")</span></span>
   
    <span data-ttu-id="d716f-201">a.</span><span class="sxs-lookup"><span data-stu-id="d716f-201">a.</span></span> <span data-ttu-id="d716f-202">ID 공급자 이름 텍스트 상자에 공급자 이름(예: *SPInitiatedSSO*)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-202">In the Identity Provider Name textbox, type a provider name (for example: *SPInitiatedSSO*).</span></span>
   
    <span data-ttu-id="d716f-203">b.</span><span class="sxs-lookup"><span data-stu-id="d716f-203">b.</span></span> <span data-ttu-id="d716f-204">Azure Portal의 **로그온 구성** 창에서 **SAML 엔터티 ID**  값을 복사한 다음 **발급자** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-204">In the Azure portal, on the **Configure sign-on** window, copy the **SAML Entity ID** value, and then paste it into the **Issuer** textbox.</span></span>
   
    <span data-ttu-id="d716f-205">c.</span><span class="sxs-lookup"><span data-stu-id="d716f-205">c.</span></span> <span data-ttu-id="d716f-206">**Enable Workday Initiated Logout**(Workday에서 시작된 로그아웃 사용)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-206">Select **Enable Workday Initiated Logout**.</span></span>
   
    <span data-ttu-id="d716f-207">d.</span><span class="sxs-lookup"><span data-stu-id="d716f-207">d.</span></span> <span data-ttu-id="d716f-208">Azure Portal의 **로그온 구성** 창에서 **로그아웃 URL** 값을 복사한 다음 **Logout Request URL**(로그아웃 요청 URL) 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-208">In the Azure portal, on the **Configure sign-on** window, copy the **Sign-Out URL** value, and then paste it into the **Logout Request URL** textbox.</span></span>

    <span data-ttu-id="d716f-209">e.</span><span class="sxs-lookup"><span data-stu-id="d716f-209">e.</span></span> <span data-ttu-id="d716f-210">**ID 공급자 공개 키 인증서**를 클릭한 다음 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-210">Click **Identity Provider Public Key Certificate**, and then click **Create**.</span></span> 

    <span data-ttu-id="d716f-211">![만들기](./media/active-directory-saas-workday-tutorial/IC782928.png "만들기")</span><span class="sxs-lookup"><span data-stu-id="d716f-211">![Create](./media/active-directory-saas-workday-tutorial/IC782928.png "Create")</span></span>

    <span data-ttu-id="d716f-212">f.</span><span class="sxs-lookup"><span data-stu-id="d716f-212">f.</span></span> <span data-ttu-id="d716f-213">**x509 공개 키 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-213">Click **Create x509 Public Key**.</span></span> 

    <span data-ttu-id="d716f-214">![만들기](./media/active-directory-saas-workday-tutorial/IC782929.png "만들기")</span><span class="sxs-lookup"><span data-stu-id="d716f-214">![Create](./media/active-directory-saas-workday-tutorial/IC782929.png "Create")</span></span>


14. <span data-ttu-id="d716f-215">**x509 공개 키 보기** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-215">In the **View x509 Public Key** section, perform the following steps:</span></span> 
   
    <span data-ttu-id="d716f-216">![x509 공개 키 보기](./media/active-directory-saas-workday-tutorial/IC782930.png "x509 공개 키 보기")</span><span class="sxs-lookup"><span data-stu-id="d716f-216">![View x509 Public Key](./media/active-directory-saas-workday-tutorial/IC782930.png "View x509 Public Key")</span></span> 
   
    <span data-ttu-id="d716f-217">a.</span><span class="sxs-lookup"><span data-stu-id="d716f-217">a.</span></span> <span data-ttu-id="d716f-218">**이름** 텍스트 상자에 인증서 이름(예: *PPE\_SP*)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-218">In the **Name** textbox, type a name for your certificate (for example: *PPE\_SP*).</span></span>
   
    <span data-ttu-id="d716f-219">b.</span><span class="sxs-lookup"><span data-stu-id="d716f-219">b.</span></span> <span data-ttu-id="d716f-220">**유효 시작** 텍스트 상자에 인증서의 유효 시작 특성 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-220">In the **Valid From** textbox, type the valid from attribute value of your certificate.</span></span>
   
    <span data-ttu-id="d716f-221">c.</span><span class="sxs-lookup"><span data-stu-id="d716f-221">c.</span></span>  <span data-ttu-id="d716f-222">**유효 만료** 텍스트 상자에 인증서의 유효 만료 특성 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-222">In the **Valid To** textbox, type the valid to attribute value of your certificate.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="d716f-223">유효 시작일과 유효 만료일은 다운로드한 인증서를 두 번 클릭하여 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-223">You can get the valid from date and the valid to date from the downloaded certificate by double-clicking it.</span></span>  <span data-ttu-id="d716f-224">날짜는 **세부 정보** 탭에 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-224">The dates are listed under the **Details** tab.</span></span>
    > 
    >
   
    <span data-ttu-id="d716f-225">d.</span><span class="sxs-lookup"><span data-stu-id="d716f-225">d.</span></span>  <span data-ttu-id="d716f-226">메모장에서 Base-64로 인코딩된 인증서를 열고 콘텐츠를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-226">Open your base-64 encoded certificate in notepad, and then copy the content of it.</span></span>
   
    <span data-ttu-id="d716f-227">e.</span><span class="sxs-lookup"><span data-stu-id="d716f-227">e.</span></span>  <span data-ttu-id="d716f-228">**인증서** 텍스트 상자에 클립보드의 내용을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-228">In the **Certificate** textbox, paste the content of your clipboard.</span></span>
   
    <span data-ttu-id="d716f-229">f.</span><span class="sxs-lookup"><span data-stu-id="d716f-229">f.</span></span>  <span data-ttu-id="d716f-230">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-230">Click **OK**.</span></span>

15. <span data-ttu-id="d716f-231">다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-231">Perform the following steps:</span></span> 
   
    <span data-ttu-id="d716f-232">![SSO 구성](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguratio.png "SSO 구성")</span><span class="sxs-lookup"><span data-stu-id="d716f-232">![SSO configuration](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguratio.png "SSO configuration")</span></span>
   
    <span data-ttu-id="d716f-233">a.</span><span class="sxs-lookup"><span data-stu-id="d716f-233">a.</span></span>  <span data-ttu-id="d716f-234">**x509 개인 키 쌍**을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-234">Enable the **x509 Private Key Pair**.</span></span>
   
    <span data-ttu-id="d716f-235">b.</span><span class="sxs-lookup"><span data-stu-id="d716f-235">b.</span></span>  <span data-ttu-id="d716f-236">**서비스 공급자 ID** 텍스트 상자에 **http://www.workday.com**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-236">In the **Service Provider ID** textbox, type **http://www.workday.com**.</span></span>
   
    <span data-ttu-id="d716f-237">c.</span><span class="sxs-lookup"><span data-stu-id="d716f-237">c.</span></span>  <span data-ttu-id="d716f-238">**SP가 시작한 SAML 인증 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-238">Select **Enable SP Initiated SAML Authentication**.</span></span>
   
    <span data-ttu-id="d716f-239">d.</span><span class="sxs-lookup"><span data-stu-id="d716f-239">d.</span></span>  <span data-ttu-id="d716f-240">Azure Portal의 **로그온 구성** 창에서 **SAML Single Sign-On 서비스 URL** 값을 복사한 다음 **IdP SSO 서비스 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-240">In the Azure portal, on the **Configure sign-on** window, copy the **SAML Single Sign-On Service URL** value, and then paste it into the **IdP SSO Service URL** textbox.</span></span>
   
    <span data-ttu-id="d716f-241">e.</span><span class="sxs-lookup"><span data-stu-id="d716f-241">e.</span></span> <span data-ttu-id="d716f-242">**SP에서 시작한 인증 요청을 Deflate하지 않음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-242">Select **Do Not Deflate SP-initiated Authentication Request**.</span></span>
   
    <span data-ttu-id="d716f-243">f.</span><span class="sxs-lookup"><span data-stu-id="d716f-243">f.</span></span> <span data-ttu-id="d716f-244">**인증 요청 서명 메서드**로 **SHA256**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-244">As **Authentication Request Signature Method**, select **SHA256**.</span></span> 
   
    <span data-ttu-id="d716f-245">![인증 요청 서명 메서드](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguration.png "인증 요청 서명 메서드")</span><span class="sxs-lookup"><span data-stu-id="d716f-245">![Authentication Request Signature Method](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguration.png "Authentication Request Signature Method")</span></span> 
   
    <span data-ttu-id="d716f-246">g.</span><span class="sxs-lookup"><span data-stu-id="d716f-246">g.</span></span> <span data-ttu-id="d716f-247">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-247">Click **OK**.</span></span> 
   
    <span data-ttu-id="d716f-248">![확인](./media/active-directory-saas-workday-tutorial/IC782933.png "확인")
<CE></span><span class="sxs-lookup"><span data-stu-id="d716f-248">![OK](./media/active-directory-saas-workday-tutorial/IC782933.png "OK")
<CE></span></span>

> [!TIP]
> <span data-ttu-id="d716f-249">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-249">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d716f-250">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-250">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d716f-251">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-251">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d716f-252">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="d716f-252">Creating an Azure AD test user</span></span>
<span data-ttu-id="d716f-253">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-253">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="d716f-255">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="d716f-255">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d716f-256">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-256">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-workday-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d716f-258">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-258">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-workday-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d716f-260">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-260">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-workday-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d716f-262">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-262">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-workday-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d716f-264">a.</span><span class="sxs-lookup"><span data-stu-id="d716f-264">a.</span></span> <span data-ttu-id="d716f-265">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-265">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d716f-266">b.</span><span class="sxs-lookup"><span data-stu-id="d716f-266">b.</span></span> <span data-ttu-id="d716f-267">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-267">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d716f-268">c.</span><span class="sxs-lookup"><span data-stu-id="d716f-268">c.</span></span> <span data-ttu-id="d716f-269">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-269">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d716f-270">d.</span><span class="sxs-lookup"><span data-stu-id="d716f-270">d.</span></span> <span data-ttu-id="d716f-271">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-271">Click **Create**.</span></span>
 
### <a name="creating-a-workday-test-user"></a><span data-ttu-id="d716f-272">Workday 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="d716f-272">Creating a Workday test user</span></span>

<span data-ttu-id="d716f-273">Workday에 테스트 사용자를 프로비전하려면 [Workday 클라이언트 지원 팀](https://www.workday.com/en-us/partners-services/services/support.html)에 문의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-273">To get a test user provisioned into Workday, you need to contact the [Workday Client support team](https://www.workday.com/en-us/partners-services/services/support.html).</span></span>
<span data-ttu-id="d716f-274">[Workday 클라이언트 지원 팀](https://www.workday.com/en-us/partners-services/services/support.html)이 사용자를 만들어 드립니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-274">The [Workday Client support team](https://www.workday.com/en-us/partners-services/services/support.html) creates the user for you.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d716f-275">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="d716f-275">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d716f-276">이 섹션에서는 Britta Simon이 Azure Single Sign-On을 사용할 수 있도록 Workday에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-276">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Workday.</span></span>

![사용자 할당][200] 

<span data-ttu-id="d716f-278">**Britta Simon을 Workday에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="d716f-278">**To assign Britta Simon to Workday, perform the following steps:**</span></span>

1. <span data-ttu-id="d716f-279">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-279">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="d716f-281">응용 프로그램 목록에서 **Workday**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-281">In the applications list, select **Workday**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-workday-tutorial/tutorial_workday_app.png) 

3. <span data-ttu-id="d716f-283">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-283">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="d716f-285">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-285">Click **Add** button.</span></span> <span data-ttu-id="d716f-286">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-286">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="d716f-288">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-288">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d716f-289">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-289">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d716f-290">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-290">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d716f-291">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="d716f-291">Testing single sign-on</span></span>

<span data-ttu-id="d716f-292">Single Sign-On 설정을 테스트하려면 액세스 패널을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d716f-292">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="d716f-293">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d716f-293">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d716f-294">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="d716f-294">Additional resources</span></span>

* [<span data-ttu-id="d716f-295">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="d716f-295">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d716f-296">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="d716f-296">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="d716f-297">사용자 프로비저닝 구성</span><span class="sxs-lookup"><span data-stu-id="d716f-297">Configure User Provisioning</span></span>](active-directory-saas-workday-inbound-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workday-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workday-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workday-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workday-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workday-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workday-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workday-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workday-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workday-tutorial/tutorial_general_203.png

