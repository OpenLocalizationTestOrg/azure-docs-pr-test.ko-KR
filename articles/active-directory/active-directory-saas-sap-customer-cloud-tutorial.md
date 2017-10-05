---
title: "자습서: SAP Cloud for Customer와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory 및 SAP Cloud for Customer 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 90154dab-eba2-4563-bcf0-f2acc797ea97
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: e4d945525a45704f34e1d9e742220928a516f341
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-cloud-for-customer"></a><span data-ttu-id="5efdc-103">자습서: SAP Cloud for Customer와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="5efdc-103">Tutorial: Azure Active Directory integration with SAP Cloud for Customer</span></span>

<span data-ttu-id="5efdc-104">이 자습서에서는 Azure AD(Azure Active Directory)와 SAP Cloud for Customer를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-104">In this tutorial, you learn how to integrate SAP Cloud for Customer with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5efdc-105">SAP Cloud for Customer를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-105">Integrating SAP Cloud for Customer with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5efdc-106">SAP Cloud for Customer에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-106">You can control in Azure AD who has access to SAP Cloud for Customer</span></span>
- <span data-ttu-id="5efdc-107">사용자가 해당 Azure AD 계정으로 SAP Cloud for Customer에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-107">You can enable your users to automatically get signed-on to SAP Cloud for Customer (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5efdc-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="5efdc-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5efdc-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5efdc-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="5efdc-110">Prerequisites</span></span>

<span data-ttu-id="5efdc-111">SAP Cloud for Customer와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-111">To configure Azure AD integration with SAP Cloud for Customer, you need the following items:</span></span>

- <span data-ttu-id="5efdc-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="5efdc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5efdc-113">SAP Cloud for Customer Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="5efdc-113">A SAP Cloud for Customer single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5efdc-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5efdc-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5efdc-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="5efdc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5efdc-117">Azure AD 평가판 환경이 없으면 [평가판 제품](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5efdc-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="5efdc-118">Scenario description</span></span>
<span data-ttu-id="5efdc-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5efdc-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5efdc-121">갤러리에서 SAP Cloud for Customer 추가</span><span class="sxs-lookup"><span data-stu-id="5efdc-121">Adding SAP Cloud for Customer from the gallery</span></span>
2. <span data-ttu-id="5efdc-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="5efdc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sap-cloud-for-customer-from-the-gallery"></a><span data-ttu-id="5efdc-123">갤러리에서 SAP Cloud for Customer 추가</span><span class="sxs-lookup"><span data-stu-id="5efdc-123">Adding SAP Cloud for Customer from the gallery</span></span>
<span data-ttu-id="5efdc-124">SAP Cloud for Customer의 Azure AD 통합을 구성하려면 갤러리의 SAP Cloud for Customer를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-124">To configure the integration of SAP Cloud for Customer into Azure AD, you need to add SAP Cloud for Customer from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5efdc-125">**갤러리에서 SAP Cloud for Customer를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="5efdc-125">**To add SAP Cloud for Customer from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5efdc-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5efdc-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5efdc-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="5efdc-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="5efdc-133">검색 상자에 **SAP Cloud for Customer**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-133">In the search box, type **SAP Cloud for Customer**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_search.png)

5. <span data-ttu-id="5efdc-135">결과 창에서 **SAP Cloud for Customer**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-135">In the results panel, select **SAP Cloud for Customer**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5efdc-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="5efdc-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5efdc-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 SAP Cloud for Customer에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-138">In this section, you configure and test Azure AD single sign-on with SAP Cloud for Customer based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5efdc-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 SAP Cloud for Customer 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SAP Cloud for Customer is to a user in Azure AD.</span></span> <span data-ttu-id="5efdc-140">즉, Azure AD 사용자와 SAP Cloud for Customer의 관련 사용자 간에 연결 관계가 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-140">In other words, a link relationship between an Azure AD user and the related user in SAP Cloud for Customer needs to be established.</span></span>

<span data-ttu-id="5efdc-141">SAP Cloud for Customer에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-141">In SAP Cloud for Customer, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="5efdc-142">SAP Cloud for Customer에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-142">To configure and test Azure AD single sign-on with SAP Cloud for Customer, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5efdc-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5efdc-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5efdc-145">**[SAP Cloud for Customer 테스트 사용자 만들기](#creating-a-sap-cloud-for-customer-test-user)** - Azure AD를 대표하여 SAP Cloud for Customer에서 Britta Simon에 해당하는 사용자가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-145">**[Creating a SAP Cloud for Customer test user](#creating-a-sap-cloud-for-customer-test-user)** - to have a counterpart of Britta Simon in SAP Cloud for Customer that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5efdc-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5efdc-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5efdc-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="5efdc-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5efdc-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 SAP Cloud for Customer 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SAP Cloud for Customer application.</span></span>

<span data-ttu-id="5efdc-150">**SAP Cloud for Customer에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="5efdc-150">**To configure Azure AD single sign-on with SAP Cloud for Customer, perform the following steps:**</span></span>

1. <span data-ttu-id="5efdc-151">Azure Portal의 **SAP Cloud for Customer** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-151">In the Azure portal, on the **SAP Cloud for Customer** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="5efdc-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_samlbase.png)

