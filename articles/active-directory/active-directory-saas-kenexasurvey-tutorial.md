---
title: "자습서: IBM Kenexa Survey Enterprise와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory 및 IBM Kenexa Survey Enterprise 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c7aac6da-f4bf-419e-9e1a-16b460641a52
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 5c276c23288292a1c54dd9d57177d5072b90c9e3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ibm-kenexa-survey-enterprise"></a><span data-ttu-id="91c11-103">자습서: IBM Kenexa Survey Enterprise와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="91c11-103">Tutorial: Azure Active Directory integration with IBM Kenexa Survey Enterprise</span></span>

<span data-ttu-id="91c11-104">이 자습서에서는 Azure AD(Azure Active Directory)와 IBM Kenexa Survey Enterprise을 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="91c11-104">In this tutorial, you learn how to integrate IBM Kenexa Survey Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="91c11-105">IBM Kenexa Survey Enterprise를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="91c11-105">Integrating IBM Kenexa Survey Enterprise with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="91c11-106">Azure AD에서 사용자의 IBM Kenexa Survey Enterprise에 대한 액세스 권한을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91c11-106">You can control in Azure AD who has access to IBM Kenexa Survey Enterprise.</span></span>
- <span data-ttu-id="91c11-107">사용자가 해당 Azure AD 계정에서 SSO(Single Sign-on)를 사용하여 IBM Kenexa Survey Enterprise에 자동으로 로그인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91c11-107">You can enable your users to automatically sign in to IBM Kenexa Survey Enterprise by using single sign-on (SSO) with their Azure AD accounts.</span></span>
- <span data-ttu-id="91c11-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91c11-108">You can manage your accounts in one central location: the Azure portal.</span></span>

