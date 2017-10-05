---
title: "자습서: Mimecast Personal Portal과 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 Mimecast Personal Portal 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 345b22be-d87e-45a4-b4c0-70a67eaf9bfd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: bf46da35a55608d7e4656c9dd3ad9d5f2253e225
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mimecast-personal-portal"></a><span data-ttu-id="22394-103">자습서: Mimecast Personal Portal과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="22394-103">Tutorial: Azure Active Directory integration with Mimecast Personal Portal</span></span>

<span data-ttu-id="22394-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Mimecast Personal Portal을 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="22394-104">In this tutorial, you learn how to integrate Mimecast Personal Portal with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="22394-105">Mimecast Personal Portal을 Azure AD와 통합하면 다음과 같은 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22394-105">Integrating Mimecast Personal Portal with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="22394-106">Mimecast Personal Portal에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22394-106">You can control in Azure AD who has access to Mimecast Personal Portal</span></span>
- <span data-ttu-id="22394-107">사용자가 자신의 Azure AD 계정으로 Mimecast Personal Portal에 자동으로 로그온(Single Sign-On) 되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22394-107">You can enable your users to automatically get signed-on to Mimecast Personal Portal (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="22394-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22394-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="22394-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="22394-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="22394-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="22394-110">Prerequisites</span></span>

<span data-ttu-id="22394-111">Mimecast Personal Portal과 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="22394-111">To configure Azure AD integration with Mimecast Personal Portal, you need the following items:</span></span>

- <span data-ttu-id="22394-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="22394-112">An Azure AD subscription</span></span>
- <span data-ttu-id="22394-113">Mimecast Personal Portal에서 Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="22394-113">A Mimecast Personal Portal single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="22394-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="22394-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="22394-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22394-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="22394-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="22394-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="22394-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22394-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="22394-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="22394-118">Scenario description</span></span>
<span data-ttu-id="22394-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="22394-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="22394-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22394-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="22394-121">갤러리에서 Mimecast Personal Portal 추가</span><span class="sxs-lookup"><span data-stu-id="22394-121">Adding Mimecast Personal Portal from the gallery</span></span>
2. <span data-ttu-id="22394-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="22394-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mimecast-personal-portal-from-the-gallery"></a><span data-ttu-id="22394-123">갤러리에서 Mimecast Personal Portal 추가</span><span class="sxs-lookup"><span data-stu-id="22394-123">Adding Mimecast Personal Portal from the gallery</span></span>
<span data-ttu-id="22394-124">Mimecast Personal Portal이 Azure AD에 통합되도록 구성하려면 갤러리에서 Mimecast Personal Portal을 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22394-124">To configure the integration of Mimecast Personal Portal into Azure AD, you need to add Mimecast Personal Portal from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="22394-125">**갤러리에서 Mimecast Personal Portal을 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="22394-125">**To add Mimecast Personal Portal from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="22394-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="22394-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="22394-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="22394-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="22394-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="22394-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="22394-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="22394-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="22394-133">검색 상자에 **Mimecast Personal Portal**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="22394-133">In the search box, type **Mimecast Personal Portal**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_search.png)

5. <span data-ttu-id="22394-135">결과 창에서 **Mimecast Personal Portal**을 선택하고 **추가**를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="22394-135">In the results panel, select **Mimecast Personal Portal**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="22394-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="22394-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="22394-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Mimecast Personal Portal에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="22394-138">In this section, you configure and test Azure AD single sign-on with Mimecast Personal Portal based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="22394-139">Single Sign-On이 작동하려면 Azure AD 사용자에 해당하는 Mimecast Personal Portal 사용자가 누구인지 Azure AD에서 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22394-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Mimecast Personal Portal is to a user in Azure AD.</span></span> <span data-ttu-id="22394-140">즉, Azure AD 사용자와 Mimecast Personal Portal의 관련 사용자 간에 링크 관계가 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22394-140">In other words, a link relationship between an Azure AD user and the related user in Mimecast Personal Portal needs to be established.</span></span>

<span data-ttu-id="22394-141">Mimecast Personal Portal에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="22394-141">In Mimecast Personal Portal, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="22394-142">Mimecast Personal Portal에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22394-142">To configure and test Azure AD single sign-on with Mimecast Personal Portal, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="22394-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="22394-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="22394-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="22394-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="22394-145">**[Mimecast Personal Portal 테스트 사용자 만들기](#creating-a-mimecast-personal-portal-test-user)** - Britta Simon의 Azure AD 표현과 연결되는 대응 사용자를 Mimecast Personal Portal에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="22394-145">**[Creating a Mimecast Personal Portal test user](#creating-a-mimecast-personal-portal-test-user)** - to have a counterpart of Britta Simon in Mimecast Personal Portal that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="22394-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="22394-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="22394-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="22394-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="22394-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="22394-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="22394-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Mimecast Personal Portal 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="22394-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Mimecast Personal Portal application.</span></span>

