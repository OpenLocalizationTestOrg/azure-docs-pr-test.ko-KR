---
title: "자습서: Egnyte와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 Egnyte 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8c2101d4-1779-4b36-8464-5c1ff780da18
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: 62d01333b61e73c83588d2d1701c0c300df4ab1c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-egnyte"></a><span data-ttu-id="597ca-103">자습서: Egnyte와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="597ca-103">Tutorial: Azure Active Directory integration with Egnyte</span></span>

<span data-ttu-id="597ca-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Egnyte를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-104">In this tutorial, you learn how to integrate Egnyte with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="597ca-105">Egnyte를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-105">Integrating Egnyte with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="597ca-106">Egnyte에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-106">You can control in Azure AD who has access to Egnyte</span></span>
- <span data-ttu-id="597ca-107">사용자가 해당 Azure AD 계정으로 Egnyte에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-107">You can enable your users to automatically get signed-on to Egnyte (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="597ca-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="597ca-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="597ca-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="597ca-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="597ca-110">Prerequisites</span></span>

<span data-ttu-id="597ca-111">Egnyte와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-111">To configure Azure AD integration with Egnyte, you need the following items:</span></span>

- <span data-ttu-id="597ca-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="597ca-112">An Azure AD subscription</span></span>
- <span data-ttu-id="597ca-113">Egnyte Single Sign-on이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="597ca-113">An Egnyte single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="597ca-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="597ca-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="597ca-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="597ca-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="597ca-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="597ca-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="597ca-118">Scenario description</span></span>
<span data-ttu-id="597ca-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="597ca-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="597ca-121">갤러리에서 Egnyte 추가</span><span class="sxs-lookup"><span data-stu-id="597ca-121">Adding Egnyte from the gallery</span></span>
2. <span data-ttu-id="597ca-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="597ca-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-egnyte-from-the-gallery"></a><span data-ttu-id="597ca-123">갤러리에서 Egnyte 추가</span><span class="sxs-lookup"><span data-stu-id="597ca-123">Adding Egnyte from the gallery</span></span>
<span data-ttu-id="597ca-124">Egnyte의 Azure AD 통합을 구성하려면 갤러리의 Egnyte를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-124">To configure the integration of Egnyte into Azure AD, you need to add Egnyte from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="597ca-125">**갤러리에서 Egnyte를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="597ca-125">**To add Egnyte from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="597ca-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="597ca-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="597ca-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="597ca-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="597ca-133">검색 상자에 **Egnyte**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-133">In the search box, type **Egnyte**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_search.png)

5. <span data-ttu-id="597ca-135">결과 패널에서 **Egnyte**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-135">In the results panel, select **Egnyte**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="597ca-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="597ca-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="597ca-138">이 섹션에서는 “Britta Simon”이라는 테스트 사용자를 기반으로 Egnyte에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-138">In this section, you configure and test Azure AD single sign-on with Egnyte based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="597ca-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Egnyte 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Egnyte is to a user in Azure AD.</span></span> <span data-ttu-id="597ca-140">즉, Azure AD 사용자와 Egnyte의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-140">In other words, a link relationship between an Azure AD user and the related user in Egnyte needs to be established.</span></span>

<span data-ttu-id="597ca-141">Egnyte에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-141">In Egnyte, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="597ca-142">Egnyte에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-142">To configure and test Azure AD single sign-on with Egnyte, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="597ca-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="597ca-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="597ca-145">**[Egnyte 테스트 사용자 만들기](#creating-an-egnyte-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 Egnyte에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-145">**[Creating an Egnyte test user](#creating-an-egnyte-test-user)** - to have a counterpart of Britta Simon in Egnyte that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="597ca-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="597ca-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="597ca-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="597ca-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="597ca-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Egnyte 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Egnyte application.</span></span>

<span data-ttu-id="597ca-150">**Egnyte에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="597ca-150">**To configure Azure AD single sign-on with Egnyte, perform the following steps:**</span></span>

1. <span data-ttu-id="597ca-151">Azure Portal의 **Egnyte** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-151">In the Azure portal, on the **Egnyte** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="597ca-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_samlbase.png)

