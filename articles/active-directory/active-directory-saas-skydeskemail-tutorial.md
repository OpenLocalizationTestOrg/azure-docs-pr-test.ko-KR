---
title: "자습서: SkyDesk Email과 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory 및 SkyDesk Email 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a9d0bbcb-ddb5-473f-a4aa-028ae88ced1a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: 0ffcca4161fc836192fc9c9871a905f36ea76b32
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-skydesk-email"></a><span data-ttu-id="41a8c-103">자습서: SkyDesk Email과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="41a8c-103">Tutorial: Azure Active Directory integration with SkyDesk Email</span></span>

<span data-ttu-id="41a8c-104">이 자습서에서는 Azure AD(Azure Active Directory)와 SkyDesk Email을 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-104">In this tutorial, you learn how to integrate SkyDesk Email with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="41a8c-105">SkyDesk Email을 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-105">Integrating SkyDesk Email with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="41a8c-106">SkyDesk Email에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-106">You can control in Azure AD who has access to SkyDesk Email</span></span>
- <span data-ttu-id="41a8c-107">사용자가 자신의 Azure AD 계정으로 SkyDesk Email에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-107">You can enable your users to automatically get signed-on to SkyDesk Email (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="41a8c-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="41a8c-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="41a8c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="41a8c-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="41a8c-110">Prerequisites</span></span>

<span data-ttu-id="41a8c-111">SkyDesk Email와의 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-111">To configure Azure AD integration with SkyDesk Email, you need the following items:</span></span>

- <span data-ttu-id="41a8c-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="41a8c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="41a8c-113">SkyDesk Email Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="41a8c-113">A SkyDesk Email single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="41a8c-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="41a8c-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="41a8c-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="41a8c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="41a8c-117">Azure AD 평가판 환경이 없으면 [평가판 제품](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-117">If you don't have an Azure AD trial environment, you can get a one-month trial here [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="41a8c-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="41a8c-118">Scenario description</span></span>
<span data-ttu-id="41a8c-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="41a8c-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="41a8c-121">갤러리에서 SkyDesk Email 추가</span><span class="sxs-lookup"><span data-stu-id="41a8c-121">Adding SkyDesk Email from the gallery</span></span>
2. <span data-ttu-id="41a8c-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="41a8c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-skydesk-email-from-the-gallery"></a><span data-ttu-id="41a8c-123">갤러리에서 SkyDesk Email 추가</span><span class="sxs-lookup"><span data-stu-id="41a8c-123">Adding SkyDesk Email from the gallery</span></span>
<span data-ttu-id="41a8c-124">SkyDesk Email의 Azure AD 통합을 구성하려면 갤러리의 SkyDesk Email을 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-124">To configure the integration of SkyDesk Email into Azure AD, you need to add SkyDesk Email from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="41a8c-125">**갤러리에서 SkyDesk Email을 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="41a8c-125">**To add SkyDesk Email from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="41a8c-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="41a8c-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="41a8c-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="41a8c-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="41a8c-133">검색 상자에 **SkyDesk Email**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-133">In the search box, type **SkyDesk Email**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_search.png)

5. <span data-ttu-id="41a8c-135">결과 창에서 **SkyDesk Email**을 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-135">In the results panel, select **SkyDesk Email**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="41a8c-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="41a8c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="41a8c-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 SkyDesk Email에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-138">In this section, you configure and test Azure AD single sign-on with SkyDesk Email based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="41a8c-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 SkyDesk Email 사용자가 누군지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SkyDesk Email is to a user in Azure AD.</span></span> <span data-ttu-id="41a8c-140">즉, Azure AD 사용자와 SkyDesk Email의 관련 사용자 간에 연결 관계가 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-140">In other words, a link relationship between an Azure AD user and the related user in SkyDesk Email needs to be established.</span></span>

<span data-ttu-id="41a8c-141">SkyDesk Email에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-141">In SkyDesk Email, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="41a8c-142">SkyDesk Email에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-142">To configure and test Azure AD single sign-on with SkyDesk Email, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="41a8c-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="41a8c-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="41a8c-145">**[SkyDesk Email 테스트 사용자 만들기](#creating-a-skydesk-email-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 SkyDesk Email에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-145">**[Creating a SkyDesk Email test user](#creating-a-skydesk-email-test-user)** - to have a counterpart of Britta Simon in SkyDesk Email that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="41a8c-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="41a8c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="41a8c-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="41a8c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="41a8c-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 SkyDesk Email 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SkyDesk Email application.</span></span>

<span data-ttu-id="41a8c-150">**SkyDesk Email에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="41a8c-150">**To configure Azure AD single sign-on with SkyDesk Email, perform the following steps:**</span></span>

1. <span data-ttu-id="41a8c-151">Azure Portal의 **SkyDesk Email** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-151">In the Azure portal, on the **SkyDesk Email** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="41a8c-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_samlbase.png)

