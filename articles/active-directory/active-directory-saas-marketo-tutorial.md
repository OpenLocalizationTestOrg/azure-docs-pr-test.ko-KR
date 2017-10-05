---
title: "자습서: Marketo와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 Marketo 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b88c45f5-d288-4717-835c-ca965add8735
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: e146fd5a8075bc9c7ba049b25e5f301fc2645ed9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-marketo"></a><span data-ttu-id="684f6-103">자습서:Azure Active Directory와 Marketo 통합</span><span class="sxs-lookup"><span data-stu-id="684f6-103">Tutorial: Azure Active Directory integration with Marketo</span></span>

<span data-ttu-id="684f6-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Marketo를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-104">In this tutorial, you learn how to integrate Marketo with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="684f6-105">Marketo를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-105">Integrating Marketo with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="684f6-106">Marketo에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-106">You can control in Azure AD who has access to Marketo</span></span>
- <span data-ttu-id="684f6-107">사용자가 해당 Azure AD 계정으로 Marketo에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-107">You can enable your users to automatically get signed-on to Marketo (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="684f6-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="684f6-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="684f6-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="684f6-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="684f6-110">Prerequisites</span></span>

<span data-ttu-id="684f6-111">Marketo와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-111">To configure Azure AD integration with Marketo, you need the following items:</span></span>

- <span data-ttu-id="684f6-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="684f6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="684f6-113">Marketo Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="684f6-113">A Marketo single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="684f6-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="684f6-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="684f6-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="684f6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="684f6-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="684f6-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="684f6-118">Scenario description</span></span>
<span data-ttu-id="684f6-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="684f6-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="684f6-121">갤러리에서 Marketo 추가</span><span class="sxs-lookup"><span data-stu-id="684f6-121">Adding Marketo from the gallery</span></span>
2. <span data-ttu-id="684f6-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="684f6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-marketo-from-the-gallery"></a><span data-ttu-id="684f6-123">갤러리에서 Marketo 추가</span><span class="sxs-lookup"><span data-stu-id="684f6-123">Adding Marketo from the gallery</span></span>
<span data-ttu-id="684f6-124">Marketo의 Azure AD 통합을 구성하려면 갤러리의 Marketo를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-124">To configure the integration of Marketo into Azure AD, you need to add Marketo from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="684f6-125">**갤러리에서 Marketo를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="684f6-125">**To add Marketo from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="684f6-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="684f6-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="684f6-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="684f6-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="684f6-133">검색 상자에 **Marketo**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-133">In the search box, type **Marketo**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_search.png)

5. <span data-ttu-id="684f6-135">결과 창에서 **Marketo**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-135">In the results panel, select **Marketo**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="684f6-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="684f6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="684f6-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Marketo에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-138">In this section, you configure and test Azure AD single sign-on with Marketo based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="684f6-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Marketo 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Marketo is to a user in Azure AD.</span></span> <span data-ttu-id="684f6-140">즉, Azure AD 사용자와 Marketo의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-140">In other words, a link relationship between an Azure AD user and the related user in Marketo needs to be established.</span></span>

<span data-ttu-id="684f6-141">Marketo에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 연결 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-141">In Marketo, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="684f6-142">Marketo에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-142">To configure and test Azure AD single sign-on with Marketo, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="684f6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="684f6-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="684f6-145">**[Marketo 테스트 사용자 만들기](#creating-a-marketo-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 Marketo에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-145">**[Creating a Marketo test user](#creating-a-marketo-test-user)** - to have a counterpart of Britta Simon in Marketo that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="684f6-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="684f6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="684f6-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="684f6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="684f6-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Marketo 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Marketo application.</span></span>

<span data-ttu-id="684f6-150">**Marketo에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="684f6-150">**To configure Azure AD single sign-on with Marketo, perform the following steps:**</span></span>

1. <span data-ttu-id="684f6-151">Azure Portal의 **Marketo** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-151">In the Azure portal, on the **Marketo** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="684f6-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_samlbase.png)

