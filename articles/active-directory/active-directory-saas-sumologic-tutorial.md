---
title: "자습서: SumoLogic과 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory 및 SumoLogic 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: fbb76765-92d7-4801-9833-573b11b4d910
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: e739106472ccf930b2942eb810dd844f2b1ade7c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sumologic"></a><span data-ttu-id="3ef44-103">자습서: SumoLogic과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="3ef44-103">Tutorial: Azure Active Directory integration with SumoLogic</span></span>

<span data-ttu-id="3ef44-104">이 자습서에서는 Azure AD(Azure Active Directory)와 SumoLogic을 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-104">In this tutorial, you learn how to integrate SumoLogic with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3ef44-105">SumoLogic과 Azure AD를 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-105">Integrating SumoLogic with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3ef44-106">SumoLogic에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-106">You can control in Azure AD who has access to SumoLogic</span></span>
- <span data-ttu-id="3ef44-107">사용자가 해당 Azure AD 계정으로 SumoLogic(Single Sign-on)에 자동으로 로그인하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-107">You can enable your users to automatically get signed-on to SumoLogic (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3ef44-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="3ef44-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3ef44-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3ef44-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="3ef44-110">Prerequisites</span></span>

<span data-ttu-id="3ef44-111">SumoLogic과 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-111">To configure Azure AD integration with SumoLogic, you need the following items:</span></span>

- <span data-ttu-id="3ef44-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="3ef44-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3ef44-113">SumoLogic Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="3ef44-113">A SumoLogic single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3ef44-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3ef44-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3ef44-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="3ef44-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3ef44-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3ef44-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="3ef44-118">Scenario description</span></span>
<span data-ttu-id="3ef44-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3ef44-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3ef44-121">갤러리에서 SumoLogic 추가</span><span class="sxs-lookup"><span data-stu-id="3ef44-121">Adding SumoLogic from the gallery</span></span>
2. <span data-ttu-id="3ef44-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="3ef44-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sumologic-from-the-gallery"></a><span data-ttu-id="3ef44-123">갤러리에서 SumoLogic 추가</span><span class="sxs-lookup"><span data-stu-id="3ef44-123">Adding SumoLogic from the gallery</span></span>
<span data-ttu-id="3ef44-124">SumoLogic의 Azure AD 통합을 구성하려면 갤러리의 SumoLogic을 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-124">To configure the integration of SumoLogic into Azure AD, you need to add SumoLogic from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3ef44-125">**갤러리에서 SumoLogic을 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="3ef44-125">**To add SumoLogic from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3ef44-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3ef44-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3ef44-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="3ef44-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="3ef44-133">검색 상자에 **SumoLogic**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-133">In the search box, type **SumoLogic**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_search.png)

5. <span data-ttu-id="3ef44-135">결과 패널에서 **SumoLogic**을 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-135">In the results panel, select **SumoLogic**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3ef44-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="3ef44-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3ef44-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 SumoLogic에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-138">In this section, you configure and test Azure AD single sign-on with SumoLogic based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3ef44-139">Single Sign-On이 작동하려면 Azure AD 사용자에 해당하는 SumoLogic 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SumoLogic is to a user in Azure AD.</span></span> <span data-ttu-id="3ef44-140">즉, Azure AD 사용자와 SumoLogic의 관련 사용자 간에 연결 관계가 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-140">In other words, a link relationship between an Azure AD user and the related user in SumoLogic needs to be established.</span></span>

<span data-ttu-id="3ef44-141">SumoLogic에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 연결 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-141">In SumoLogic, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="3ef44-142">SumoLogic에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-142">To configure and test Azure AD single sign-on with SumoLogic, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3ef44-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3ef44-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3ef44-145">**[SumoLogic 테스트 사용자 만들기](#creating-a-sumologic-test-user)** - Britta Simon의 Azure AD 표현과 연결되는 대응 사용자를 SumoLogic에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-145">**[Creating a SumoLogic test user](#creating-a-sumologic-test-user)** - to have a counterpart of Britta Simon in SumoLogic that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3ef44-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3ef44-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3ef44-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="3ef44-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3ef44-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 SumoLogic 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SumoLogic application.</span></span>

<span data-ttu-id="3ef44-150">**SumoLogic에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="3ef44-150">**To configure Azure AD single sign-on with SumoLogic, perform the following steps:**</span></span>

1. <span data-ttu-id="3ef44-151">Azure Portal의 **SumoLogic** 응용 프로그램 통합 페이지에서 **Single sign-on**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-151">In the Azure portal, on the **SumoLogic** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="3ef44-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_samlbase.png)

