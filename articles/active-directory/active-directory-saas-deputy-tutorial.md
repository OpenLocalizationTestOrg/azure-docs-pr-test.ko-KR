---
title: "자습서: Deputy와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 Deputy 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5665c3ac-5689-4201-80fe-fcc677d4430d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 51aed908208b7a40ea2ab710dffe84370b573991
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-deputy"></a><span data-ttu-id="db942-103">자습서: Deputy와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="db942-103">Tutorial: Azure Active Directory integration with Deputy</span></span>

<span data-ttu-id="db942-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Deputy를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="db942-104">In this tutorial, you learn how to integrate Deputy with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="db942-105">Deputy를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="db942-105">Integrating Deputy with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="db942-106">Deputy에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db942-106">You can control in Azure AD who has access to Deputy</span></span>
- <span data-ttu-id="db942-107">사용자가 해당 Azure AD 계정으로 Deputy에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db942-107">You can enable your users to automatically get signed-on to Deputy (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="db942-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db942-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="db942-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="db942-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="db942-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="db942-110">Prerequisites</span></span>

<span data-ttu-id="db942-111">Deputy와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="db942-111">To configure Azure AD integration with Deputy, you need the following items:</span></span>

- <span data-ttu-id="db942-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="db942-112">An Azure AD subscription</span></span>
- <span data-ttu-id="db942-113">Deputy Single Sign-on이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="db942-113">A Deputy single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="db942-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="db942-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="db942-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db942-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="db942-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="db942-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="db942-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db942-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="db942-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="db942-118">Scenario description</span></span>
<span data-ttu-id="db942-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="db942-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="db942-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db942-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="db942-121">갤러리에서 Deputy 추가</span><span class="sxs-lookup"><span data-stu-id="db942-121">Adding Deputy from the gallery</span></span>
2. <span data-ttu-id="db942-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="db942-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-deputy-from-the-gallery"></a><span data-ttu-id="db942-123">갤러리에서 Deputy 추가</span><span class="sxs-lookup"><span data-stu-id="db942-123">Adding Deputy from the gallery</span></span>
<span data-ttu-id="db942-124">Deputy의 Azure AD 통합을 구성하려면 갤러리의 Deputy를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db942-124">To configure the integration of Deputy into Azure AD, you need to add Deputy from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="db942-125">**갤러리에서 Deputy를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="db942-125">**To add Deputy from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="db942-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db942-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="db942-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="db942-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="db942-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="db942-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="db942-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db942-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="db942-133">검색 상자에 **Deputy**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="db942-133">In the search box, type **Deputy**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_search.png)

5. <span data-ttu-id="db942-135">결과 패널에서 **Deputy**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="db942-135">In the results panel, select **Deputy**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="db942-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="db942-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="db942-138">이 섹션에서는 “Britta Simon”이라는 테스트 사용자를 기반으로 Deputy에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="db942-138">In this section, you configure and test Azure AD single sign-on with Deputy based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="db942-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Deputy 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db942-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Deputy is to a user in Azure AD.</span></span> <span data-ttu-id="db942-140">즉, Azure AD 사용자와 Deputy의 관련 사용자 간에 연결 관계가 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db942-140">In other words, a link relationship between an Azure AD user and the related user in Deputy needs to be established.</span></span>

<span data-ttu-id="db942-141">Deputy에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="db942-141">In Deputy, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="db942-142">Deputy에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db942-142">To configure and test Azure AD single sign-on with Deputy, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="db942-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="db942-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="db942-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="db942-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="db942-145">**[Deputy 테스트 사용자 만들기](#creating-a-deputy-test-user)** - Azure AD 표현과 연결된 Deputy의 Britta Simon에 해당하는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="db942-145">**[Creating a Deputy test user](#creating-a-deputy-test-user)** - to have a counterpart of Britta Simon in Deputy that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="db942-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="db942-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="db942-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="db942-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="db942-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="db942-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="db942-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Deputy 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="db942-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Deputy application.</span></span>

<span data-ttu-id="db942-150">**Deputy에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="db942-150">**To configure Azure AD single sign-on with Deputy, perform the following steps:**</span></span>

1. <span data-ttu-id="db942-151">Azure Portal의 **Deputy** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db942-151">In the Azure portal, on the **Deputy** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="db942-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="db942-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_samlbase.png)