3. <span data-ttu-id="684f6-155">**Marketo 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-155">On the **Marketo Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_url.png)

    <span data-ttu-id="684f6-157">a.</span><span class="sxs-lookup"><span data-stu-id="684f6-157">a.</span></span> <span data-ttu-id="684f6-158">**식별자** 텍스트 상자에서 `https://saml.marketo.com/sp` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-158">In the **Identifier** textbox, type a URL using the following pattern: `https://saml.marketo.com/sp`</span></span>

    <span data-ttu-id="684f6-159">b.</span><span class="sxs-lookup"><span data-stu-id="684f6-159">b.</span></span> <span data-ttu-id="684f6-160">**회신 URL** 텍스트 상자에 다음 패턴으로 URL을 입력합니다.`https://login.marketo.com/saml/assertion/\<munchkinid\>`</span><span class="sxs-lookup"><span data-stu-id="684f6-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://login.marketo.com/saml/assertion/\<munchkinid\>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="684f6-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-161">These values are not real.</span></span> <span data-ttu-id="684f6-162">실제 식별자 및 회신 URL로 해당 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="684f6-163">이러한 값을 얻으려면 [Marketo 지원 팀](http://investors.marketo.com/contactus.cfm)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="684f6-163">Contact [Marketo support team](http://investors.marketo.com/contactus.cfm) to get these values.</span></span>
 
4. <span data-ttu-id="684f6-164">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_certificate.png) 

5. <span data-ttu-id="684f6-166">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-166">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-marketo-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="684f6-168">**Marketo 구성** 섹션에서 **Marketo 구성**을 클릭하여 **로그인 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-168">On the **Marketo Configuration** section, click **Configure Marketo** to open **Configure sign-on** window.</span></span> <span data-ttu-id="684f6-169">**빠른 참조 섹션**에서 **로그아웃 URL, SAML 엔터티 ID 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_configure.png) 

7. <span data-ttu-id="684f6-171">응용 프로그램의 Munchkin ID를 가져오려면 관리자 자격 증명을 사용하여 Marketo에 로그인하고 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-171">To get Munchkin Id of your application, log in to Marketo using admin credentials and perform following actions:</span></span>
   
    <span data-ttu-id="684f6-172">a.</span><span class="sxs-lookup"><span data-stu-id="684f6-172">a.</span></span> <span data-ttu-id="684f6-173">관리자 자격 증명을 사용하여 Marketo 앱에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-173">Log in to Marketo app using admin credentials.</span></span>
   
    <span data-ttu-id="684f6-174">b.</span><span class="sxs-lookup"><span data-stu-id="684f6-174">b.</span></span> <span data-ttu-id="684f6-175">위쪽 탐색 창에서 **관리자** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-175">Click the **Admin** button on the top navigation pane.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    <span data-ttu-id="684f6-177">c.</span><span class="sxs-lookup"><span data-stu-id="684f6-177">c.</span></span> <span data-ttu-id="684f6-178">통합 메뉴로 이동하여 **Munchkin 링크**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-178">Navigate to the Integration menu and click the **Munchkin link**.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_11.png)
   
    <span data-ttu-id="684f6-180">d.</span><span class="sxs-lookup"><span data-stu-id="684f6-180">d.</span></span> <span data-ttu-id="684f6-181">화면에 표시된 Munchkin ID를 복사하고 Azure AD 구성 마법사에서 회신 URL을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-181">Copy the Munchkin Id shown on the screen and complete your Reply URL in the Azure AD configuration wizard.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_12.png) 

