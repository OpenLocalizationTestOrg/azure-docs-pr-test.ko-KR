---
title: "자습서: Tangoe Command Premium Mobile과 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 Tangoe Command Premium Mobile 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 2b0b544c-9c2c-49cd-862b-ec2ee9330126
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 595541e7248a7486e58123927389c552af0e50f7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tangoe-command-premium-mobile"></a><span data-ttu-id="0cacb-103">자습서: Tangoe Command Premium Mobile과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="0cacb-103">Tutorial: Azure Active Directory integration with Tangoe Command Premium Mobile</span></span>

<span data-ttu-id="0cacb-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Tangoe Command Premium Mobile을 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="0cacb-104">In this tutorial, you learn how to integrate Tangoe Command Premium Mobile with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0cacb-105">Tangoe Command Premium Mobile을 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cacb-105">Integrating Tangoe Command Premium Mobile with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0cacb-106">Tangoe Command Premium Mobile에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cacb-106">You can control in Azure AD who has access to Tangoe Command Premium Mobile</span></span>
- <span data-ttu-id="0cacb-107">사용자가 해당 Azure AD 계정으로 Tangoe Command Premium Mobile에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cacb-107">You can enable your users to automatically get signed-on to Tangoe Command Premium Mobile (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0cacb-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cacb-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="0cacb-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0cacb-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0cacb-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="0cacb-110">Prerequisites</span></span>

<span data-ttu-id="0cacb-111">Tangoe Command Premium Mobile과 Azure AD의 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0cacb-111">To configure Azure AD integration with Tangoe Command Premium Mobile, you need the following items:</span></span>

