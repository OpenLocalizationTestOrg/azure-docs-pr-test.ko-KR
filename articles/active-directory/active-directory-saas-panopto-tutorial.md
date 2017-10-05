---
title: "자습서: Panopto와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 Panopto 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 89c88e23-93ce-4970-9baa-1104c4e8fe4a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 725fba1227cfc9c4850f9e2d6fd0b13e88eafa20
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-panopto"></a><span data-ttu-id="2cd0d-103">자습서: Panopto와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="2cd0d-103">Tutorial: Azure Active Directory integration with Panopto</span></span>

<span data-ttu-id="2cd0d-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Panopto를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-104">In this tutorial, you learn how to integrate Panopto with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2cd0d-105">Panopto를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-105">Integrating Panopto with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="2cd0d-106">Panopto에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-106">You can control in Azure AD who has access to Panopto</span></span>
- <span data-ttu-id="2cd0d-107">사용자가 해당 Azure AD 계정으로 Panopto에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-107">You can enable your users to automatically get signed-on to Panopto (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2cd0d-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="2cd0d-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2cd0d-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="2cd0d-110">Prerequisites</span></span>

<span data-ttu-id="2cd0d-111">Panopto와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-111">To configure Azure AD integration with Panopto, you need the following items:</span></span>

- <span data-ttu-id="2cd0d-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="2cd0d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2cd0d-113">Panopto Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="2cd0d-113">A Panopto single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2cd0d-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2cd0d-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2cd0d-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2cd0d-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2cd0d-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="2cd0d-118">Scenario description</span></span>
<span data-ttu-id="2cd0d-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2cd0d-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2cd0d-121">갤러리에서 Panopto 추가</span><span class="sxs-lookup"><span data-stu-id="2cd0d-121">Adding Panopto from the gallery</span></span>
2. <span data-ttu-id="2cd0d-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="2cd0d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-panopto-from-the-gallery"></a><span data-ttu-id="2cd0d-123">갤러리에서 Panopto 추가</span><span class="sxs-lookup"><span data-stu-id="2cd0d-123">Adding Panopto from the gallery</span></span>
<span data-ttu-id="2cd0d-124">Panopto의 Azure AD 통합을 구성하려면 갤러리의 Panopto를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-124">To configure the integration of Panopto into Azure AD, you need to add Panopto from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2cd0d-125">**갤러리에서 Panopto를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="2cd0d-125">**To add Panopto from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2cd0d-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2cd0d-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="2cd0d-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="2cd0d-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="2cd0d-133">검색 상자에 **Panopto**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-133">In the search box, type **Panopto**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_search.png)

5. <span data-ttu-id="2cd0d-135">결과 패널에서 **Panopto**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-135">In the results panel, select **Panopto**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2cd0d-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="2cd0d-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="2cd0d-138">이 섹션에서는 “Britta Simon”이라는 테스트 사용자를 기반으로 Panopto에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-138">In this section, you configure and test Azure AD single sign-on with Panopto based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="2cd0d-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Panopto 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Panopto is to a user in Azure AD.</span></span> <span data-ttu-id="2cd0d-140">즉, Azure AD 사용자와 Panopto의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-140">In other words, a link relationship between an Azure AD user and the related user in Panopto needs to be established.</span></span>

<span data-ttu-id="2cd0d-141">Panopto에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-141">In Panopto, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="2cd0d-142">Panopto에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-142">To configure and test Azure AD single sign-on with Panopto, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2cd0d-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="2cd0d-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2cd0d-145">**[Panopto 테스트 사용자 만들기](#creating-a-panopto-test-user)** - Britta Simon의 Azure AD 표현과 연결되는 대응 사용자를 Panopto에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-145">**[Creating a Panopto test user](#creating-a-panopto-test-user)** - to have a counterpart of Britta Simon in Panopto that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="2cd0d-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2cd0d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2cd0d-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="2cd0d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2cd0d-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Panopto 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Panopto application.</span></span>

<span data-ttu-id="2cd0d-150">**Panopto에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="2cd0d-150">**To configure Azure AD single sign-on with Panopto, perform the following steps:**</span></span>

1. <span data-ttu-id="2cd0d-151">Azure Portal의 **Panopto** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-151">In the Azure portal, on the **Panopto** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="2cd0d-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_samlbase.png)