3. <span data-ttu-id="db942-155">**Deputy 도메인 및 URL** 섹션에서 **IDP 시작 모드**로 응용 프로그램을 구성하려는 경우 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="db942-155">On the **Deputy Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_url1.png)

    <span data-ttu-id="db942-157">a.</span><span class="sxs-lookup"><span data-stu-id="db942-157">a.</span></span> <span data-ttu-id="db942-158">**식별자** 텍스트 상자에서 다음 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="db942-158">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    |  |
    | ----|
    | `https://<subdomain>.<region>.au.deputy.com` |
    | `https://<subdomain>.<region>.ent-au.deputy.com` |
    | `https://<subdomain>.<region>.na.deputy.com`|
    | `https://<subdomain>.<region>.ent-na.deputy.com`|
    | `https://<subdomain>.<region>.eu.deputy.com` |
    | `https://<subdomain>.<region>.ent-eu.deputy.com` |
    | `https://<subdomain>.<region>.as.deputy.com` |
    | `https://<subdomain>.<region>.ent-as.deputy.com` |
    | `https://<subdomain>.<region>.la.deputy.com` |
    | `https://<subdomain>.<region>.ent-la.deputy.com` |
    | `https://<subdomain>.<region>.af.deputy.com` |
    | `https://<subdomain>.<region>.ent-af.deputy.com` |
    | `https://<subdomain>.<region>.an.deputy.com` |
    | `https://<subdomain>.<region>.ent-an.deputy.com` |
    | `https://<subdomain>.<region>.deputy.com` |

    <span data-ttu-id="db942-159">b.</span><span class="sxs-lookup"><span data-stu-id="db942-159">b.</span></span> <span data-ttu-id="db942-160">**회신 URL** 텍스트 상자에 다음 패턴으로 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="db942-160">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |----|
    | `https://<subdomain>.<region>.au.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-au.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.na.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-na.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.eu.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-eu.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.as.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-as.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.la.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-la.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.af.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-af.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.an.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-an.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.deputy.com/exec/devapp/samlacs.` |

4. <span data-ttu-id="db942-161">**고급 URL 설정 표시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="db942-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="db942-162">**SP** 시작 모드에서 응용 프로그램을 구성하려면:</span><span class="sxs-lookup"><span data-stu-id="db942-162">If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_url2.png)

    <span data-ttu-id="db942-164">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<your-subdomain>.<region>.deputy.com`</span><span class="sxs-lookup"><span data-stu-id="db942-164">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<your-subdomain>.<region>.deputy.com`</span></span>
    
    >[!NOTE]
    > <span data-ttu-id="db942-165">Deputy 지역 접미사는 선택 사항이거나 au | na | eu |as |la |af |an |ent-au |ent-na |ent-eu |ent-as | ent-la | ent-af | ent-an 중 하나를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db942-165">Deputy region suffix is optional, or it should use one of these: au | na | eu |as |la |af |an |ent-au |ent-na |ent-eu |ent-as | ent-la | ent-af | ent-an</span></span>

    > [!NOTE] 
    > <span data-ttu-id="db942-166">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="db942-166">These values are not real.</span></span> <span data-ttu-id="db942-167">이러한 값을 실제 식별자, 회신 URL 및 로그온 URL로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="db942-167">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="db942-168">이러한 값을 얻으려면 [Deputy 지원 팀](https://www.deputy.com/call-centers-customer-support-scheduling-software)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="db942-168">Contact [Deputy support team](https://www.deputy.com/call-centers-customer-support-scheduling-software) to get these values.</span></span> 

5. <span data-ttu-id="db942-169">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="db942-169">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_certificate.png) 

6. <span data-ttu-id="db942-171">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db942-171">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-deputy-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="db942-173">**Deputy 구성** 섹션에서 **Deputy 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="db942-173">On the **Deputy Configuration** section, click **Configure Deputy** to open **Configure sign-on** window.</span></span> <span data-ttu-id="db942-174">**빠른 참조 섹션**에서 **SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="db942-174">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_configure.png) 

