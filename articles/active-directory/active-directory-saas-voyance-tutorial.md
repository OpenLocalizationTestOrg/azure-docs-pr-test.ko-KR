---
title: "자습서: Voyance와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 Voyance 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 539dc1f9-64c9-4dce-b259-2b0b49dcf857
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/16/2017
ms.author: jeedes
ms.openlocfilehash: e860b810904fb7972d75d55d913d5622ff9a406a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-voyance"></a><span data-ttu-id="f768f-103">자습서: Azure Active Directory와 Voyance 통합</span><span class="sxs-lookup"><span data-stu-id="f768f-103">Tutorial: Azure Active Directory integration with Voyance</span></span>

<span data-ttu-id="f768f-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Voyance를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-104">In this tutorial, you learn how to integrate Voyance with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f768f-105">Voyance를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-105">Integrating Voyance with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f768f-106">Voyance에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-106">You can control in Azure AD who has access to Voyance</span></span>
- <span data-ttu-id="f768f-107">사용자가 해당 Azure AD 계정으로 Voyance에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-107">You can enable your users to automatically get signed-on to Voyance (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f768f-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f768f-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f768f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f768f-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="f768f-110">Prerequisites</span></span>

<span data-ttu-id="f768f-111">Voyance와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-111">To configure Azure AD integration with Voyance, you need the following items:</span></span>

- <span data-ttu-id="f768f-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="f768f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f768f-113">Voyance Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="f768f-113">A Voyance single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f768f-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f768f-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f768f-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="f768f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f768f-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f768f-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="f768f-118">Scenario description</span></span>
<span data-ttu-id="f768f-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f768f-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f768f-121">갤러리에서 Voyance 추가</span><span class="sxs-lookup"><span data-stu-id="f768f-121">Adding Voyance from the gallery</span></span>
2. <span data-ttu-id="f768f-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="f768f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-voyance-from-the-gallery"></a><span data-ttu-id="f768f-123">갤러리에서 Voyance 추가</span><span class="sxs-lookup"><span data-stu-id="f768f-123">Adding Voyance from the gallery</span></span>
<span data-ttu-id="f768f-124">Voyance의 Azure AD 통합을 구성하려면 갤러리의 Voyance를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-124">To configure the integration of Voyance into Azure AD, you need to add Voyance from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f768f-125">**갤러리에서 Voyance를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="f768f-125">**To add Voyance from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f768f-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory 단추][1]

2. <span data-ttu-id="f768f-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f768f-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-129">Then go to **All applications**.</span></span>

    ![엔터프라이즈 응용 프로그램 블레이드][2]
    
3. <span data-ttu-id="f768f-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![새 응용 프로그램 단추][3]