3. <span data-ttu-id="41a8c-155">**SkyDesk Email 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-155">On the **SkyDesk Email Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_url.png)

    <span data-ttu-id="41a8c-157">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://mail.skydesk.jp/portal/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="41a8c-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://mail.skydesk.jp/portal/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="41a8c-158">이 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-158">The value is not real.</span></span> <span data-ttu-id="41a8c-159">이 값을 실제 로그온 URL로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="41a8c-160">값을 얻으려면 [SkyDesk Email 클라이언트 지원 팀](https://www.skydesk.sg/support/)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="41a8c-160">Contact [SkyDesk Email Client support team](https://www.skydesk.sg/support/) to get the value.</span></span> 
 
4. <span data-ttu-id="41a8c-161">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_certificate.png) 

5. <span data-ttu-id="41a8c-163">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-163">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="41a8c-165">**SkyDesk Email 구성** 섹션에서 **SkyDesk Email 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-165">On the **SkyDesk Email Configuration** section, click **Configure SkyDesk Email** to open **Configure sign-on** window.</span></span> <span data-ttu-id="41a8c-166">**빠른 참조 섹션**에서 **로그아웃 URL 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-166">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_configure.png) 

7. <span data-ttu-id="41a8c-168">**SkyDesk Email**에서 SSO를 사용하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-168">To enable SSO in **SkyDesk Email**, perform the following steps:</span></span>

    <span data-ttu-id="41a8c-169">a.</span><span class="sxs-lookup"><span data-stu-id="41a8c-169">a.</span></span> <span data-ttu-id="41a8c-170">SkyDesk Email 계정에 관리자 권한으로 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-170">Sign-on to your SkyDesk Email account as administrator.</span></span>

    <span data-ttu-id="41a8c-171">b.</span><span class="sxs-lookup"><span data-stu-id="41a8c-171">b.</span></span> <span data-ttu-id="41a8c-172">위쪽 메뉴에서 **설정**을 클릭한 다음 **조직**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-172">In the menu on the top, click **Setup**, and select **Org**.</span></span> 
    
      ![Single Sign-on 구성](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_51.png)
  
    <span data-ttu-id="41a8c-174">c.</span><span class="sxs-lookup"><span data-stu-id="41a8c-174">c.</span></span> <span data-ttu-id="41a8c-175">왼쪽 패널에서 **도메인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-175">Click on **Domains** from the left panel.</span></span>
    
      ![Single Sign-on 구성](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_53.png)

    <span data-ttu-id="41a8c-177">d.</span><span class="sxs-lookup"><span data-stu-id="41a8c-177">d.</span></span> <span data-ttu-id="41a8c-178">**도메인 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-178">Click on **Add Domain**.</span></span>
    
      ![Single Sign-on 구성](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_54.png)

    <span data-ttu-id="41a8c-180">e.</span><span class="sxs-lookup"><span data-stu-id="41a8c-180">e.</span></span> <span data-ttu-id="41a8c-181">도메인 이름을 입력하고 도메인을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-181">Enter your Domain name, and then verify the Domain.</span></span>
    
      ![Single Sign-on 구성](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_55.png)

    <span data-ttu-id="41a8c-183">f.</span><span class="sxs-lookup"><span data-stu-id="41a8c-183">f.</span></span> <span data-ttu-id="41a8c-184">왼쪽 패널에서 **SAML 인증** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-184">Click on **SAML Authentication** from the left panel.</span></span>
    
      ![Single Sign-On 구성](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_52.png)

8. <span data-ttu-id="41a8c-186">**SAML 인증** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-186">On the **SAML Authentication** dialog page, perform the following steps:</span></span>
   
      ![Single Sign-On 구성](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_56.png)
   
    >[!NOTE]
    ><span data-ttu-id="41a8c-188">SAML 기반 인증을 사용하려면 **확인된 도메인** 또는 **포털 URL** 설정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-188">To use SAML based authentication, you should either have **verified domain** or **portal URL** setup.</span></span> <span data-ttu-id="41a8c-189">고유의 이름으로 포털 URL을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-189">You can set the portal URL with the unique name.</span></span>
    > 
    > 
   
    ![Single Sign-on 구성](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_57.png)

    <span data-ttu-id="41a8c-191">a.</span><span class="sxs-lookup"><span data-stu-id="41a8c-191">a.</span></span> <span data-ttu-id="41a8c-192">Azure Portal에서 복사한 **SAML Single Sign-On 서비스 URL** 값을 **로그인 URL** 텍스트 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-192">In the **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="41a8c-193">b.</span><span class="sxs-lookup"><span data-stu-id="41a8c-193">b.</span></span> <span data-ttu-id="41a8c-194">Azure Portal에서 복사한 **로그아웃 URL** 값을 **로그아웃 URL** 텍스트 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-194">In the **Logout** URL textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="41a8c-195">c.</span><span class="sxs-lookup"><span data-stu-id="41a8c-195">c.</span></span> <span data-ttu-id="41a8c-196">**암호 변경 URL** 은 선택 사항이므로 비워 둡니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-196">**Change Password URL** is optional so leave it blank.</span></span>

    <span data-ttu-id="41a8c-197">d.</span><span class="sxs-lookup"><span data-stu-id="41a8c-197">d.</span></span> <span data-ttu-id="41a8c-198">**파일에서 키 가져오기**를 클릭하여 Azure Portal에서 다운로드한 인증서를 선택하고 **열기**를 클릭하여 인증서를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-198">Click on **Get Key From File** to select your downloaded certificate from Azure portal, and then click **Open** to upload the certificate.</span></span>

    <span data-ttu-id="41a8c-199">e.</span><span class="sxs-lookup"><span data-stu-id="41a8c-199">e.</span></span> <span data-ttu-id="41a8c-200">**알고리즘**으로 **RSA**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-200">As **Algorithm**, select **RSA**.</span></span>

    <span data-ttu-id="41a8c-201">f.</span><span class="sxs-lookup"><span data-stu-id="41a8c-201">f.</span></span> <span data-ttu-id="41a8c-202">**확인** 을 클릭하여 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-202">Click **Ok** to save the changes.</span></span>