3. <span data-ttu-id="2cd0d-155">**Panopto 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-155">On the **Panopto Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_url.png)

    <span data-ttu-id="2cd0d-157">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<tenant-name>.panopto.com`</span><span class="sxs-lookup"><span data-stu-id="2cd0d-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.panopto.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2cd0d-158">이 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-158">This value is not real.</span></span> <span data-ttu-id="2cd0d-159">이 값을 실제 로그온 URL로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="2cd0d-160">이 값을 얻으려면 [Panopto 클라이언트 지원 팀](mailto:support@panopto.com‎)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-160">Contact [Panopto Client support team](mailto:support@panopto.com‎) to get this value.</span></span> 
 
4. <span data-ttu-id="2cd0d-161">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 메타데이터 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_certificate.png) 

5. <span data-ttu-id="2cd0d-163">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-163">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-panopto-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="2cd0d-165">**Panopto 구성** 섹션에서 **Panopto 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-165">On the **Panopto Configuration** section, click **Configure Panopto** to open **Configure sign-on** window.</span></span> <span data-ttu-id="2cd0d-166">**빠른 참조 섹션**에서 **SAML 엔터티 ID 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-166">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_configure.png) 

7. <span data-ttu-id="2cd0d-168">다른 웹 브라우저 창에서 Panopto 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-168">In a different web browser window, log in to your Panopto company site as an administrator.</span></span>

8. <span data-ttu-id="2cd0d-169">왼쪽의 도구 모음에서 **시스템**을 클릭한 다음 **ID 공급자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-169">In the toolbar on the left, click **System**, and then click **Identity Providers**.</span></span>
   
   <span data-ttu-id="2cd0d-170">![시스템](./media/active-directory-saas-panopto-tutorial/ic777670.png "시스템")</span><span class="sxs-lookup"><span data-stu-id="2cd0d-170">![System](./media/active-directory-saas-panopto-tutorial/ic777670.png "System")</span></span>
9. <span data-ttu-id="2cd0d-171">**공급자 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-171">Click **Add Provider**.</span></span>
   
   <span data-ttu-id="2cd0d-172">![ID 공급자](./media/active-directory-saas-panopto-tutorial/ic777671.png "ID 공급자")</span><span class="sxs-lookup"><span data-stu-id="2cd0d-172">![Identity Providers](./media/active-directory-saas-panopto-tutorial/ic777671.png "Identity Providers")</span></span>
   
10. <span data-ttu-id="2cd0d-173">SAML 공급자 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-173">In the SAML provider section, perform the following steps:</span></span>
   
    <span data-ttu-id="2cd0d-174">![SaaS 구성](./media/active-directory-saas-panopto-tutorial/ic777672.png "SaaS 구성")</span><span class="sxs-lookup"><span data-stu-id="2cd0d-174">![SaaS configuration](./media/active-directory-saas-panopto-tutorial/ic777672.png "SaaS configuration")</span></span>
    
    <span data-ttu-id="2cd0d-175">a.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-175">a.</span></span> <span data-ttu-id="2cd0d-176">**공급자 유형** 목록에서 **SAML20**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-176">From the **Provider Type** list, select **SAML20**.</span></span>    
    
    <span data-ttu-id="2cd0d-177">b.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-177">b.</span></span> <span data-ttu-id="2cd0d-178">**인스턴스 이름** 텍스트 상자에 인스턴스 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-178">In the **Instance Name** textbox, type a name for the instance.</span></span>

    <span data-ttu-id="2cd0d-179">c.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-179">c.</span></span> <span data-ttu-id="2cd0d-180">**간단한 설명** 텍스트 상자에 간단한 설명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-180">In the **Friendly Description** textbox, type a friendly description.</span></span>
    
    <span data-ttu-id="2cd0d-181">d.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-181">d.</span></span> <span data-ttu-id="2cd0d-182">Azure Portal에서 복사한 **SAML Single Sign-On 서비스 URL** 값을 **Bounce Page Url**(바운스 페이지 URL) 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-182">In **Bounce Page Url** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="2cd0d-183">e.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-183">e.</span></span> <span data-ttu-id="2cd0d-184">Azure Portal에서 복사한 **SAML 엔터티 ID** 값을 **발급자** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-184">In the **Issuer** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="2cd0d-185">f.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-185">f.</span></span> <span data-ttu-id="2cd0d-186">Azure Portal에서 다운로드한 Base-64로 인코딩된 인증서를 열고, 내용을 클립보드에 복사한 다음, **공개 키** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-186">Open your base-64 encoded certificate, which you have downloaded from Azure portal, copy the content of it in to your clipboard, and then paste it to the **Public Key**  textbox.</span></span>

11. <span data-ttu-id="2cd0d-187">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-187">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="2cd0d-188">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="2cd0d-189">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="2cd0d-190">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2cd0d-191">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="2cd0d-191">Creating an Azure AD test user</span></span>

<span data-ttu-id="2cd0d-192">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="2cd0d-194">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="2cd0d-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2cd0d-195">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-panopto-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2cd0d-197">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-197">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-panopto-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2cd0d-199">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-199">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-panopto-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2cd0d-201">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-201">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-panopto-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2cd0d-203">a.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-203">a.</span></span> <span data-ttu-id="2cd0d-204">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-204">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2cd0d-205">b.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-205">b.</span></span> <span data-ttu-id="2cd0d-206">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2cd0d-207">c.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-207">c.</span></span> <span data-ttu-id="2cd0d-208">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-208">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="2cd0d-209">d.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-209">d.</span></span> <span data-ttu-id="2cd0d-210">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-210">Click **Create**.</span></span>
 
### <a name="creating-a-panopto-test-user"></a><span data-ttu-id="2cd0d-211">Panopto 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="2cd0d-211">Creating a Panopto test user</span></span>

<span data-ttu-id="2cd0d-212">Panopto를 프로비전하는 사용자를 구성할 작업 항목이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-212">There is no action item for you to configure user provisioning to Panopto.</span></span>  
<span data-ttu-id="2cd0d-213">할당된 사용자가 액세스 패널을 사용하여 Panopto에 로그인하려는 경우 Panopto는 사용자가 존재하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-213">When an assigned user tries to log in to Panopto using the access panel, Panopto checks whether the user exists.</span></span>  

<span data-ttu-id="2cd0d-214">사용할 수 있는 사용자 계정이 없으면 자동으로 Panopto에 의해 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-214">If there is no user account available yet, it is automatically created by Panopto.</span></span>

>[!NOTE]
><span data-ttu-id="2cd0d-215">다른 Panopto 사용자 계정 생성 도구 또는 Panopto가 제공한 API를 사용하여 Azure AD 사용자 계정을 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-215">You can use any other Panopto user account creation tools or APIs provided by Panopto to provision Azure AD user accounts.</span></span>
>
>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="2cd0d-216">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="2cd0d-216">Assigning the Azure AD test user</span></span>

<span data-ttu-id="2cd0d-217">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Panopto에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Panopto.</span></span>

![사용자 할당][200] 

<span data-ttu-id="2cd0d-219">**Britta Simon을 Panopto에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="2cd0d-219">**To assign Britta Simon to Panopto, perform the following steps:**</span></span>

1. <span data-ttu-id="2cd0d-220">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="2cd0d-222">응용 프로그램 목록에서 **Panopto**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-222">In the applications list, select **Panopto**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_app.png) 

3. <span data-ttu-id="2cd0d-224">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-224">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="2cd0d-226">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-226">Click **Add** button.</span></span> <span data-ttu-id="2cd0d-227">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="2cd0d-229">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="2cd0d-230">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2cd0d-231">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2cd0d-232">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="2cd0d-232">Testing single sign-on</span></span>

<span data-ttu-id="2cd0d-233">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-233">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="2cd0d-234">액세스 패널에서 Panopto 타일을 클릭하면 Panopto 응용 프로그램의 로그인 페이지가 자동으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-234">When you click the Panopto tile in the Access Panel, you should get automatically login page of Panopto application.</span></span>
<span data-ttu-id="2cd0d-235">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2cd0d-235">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2cd0d-236">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="2cd0d-236">Additional resources</span></span>

* [<span data-ttu-id="2cd0d-237">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="2cd0d-237">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2cd0d-238">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="2cd0d-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_203.png