3. <span data-ttu-id="5efdc-155">**SAP Cloud for Customer 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-155">On the **SAP Cloud for Customer Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_url.png)

    <span data-ttu-id="5efdc-157">a.</span><span class="sxs-lookup"><span data-stu-id="5efdc-157">a.</span></span> <span data-ttu-id="5efdc-158">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<server name>.crm.ondemand.com`</span><span class="sxs-lookup"><span data-stu-id="5efdc-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<server name>.crm.ondemand.com`</span></span>

    <span data-ttu-id="5efdc-159">b.</span><span class="sxs-lookup"><span data-stu-id="5efdc-159">b.</span></span> <span data-ttu-id="5efdc-160">**식별자** 텍스트 상자에서 `https://<server name>.crm.ondemand.com` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<server name>.crm.ondemand.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5efdc-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-161">These values are not real.</span></span> <span data-ttu-id="5efdc-162">실제 로그온 URL 및 식별자로 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="5efdc-163">이러한 값을 얻으려면 [SAP Cloud for Customer 클라이언트 지원 팀](https://www.sap.com/about/agreements.sap-cloud-services-customers.html)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="5efdc-163">Contact [SAP Cloud for Customer Client support team](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) to get these values.</span></span> 

4. <span data-ttu-id="5efdc-164">**사용자 특성** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-164">On the **User Attributes** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_attribute.png)

    <span data-ttu-id="5efdc-166">a.</span><span class="sxs-lookup"><span data-stu-id="5efdc-166">a.</span></span> <span data-ttu-id="5efdc-167">**사용자 ID** 목록에서 **ExtractMailPrefix()** 함수를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-167">In **User Identifier** list, select the **ExtractMailPrefix()** function.</span></span>

    <span data-ttu-id="5efdc-168">b.</span><span class="sxs-lookup"><span data-stu-id="5efdc-168">b.</span></span> <span data-ttu-id="5efdc-169">**메일** 목록에서 구현에 사용할 사용자 특성을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-169">From the **Mail** list, select the user attribute you want to use for your implementation.</span></span>
    <span data-ttu-id="5efdc-170">예를 들어, EmployeeID를 고유한 사용자 식별자로 사용하고자 하고 ExtensionAttribute2에 특성 값을 저장했다면 user.extensionattribute2를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-170">For example, if you want to use the EmployeeID as unique user identifier and you have stored the attribute value in the ExtensionAttribute2, then select user.extensionattribute2.</span></span>  

5. <span data-ttu-id="5efdc-171">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 메타데이터 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-171">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_certificate.png) 

6. <span data-ttu-id="5efdc-173">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-173">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="5efdc-175">**SAP Cloud for Customer 구성** 섹션에서 **SAP Cloud for Customer 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-175">On the **SAP Cloud for Customer Configuration** section, click **Configure SAP Cloud for Customer** to open **Configure sign-on** window.</span></span> <span data-ttu-id="5efdc-176">**빠른 참조 섹션**에서 **SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-176">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_configure.png) 