- <span data-ttu-id="0cacb-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="0cacb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0cacb-113">Tangoe Command Premium Mobile Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="0cacb-113">A Tangoe Command Premium Mobile single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0cacb-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0cacb-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0cacb-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cacb-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0cacb-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="0cacb-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0cacb-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cacb-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0cacb-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="0cacb-118">Scenario description</span></span>
<span data-ttu-id="0cacb-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cacb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0cacb-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cacb-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0cacb-121">갤러리에서 Tangoe Command Premium Mobile 추가</span><span class="sxs-lookup"><span data-stu-id="0cacb-121">Add Tangoe Command Premium Mobile from the gallery</span></span>
2. <span data-ttu-id="0cacb-122">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="0cacb-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-tangoe-command-premium-mobile-from-the-gallery"></a><span data-ttu-id="0cacb-123">갤러리에서 Tangoe Command Premium Mobile 추가</span><span class="sxs-lookup"><span data-stu-id="0cacb-123">Add Tangoe Command Premium Mobile from the gallery</span></span>
<span data-ttu-id="0cacb-124">Tangoe Command Premium Mobile과 Azure AD 통합을 구성하려면 갤러리의 Tangoe Command Premium Mobile을 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cacb-124">To configure the integration of Tangoe Command Premium Mobile into Azure AD, you need to add Tangoe Command Premium Mobile from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0cacb-125">**갤러리에서 Tangoe Command Premium Mobile을 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="0cacb-125">**To add Tangoe Command Premium Mobile from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0cacb-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0cacb-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0cacb-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="0cacb-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0cacb-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="0cacb-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="0cacb-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0cacb-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="0cacb-133">검색 상자에 **Tangoe Command Premium Mobile**을 입력하고, 결과 패널에서 **Tangoe Command Premium Mobile**을 선택한 다음 **추가** 단추를 눌러 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0cacb-133">In the search box, type **Tangoe Command Premium Mobile**, select **Tangoe Command Premium Mobile** from result panel then click **Add** button to add the application.</span></span>

    ![<span data-ttu-id="0cacb-134">갤러리에서 Tangoe Command Premium Mobile 추가</span><span class="sxs-lookup"><span data-stu-id="0cacb-134">Add Tangoe Command Premium Mobile from gallery</span></span> ](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="0cacb-135">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="0cacb-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="0cacb-136">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Tangoe Command Premium Mobile에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="0cacb-136">In this section, you configure and test Azure AD single sign-on with Tangoe Command Premium Mobile based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0cacb-137">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Tangoe Command Premium Mobile 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cacb-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Tangoe Command Premium Mobile is to a user in Azure AD.</span></span> <span data-ttu-id="0cacb-138">즉, Azure AD 사용자와 Tangoe Command Premium Mobile의 관련 사용자 간에 연결이 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cacb-138">In other words, a link relationship between an Azure AD user and the related user in Tangoe Command Premium Mobile needs to be established.</span></span>

<span data-ttu-id="0cacb-139">Tangoe Command Premium Mobile에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 연결 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0cacb-139">In Tangoe Command Premium Mobile, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="0cacb-140">Tangoe Command Premium Mobile에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cacb-140">To configure and test Azure AD single sign-on with Tangoe Command Premium Mobile, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0cacb-141">**[Azure AD Single Sign-On 구성](#configure-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cacb-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="0cacb-142">**[Azure AD 테스트 사용자 만들기](#create-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0cacb-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0cacb-143">**[Tangoe Command Premium Mobile 테스트 사용자 만들기](#create-a-tangoe-command-premium-mobile-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 Tangoe Command Premium Mobile에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0cacb-143">**[Create a Tangoe Command Premium Mobile test user](#create-a-tangoe-command-premium-mobile-test-user)** - to have a counterpart of Britta Simon in Tangoe Command Premium Mobile that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="0cacb-144">**[Azure AD 테스트 사용자 할당](#assign-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cacb-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0cacb-145">**[Single Sign-on 테스트](#test-single-sign-on)** - 구성이 작동하는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0cacb-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="0cacb-146">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="0cacb-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="0cacb-147">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Tangoe Command Premium Mobile 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="0cacb-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Tangoe Command Premium Mobile application.</span></span>

<span data-ttu-id="0cacb-148">**Tangoe Command Premium Mobile에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="0cacb-148">**To configure Azure AD single sign-on with Tangoe Command Premium Mobile, perform the following steps:**</span></span>

1. <span data-ttu-id="0cacb-149">Azure Portal의 **Tangoe Command Premium Mobile** 응용 프로그램 통합 페이지에서 **Single sign-on**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0cacb-149">In the Azure portal, on the **Tangoe Command Premium Mobile** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="0cacb-151">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0cacb-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![SAML 기반 로그온](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_samlbase.png)

3. <span data-ttu-id="0cacb-153">**Tangoe Command Premium Mobile 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="0cacb-153">On the **Tangoe Command Premium Mobile Domain and URLs** section, perform the following steps:</span></span>

    ![Tangoe Command Premium Mobile 도메인 및 URL](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_url.png)

    <span data-ttu-id="0cacb-155">a.</span><span class="sxs-lookup"><span data-stu-id="0cacb-155">a.</span></span> <span data-ttu-id="0cacb-156">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://sso.tangoe.com/sp/startSSO.ping?PartnerIdpId=<tenant issuer>&TARGET=<target page url>`</span><span class="sxs-lookup"><span data-stu-id="0cacb-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://sso.tangoe.com/sp/startSSO.ping?PartnerIdpId=<tenant issuer>&TARGET=<target page url>`</span></span>

    <span data-ttu-id="0cacb-157">b.</span><span class="sxs-lookup"><span data-stu-id="0cacb-157">b.</span></span> <span data-ttu-id="0cacb-158">**회신 URL** 텍스트 상자에 다음 패턴으로 URL을 입력합니다.`https://sso.tangoe.com/sp/ACS.saml2`</span><span class="sxs-lookup"><span data-stu-id="0cacb-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://sso.tangoe.com/sp/ACS.saml2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0cacb-159">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="0cacb-159">These values are not real.</span></span> <span data-ttu-id="0cacb-160">실제 회신 URL 및 로그온 URL을 사용하여 이러한 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="0cacb-160">Update these values with the actual  Reply URL and Sign-On URL.</span></span> <span data-ttu-id="0cacb-161">이러한 값을 얻으려면 [Tangoe Command Premium Mobile 클라이언트 지원 팀](https://www.tangoe.com/contact-2/)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="0cacb-161">Contact [Tangoe Command Premium Mobile Client support team](https://www.tangoe.com/contact-2/) to get these values.</span></span> 

4. <span data-ttu-id="0cacb-162">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 메타데이터 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="0cacb-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![SAML 서명 인증서 섹션](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_certificate.png) 

5. <span data-ttu-id="0cacb-164">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0cacb-164">Click **Save** button.</span></span>

    ![저장 단추](./media/active-directory-saas-tangoe-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="0cacb-166">**Tangoe Command Premium Mobile** 섹션에서 **Tangoe Command Premium Mobile 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0cacb-166">On the **Tangoe Command Premium Mobile Configuration** section, click **Configure Tangoe Command Premium Mobile** to open **Configure sign-on** window.</span></span> <span data-ttu-id="0cacb-167">**빠른 참조 섹션**에서 **로그아웃 URL, SAML 엔터티 ID 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="0cacb-167">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Tangoe Command Premium Mobile 구성 섹션](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_configure.png) 

7. <span data-ttu-id="0cacb-169">응용 프로그램에 SSO를 구성하려면 [Tangoe Command Premium Mobile 클라이언트 지원 팀](https://www.tangoe.com/contact-2/)에 연락하여 다음 정보를 제공하세요.</span><span class="sxs-lookup"><span data-stu-id="0cacb-169">To get SSO configured for your application, contact your [Tangoe Command Premium Mobile Client support team](https://www.tangoe.com/contact-2/) and provide the following:</span></span>

   - <span data-ttu-id="0cacb-170">다운로드한 메타데이터 파일</span><span class="sxs-lookup"><span data-stu-id="0cacb-170">The downloaded metadata file</span></span>
   - <span data-ttu-id="0cacb-171">**SAML 엔터티 ID**</span><span class="sxs-lookup"><span data-stu-id="0cacb-171">The **SAML Entity ID**</span></span>
   - <span data-ttu-id="0cacb-172">**SAML Single Sign-On 서비스 URL**</span><span class="sxs-lookup"><span data-stu-id="0cacb-172">The **SAML Single Sign-On Service URL**</span></span>
   - <span data-ttu-id="0cacb-173">**로그아웃 URL**</span><span class="sxs-lookup"><span data-stu-id="0cacb-173">The **Sign-Out URL**</span></span>

> [!TIP]
> <span data-ttu-id="0cacb-174">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cacb-174">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="0cacb-175">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cacb-175">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="0cacb-176">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cacb-176">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="0cacb-177">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="0cacb-177">Create an Azure AD test user</span></span>
<span data-ttu-id="0cacb-178">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0cacb-178">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="0cacb-180">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="0cacb-180">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0cacb-181">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0cacb-181">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-tangoe-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0cacb-183">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0cacb-183">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![사용자 및 그룹 -> 모든 사용자](./media/active-directory-saas-tangoe-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0cacb-185">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0cacb-185">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![사용자 추가](./media/active-directory-saas-tangoe-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0cacb-187">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="0cacb-187">On the **User** dialog page, perform the following steps:</span></span>
 
    ![사용자 대화 상자 페이지](./media/active-directory-saas-tangoe-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0cacb-189">a.</span><span class="sxs-lookup"><span data-stu-id="0cacb-189">a.</span></span> <span data-ttu-id="0cacb-190">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0cacb-190">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0cacb-191">b.</span><span class="sxs-lookup"><span data-stu-id="0cacb-191">b.</span></span> <span data-ttu-id="0cacb-192">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0cacb-192">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0cacb-193">c.</span><span class="sxs-lookup"><span data-stu-id="0cacb-193">c.</span></span> <span data-ttu-id="0cacb-194">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="0cacb-194">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="0cacb-195">d.</span><span class="sxs-lookup"><span data-stu-id="0cacb-195">d.</span></span> <span data-ttu-id="0cacb-196">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0cacb-196">Click **Create**.</span></span>
 
### <a name="create-a-tangoe-command-premium-mobile-test-user"></a><span data-ttu-id="0cacb-197">Tangoe Command Premium Mobile 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="0cacb-197">Create a Tangoe Command Premium Mobile test user</span></span>

<span data-ttu-id="0cacb-198">이 섹션에서는 Tangoe Command Premium Mobile에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0cacb-198">In this section, you create a user called Britta Simon in Tangoe Command Premium Mobile.</span></span> 

<span data-ttu-id="0cacb-199">Tangoe Command Premium Mobile 응용 프로그램에서는 Single Sign On을 수행하기 전에 모든 사용자를 프로비전해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cacb-199">Tangoe Command Premium Mobile application needs all the users to be provisioned in the application before doing Single Sign On.</span></span> <span data-ttu-id="0cacb-200">따라서 [Tangoe Command Premium Mobile 클라이언트 지원 팀](https://www.tangoe.com/contact-2/)과 협력하여 모든 사용자를 응용 프로그램에 프로비전하세요.</span><span class="sxs-lookup"><span data-stu-id="0cacb-200">So please work with the [Tangoe Command Premium Mobile Client support team](https://www.tangoe.com/contact-2/) to provision all these users into the application.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="0cacb-201">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="0cacb-201">Assign the Azure AD test user</span></span>

<span data-ttu-id="0cacb-202">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Tangoe Command Premium Mobile에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="0cacb-202">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Tangoe Command Premium Mobile.</span></span>

![사용자 할당][200] 

<span data-ttu-id="0cacb-204">**Britta Simon을 Tangoe Command Premium Mobile에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="0cacb-204">**To assign Britta Simon to Tangoe Command Premium Mobile, perform the following steps:**</span></span>

1. <span data-ttu-id="0cacb-205">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0cacb-205">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="0cacb-207">응용 프로그램 목록에서 **Tangoe Command Premium Mobile**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0cacb-207">In the applications list, select **Tangoe Command Premium Mobile**.</span></span>

    ![앱 목록의 Tangoe Command Premium Mobile](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_app.png) 

3. <span data-ttu-id="0cacb-209">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0cacb-209">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="0cacb-211">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0cacb-211">Click **Add** button.</span></span> <span data-ttu-id="0cacb-212">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0cacb-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="0cacb-214">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0cacb-214">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="0cacb-215">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0cacb-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0cacb-216">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0cacb-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="0cacb-217">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="0cacb-217">Test single sign-on</span></span>

<span data-ttu-id="0cacb-218">이 섹션에서는 액세스 패널을 사용하여 Azure AD SSO 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="0cacb-218">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="0cacb-219">액세스 패널에서 Tangoe Command Premium Mobile 타일을 클릭하면 Tangoe Command Premium Mobile 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cacb-219">When you click the Tangoe Command Premium Mobile tile in the Access Panel, you should get automatically signed-on to your Tangoe Command Premium Mobile application.</span></span> <span data-ttu-id="0cacb-220">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0cacb-220">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="0cacb-221">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="0cacb-221">Additional resources</span></span>

* [<span data-ttu-id="0cacb-222">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="0cacb-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0cacb-223">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="0cacb-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_203.png

