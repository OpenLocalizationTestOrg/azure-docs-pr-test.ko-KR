---
title: "자습서: Mozy Enterprise와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 Mozy Enterprise 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 489b5e62-85c2-45c9-8766-326632d48114
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: jeedes
ms.openlocfilehash: ac73aadcb8205f24f9d2dbce5af76f53bbcb9753
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mozy-enterprise"></a><span data-ttu-id="f7c94-103">자습서: Mozy Enterprise와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="f7c94-103">Tutorial: Azure Active Directory integration with Mozy Enterprise</span></span>

<span data-ttu-id="f7c94-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Mozy Enterprise를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-104">In this tutorial, you learn how to integrate Mozy Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f7c94-105">Mozy Enterprise를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-105">Integrating Mozy Enterprise with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f7c94-106">Azure AD에서 사용자의 Mozy Enterprise에 대한 액세스 권한을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-106">You can control in Azure AD who has access to Mozy Enterprise</span></span>
- <span data-ttu-id="f7c94-107">사용자의 Azure AD 계정으로 Mozy Enterprise에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-107">You can enable your users to automatically get signed-on to Mozy Enterprise (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f7c94-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f7c94-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f7c94-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f7c94-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="f7c94-110">Prerequisites</span></span>

<span data-ttu-id="f7c94-111">Mozy Enterprise와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-111">To configure Azure AD integration with Mozy Enterprise, you need the following items:</span></span>

- <span data-ttu-id="f7c94-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="f7c94-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f7c94-113">Mozy Enterprise Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="f7c94-113">A Mozy Enterprise single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f7c94-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f7c94-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f7c94-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="f7c94-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f7c94-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f7c94-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="f7c94-118">Scenario description</span></span>
<span data-ttu-id="f7c94-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f7c94-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f7c94-121">갤러리에서 Mozy Enterprise 추가</span><span class="sxs-lookup"><span data-stu-id="f7c94-121">Adding Mozy Enterprise from the gallery</span></span>
2. <span data-ttu-id="f7c94-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="f7c94-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mozy-enterprise-from-the-gallery"></a><span data-ttu-id="f7c94-123">갤러리에서 Mozy Enterprise 추가</span><span class="sxs-lookup"><span data-stu-id="f7c94-123">Adding Mozy Enterprise from the gallery</span></span>
<span data-ttu-id="f7c94-124">Mozy Enterprise의 Azure AD 통합을 구성하려면 갤러리의 Mozy Enterprise를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-124">To configure the integration of Mozy Enterprise into Azure AD, you need to add Mozy Enterprise from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f7c94-125">**갤러리에서 Mozy Enterprise를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="f7c94-125">**To add Mozy Enterprise from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f7c94-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f7c94-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f7c94-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="f7c94-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="f7c94-133">검색 상자에 **Mozy Enterprise**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-133">In the search box, type **Mozy Enterprise**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_search.png)

5. <span data-ttu-id="f7c94-135">결과 패널에서 **Mozy Enterprise**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-135">In the results panel, select **Mozy Enterprise**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f7c94-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="f7c94-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f7c94-138">이 섹션에서는 “Britta Simon”이라는 테스트 사용자를 기반으로 Mozy Enterprise에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-138">In this section, you configure and test Azure AD single sign-on with Mozy Enterprise based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f7c94-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Mozy Enterprise 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Mozy Enterprise is to a user in Azure AD.</span></span> <span data-ttu-id="f7c94-140">즉, Azure AD 사용자와 Mozy Enterprise의 관련 사용자 간에 연결 관계가 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-140">In other words, a link relationship between an Azure AD user and the related user in Mozy Enterprise needs to be established.</span></span>

<span data-ttu-id="f7c94-141">Mozy Enterprise에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-141">In Mozy Enterprise, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f7c94-142">Mozy Enterprise에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-142">To configure and test Azure AD single sign-on with Mozy Enterprise, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f7c94-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f7c94-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f7c94-145">**[Mozy Enterprise 테스트 사용자 만들기](#creating-a-mozy-enterprise-test-user)** - Britta Simon의 Azure AD 표현과 연결되는 대응 사용자를 Mozy Enterprise에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-145">**[Creating a Mozy Enterprise test user](#creating-a-mozy-enterprise-test-user)** - to have a counterpart of Britta Simon in Mozy Enterprise that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f7c94-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f7c94-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f7c94-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="f7c94-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f7c94-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Mozy Enterprise 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Mozy Enterprise application.</span></span>

<span data-ttu-id="f7c94-150">**Mozy Enterprise에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="f7c94-150">**To configure Azure AD single sign-on with Mozy Enterprise, perform the following steps:**</span></span>

1. <span data-ttu-id="f7c94-151">Azure Portal의 **Mozy Enterprise** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-151">In the Azure portal, on the **Mozy Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="f7c94-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_samlbase.png)