8. <span data-ttu-id="684f6-183">아래 단계에 따라 응용 프로그램에서 SSO를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-183">To configure the SSO in the application, follow the below steps:</span></span>
   
    <span data-ttu-id="684f6-184">a.</span><span class="sxs-lookup"><span data-stu-id="684f6-184">a.</span></span> <span data-ttu-id="684f6-185">관리자 자격 증명을 사용하여 Marketo 앱에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-185">Log in to Marketo app using admin credentials.</span></span>
   
    <span data-ttu-id="684f6-186">b.</span><span class="sxs-lookup"><span data-stu-id="684f6-186">b.</span></span> <span data-ttu-id="684f6-187">위쪽 탐색 창에서 **관리자** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-187">Click the **Admin** button on the top navigation pane.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    <span data-ttu-id="684f6-189">c.</span><span class="sxs-lookup"><span data-stu-id="684f6-189">c.</span></span> <span data-ttu-id="684f6-190">통합 메뉴로 이동하여 **Single Sign On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-190">Navigate to the Integration menu and click **Single Sign On**.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_07.png) 
   
    <span data-ttu-id="684f6-192">d.</span><span class="sxs-lookup"><span data-stu-id="684f6-192">d.</span></span> <span data-ttu-id="684f6-193">SAML 설정을 사용하려면 **편집** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-193">To enable the SAML Settings, click **Edit** button.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_08.png) 
   
    <span data-ttu-id="684f6-195">e.</span><span class="sxs-lookup"><span data-stu-id="684f6-195">e.</span></span> <span data-ttu-id="684f6-196">Single Sign-On 설정을 사용하도록 **설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-196">**Enabled** Single Sign-On settings.</span></span>
   
    <span data-ttu-id="684f6-197">f.</span><span class="sxs-lookup"><span data-stu-id="684f6-197">f.</span></span> <span data-ttu-id="684f6-198">**SAML 엔터티 ID**를 **발급자 ID** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-198">Paste the **SAML Entity ID**, in the **Issuer ID** textbox.</span></span>
   
    <span data-ttu-id="684f6-199">g.</span><span class="sxs-lookup"><span data-stu-id="684f6-199">g.</span></span> <span data-ttu-id="684f6-200">**엔터티 ID** 텍스트 상자에 URL을 `http://saml.marketo.com/sp`로 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-200">In the **Entity ID** textbox, enter the URL as `http://saml.marketo.com/sp`.</span></span>
   
    <span data-ttu-id="684f6-201">h.</span><span class="sxs-lookup"><span data-stu-id="684f6-201">h.</span></span> <span data-ttu-id="684f6-202">**이름 식별자 요소**로 사용자 ID 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-202">Select the User ID Location as **Name Identifier element**.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_09.png)
   
    > [!NOTE]
    > <span data-ttu-id="684f6-204">사용자 ID가 UPN 값이 아닌 경우 특성 탭에서 값을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-204">If your User Identifier is not UPN value then change the value in the Attribute tab.</span></span>
   
    <span data-ttu-id="684f6-205">i.</span><span class="sxs-lookup"><span data-stu-id="684f6-205">i.</span></span> <span data-ttu-id="684f6-206">Azure AD 구성 마법사에서 다운로드한 인증서를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-206">Upload the certificate, which you have downloaded from Azure AD configuration wizard.</span></span> <span data-ttu-id="684f6-207">설정을 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-207">**Save** the settings.</span></span>
   
    <span data-ttu-id="684f6-208">j.</span><span class="sxs-lookup"><span data-stu-id="684f6-208">j.</span></span> <span data-ttu-id="684f6-209">리디렉션 페이지 설정을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-209">Edit the Redirect Pages settings.</span></span>
   
    <span data-ttu-id="684f6-210">k.</span><span class="sxs-lookup"><span data-stu-id="684f6-210">k.</span></span> <span data-ttu-id="684f6-211">**SAML Single Sign-On 서비스 URL**을 **로그인 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-211">Paste the **SAML Single Sign-On Service URL** in the **Login URL** textbox.</span></span>
   
    <span data-ttu-id="684f6-212">l.</span><span class="sxs-lookup"><span data-stu-id="684f6-212">l.</span></span> <span data-ttu-id="684f6-213">**로그아웃 URL**을 **로그아웃 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-213">Paste the **Sign-Out URL** in the **Logout URL** textbox.</span></span>
   
    <span data-ttu-id="684f6-214">m.</span><span class="sxs-lookup"><span data-stu-id="684f6-214">m.</span></span> <span data-ttu-id="684f6-215">**오류 URL**에서 **Marketo 인스턴스 URL**을 복사하고 **저장** 단추를 클릭하여 설정을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-215">In the **Error URL**, copy your **Marketo instance URL** and click **Save** button to save settings.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_10.png)