3. <span data-ttu-id="3ef44-155">**SumoLogic 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-155">On the **SumoLogic Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_url.png)

    <span data-ttu-id="3ef44-157">a.</span><span class="sxs-lookup"><span data-stu-id="3ef44-157">a.</span></span> <span data-ttu-id="3ef44-158">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<tenantname>.SumoLogic.com`</span><span class="sxs-lookup"><span data-stu-id="3ef44-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenantname>.SumoLogic.com`</span></span>

    <span data-ttu-id="3ef44-159">b.</span><span class="sxs-lookup"><span data-stu-id="3ef44-159">b.</span></span> <span data-ttu-id="3ef44-160">**식별자** 텍스트 상자에서 다음 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<tenantname>.us2.sumologic.com` |
    | `https://<tenantname>.sumologic.com` |
    | `https://<tenantname>.us4.sumologic.com` |
    | `https://<tenantname>.eu.sumologic.com` |
    | `https://<tenantname>.au.sumologic.com` |

    > [!NOTE] 
    > <span data-ttu-id="3ef44-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-161">These values are not real.</span></span> <span data-ttu-id="3ef44-162">실제 로그온 URL 및 식별자로 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="3ef44-163">이러한 값을 얻으려면 [SumoLogic 클라이언트 지원 팀](https://www.sumologic.com/contact-us/)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="3ef44-163">Contact [SumoLogic Client support team](https://www.sumologic.com/contact-us/) to get these values.</span></span> 
 
4. <span data-ttu-id="3ef44-164">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_certificate.png) 

5. <span data-ttu-id="3ef44-166">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-166">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-sumologic-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3ef44-168">**SumoLogic 구성** 섹션에서 **SumoLogic 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-168">On the **SumoLogic Configuration** section, click **Configure SumoLogic** to open **Configure sign-on** window.</span></span> <span data-ttu-id="3ef44-169">**빠른 참조 섹션**에서 **SAML 엔터티 ID 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-169">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_configure.png) 

7. <span data-ttu-id="3ef44-171">다른 웹 브라우저 창에서 SumoLogic 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-171">In a different web browser window, log in to your SumoLogic company site as an administrator.</span></span>

8. <span data-ttu-id="3ef44-172">**관리 \> 보안**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-172">Go to **Manage \> Security**.</span></span>
   
    <span data-ttu-id="3ef44-173">![관리](./media/active-directory-saas-sumologic-tutorial/ic778556.png "관리")</span><span class="sxs-lookup"><span data-stu-id="3ef44-173">![Manage](./media/active-directory-saas-sumologic-tutorial/ic778556.png "Manage")</span></span>

9. <span data-ttu-id="3ef44-174">**SAML**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-174">Click **SAML**.</span></span>
   
    <span data-ttu-id="3ef44-175">![전역 보안 설정](./media/active-directory-saas-sumologic-tutorial/ic778557.png "전역 보안 설정")</span><span class="sxs-lookup"><span data-stu-id="3ef44-175">![Global security settings](./media/active-directory-saas-sumologic-tutorial/ic778557.png "Global security settings")</span></span>

10. <span data-ttu-id="3ef44-176">**구성 선택 또는 새로 만들기** 목록에서 **Azure AD**를 선택하고 **구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-176">From the **Select a configuration or create a new one** list, select **Azure AD**, and then click **Configure**.</span></span>
   
    <span data-ttu-id="3ef44-177">![SAML 2.0 구성](./media/active-directory-saas-sumologic-tutorial/ic778558.png "SAML 2.0 구성")</span><span class="sxs-lookup"><span data-stu-id="3ef44-177">![Configure SAML 2.0](./media/active-directory-saas-sumologic-tutorial/ic778558.png "Configure SAML 2.0")</span></span>

