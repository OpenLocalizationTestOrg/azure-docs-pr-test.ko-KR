---
title: "자습서: SAP HANA Cloud Platform Identity Authentication과 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory 및 SAP HANA Cloud Platform Identity Authentication 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1c1320d1-7ba4-4b5f-926f-4996b44d9b5e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 7799bf03cc6705f805a48f329a265a3d84bed55f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana-cloud-platform-identity-authentication"></a><span data-ttu-id="83c0f-103">자습서: SAP HANA Cloud Platform Identity Authentication과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="83c0f-103">Tutorial: Azure Active Directory integration with SAP HANA Cloud Platform Identity Authentication</span></span>

<span data-ttu-id="83c0f-104">이 자습서에서는 Azure AD(Azure Active Directory)와 SAP HANA Cloud Platform Identity Authentication을 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-104">In this tutorial, you learn how to integrate SAP HANA Cloud Platform Identity Authentication with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="83c0f-105">기본 IdP로 Azure AD를 사용하여 SAP 응용 프로그램에 액세스하는 프록시 IdP로 SAP HANA Cloud Platform Identity Authentication이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-105">SAP HANA Cloud Platform Identity Authentication is used as a proxy IdP to access SAP applications using Azure AD as the main IdP.</span></span>

<span data-ttu-id="83c0f-106">SAP HANA Cloud Platform Identity Authentication을 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-106">Integrating SAP HANA Cloud Platform Identity Authentication with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="83c0f-107">SAP 응용 프로그램에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-107">You can control in Azure AD who has access to SAP application</span></span>
- <span data-ttu-id="83c0f-108">사용자가 해당 Azure AD 계정으로 SAP 응용 프로그램 SSO(Single Sign-on)에 자동으로 로그온되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-108">You can enable your users to automatically get signed-on to SAP applications single sign-on (SSO) with their Azure AD accounts</span></span>
- <span data-ttu-id="83c0f-109">단일 중앙 위치인 Azure 클래식 포털에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-109">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="83c0f-110">Azure AD와의 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory를 사용한 응용 프로그램 액세스 및 Single Sign-On](active-directory-appssoaccess-whatis.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="83c0f-110">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="83c0f-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="83c0f-111">Prerequisites</span></span>

<span data-ttu-id="83c0f-112">SAP HANA Cloud Platform Identity Authentication과 Azure AD의 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-112">To configure Azure AD integration with SAP HANA Cloud Platform Identity Authentication, you need the following items:</span></span>

- <span data-ttu-id="83c0f-113">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="83c0f-113">An Azure AD subscription</span></span>
- <span data-ttu-id="83c0f-114">**SAP HANA Cloud Platform Identity Authentication** SSO가 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="83c0f-114">A **SAP HANA Cloud Platform Identity Authentication** SSO enabled subscription</span></span>


>[!NOTE] 
><span data-ttu-id="83c0f-115">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
>

<span data-ttu-id="83c0f-116">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="83c0f-117">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-117">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="83c0f-118">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-118">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="83c0f-119">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="83c0f-119">Scenario description</span></span>
<span data-ttu-id="83c0f-120">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="83c0f-121">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="83c0f-122">갤러리에서 SAP HANA Cloud Platform Identity Authentication 추가</span><span class="sxs-lookup"><span data-stu-id="83c0f-122">Adding SAP HANA Cloud Platform Identity Authentication from the gallery</span></span>
2. <span data-ttu-id="83c0f-123">Azure AD SSO 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="83c0f-123">Configuring and testing Azure AD SSO</span></span>

<span data-ttu-id="83c0f-124">기술 세부 정보를 분석하기 앞서 확인하려는 개념을 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-124">Before diving into the technical details, it is vital to understand the concepts you're going to look at.</span></span> <span data-ttu-id="83c0f-125">SAP HANA Cloud Platform Identity Authentication 및 Azure Active Directory 페더레이션을 통해 SAP HANA Cloud Platform Identity Authentication으로 보호되는 SAP 응용 프로그램 및 서비스와 함께 AAD(IdP로)로 보호되는 응용 프로그램 또는 서비스 간에 SSO를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-125">The SAP HANA Cloud Platform Identity Authentication and Azure Active Directory federation enables you to implement SSO across applications or services protected by AAD (as an IdP) with SAP applications and services protected by SAP HANA Cloud Platform Identity Authentication.</span></span>