<span data-ttu-id="91c11-109">Azure AD와의 SaaS(Software as a Service) 앱 통합에 대한 자세한 내용은 [Azure Active Directory를 사용한 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="91c11-109">If you want to know more about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="91c11-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="91c11-110">Prerequisites</span></span>

<span data-ttu-id="91c11-111">IBM Kenexa Survey Enterprise와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="91c11-111">To configure Azure AD integration with IBM Kenexa Survey Enterprise, you need the following items:</span></span>

- <span data-ttu-id="91c11-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="91c11-112">An Azure AD subscription</span></span>
- <span data-ttu-id="91c11-113">IBM Kenexa Survey Enterprise SSO가 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="91c11-113">An IBM Kenexa Survey Enterprise SSO-enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="91c11-114">이 자습서의 단계를 테스트하는 경우 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="91c11-114">When you test the steps in this tutorial, we recommend that you do not use a production environment.</span></span>

<span data-ttu-id="91c11-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="91c11-115">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="91c11-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="91c11-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="91c11-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91c11-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="91c11-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="91c11-118">Scenario description</span></span>
<span data-ttu-id="91c11-119">이 자습서에서는 테스트 환경에서 Azure AD SSO를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="91c11-119">In this tutorial, you test Azure AD SSO in a test environment.</span></span> <span data-ttu-id="91c11-120">자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91c11-120">The scenario outlined in the tutorial consists of two main building blocks:</span></span>

* <span data-ttu-id="91c11-121">갤러리에서 IBM Kenexa Survey Enterprise 추가</span><span class="sxs-lookup"><span data-stu-id="91c11-121">Adding IBM Kenexa Survey Enterprise from the gallery</span></span>
* <span data-ttu-id="91c11-122">Azure AD SSO 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="91c11-122">Configuring and testing Azure AD SSO</span></span>

## <a name="add-ibm-kenexa-survey-enterprise-from-the-gallery"></a><span data-ttu-id="91c11-123">갤러리에서 IBM Kenexa Survey Enterprise 추가</span><span class="sxs-lookup"><span data-stu-id="91c11-123">Add IBM Kenexa Survey Enterprise from the gallery</span></span>
<span data-ttu-id="91c11-124">Azure AD에 IBM Kenexa Survey Enterprise의 통합을 구성하려면 갤러리의 IBM Kenexa Survey Enterprise를 관리되는 SaaS 앱 목록에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="91c11-124">To configure the integration of IBM Kenexa Survey Enterprise into Azure AD, add IBM Kenexa Survey Enterprise from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="91c11-125">갤러리의 IBM Kenexa Survey Enterprise를 추가하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="91c11-125">To add IBM Kenexa Survey Enterprise from the gallery, do the following:</span></span>

1. <span data-ttu-id="91c11-126">[Azure Portal](https://portal.azure.com)의 왼쪽 창에서 **Azure Active Directory** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="91c11-126">In the [Azure portal](https://portal.azure.com), in the left pane, click the **Azure Active Directory** button.</span></span> 

    ![Azure Active Directory 단추][1]

2. <span data-ttu-id="91c11-128">**엔터프라이즈 응용 프로그램**을 선택한 다음 **모든 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="91c11-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![엔터프라이즈 응용 프로그램 블레이드][2]
    
3. <span data-ttu-id="91c11-130">응용 프로그램을 추가하려면 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="91c11-130">To add an application, click the **New application** button.</span></span>

    ![새 응용 프로그램 단추][3]

4. <span data-ttu-id="91c11-132">검색 상자에 **IBM Kenexa Survey Enterprise**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="91c11-132">In the search box, type **IBM Kenexa Survey Enterprise**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_search.png)

5. <span data-ttu-id="91c11-134">결과 목록에서 **IBM Kenexa Survey Enterprise**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="91c11-134">In the results list, select **IBM Kenexa Survey Enterprise**, and then click the **Add** button to add the application.</span></span>

    ![결과 목록의 IBM Kenexa Survey Enterprise](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="91c11-136">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="91c11-136">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="91c11-137">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 IBM Kenexa Survey Enterprise에서 Azure AD SSO를 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="91c11-137">In this section, you configure and test Azure AD SSO with IBM Kenexa Survey Enterprise based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="91c11-138">SSO가 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 IBM Kenexa Survey Enterprise 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91c11-138">For SSO to work, Azure AD needs to identify the IBM Kenexa Survey Enterprise user counterpart in Azure AD.</span></span> <span data-ttu-id="91c11-139">즉, Azure AD에서는 Azure AD 사용자와 IBM Kenexa Survey Enterprise의 관련 사용자 간에 연결을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91c11-139">In other words, Azure AD must establish a link relationship between an Azure AD user and a related user in IBM Kenexa Survey Enterprise.</span></span>

<span data-ttu-id="91c11-140">링크 관계를 설정하려면 IBM Kenexa Survey Enterprise의 **사용자 이름** 값을 Azure AD의 **Username** 값으로 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="91c11-140">To establish the link relationship, assign the value of the **user name** in IBM Kenexa Survey Enterprise as the value of the **Username** in Azure AD.</span></span>

<span data-ttu-id="91c11-141">IBM Kenexa Survey Enterprise에서 Azure AD SSO를 구성하고 테스트하려면 다음 두 개의 섹션에서 구성 요소를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="91c11-141">To configure and test Azure AD SSO with IBM Kenexa Survey Enterprise, complete the building blocks in the next two sections.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="91c11-142">Azure AD SSO 구성</span><span class="sxs-lookup"><span data-stu-id="91c11-142">Configure Azure AD SSO</span></span>

<span data-ttu-id="91c11-143">이 섹션에서는 Azure Portal에서 Azure AD SSO를 사용하도록 설정하고 다음을 수행하여 IBM Kenexa Survey Enterprise 응용 프로그램에서 SSO를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="91c11-143">In this section, you enable Azure AD SSO in the Azure portal and configure SSO in your IBM Kenexa Survey Enterprise application by doing the following:</span></span>

1. <span data-ttu-id="91c11-144">Azure Portal의 **IBM Kenexa Survey Enterprise** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="91c11-144">In the Azure portal, on the **IBM Kenexa Survey Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![IBM Kenexa Survey Enterprise 구성 Single Sign-On 링크][4]

2. <span data-ttu-id="91c11-146">**Single Sign-On** 대화 상자의 **모드** 상자에서 **SAML 기반 로그온**을 선택하여 SSO를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="91c11-146">In the **Single sign-on** dialog box, in the **Mode** box, select **SAML-based Sign-on** to enable SSO.</span></span>
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_samlbase.png)

3. <span data-ttu-id="91c11-148">**IBM Kenexa Survey Enterprise 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="91c11-148">In the **IBM Kenexa Survey Enterprise Domain and URLs** section, perform the following steps:</span></span>

    ![IBM Kenexa Survey Enterprise 도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_url.png)

    <span data-ttu-id="91c11-150">a.</span><span class="sxs-lookup"><span data-stu-id="91c11-150">a.</span></span> <span data-ttu-id="91c11-151">**식별자** 텍스트 상자에서 `https://surveys.kenexa.com/<companycode>` 패턴으로 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="91c11-151">In the **Identifier** textbox, type a URL with the following pattern: `https://surveys.kenexa.com/<companycode>`</span></span>

    <span data-ttu-id="91c11-152">b.</span><span class="sxs-lookup"><span data-stu-id="91c11-152">b.</span></span> <span data-ttu-id="91c11-153">**회신 URL** 텍스트 상자에 다음 패턴으로 URL을 입력합니다. `https://surveys.kenexa.com/<companycode>/tools/sso.asp`</span><span class="sxs-lookup"><span data-stu-id="91c11-153">In the **Reply URL** textbox, type a URL with the following pattern: `https://surveys.kenexa.com/<companycode>/tools/sso.asp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="91c11-154">위의 값은 실제가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="91c11-154">The preceding values are not real.</span></span> <span data-ttu-id="91c11-155">실제 식별자 및 회신 URL로 해당 항목을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="91c11-155">Update them with the actual identifier and reply URL.</span></span> <span data-ttu-id="91c11-156">실제 값을 가져오려면 [IBM Kenexa Survey Enterprise 지원팀](https://www.ibm.com/support/home/?lnk=fcw)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="91c11-156">To obtain the actual values, contact the [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span>

4. <span data-ttu-id="91c11-157">**SAML 서명 인증서** 아래에서 **인증서(Base64)**를 클릭한 후 사용자의 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="91c11-157">Under **SAML Signing Certificate**, click **Certificate (Base64)**, and then save the certificate file to your computer.</span></span>

    ![인증서(Base64) 다운로드 링크](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_certificate.png) 

    <span data-ttu-id="91c11-159">IBM Kenexa Survey Enterprise 응용 프로그램은 특정 형식인 SAML(Security Assertions Markup Language) 어설션을 수신하므로, SAML 토큰 특성 구성에 사용자 지정 특성 매핑을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91c11-159">The IBM Kenexa Survey Enterprise application expects to receive the Security Assertions Markup Language (SAML) assertions in a specific format, which requires you to add custom attribute mappings to the configuration of your SAML token attributes.</span></span> <span data-ttu-id="91c11-160">응답에서 사용자 ID 클레임의 값은 Kenexa 시스템에서 구성된 SSO ID와 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91c11-160">The value of the user-identifier claim in the response must match the SSO ID that's configured in the Kenexa system.</span></span> <span data-ttu-id="91c11-161">조직에서 적절한 사용자 ID를 SSO IDP(Internet Datagram Protocol)로 매핑하려면 [IBM Kenexa Survey Enterprise 지원팀](https://www.ibm.com/support/home/?lnk=fcw)과 함께 작업하세요.</span><span class="sxs-lookup"><span data-stu-id="91c11-161">To map the appropriate user identifier in your organization as SSO Internet Datagram Protocol (IDP), work with the [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span> 

    <span data-ttu-id="91c11-162">기본적으로 Azure AD는 사용자 ID를 UPN(사용자 계정 이름) 값으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="91c11-162">By default, Azure AD sets the user identifier as the user principal name (UPN) value.</span></span> <span data-ttu-id="91c11-163">아래 스크린샷에 표시된 것처럼 **특성** 탭에서 이 값을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91c11-163">You can change this value on the **Attribute** tab, as shown in the following screenshot.</span></span> <span data-ttu-id="91c11-164">통합은 매핑을 완료한 후에만 정확하게 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="91c11-164">The integration works only after you've completed the mapping correctly.</span></span>
    
    ![사용자 특성 대화 상자](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_attribute.png)   

5. <span data-ttu-id="91c11-166">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="91c11-166">Click **Save**.</span></span>

    ![Single Sign-On 구성 저장 단추](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="91c11-168">**로그온 구성** 창을 열려면 **IBM Kenexa Survey Enterprise 구성** 섹션에서 **IBM Kenexa Survey Enterprise 구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="91c11-168">To open the **Configure sign-on** window, under **IBM Kenexa Survey Enterprise Configuration**, click **Configure IBM Kenexa Survey Enterprise**.</span></span> 
 
    ![IBM Kenexa Survey Enterprise 구성 링크](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_configure.png)

7. <span data-ttu-id="91c11-170">**빠른 참조** 섹션에서 **로그아웃 URL**, **SAML 엔터티 ID** 및 **SAML Single Sign-On 서비스 URL** 값을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="91c11-170">Copy the **Sign-Out URL**, **SAML Entity ID**, and **SAML single sign-on Service URL** values from the **Quick Reference** section.</span></span>

8. <span data-ttu-id="91c11-171">**로그온 구성** 창의 **빠른 참조**에서 **로그아웃 URL**, **SAML 엔터티 ID** 및 **SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="91c11-171">In the **Configure sign-on** window, under **Quick Reference**, copy the **Sign-Out URL**, **SAML Entity ID**, and **SAML single sign-on Service URL** values.</span></span>

9. <span data-ttu-id="91c11-172">**IBM Kenexa Survey Enterprise** 쪽에서 SSO를 구성하려면 다운로드한 **인증서(Base64)**, **로그아웃 URL**, **SAML 엔터티 ID** 및 **SAML Single Sign-On 서비스 URL** 값을 [IBM Kenexa Survey Enterprise 지원팀](https://www.ibm.com/support/home/?lnk=fcw)에 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91c11-172">To configure SSO on the **IBM Kenexa Survey Enterprise** side, send the downloaded **Certificate (Base64)**, **Sign-Out URL**, **SAML Entity ID**, and **SAML single sign-on Service URL** values to the [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span>

> [!TIP]
> <span data-ttu-id="91c11-173">앱을 설정하는 동안 [Azure Portal](https://portal.azure.com)에서 이러한 지침의 간결한 버전을 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91c11-173">You can refer to a concise version of these instructions in the [Azure portal](https://portal.azure.com) while you are setting up the app.</span></span> <span data-ttu-id="91c11-174">**Active Directory** > **엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="91c11-174">After you add the app from the **Active Directory** > **Enterprise Applications** section, simply click the **single sign-on** tab, and then access the embedded documentation through the **Configuration** section at the end.</span></span> <span data-ttu-id="91c11-175">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서](https://go.microsoft.com/fwlink/?linkid=845985)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="91c11-175">To learn more about the embedded documentation feature, see [Azure AD embedded documentation](https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="91c11-176">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="91c11-176">Create an Azure AD test user</span></span>
<span data-ttu-id="91c11-177">이 섹션에서는 다음을 수행하여 Azure Portal에서 테스트 사용자인 Britta Simon을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="91c11-177">In this section, you create test user Britta Simon in the Azure portal by doing the following:</span></span>

![Azure AD 테스트 사용자 만들기][100]

1. <span data-ttu-id="91c11-179">Azure Portal의 왼쪽 창에서 **Azure Active Directory** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="91c11-179">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Azure Active Directory 단추](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="91c11-181">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="91c11-181">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>
    
    !["사용자 및 그룹" 및 "모든 사용자" 링크](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="91c11-183">**사용자** 대화 상자를 열려면 **모든 사용자** 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="91c11-183">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>
 
    ![추가 단추](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="91c11-185">**사용자** 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="91c11-185">In the **User** dialog box, perform the following steps:</span></span>
 
    ![사용자 대화 상자](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="91c11-187">a.</span><span class="sxs-lookup"><span data-stu-id="91c11-187">a.</span></span> <span data-ttu-id="91c11-188">**이름** 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="91c11-188">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="91c11-189">b.</span><span class="sxs-lookup"><span data-stu-id="91c11-189">b.</span></span> <span data-ttu-id="91c11-190">**사용자 이름** 상자에 사용자인 Britta Simon의 전자 메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="91c11-190">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="91c11-191">c.</span><span class="sxs-lookup"><span data-stu-id="91c11-191">c.</span></span> <span data-ttu-id="91c11-192">**암호 표시** 확인란을 선택한 다음 **암호** 상자에 표시된 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="91c11-192">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="91c11-193">d.</span><span class="sxs-lookup"><span data-stu-id="91c11-193">d.</span></span> <span data-ttu-id="91c11-194">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="91c11-194">Click **Create**.</span></span>
 
### <a name="create-an-ibm-kenexa-survey-enterprise-test-user"></a><span data-ttu-id="91c11-195">IBM Kenexa Survey Enterprise 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="91c11-195">Create an IBM Kenexa Survey Enterprise test user</span></span>

<span data-ttu-id="91c11-196">이 섹션에서는 IBM Kenexa Survey Enterprise에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="91c11-196">In this section, you create a user called Britta Simon in IBM Kenexa Survey Enterprise.</span></span> 

<span data-ttu-id="91c11-197">IBM Kenexa Survey Enterprise 시스템에서 사용자를 만들고 여기에 SSO ID를 매핑하려면 [IBM Kenexa Survey Enterprise 지원팀](https://www.ibm.com/support/home/?lnk=fcw)과 함께 작업하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="91c11-197">To create users in the IBM Kenexa Survey Enterprise system and map the SSO ID for them, you can work with the [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span> <span data-ttu-id="91c11-198">또한 이 SSO ID 값을 Azure AD의 사용자 ID 값에 매핑해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91c11-198">This SSO ID value should also be mapped to the user identifier value from Azure AD.</span></span> <span data-ttu-id="91c11-199">**특성** 탭에서 이 기본 설정을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91c11-199">You can change this default setting on the **Attribute** tab.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="91c11-200">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="91c11-200">Assign the Azure AD test user</span></span>

<span data-ttu-id="91c11-201">이 섹션에서는 Azure SSO을 사용할 수 있도록 사용자인 Britta Simon에게 IBM Kenexa Survey Enterprise에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="91c11-201">In this section, you enable user Britta Simon to use Azure SSO by granting access to IBM Kenexa Survey Enterprise.</span></span>

![사용자 역할 할당][200] 

<span data-ttu-id="91c11-203">IBM Kenexa Survey Enterprise에 사용자인 Britta Simon을 할당하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="91c11-203">To assign user Britta Simon to IBM Kenexa Survey Enterprise, do the following:</span></span>

1. <span data-ttu-id="91c11-204">Azure Portal에서 **응용 프로그램** 보기를 열고 **디렉터리** 보기로 이동한 후 **엔터프라이즈 응용 프로그램**을 선택하고 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="91c11-204">In the Azure portal, open the **Applications** view, go to the **Directory** view, select **Enterprise applications**, and then click **All applications**.</span></span>

    !["엔터프라이즈 응용 프로그램" 및 "모든 응용 프로그램" 링크][201] 

2. <span data-ttu-id="91c11-206">**응용 프로그램** 목록에서 **IBM Kenexa Survey Enterprise**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="91c11-206">In the **Applications** list, select **IBM Kenexa Survey Enterprise**.</span></span>

    ![응용 프로그램 목록의 IBM Kenexa Survey Enterprise 링크](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_app.png) 

3. <span data-ttu-id="91c11-208">왼쪽 창에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="91c11-208">In the left pane, click **Users and groups**.</span></span>

    ![“사용자 및 그룹” 링크][202] 

4. <span data-ttu-id="91c11-210">**추가** 단추를 클릭한 다음 **할당 추가** 창에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="91c11-210">Click the **Add** button and then, in the **Add Assignment** pane, select **Users and groups**.</span></span>

    ![할당 추가 창][203]

5. <span data-ttu-id="91c11-212">**사용자 및 그룹** 대화 상자의 **사용자 목록**에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="91c11-212">In the **Users and groups** dialog box, in the **Users** list, select **Britta Simon**.</span></span>

6. <span data-ttu-id="91c11-213">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="91c11-213">In the **Users and groups** dialog box, click the **Select** button.</span></span>

7. <span data-ttu-id="91c11-214">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="91c11-214">In the **Add Assignment** dialog box, click the **Assign** button.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="91c11-215">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="91c11-215">Test single sign-on</span></span>

<span data-ttu-id="91c11-216">이 섹션에서는 액세스 패널을 사용하여 Azure AD SSO 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="91c11-216">In this section, you test your Azure AD SSO configuration by using the Access Panel.</span></span>

<span data-ttu-id="91c11-217">액세스 패널에서 **IBM Kenexa Survey Enterprise** 타일을 클릭하면 IBM Kenexa Survey Enterprise 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="91c11-217">When you click the **IBM Kenexa Survey Enterprise** tile in the Access Panel, you should be automatically signed in to your IBM Kenexa Survey Enterprise application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="91c11-218">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="91c11-218">Additional resources</span></span>

* [<span data-ttu-id="91c11-219">Azure Active Directory를 사용하여 SaaS 앱을 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="91c11-219">List of tutorials on how to integrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="91c11-220">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="91c11-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_203.png

 