11. <span data-ttu-id="3ef44-178">**SAML 2.0 구성** 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-178">On the **Configure SAML 2.0** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="3ef44-179">![SAML 2.0 구성](./media/active-directory-saas-sumologic-tutorial/ic778559.png "SAML 2.0 구성")</span><span class="sxs-lookup"><span data-stu-id="3ef44-179">![Configure SAML 2.0](./media/active-directory-saas-sumologic-tutorial/ic778559.png "Configure SAML 2.0")</span></span>
   
    <span data-ttu-id="3ef44-180">a.</span><span class="sxs-lookup"><span data-stu-id="3ef44-180">a.</span></span> <span data-ttu-id="3ef44-181">**구성 이름** 텍스트 상자에 **Azure AD**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-181">In the **Configuration Name** textbox, type **Azure AD**.</span></span> 

    <span data-ttu-id="3ef44-182">b.</span><span class="sxs-lookup"><span data-stu-id="3ef44-182">b.</span></span> <span data-ttu-id="3ef44-183">**디버그 모드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-183">Select **Debug Mode**.</span></span>

    <span data-ttu-id="3ef44-184">c.</span><span class="sxs-lookup"><span data-stu-id="3ef44-184">c.</span></span> <span data-ttu-id="3ef44-185">Azure Portal에서 복사한 **SAML 엔터티 ID** 값을 **발급자** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-185">In the **Issuer** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="3ef44-186">d.</span><span class="sxs-lookup"><span data-stu-id="3ef44-186">d.</span></span> <span data-ttu-id="3ef44-187">Azure Portal에서 복사한 **SAML Single Sign-On 서비스 URL** 값을 **Authn 요청 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-187">In the **Authn Request URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="3ef44-188">e.</span><span class="sxs-lookup"><span data-stu-id="3ef44-188">e.</span></span> <span data-ttu-id="3ef44-189">Base 64로 인코딩된 인증서를 메모장에서 열고, 내용을 클립보드에 복사한 다음 전체 인증서를 **X.509 인증서** 텍스트 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-189">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste the entire Certificate into **X.509 Certificate** textbox.</span></span>

    <span data-ttu-id="3ef44-190">f.</span><span class="sxs-lookup"><span data-stu-id="3ef44-190">f.</span></span> <span data-ttu-id="3ef44-191">**이메일 속성**에서는 **SAML 제목 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-191">As **Email Attribute**, select **Use SAML subject**.</span></span>  

    <span data-ttu-id="3ef44-192">g.</span><span class="sxs-lookup"><span data-stu-id="3ef44-192">g.</span></span> <span data-ttu-id="3ef44-193">**SP 시작 로그인 구성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-193">Select **SP initiated Login Configuration**.</span></span>

    <span data-ttu-id="3ef44-194">h.</span><span class="sxs-lookup"><span data-stu-id="3ef44-194">h.</span></span> <span data-ttu-id="3ef44-195">**로그인 경로** 텍스트 상자에 **Azure**를 입력하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-195">In the **Login Path** textbox, type **Azure** and click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="3ef44-196">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-196">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3ef44-197">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-197">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3ef44-198">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-198">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3ef44-199">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="3ef44-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="3ef44-200">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-200">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="3ef44-202">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="3ef44-202">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3ef44-203">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-203">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sumologic-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3ef44-205">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-205">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sumologic-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3ef44-207">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-207">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sumologic-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3ef44-209">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-209">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sumologic-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3ef44-211">a.</span><span class="sxs-lookup"><span data-stu-id="3ef44-211">a.</span></span> <span data-ttu-id="3ef44-212">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-212">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3ef44-213">b.</span><span class="sxs-lookup"><span data-stu-id="3ef44-213">b.</span></span> <span data-ttu-id="3ef44-214">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-214">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3ef44-215">c.</span><span class="sxs-lookup"><span data-stu-id="3ef44-215">c.</span></span> <span data-ttu-id="3ef44-216">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-216">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="3ef44-217">d.</span><span class="sxs-lookup"><span data-stu-id="3ef44-217">d.</span></span> <span data-ttu-id="3ef44-218">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-218">Click **Create**.</span></span>
 
### <a name="creating-a-sumologic-test-user"></a><span data-ttu-id="3ef44-219">SumoLogic 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="3ef44-219">Creating a SumoLogic test user</span></span>

<span data-ttu-id="3ef44-220">Azure AD 사용자가 SumoLogic에 로그인할 수 있도록 하려면 SumoLogic으로 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-220">In order to enable Azure AD users to log in to SumoLogic, they must be provisioned to SumoLogic.</span></span>  

* <span data-ttu-id="3ef44-221">SumoLogic의 경우 프로비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-221">In the case of SumoLogic, provisioning is a manual task.</span></span>

