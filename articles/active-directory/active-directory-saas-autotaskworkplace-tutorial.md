---
title: "자습서: Autotask Workplace와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory 및 Autotask Workplace 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: a9a7ff71-c389-4169-aafd-d7a505244797
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 45130162271b20860607497ff93c6a668c415233
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-autotask-workplace"></a><span data-ttu-id="62acc-103">자습서: Autotask Workplace와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="62acc-103">Tutorial: Azure Active Directory integration with Autotask Workplace</span></span>

<span data-ttu-id="62acc-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Autotask Workplace를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-104">In this tutorial, you learn how to integrate Autotask Workplace with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="62acc-105">Autotask Workplace와 Azure AD를 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-105">Integrating Autotask Workplace with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="62acc-106">Azure AD에서는 Autotask Workplace에 대한 액세스 권한이 있는 사용자를 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-106">You can control in Azure AD who has access to Autotask Workplace</span></span>
- <span data-ttu-id="62acc-107">사용자가 해당 Azure AD 계정으로 Autotask Workplace에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-107">You can enable your users to automatically get signed-on to Autotask Workplace (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="62acc-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="62acc-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="62acc-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="62acc-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="62acc-110">Prerequisites</span></span>

<span data-ttu-id="62acc-111">Autotask Workplace와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-111">To configure Azure AD integration with Autotask Workplace, you need the following items:</span></span>

- <span data-ttu-id="62acc-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="62acc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="62acc-113">Autotask Workplace Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="62acc-113">An Autotask Workplace single-sign on enabled subscription</span></span>
- <span data-ttu-id="62acc-114">Workplace에서 관리자 또는 최고 관리자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-114">You must be an administrator or super administrator in Workplace.</span></span>
- <span data-ttu-id="62acc-115">Azure AD에서 관리자 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-115">You must have an administrator account in the Azure AD.</span></span>
- <span data-ttu-id="62acc-116">이 기능을 활용하는 사용자는 Workplace 및 Azure AD 내에 계정이 있어야 하며 둘에 대한 이메일 주소가 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-116">The users that will utilize this feature must have accounts within Workplace and the Azure AD, and their email addresses for both must match.</span></span>

> [!NOTE]
> <span data-ttu-id="62acc-117">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-117">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="62acc-118">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-118">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="62acc-119">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="62acc-119">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="62acc-120">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-120">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="62acc-121">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="62acc-121">Scenario description</span></span>
<span data-ttu-id="62acc-122">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-122">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="62acc-123">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-123">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="62acc-124">갤러리에서 Autotask Workplace 추가</span><span class="sxs-lookup"><span data-stu-id="62acc-124">Adding Autotask Workplace from the gallery</span></span>
2. <span data-ttu-id="62acc-125">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="62acc-125">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-autotask-workplace-from-the-gallery"></a><span data-ttu-id="62acc-126">갤러리에서 Autotask Workplace 추가</span><span class="sxs-lookup"><span data-stu-id="62acc-126">Adding Autotask Workplace from the gallery</span></span>
<span data-ttu-id="62acc-127">Autotask Workplace의 Azure AD 통합을 구성하려면 갤러리의 Autotask Workplace를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-127">To configure the integration of Autotask Workplace into Azure AD, you need to add Autotask Workplace from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="62acc-128">**갤러리에서 Autotask Workplace를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="62acc-128">**To add Autotask Workplace from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="62acc-129">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-129">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory 단추][1]

2. <span data-ttu-id="62acc-131">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-131">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="62acc-132">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-132">Then go to **All applications**.</span></span>

    ![엔터프라이즈 응용 프로그램 블레이드][2]
    
3. <span data-ttu-id="62acc-134">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-134">To add new application, click **New application** button on the top of dialog.</span></span>

    ![새 응용 프로그램 단추][3]