9. <span data-ttu-id="684f6-217">사용자에 대한 SSO를 사용하려면 다음 작업을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-217">To enable the SSO for users, complete the following actions:</span></span>
   
    <span data-ttu-id="684f6-218">a.</span><span class="sxs-lookup"><span data-stu-id="684f6-218">a.</span></span> <span data-ttu-id="684f6-219">관리자 자격 증명을 사용하여 Marketo 앱에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-219">Log in to Marketo app using admin credentials.</span></span>
   
    <span data-ttu-id="684f6-220">b.</span><span class="sxs-lookup"><span data-stu-id="684f6-220">b.</span></span> <span data-ttu-id="684f6-221">위쪽 탐색 창에서 **관리자** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-221">Click the **Admin** button on the top navigation pane.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    <span data-ttu-id="684f6-223">c.</span><span class="sxs-lookup"><span data-stu-id="684f6-223">c.</span></span> <span data-ttu-id="684f6-224">**보안** 메뉴로 이동하여 **로그인 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-224">Navigate to the **Security** menu and click **Login Settings**.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_13.png)
   
    <span data-ttu-id="684f6-226">d.</span><span class="sxs-lookup"><span data-stu-id="684f6-226">d.</span></span> <span data-ttu-id="684f6-227">**SSO 필요** 옵션을 선택하고 설정을 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-227">Check the **Require SSO** option and **Save** the settings.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_14.png)

> [!TIP]
> <span data-ttu-id="684f6-229">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-229">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="684f6-230">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-230">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="684f6-231">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-231">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="684f6-232">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="684f6-232">Creating an Azure AD test user</span></span>
<span data-ttu-id="684f6-233">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-233">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="684f6-235">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="684f6-235">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="684f6-236">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-236">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-marketo-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="684f6-238">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-238">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-marketo-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="684f6-240">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-240">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-marketo-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="684f6-242">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-242">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-marketo-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="684f6-244">a.</span><span class="sxs-lookup"><span data-stu-id="684f6-244">a.</span></span> <span data-ttu-id="684f6-245">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-245">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="684f6-246">b.</span><span class="sxs-lookup"><span data-stu-id="684f6-246">b.</span></span> <span data-ttu-id="684f6-247">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-247">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="684f6-248">c.</span><span class="sxs-lookup"><span data-stu-id="684f6-248">c.</span></span> <span data-ttu-id="684f6-249">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-249">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="684f6-250">d.</span><span class="sxs-lookup"><span data-stu-id="684f6-250">d.</span></span> <span data-ttu-id="684f6-251">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-251">Click **Create**.</span></span>
 
### <a name="creating-a-marketo-test-user"></a><span data-ttu-id="684f6-252">Marketo 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="684f6-252">Creating a Marketo test user</span></span>

<span data-ttu-id="684f6-253">이 섹션에서는 Marketo에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-253">In this section, you create a user called Britta Simon in Marketo.</span></span> <span data-ttu-id="684f6-254">다음 단계에 따라 Marketo 플랫폼에서 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-254">follow these steps to create a user in Marketo platform.</span></span>

1. <span data-ttu-id="684f6-255">관리자 자격 증명을 사용하여 Marketo 앱에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-255">Log in to Marketo app using admin credentials.</span></span>