<span data-ttu-id="83c0f-126">현재는 SAP HANA Cloud Platform Identity Authentication이 SAP 응용 프로그램에 대한 프록시 ID 공급자로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-126">Currently, SAP HANA Cloud Platform Identity Authentication acts as a Proxy Identity Provider to SAP-applications.</span></span> <span data-ttu-id="83c0f-127">그리고 Azure Active Directory는 이 설정에서 주요 ID 공급자로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-127">Azure Active Directory in turn acts as the leading Identity Provider in this setup.</span></span> 

<span data-ttu-id="83c0f-128">아래 다이어그램은 다음 사항을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-128">The following diagram illustrates this:</span></span>    

![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/architecture-01.png)

<span data-ttu-id="83c0f-130">이 설정을 통해 SAP HANA Cloud Platform Identity Authentication 테넌트가 Azure Active Directory에서 신뢰할 수 있는 응용 프로그램으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-130">With this setup, your SAP HANA Cloud Platform Identity Authentication tenant will be configured as a trusted application in Azure Active Directory.</span></span> 

<span data-ttu-id="83c0f-131">이 방법을 통해 보호하려는 모든 SAP 응용 프로그램 및 서비스는 SAP HANA Cloud Platform Identity Authentication 관리 콘솔에서 나중에 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-131">All SAP applications and services you want to protect through this way are subsequently configured in the SAP HANA Cloud Platform Identity Authentication management console!</span></span>

<span data-ttu-id="83c0f-132">따라서 이러한 설정을 위해 SAP HANA Cloud Platform Identity Authentication에서 SAP 응용 프로그램 및 서비스에 대한 액세스 권한 부여를 수행해야 합니다(Azure Active Directory에서 권한 부여 구성이 아님).</span><span class="sxs-lookup"><span data-stu-id="83c0f-132">This means that authorization for granting access to SAP applications and services needs to take place in SAP HANA Cloud Platform Identity Authentication for such a setup (as opposed to configuring authorization in Azure Active Directory).</span></span>

<span data-ttu-id="83c0f-133">Azure Active Directory Marketplace를 통해 응용 프로그램으로 SAP HANA Cloud Platform Identity Authentication을 구성하면, 필요한 개별 클레임/SAML 어설션 및 SAP 응용 프로그램에 유효한 인증 토큰을 생성하는 데 필요한 변환을 구성할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-133">By configuring SAP HANA Cloud Platform Identity Authentication as an application through the Azure Active Directory Marketplace, you don't need to take care of configuring needed individual claims / SAML assertions and transformations needed to produce a valid authentication token for SAP applications.</span></span>

>[!NOTE] 
><span data-ttu-id="83c0f-134">현재 웹 SSO는 두 파티에서만 테스트되었습니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-134">Currently Web SSO has been tested by both parties, only.</span></span> <span data-ttu-id="83c0f-135">앱-API 또는 API-API 통신에 필요한 흐름은 작동하지만 아직 테스트되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-135">Flows needed for App-to-API or API-to-API communication should work but have not been tested, yet.</span></span> <span data-ttu-id="83c0f-136">후속 작업의 일부로 테스트될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-136">They will be tested as part of subsequent activities.</span></span>
>

