---
title: "자습서: SAP NetWeaver와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 SAP NetWeaver 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1b9e59e3-e7ae-4e74-b16c-8c1a7ccfdef3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: ad4140eb1183094a67822ad92eabcd35101360b6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-netweaver"></a><span data-ttu-id="1c63c-103">자습서: SAP NetWeaver와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="1c63c-103">Tutorial: Azure Active Directory integration with SAP NetWeaver</span></span>

<span data-ttu-id="1c63c-104">이 자습서에서는 Azure AD(Azure Active Directory)와 SAP NetWeaver를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1c63c-104">In this tutorial, you learn how to integrate SAP NetWeaver with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1c63c-105">SAP NetWeaver를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c63c-105">Integrating SAP NetWeaver with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1c63c-106">SAP NetWeaver에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c63c-106">You can control in Azure AD who has access to SAP NetWeaver</span></span>
- <span data-ttu-id="1c63c-107">사용자가 해당 Azure AD 계정으로 SAP NetWeaver에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c63c-107">You can enable your users to automatically get signed-on to SAP NetWeaver (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1c63c-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c63c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1c63c-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1c63c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="1c63c-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="1c63c-110">Prerequisites</span></span>

<span data-ttu-id="1c63c-111">SAP NetWeaver와의 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1c63c-111">To configure Azure AD integration with SAP NetWeaver, you need the following items:</span></span>

- <span data-ttu-id="1c63c-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="1c63c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1c63c-113">SAP NetWeaver Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="1c63c-113">An SAP NetWeaver single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1c63c-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1c63c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1c63c-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c63c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1c63c-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="1c63c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1c63c-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c63c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1c63c-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="1c63c-118">Scenario description</span></span>
<span data-ttu-id="1c63c-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c63c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1c63c-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c63c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1c63c-121">갤러리에서 SAP NetWeaver 추가</span><span class="sxs-lookup"><span data-stu-id="1c63c-121">Adding SAP NetWeaver from the gallery</span></span>
2. <span data-ttu-id="1c63c-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="1c63c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sap-netweaver-from-the-gallery"></a><span data-ttu-id="1c63c-123">갤러리에서 SAP NetWeaver 추가</span><span class="sxs-lookup"><span data-stu-id="1c63c-123">Adding SAP NetWeaver from the gallery</span></span>
<span data-ttu-id="1c63c-124">SAP NetWeaver의 Azure AD 통합을 구성하려면 갤러리의 SAP NetWeaver를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c63c-124">To configure the integration of SAP NetWeaver into Azure AD, you need to add SAP NetWeaver from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1c63c-125">**갤러리에서 SAP NetWeaver를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="1c63c-125">**To add SAP NetWeaver from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1c63c-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1c63c-126">In the **[Azure Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1c63c-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="1c63c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1c63c-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="1c63c-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="1c63c-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1c63c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="1c63c-133">검색 상자에 **SAP NetWeaver**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1c63c-133">In the search box, type **SAP NetWeaver**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_search.png)

5. <span data-ttu-id="1c63c-135">결과 창에서 **SAP NetWeaver**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1c63c-135">In the results panel, select **SAP NetWeaver**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1c63c-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="1c63c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1c63c-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 SAP NetWeaver에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="1c63c-138">In this section, you configure and test Azure AD single sign-on with SAP NetWeaver based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="1c63c-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 SAP NetWeaver 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c63c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SAP NetWeaver is to a user in Azure AD.</span></span> <span data-ttu-id="1c63c-140">즉, Azure AD 사용자와 SAP NetWeaver의 관련 사용자 간에 연결 관계가 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c63c-140">In other words, a link relationship between an Azure AD user and the related user in SAP NetWeaver needs to be established.</span></span>

<span data-ttu-id="1c63c-141">이 연결 관계는 Azure AD의 **사용자 이름** 값을 SAP NetWeaver의 **Username** 값으로 할당하여 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1c63c-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in SAP NetWeaver.</span></span>