8. <span data-ttu-id="5efdc-178">SSO를 구성하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-178">To get SSO configured, perform the following steps:</span></span>
   
    <span data-ttu-id="5efdc-179">a.</span><span class="sxs-lookup"><span data-stu-id="5efdc-179">a.</span></span> <span data-ttu-id="5efdc-180">SAP Cloud for Customer 포털에 관리자 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-180">Login into SAP Cloud for Customer portal with administrator rights.</span></span>
   
    <span data-ttu-id="5efdc-181">b.</span><span class="sxs-lookup"><span data-stu-id="5efdc-181">b.</span></span> <span data-ttu-id="5efdc-182">**응용 프로그램 및 사용자 관리 일반 작업**으로 이동하여 **ID 공급자** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-182">Navigate to the **Application and User Management Common Task** and click the **Identity Provider** tab.</span></span>
   
    <span data-ttu-id="5efdc-183">c.</span><span class="sxs-lookup"><span data-stu-id="5efdc-183">c.</span></span> <span data-ttu-id="5efdc-184">**새 ID 공급자** 를 클릭하고 Azure Portal에서 다운로드한 메타데이터 XML 파일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-184">Click **New Identity Provider** and select the metadata XML file you have downloaded from the Azure portal.</span></span> <span data-ttu-id="5efdc-185">시스템은 메타데이터를 가져와서 필수 서명 인증서 및 암호화 인증서를 자동으로 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-185">By importing the metadata, the system automatically uploads the required signature certificate and encryption certificate.</span></span>
   
    ![Single Sign-On 구성](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_54.png)
   
    <span data-ttu-id="5efdc-187">d.</span><span class="sxs-lookup"><span data-stu-id="5efdc-187">d.</span></span> <span data-ttu-id="5efdc-188">Azure Active Directory에서는 SAML 요청에서 어설션 소비자 서비스 URL 요소가 필요합니다. 따라서 **어설션 소비자 서비스 URL 포함** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-188">Azure Active Directory requires the element Assertion Consumer Service URL in the SAML request, so select the **Include Assertion Consumer Service URL** checkbox.</span></span>
   
    <span data-ttu-id="5efdc-189">e.</span><span class="sxs-lookup"><span data-stu-id="5efdc-189">e.</span></span> <span data-ttu-id="5efdc-190">**Single Sign-on 활성화**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-190">Click **Activate Single Sign-On**.</span></span>
   
    <span data-ttu-id="5efdc-191">f.</span><span class="sxs-lookup"><span data-stu-id="5efdc-191">f.</span></span> <span data-ttu-id="5efdc-192">변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-192">Save your changes.</span></span>
   
    <span data-ttu-id="5efdc-193">g.</span><span class="sxs-lookup"><span data-stu-id="5efdc-193">g.</span></span> <span data-ttu-id="5efdc-194">**내 시스템** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-194">Click the **My System** tab.</span></span>
   
    ![Single Sign-On 구성](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_52.png)
   
    <span data-ttu-id="5efdc-196">h.</span><span class="sxs-lookup"><span data-stu-id="5efdc-196">h.</span></span> <span data-ttu-id="5efdc-197">Azure Portal에서 복사한 **SAML Single Sign-On 서비스 URL**을 **Azure AD 로그온 URL** 텍스트 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-197">In **Azure AD Sign On URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_53.png)
   
    <span data-ttu-id="5efdc-199">i.</span><span class="sxs-lookup"><span data-stu-id="5efdc-199">i.</span></span> <span data-ttu-id="5efdc-200">직원이 **수동 ID 공급자 선택**을 선택하여 사용자 ID 및 암호 또는 SSO를 사용하는 로그온 중 하나를 수동으로 선택할 수 있는지 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-200">Specify whether the employee can manually choose between logging on with user ID and password or SSO by selecting the **Manual Identity Provider Selection**.</span></span>
   
    <span data-ttu-id="5efdc-201">j.</span><span class="sxs-lookup"><span data-stu-id="5efdc-201">j.</span></span> <span data-ttu-id="5efdc-202">**SSO URL** 섹션에서 시스템에 로그온하는 직원이 사용해야 하는 URL을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-202">In the **SSO URL** section, specify the URL that should be used by your employees to sign on to the system.</span></span> 
    <span data-ttu-id="5efdc-203">**직원에게 전송된 URL** 목록에서 다음 옵션 중 하나를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-203">In the **URL Sent to Employee** list, you can choose between the following options:</span></span>
   
    <span data-ttu-id="5efdc-204">**SSO가 아닌 URL**</span><span class="sxs-lookup"><span data-stu-id="5efdc-204">**Non-SSO URL**</span></span>
   
    <span data-ttu-id="5efdc-205">시스템은 직원에게 정상적인 시스템 URL만을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-205">The system sends only the normal system URL to the employee.</span></span> <span data-ttu-id="5efdc-206">직원은 SSO를 사용하여 로그온할 수 없고 대신 암호 또는 인증서를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-206">The employee cannot log on using SSO, and must use password or certificate instead.</span></span>
   
    <span data-ttu-id="5efdc-207">**SSO URL**</span><span class="sxs-lookup"><span data-stu-id="5efdc-207">**SSO URL**</span></span> 
   
    <span data-ttu-id="5efdc-208">시스템은 직원에게 SSO URL만을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-208">The system sends only the SSO URL to the employee.</span></span> <span data-ttu-id="5efdc-209">직원은 SSO를 사용하여 로그온할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-209">The employee can log on using SSO.</span></span> <span data-ttu-id="5efdc-210">IdP를 통해 인증 요청이 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-210">Authentication request is redirected through the IdP.</span></span>
   
    <span data-ttu-id="5efdc-211">**자동 선택**</span><span class="sxs-lookup"><span data-stu-id="5efdc-211">**Automatic Selection**</span></span>
   
    <span data-ttu-id="5efdc-212">SSO가 활성 상태가 아닌 경우 시스템은 직원에게 정상적인 시스템 URL을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-212">If SSO is not active, the system sends the normal system URL to the employee.</span></span> <span data-ttu-id="5efdc-213">SSO가 활성 상태인 경우 시스템은 직원이 암호를 가지는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-213">If SSO is active, the system checks whether the employee has a password.</span></span> <span data-ttu-id="5efdc-214">암호를 사용할 수 있는 경우 SSO URL와 SSO가 아닌 URL은 직원에게 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-214">If a password is available, both SSO URL and Non-SSO URL are sent to the employee.</span></span> <span data-ttu-id="5efdc-215">그러나 직원에게 암호가 없는 경우 SSO URL만이 직원에게 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-215">However, if the employee has no password, only the SSO URL is sent to the employee.</span></span>
   
    <span data-ttu-id="5efdc-216">k.</span><span class="sxs-lookup"><span data-stu-id="5efdc-216">k.</span></span> <span data-ttu-id="5efdc-217">변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-217">Save your changes.</span></span>