## <a name="add-sap-hana-cloud-platform-identity-authentication-from-the-gallery"></a><span data-ttu-id="83c0f-137">갤러리에서 SAP HANA Cloud Platform Identity Authentication 추가</span><span class="sxs-lookup"><span data-stu-id="83c0f-137">Add SAP HANA Cloud Platform Identity Authentication from the gallery</span></span>
<span data-ttu-id="83c0f-138">SAP HANA Cloud Platform Identity Authentication의 Azure AD 통합을 구성하려면 갤러리의 SAP HANA Cloud Platform Identity Authentication을 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-138">To configure the integration of SAP HANA Cloud Platform Identity Authentication into Azure AD, you need to add SAP HANA Cloud Platform Identity Authentication from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="83c0f-139">**갤러리에서 SAP HANA Cloud Platform Identity Authentication을 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="83c0f-139">**To add SAP HANA Cloud Platform Identity Authentication from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="83c0f-140">[**Azure 관리 포털**](https://portal.azure.com)의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-140">In the [**Azure Management portal**](https://portal.azure.com), on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="83c0f-142">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-142">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="83c0f-143">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-143">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="83c0f-145">대화 상자 위쪽에 있는 **추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-145">Click **Add** button on the top of the dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="83c0f-147">검색 상자에 **SAP HANA Cloud Platform Identity Authentication**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-147">In the search box, type **SAP HANA Cloud Platform Identity Authentication**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_01.png)

5. <span data-ttu-id="83c0f-149">결과 창에서 **SAP HANA Cloud Platform Identity Authentication**을 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-149">In the results panel, select **SAP HANA Cloud Platform Identity Authentication**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_02.png)


##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="83c0f-151">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="83c0f-151">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="83c0f-152">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 SAP HANA Cloud Platform Identity Authentication에서 Azure AD SSO를 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-152">In this section, you configure and test Azure AD SSO with SAP HANA Cloud Platform Identity Authentication based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="83c0f-153">SSO가 작동하려면 Azure AD에서 사용자에 해당하는 SAP HANA Cloud Platform Identity Authentication 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-153">For SSO to work, Azure AD needs to know what the counterpart user in SAP HANA Cloud Platform Identity Authentication is to a user in Azure AD.</span></span> <span data-ttu-id="83c0f-154">즉, Azure AD 사용자와 SAP HANA Cloud Platform Identity Authentication의 관련 사용자 간에 연결 관계가 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-154">In other words, a link relationship between an Azure AD user and the related user in SAP HANA Cloud Platform Identity Authentication needs to be established.</span></span>

<span data-ttu-id="83c0f-155">이 연결 관계는 Azure AD의 **사용자 이름** 값을 SAP HANA Cloud Platform Identity Authentication의 **Username** 값으로 할당하여 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-155">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in SAP HANA Cloud Platform Identity Authentication.</span></span>

<span data-ttu-id="83c0f-156">SAP HANA Cloud Platform Identity Authentication에서 Azure AD SSO를 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-156">To configure and test Azure AD SSO with SAP HANA Cloud Platform Identity Authentication, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="83c0f-157">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-157">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="83c0f-158">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-158">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="83c0f-159">**[SAP HANA Cloud Platform Identity Authentication 테스트 사용자 만들기](#creating-a-sap-hana-cloud-platform-identity-authentication-test-user)** - Azure AD를 대표하여 SAP HANA Cloud Platform Identity Authentication에서 Britta Simon에 해당하는 사용자가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-159">**[Creating a SAP HANA Cloud Platform Identity Authentication test user](#creating-a-sap-hana-cloud-platform-identity-authentication-test-user)** - to have a counterpart of Britta Simon in SAP HANA Cloud Platform Identity Authentication that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="83c0f-160">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-160">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="83c0f-161">**[Single Sign-On 테스트](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-161">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-sso"></a><span data-ttu-id="83c0f-162">Azure AD SSO 구성</span><span class="sxs-lookup"><span data-stu-id="83c0f-162">Configuring Azure AD SSO</span></span>

<span data-ttu-id="83c0f-163">이 섹션에서는 Azure 관리 포털에서 Azure AD SSO를 사용하도록 설정하고 SAP HANA Cloud Platform Identity Authentication 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-163">In this section, you enable Azure AD SSO in the Azure Management portal and configure single sign-on in your SAP HANA Cloud Platform Identity Authentication application.</span></span>

<span data-ttu-id="83c0f-164">SAP HANA Cloud Platform Identity Authentication 응용 프로그램은 특정 형식의 SAML 어설션이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-164">SAP HANA Cloud Platform Identity Authentication application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="83c0f-165">응용 프로그램 통합 페이지의 **"사용자 특성"** 섹션에서 이러한 특성의 값을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-165">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="83c0f-166">다음 스크린샷은 이에 대한 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-166">The following screenshot shows an example for this.</span></span>

![Single Sign-on 구성](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_03.png)

<span data-ttu-id="83c0f-168">**SAP HANA Cloud Platform Identity Authentication에서 Azure AD SSO를 구성하려면 다음 단계가 필요합니다.**</span><span class="sxs-lookup"><span data-stu-id="83c0f-168">**To configure Azure AD SSO with SAP HANA Cloud Platform Identity Authentication, perform the following steps:**</span></span>

1. <span data-ttu-id="83c0f-169">Azure 관리 포털의 **SAP HANA Cloud Platform Identity Authentication** 응용 프로그램 통합 페이지에서 **Single sign-on**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-169">In the Azure Management portal, on the **SAP HANA Cloud Platform Identity Authentication** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="83c0f-171">**Single sign on** 대화 상자에서 **모드**로 **SAML 기반 로그온**을 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-171">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Single Sign-On 구성][5]

3. <span data-ttu-id="83c0f-173">**Single sign-on** 대화 상자의 **사용자 특성** 섹션에서 SAP 응용 프로그램에 특성이 필요한 경우(예: "firstName")</span><span class="sxs-lookup"><span data-stu-id="83c0f-173">In the **User Attributes** section on the **Single sign-on** dialog, if your SAP application expects an attribute for example "firstName".</span></span> <span data-ttu-id="83c0f-174">SAML 토큰 특성 대화 상자에서 "firstName" 특성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-174">On the SAML token attributes dialog, add the "firstName" attribute.</span></span>
 1. <span data-ttu-id="83c0f-175">**특성 추가**를 클릭하여 **특성 추가** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-175">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>
 
    ![Single Sign-On 구성][6]

    ![Single Sign-on 구성](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_05.png)
 2. <span data-ttu-id="83c0f-178">**특성 이름** 텍스트 상자에서 특성 이름 "firstName"을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-178">In the **Attribute Name** textbox, type the attribute name "firstName".</span></span>
 3. <span data-ttu-id="83c0f-179">**특성 값** 목록에서 특성 값으로 "user.givenname"을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-179">From the **Attribute Value** list, select the attribute value "user.givenname".</span></span>
 4. <span data-ttu-id="83c0f-180">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-180">Click **Ok**.</span></span>

4. <span data-ttu-id="83c0f-181">**SAP HANA Cloud Platform Identity Authentication 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-181">On the **SAP HANA Cloud Platform Identity Authentication Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_06.png)
 1. <span data-ttu-id="83c0f-183">**로그인 URL** 텍스트 상자에 SAP 응용 프로그램에 대한 로그인 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-183">In the **Sign On URL** textbox, type the sign on URL for the SAP application.</span></span>
 2. <span data-ttu-id="83c0f-184">**식별자** 텍스트 상자에 다음 패턴으로 값을 입력합니다. `<entity-id>.accounts.ondemand.com`</span><span class="sxs-lookup"><span data-stu-id="83c0f-184">In the **Identifier** textbox, type the value following pattern: `<entity-id>.accounts.ondemand.com`</span></span> 
    * <span data-ttu-id="83c0f-185">이 값을 모르는 경우 [Tenant SAML 2.0 구성](https://help.hana.ondemand.com/cloud_identity/frameset.htm?e81a19b0067f4646982d7200a8dab3ca.html)에서 SAP HANA Cloud Platform Identity Authentication 설명서를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="83c0f-185">If you don't know this value, please follow the SAP HANA Cloud Platform Identity Authentication documentation on [Tenant SAML 2.0 Configuration](https://help.hana.ondemand.com/cloud_identity/frameset.htm?e81a19b0067f4646982d7200a8dab3ca.html).</span></span>

5. <span data-ttu-id="83c0f-186">**SAP HANA Cloud Platform Identity Authentication 구성** 섹션에서 **SAP HANA Cloud Platform Identity Authentication 구성**을 클릭하여 **로그온 구성** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-186">On the **SAP HANA Cloud Platform Identity Authentication Configuration** section, click **Configure SAP HANA Cloud Platform Identity Authentication** to open **Configure sign-on** dialog.</span></span> <span data-ttu-id="83c0f-187">**SAML XML 메타데이터**를 클릭한 후, 컴퓨터에 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-187">Then, click on **SAML XML Metadata** and save the file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_07.png) 

    ![Single Sign-on 구성](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_08.png)

6. <span data-ttu-id="83c0f-190">응용 프로그램에 대해 SSO를 구성하려면 SAP HANA Cloud Platform Identity Authentication 관리 콘솔로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-190">To get SSO configured for your application, go to SAP HANA Cloud Platform Identity Authentication Administration Console.</span></span> <span data-ttu-id="83c0f-191">URL 패턴은 다음과 같습니다. `https://<tenant-id>.accounts.ondemand.com/admin`</span><span class="sxs-lookup"><span data-stu-id="83c0f-191">The URL has the following pattern: `https://<tenant-id>.accounts.ondemand.com/admin`</span></span>
 * <span data-ttu-id="83c0f-192">그런 다음 SAP HANA Cloud Platform Identity Authentication 설명서에 따라 [SAP HANA Cloud Platform Identity Authentication에서 기업 ID 공급자로 Microsoft Azure AD를 구성](https://help.hana.ondemand.com/cloud_identity/frameset.htm?626b17331b4d4014b8790d3aea70b240.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-192">Then, follow the documentation on SAP HANA Cloud Platform Identity Authentication to [Configure Microsoft Azure AD as Corporate Identity Provider at SAP HANA Cloud Platform Identity Authentication](https://help.hana.ondemand.com/cloud_identity/frameset.htm?626b17331b4d4014b8790d3aea70b240.html).</span></span> 

7. <span data-ttu-id="83c0f-193">Azure 관리 포털에서 **저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-193">In the Azure Management portal, click **Save** button.</span></span>
8. <span data-ttu-id="83c0f-194">다른 SAP 응용 프로그램에 대해 SSO를 추가하고 사용하도록 설정하려는 경우에만 다음 단계를 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-194">Continue the following steps only if you want to add and enable SSO for another SAP application.</span></span> <span data-ttu-id="83c0f-195">SAP HANA Cloud Platform Identity Authentication의 다른 인스턴스를 추가하려면 "갤러리에서 SAP HANA Cloud Platform Identity Authentication 추가" 섹션의 단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-195">Repeat steps under the section “Adding SAP HANA Cloud Platform Identity Authentication from the gallery” to add another instance of SAP HANA Cloud Platform Identity Authentication.</span></span>
9. <span data-ttu-id="83c0f-196">Azure 관리 포털의 **SAP HANA Cloud Platform Identity Authentication** 응용 프로그램 통합 페이지에서 **연결된 로그온**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-196">In the Azure Management portal, on the **SAP HANA Cloud Platform Identity Authentication** application integration page, click **Linked Sign-on**.</span></span>

    ![연결된 로그온 구성](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/linked_sign_on.png)
10. <span data-ttu-id="83c0f-198">그런 다음 구성을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-198">Then, save the configuration.</span></span>

>[!NOTE] 
><span data-ttu-id="83c0f-199">새 응용 프로그램은 이전 SAP 응용 프로그램의 SSO 구성을 활용합니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-199">The new application will leverage the SSO configuration for the previous SAP application.</span></span> <span data-ttu-id="83c0f-200">SAP HANA Cloud Platform Identity Authentication 관리 콘솔에서 동일한 회사 ID 공급자를 사용하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-200">Please make sure you use the same Corporate Identity Providers in the SAP HANA Cloud Platform Identity Authentication Administration Console.</span></span>
>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="83c0f-201">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="83c0f-201">Create an Azure AD test user</span></span>
<span data-ttu-id="83c0f-202">이 섹션의 목적은 새로운 포털에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-202">The objective of this section is to create a test user in the new portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="83c0f-204">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="83c0f-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="83c0f-205">**Azure 관리 포털**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-205">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="83c0f-207">**사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭하여 사용자 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-207">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="83c0f-209">대화 상자 위쪽에서 **추가**를 클릭하여 **사용자** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-209">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="83c0f-211">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-211">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_04.png) 
  1. <span data-ttu-id="83c0f-213">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-213">In the **Name** textbox, type **BrittaSimon**.</span></span>
  2. <span data-ttu-id="83c0f-214">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-214">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>
  3. <span data-ttu-id="83c0f-215">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-215">Select **Show Password** and write down the value of the **Password**.</span></span>
  4. <span data-ttu-id="83c0f-216">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-216">Click **Create**.</span></span> 

### <a name="create-a-sap-hana-cloud-platform-identity-authentication-test-user"></a><span data-ttu-id="83c0f-217">SAP HANA Cloud Platform Identity Authentication 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="83c0f-217">Create a SAP HANA Cloud Platform Identity Authentication test user</span></span>

<span data-ttu-id="83c0f-218">SAP HANA Cloud Platform Identity Authentication에서 사용자를 만들 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-218">You don't need to create an user on SAP HANA Cloud Platform Identity Authentication.</span></span> <span data-ttu-id="83c0f-219">Azure AD 사용자 저장소에 있는 사용자는 SSO 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-219">Users who are in the Azure AD user store can use the SSO functionality.</span></span>

<span data-ttu-id="83c0f-220">SAP HANA Cloud Platform Identity Authentication에서는 ID 페더레이션 옵션을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-220">SAP HANA Cloud Platform Identity Authentication supports the Identity Federation option.</span></span> <span data-ttu-id="83c0f-221">이 옵션을 통해 응용 프로그램에서 기업 ID 공급자가 인증한 사용자가 SAP HANA Cloud Platform Identity Authentication의 사용자 저장소에 있는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-221">This option allows the application to check if the users authenticated by the corporate identity provider exist in the user store of SAP HANA Cloud Platform Identity Authentication.</span></span> 

<span data-ttu-id="83c0f-222">기본 설정에서는 ID 페더레이션 옵션을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-222">In the default setting, the Identity Federation option is disabled.</span></span> <span data-ttu-id="83c0f-223">ID 페더레이션이 사용된 경우 SAP HANA Cloud Platform Identity Authentication에서 가져온 사용자만 응용 프로그램에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-223">If Identity Federation is enabled, only the users that are imported in SAP HANA Cloud Platform Identity Authentication are able to access the application.</span></span> 

<span data-ttu-id="83c0f-224">SAP HANA Cloud Platform Identity Authentication에서 ID 페더레이션을 사용 또는 사용하지 않도록 설정하는 방법에 대한 자세한 내용은 [SAP HANA Cloud Platform Identity Authentication의 사용자 저장소에서 ID 페더레이션 구성](https://help.hana.ondemand.com/cloud_identity/frameset.htm?c029bbbaefbf4350af15115396ba14e2.html)의 SAP HANA Cloud Platform Identity Authentication으로 ID 페더레이션 설정을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="83c0f-224">For more information about how to enable or disable Identity Federation with SAP HANA Cloud Platform Identity Authentication, see Enable Identity Federation with SAP HANA Cloud Platform Identity Authentication in [Configure Identity Federation with the User Store of SAP HANA Cloud Platform Identity Authentication.](https://help.hana.ondemand.com/cloud_identity/frameset.htm?c029bbbaefbf4350af15115396ba14e2.html).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="83c0f-225">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="83c0f-225">Assign the Azure AD test user</span></span>

<span data-ttu-id="83c0f-226">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 SAP HANA Cloud Platform Identity Authentication에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-226">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to SAP HANA Cloud Platform Identity Authentication.</span></span>

![사용자 할당][200] 

<span data-ttu-id="83c0f-228">**SAP HANA Cloud Platform Identity Authentication에 Britta Simon을 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="83c0f-228">**To assign Britta Simon to SAP HANA Cloud Platform Identity Authentication, perform the following steps:**</span></span>

1. <span data-ttu-id="83c0f-229">Azure 관리 포털에서 응용 프로그램 보기를 열고 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-229">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="83c0f-231">응용 프로그램 목록에서 **SAP HANA Cloud Platform Identity Authentication**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-231">In the applications list, select **SAP HANA Cloud Platform Identity Authentication**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_09.png)

3. <span data-ttu-id="83c0f-233">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-233">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="83c0f-235">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-235">Click **Add** button.</span></span> <span data-ttu-id="83c0f-236">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="83c0f-238">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="83c0f-239">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="83c0f-240">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    

### <a name="test-single-sign-on"></a><span data-ttu-id="83c0f-241">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="83c0f-241">Test single sign-on</span></span>

<span data-ttu-id="83c0f-242">이 섹션에서는 액세스 패널을 사용하여 Azure AD SSO 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-242">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="83c0f-243">액세스 패널에서 SAP HANA Cloud Platform Identity Authentication 타일을 클릭하면 SAP HANA Cloud Platform Identity Authentication 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="83c0f-243">When you click the SAP HANA Cloud Platform Identity Authentication tile in the Access Panel, you should get automatically signed-on to your SAP HANA Cloud Platform Identity Authentication application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="83c0f-244">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="83c0f-244">Additional resources</span></span>

* [<span data-ttu-id="83c0f-245">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="83c0f-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="83c0f-246">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="83c0f-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_05.png
[6]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_06.png

[100]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_203.png