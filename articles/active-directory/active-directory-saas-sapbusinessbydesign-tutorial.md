---
title: "자습서: SAP Business ByDesign과 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory 및 SAP Business ByDesign 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 82938920-33ba-47cb-b141-511b46d19e66
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: ab76a0ac1ef954efd3c66e6f565514b889ed9444
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-business-bydesign"></a><span data-ttu-id="d540b-103">자습서: SAP Business ByDesign과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="d540b-103">Tutorial: Azure Active Directory integration with SAP Business ByDesign</span></span>

<span data-ttu-id="d540b-104">이 자습서에서는 Azure AD(Azure Active Directory)와 SAP Business ByDesign을 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-104">In this tutorial, you learn how to integrate SAP Business ByDesign with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d540b-105">SAP Business ByDesign을 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-105">Integrating SAP Business ByDesign with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d540b-106">SAP Business ByDesign에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-106">You can control in Azure AD who has access to SAP Business ByDesign.</span></span>
- <span data-ttu-id="d540b-107">사용자가 해당 Azure AD 계정으로 SAP Business ByDesign에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-107">You can enable your users to automatically get signed-on to SAP Business ByDesign (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="d540b-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="d540b-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d540b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d540b-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d540b-110">Prerequisites</span></span>

<span data-ttu-id="d540b-111">SAP Business ByDesign과 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-111">To configure Azure AD integration with SAP Business ByDesign, you need the following items:</span></span>

- <span data-ttu-id="d540b-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="d540b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d540b-113">SAP Business ByDesign Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="d540b-113">An SAP Business ByDesign single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d540b-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d540b-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d540b-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="d540b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d540b-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d540b-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="d540b-118">Scenario description</span></span>
<span data-ttu-id="d540b-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d540b-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d540b-121">갤러리에서 SAP Business ByDesign 추가</span><span class="sxs-lookup"><span data-stu-id="d540b-121">Adding SAP Business ByDesign from the gallery</span></span>
2. <span data-ttu-id="d540b-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="d540b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sap-business-bydesign-from-the-gallery"></a><span data-ttu-id="d540b-123">갤러리에서 SAP Business ByDesign 추가</span><span class="sxs-lookup"><span data-stu-id="d540b-123">Adding SAP Business ByDesign from the gallery</span></span>
<span data-ttu-id="d540b-124">SAP Business ByDesign의 Azure AD 통합을 구성하려면 갤러리의 SAP Business ByDesign을 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-124">To configure the integration of SAP Business ByDesign into Azure AD, you need to add SAP Business ByDesign from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d540b-125">**갤러리에서 SAP Business ByDesign을 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="d540b-125">**To add SAP Business ByDesign from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d540b-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory 단추][1]

2. <span data-ttu-id="d540b-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d540b-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-129">Then go to **All applications**.</span></span>

    ![엔터프라이즈 응용 프로그램 블레이드][2]
    
3. <span data-ttu-id="d540b-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![새 응용 프로그램 단추][3]