8. <span data-ttu-id="db942-176">다음 URL, [https://(your-subdomain).deputy.com/exec/config/system_config]( https://(your-subdomain).deputy.com/exec/config/system_config)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="db942-176">Navigate to the following URL:[https://(your-subdomain).deputy.com/exec/config/system_config]( https://(your-subdomain).deputy.com/exec/config/system_config).</span></span> <span data-ttu-id="db942-177">**보안 설정**으로 이동하고 **편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db942-177">Go to **Security Settings** and click **Edit**.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_004.png)

9. <span data-ttu-id="db942-179">이 **보안 설정** 페이지에서 아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="db942-179">On this **Security Settings** page, perform below steps.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_005.png)
    
    <span data-ttu-id="db942-181">a.</span><span class="sxs-lookup"><span data-stu-id="db942-181">a.</span></span> <span data-ttu-id="db942-182">**소셜 로그인**을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="db942-182">Enable **Social Login**.</span></span>
   
    <span data-ttu-id="db942-183">b.</span><span class="sxs-lookup"><span data-stu-id="db942-183">b.</span></span> <span data-ttu-id="db942-184">Azure Portal에서 다운로드한 Base64로 인코딩된 인증서를 메모장에서 열고, 내용을 클립보드에 복사한 다음 **OpenSSL 인증서** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="db942-184">Open your Base64 encoded certificate downloaded from Azure portal in notepad, copy the content of it into your clipboard, and then paste it to the **OpenSSL Certificate** textbox.</span></span>
   
    <span data-ttu-id="db942-185">c.</span><span class="sxs-lookup"><span data-stu-id="db942-185">c.</span></span> <span data-ttu-id="db942-186">SAML SSO URL 텍스트 상자에 `https://<your subdomain>.deputy.com/exec/devapp/samlacs?dpLoginTo=<saml sso url>`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="db942-186">In the SAML SSO URL textbox, type `https://<your subdomain>.deputy.com/exec/devapp/samlacs?dpLoginTo=<saml sso url>`</span></span>
    
    <span data-ttu-id="db942-187">d.</span><span class="sxs-lookup"><span data-stu-id="db942-187">d.</span></span> <span data-ttu-id="db942-188">SAML SSO URL 텍스트 상자에서 `<your subdomain>`를 하위 도메인으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="db942-188">In the SAML SSO URL textbox, replace `<your subdomain>` with your subdomain.</span></span>
   
    <span data-ttu-id="db942-189">e.</span><span class="sxs-lookup"><span data-stu-id="db942-189">e.</span></span> <span data-ttu-id="db942-190">SAML SSO URL 텍스트 상자에서 `<saml sso url>`을 Azure Portal에서 복사한 **SAML Single Sign-On 서비스 URL**로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="db942-190">In the SAML SSO URL textbox, replace `<saml sso url>` with the **SAML Single Sign-On Service URL** you have copied from the Azure portal.</span></span>
   
    <span data-ttu-id="db942-191">f.</span><span class="sxs-lookup"><span data-stu-id="db942-191">f.</span></span> <span data-ttu-id="db942-192">**설정 저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db942-192">Click **Save Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="db942-193">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db942-193">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="db942-194">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="db942-194">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="db942-195">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db942-195">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="db942-196">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="db942-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="db942-197">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="db942-197">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="db942-199">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="db942-199">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="db942-200">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db942-200">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-deputy-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="db942-202">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db942-202">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-deputy-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="db942-204">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db942-204">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-deputy-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="db942-206">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="db942-206">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-deputy-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="db942-208">a.</span><span class="sxs-lookup"><span data-stu-id="db942-208">a.</span></span> <span data-ttu-id="db942-209">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="db942-209">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="db942-210">b.</span><span class="sxs-lookup"><span data-stu-id="db942-210">b.</span></span> <span data-ttu-id="db942-211">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="db942-211">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="db942-212">c.</span><span class="sxs-lookup"><span data-stu-id="db942-212">c.</span></span> <span data-ttu-id="db942-213">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="db942-213">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="db942-214">d.</span><span class="sxs-lookup"><span data-stu-id="db942-214">d.</span></span> <span data-ttu-id="db942-215">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db942-215">Click **Create**.</span></span>
 
### <a name="creating-a-deputy-test-user"></a><span data-ttu-id="db942-216">Deputy 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="db942-216">Creating a Deputy test user</span></span>

<span data-ttu-id="db942-217">Azure AD 사용자가 Deputy에 로그인할 수 있도록 하려면 Deputy로 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db942-217">To enable Azure AD users to log in to Deputy, they must be provisioned into Deputy.</span></span> <span data-ttu-id="db942-218">Deputy의 경우 프로비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="db942-218">In case of Deputy, provisioning is a manual task.</span></span>

#### <a name="to-provision-a-user-account-perform-the-following-steps"></a><span data-ttu-id="db942-219">사용자 계정을 프로비저닝하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="db942-219">To provision a user account, perform the following steps:</span></span>
1. <span data-ttu-id="db942-220">Deputy 회사 사이트에 관리자 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="db942-220">Log in to your Deputy company site as an administrator.</span></span>

