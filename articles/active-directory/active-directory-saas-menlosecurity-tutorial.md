---
title: "자습서: Menlo Security와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 Menlo Security 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9e63fe6b-0ad0-405d-9e41-6a1a40a41df8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: jeedes
ms.openlocfilehash: 75366abafa551d21630b0edddb65db23b9ea9d42
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-menlo-security"></a><span data-ttu-id="4e26e-103">자습서: Menlo Security와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="4e26e-103">Tutorial: Azure Active Directory integration with Menlo Security</span></span>

<span data-ttu-id="4e26e-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Menlo Security를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-104">In this tutorial, you learn how to integrate Menlo Security with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4e26e-105">Menlo Security를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-105">Integrating Menlo Security with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4e26e-106">Menlo Security에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-106">You can control in Azure AD who has access to Menlo Security</span></span>
- <span data-ttu-id="4e26e-107">사용자의 Azure AD 계정으로 Menlo Security에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-107">You can enable your users to automatically get signed-on to Menlo Security (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4e26e-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="4e26e-109">Azure AD와의 SaaS 앱 통합에 대한 자세한 내용은</span><span class="sxs-lookup"><span data-stu-id="4e26e-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="4e26e-110">[Azure Active Directory를 사용한 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4e26e-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4e26e-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="4e26e-111">Prerequisites</span></span>

<span data-ttu-id="4e26e-112">Menlo Security와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-112">To configure Azure AD integration with Menlo Security, you need the following items:</span></span>

- <span data-ttu-id="4e26e-113">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="4e26e-113">An Azure AD subscription</span></span>
- <span data-ttu-id="4e26e-114">Menlo Security Single Sign-on이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="4e26e-114">A Menlo Security single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4e26e-115">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4e26e-116">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4e26e-117">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="4e26e-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4e26e-118">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4e26e-119">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="4e26e-119">Scenario description</span></span>
<span data-ttu-id="4e26e-120">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4e26e-121">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4e26e-122">갤러리에서 Menlo Security 추가</span><span class="sxs-lookup"><span data-stu-id="4e26e-122">Adding Menlo Security from the gallery</span></span>
2. <span data-ttu-id="4e26e-123">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="4e26e-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-menlo-security-from-the-gallery"></a><span data-ttu-id="4e26e-124">갤러리에서 Menlo Security 추가</span><span class="sxs-lookup"><span data-stu-id="4e26e-124">Adding Menlo Security from the gallery</span></span>
<span data-ttu-id="4e26e-125">Menlo Security가 Azure AD로 통합되도록 구성하려면 갤러리에서 Menlo Security를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-125">To configure the integration of Menlo Security into Azure AD, you need to add Menlo Security from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4e26e-126">**갤러리에서 Menlo Security를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="4e26e-126">**To add Menlo Security from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4e26e-127">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4e26e-129">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4e26e-130">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-130">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="4e26e-132">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="4e26e-134">검색 상자에 **Menlo Security**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-134">In the search box, type **Menlo Security**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_search.png)

5. <span data-ttu-id="4e26e-136">결과 창에서 **Menlo Security**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-136">In the results panel, select **Menlo Security**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4e26e-138">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="4e26e-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4e26e-139">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Menlo Security에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-139">In this section, you configure and test Azure AD single sign-on with Menlo Security based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4e26e-140">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 대응하는 Menlo Security 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Menlo Security is to a user in Azure AD.</span></span> <span data-ttu-id="4e26e-141">즉, Azure AD 사용자와 Menlo Security의 관련 사용자 간에 연결 관계가 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-141">In other words, a link relationship between an Azure AD user and the related user in Menlo Security needs to be established.</span></span>

<span data-ttu-id="4e26e-142">이 연결 관계는 Azure AD의 **사용자 이름** 값을 Menlo Security의 **Username** 값으로 할당하여 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Menlo Security.</span></span>

<span data-ttu-id="4e26e-143">Menlo Security에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-143">To configure and test Azure AD single sign-on with Menlo Security, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4e26e-144">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="4e26e-145">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4e26e-146">**[Menlo Security 테스트 사용자 만들기](#creating-a-menlo-security-test-user)** - Britta Simon의 Azure AD 표현과 연결되는 대응 사용자를 Menlo Security에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-146">**[Creating a Menlo Security test user](#creating-a-menlo-security-test-user)** - to have a counterpart of Britta Simon in Menlo Security that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="4e26e-147">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4e26e-148">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4e26e-149">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="4e26e-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4e26e-150">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Menlo Security 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Menlo Security application.</span></span>

<span data-ttu-id="4e26e-151">**Menlo Security에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="4e26e-151">**To configure Azure AD single sign-on with Menlo Security, perform the following steps:**</span></span>

1. <span data-ttu-id="4e26e-152">Azure Portal의 **Menlo Security** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-152">In the Azure portal, on the **Menlo Security** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="4e26e-154">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_samlbase.png)

3. <span data-ttu-id="4e26e-156">**Menlo Security 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-156">On the **Menlo Security Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_url.png)

    <span data-ttu-id="4e26e-158">a.</span><span class="sxs-lookup"><span data-stu-id="4e26e-158">a.</span></span> <span data-ttu-id="4e26e-159">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<subdomain>.menlosecurity.com/account/login`</span><span class="sxs-lookup"><span data-stu-id="4e26e-159">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.menlosecurity.com/account/login`</span></span>

    <span data-ttu-id="4e26e-160">b.</span><span class="sxs-lookup"><span data-stu-id="4e26e-160">b.</span></span> <span data-ttu-id="4e26e-161">**식별자** 텍스트 상자에서 `https://<subdomain>.menlosecurity.com/safeview-auth-server/saml/metadata` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-161">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.menlosecurity.com/safeview-auth-server/saml/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4e26e-162">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-162">These values are not the real.</span></span> <span data-ttu-id="4e26e-163">실제 로그온 URL 및 식별자로 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-163">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="4e26e-164">이러한 값을 얻으려면 [Menlo Security 클라이언트 지원 팀](https://www.menlosecurity.com/menlo-contact)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="4e26e-164">Contact [Menlo Security Client support team](https://www.menlosecurity.com/menlo-contact) to get these values.</span></span> 
 
4. <span data-ttu-id="4e26e-165">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-165">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the Certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_certificate.png) 

5. <span data-ttu-id="4e26e-167">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-167">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4e26e-169">**Menlo Security 구성** 섹션에서 **Menlo Security 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-169">On the **Menlo Security Configuration** section, click **Configure Menlo Security** to open **Configure sign-on** window.</span></span> <span data-ttu-id="4e26e-170">**빠른 참조 섹션**에서 **SAML 엔터티 ID** 및 **SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-170">Copy the **SAML Entity ID**, and **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_configure.png) 

7. <span data-ttu-id="4e26e-172">**Menlo Security** 쪽에서 Single Sign-On을 구성하려면 관리자 권한으로 **Menlo Security** 웹 사이트에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-172">To configure single sign-on on **Menlo Security** side, login to the **Menlo Security** website as an administrator.</span></span>

8. <span data-ttu-id="4e26e-173">**Settings(설정)**에서 **Authentication(인증)**으로 이동하여 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-173">Under **Settings** go to **Authentication** and perform following actions:</span></span>
    
    ![Single Sign-on 구성](./media/active-directory-saas-menlosecurity-tutorial/menlo_user_setup.png)

    <span data-ttu-id="4e26e-175">a.</span><span class="sxs-lookup"><span data-stu-id="4e26e-175">a.</span></span> <span data-ttu-id="4e26e-176">**Enable user authentication using SAML(SAML을 사용한 사용자 인증 사용)** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-176">Tick the checkbox **Enable user authentication using SAML**.</span></span>

    <span data-ttu-id="4e26e-177">b.</span><span class="sxs-lookup"><span data-stu-id="4e26e-177">b.</span></span> <span data-ttu-id="4e26e-178">**Allow External Access(외부 액세스 허용)**을 **Yes(예)**로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-178">Select **Allow External Access** to **Yes**.</span></span>

    <span data-ttu-id="4e26e-179">c.</span><span class="sxs-lookup"><span data-stu-id="4e26e-179">c.</span></span> <span data-ttu-id="4e26e-180">**SAML Provider(SAML 공급자)**에서 **Azure Active Directory**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-180">Under **SAML Provider**, select **Azure Active Directory**.</span></span>

    <span data-ttu-id="4e26e-181">d.</span><span class="sxs-lookup"><span data-stu-id="4e26e-181">d.</span></span> <span data-ttu-id="4e26e-182">**SAML 2.0 Endpoint(SAML 2.0 끝점)**: Azure Portal에서 복사한 **SAML Single Sign-On 서비스 URL**을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-182">**SAML 2.0 Endpoint** : Paste the **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="4e26e-183">e.</span><span class="sxs-lookup"><span data-stu-id="4e26e-183">e.</span></span> <span data-ttu-id="4e26e-184">**Service Identifier (Issuer)(서비스 식별자/발급자)**: Azure Portal에서 복사한 **SAML 엔터티 ID**를 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-184">**Service Identifier (Issuer)** : Paste the **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="4e26e-185">f.</span><span class="sxs-lookup"><span data-stu-id="4e26e-185">f.</span></span> <span data-ttu-id="4e26e-186">**X.509 Certificate(X.509 인증서)** : Azure Portal에서 다운로드한 **인증서(Base64)**를 메모장에서 열어서 이 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-186">**X.509 Certificate** : Open the **Certificate (Base64)** downloaded from the Azure Portal in notepad and paste it in this box.</span></span>

    <span data-ttu-id="4e26e-187">g.</span><span class="sxs-lookup"><span data-stu-id="4e26e-187">g.</span></span> <span data-ttu-id="4e26e-188">**저장**을 클릭하여 설정을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-188">Click **Save** to save the settings.</span></span>

> [!TIP]
> <span data-ttu-id="4e26e-189">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="4e26e-190">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="4e26e-191">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4e26e-192">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="4e26e-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="4e26e-193">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="4e26e-195">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="4e26e-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4e26e-196">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4e26e-198">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4e26e-200">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4e26e-202">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4e26e-204">a.</span><span class="sxs-lookup"><span data-stu-id="4e26e-204">a.</span></span> <span data-ttu-id="4e26e-205">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4e26e-206">b.</span><span class="sxs-lookup"><span data-stu-id="4e26e-206">b.</span></span> <span data-ttu-id="4e26e-207">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4e26e-208">c.</span><span class="sxs-lookup"><span data-stu-id="4e26e-208">c.</span></span> <span data-ttu-id="4e26e-209">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="4e26e-210">d.</span><span class="sxs-lookup"><span data-stu-id="4e26e-210">d.</span></span> <span data-ttu-id="4e26e-211">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-211">Click **Create**.</span></span>
 
### <a name="creating-a-menlo-security-test-user"></a><span data-ttu-id="4e26e-212">Menlo Security 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="4e26e-212">Creating a Menlo Security test user</span></span>
 
<span data-ttu-id="4e26e-213">이 섹션에서는 Menlo Security에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-213">In this section, you create a user called Britta Simon in Menlo Security.</span></span> <span data-ttu-id="4e26e-214">Menlo Security 플랫폼에서 사용자를 추가하려면 [Menlo Security 클라이언트 지원 팀](https://www.menlosecurity.com/menlo-contact)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="4e26e-214">Work with [Menlo Security Client support team](https://www.menlosecurity.com/menlo-contact) to add the users in the Menlo Security platform.</span></span> <span data-ttu-id="4e26e-215">Single Sign-On을 사용하려면 먼저 사용자를 만들고 활성화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-215">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="4e26e-216">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="4e26e-216">Assigning the Azure AD test user</span></span>

<span data-ttu-id="4e26e-217">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Menlo Security에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Menlo Security.</span></span>

![사용자 할당][200] 

<span data-ttu-id="4e26e-219">**Britta Simon을 Menlo Security에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="4e26e-219">**To assign Britta Simon to Menlo Security, perform the following steps:**</span></span>

1. <span data-ttu-id="4e26e-220">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="4e26e-222">응용 프로그램 목록에서 **Menlo Security**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-222">In the applications list, select **Menlo Security**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_app.png) 

3. <span data-ttu-id="4e26e-224">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-224">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="4e26e-226">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-226">Click **Add** button.</span></span> <span data-ttu-id="4e26e-227">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="4e26e-229">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="4e26e-230">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4e26e-231">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4e26e-232">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="4e26e-232">Testing single sign-on</span></span>

<span data-ttu-id="4e26e-233">이 섹션에서는 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-233">In this section, you test your Azure AD single sign-on configuration.</span></span>

<span data-ttu-id="4e26e-234">"InPrivate" 또는 "Incognito" 모드에서 브라우저 창을 열어 새 인증을 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-234">Open a browser window in an "InPrivate" or "Incognito" mode to trigger a new authentication.</span></span>  <span data-ttu-id="4e26e-235">Internet Explorer에서는 Ctrl+Shift+P를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-235">In Internet Explorer, use Ctrl+Shift+P.</span></span>  <span data-ttu-id="4e26e-236">Chrome에서는 Ctrl+Shift+N을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-236">In Chrome, use Ctrl+Shift+N.</span></span>  <span data-ttu-id="4e26e-237">개인 탐색 창에서 보호된 리소스로 이동한 후 Azure AD 로그인을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-237">In the private browsing window, browse to a protected resource and perform an Azure AD login.</span></span>  <span data-ttu-id="4e26e-238">로그인에 성공하면 격리된 세션에서 요청된 사이트로 이동됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e26e-238">Upon successful login, you will be taken to the requested site in an isolation session.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4e26e-239">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="4e26e-239">Additional resources</span></span>

* [<span data-ttu-id="4e26e-240">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="4e26e-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4e26e-241">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="4e26e-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_203.png