4. <span data-ttu-id="62acc-136">검색 상자에 **Autotask Workplace**를 입력하고 결과 패널에서 **Autotask Workplace**를 선택한 후 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-136">In the search box, type **Autotask Workplace**, select  **Autotask Workplace**  from result panel then click **Add** button to add the application.</span></span>

    ![결과 목록에서 Autotask Workplace](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="62acc-138">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="62acc-138">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="62acc-139">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Autotask Workplace에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-139">In this section, you configure and test Azure AD single sign-on with Autotask Workplace based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="62acc-140">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 대응하는 Autotask Workplace 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Autotask Workplace is to a user in Azure AD.</span></span> <span data-ttu-id="62acc-141">즉, Azure AD 사용자와 Autotask Workplace의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-141">In other words, a link relationship between an Azure AD user and the related user in Autotask Workplace needs to be established.</span></span>

<span data-ttu-id="62acc-142">Autotask Workplace에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-142">In Autotask Workplace, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="62acc-143">Autotask Workplace에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-143">To configure and test Azure AD single sign-on with Autotask Workplace, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="62acc-144">**[Azure AD Single Sign-On 구성](#configure-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-144">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="62acc-145">**[Azure AD 테스트 사용자 만들기](#create-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-145">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="62acc-146">**[Autotask Workplace 테스트 사용자 만들기](#create-an-autotask-workplace-test-user)** - Britta Simon의 Azure AD 표현과 연결되는 대응 사용자를 Autotask Workplace에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-146">**[Create an Autotask Workplace test user](#create-an-autotask-workplace-test-user)** - to have a counterpart of Britta Simon in Autotask Workplace that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="62acc-147">**[Azure AD 테스트 사용자 할당](#assign-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-147">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="62acc-148">**[Single Sign-on 테스트](#test-single-sign-on)** - 구성이 작동하는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-148">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="62acc-149">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="62acc-149">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="62acc-150">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Autotask Workplace 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Autotask Workplace application.</span></span>

<span data-ttu-id="62acc-151">**Autotask Workplace에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="62acc-151">**To configure Azure AD single sign-on with Autotask Workplace, perform the following steps:**</span></span>

1. <span data-ttu-id="62acc-152">Azure Portal의 **Autotask Workplace** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-152">In the Azure portal, on the **Autotask Workplace** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-On 구성 링크][4]

2. <span data-ttu-id="62acc-154">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_samlbase.png)

3. <span data-ttu-id="62acc-156">**Autotask Workplace 도메인 및 URL** 섹션에서 **IDP** 시작 모드로 응용 프로그램을 구성하려는 경우 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-156">If you wish to configure the application in **IDP** initiated mode, perform the following steps on the **Autotask Workplace Domain and URLs** section:</span></span>

    ![IDP에 대한 Autotask Workplace 도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_url.png)

    <span data-ttu-id="62acc-158">a.</span><span class="sxs-lookup"><span data-stu-id="62acc-158">a.</span></span> <span data-ttu-id="62acc-159">**식별자** 텍스트 상자에서 `https://<subdomain>.awp.autotask.net/singlesignon/saml/metadata` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-159">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.awp.autotask.net/singlesignon/saml/metadata`</span></span>

    <span data-ttu-id="62acc-160">b.</span><span class="sxs-lookup"><span data-stu-id="62acc-160">b.</span></span> <span data-ttu-id="62acc-161">**회신 URL** 텍스트 상자에 다음 패턴으로 URL을 입력합니다.`https://<subdomain>.awp.autotask.net/singlesignon/saml/SSO`</span><span class="sxs-lookup"><span data-stu-id="62acc-161">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.awp.autotask.net/singlesignon/saml/SSO`</span></span>

4. <span data-ttu-id="62acc-162">**SP** 시작 모드에서 응용 프로그램을 구성하려면 **고급 URL 설정**을 확인하고 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-162">If you wish to configure the application in **SP** initiated mode, check **Show advanced URL settings** and perform the following steps:</span></span>

    ![SP에 대한 Autotask Workplace 도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_url1.png)

    <span data-ttu-id="62acc-164">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<subdomain>.awp.autotask.net/loginsso`</span><span class="sxs-lookup"><span data-stu-id="62acc-164">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.awp.autotask.net/loginsso`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="62acc-165">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-165">These values are not real.</span></span> <span data-ttu-id="62acc-166">이러한 값을 실제 식별자, 회신 URL 및 로그온 URL로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-166">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="62acc-167">이러한 값을 얻으려면 [Autotask Workplace 클라이언트 지원팀](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="62acc-167">Contact [Autotask Workplace Client support team](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) to get these values.</span></span> 

5. <span data-ttu-id="62acc-168">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 메타데이터 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-168">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![인증서 다운로드 링크](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_certificate.png) 

6. <span data-ttu-id="62acc-170">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-170">Click **Save** button.</span></span>

    ![Single Sign-On 구성 저장 단추](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="62acc-172">다른 웹 브라우저 창에서 관리자 자격 증명을 사용하여 Workplace Online에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-172">In a different web browser window, Log in to Workplace Online using the administrator credentials.</span></span>

    >[!Note]
    ><span data-ttu-id="62acc-173">IdP를 구성할 때 하위 도메인을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-173">When configuring the IdP, a subdomain will need to be specified.</span></span> <span data-ttu-id="62acc-174">올바른 하위 도메인을 확인하려면 Workplace Online에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-174">To confirm the correct subdomain, login to Workplace Online.</span></span> <span data-ttu-id="62acc-175">로그인되면 URL에서 하위 도메인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-175">Once logged in, make note to the subdomain in the URL.</span></span>
    ><span data-ttu-id="62acc-176">하위 도메인은“https://“ 와 “.awp.autotask.net/“ 사이의 부분이며 us, eu, ca 또는 au여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-176">The subdomain is the part between the “https://“ and “.awp.autotask.net/“ and should be us, eu, ca, or au.</span></span>

8. <span data-ttu-id="62acc-177">**구성** > **Single Sign-On**으로 이동하고 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-177">Go to **Configuration** > **Single Sign-On** and perform the following steps:</span></span>

    ![Autotask Single Sign-On 구성](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskssoconfig1.png)
 
    <span data-ttu-id="62acc-179">a.</span><span class="sxs-lookup"><span data-stu-id="62acc-179">a.</span></span> <span data-ttu-id="62acc-180">**XML 메타데이터 파일** 옵션을 선택한 다음 Azure Portal에서 다운로드한 **메타데이터 XML**을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-180">Select the **XML Metadata File** option, and then upload the **Metadata XML** downloaded from Azure portal.</span></span>

    <span data-ttu-id="62acc-181">b.</span><span class="sxs-lookup"><span data-stu-id="62acc-181">b.</span></span> <span data-ttu-id="62acc-182">**SSO 사용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-182">Click **Enable SSO**.</span></span>
    
    ![Autotask Single Sign-On 승인 구성](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskssoconfig2.png)

    <span data-ttu-id="62acc-184">c.</span><span class="sxs-lookup"><span data-stu-id="62acc-184">c.</span></span> <span data-ttu-id="62acc-185">**I confirm this information is correct and I trust this IdP** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-185">Select the **I confirm this information is correct and I trust this IdP** check box.</span></span>

    <span data-ttu-id="62acc-186">d.</span><span class="sxs-lookup"><span data-stu-id="62acc-186">d.</span></span> <span data-ttu-id="62acc-187">**승인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-187">Click **Approve**.</span></span>
     
>[!Note]
><span data-ttu-id="62acc-188">Autotask Workplace 구성에 대한 도움이 필요한 경우 [이 페이지](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm)를 참조하여 Workplace 계정으로 지원을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-188">If you require assistance with configuring Autotask Workplace, please see [this page](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) to get assistance with your Workplace account.</span></span>

> [!TIP]
> <span data-ttu-id="62acc-189">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="62acc-190">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="62acc-191">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="62acc-192">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="62acc-192">Create an Azure AD test user</span></span>

<span data-ttu-id="62acc-193">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Azure AD 테스트 사용자 만들기][100]

<span data-ttu-id="62acc-195">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="62acc-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="62acc-196">Azure Portal의 왼쪽 창에서 **Azure Active Directory** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-196">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Azure Active Directory 단추](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="62acc-198">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-198">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !["사용자 및 그룹" 및 "모든 사용자" 링크](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="62acc-200">**사용자** 대화 상자를 열려면 **모든 사용자** 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-200">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![추가 단추](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="62acc-202">**사용자** 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-202">In the **User** dialog box, perform the following steps:</span></span>

    ![사용자 대화 상자](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_04.png)

    <span data-ttu-id="62acc-204">a.</span><span class="sxs-lookup"><span data-stu-id="62acc-204">a.</span></span> <span data-ttu-id="62acc-205">**이름** 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-205">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="62acc-206">b.</span><span class="sxs-lookup"><span data-stu-id="62acc-206">b.</span></span> <span data-ttu-id="62acc-207">**사용자 이름** 상자에 사용자인 Britta Simon의 전자 메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-207">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="62acc-208">c.</span><span class="sxs-lookup"><span data-stu-id="62acc-208">c.</span></span> <span data-ttu-id="62acc-209">**암호 표시** 확인란을 선택한 다음 **암호** 상자에 표시된 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-209">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="62acc-210">d.</span><span class="sxs-lookup"><span data-stu-id="62acc-210">d.</span></span> <span data-ttu-id="62acc-211">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-211">Click **Create**.</span></span>

### <a name="create-an-autotask-workplace-test-user"></a><span data-ttu-id="62acc-212">Autotask Workplace 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="62acc-212">Create an Autotask Workplace test user</span></span>

<span data-ttu-id="62acc-213">이 섹션에서는 Autotask에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-213">In this section, you create a user called Britta Simon in Autotask.</span></span> <span data-ttu-id="62acc-214">[Autotask Workplace 지원팀](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm)에 문의하여 Autotask Workplace 플랫폼에 사용자를 추가하세요.</span><span class="sxs-lookup"><span data-stu-id="62acc-214">Please work with [Autotask Workplace support team](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) to add the users in the Autotask Workplace platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="62acc-215">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="62acc-215">Assign the Azure AD test user</span></span>

<span data-ttu-id="62acc-216">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Autotask Workplace에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-216">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Autotask Workplace.</span></span>

![사용자 역할 할당][200] 

<span data-ttu-id="62acc-218">**Britta Simon을 Autotask Workplace에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="62acc-218">**To assign Britta Simon to Autotask Workplace, perform the following steps:**</span></span>

1. <span data-ttu-id="62acc-219">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-219">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="62acc-221">응용 프로그램 목록에서 **Autotask Workplace**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-221">In the applications list, select **Autotask Workplace**.</span></span>

    ![응용 프로그램 목록에서 Autotask Workplace 연결](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_app.png) 

3. <span data-ttu-id="62acc-223">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-223">In the menu on the left, click **Users and groups**.</span></span>

    !["사용자 및 그룹" 링크][202]

4. <span data-ttu-id="62acc-225">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-225">Click **Add** button.</span></span> <span data-ttu-id="62acc-226">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![할당 추가 창][203]

5. <span data-ttu-id="62acc-228">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-228">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="62acc-229">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="62acc-230">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="62acc-231">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="62acc-231">Test single sign-on</span></span>

<span data-ttu-id="62acc-232">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-232">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="62acc-233">액세스 패널에서 Autotask Workplace 타일을 클릭하면 Autotask Workplace 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="62acc-233">When you click the Autotask Workplace tile in the Access Panel, you should get automatically signed-on to your Autotask Workplace application.</span></span>
<span data-ttu-id="62acc-234">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="62acc-234">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="62acc-235">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="62acc-235">Additional resources</span></span>

* [<span data-ttu-id="62acc-236">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="62acc-236">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="62acc-237">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="62acc-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_203.png