2. <span data-ttu-id="db942-221">탐색 창 상단에서 **사람**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db942-221">On the top navigation pane, click **People**.</span></span>
   
   <span data-ttu-id="db942-222">![사람](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_001.png "사람")</span><span class="sxs-lookup"><span data-stu-id="db942-222">![People](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_001.png "People")</span></span>

3. <span data-ttu-id="db942-223">**구성원 추가** 단추를 클릭하고 **단일 구성원 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db942-223">Click the **Add People** button and click **Add a single person**.</span></span>
   
   <span data-ttu-id="db942-224">![피플 추가](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_002.png "피플 추가")</span><span class="sxs-lookup"><span data-stu-id="db942-224">![Add People](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_002.png "Add People")</span></span>

4. <span data-ttu-id="db942-225">다음 단계를 수행하고 **저장 및 초대**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db942-225">Perform the following steps and click **Save & Invite**.</span></span>
   
   <span data-ttu-id="db942-226">![새 사용자](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_003.png "새 사용자")</span><span class="sxs-lookup"><span data-stu-id="db942-226">![New User](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_003.png "New User")</span></span>

   <span data-ttu-id="db942-227">a.</span><span class="sxs-lookup"><span data-stu-id="db942-227">a.</span></span> <span data-ttu-id="db942-228">**이름** 텍스트 상자에 사용자의 이름(예: **BrittaSimon**)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="db942-228">In the **Name** textbox, type name of the user like **BrittaSimon**.</span></span>
   
   <span data-ttu-id="db942-229">b.</span><span class="sxs-lookup"><span data-stu-id="db942-229">b.</span></span> <span data-ttu-id="db942-230">**전자 메일** 텍스트 상자에 프로비전하려는 Azure AD 계정의 전자 메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="db942-230">In the **Email** textbox, type the email address of an Azure AD account you want to provision.</span></span>
   
   <span data-ttu-id="db942-231">c.</span><span class="sxs-lookup"><span data-stu-id="db942-231">c.</span></span> <span data-ttu-id="db942-232">**작업 위치** 텍스트 상자에 비즈니스 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="db942-232">In the **Work at** textbox, type the business name.</span></span>
   
   <span data-ttu-id="db942-233">d.</span><span class="sxs-lookup"><span data-stu-id="db942-233">d.</span></span> <span data-ttu-id="db942-234">**저장 및 초대** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db942-234">Click **Save & Invite** button.</span></span>

5. <span data-ttu-id="db942-235">AAD 계정 보유자에게 전자 메일이 발송되며 여기에 포함된 링크를 클릭하여 계정을 확인하면 계정이 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="db942-235">The AAD account holder receives an email and follows a link to confirm their account before it becomes active.</span></span> <span data-ttu-id="db942-236">다른 Deputy 사용자 계정 생성 도구 또는 Deputy가 제공한 API를 사용하여 AAD 사용자 계정을 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db942-236">You can use any other Deputy user account creation tools or APIs provided by Deputy to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="db942-237">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="db942-237">Assigning the Azure AD test user</span></span>

<span data-ttu-id="db942-238">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Deputy에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="db942-238">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Deputy.</span></span>

![사용자 할당][200] 

<span data-ttu-id="db942-240">**Britta Simon을 Deputy에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="db942-240">**To assign Britta Simon to Deputy, perform the following steps:**</span></span>

1. <span data-ttu-id="db942-241">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db942-241">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="db942-243">응용 프로그램 목록에서 **Deputy**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="db942-243">In the applications list, select **Deputy**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_app.png) 

3. <span data-ttu-id="db942-245">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db942-245">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="db942-247">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db942-247">Click **Add** button.</span></span> <span data-ttu-id="db942-248">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="db942-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="db942-250">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="db942-250">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="db942-251">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db942-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="db942-252">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db942-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="db942-253">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="db942-253">Testing single sign-on</span></span>

<span data-ttu-id="db942-254">이 섹션은 액세스 패널을 사용하여 Azure AD SSO 구성을 테스트하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="db942-254">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="db942-255">액세스 패널에서 Deputy 타일을 클릭하면 Deputy 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="db942-255">When you click the Deputy tile in the Access Panel, you should get automatically signed-on to your Deputy application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="db942-256">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="db942-256">Additional resources</span></span>

* [<span data-ttu-id="db942-257">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="db942-257">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="db942-258">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="db942-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_203.png