2. <span data-ttu-id="684f6-256">위쪽 탐색 창에서 **관리자** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-256">Click the **Admin** button on the top navigation pane.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 

3. <span data-ttu-id="684f6-258">**보안** 메뉴로 이동하여 **사용자 및 역할**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-258">Navigate to the **Security** menu and click **Users & Roles**</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_19.png)  

4. <span data-ttu-id="684f6-260">사용자 탭에서 **새 사용자 초대** 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-260">Click the **Invite New User** link on the Users tab</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_15.png) 

5. <span data-ttu-id="684f6-262">새 사용자 초대 마법사에서 다음 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-262">In the Invite New User wizard fill the following information</span></span>
   
    <span data-ttu-id="684f6-263">a.</span><span class="sxs-lookup"><span data-stu-id="684f6-263">a.</span></span> <span data-ttu-id="684f6-264">텍스트 상자에 사용자 **메일** 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-264">Enter the user **Email** address in the textbox</span></span>
   
    ![Single Sign-On 구성](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_16.png)
   
    <span data-ttu-id="684f6-266">b.</span><span class="sxs-lookup"><span data-stu-id="684f6-266">b.</span></span> <span data-ttu-id="684f6-267">텍스트 상자에 **이름** 을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-267">Enter the **First Name** in the textbox</span></span>
   
    <span data-ttu-id="684f6-268">c.</span><span class="sxs-lookup"><span data-stu-id="684f6-268">c.</span></span> <span data-ttu-id="684f6-269">텍스트 상자에 **성**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-269">Enter the **Last Name**  in the textbox</span></span>
   
    <span data-ttu-id="684f6-270">d.</span><span class="sxs-lookup"><span data-stu-id="684f6-270">d.</span></span> <span data-ttu-id="684f6-271">**다음**을 누릅니다</span><span class="sxs-lookup"><span data-stu-id="684f6-271">Click **Next**</span></span>

6. <span data-ttu-id="684f6-272">**권한** 탭에서 **사용자 역할**을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-272">In the **Permissions** tab, select the **userRoles** and click **Next**</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_17.png)
7. <span data-ttu-id="684f6-274">**보내기** 단추를 클릭하여 사용자 초대를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-274">Click the **Send** button to send the user invitation</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_18.png)

8. <span data-ttu-id="684f6-276">사용자는 이메일 알림을 받으면 링크를 클릭하고 암호를 변경하여 계정을 활성화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-276">User receives the email notification and has to click the link and change the password to activate the account.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="684f6-277">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="684f6-277">Assigning the Azure AD test user</span></span>

<span data-ttu-id="684f6-278">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Marketo에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-278">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Marketo.</span></span>

![사용자 할당][200] 

<span data-ttu-id="684f6-280">**Britta Simon을 Marketo에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="684f6-280">**To assign Britta Simon to Marketo, perform the following steps:**</span></span>

1. <span data-ttu-id="684f6-281">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-281">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="684f6-283">응용 프로그램 목록에서 **Marketo**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-283">In the applications list, select **Marketo**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_app.png) 

3. <span data-ttu-id="684f6-285">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-285">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="684f6-287">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-287">Click **Add** button.</span></span> <span data-ttu-id="684f6-288">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-288">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="684f6-290">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-290">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="684f6-291">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-291">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="684f6-292">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-292">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="684f6-293">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="684f6-293">Testing single sign-on</span></span>

<span data-ttu-id="684f6-294">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-294">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="684f6-295">액세스 패널에서 Marketo 타일을 클릭하면 Marketo 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="684f6-295">When you click the Marketo tile in the Access Panel, you should get automatically signed-on to your Marketo application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="684f6-296">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="684f6-296">Additional resources</span></span>

* [<span data-ttu-id="684f6-297">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="684f6-297">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="684f6-298">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="684f6-298">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_203.png