<span data-ttu-id="1c63c-142">SAP NetWeaver에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c63c-142">To configure and test Azure AD single sign-on with SAP NetWeaver, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1c63c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c63c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1c63c-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1c63c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1c63c-145">**[SAP NetWeaver 테스트 사용자 만들기](#creating-an-sap-netweaver-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 SAP NetWeaver에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1c63c-145">**[Creating an SAP NetWeaver test user](#creating-an-sap-netweaver-test-user)** - to have a counterpart of Britta Simon in SAP NetWeaver that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1c63c-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c63c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1c63c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1c63c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1c63c-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="1c63c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1c63c-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 SAP NetWeaver 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="1c63c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SAP NetWeaver application.</span></span>

<span data-ttu-id="1c63c-150">**SAP NetWeaver에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="1c63c-150">**To configure Azure AD single sign-on with SAP NetWeaver, perform the following steps:**</span></span>

1. <span data-ttu-id="1c63c-151">Azure Portal의 **SAP NetWeaver** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1c63c-151">In the Azure portal, on the **SAP NetWeaver** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="1c63c-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1c63c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_samlbase.png)

3. <span data-ttu-id="1c63c-155">**SAP NetWeaver 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1c63c-155">On the **SAP NetWeaver Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_url.png)

    <span data-ttu-id="1c63c-157">a.</span><span class="sxs-lookup"><span data-stu-id="1c63c-157">a.</span></span> <span data-ttu-id="1c63c-158">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<your company instance of SAP NetWeaver>`</span><span class="sxs-lookup"><span data-stu-id="1c63c-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<your company instance of SAP NetWeaver>`</span></span>

    <span data-ttu-id="1c63c-159">b.</span><span class="sxs-lookup"><span data-stu-id="1c63c-159">b.</span></span> <span data-ttu-id="1c63c-160">**식별자** 텍스트 상자에서 `https://<your company instance of SAP NetWeaver>` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1c63c-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<your company instance of SAP NetWeaver>`</span></span>

    <span data-ttu-id="1c63c-161">c.</span><span class="sxs-lookup"><span data-stu-id="1c63c-161">c.</span></span> <span data-ttu-id="1c63c-162">**회신 URL** 텍스트 상자에 다음 패턴으로 URL을 입력합니다.`https://<your company instance of SAP NetWeaver>/sap/saml2/sp/acs/100`</span><span class="sxs-lookup"><span data-stu-id="1c63c-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://<your company instance of SAP NetWeaver>/sap/saml2/sp/acs/100`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="1c63c-163">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="1c63c-163">These values are not the real.</span></span> <span data-ttu-id="1c63c-164">실제 식별자, 회신 URL 및 로그온 URL을 사용하여 이러한 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="1c63c-164">Update these values with the actual Identifier and Reply URL and Sign-On URL.</span></span> <span data-ttu-id="1c63c-165">식별자에는 고유한 문자열 값을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1c63c-165">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="1c63c-166">이러한 값을 얻으려면 [SAP NetWeaver 클라이언트 지원 팀](https://www.sap.com/support.html)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="1c63c-166">Contact [SAP NetWeaver Client support team](https://www.sap.com/support.html) to get these values.</span></span> 

4. <span data-ttu-id="1c63c-167">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 XML 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="1c63c-167">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_certificate.png) 

5. <span data-ttu-id="1c63c-169">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1c63c-169">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="1c63c-171">**SAP NetWeaver 구성** 섹션에서 **SAP NetWeaver 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1c63c-171">On the **SAP NetWeaver Configuration** section, click **Configure SAP NetWeaver** to open **Configure sign-on** window.</span></span> <span data-ttu-id="1c63c-172">**빠른 참조 섹션**에서 **SAML 엔터티 ID**를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="1c63c-172">Copy the **SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_configure.png) 