3. <span data-ttu-id="597ca-155">**Egnyte 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-155">On the **Egnyte Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_url.png)

    <span data-ttu-id="597ca-157">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<companyname>.egnyte.com`</span><span class="sxs-lookup"><span data-stu-id="597ca-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.egnyte.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="597ca-158">이 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-158">This value is not real.</span></span> <span data-ttu-id="597ca-159">이 값을 실제 로그온 URL로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="597ca-160">이 값을 얻으려면 [Egnyte 클라이언트 지원 팀](https://www.egnyte.com/corp/contact_egnyte.html)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="597ca-160">Contact [Egnyte Client support team](https://www.egnyte.com/corp/contact_egnyte.html) to get this value.</span></span> 
 
4. <span data-ttu-id="597ca-161">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_certificate.png) 

5. <span data-ttu-id="597ca-163">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-163">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-egnyte-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="597ca-165">**Egnyte 구성** 섹션에서 **Egnyte 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-165">On the **Egnyte Configuration** section, click **Configure Egnyte** to open **Configure sign-on** window.</span></span> <span data-ttu-id="597ca-166">**빠른 참조 섹션**에서 **SAML 엔터티 ID 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-166">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_configure.png) 

7. <span data-ttu-id="597ca-168">다른 웹 브라우저 창에서 Egnyte 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-168">In a different web browser window, log in to your Egnyte company site as an administrator.</span></span>

8. <span data-ttu-id="597ca-169">**설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-169">Click **Settings**.</span></span>
   
   <span data-ttu-id="597ca-170">![설정](./media/active-directory-saas-egnyte-tutorial/ic787819.png "설정")</span><span class="sxs-lookup"><span data-stu-id="597ca-170">![Settings](./media/active-directory-saas-egnyte-tutorial/ic787819.png "Settings")</span></span>

9. <span data-ttu-id="597ca-171">메뉴에서 **설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-171">In the menu, click **Settings**.</span></span>

   <span data-ttu-id="597ca-172">![설정](./media/active-directory-saas-egnyte-tutorial/ic787820.png "설정")</span><span class="sxs-lookup"><span data-stu-id="597ca-172">![Settings](./media/active-directory-saas-egnyte-tutorial/ic787820.png "Settings")</span></span>

10. <span data-ttu-id="597ca-173">**구성**탭을 클릭한 다음 **보안**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-173">Click the **Configuration** tab, and then click **Security**.</span></span>

    <span data-ttu-id="597ca-174">![보안](./media/active-directory-saas-egnyte-tutorial/ic787821.png "보안")</span><span class="sxs-lookup"><span data-stu-id="597ca-174">![Security](./media/active-directory-saas-egnyte-tutorial/ic787821.png "Security")</span></span>

11. <span data-ttu-id="597ca-175">**Single Sign-On 인증** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-175">In the **Single Sign-On Authentication** section, perform the following steps:</span></span>

    <span data-ttu-id="597ca-176">![Single Sign On 인증](./media/active-directory-saas-egnyte-tutorial/ic787822.png "Single Sign On 인증")</span><span class="sxs-lookup"><span data-stu-id="597ca-176">![Single Sign On Authentication](./media/active-directory-saas-egnyte-tutorial/ic787822.png "Single Sign On Authentication")</span></span>   
    
    <span data-ttu-id="597ca-177">a.</span><span class="sxs-lookup"><span data-stu-id="597ca-177">a.</span></span> <span data-ttu-id="597ca-178">**Single sign-on 인증**으로 **SAML 2.0**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-178">As **Single sign-on authentication**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="597ca-179">b.</span><span class="sxs-lookup"><span data-stu-id="597ca-179">b.</span></span> <span data-ttu-id="597ca-180">**ID 공급자**로 **AzureAD**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-180">As **Identity provider**, select **AzureAD**.</span></span>
   
    <span data-ttu-id="597ca-181">c.</span><span class="sxs-lookup"><span data-stu-id="597ca-181">c.</span></span> <span data-ttu-id="597ca-182">Azure Portal에서 복사한 **SAML Single Sign-On 서비스 URL**을 **ID 공급자 로그인 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-182">Paste **SAML Single Sign-On Service URL** copied from Azure portal into the **Identity provider login URL** textbox.</span></span>
   
    <span data-ttu-id="597ca-183">d.</span><span class="sxs-lookup"><span data-stu-id="597ca-183">d.</span></span> <span data-ttu-id="597ca-184">Azure Portal에서 복사한 **SAML 엔터티 ID**를 **ID 공급자 엔터티 ID** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-184">Paste **SAML Entity ID** which you have copied from Azure portal into the **Identity provider entity ID** textbox.</span></span>
      
    <span data-ttu-id="597ca-185">e.</span><span class="sxs-lookup"><span data-stu-id="597ca-185">e.</span></span> <span data-ttu-id="597ca-186">Azure Portal에서 다운로드한 base-64로 인코딩된 인증서를 메모장에서 열고, 콘텐츠를 클립보드에 복사한 다음, **ID 공급자 인증서** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-186">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **Identity provider certificate** textbox.</span></span>
   
    <span data-ttu-id="597ca-187">f.</span><span class="sxs-lookup"><span data-stu-id="597ca-187">f.</span></span> <span data-ttu-id="597ca-188">**기본 사용자 매핑**으로 **전자 메일 주소**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-188">As **Default user mapping**, select **Email address**.</span></span>
   
    <span data-ttu-id="597ca-189">g.</span><span class="sxs-lookup"><span data-stu-id="597ca-189">g.</span></span> <span data-ttu-id="597ca-190">**도메인 특정 발급자 값 사용**을 **비활성화**로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-190">As **Use domain-specific issuer value**, select **disabled**.</span></span>
   
    <span data-ttu-id="597ca-191">h.</span><span class="sxs-lookup"><span data-stu-id="597ca-191">h.</span></span> <span data-ttu-id="597ca-192">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-192">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="597ca-193">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-193">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="597ca-194">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-194">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="597ca-195">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-195">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="597ca-196">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="597ca-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="597ca-197">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-197">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="597ca-199">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="597ca-199">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="597ca-200">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-200">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-egnyte-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="597ca-202">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-202">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-egnyte-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="597ca-204">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-204">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-egnyte-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="597ca-206">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-206">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-egnyte-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="597ca-208">a.</span><span class="sxs-lookup"><span data-stu-id="597ca-208">a.</span></span> <span data-ttu-id="597ca-209">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-209">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="597ca-210">b.</span><span class="sxs-lookup"><span data-stu-id="597ca-210">b.</span></span> <span data-ttu-id="597ca-211">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-211">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="597ca-212">c.</span><span class="sxs-lookup"><span data-stu-id="597ca-212">c.</span></span> <span data-ttu-id="597ca-213">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-213">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="597ca-214">d.</span><span class="sxs-lookup"><span data-stu-id="597ca-214">d.</span></span> <span data-ttu-id="597ca-215">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-215">Click **Create**.</span></span>
 
### <a name="creating-an-egnyte-test-user"></a><span data-ttu-id="597ca-216">Egnyte 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="597ca-216">Creating an Egnyte test user</span></span>

<span data-ttu-id="597ca-217">Azure AD 사용자가 Egnyte에 로그인할 수 있도록 하려면 Egnyte로 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-217">To enable Azure AD users to log in to Egnyte, they must be provisioned into Egnyte.</span></span> <span data-ttu-id="597ca-218">Egnyte의 경우 프로비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-218">In the case of Egnyte, provisioning is a manual task.</span></span>

<span data-ttu-id="597ca-219">**사용자 계정을 프로비전하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="597ca-219">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="597ca-220">**Egnyte** 회사 사이트에 관리자 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-220">Log in to your **Egnyte** company site as administrator.</span></span>

2. <span data-ttu-id="597ca-221">**설정 \> 사용자 및 그룹**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-221">Go to **Settings \> Users & Groups**.</span></span>

3. <span data-ttu-id="597ca-222">**새 사용자 추가**를 클릭한 다음 추가하려는 사용자의 유형을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-222">Click **Add New User**, and then select the type of user you want to add.</span></span>
   
   <span data-ttu-id="597ca-223">![사용자](./media/active-directory-saas-egnyte-tutorial/ic787824.png "사용자")</span><span class="sxs-lookup"><span data-stu-id="597ca-223">![Users](./media/active-directory-saas-egnyte-tutorial/ic787824.png "Users")</span></span>

4. <span data-ttu-id="597ca-224">**새 표준 사용자** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-224">In the **New Standard User** section, perform the following steps:</span></span>
   
   <span data-ttu-id="597ca-225">![새 표준 사용자](./media/active-directory-saas-egnyte-tutorial/ic787825.png "새 표준 사용자")</span><span class="sxs-lookup"><span data-stu-id="597ca-225">![New Standard User](./media/active-directory-saas-egnyte-tutorial/ic787825.png "New Standard User")</span></span>   

   <span data-ttu-id="597ca-226">a.</span><span class="sxs-lookup"><span data-stu-id="597ca-226">a.</span></span> <span data-ttu-id="597ca-227">프로비전하려는 유효한 Azure Active Directory 계정의 **전자 메일**, **사용자 이름** 및 다른 세부 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-227">Type the **Email**, **Username**, and other details of a valid Azure Active Directory account you want to provision.</span></span>
   
   <span data-ttu-id="597ca-228">b.</span><span class="sxs-lookup"><span data-stu-id="597ca-228">b.</span></span> <span data-ttu-id="597ca-229">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-229">Click **Save**.</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="597ca-230">Azure Active Directory 계정 소유자는 알림 전자 메일을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-230">The Azure Active Directory account holder will receive a notification email.</span></span>
    >

>[!NOTE]
><span data-ttu-id="597ca-231">다른 Egnyte 사용자 계정 생성 도구 또는 Egnyte가 제공한 API를 사용하여 AAD 사용자 계정을 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-231">You can use any other Egnyte user account creation tools or APIs provided by Egnyte to provision AAD user accounts.</span></span>
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="597ca-232">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="597ca-232">Assigning the Azure AD test user</span></span>

<span data-ttu-id="597ca-233">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Egnyte에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-233">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Egnyte.</span></span>

![사용자 할당][200] 

<span data-ttu-id="597ca-235">**Britta Simon을 Egnyte에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="597ca-235">**To assign Britta Simon to Egnyte, perform the following steps:**</span></span>

1. <span data-ttu-id="597ca-236">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-236">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="597ca-238">응용 프로그램 목록에서 **Egnyte**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-238">In the applications list, select **Egnyte**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_app.png) 

3. <span data-ttu-id="597ca-240">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-240">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="597ca-242">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-242">Click **Add** button.</span></span> <span data-ttu-id="597ca-243">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="597ca-245">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-245">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="597ca-246">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="597ca-247">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="597ca-248">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="597ca-248">Testing single sign-on</span></span>

<span data-ttu-id="597ca-249">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-249">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="597ca-250">액세스 패널에서 Egnyte 타일을 클릭하면 Egnyte 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="597ca-250">When you click the Egnyte tile in the Access Panel, you should get automatically signed-on to your Egnyte application.</span></span>
<span data-ttu-id="597ca-251">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="597ca-251">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="597ca-252">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="597ca-252">Additional resources</span></span>

* [<span data-ttu-id="597ca-253">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="597ca-253">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="597ca-254">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="597ca-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_203.png