> [!TIP]
> <span data-ttu-id="5efdc-218">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-218">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5efdc-219">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-219">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5efdc-220">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-220">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5efdc-221">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="5efdc-221">Creating an Azure AD test user</span></span>
<span data-ttu-id="5efdc-222">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-222">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="5efdc-224">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="5efdc-224">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5efdc-225">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-225">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5efdc-227">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-227">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5efdc-229">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-229">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5efdc-231">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-231">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5efdc-233">a.</span><span class="sxs-lookup"><span data-stu-id="5efdc-233">a.</span></span> <span data-ttu-id="5efdc-234">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-234">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5efdc-235">b.</span><span class="sxs-lookup"><span data-stu-id="5efdc-235">b.</span></span> <span data-ttu-id="5efdc-236">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-236">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5efdc-237">c.</span><span class="sxs-lookup"><span data-stu-id="5efdc-237">c.</span></span> <span data-ttu-id="5efdc-238">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-238">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="5efdc-239">d.</span><span class="sxs-lookup"><span data-stu-id="5efdc-239">d.</span></span> <span data-ttu-id="5efdc-240">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-240">Click **Create**.</span></span>
 
### <a name="creating-a-sap-cloud-for-customer-test-user"></a><span data-ttu-id="5efdc-241">SAP Cloud for Customer 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="5efdc-241">Creating a SAP Cloud for Customer test user</span></span>

<span data-ttu-id="5efdc-242">이 섹션에서는 SAP Cloud for Customer에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-242">In this section, you create a user called Britta Simon in SAP Cloud for Customer.</span></span> <span data-ttu-id="5efdc-243">[SAP Cloud for Customer 지원 팀](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) SAP Cloud for Customer 플랫폼에 사용자를 추가하세요.</span><span class="sxs-lookup"><span data-stu-id="5efdc-243">Please work with [SAP Cloud for Customer support team](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) to add the users in the SAP Cloud for Customer platform.</span></span> 

> [!NOTE]
> <span data-ttu-id="5efdc-244">NameID 값이 SAP Cloud for Customer 플랫폼에서 사용자 이름 필드와 일치하는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="5efdc-244">Please make sure that NameID value should match with the username field in the SAP Cloud for Customer platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="5efdc-245">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="5efdc-245">Assigning the Azure AD test user</span></span>

<span data-ttu-id="5efdc-246">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 SAP Cloud for Customer에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-246">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SAP Cloud for Customer.</span></span>

![사용자 할당][200] 

<span data-ttu-id="5efdc-248">**Britta Simon을 SAP Cloud for Customer에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="5efdc-248">**To assign Britta Simon to SAP Cloud for Customer, perform the following steps:**</span></span>

1. <span data-ttu-id="5efdc-249">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-249">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="5efdc-251">응용 프로그램 목록에서 **SAP Cloud for Customer**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-251">In the applications list, select **SAP Cloud for Customer**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_app.png) 

3. <span data-ttu-id="5efdc-253">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-253">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="5efdc-255">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-255">Click **Add** button.</span></span> <span data-ttu-id="5efdc-256">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-256">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="5efdc-258">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-258">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5efdc-259">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-259">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5efdc-260">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-260">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5efdc-261">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="5efdc-261">Testing single sign-on</span></span>

<span data-ttu-id="5efdc-262">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-262">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="5efdc-263">액세스 패널에서 SAP Cloud for Customer 타일을 클릭하면 SAP Cloud for Customer 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="5efdc-263">When you click the SAP Cloud for Customer tile in the Access Panel, you should get automatically signed-on to your SAP Cloud for Customer application.</span></span>
<span data-ttu-id="5efdc-264">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5efdc-264">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5efdc-265">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="5efdc-265">Additional resources</span></span>

* [<span data-ttu-id="5efdc-266">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="5efdc-266">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5efdc-267">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="5efdc-267">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_203.png