3. <span data-ttu-id="f7c94-155">**Mozy 엔터프라이즈 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-155">On the **Mozy Enterprise Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_url.png)

    <span data-ttu-id="f7c94-157">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<tenantname>.Mozyenterprise.com`</span><span class="sxs-lookup"><span data-stu-id="f7c94-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenantname>.Mozyenterprise.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f7c94-158">이 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-158">This value is not real.</span></span> <span data-ttu-id="f7c94-159">이 값을 실제 로그온 URL로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="f7c94-160">이 값을 얻으려면 [Mozy Enterprise 클라이언트 지원 팀](http://support.mozy.com/)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="f7c94-160">Contact [Mozy Enterprise Client support team](http://support.mozy.com/) to get this value.</span></span>

4. <span data-ttu-id="f7c94-161">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_certificate.png) 

5. <span data-ttu-id="f7c94-163">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-163">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f7c94-165">**Mozy Enterprise 구성** 섹션에서 **Mozy Enterprise 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-165">On the **Mozy Enterprise Configuration** section, click **Configure Mozy Enterprise** to open **Configure sign-on** window.</span></span> <span data-ttu-id="f7c94-166">**빠른 참조 섹션**에서 **SAML 엔터티 ID 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-166">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_configure.png) 

7. <span data-ttu-id="f7c94-168">다른 웹 브라우저 창에서 Mozy Enterprise 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-168">In a different web browser window, log into your Mozy Enterprise company site as an administrator.</span></span>

8. <span data-ttu-id="f7c94-169">**구성** 섹션에서 **인증 정책**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-169">In the **Configuration** section, click **Authentication Policy**.</span></span>
   
   <span data-ttu-id="f7c94-170">![인증 정책](./media/active-directory-saas-mozy-enterprise-tutorial/ic777314.png "인증 정책")</span><span class="sxs-lookup"><span data-stu-id="f7c94-170">![Authentication policy](./media/active-directory-saas-mozy-enterprise-tutorial/ic777314.png "Authentication policy")</span></span>

9. <span data-ttu-id="f7c94-171">**인증 정책** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-171">On the **Authentication Policy** section, perform the following steps:</span></span>
   
   <span data-ttu-id="f7c94-172">![인증 정책](./media/active-directory-saas-mozy-enterprise-tutorial/ic777315.png "인증 정책")</span><span class="sxs-lookup"><span data-stu-id="f7c94-172">![Authentication policy](./media/active-directory-saas-mozy-enterprise-tutorial/ic777315.png "Authentication policy")</span></span>
   
   <span data-ttu-id="f7c94-173">a.</span><span class="sxs-lookup"><span data-stu-id="f7c94-173">a.</span></span> <span data-ttu-id="f7c94-174">**디렉터리 서비스**를 **공급자**로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-174">Select **Directory Service** as **Provider**.</span></span>
   
   <span data-ttu-id="f7c94-175">b.</span><span class="sxs-lookup"><span data-stu-id="f7c94-175">b.</span></span> <span data-ttu-id="f7c94-176">**LDAP 푸시 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-176">Select **Use LDAP Push**.</span></span>
   
   <span data-ttu-id="f7c94-177">c.</span><span class="sxs-lookup"><span data-stu-id="f7c94-177">c.</span></span> <span data-ttu-id="f7c94-178">**SAML 인증** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-178">Click the **SAML Authentication** tab.</span></span>
   
   <span data-ttu-id="f7c94-179">d.</span><span class="sxs-lookup"><span data-stu-id="f7c94-179">d.</span></span> <span data-ttu-id="f7c94-180">Azure Portal에서 복사한 **SAML Single Sign-On 서비스 URL**을 **인증 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-180">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal into the **Authentication URL** textbox.</span></span>
   
   <span data-ttu-id="f7c94-181">e.</span><span class="sxs-lookup"><span data-stu-id="f7c94-181">e.</span></span> <span data-ttu-id="f7c94-182">Azure Portal에서 복사한 **SAML 엔터티 ID**를 **SAML 끝점** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-182">Paste **SAML Entity ID**, which you have copied from the Azure portal into the **SAML Endpoint** textbox.</span></span>
   
   <span data-ttu-id="f7c94-183">f.</span><span class="sxs-lookup"><span data-stu-id="f7c94-183">f.</span></span> <span data-ttu-id="f7c94-184">다운로드한 Base-64로 인코딩된 인증서를 메모장에서 열고, 내용을 클립보드에 복사한 다음, 전체 인증서를 **SAML 인증서** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-184">Open your downloaded base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste the entire Certificate into **SAML Certificate** textbox.</span></span>
   
   <span data-ttu-id="f7c94-185">g.</span><span class="sxs-lookup"><span data-stu-id="f7c94-185">g.</span></span> <span data-ttu-id="f7c94-186">**SSO를 사용하여 관리자가 네트워크 자격 증명으로 로그인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-186">Select **Enable SSO for Admins to log in with their network credentials**.</span></span>
   
   <span data-ttu-id="f7c94-187">h.</span><span class="sxs-lookup"><span data-stu-id="f7c94-187">h.</span></span> <span data-ttu-id="f7c94-188">**변경 내용 저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-188">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="f7c94-189">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f7c94-190">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f7c94-191">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f7c94-192">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="f7c94-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="f7c94-193">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="f7c94-195">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="f7c94-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f7c94-196">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f7c94-198">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f7c94-200">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f7c94-202">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f7c94-204">a.</span><span class="sxs-lookup"><span data-stu-id="f7c94-204">a.</span></span> <span data-ttu-id="f7c94-205">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f7c94-206">b.</span><span class="sxs-lookup"><span data-stu-id="f7c94-206">b.</span></span> <span data-ttu-id="f7c94-207">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f7c94-208">c.</span><span class="sxs-lookup"><span data-stu-id="f7c94-208">c.</span></span> <span data-ttu-id="f7c94-209">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f7c94-210">d.</span><span class="sxs-lookup"><span data-stu-id="f7c94-210">d.</span></span> <span data-ttu-id="f7c94-211">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-211">Click **Create**.</span></span>
 
### <a name="creating-a-mozy-enterprise-test-user"></a><span data-ttu-id="f7c94-212">Mozy Enterprise 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="f7c94-212">Creating a Mozy Enterprise test user</span></span>

<span data-ttu-id="f7c94-213">Azure AD 사용자가 Mozy Enterprise에 로그인할 수 있도록 하려면 Mozy Enterprise로 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-213">In order to enable Azure AD users to log into Mozy Enterprise, they must be provisioned into Mozy Enterprise.</span></span> <span data-ttu-id="f7c94-214">Mozy Enterprise의 경우 프로비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-214">In the case of Mozy Enterprise, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="f7c94-215">다른 Mozy Enterprise 사용자 계정 생성 도구 또는 Mozy Enterprise가 제공한 API를 사용하여 AAD 사용자 계정을 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-215">You can use any other Mozy Enterprise user account creation tools or APIs provided by Mozy Enterprise to provision AAD user accounts.</span></span>

<span data-ttu-id="f7c94-216">**사용자 계정을 프로비전하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="f7c94-216">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="f7c94-217">**Mozy Enterprise** 테넌트에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-217">Log in to your **Mozy Enterprise** tenant.</span></span>

2. <span data-ttu-id="f7c94-218">**사용자**를 클릭한 후 **새 사용자 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-218">Click **Users**, and then click **Add New User**.</span></span>
   
   <span data-ttu-id="f7c94-219">![사용자](./media/active-directory-saas-mozy-enterprise-tutorial/ic777317.png "사용자")</span><span class="sxs-lookup"><span data-stu-id="f7c94-219">![Users](./media/active-directory-saas-mozy-enterprise-tutorial/ic777317.png "Users")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="f7c94-220">**Mozy**가 **인증 정책**에서 공급자로 선택된 경우에만 **새 사용자 추가** 옵션이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-220">The **Add New User** option is only displayed only if **Mozy** is selected as the provider under **Authentication policy**.</span></span> <span data-ttu-id="f7c94-221">SAML 인증이 구성된 경우 Single Sign-On을 통해 처음 로그인 시 사용자가 자동으로 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-221">If SAML Authentication is configured, then the users are added automatically on their first login through Single sign on.</span></span>
    
3. <span data-ttu-id="f7c94-222">새 사용자 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-222">On the new user dialog, perform the following steps:</span></span>
   
   <span data-ttu-id="f7c94-223">![사용자 추가](./media/active-directory-saas-mozy-enterprise-tutorial/ic777318.png "사용자 추가")</span><span class="sxs-lookup"><span data-stu-id="f7c94-223">![Add Users](./media/active-directory-saas-mozy-enterprise-tutorial/ic777318.png "Add Users")</span></span>
   
   <span data-ttu-id="f7c94-224">a.</span><span class="sxs-lookup"><span data-stu-id="f7c94-224">a.</span></span> <span data-ttu-id="f7c94-225">**그룹 선택** 목록에서 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-225">From the **Choose a Group** list, select a group.</span></span>
   
   <span data-ttu-id="f7c94-226">b.</span><span class="sxs-lookup"><span data-stu-id="f7c94-226">b.</span></span> <span data-ttu-id="f7c94-227">**사용자 유형** 목록에서 유형을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-227">From the **What type of user** list, select a type.</span></span>
   
   <span data-ttu-id="f7c94-228">c.</span><span class="sxs-lookup"><span data-stu-id="f7c94-228">c.</span></span> <span data-ttu-id="f7c94-229">**사용자 이름** 텍스트 상자에 Azure AD 사용자의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-229">In the **Username** textbox, type the name of the Azure AD user.</span></span>
   
   <span data-ttu-id="f7c94-230">d.</span><span class="sxs-lookup"><span data-stu-id="f7c94-230">d.</span></span> <span data-ttu-id="f7c94-231">**이메일** 텍스트 상자에 Azure AD 사용자의 이메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-231">In the **Email** textbox, type the email address of the Azure AD user.</span></span>
   
   <span data-ttu-id="f7c94-232">e.</span><span class="sxs-lookup"><span data-stu-id="f7c94-232">e.</span></span> <span data-ttu-id="f7c94-233">**사용자 명령 이메일 보내기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-233">Select **Send user instruction email**.</span></span>
   
   <span data-ttu-id="f7c94-234">f.</span><span class="sxs-lookup"><span data-stu-id="f7c94-234">f.</span></span> <span data-ttu-id="f7c94-235">**사용자 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-235">Click **Add User(s)**.</span></span>

     >[!NOTE]
     > <span data-ttu-id="f7c94-236">사용자를 만든 후 활성화되기 전에 계정을 확인하기 위해 링크가 포함된 Azure AD 사용자에게 이메일이 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-236">After creating the user, an email will be sent to the Azure AD user that includes a link to confirm the account before it becomes active.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f7c94-237">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="f7c94-237">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f7c94-238">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Mozy Enterprise에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-238">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Mozy Enterprise.</span></span>

![사용자 할당][200] 

<span data-ttu-id="f7c94-240">**Mozy Enterprise에 Britta Simon을 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="f7c94-240">**To assign Britta Simon to Mozy Enterprise, perform the following steps:**</span></span>

1. <span data-ttu-id="f7c94-241">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-241">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="f7c94-243">응용 프로그램 목록에서 **Mozy Enterprise**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-243">In the applications list, select **Mozy Enterprise**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_app.png) 

3. <span data-ttu-id="f7c94-245">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-245">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="f7c94-247">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-247">Click **Add** button.</span></span> <span data-ttu-id="f7c94-248">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="f7c94-250">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-250">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f7c94-251">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f7c94-252">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f7c94-253">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="f7c94-253">Testing single sign-on</span></span>

<span data-ttu-id="f7c94-254">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-254">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f7c94-255">액세스 패널에서 Mozy Enterprise 타일을 클릭하면 Mozy Enterprise 응용 프로그램의 로그인 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7c94-255">When you click the Mozy Enterprise tile in the Access Panel, you should get login page of Mozy Enterprise application.</span></span>
<span data-ttu-id="f7c94-256">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f7c94-256">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f7c94-257">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="f7c94-257">Additional resources</span></span>

* [<span data-ttu-id="f7c94-258">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="f7c94-258">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f7c94-259">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="f7c94-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_203.png