4. <span data-ttu-id="d540b-133">검색 상자에 **SAP Business ByDesign**을 입력하고 결과 패널에서 **SAP Business ByDesign**을 선택한 후 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-133">In the search box, type **SAP Business ByDesign**, select **SAP Business ByDesign** from result panel then click **Add** button to add the application.</span></span>

    ![결과 목록의 SAP Business ByDesign](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="d540b-135">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="d540b-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="d540b-136">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 SAP Business ByDesign에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-136">In this section, you configure and test Azure AD single sign-on with SAP Business ByDesign based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d540b-137">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 SAP Business ByDesign 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-137">For single sign-on to work, Azure AD needs to know what the counterpart user in SAP Business ByDesign is to a user in Azure AD.</span></span> <span data-ttu-id="d540b-138">즉, Azure AD 사용자와 SAP Business ByDesign의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-138">In other words, a link relationship between an Azure AD user and the related user in SAP Business ByDesign needs to be established.</span></span>

<span data-ttu-id="d540b-139">SAP Business ByDesign에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 연결 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-139">In SAP Business ByDesign, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d540b-140">SAP Business ByDesign에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-140">To configure and test Azure AD single sign-on with SAP Business ByDesign, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d540b-141">**[Azure AD Single Sign-On 구성](#configure-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d540b-142">**[Azure AD 테스트 사용자 만들기](#create-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d540b-143">**[SAP Business ByDesign 테스트 사용자 만들기](#create-an-sap-business-bydesign-test-user)** - Azure AD를 대표하여 SAP Business ByDesign에서 Britta Simon에 해당하는 사용자가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-143">**[Create an SAP Business ByDesign test user](#create-an-sap-business-bydesign-test-user)** - to have a counterpart of Britta Simon in SAP Business ByDesign that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d540b-144">**[Azure AD 테스트 사용자 할당](#assign-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d540b-145">**[Single Sign-On 테스트](#test-single-sign-on)** - 구성이 작동하는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="d540b-146">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="d540b-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="d540b-147">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 SAP Business ByDesign 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SAP Business ByDesign application.</span></span>

<span data-ttu-id="d540b-148">**SAP Business ByDesign에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="d540b-148">**To configure Azure AD single sign-on with SAP Business ByDesign, perform the following steps:**</span></span>

1. <span data-ttu-id="d540b-149">Azure Portal의 **SAP Business ByDesign** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-149">In the Azure portal, on the **SAP Business ByDesign** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-On 구성 링크][4]

2. <span data-ttu-id="d540b-151">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_samlbase.png)

3. <span data-ttu-id="d540b-153">**SAP Business ByDesign 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-153">On the **SAP Business ByDesign Domain and URLs** section, perform the following steps:</span></span>

    ![SAP Business ByDesign 도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_url.png)

    <span data-ttu-id="d540b-155">a.</span><span class="sxs-lookup"><span data-stu-id="d540b-155">a.</span></span> <span data-ttu-id="d540b-156">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<servername>.sapbydesign.com`</span><span class="sxs-lookup"><span data-stu-id="d540b-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<servername>.sapbydesign.com`</span></span>

    <span data-ttu-id="d540b-157">b.</span><span class="sxs-lookup"><span data-stu-id="d540b-157">b.</span></span> <span data-ttu-id="d540b-158">**식별자** 텍스트 상자에서 `https://<servername>.sapbydesign.com` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<servername>.sapbydesign.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d540b-159">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-159">These values are not real.</span></span> <span data-ttu-id="d540b-160">실제 로그온 URL 및 식별자로 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="d540b-161">이러한 값을 얻으려면 [SAP Business ByDesign 클라이언트 지원 팀](https://www.sap.com/products/cloud-analytics.support.html)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="d540b-161">Contact [SAP Business ByDesign Client support team](https://www.sap.com/products/cloud-analytics.support.html) to get these values.</span></span>

4. <span data-ttu-id="d540b-162">**사용자 특성** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-162">On the **User Attributes** section, perform the following steps:</span></span>

    ![SAP Business ByDesign 특성 섹션](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_attribute.png)
    
    <span data-ttu-id="d540b-164">a.</span><span class="sxs-lookup"><span data-stu-id="d540b-164">a.</span></span> <span data-ttu-id="d540b-165">**사용자 ID** 목록에서 **ExtractMailPrefix()** 함수를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-165">In **User Identifier** list, select the **ExtractMailPrefix()** function.</span></span>
    
    <span data-ttu-id="d540b-166">b.</span><span class="sxs-lookup"><span data-stu-id="d540b-166">b.</span></span> <span data-ttu-id="d540b-167">**메일** 목록에서 구현에 사용할 사용자 특성을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-167">From the **Mail** list, select the user attribute you want to use for your implementation.</span></span> <span data-ttu-id="d540b-168">예를 들어, EmployeeID를 고유한 사용자 식별자로 사용하고자 하고 ExtensionAttribute2에 특성 값을 저장했다면 user.extensionattribute2를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-168">For example, if you want to use the EmployeeID as unique user identifier and you have stored the attribute value in the ExtensionAttribute2, then select user.extensionattribute2.</span></span>     

5. <span data-ttu-id="d540b-169">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 메타데이터 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-169">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![인증서 다운로드 링크](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_certificate.png) 

6. <span data-ttu-id="d540b-171">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-171">Click **Save** button.</span></span>

    ![Single Sign-On 구성 저장 단추](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="d540b-173">**SAP Business ByDesign 구성** 섹션에서 **SAP Business ByDesign 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-173">On the **SAP Business ByDesign Configuration** section, click **Configure SAP Business ByDesign** to open **Configure sign-on** window.</span></span> <span data-ttu-id="d540b-174">**빠른 참조 섹션**에서 **SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-174">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![SAP Business ByDesign 구성](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_configure.png) 

8. <span data-ttu-id="d540b-176">응용 프로그램에 SSO를 구성하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-176">To get SSO configured for your application, perform the following steps:</span></span>
   
    <span data-ttu-id="d540b-177">a.</span><span class="sxs-lookup"><span data-stu-id="d540b-177">a.</span></span> <span data-ttu-id="d540b-178">관리자 권한으로 SAP Business ByDesign 포털에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-178">Sign on to your SAP Business ByDesign portal with administrator rights.</span></span>
   
    <span data-ttu-id="d540b-179">b.</span><span class="sxs-lookup"><span data-stu-id="d540b-179">b.</span></span> <span data-ttu-id="d540b-180">**응용 프로그램 및 사용자 관리 일반 작업**으로 이동하여 **ID 공급자** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-180">Navigate to **Application and User Management Common Task** and click the **Identity Provider** tab.</span></span>
   
    <span data-ttu-id="d540b-181">c.</span><span class="sxs-lookup"><span data-stu-id="d540b-181">c.</span></span> <span data-ttu-id="d540b-182">**새 ID 공급자**를 클릭하고 Azure Portal에서 다운로드한 메타데이터 XML 파일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-182">Click **New Identity Provider** and select the metadata XML file that you have downloaded from the Azure portal.</span></span> <span data-ttu-id="d540b-183">시스템은 메타데이터를 가져와서 필수 서명 인증서 및 암호화 인증서를 자동으로 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-183">By importing the metadata, the system automatically uploads the required signature certificate and encryption certificate.</span></span>
   
    ![Single Sign-On 구성](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_54.png)
   
    <span data-ttu-id="d540b-185">d.</span><span class="sxs-lookup"><span data-stu-id="d540b-185">d.</span></span> <span data-ttu-id="d540b-186">**어설션 소비자 서비스 URL**을 SAML 요청에 포함하려면 **어설션 소비자 서비스 URL 포함**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-186">To include the **Assertion Consumer Service URL** into the SAML request, select **Include Assertion Consumer Service URL**.</span></span>
   
    <span data-ttu-id="d540b-187">e.</span><span class="sxs-lookup"><span data-stu-id="d540b-187">e.</span></span> <span data-ttu-id="d540b-188">**Single Sign-on 활성화**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-188">Click **Activate Single Sign-On**.</span></span>
   
    <span data-ttu-id="d540b-189">f.</span><span class="sxs-lookup"><span data-stu-id="d540b-189">f.</span></span> <span data-ttu-id="d540b-190">변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-190">Save your changes.</span></span>
   
    <span data-ttu-id="d540b-191">g.</span><span class="sxs-lookup"><span data-stu-id="d540b-191">g.</span></span> <span data-ttu-id="d540b-192">**내 시스템** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-192">Click the **My System** tab.</span></span>
   
    ![Single Sign-On 구성](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_52.png)
   
    <span data-ttu-id="d540b-194">h.</span><span class="sxs-lookup"><span data-stu-id="d540b-194">h.</span></span> <span data-ttu-id="d540b-195">Azure Portal에서 복사한 **SAML Single Sign-On 서비스 URL**을 **Azure AD 로그온 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-195">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal it into the **Azure AD Sign On URL** textbox.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_53.png)
   
    <span data-ttu-id="d540b-197">i.</span><span class="sxs-lookup"><span data-stu-id="d540b-197">i.</span></span> <span data-ttu-id="d540b-198">직원이 **수동 ID 공급자 선택**을 선택하여 사용자 ID 및 암호 또는 SSO를 사용하는 로그온 중 하나를 수동으로 선택할 수 있는지 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-198">Specify whether the employee can manually choose between logging on with user ID and password or SSO by selecting **Manual Identity Provider Selection**.</span></span>
   
    <span data-ttu-id="d540b-199">j.</span><span class="sxs-lookup"><span data-stu-id="d540b-199">j.</span></span> <span data-ttu-id="d540b-200">**SSO URL** 섹션에서 시스템에 로그온하려는 직원이 사용해야 하는 URL을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-200">In the **SSO URL** section, specify the URL that should be used by the employee to logon to the system.</span></span> 
    <span data-ttu-id="d540b-201">직원에게 전송된 URL 드롭다운 목록에서 다음 옵션 중 하나를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-201">In the URL Sent to Employee dropdown list, you can choose between the following options:</span></span>
   
    <span data-ttu-id="d540b-202">**SSO가 아닌 URL**</span><span class="sxs-lookup"><span data-stu-id="d540b-202">**Non-SSO URL**</span></span>
   
    <span data-ttu-id="d540b-203">시스템은 직원에게 정상적인 시스템 URL만을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-203">The system sends only the normal system URL to the employee.</span></span> <span data-ttu-id="d540b-204">직원은 SSO를 사용하여 로그온할 수 없고 대신 암호 또는 인증서를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-204">The employee cannot log on using SSO, and must use password or certificate instead.</span></span>
   
    <span data-ttu-id="d540b-205">**SSO URL**</span><span class="sxs-lookup"><span data-stu-id="d540b-205">**SSO URL**</span></span> 
   
    <span data-ttu-id="d540b-206">시스템은 직원에게 SSO URL만을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-206">The system sends only the SSO URL to the employee.</span></span> <span data-ttu-id="d540b-207">직원은 SSO를 사용하여 로그온할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-207">The employee can log on using SSO.</span></span> <span data-ttu-id="d540b-208">IdP를 통해 인증 요청이 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-208">Authentication request is redirected through the IdP.</span></span>
   
    <span data-ttu-id="d540b-209">**자동 선택**</span><span class="sxs-lookup"><span data-stu-id="d540b-209">**Automatic Selection**</span></span>
   
    <span data-ttu-id="d540b-210">SSO가 활성 상태가 아닌 경우 시스템은 직원에게 정상적인 시스템 URL을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-210">If SSO is not active, the system sends the normal system URL to the employee.</span></span> <span data-ttu-id="d540b-211">SSO가 활성 상태인 경우 시스템은 직원이 암호를 가지는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-211">If SSO is active, the system checks whether the employee has a password.</span></span> <span data-ttu-id="d540b-212">암호를 사용할 수 있는 경우 SSO URL와 SSO가 아닌 URL은 직원에게 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-212">If a password is available, both SSO URL and Non-SSO URL are sent to the employee.</span></span> <span data-ttu-id="d540b-213">그러나 직원에게 암호가 없는 경우 SSO URL만이 직원에게 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-213">However, if the employee has no password, only the SSO URL is sent to the employee.</span></span>
   
    <span data-ttu-id="d540b-214">k.</span><span class="sxs-lookup"><span data-stu-id="d540b-214">k.</span></span> <span data-ttu-id="d540b-215">변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-215">Save your changes.</span></span>

> [!TIP]
> <span data-ttu-id="d540b-216">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-216">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d540b-217">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-217">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d540b-218">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-218">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="d540b-219">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="d540b-219">Create an Azure AD test user</span></span>

<span data-ttu-id="d540b-220">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-220">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Azure AD 테스트 사용자 만들기][100]

<span data-ttu-id="d540b-222">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="d540b-222">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d540b-223">Azure Portal의 왼쪽 창에서 **Azure Active Directory** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-223">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Azure Active Directory 단추](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="d540b-225">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-225">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !["사용자 및 그룹" 및 "모든 사용자" 링크](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="d540b-227">**사용자** 대화 상자를 열려면 **모든 사용자** 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-227">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![추가 단추](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="d540b-229">**사용자** 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-229">In the **User** dialog box, perform the following steps:</span></span>

    ![사용자 대화 상자](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_04.png)

    <span data-ttu-id="d540b-231">a.</span><span class="sxs-lookup"><span data-stu-id="d540b-231">a.</span></span> <span data-ttu-id="d540b-232">**이름** 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-232">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d540b-233">b.</span><span class="sxs-lookup"><span data-stu-id="d540b-233">b.</span></span> <span data-ttu-id="d540b-234">**사용자 이름** 상자에 사용자인 Britta Simon의 전자 메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-234">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="d540b-235">c.</span><span class="sxs-lookup"><span data-stu-id="d540b-235">c.</span></span> <span data-ttu-id="d540b-236">**암호 표시** 확인란을 선택한 다음 **암호** 상자에 표시된 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-236">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="d540b-237">d.</span><span class="sxs-lookup"><span data-stu-id="d540b-237">d.</span></span> <span data-ttu-id="d540b-238">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-238">Click **Create**.</span></span>
 
### <a name="create-an-sap-business-bydesign-test-user"></a><span data-ttu-id="d540b-239">SAP Business ByDesign 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="d540b-239">Create an SAP Business ByDesign test user</span></span>

<span data-ttu-id="d540b-240">이 섹션에서는 SAP Business ByDesign에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-240">In this section, you create a user called Britta Simon in SAP Business ByDesign.</span></span> <span data-ttu-id="d540b-241">[SAP Business ByDesign 클라이언트 지원 팀](https://www.sap.com/products/cloud-analytics.support.html)과 협력하여 SAP Business ByDesign 플랫폼에 사용자를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-241">Please work with [SAP Business ByDesign Client support team](https://www.sap.com/products/cloud-analytics.support.html) to add the users in the SAP Business ByDesign platform.</span></span> 

> [!NOTE]
> <span data-ttu-id="d540b-242">NameID 값이 SAP Business ByDesign 플랫폼에서 사용자 이름 필드와 일치하는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="d540b-242">Please make sure that NameID value should match with the username field in the SAP Business ByDesign platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="d540b-243">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="d540b-243">Assign the Azure AD test user</span></span>

<span data-ttu-id="d540b-244">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 SAP Business ByDesign에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-244">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SAP Business ByDesign.</span></span>

![사용자 역할 할당][200] 

<span data-ttu-id="d540b-246">**Britta Simon을 SAP Business ByDesign에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="d540b-246">**To assign Britta Simon to SAP Business ByDesign, perform the following steps:**</span></span>

1. <span data-ttu-id="d540b-247">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-247">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="d540b-249">응용 프로그램 목록에서 **SAP Business ByDesign**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-249">In the applications list, select **SAP Business ByDesign**.</span></span>

    ![응용 프로그램 목록의 SAP Business ByDesign 연결](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_app.png)  

3. <span data-ttu-id="d540b-251">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-251">In the menu on the left, click **Users and groups**.</span></span>

    !["사용자 및 그룹" 링크][202]

4. <span data-ttu-id="d540b-253">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-253">Click **Add** button.</span></span> <span data-ttu-id="d540b-254">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![할당 추가 창][203]

5. <span data-ttu-id="d540b-256">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-256">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d540b-257">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d540b-258">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="d540b-259">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="d540b-259">Test single sign-on</span></span>

<span data-ttu-id="d540b-260">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-260">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d540b-261">액세스 패널에서 SAP Business ByDesign 타일을 클릭하면 SAP Business ByDesign 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="d540b-261">When you click the SAP Business ByDesign tile in the Access Panel, you should get automatically signed-on to your SAP Business ByDesign application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d540b-262">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="d540b-262">Additional resources</span></span>

* [<span data-ttu-id="d540b-263">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="d540b-263">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d540b-264">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="d540b-264">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_203.png