> [!TIP]
> <span data-ttu-id="41a8c-203">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-203">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="41a8c-204">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-204">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="41a8c-205">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-205">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="41a8c-206">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="41a8c-206">Creating an Azure AD test user</span></span>
<span data-ttu-id="41a8c-207">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-207">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="41a8c-209">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="41a8c-209">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="41a8c-210">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-210">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="41a8c-212">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-212">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="41a8c-214">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-214">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="41a8c-216">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-216">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="41a8c-218">a.</span><span class="sxs-lookup"><span data-stu-id="41a8c-218">a.</span></span> <span data-ttu-id="41a8c-219">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-219">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="41a8c-220">b.</span><span class="sxs-lookup"><span data-stu-id="41a8c-220">b.</span></span> <span data-ttu-id="41a8c-221">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-221">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="41a8c-222">c.</span><span class="sxs-lookup"><span data-stu-id="41a8c-222">c.</span></span> <span data-ttu-id="41a8c-223">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-223">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="41a8c-224">d.</span><span class="sxs-lookup"><span data-stu-id="41a8c-224">d.</span></span> <span data-ttu-id="41a8c-225">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-225">Click **Create**.</span></span>
 
### <a name="creating-a-skydesk-email-test-user"></a><span data-ttu-id="41a8c-226">SkyDesk Email 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="41a8c-226">Creating a SkyDesk Email test user</span></span>

<span data-ttu-id="41a8c-227">이 섹션에서는 SkyDesk Email에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-227">In this section, you create a user called Britta Simon in SkyDesk Email.</span></span>

1. <span data-ttu-id="41a8c-228">SkyDesk Email의 왼쪽 패널에서 **사용자 액세스**를 클릭하고 사용자 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-228">Click on **User Access** from the left panel in SkyDesk Email and then enter your username.</span></span> 

    ![Single Sign-on 구성](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_58.png)

>[!NOTE] 
><span data-ttu-id="41a8c-230">일괄 사용자를 만들어야 하는 경우에는 [SkyDesk Email 클라이언트 지원 팀](https://www.skydesk.sg/support/)에 문의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-230">If you need to create bulk users, you need to contact the [SkyDesk Email Client support team](https://www.skydesk.sg/support/).</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="41a8c-231">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="41a8c-231">Assigning the Azure AD test user</span></span>

<span data-ttu-id="41a8c-232">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 SkyDesk Email에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-232">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SkyDesk Email.</span></span>

![사용자 할당][200] 

<span data-ttu-id="41a8c-234">**Britta Simon을 SkyDesk Email에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="41a8c-234">**To assign Britta Simon to SkyDesk Email, perform the following steps:**</span></span>

1. <span data-ttu-id="41a8c-235">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-235">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="41a8c-237">응용 프로그램 목록에서 **SkyDesk Email**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-237">In the applications list, select **SkyDesk Email**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_app.png) 

3. <span data-ttu-id="41a8c-239">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-239">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="41a8c-241">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-241">Click **Add** button.</span></span> <span data-ttu-id="41a8c-242">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="41a8c-244">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="41a8c-245">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="41a8c-246">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="41a8c-247">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="41a8c-247">Testing single sign-on</span></span>

<span data-ttu-id="41a8c-248">이 섹션은 액세스 패널을 사용하여 Azure AD SSO 구성을 테스트하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-248">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="41a8c-249">액세스 패널에서 SkyDesk Email 타일을 클릭하면 SkyDesk Email 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="41a8c-249">When you click the SkyDesk Email tile in the Access Panel, you should get automatically signed-on to your SkyDesk Email application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="41a8c-250">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="41a8c-250">Additional resources</span></span>

* [<span data-ttu-id="41a8c-251">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="41a8c-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="41a8c-252">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="41a8c-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_203.png