<span data-ttu-id="22394-150">**Mimecast Personal Portal에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="22394-150">**To configure Azure AD single sign-on with Mimecast Personal Portal, perform the following steps:**</span></span>

1. <span data-ttu-id="22394-151">Azure Portal의 **Mimecast Personal Portal** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="22394-151">In the Azure portal, on the **Mimecast Personal Portal** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="22394-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="22394-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_samlbase.png)

3. <span data-ttu-id="22394-155">**Mimecast Personal Portal 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="22394-155">On the **Mimecast Personal Portal Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_url.png)

    <span data-ttu-id="22394-157">a.</span><span class="sxs-lookup"><span data-stu-id="22394-157">a.</span></span> <span data-ttu-id="22394-158">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="22394-158">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span> 
    | |     
    | ----------------------------------------|
    | `https://webmail-uk.mimecast.com`|
    | `https://webmail-us.mimecast.com`|
    | |
   
    <span data-ttu-id="22394-159">b.</span><span class="sxs-lookup"><span data-stu-id="22394-159">b.</span></span> <span data-ttu-id="22394-160">**식별자** 텍스트 상자에서 다음 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="22394-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span>

    | |     
    | --- |
    | `https://webmail-us.mimecast.com/sso/<companyname>`|
    | `https://webmail-uk.mimecast.com/sso/<companyname>`|    
    | `https://webmail-za.mimecast.com/sso/<companyname>`|
    | `https://webmail.mimecast-offshore.com/sso/<companyname>`|
    ||                                                 
    
    > [!NOTE] 
    > <span data-ttu-id="22394-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="22394-161">These values are not real.</span></span> <span data-ttu-id="22394-162">실제 로그온 URL 및 식별자로 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="22394-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="22394-163">이러한 값을 얻으려면 [Mimecast Personal Portal 클라이언트 지원 팀](https://www.mimecast.com/customer-success/technical-support/)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="22394-163">Contact [Mimecast Personal Portal Client support team](https://www.mimecast.com/customer-success/technical-support/) to get these values.</span></span> 
 


4. <span data-ttu-id="22394-164">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="22394-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_certificate.png) 

5. <span data-ttu-id="22394-166">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="22394-166">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="22394-168">**Mimecast Personal Portal 구성** 섹션에서 **Mimecast Personal Portal 구성**을 클릭하고 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="22394-168">On the **Mimecast Personal Portal Configuration** section, click **Configure Mimecast Personal Portal** to open **Configure sign-on** window.</span></span> <span data-ttu-id="22394-169">**빠른 참조 섹션**에서 **로그아웃 URL, SAML 엔터티 ID 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="22394-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_configure.png) 

7. <span data-ttu-id="22394-171">다른 웹 브라우저 창에서 Mimecast Personal Portal 포털에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="22394-171">In a different web browser window, log into your Mimecast Personal Portal as an administrator.</span></span>

8. <span data-ttu-id="22394-172">**서비스 \> 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="22394-172">Go to **Services \> Applications**.</span></span>
   
    <span data-ttu-id="22394-173">![응용 프로그램](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794998.png "응용 프로그램")</span><span class="sxs-lookup"><span data-stu-id="22394-173">![Applications](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794998.png "Applications")</span></span>

9. <span data-ttu-id="22394-174">**인증 프로필**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="22394-174">Click **Authentication Profiles**.</span></span>
   
    <span data-ttu-id="22394-175">![인증 프로필](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794999.png "인증 프로필")</span><span class="sxs-lookup"><span data-stu-id="22394-175">![Authentication Profiles](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794999.png "Authentication Profiles")</span></span>

10. <span data-ttu-id="22394-176">**새 인증 프로필**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="22394-176">Click **New Authentication Profile**.</span></span>
   
    <span data-ttu-id="22394-177">![새 인증 프로필](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795000.png "새 인증 프로필")</span><span class="sxs-lookup"><span data-stu-id="22394-177">![New Authentication Profile](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795000.png "New Authentication Profile")</span></span>

11. <span data-ttu-id="22394-178">**인증 프로필** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="22394-178">In the **Authentication Profile** section, perform the following steps:</span></span>
   
    <span data-ttu-id="22394-179">![인증 프로필](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795001.png "인증 프로필")</span><span class="sxs-lookup"><span data-stu-id="22394-179">![Authentication Profile](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795001.png "Authentication Profile")</span></span>
   
    <span data-ttu-id="22394-180">a.</span><span class="sxs-lookup"><span data-stu-id="22394-180">a.</span></span> <span data-ttu-id="22394-181">**설명** 텍스트 상자에 구성 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="22394-181">In the **Description** textbox, type a name for your configuration.</span></span>
   
    <span data-ttu-id="22394-182">b.</span><span class="sxs-lookup"><span data-stu-id="22394-182">b.</span></span> <span data-ttu-id="22394-183">**Mimecast Personal Portal에 대한 SAML 인증 적용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="22394-183">Select **Enforce SAML Authentication for Mimecast Personal Portal**.</span></span>
   
    <span data-ttu-id="22394-184">c.</span><span class="sxs-lookup"><span data-stu-id="22394-184">c.</span></span> <span data-ttu-id="22394-185">**공급자**로 **Azure Active Directory**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="22394-185">As **Provider**, select **Azure Active Directory**.</span></span>
   
    <span data-ttu-id="22394-186">d.</span><span class="sxs-lookup"><span data-stu-id="22394-186">d.</span></span> <span data-ttu-id="22394-187">**발급자 URL** 텍스트 상자에 Azure Portal에서 복사한 **SAML 엔터티 ID** 값을 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="22394-187">In **Issuer URL** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="22394-188">e.</span><span class="sxs-lookup"><span data-stu-id="22394-188">e.</span></span> <span data-ttu-id="22394-189">Azure Portal에서 복사한 **SAML Single Sign-On 서비스 URL** 값을 **로그인 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="22394-189">In **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="22394-190">f.</span><span class="sxs-lookup"><span data-stu-id="22394-190">f.</span></span> <span data-ttu-id="22394-191">Azure Portal에서 복사한 **로그아웃 URL** 값을 **로그아웃 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="22394-191">In **Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="22394-192">g.</span><span class="sxs-lookup"><span data-stu-id="22394-192">g.</span></span> <span data-ttu-id="22394-193">Azure Portal에서 다운로드한 **base-64**로 인코딩된 인증서를 메모장에서 열고 콘텐츠를 클립보드에 복사한 다음 **Identity Provider Certificate (Metadata)**(ID 공급자 인증서)(Metadata) 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="22394-193">Open your **base-64** encoded certificate in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **Identity Provider Certificate (Metadata)** textbox.</span></span>

    <span data-ttu-id="22394-194">h.</span><span class="sxs-lookup"><span data-stu-id="22394-194">h.</span></span> <span data-ttu-id="22394-195">**Single Sign-On 허용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="22394-195">Select **Allow Single Sign On**.</span></span>
   
    <span data-ttu-id="22394-196">i.</span><span class="sxs-lookup"><span data-stu-id="22394-196">i.</span></span> <span data-ttu-id="22394-197">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="22394-197">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="22394-198">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22394-198">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="22394-199">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="22394-199">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="22394-200">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22394-200">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="22394-201">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="22394-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="22394-202">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="22394-202">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="22394-204">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="22394-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="22394-205">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="22394-205">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="22394-207">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="22394-207">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="22394-209">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="22394-209">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="22394-211">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="22394-211">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="22394-213">a.</span><span class="sxs-lookup"><span data-stu-id="22394-213">a.</span></span> <span data-ttu-id="22394-214">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="22394-214">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="22394-215">b.</span><span class="sxs-lookup"><span data-stu-id="22394-215">b.</span></span> <span data-ttu-id="22394-216">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="22394-216">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="22394-217">c.</span><span class="sxs-lookup"><span data-stu-id="22394-217">c.</span></span> <span data-ttu-id="22394-218">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="22394-218">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="22394-219">d.</span><span class="sxs-lookup"><span data-stu-id="22394-219">d.</span></span> <span data-ttu-id="22394-220">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="22394-220">Click **Create**.</span></span>
 
### <a name="creating-a-mimecast-personal-portal-test-user"></a><span data-ttu-id="22394-221">Mimecast Personal Portal 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="22394-221">Creating a Mimecast Personal Portal test user</span></span>

<span data-ttu-id="22394-222">Azure AD 사용자가 Mimecast Personal Portal에 로그인하게 하려면 Mimecast Personal Portal에 프로비전해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22394-222">In order to enable Azure AD users to log into Mimecast Personal Portal, they must be provisioned into Mimecast Personal Portal.</span></span> <span data-ttu-id="22394-223">Mimecast Personal Portal의 경우 프로비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="22394-223">In the case of Mimecast Personal Portal, provisioning is a manual task.</span></span>

<span data-ttu-id="22394-224">사용자를 만들려면 먼저 도메인을 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22394-224">You need to register a domain before you can create users.</span></span>

<span data-ttu-id="22394-225">**사용자 프로비전을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="22394-225">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="22394-226">**Mimecast Personal Portal** 에 관리자 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="22394-226">Sign on to your **Mimecast Personal Portal** as administrator.</span></span>

2. <span data-ttu-id="22394-227">**디렉터리 \> 내부**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="22394-227">Go to **Directories \> Internal**.</span></span>
   
    <span data-ttu-id="22394-228">![디렉터리](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795003.png "디렉터리")</span><span class="sxs-lookup"><span data-stu-id="22394-228">![Directories](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795003.png "Directories")</span></span>

3. <span data-ttu-id="22394-229">**새 도메인에 등록**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="22394-229">Click **Register New Domain**.</span></span>
   
    <span data-ttu-id="22394-230">![새 도메인에 등록](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795004.png "새 도메인에 등록")</span><span class="sxs-lookup"><span data-stu-id="22394-230">![Register New Domain](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795004.png "Register New Domain")</span></span>

4. <span data-ttu-id="22394-231">새 도메인을 만든 후 **새 주소**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="22394-231">After your new domain has been created, click **New Address**.</span></span>
   
    <span data-ttu-id="22394-232">![새 주소](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795005.png "새 주소")</span><span class="sxs-lookup"><span data-stu-id="22394-232">![New Address](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795005.png "New Address")</span></span>

5. <span data-ttu-id="22394-233">새 주소 대화 상자에서 프로비전할 유효한 Azure AD 계정에 대한 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="22394-233">In the new address dialog, perform the following steps of a valid Azure AD account you want to provision:</span></span>
   
    <span data-ttu-id="22394-234">![저장](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795006.png "저장")</span><span class="sxs-lookup"><span data-stu-id="22394-234">![Save](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795006.png "Save")</span></span>
   
    <span data-ttu-id="22394-235">a.</span><span class="sxs-lookup"><span data-stu-id="22394-235">a.</span></span> <span data-ttu-id="22394-236">**이메일 주소** 텍스트 상자에 사용자의 **이메일 주소**를 **BrittaSimon@contoso.com**으로 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="22394-236">In the **Email Address** textbox, type **Email Address** of the user as **BrittaSimon@contoso.com**.</span></span>
    
    <span data-ttu-id="22394-237">b.</span><span class="sxs-lookup"><span data-stu-id="22394-237">b.</span></span> <span data-ttu-id="22394-238">**Global Name**(전역 이름) 텍스트 상자에 **사용자 이름**을 **BrittaSimon**으로 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="22394-238">In the **Global Name** textbox, type the **username** as **BrittaSimon**.</span></span>

    <span data-ttu-id="22394-239">c.</span><span class="sxs-lookup"><span data-stu-id="22394-239">c.</span></span> <span data-ttu-id="22394-240">**암호** 및 **암호 확인** 텍스트 상자에 사용자의 **암호**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="22394-240">In the **Password**, and **Confirm Password** textboxes, type the **Password** of the user.</span></span>
   
    <span data-ttu-id="22394-241">b.</span><span class="sxs-lookup"><span data-stu-id="22394-241">b.</span></span> <span data-ttu-id="22394-242">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="22394-242">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="22394-243">Mimecast Personal Portal 사용자 계정 생성 도구 또는 Mimecast Personal Portal에서 제공한 API를 사용하여 Azure AD 사용자 계정을 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="22394-243">You can use any other Mimecast Personal Portal user account creation tools or APIs provided by Mimecast Personal Portal to provision Azure AD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="22394-244">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="22394-244">Assigning the Azure AD test user</span></span>

<span data-ttu-id="22394-245">이 섹션에서는 Britta Simon이 Azure Single Sign-On을 사용할 수 있도록 Mimecast Personal Portal에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="22394-245">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Mimecast Personal Portal.</span></span>

![사용자 할당][200] 

<span data-ttu-id="22394-247">**Mimecast Personal Portal에 Britta Simon을 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="22394-247">**To assign Britta Simon to Mimecast Personal Portal, perform the following steps:**</span></span>

1. <span data-ttu-id="22394-248">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="22394-248">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="22394-250">응용 프로그램 목록에서 **Mimecast Personal Portal**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="22394-250">In the applications list, select **Mimecast Personal Portal**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_app.png) 

3. <span data-ttu-id="22394-252">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="22394-252">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="22394-254">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="22394-254">Click **Add** button.</span></span> <span data-ttu-id="22394-255">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="22394-255">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="22394-257">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="22394-257">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="22394-258">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="22394-258">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="22394-259">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="22394-259">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="22394-260">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="22394-260">Testing single sign-on</span></span>
<span data-ttu-id="22394-261">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="22394-261">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="22394-262">액세스 패널에서 Mimecast Personal Portal 타일을 클릭하면 Mimecast Personal Portal 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="22394-262">When you click the Mimecast Personal Portal tile in the Access Panel, you should get automatically signed-on to your Mimecast Personal Portal application.</span></span> <span data-ttu-id="22394-263">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="22394-263">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="22394-264">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="22394-264">Additional resources</span></span>

* [<span data-ttu-id="22394-265">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="22394-265">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="22394-266">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="22394-266">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_203.png