7. <span data-ttu-id="1c63c-174">**SAP NetWeaver** 쪽에서 Single Sign-On을 구성하려면 다운로드한 **메타데이터 XML** 및 **SAML 엔터티 ID**를 [SAP NetWeaver 지원](https://www.sap.com/support.html)으로 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c63c-174">To configure single sign-on on **SAP NetWeaver** side, you need to send the downloaded **Metadata XML** and **SAML Entity ID** to [SAP NetWeaver support](https://www.sap.com/support.html).</span></span> 

> [!TIP]
> <span data-ttu-id="1c63c-175">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c63c-175">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1c63c-176">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c63c-176">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1c63c-177">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c63c-177">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1c63c-178">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="1c63c-178">Creating an Azure AD test user</span></span>
<span data-ttu-id="1c63c-179">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1c63c-179">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="1c63c-181">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="1c63c-181">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1c63c-182">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1c63c-182">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sap-netweaver-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1c63c-184">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1c63c-184">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sap-netweaver-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1c63c-186">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1c63c-186">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sap-netweaver-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1c63c-188">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1c63c-188">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sap-netweaver-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1c63c-190">a.</span><span class="sxs-lookup"><span data-stu-id="1c63c-190">a.</span></span> <span data-ttu-id="1c63c-191">**이름** 텍스트 상자에 **Britta Simon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1c63c-191">In the **Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="1c63c-192">b.</span><span class="sxs-lookup"><span data-stu-id="1c63c-192">b.</span></span> <span data-ttu-id="1c63c-193">**사용자 이름** 텍스트 상자에 Britta Simon의 **메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1c63c-193">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="1c63c-194">c.</span><span class="sxs-lookup"><span data-stu-id="1c63c-194">c.</span></span> <span data-ttu-id="1c63c-195">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="1c63c-195">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1c63c-196">d.</span><span class="sxs-lookup"><span data-stu-id="1c63c-196">d.</span></span> <span data-ttu-id="1c63c-197">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1c63c-197">Click **Create**.</span></span>
 
### <a name="creating-an-sap-netweaver-test-user"></a><span data-ttu-id="1c63c-198">SAP NetWeaver 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="1c63c-198">Creating an SAP NetWeaver test user</span></span>

<span data-ttu-id="1c63c-199">이 섹션에서는 SAP NetWeaver에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1c63c-199">In this section, you create a user called Britta Simon in SAP NetWeaver.</span></span> <span data-ttu-id="1c63c-200">SAP NetWeaver 플랫폼에서 사용자를 추가하려면 [SAP NetWeaver 지원](https://www.sap.com/support.html)으로 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="1c63c-200">Work with your [SAP NetWeaver support](https://www.sap.com/support.html) to add the users in the SAP NetWeaver platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1c63c-201">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="1c63c-201">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1c63c-202">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 SAP NetWeaver에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="1c63c-202">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SAP NetWeaver.</span></span>

![사용자 할당][200] 

<span data-ttu-id="1c63c-204">**Britta Simon을 SAP NetWeaver에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="1c63c-204">**To assign Britta Simon to SAP NetWeaver, perform the following steps:**</span></span>

1. <span data-ttu-id="1c63c-205">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1c63c-205">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="1c63c-207">응용 프로그램 목록에서 **SAP NetWeaver**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1c63c-207">In the applications list, select **SAP NetWeaver**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_app.png) 

3. <span data-ttu-id="1c63c-209">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1c63c-209">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="1c63c-211">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1c63c-211">Click **Add** button.</span></span> <span data-ttu-id="1c63c-212">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1c63c-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="1c63c-214">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1c63c-214">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1c63c-215">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1c63c-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1c63c-216">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1c63c-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1c63c-217">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="1c63c-217">Testing single sign-on</span></span>

<span data-ttu-id="1c63c-218">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="1c63c-218">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="1c63c-219">액세스 패널에서 SAP NetWeaver 타일을 클릭하면 SAP NetWeaver 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c63c-219">When you click the SAP NetWeaver tile in the Access Panel, you should get automatically signed-on to your SAP NetWeaver application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1c63c-220">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="1c63c-220">Additional resources</span></span>

* [<span data-ttu-id="1c63c-221">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="1c63c-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1c63c-222">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="1c63c-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_203.png