<span data-ttu-id="3ef44-222">**사용자 계정을 프로비전하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="3ef44-222">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="3ef44-223">자신의 **SumoLogic** 테넌트에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-223">Log in to your **SumoLogic** tenant.</span></span>

2. <span data-ttu-id="3ef44-224">**\> 사용자 관리**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-224">Go to **Manage \> Users**.</span></span>
   
    <span data-ttu-id="3ef44-225">![사용자](./media/active-directory-saas-sumologic-tutorial/ic778561.png "사용자")</span><span class="sxs-lookup"><span data-stu-id="3ef44-225">![Users](./media/active-directory-saas-sumologic-tutorial/ic778561.png "Users")</span></span>

3. <span data-ttu-id="3ef44-226">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-226">Click **Add**.</span></span>
   
    <span data-ttu-id="3ef44-227">![사용자](./media/active-directory-saas-sumologic-tutorial/ic778562.png "사용자")</span><span class="sxs-lookup"><span data-stu-id="3ef44-227">![Users](./media/active-directory-saas-sumologic-tutorial/ic778562.png "Users")</span></span>

4. <span data-ttu-id="3ef44-228">**새 사용자** 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-228">On the **New User** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="3ef44-229">![새 사용자](./media/active-directory-saas-sumologic-tutorial/ic778563.png "새 사용자")</span><span class="sxs-lookup"><span data-stu-id="3ef44-229">![New User](./media/active-directory-saas-sumologic-tutorial/ic778563.png "New User")</span></span> 
 
    <span data-ttu-id="3ef44-230">a.</span><span class="sxs-lookup"><span data-stu-id="3ef44-230">a.</span></span> <span data-ttu-id="3ef44-231">프로비전하려는 Azure AD 계정의 관련 정보를 **이름**, **성** 및 **전자 메일** 텍스트 상자에 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-231">Type the related information of the Azure AD account you want to provision into the **First Name**, **Last Name**, and **Email** textboxes.</span></span>
  
    <span data-ttu-id="3ef44-232">b.</span><span class="sxs-lookup"><span data-stu-id="3ef44-232">b.</span></span> <span data-ttu-id="3ef44-233">원하는 역할을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-233">Select a role.</span></span>
  
    <span data-ttu-id="3ef44-234">c.</span><span class="sxs-lookup"><span data-stu-id="3ef44-234">c.</span></span> <span data-ttu-id="3ef44-235">**상태**는 **활성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-235">As **Status**, select **Active**.</span></span>
  
    <span data-ttu-id="3ef44-236">ㄹ.</span><span class="sxs-lookup"><span data-stu-id="3ef44-236">d.</span></span> <span data-ttu-id="3ef44-237">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-237">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="3ef44-238">다른 SumoLogic 사용자 계정 생성 도구 또는 SumoLogic이 제공한 API를 사용하여 AAD 사용자 계정을 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-238">You can use any other SumoLogic user account creation tools or APIs provided by SumoLogic to provision AAD user accounts.</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="3ef44-239">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="3ef44-239">Assigning the Azure AD test user</span></span>

<span data-ttu-id="3ef44-240">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 SumoLogic에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-240">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SumoLogic.</span></span>

![사용자 할당][200] 

<span data-ttu-id="3ef44-242">**Britta Simon을 SumoLogic에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="3ef44-242">**To assign Britta Simon to SumoLogic, perform the following steps:**</span></span>

1. <span data-ttu-id="3ef44-243">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-243">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="3ef44-245">응용 프로그램 목록에서 **SumoLogic**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-245">In the applications list, select **SumoLogic**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_app.png) 

3. <span data-ttu-id="3ef44-247">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-247">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="3ef44-249">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-249">Click **Add** button.</span></span> <span data-ttu-id="3ef44-250">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="3ef44-252">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-252">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3ef44-253">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3ef44-254">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3ef44-255">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="3ef44-255">Testing single sign-on</span></span>

<span data-ttu-id="3ef44-256">이 섹션은 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-256">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="3ef44-257">액세스 패널에서 SumoLogic 타일을 클릭하면 SumoLogic 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="3ef44-257">When you click the SumoLogic tile in the Access Panel, you should get automatically signed-on to your SumoLogic application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3ef44-258">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="3ef44-258">Additional resources</span></span>

* [<span data-ttu-id="3ef44-259">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="3ef44-259">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3ef44-260">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="3ef44-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_203.png