4. <span data-ttu-id="f768f-133">검색 상자에 **Voyance**를 입력하고 결과 패널에서 **Voyance**를 선택한 후 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-133">In the search box, type **Voyance**, select  **Voyance**  from result panel then click **Add** button to add the application.</span></span>

    ![결과 목록의 Voyance](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="f768f-135">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="f768f-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="f768f-136">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Voyance에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-136">In this section, you configure and test Azure AD single sign-on with Voyance based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f768f-137">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Voyance 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Voyance is to a user in Azure AD.</span></span> <span data-ttu-id="f768f-138">즉, Azure AD 사용자와 Voyance의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-138">In other words, a link relationship between an Azure AD user and the related user in Voyance needs to be established.</span></span>

<span data-ttu-id="f768f-139">Voyance에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 연결 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-139">In Voyance, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f768f-140">Voyance에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-140">To configure and test Azure AD single sign-on with Voyance, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f768f-141">**[Azure AD Single Sign-On 구성](#configure-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f768f-142">**[Azure AD 테스트 사용자 만들기](#create-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f768f-143">**[Voyance 테스트 사용자 만들기](#create-a-voyance-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 Voyance에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-143">**[Create a Voyance test user](#create-a-voyance-test-user)** - to have a counterpart of Britta Simon in Voyance that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f768f-144">**[Azure AD 테스트 사용자 할당](#assign-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f768f-145">**[Single Sign-on 테스트](#test-single-sign-on)** - 구성이 작동하는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="f768f-146">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="f768f-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="f768f-147">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Voyance 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Voyance application.</span></span>

<span data-ttu-id="f768f-148">**Voyance에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="f768f-148">**To configure Azure AD single sign-on with Voyance, perform the following steps:**</span></span>

1. <span data-ttu-id="f768f-149">Azure Portal의 **Voyance** 응용 프로그램 통합 페이지에서 **Single sign-on**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-149">In the Azure portal, on the **Voyance** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-On 구성 링크][4]

2. <span data-ttu-id="f768f-151">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_samlbase.png)

3. <span data-ttu-id="f768f-153">**Voyance 도메인 및 URL** 섹션에서 **IDP** 시작 모드로 응용 프로그램을 구성하려는 경우 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-153">On the **Voyance Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![IDP에 대한 Voyance 도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_url1.png)

    <span data-ttu-id="f768f-155">a.</span><span class="sxs-lookup"><span data-stu-id="f768f-155">a.</span></span> <span data-ttu-id="f768f-156">**식별자** 텍스트 상자에서 `https://<companyname>.nyansa.com` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-156">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.nyansa.com`</span></span>

    <span data-ttu-id="f768f-157">b.</span><span class="sxs-lookup"><span data-stu-id="f768f-157">b.</span></span> <span data-ttu-id="f768f-158">**회신 URL** 텍스트 상자에 다음 패턴으로 URL을 입력합니다.`https://<companyname>.nyansa.com/saml/create/`</span><span class="sxs-lookup"><span data-stu-id="f768f-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.nyansa.com/saml/create/`</span></span>

4. <span data-ttu-id="f768f-159">**SP** 시작 모드에서 응용 프로그램을 구성하려면 **고급 URL 설정 표시**를 확인하고 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-159">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![SP에 대한 Voyance 도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_url2.png)

    <span data-ttu-id="f768f-161">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<companyname>.nyansa.com/`</span><span class="sxs-lookup"><span data-stu-id="f768f-161">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.nyansa.com/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="f768f-162">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-162">These values are not real.</span></span> <span data-ttu-id="f768f-163">이러한 값을 실제 식별자, 회신 URL 및 로그온 URL로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-163">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="f768f-164">이러한 값을 얻으려면 [Voyance 클라이언트 지원 팀](mailto:support@nyansa.com)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="f768f-164">Contact [Voyance Client support team](mailto:support@nyansa.com) to get these values.</span></span> 

5. <span data-ttu-id="f768f-165">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-165">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![인증서 다운로드 링크](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_certificate.png) 

6. <span data-ttu-id="f768f-167">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-167">Click **Save** button.</span></span>

    ![Single Sign-On 구성 저장 단추](./media/active-directory-saas-voyance-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="f768f-169">**Voyance 구성** 섹션에서 **Voyance 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-169">On the **Voyance Configuration** section, click **Configure Voyance** to open **Configure sign-on** window.</span></span> <span data-ttu-id="f768f-170">**빠른 참조 섹션**에서 **SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-170">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Voyance 구성](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_configure.png) 

8. <span data-ttu-id="f768f-172">다른 웹 브라우저 창에서 Voyance 테넌트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-172">In a different web browser window, sign-on to your Voyance tenant as an administrator.</span></span>

9. <span data-ttu-id="f768f-173">탐색 모음의 오른쪽 위 구석으로 이동한 후 "**Acme University**"라는 드롭다운을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-173">Go to the top right corner of the navigation bar and click on the drop-down that says "**Acme University**".</span></span>
    
    ![앱 쪽에서 Single Sign-On 구성 Acme University](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_001.png) 

10. <span data-ttu-id="f768f-175">"**관리 설정**"을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-175">Click "**Admin Settings**".</span></span>

    ![앱 쪽에서 Single Sign-On 구성 관리 설정](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_002.png)

11. <span data-ttu-id="f768f-177">"**사용자 액세스**" 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-177">Click "**User Access**" tab.</span></span>

    ![앱 쪽에서 Single Sign-On 구성 사용자 액세스](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_003.png)

12. <span data-ttu-id="f768f-179">"**SSO 사용 안 함**" 단추를 클릭하여 SAML 2.0을 사용하여 IdP로 Azure AD를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-179">Click the "**SSO is disabled**" button to configure Azure AD as an IdP using SAML 2.0.</span></span>

    ![앱 쪽에서 Single Sign-On 구성 SSO가 비활성화됨 단추](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_004.png)

13. <span data-ttu-id="f768f-181">**SAML v2** 섹션으로 이동한 후 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-181">Go to **SAML v2** section and perform below steps:</span></span>

    ![앱 쪽에서 Single Sign-On 구성 SAML v2](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_005.png)
    
    <span data-ttu-id="f768f-183">a.</span><span class="sxs-lookup"><span data-stu-id="f768f-183">a.</span></span> <span data-ttu-id="f768f-184">**사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-184">Select **Enabled**.</span></span>
    
    <span data-ttu-id="f768f-185">b.</span><span class="sxs-lookup"><span data-stu-id="f768f-185">b.</span></span> <span data-ttu-id="f768f-186">Azure Portal에서 복사한 **SAML Single Sign-On 서비스 URL**을 **IdP 로그인 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-186">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal Into the **IdP Login URL** textbox.</span></span>

    <span data-ttu-id="f768f-187">c.</span><span class="sxs-lookup"><span data-stu-id="f768f-187">c.</span></span> <span data-ttu-id="f768f-188">다운로드한 Base64로 인코딩된 인증서를 메모장에서 열고, 내용을 클립보드에 복사한 다음 **IdP 인증서** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-188">Open your downloaded Base64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **IdP Cert** textbox.</span></span>
    
    <span data-ttu-id="f768f-189">d.</span><span class="sxs-lookup"><span data-stu-id="f768f-189">d.</span></span> <span data-ttu-id="f768f-190">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-190">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="f768f-191">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-191">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f768f-192">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-192">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f768f-193">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-193">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="f768f-194">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="f768f-194">Create an Azure AD test user</span></span>

<span data-ttu-id="f768f-195">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-195">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 테스트 사용자 만들기][100]

<span data-ttu-id="f768f-197">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="f768f-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f768f-198">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-198">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure Active Directory 단추](./media/active-directory-saas-voyance-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f768f-200">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-200">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    !["사용자 및 그룹" 및 "모든 사용자" 링크](./media/active-directory-saas-voyance-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f768f-202">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-202">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![추가 단추](./media/active-directory-saas-voyance-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f768f-204">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-204">On the **User** dialog page, perform the following steps:</span></span>
 
    ![사용자 대화 상자](./media/active-directory-saas-voyance-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f768f-206">a.</span><span class="sxs-lookup"><span data-stu-id="f768f-206">a.</span></span> <span data-ttu-id="f768f-207">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-207">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f768f-208">b.</span><span class="sxs-lookup"><span data-stu-id="f768f-208">b.</span></span> <span data-ttu-id="f768f-209">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-209">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f768f-210">c.</span><span class="sxs-lookup"><span data-stu-id="f768f-210">c.</span></span> <span data-ttu-id="f768f-211">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-211">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f768f-212">d.</span><span class="sxs-lookup"><span data-stu-id="f768f-212">d.</span></span> <span data-ttu-id="f768f-213">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-213">Click **Create**.</span></span>
 
### <a name="create-a-voyance-test-user"></a><span data-ttu-id="f768f-214">Voyance 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="f768f-214">Create a Voyance test user</span></span>

<span data-ttu-id="f768f-215">이 섹션은 Voyance에서 Britta Simon이라는 사용자를 만들기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-215">The objective of this section is to create a user called Britta Simon in Voyance.</span></span> <span data-ttu-id="f768f-216">Voyance는 적시에 프로비전을 지원하며 기본적으로 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-216">Voyance supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="f768f-217">이 섹션에 작업 항목이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-217">There is no action item for you in this section.</span></span> <span data-ttu-id="f768f-218">새 사용자가 아직 없는 경우 Voyance에 액세스를 시도하는 동안 새로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-218">A new user is created during an attempt to access Voyance if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="f768f-219">사용자를 수동으로 만들어야 하는 경우 [Voyance 지원 팀](maiLto:support@nyansa.com)에 문의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-219">If you need to create a user manually, you need to contact [Voyance support team](maiLto:support@nyansa.com).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="f768f-220">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="f768f-220">Assign the Azure AD test user</span></span>

<span data-ttu-id="f768f-221">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Voyance에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Voyance.</span></span>

![사용자 역할 할당][200]

<span data-ttu-id="f768f-223">**Britta Simon을 Voyance에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="f768f-223">**To assign Britta Simon to Voyance, perform the following steps:**</span></span>

1. <span data-ttu-id="f768f-224">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="f768f-226">응용 프로그램 목록에서 **Voyance**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-226">In the applications list, select **Voyance**.</span></span>

    ![응용 프로그램 목록의 Voyance 연결](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_app.png) 

3. <span data-ttu-id="f768f-228">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-228">In the menu on the left, click **Users and groups**.</span></span>

    !["사용자 및 그룹" 링크][202]

4. <span data-ttu-id="f768f-230">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-230">Click **Add** button.</span></span> <span data-ttu-id="f768f-231">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![할당 추가 창][203]

5. <span data-ttu-id="f768f-233">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f768f-234">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f768f-235">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="f768f-236">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="f768f-236">Test single sign-on</span></span>

<span data-ttu-id="f768f-237">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f768f-238">액세스 패널에서 Voyance 타일을 클릭하면 Voyance 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="f768f-238">When you click the Voyance tile in the Access Panel, you should get automatically signed-on to your Voyance application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f768f-239">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="f768f-239">Additional resources</span></span>

* [<span data-ttu-id="f768f-240">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="f768f-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f768f-241">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="f768f-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_203.png

